# Leaderboard protocol

This is the shared contract for generated boards. Adapt storage and metric details to the project while preserving the trust boundaries and lifecycle.

## Ownership and repository layout

A named engineer owns objective changes, budgets, and acceptance. A team owns the resulting production code. Contributors propose experiments; a trusted evaluator measures them; a publisher records verified evidence. These can be simple services or owner-operated workflows, but a candidate process cannot assume evaluator or publisher authority.

Suggested generated layout:

```text
AGENTS.md
skills/benchcoding-contribute/SKILL.md
skills/benchcoding-maintain/SKILL.md
skills/benchcoding-create/references/{protocol,github,gitlab}.md
leaderboard/README.md
leaderboard/objective.yaml
leaderboard/board.md                 # generated view
leaderboard/submissions/<id>.json    # owner-admitted immutable requests
leaderboard/results/<run-id>.json    # trusted append-only evidence
leaderboard/experiments/             # or linked provider issues
validation/controller.py            # trusted orchestration, never candidate code
validation/render_board.py
validation/tests/
```

If contributors can edit the code repository, keep authoritative requests/results and evaluator configuration in a separate protected control repository, or admit them only through a protected owner-reviewed branch. Files merely placed in a `validation/` directory are not isolated. Hidden holdouts never belong in a repository readable by contributors.

## Objective contract

Use machine-readable fields and document their actual values:

| Field | Required meaning |
| --- | --- |
| `schema_version`, `objective_id`, `objective_version` | Stable identity and explicit contract revision. |
| `owner`, `reviewers`, `maintenance_team` | Actual identities and responsibility. |
| `visibility`, `source_repository`, `allowed_contributors` | Provider host/project identity and data audience. |
| `baseline_revision` | Full immutable commit ID, never just a branch name. |
| `metric` | Name, units, minimize/maximize, aggregation, repetitions, noise/tie policy, and minimum meaningful improvement. |
| `gates` | Named correctness, completeness, resource, and behavioral constraints with thresholds and operators. |
| `evaluation_version`, `workload_version`, `environment_id` | Evaluator revision/digest, dataset identity without hidden content, and hardware/runtime class. |
| `measurement_protocol` | Warmup, timer boundaries, cache policy, synchronization, seeds policy, and comparable baseline replay. |
| `allowed_changes` | Scope of candidate edits and integration assumptions. |
| `budget` | Per-experiment and total validation limits, payer, timeouts, concurrency, retries, acceptance-query cap. |
| `data_policy` | Development inputs, holdout custodian, disclosure policy, artifact audience and retention. |
| `submission_route`, `validation_route` | How a contributor registers and how an authorized owner dispatches. |

If nondeterminism is material, define repeated trials and uncertainty before inspecting winners. An environmental drift check may invalidate a timing comparison even when CI passes. Define a retention period and durable storage for accepted evidence; expiring CI artifacts alone are insufficient for long-lived baselines.

## Experiment and submission

An experiment groups runs around a hypothesis. Preserve negative findings and attribution. A submission names one immutable candidate plus:

- Submission/experiment ID, contributor and payer, source repository, full candidate revision and baseline revision.
- Objective/evaluation versions, allowed-change summary, development results labeled `reported`.
- Harness/model/configuration, run IDs, reproduction instructions, costs and resource use, trace/evidence references.
- Requested validation allocation and known limitations.

Treat request fields as data. Validate identifiers, bound sizes, allowlist provider repository identities, and quote command arguments. Reject arbitrary fetch URLs and shell fragments. Pin once at admission; a later force-push must not alter the evaluated candidate. If that commit becomes unavailable, fail the run rather than fetching the new branch head.

## Lifecycle

Experiments: `proposed → funded → running → completed|stopped`. Completed experiments may have no submission.

Submissions: `submitted → queued → evaluating → verified|rejected|error`. `verified → accepted` requires integration review and owner decision. `stale` identifies evidence no longer eligible for the current cohort; `invalidated` records a discovered evaluation flaw. Retain prior events and reasons.

