# GitLab setup

Read after the protocol when the destination is GitLab. GitLab's equivalent of GitHub Actions is GitLab CI/CD. Use an available connector, authenticated `glab`, or the API for the configured GitLab host; do not assume GitLab.com or a particular paid tier.

## Source and validation projects

Prefer a private source project plus a private validation/control project whose maintainers are the trusted evaluator owners. Contributors can access development data, issues, and source without gaining control-project write or pipeline permissions. Explicitly choose visibility; GitLab `internal` may expose a project more broadly than the intended team, depending on the instance.

Protect the control default branch, restrict pushes/merges and pipeline dispatch to trusted roles, and prevent force pushes. Add approval/code-owner rules where supported. Confirm effective settings on the actual instance: a CODEOWNERS file or a protected variable alone is not a trust boundary. Keep the control project free of contributor-modified CI configuration and scope its job-token access to only the resources it needs.

## Seed contributor routes

Copy the AGENTS guide and skills into the source project. Adapt templates into `.gitlab/issue_templates/Experiment.md` and `.gitlab/merge_request_templates/Leaderboard.md`. The source project's MR pipeline is useful development feedback, not independent acceptance evidence.

For a minimal pilot, the owner admits a pinned candidate by committing its request to the control project's protected branch, reserves its validation budget, then runs the control pipeline with `SUBMISSION_ID`. Document the exact route for contributors and the owner. Do not hand contributors a control-project trigger token.

## Trusted CI

Adapt [the CI template](../assets/gitlab-ci.yml.template) in the control project. Use isolated, ephemeral controller runners and a separately isolated candidate worker or evaluator service. The sample uses a runner tag `benchcoding-controller`; provision and verify that runner explicitly. It must supply trusted Python/git dependencies. Disable shared privileged execution and ensure that candidate code never runs directly in this job.

The pipeline accepts manual web/API dispatch only on the protected default branch. CI rules are not authorization: restrict membership, pipeline-variable overrides, token permissions, and who can trigger that project. Verify the server-controlled checkout ref and project identity at ingestion. Read admitted requests from the trusted checkout, not from a variable containing arbitrary URLs or commands.

Never run a fork's MR configuration in a privileged parent project as the acceptance judge. GitLab documents that such pipelines can use the fork's CI configuration with parent-project resources. Keep that path disabled where possible. Do not enable protected-variable access for candidate-controlled pipelines. Review GitLab version/edition behavior rather than assuming all protection settings are available.

The controller implements the protocol and stores durable, provenance-bound evidence. The sample artifact is a diagnostic delivery mechanism, not proof by itself. Restrict artifact visibility on the actual instance and never upload holdout content. A separate trusted publisher or owner verifies project ID, pipeline source, protected ref, config/controller revision, job status, and candidate SHA before updating the board. Failed jobs may have diagnostic artifacts; those cannot certify verification.

Protect source merges using available approval/status-check features or an explicit owner review of the trusted attestation. A passing ordinary MR pipeline does not replace this. Revalidate integration revisions before baseline promotion.

## Verify live configuration

Exercise baseline, valid-fixture, invalid-candidate, stale-version, unauthorized dispatch, and timeout paths. Check candidate jobs have neither control-project credentials nor access to answer labels. Verify contributor-provided variables cannot redirect the evaluator/configuration or change the admitted revision. Confirm artifact audience and evidence retention. Mark unsupported/unverified protections as setup blockers rather than claiming the board is operational.

Official references (verify against the destination version):
- [Merge request pipelines and forks](https://docs.gitlab.com/ci/pipelines/merge_request_pipelines/)
- [CI/CD variable security](https://docs.gitlab.com/ci/variables/)
- [Pipeline permissions and protected branches](https://docs.gitlab.com/ci/pipelines/)
