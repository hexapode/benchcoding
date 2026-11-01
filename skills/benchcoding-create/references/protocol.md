# Benchcoding experiment protocol

Use this contract for code, designs, configurations, datasets, prompts, and product variants. Preserve ownership, immutable candidate identity, independent evaluation, budgets, and evidence history. Adapt storage, execution, and presentation to the objective; a numeric leaderboard is optional.

## Ownership and infrastructure

A named engineer owns the objective, budget, and acceptance decision. Name the domain reviewers and the team that will maintain accepted work. Contributors propose experiments; authorized evaluators produce evidence; a trusted publisher records it. A contributor cannot certify their own result or rewrite acceptance rules.

Reuse existing experiment platforms, analytics, artifact storage, review tools, and evaluation services. GitHub/GitLab and a Python controller are defaults for repository-based pilots, not requirements. Document an equivalent invocation and evidence boundary when choosing another stack. Do not build services the selected evaluation mode does not need.

Suggested repository layout:

```text
AGENTS.md
skills/benchcoding-contribute/SKILL.md
skills/benchcoding-maintain/SKILL.md
skills/benchcoding-create/references/{protocol,evaluation-modes}.md
leaderboard/README.md                # collaboration and validation guide
leaderboard/objective.yaml
leaderboard/board.md                 # evidence/status view, optionally ranked
leaderboard/submissions/             # or authorized external request store
leaderboard/results/                 # or durable protected evidence store
leaderboard/experiments/             # or linked issues
validation/                         # adapters, ingestion, renderer, tests as needed
```

Copy provider references only when used. If contributors can edit the source, authoritative requests, evaluation configuration, and evidence need a separately restricted store or an enforced protected review path. A directory name is not isolation. Restricted acceptance inputs and answers must remain outside contributor access.

## Objective contract

Declare actual values and explicitly mark fields that do not apply, with a reason. Do not fabricate metrics, datasets, or Git revisions to satisfy a schema.

| Field | Meaning |
| --- | --- |
| `schema_version`, `objective_id`, `objective_version` | Contract identity and revision. |
| `owner`, `reviewers`, `maintenance_team` | Accountable engineer, domain reviewers, and maintenance responsibility. |
| `visibility`, `allowed_contributors`, `data_policy` | Access, approved inputs, protected evidence, retention, and disclosure. |
| `evaluation_mode`, `evaluation_plan` | Offline, human review, live controlled, or hybrid; required stages, their dependencies, authorities, and completion rules. See [evaluation modes](evaluation-modes.md). |
| `baseline`, `candidate_types`, `allowed_changes` | Immutable baseline manifest, permitted artifact types, edit scope, and integration assumptions. |
| `metrics` | Zero or more measures with units, direction, aggregation, uncertainty, and minimum meaningful change. |
| `rubrics`, `gates`, `decision_policy` | Review criteria, mandatory constraints, and how evidence supports a decision. Define reviewer disagreement and tradeoff resolution. No numeric score is required for rubric-only work. |
| `evaluation_version`, `comparison_context` | Evaluation/rubric revision plus applicable workload, task set, environment, cohort, assignment, observation period, or study identity. |
| `measurement_protocol` | Applicable timing/repetition rules, review procedure, or study design. Include collection cutoffs, missing-data treatment, and stopping rules where needed. |
| `budget` | Per-experiment and total limits, payer, compute, wall time, review hours, concurrency, retries, and acceptance-query limits. |
| `submission_route`, `validation_route` | Registration, admission, evidence collection, review, and who may advance each state. |
| `rollout_policy` | Authorization and scope for live exposure, monitoring, pause/rollback, and promotion. Setup permission alone does not authorize exposure to users. |

For multiple metrics, specify gates and how tradeoffs are decided: for example an owner-reviewed comparison or a Pareto view. Never invent weights or flatten subjective judgments into a universal score. Keep unrelated objectives separate.

## Immutable candidates and experiments

An experiment groups attempts around a hypothesis. Preserve failed findings, costs, and attribution even when there is no submission.

Identify every baseline and candidate with a manifest: artifact type, approved source identity, immutable version or content digest, and relevant dependencies. Code uses a full commit ID; designs use a frozen export/version and digest; configurations, prompts, and datasets use versioned snapshots. Live variants also bind the deployed build, configuration, assignment definition, and exposure period. A mutable URL, branch, or screenshot of a changing deployment is insufficient. Restrict artifact access according to its data policy.

A submission contains experiment and contributor identities, payer, candidate and baseline manifests, objective/evaluation versions, hypothesis, allowed-change summary, reported development evidence, reproduction or review instructions, costs (including unknowns), and requested validation resources. Include any required live-exposure authorization separately.

Validate request identifiers and source allowlists, bound artifact sizes, and treat supplied paths/commands/content as untrusted data. Pin at admission; later source changes require a new candidate. If an admitted artifact disappears, report an error rather than substituting the current version. Do not fetch arbitrary contributor URLs with privileged credentials.

## Lifecycle and delayed work

Experiments: `proposed → funded → running → completed|stopped`. Findings-only experiments can complete without a submission.

Submissions begin `submitted → queued → evaluating`. Required stages may move into `awaiting_evidence` or `awaiting_review` and resume `evaluating` when the authorized evidence or review arrives. Each wait records the missing item, responsible party, due/check-in time, reserved budget, and next action. Persist these states outside a CI process; do not hold a runner open for weeks.

