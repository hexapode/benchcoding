---
name: benchcoding-create
description: Create an internal benchmark leaderboard with an owned objective, contributor agent instructions, and independent entry validation using GitHub Actions or GitLab CI.
---

# Create a Benchcoding leaderboard

Use this skill when asked to start a leaderboard or turn an optimization objective into a shared agent experiment workflow. Work in the user's chosen destination. These instructions support local preparation and authorized remote setup; reading this skill does not itself authorize spending compute or publishing company data.

## Establish the contract

Inspect repository instructions, existing CI, evaluator code, and available provider tools first. Preserve existing workflows and contributor guidance. Infer what is already established; ask only for missing decisions that materially affect the setup:

- Objective, representative workload, metric direction and units, correctness/resource constraints.
- Named owner, reviewing team, maintenance owner, and allowed contributors.
- GitHub or GitLab host, organization/group, source repository and destination; internal/private visibility by default.
- Baseline revision, permissible code changes, data access, runner requirements.
- Experiment and validation budgets: money or compute, wall time, concurrency, retry limits, and human review capacity.

If the objective cannot be evaluated repeatably, help define an evaluation first; do not invent a score or correctness oracle. Never assume a numeric result, permission to access customer data, or access to specialized hardware.

Read [the protocol](references/protocol.md), then only the selected provider guide: [GitHub](references/github.md) or [GitLab](references/gitlab.md). They define evidence authority and the separation between candidate execution and the judge.

## Design validation with the human when needed

Draft the validation flow from existing tests, product requirements, and the objective. Show what the candidate may change, how it will be exercised, who or what judges the outcome, the acceptance gates, and what evidence reaches the board. Include a plausible improvement and a misleading result that must be rejected.

Ask the human owner for help when representative inputs, acceptable tradeoffs, success criteria, or review authority cannot be inferred. Offer a concrete draft and focused choices rather than asking them to design everything from scratch. For example: which document failures are unacceptable; which user tasks a redesign must support; how long a retention trial must run; or who performs a human review. Record agreed decisions in `leaderboard/objective.yaml` and explain the validation flow in `leaderboard/README.md`.

Validation may include human judgment or delayed product measurements. Implement the queue, evidence capture, and authorized review step where those are required; do not substitute an invented automatic score. Keep unresolved acceptance decisions explicit and affected submissions pending until resolved. Continue infrastructure and documentation work that does not depend on the missing answer. Do not activate an evaluator against guessed acceptance rules.

## Build the smallest complete loop

Build and test the infrastructure, not just a plan or copied templates. The deliverable includes executable validation orchestration, result storage and ingestion, budget tracking, a board renderer, provider integration, and the collaboration material needed by the next agent. Use existing project infrastructure where it already satisfies the contract. When access or an unresolved human decision blocks completion, finish the independent work and report the specific blocker.

1. Write `leaderboard/objective.yaml` using the contract fields in the protocol. Resolve setup placeholders before activation. Keep the development dataset distributable within its permitted audience and acceptance data outside candidate access.
2. Create `leaderboard/README.md` with local reproduction commands, how to register an experiment, request validation, interpret states, and contact the owner. Explain cost accounting and what is and is not measured. Include a collaboration guide covering how another agent finds open work, registers or claims a hypothesis, checks for duplicates, coordinates overlapping attempts, records costs and failures, hands off findings, and requests review. Identify the owner and escalation route for unclear evaluation rules.
3. Adapt [the contributor AGENTS template](assets/AGENTS.md.template) into the destination's `AGENTS.md`. Merge it into existing instructions rather than overwriting them. Copy the contribute and maintain skills plus the create skill's protocol/provider references into the destination, preserving `skills/` paths; exclude creation-only assets if unnecessary. Adapt those skills to the objective with real commands, submission and validation routes, budget rules, and handoff instructions. Keep shared definitions in the contract and guide, and link to them from the skills. Ensure the resulting repository works without a link back to a private source checkout.
4. Use [the experiment template](assets/experiment.md.template) for GitHub issue forms/templates or GitLab issue templates, and [the submission template](assets/submission.md.template) for PRs/MRs. Support findings-only experiments; not every run needs a PR/MR. Register a hypothesis before spending its allocated budget.
5. Implement the evaluation adapter described in the protocol. Include a baseline replay and a deliberately invalid candidate. Use a trusted controller to launch isolated candidate execution; never run submission build scripts directly in a privileged judge job.
6. Adapt the provider CI template to the actual runner and evaluator. Keep trusted workflow/configuration on a protected ref or separate validation repository. A first pilot can require an authorized owner to dispatch a registered submission. Do not add a public privileged comment-command bot by default.
7. Implement strict result ingestion and a deterministic Markdown/JSON board renderer. Only authenticated validation records can advance a score to verified. Render submitted descriptions as text, not executable markup. Partition rankings by the comparison key and retain rejected/stale experiments with explanations.
8. Configure the provider controls in its guide if remote setup is authorized and accessible. Otherwise produce the complete local changes and a precise list of remaining remote settings. Do not claim branch protection or CI activation without checking them.

## Verify before calling it ready

Run the baseline end to end, validate a valid candidate, and reject an invalid one. Exercise: evaluator/config edits in a submission; missing/nonfinite metrics; failed correctness gates; a stale evaluation version; a moved branch after submission; a duplicate dispatch; exhausted budget; and an execution timeout. Use a deliberately failing fixture if no real improvement exists, and label any synthetic successful candidate as a fixture rather than a performance claim.

Walk through the collaboration guide from a fresh contributor checkout using only the generated instructions and skills: discover an objective, register an experiment, run development evaluation, record a failed attempt and its cost, and prepare a pinned submission for the owner’s validation queue. Check that referenced commands and paths work and that no required setup placeholders remain. This walkthrough does not authorize additional agents, paid runs, or remote writes outside the user’s scope.

Check that public logs/artifacts expose neither hidden examples nor credentials, and that candidate execution cannot write the result record. Check permissions and trusted refs on the live provider when available. A locally successful harness does not prove hosted isolation or CI operation.

Report the objective, destination, owner, files created, verified local/hosted behavior, and exact remaining blockers. Distinguish `scaffolded`, `locally validated`, and `operational`. Include a copyable instruction for the next contributing agent. Do not auto-merge candidates or deploy production changes as part of setup.
