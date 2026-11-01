---
name: benchcoding-contribute
description: Contribute a bounded agent experiment or candidate to an existing Benchcoding leaderboard, preserving evidence and requesting independent validation.
---

# Contribute to a leaderboard

Read the destination `AGENTS.md`, `leaderboard/README.md`, objective contract, and [protocol](../benchcoding-create/references/protocol.md). Use the current board to find the owner, baseline, allowed changes, active hypotheses, and failed approaches. If instructions or evaluation versions conflict, resolve that before spending the experiment budget.

1. Register a hypothesis with the source baseline, approach, expected benefit, team/payer, harness/model, and bounded budget. Link related experiments and explain why another attempt is useful. Registration and funding are separate: use existing budget authorization or obtain an allocation before consuming shared resources.
2. Create an isolated checkout from the recorded baseline. Use only approved data and execution resources. Run the baseline development evaluation to establish the local environment; do not compare local timing to a hosted score as if hardware were identical.
3. Explore within the allowed code boundary and budget. Record changes, commands, resource use, failures, and findings. Keep traces free of secrets and restricted data. Stop at the budget/time limit or when redirected by the owner. Retry only within the original allocation.
4. Run the development evaluator and inspect completeness/correctness, not only speed. Do not weaken checks, edit acceptance data, move work outside the measured boundary, or tune against restricted acceptance feedback. If the contract has a gap, report it as a harness issue.
5. For a candidate, commit changes and submit the full immutable revision, repository identity, baseline, objective/evaluation versions, hypothesis, local results, costs, and reproduction instructions. Use the repository's submission template. Code changes after submission require a new revision and validation request. Never claim that a local score is independently verified.
6. Request validation through the documented issue/PR/MR process. The owner or trusted dispatcher reserves the validation budget. Do not trigger pipelines on arbitrary refs or bypass the protected validation path. Do not repeatedly query a holdout to guide optimization.
7. Report a useful failure even when there is no PR/MR. For passing candidates, respond to review and retest against updated baselines when requested. Integration and production acceptance remain the owner's decisions.

Finish with experiment/submission links or local paths, exact revision, reported measurements and their environment, total known cost, unknown cost fields, and current state. Do not edit official result records or the generated board to promote your entry.
