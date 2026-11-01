# Start an internal Benchcoding leaderboard

Give your coding agent this repository and the following instruction:

> Read `skills/benchcoding-create/SKILL.md` and follow it to create an internal leaderboard for my objective. Use the existing repository context where available. Establish the evaluation contract, seed contributor instructions, and prepare GitHub Actions or GitLab CI validation. Ask me for the objective, owner, destination, and resource limits if they are missing. Make the setup reviewable and distinguish a local scaffold from a working, independently validated board.

You can point an agent at this file without installing a plugin. It must fetch the linked skill and its referenced files, not just this page. For local skill installation, preserve the three sibling skill directories and their relative paths. These instructions are intended for any coding harness that can read Markdown, edit repositories, and operate the selected hosting provider.

## Choose the work

| Skill | Use it to |
| --- | --- |
| [Create](skills/benchcoding-create/SKILL.md) | Define an objective and build its repository, evaluator integration, CI, and contributor guide. |
| [Contribute](skills/benchcoding-contribute/SKILL.md) | Register a hypothesis, run bounded experiments, and submit immutable candidates. |
| [Maintain](skills/benchcoding-maintain/SKILL.md) | Independently evaluate submissions, publish evidence, manage budgets, and promote baselines. |

A board belongs to a named engineer, with a team responsible for maintenance. Other teams can discover and contribute to it within company access policies. GitHub or GitLab holds the code and review history; the board summarizes experiments and verified evidence.

## What the setup produces

- An objective contract defining metrics, acceptance gates, budgets, allowed changes, and ownership.
- A reproducible baseline and a public development evaluation.
- A trusted validation workflow, separate from candidate-controlled configuration.
- A seeded `AGENTS.md`, experiment/submission templates, and submission tracking.
- Versioned result records and a generated leaderboard that separates reported, verified, and accepted results.
- Operating instructions for review, integration, baseline changes, and reruns.

The supplied CI files deliberately fail until a domain-specific validation controller is implemented. A generic template cannot decide whether a parser is correct or a kernel is faster. The creation skill must implement that adapter and exercise its failure cases before calling the board ready. No new remote repository is created by reading these files.

Start with one objective and owner-managed validation requests. Add automatic dispatch and company-wide discovery after the basic submission-to-evidence loop works. Never combine unrelated objectives into one score ranking.
