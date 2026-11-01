# GitHub setup

Read after the protocol when the destination is GitHub (including an enterprise host). Use an available GitHub connector or authenticated `gh` for that host. Inspect existing organization policies and repo settings before proposing changes. GitHub Actions is the runner/orchestrator; it does not automatically make candidate-produced results trustworthy.

## Evaluation mode comes first

Use this provider for source/collaboration and short dispatch/resume jobs when it fits the objective. Human reviews and live studies may use an existing external system; CI coordinates or ingests evidence rather than running the entire evaluation. Read [evaluation modes](evaluation-modes.md). Use the artifact manifest from the protocol, not a fabricated commit for a non-code submission. Provide an issue/form route when a PR/MR is unnecessary.

Adapt the template's default Python command to the implemented adapter. Store waiting states durably and exit; use an authorized follow-up event/job to resume. Successful orchestration can produce `awaiting_evidence`, `awaiting_review`, or `inconclusive`. Ingestion must inspect authenticated stage records and all required gates before publishing verification. A failed job cannot certify success. Live exposure requires the objective's separate authorization and stop/rollback process.


## Source and control repositories

For the first pilot, use a private source repository and a private validation/control repository writable only by the owner/evaluator maintainers. The source repository contains the objective, experiments, contributor `AGENTS.md`, and development CI. The control repository holds admitted requests, trusted evaluator/configuration, and authoritative evidence. A same-repo protected-branch arrangement is possible only if runner, workflow modification, dispatch, and secret-access restrictions actually enforce equivalent separation.

Create remote repositories only within the user's requested organization and authorized scope. Never turn on public visibility for an internal board. Record the host and full repository identity rather than assuming github.com. Set up access for contributors without giving them write access to the control repository.

Protect the control default branch: restrict direct updates, require owner review and checks, prevent force-push/deletion, and configure bypass permissions deliberately. Protect evaluator, workflow, contract, and result paths with CODEOWNERS plus required code-owner reviews where available. CODEOWNERS alone is not enforcement. If plan/organization settings prevent these controls, report that and use a separately restricted control repository instead of claiming protection.

## Seed contributor routes

Add the AGENTS guide and skills to the source repository. Adapt the experiment template into `.github/ISSUE_TEMPLATE/experiment.md` and submission template into `.github/pull_request_template.md`, preserving existing templates. Link each candidate to its experiment. For findings-only work, close the experiment with evidence and cost. A PR is not required for every trial.

Document a pilot admission process: the contributor posts a pinned artifact manifest; the owner verifies it, reserves budget, and commits a request record to the control repository through the protected process. The owner dispatches validation with that ID. This avoids building an authenticated bot before the protocol is proven.

## Actions validation

If using Actions for dispatch/resume, adapt [the workflow template](../assets/github-validate.yml.template) in the control repository as `.github/workflows/validate-entry.yml`. It intentionally fails until the chosen adapter implements the protocol; `validation/controller.py` is the default interface, not a required language. Pin actions to reviewed full commit SHAs before activation; the template contains no third-party actions. Verify the runner image has the declared Python/git dependencies or install them through trusted setup.

The controller source is checked out from the protected default branch revision, never from a submitted PR. Dispatch on that branch only; the runtime branch guard is additional protection, not an access-control substitute, because someone able to edit a workflow could remove it. Restrict control-repo writers/dispatchers and workflow policy accordingly.

For executable candidates, the controller fetches candidate source and launches a separate isolated worker or evaluator service. It must not execute candidate build/test code on the Actions controller runner. If private source access is needed, use a narrowly scoped credential on the controller only; do not pass it to the worker. Keep holdouts and answer labels in the evaluator service. Do not use `pull_request_target` or a privileged `workflow_run` to execute submitted code.

The starter workflow validates but does not publish a board automatically. Implement a separate trusted ingestion/publication step or owner-operated process that checks the Actions run's repository, protected ref, controller revision, conclusion, and evidence provenance. Persist results in trusted durable storage and link them from the source repo's board. Give the publisher only the permissions needed to write that view; it must never execute candidate artifacts. If using artifact actions, pin them, restrict content, choose retention, and archive accepted evidence before expiry.

A generic green workflow is not a per-candidate check: it ran in the control repository. Either have the owner verify the attestation before merge or publish a candidate-specific check using a narrowly scoped GitHub App and require that expected integration as the check source. Bind it to the exact code SHA when publishing a code check; other artifacts use their admitted manifest identity in the evidence view. Do not let a contributor's same-named check satisfy the acceptance rule.

## Verify live configuration

Inspect effective branch/ruleset protections, app/token scopes, Actions permissions, and identities allowed to dispatch. Exercise the selected mode’s readiness cases from the protocol: offline baseline/pass/fail/timeout; authorized and conflicting human reviews; or live wait/resume/stop with synthetic observations. Mark real integrations that remain untested. Verify an unauthorized contributor cannot alter the judge or publish a verified score. Confirm source updates cannot change the admitted artifact identity. Record any checks unavailable under the organization's plan or your permissions.

Official references (verify current behavior on the destination):
- [Secure use](https://docs.github.com/en/actions/reference/security/secure-use)
- [Workflow events](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows)
- [Checks API for external evaluators](https://docs.github.com/en/rest/guides/using-the-rest-api-to-interact-with-checks)
