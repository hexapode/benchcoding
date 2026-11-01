# Start a Benchcoding experiment workspace

Give your coding agent this repository and the following instruction:

> Read `skills/benchcoding-create/SKILL.md` and build a Benchcoding workspace for my objective. Choose automated offline, human review, live controlled, or hybrid evaluation before selecting infrastructure. Reuse my existing tools where appropriate. Implement and test the required adapters, evidence/state storage, budget accounting, and board; create a collaboration guide and adapt the contributor and maintainer skills so other agents can join. Propose validation with a passing, failing, and ambiguous example, and ask for my help with missing success criteria, tradeoffs, or review authority. Continue independent work while those decisions are pending. Support immutable non-code artifacts and delayed evidence when needed. Distinguish a scaffold, tested infrastructure, and real results. Live user exposure requires separate authorization.

You can point an agent at this file without installing a plugin. It must fetch the linked skill and its referenced files, not just this page. For local skill installation, preserve the three sibling skill directories and their relative paths. These instructions are intended for any coding harness that can read Markdown, edit repositories, and operate the selected hosting provider.

## Choose the work

| Skill | Use it to |
| --- | --- |
| [Create](skills/benchcoding-create/SKILL.md) | Choose evaluation methods and build the infrastructure and contributor guide for the objective. |
| [Contribute](skills/benchcoding-contribute/SKILL.md) | Register a hypothesis, run bounded experiments, and submit immutable candidates. |
| [Maintain](skills/benchcoding-maintain/SKILL.md) | Independently evaluate submissions, coordinate reviews or delayed evidence, manage budgets, and promote baselines. |

A board belongs to a named engineer, with a team responsible for maintenance. Other teams can discover and contribute to it within company access policies. GitHub or GitLab can hold code and collaboration history; existing review, analytics, or experiment tools can supply evaluation. The board summarizes evidence and pending work, with rankings only where the objective supports them.

## What the setup produces

- An objective contract defining applicable metrics or review rubrics, acceptance gates, budgets, allowed changes, and ownership.
- An immutable baseline and a development test, review procedure, or study plan appropriate to the objective.
- Implemented validation orchestration, evidence storage, budget tracking, and applicable provider/service integration, separate from candidate-controlled configuration.
- A documented validation flow, with the human owner resolving any missing acceptance criteria or review decisions.
- A collaboration guide, seeded `AGENTS.md`, adapted contributor and maintainer skills, experiment/submission templates, and submission tracking.
- Versioned evidence and a board that distinguishes reported, pending, inconclusive, verified, and accepted work, without requiring a numeric ranking.
- Operating instructions for review, integration, baseline changes, and reruns.

The optional GitHub/GitLab CI starters deliberately fail until the selected evaluation adapters are implemented and tested. A generic template cannot judge a parser, a design, or a retention experiment. Other stacks may use existing review or experiment services. A live dry run verifies infrastructure, not product impact. No new remote repository is created by reading these files.

Start with one objective and owner-managed validation requests. Add automatic dispatch and company-wide discovery after the basic submission-to-evidence loop works. Never combine unrelated objectives into one score ranking.
