# Choose evaluation before infrastructure

Select one mode or an explicit combination from the objective and available evidence. Propose a passing candidate, a failing candidate, and an ambiguous case to the human owner. Resolve missing acceptance criteria, tradeoffs, or authority with focused questions; implement independent work while decisions are pending. Reuse agreed rules rather than asking for approval again.

## Automated offline

Examples: runtime performance, parser correctness, data pipeline replay, QA fault detection.

Build a reproducible development evaluation, a protected acceptance evaluation, baseline comparison, isolated execution, and evidence ingestion. Declare workloads, limits, measurement boundaries, repetitions, and uncertainty. Validate a useful fixture and a deliberately invalid one, evaluator tampering, version drift, timeout, and missing results. QA can measure held-out bug detection with runtime and false-alarm constraints rather than coverage alone.

## Human review

Examples: design quality, accessibility review, maintainability tasks, usefulness of generated content.

Build pinned review packages, a task/rubric, an authorized reviewer queue, and recorded judgments. Define reviewer eligibility, independence from the submission, any blinding/randomization, sample/tasks, required reviews, and how disagreement is resolved. Use observed task completion where appropriate; qualitative rationale may be sufficient for some criteria. Do not require reviewers to assign a number merely to populate a leaderboard.

A maintainability trial might ask engineers unfamiliar with a refactor to make comparable changes. A design review might combine user task observations with designer judgment. Record task versions, baseline/candidate materials, assistance allowed, errors, and limitations. Reviewer disagreement or missing reviews cannot silently become a pass. Exercise duplicate/unauthorized attestations and the path from waiting to a final decision using clearly labeled fixtures.

## Live controlled experiment

Examples: onboarding, retention/churn, feature usefulness in production.

First inspect existing feature flags, assignment, analytics, and experimentation tools. Agree on the eligible population, assignment unit and method, control/variant identities, primary and secondary outcomes, guardrails, observation window, minimum evidence/uncertainty rule, missing-data treatment, and stopping/rollback rules. Ask the owner or an appropriate specialist when the design cannot support a defensible comparison. Do not choose arbitrary sample sizes or claim causality from an uncontrolled before/after change.

Build or integrate approved variant registration, authorization for exposure, durable dispatch, observation collection, scheduled/event-driven resume, analysis, and pause/rollback control. Pin code/configuration and assignment changes. Do not expose real users merely because setup was requested. Document what the owner must authorize before activation; test orchestration with synthetic events without claiming measured retention gains.

Track `awaiting_evidence` without an idle CI job. Resume idempotently when the observation window and completeness rules are satisfied. Missing observations, a changing variant, an early stop, or inconclusive evidence need explicit outcomes. Offline predictions can shortlist variants but cannot certify the live result. Exercise duplicate callbacks, delayed/missing observations, budget exhaustion, unauthorized exposure, and stop/rollback behavior.

## Hybrid

Examples: a website change with accessibility checks, user review, and a later live trial; a feature with offline quality tests and product metrics.

Define a stage graph with prerequisites and an authority for each stage. Automated checks may run before review; live exposure follows its separate authorization. Specify which failures stop later stages and which missing judgments keep the candidate pending. The final decision must include every required stage and guardrail; a high offline score cannot replace missing human or live evidence.

## Tradeoffs and infrastructure choice

Use multiple measures when one score would hide a decision, such as retention versus complaints or speed versus cost. Set hard constraints where justified. Otherwise present evidence side by side or use a declared Pareto view and leave the choice to the owner. Only use weighted scores when the owner has agreed to the weighting and its meaning.

The chosen mode determines the implementation. An existing review tool plus trusted evidence ingestion may be enough for design. A feature-flag/analytics platform may handle live studies. GitHub/GitLab can still hold source and collaboration history without being the evaluator. Document actual integration commands, artifacts, permissions, and unresolved access needs. Do not provision a Python benchmark runner for a process that does not run a benchmark.
