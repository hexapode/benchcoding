# Writing notes

This is the evolving editorial guide for the Benchcoding blog. Keep the filename `writting.md`. Apply it when drafting or revising the article, home page, captions, metadata, and other reader-facing text. Add concrete examples as we find more preferences; do not turn every preference into an absolute ban.

## What we are aiming for

Write as an engineer explaining a proposal to a skeptical colleague. Explain what would happen, who makes the decisions, and why the arrangement might be useful. Let the reader assess the argument without telling them how profound it is.

The central idea is an engineer taking responsibility for a measurable outcome and directing a sustained search across agent experiments. Benchmarks, a maintained board, and verification support that work. Avoid drifting into autonomous compute markets or a claim that engineers stop coding.

## Patterns to revise

- **Clipped, balanced mini-speeches.** Avoid a run of short declarations that divides a thought into a catchy three-beat sequence. Connect the ideas where their relationship matters. Short sentences are useful when they have a job; joining everything into long sentences is not the solution.
- **Manufactured contrasts.** Watch for “not X, but Y,” “this isn't about X,” and “the real challenge is Y.” State the claim directly unless the distinction resolves an actual misunderstanding. A comparison of workflows should explain the operational difference.
- **Lists assembled for rhythm.** Do not force examples, benefits, or responsibilities into groups of three. Keep the items the argument needs, even if that means one example or four constraints.
- **Slogans used as reasoning.** Remove paragraph-ending lines that announce a lesson without adding evidence or explanation. A memorable sentence can stay if the article has earned it and the user wants it; do not manufacture a punchline for every section.
- **Inflated significance.** Avoid “fundamental shift,” “the future of,” “revolutionary,” and similar claims unless there is specific evidence to defend them. Describe the proposed change in responsibility or behavior.
- **Mechanical section templates.** Do not give every section the same opening, three examples, warning, and closing maxim. Organize around the reader's next substantive question.
- **Generic filler and jargon.** Replace vague terms with the actual action or consequence. “The owner funds a second run” says more than “dynamic resource allocation.” Use a technical term when its precision is useful, and explain unfamiliar ones.
- **Repeated disclaimers or lessons.** State the evidence boundary clearly, then proceed. Consolidate verification guidance instead of re-explaining holdouts and independent review in every section.
- **Formatting as emphasis.** Avoid bolding every conclusion or breaking ordinary prose into one-line paragraphs. Use tables for comparisons and lists for genuinely parallel requirements.

## Examples from this article

### Opening sentence

Rejected:

> An engineer owns the objective. Agents explore ways to improve it. The hard part is knowing whether they have.

Earlier revision (subsequently tightened):

> I’m interested in what happens when an engineer takes responsibility for a benchmark and lets people across the company send agents to work on it.

The revision gives the author a specific proposal and introduces the cross-team mechanism. It does not merely substitute synonyms or connect the original three sentences with commas.

### Empty closing flourish

Rejected:

> A lucky search is not a methodology.

Prefer an explanation of the consequence:

> Repeat the comparison across several runs or components so one lucky discovery doesn’t decide the outcome.

### A line to retain intentionally

> Owning the leaderboard means being accountable for what its numbers mean.

The user specifically identified this as a useful anchor. Keep it tied to concrete decisions about evaluation, review, and maintenance. Its presence is not permission to add similar slogans throughout the article.

## Argument and evidence

- Put the distinctive proposal near the opening. Existing performance benchmarks and optimization loops are not new; sustained ownership of a search across agent experiments is the change being proposed.
- Explain what a shared board enables beyond an experiment log: avoiding duplicate attempts, choosing where to spend effort, preserving failed approaches, and coordinating work against an updated baseline.
- Make organizational claims concrete. Explain who pays for an experiment, why another team would contribute, who maintains accepted code, and what happens when review becomes a bottleneck.
- Preserve the parser example and the difference between a reported score and an accepted improvement. Label its numbers as invented.
- Compare workflows by who defines the work, what agents receive, and how results are accepted. Do not present Scrum, IDEs, autocomplete, and agent workflows as a historical ladder.
- Keep observed public competitions separate from the hypothesis about internal adoption. Link claims to sources that actually support them.
- End the pilot with conditions for continuing, chosen before the results: accepted production improvement, total cost including human work and setup, and comparison with capable open-ended agent investigation. Label suggested numerical thresholds as proposals.
- Use first person for the user's proposals and judgments. Never invent experiments they ran, clients they served, anecdotes, quotations, or personal experience to make the prose seem human.

## Revision pass

Read a section aloud and check whether it sounds like someone explaining a thought or someone delivering a sequence of taglines. Check the whole paragraph as well as individual sentences. Vary sentence length as the reasoning requires; do not alternate lengths according to a formula.

For each paragraph, ask what the reader learns that they did not know before. Cut repetitions. Replace abstractions with a concrete decision where possible. Check that every source still supports the sentence beside it after editing.

After changing the article, update the home-page excerpt and metadata when needed. Check that longer text fits the layout and that captions, source links, and interactive examples still agree with the prose.

Do not use an AI-detector score as a quality target. These preferences are about clarity, substance, and the user's voice. Em dashes, short sentences, and three-item lists are not proof of machine authorship and are not automatically forbidden.

## Sources consulted

Reviewed November 1, 2026. These sources informed the editing approach; they are not a mechanical recipe or evidence that a particular text was AI-generated.

- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing). Community guidance on recurring patterns including negative parallelism, overused groups of three, inflated significance, and formulaic presentation. Its context is Wikipedia editing, so apply observations with judgment rather than importing an encyclopedia's entire style into a personal blog.
- [William Zinsser, “Simplicity,” reproduced by William P. Clement at UMass](https://websites.umass.edu/wwclement/simplicity/). A basis for removing inflated language and unnecessary work for the reader while keeping the underlying thought clear.

## Preference log

### November 1, 2026

- The user rejected the opening's three clipped declarations and asked for a rewrite of the whole article, not a vocabulary cleanup.
- Retain the understandable parser example and clearly distinguish fictional numbers from evidence.
- Center the piece on engineers owning outcomes and directing agent search.
- Expand the coordination and economic reasons for maintaining a leaderboard.
- Replace the four-era framing with a workflow comparison.
- Preserve the accountability sentence above as a deliberate exception to the preference against slogans.
- Keep this file open to revision as more examples and preferences emerge.

### Further argument revision, November 1, 2026

- Use a strong comparison: an engineer already giving agents open-ended investigations, with normal tools and freedom to explore alternatives. Do not imply that this workflow requires predetermined implementation tasks.
- Separate the within-team maintained-search hypothesis from the incremental benefit of cross-team participation. Test them in stages with comparable total resources.
- Explain cheaper experimentation as the economic hypothesis motivating wider search; do not claim proven cost savings.
- Include discovery as well as verification. Mark unexpected solutions in the parser scenario as fictional, not personal experience or measured evidence.
- Define the numerator of any improvement-per-dollar metric. Do not treat percentage improvements across unrelated components as interchangeable business value.
- Describe the proposed process directly. Reserve hedging for uncertain benefits, and remove prose that merely repeats an interactive result or caption.

### Tooling section, November 1, 2026

- Frame tooling as a product hypothesis around shared objectives with named engineer accountability, subject to access permissions.
- Group experiments by hypothesis across coding harnesses. Distinguish company-wide discovery from rankings within comparable objectives and evaluation versions.
- A pilot can build on GitHub; do not imply that a replacement platform or full autonomy is required. Keep independent evaluation separate from candidate-controlled code.
