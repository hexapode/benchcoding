---
name: benchcoding-create
description: Build an owned Benchcoding experiment workspace for software or product objectives, with independent automated, human, live, or hybrid evaluation and contributor agent instructions.
---

# Create a Benchcoding workspace

Use when asked to start a board or turn an objective into a shared agent experiment workflow. Work in the user's chosen destination. Reading this skill does not authorize spending compute, publishing company data, or exposing users to an experiment.

## Establish the objective and evaluation

Inspect destination instructions, existing evaluation/review tools, CI, analytics, and available integrations. Preserve existing workflows and contributor guidance. Infer established decisions; ask only for missing choices that materially affect setup:

- Objective, named engineer owner, domain reviewers, maintenance team, and permitted contributors.
- Candidate types and immutable baseline: code, designs, configurations, datasets, prompts, or live variants.
- Success evidence, required constraints, meaningful differences, and tradeoffs.
- Available data, approved audience, destination, and execution/review resources.
- Budget, payer, time limits, concurrency, retry limits, review capacity, and any live-exposure authority.

Read [evaluation modes](references/evaluation-modes.md) and select automated offline, human review, live controlled, or hybrid evaluation. Then read [the protocol](references/protocol.md). Choose infrastructure to fit that mode; GitHub/GitLab, Python, and numeric rankings are useful defaults for code benchmarks, not universal requirements. Read [GitHub](references/github.md) or [GitLab](references/gitlab.md) only when using that provider.

Draft the validation flow: permitted changes, collection/review steps, authorities, acceptance rules, and evidence on the board. Show a candidate that should pass, one that should fail, and one ambiguous case. Ask the human owner to resolve missing rules, representative inputs, tradeoffs, or judgment authority. Offer a concrete draft instead of asking them to design everything. Do not invent a score, sample size, or correctness oracle. Human or delayed evidence is legitimate evaluation.

Record decisions in `leaderboard/objective.yaml` and the validation guide, or equivalent existing project locations. Keep unresolved acceptance choices explicit, continue independent infrastructure work, and leave dependent evaluation pending until resolved. Existing authorization persists; do not impose redundant approval steps.

## Build the smallest complete loop

Build and test working infrastructure, not just a plan or copied templates. Reuse existing services where they satisfy the contract. Implement the selected adapters, durable evidence ingestion, budget accounting, an evidence/status board, and a collaboration handoff.

1. Write the objective contract with the mode, candidate manifest format, baseline, metrics/rubrics, gates, decision policy, stage plan, budgets, and comparison context. Mark inapplicable fields explicitly. Keep restricted acceptance material outside contributor access.
2. Create `leaderboard/README.md` describing the validation flow and collaboration routes. Explain how another agent finds work, registers/claims a hypothesis, avoids duplicate attempts, coordinates overlaps, records failures and costs, hands off findings, and requests evaluation. Include actual reproduction commands or review/study procedures, owner contacts, pending states, and escalation for unclear rules.
3. Merge [the AGENTS template](assets/AGENTS.md.template) into destination instructions. Copy and adapt the contribute/maintain skills and protocol/evaluation-mode references, plus provider guides when used. Preserve relative links: include referenced provider templates when copying those guides, or remove unused guide links from the generated skills. Replace code-only steps with applicable artifact, review, and study procedures; include real commands/routes and reference the shared contract. The next agent must be able to work from the destination alone.
4. Adapt [experiment](assets/experiment.md.template) and [submission](assets/submission.md.template) templates to the selected collaboration tools. Use issues/forms or equivalent records for non-code candidates; PRs/MRs are optional for changes that need code review. Register hypotheses and funding before spending the allocated budget. Preserve findings-only experiments.
5. Implement the mode-specific evaluation adapters. Offline code runs need isolated execution and baseline replay. Human review needs pinned materials, an authorized queue, and recorded judgments. Live experiments need approved dispatch, durable wait/resume, observation ingestion, analysis, and stop/rollback integration. Hybrid plans enforce prerequisites and all required stages. Keep acceptance decisions and evidence outside candidate control.
6. Integrate with the chosen provider/services. CI templates are optional starters for short dispatch/resume operations; adapt their command to the implementation and keep trusted configuration protected. Do not keep CI running while waiting for people or a study window. Green orchestration jobs must not certify pending, inconclusive, or partial evaluations. Configure remote controls only within authorized scope and verify effective settings.
7. Implement strict mode/stage-aware ingestion, append-only records, and a board view. Show ownership, hypotheses, pending actions, costs, evidence, and decisions. Rank only where the contract defines a valid ordering; support rubric reviews and multi-measure comparisons without a universal score. Keep rejected, inconclusive, and stale work visible with reasons.

## Verify readiness and handoff

Exercise the selected mode with labeled fixtures and realistic failure cases from the evaluation guide. Across modes check immutable identity, unauthorized evidence, duplicate events/dispatch, evaluator changes, version mismatch, budgets, and cost reconciliation. Test wait/resume and reviewer disagreement when applicable. A dry-run live study validates plumbing, not a product outcome or real-user authorization.

Walk through the collaboration guide from a fresh contributor workspace using only the generated instructions: find an objective, register an experiment, evaluate a draft using the permitted procedure, record a failure/cost, and prepare a pinned submission. Check commands, paths, artifact access, and any required review steps. This does not authorize extra agents, paid runs, or remote mutations outside the task.

Check logs and artifact audiences; verify trusted storage and reviewer/service authority. For executable candidates, verify isolation from evaluator credentials and evidence writes. Do not claim live controls or integrations that were not tested.

Report objective, mode, owner, destination, implemented infrastructure, local/hosted checks, and specific remaining blockers. Distinguish `scaffolded`, `locally validated`, and `operational` using the protocol. Include copyable instructions for a contributing agent. Setup does not auto-merge, deploy candidates, or authorize a live experiment.