Only the trusted controller can issue verified/rejected evaluation evidence. The owner can accept or invalidate it with a recorded reason. A contributor may withdraw a candidate, but cannot erase its costs or history. Separate correctness rejection from infrastructure failure. Never publish an error as zero latency.

## Trusted evaluation adapter

The CI templates invoke this generated interface:

```text
python3 validation/controller.py --submission-id ID --output result.json
```

This is a contract to implement, not a supplied generic benchmark. The controller must:

1. Load an admitted request from trusted storage, validate versions and authorization, and reserve resources idempotently. In the starter pilot an owner admits a request via a protected commit before dispatch.
2. Fetch only the allowed repository at its pinned revision. Keep checkout credentials outside candidate execution and remove them from the exported source. Guard against path traversal and symlinks when transferring artifacts.
3. Build and execute the candidate in an ephemeral worker with enforced time/memory/CPU limits, no controller credentials, no write access to evaluator/results, and restricted network/filesystem. Do not give it a host Docker socket or shared privileged runner. Builds are untrusted execution too. A container on a privileged shared runner is not an adequate default boundary for arbitrary code; select and document an isolated runner/VM or evaluation service.
4. Keep correctness labels and score computation in the evaluator. Send only the necessary test input to the candidate process and compare its bounded output outside that process. Candidate-produced scores are never authoritative. Hidden cases necessarily reveal their current input to the program, so limit feedback and prevent persistence/exfiltration; a read-only mounted answer file is not hidden.
5. Replay the baseline and candidate under the declared measurement protocol. Record gates, raw/repeated measurements or protected references, environment identity, exit state, and actual costs. Never allow candidate files to overwrite controller output.
6. Write and schema-validate the trusted result. Exit nonzero on rejection, incomplete execution, or infrastructure failure, while retaining diagnostic evidence when safe. The publisher verifies run provenance and exit status before updating the board.

Budget reservation must be durable and atomic, with a maximum lease and reconciliation for killed jobs. A CI timeout alone is not a spending limit. No automatic retries without a bound. For a minimal pilot, serialize validation and use an owner-maintained reservation ledger; do not pretend job concurrency accounts for money.

## Result and ranking rules

A trusted record contains: schema version; submission ID; repository and candidate revision; baseline revision; objective/evaluation/workload versions; environment ID; controller revision; provider project/workflow/run/attempt identity; timestamps; terminal state; metrics with units and sample counts; every gate and its measured value/threshold; resource use and cost with currency or explicit unknown values; evidence URI/digest; and a reason for rejection/error. Evidence references must respect the workload's data policy.

Validate against a strict schema. Reject absent gates, unknown status values, NaN/infinity, type mismatches, unexpected versions, and missing provenance. Verify provenance via trusted provider/service identity, not strings supplied inside the candidate artifact. Record corrections as new events rather than overwriting evidence.

Rank only verified or accepted entries with all gates passing and identical `(objective_version, evaluation_version, workload_version, environment_id, baseline_revision, measurement_protocol)` comparison keys. Use the declared metric direction and tie/noise policy. Preserve the distinction between verified and integrated. Show reported results in a separate section. A new baseline creates a new cohort until eligible candidates are replayed.

Generate Markdown/JSON from trusted records, with code/evidence links, attribution, costs, and current state. Use a narrow publication identity in a separate job/service that does not execute candidate code. Avoid automatic HTML injection from experiment titles or arbitrary artifact links. Keep the company's discovery catalog separate from per-objective rankings.

## Readiness checks

Operational means a live provider run has evaluated a pinned baseline/candidate, rejected an invalid candidate, published provenance-checked evidence, and enforced the configured controls. Verify role separation with a contributor-level identity where feasible. Document any isolation assumptions that could not be tested. Synthetic demonstration data must never appear as a measured production result.