Evaluation outcomes:

- `verified`: evidence is complete and authentic, required gates passed, and the contract's evidentiary standard was met. This does not by itself mean an improvement or approval to ship.
- `rejected`: a candidate fails a required criterion, with evidence.
- `inconclusive`: the observation window closed or review completed without enough evidence to decide. Record uncertainty or unresolved disagreement; do not present it as a pass or an infrastructure error.
- `error`: infrastructure, provenance, or collection failed; retain diagnostics and actual costs.
- `stopped`: an authorized stop or predeclared budget/stopping rule ended the evaluation before completion.

`verified → accepted` requires the owner's recorded integration/product decision. `stale` marks evidence no longer eligible for the current comparison; `invalidated` records an evaluation flaw. Preserve events and reasons. New evidence after a terminal outcome requires an authorized follow-up attempt linked to the prior one; never silently overwrite it or keep sampling until a favorable answer appears.

A controller records trusted state transitions, including authenticated human decisions and approved external evidence. Only authorized reviewers can attest review stages. The publisher checks authority and provenance rather than trusting strings in candidate artifacts.

## Evaluation adapters

Implement only the adapters required by [the selected modes](evaluation-modes.md). The default repository CLI is:

```text
python3 validation/controller.py --submission-id ID --output result.json
```

Other implementations must provide equivalent documented dispatch/resume operations and structured state records. The controller must:

1. Load the admitted request from trusted storage and validate identity, versions, stage dependencies, authorization, and budget. Reserve resources atomically and use durable attempt/event keys to prevent duplicate dispatch or exposure.
2. Resolve the pinned artifacts. Keep source-access credentials outside candidate execution. Guard artifact transfers against path traversal and symlinks.
3. Execute, route for review, or ingest external observations according to the plan. When executing untrusted code, use an ephemeral isolated worker/service with enforced limits, no controller credentials or writable evaluator/results, and restricted network/filesystem. Builds are untrusted execution too; do not expose a host Docker socket or use a privileged shared runner as the candidate boundary.
4. Keep acceptance computation, protected answers, and reviewer attestations outside candidate control. Human reviewers receive the agreed task/rubric and pinned materials; live collectors bind observations to the approved variant, cohort, and time window. Candidate-reported scores are never authoritative.
5. Capture required evidence and costs, then evaluate stage completion. Persist pending states without certifying success. Baseline replay applies to repeatable offline tests; live studies use their declared comparator, and human reviews use their agreed baseline materials and tasks.
6. Emit a schema-validated state record even when work is pending or unsuccessful, where safe. For the default CLI, use exit zero for a successfully recorded `verified`, `awaiting_evidence`, `awaiting_review`, or `inconclusive` state; use nonzero for rejection, stopped execution, or infrastructure failure. Document equivalent semantics for other adapters. In all cases the ingestion layer checks the record's state and required stages: a green job is never enough to certify a candidate.

A process killed without a trustworthy state record produces an infrastructure error. Reconcile reservations after a crash or expired lease. Track elapsed study duration separately from active compute/reviewer spend; waiting does not justify charging an idle runner. Use bounded retries. A serialized pilot may use a durable owner-managed ledger; CI concurrency alone does not enforce money or exposure limits.

## Evidence and board views

Trusted records include schema version; submission/attempt/stage identity; candidate and baseline manifests; contract/evaluation versions and comparison context; producing evaluator or reviewer identity; trusted run/event provenance; timestamps and state; applicable metrics with sample sizes and uncertainty, rubric judgments, and required gate results; actual/unknown costs; protected evidence references/digests; and reasons or pending next actions. For human review, record the rubric version, reviewer authority, decision, and rationale. For live studies, record assignment and observation versions, exposure interval, collection completeness, and the declared analysis.

Validate required fields by mode and stage. Pending evidence may be absent only when the record identifies what is missing. Reject malformed/nonfinite numeric values, invented authorities, mismatched artifact identities, and unrecognized states. Verify provenance against authenticated provider, reviewer, or service records, not contributor-provided identity strings. Store corrections as new events.

Show hypotheses, attempts, evidence, costs, ownership, and pending work for every objective. Rank only comparable verified/accepted results when the contract defines a meaningful ordering. The comparison context must explicitly establish compatibility; cohort IDs in a randomized study need not be identical, but assignment and analysis must justify comparison. Human rubric decisions and multi-objective tradeoffs can use side-by-side evidence without rankings. Uncertainty can leave candidates tied or unordered.

Changing a baseline, rubric, dataset, environment, or live study design creates a new comparison context. Replay where meaningful; otherwise mark prior evidence as historical and plan a new study. Do not pretend a past cohort can be replayed. Render contributor descriptions as text and publish only through an identity that does not execute candidate artifacts. Preserve evidence durably beyond CI artifact expiry.

## Readiness

Distinguish `scaffolded`, `locally validated`, and `operational`. Operational means the selected adapters, access controls, durable evidence, and board updates work in the destination; it does not mean the objective has improved. Exercise the selected mode with labeled fixtures: pass/fail for offline, authorized/unauthorized and conflicting reviews for human, or dispatch/wait/resume/stop for live. A dry run can validate orchestration without authorizing production exposure. Report real live integration, review, or data-access steps that remain untested; fixtures are not real study results.
