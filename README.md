# Benchcoding

A single-page illustrated manifesto by Pierre-Loic Doulcet.

The manifesto argues for applying Benchcoding across software, from code quality and performance to useful features, retention, design, QA, data pipelines, and reliability. An engineer owns each objective and decides what to try next and what to ship, with input from the relevant product and domain owners. A fictional parser example explains how colleagues can contribute and how misleading scores are rejected. The pilot tests whether keeping that shared record is worth the work.

## Files

- `docs/index.html`: illustrated manifesto and interactive teaching example.
- `docs/blog/benchcoding/index.html`: redirect for existing article links, preserving fragments and query parameters.
- `docs/styles.css`: responsive typography and layout.
- `.github/workflows/pages.yml`: publishes only `docs/` to GitHub Pages.

## Start your own leaderboard

Point a coding agent at [LEADERBOARDS.md](LEADERBOARDS.md). The repository includes skills to create a board, contribute experiments, and manage independent validation, with GitHub Actions and GitLab CI setup guides and contributor instruction templates. The setup agent adapts the evaluator to your objective before activating validation.

## Manifesto implementation

No dependencies, build step, external fonts, analytics, or backend. Figures use HTML, CSS, and inline SVG. The manifesto lives at the site root; in-page links navigate its sections. The article remains readable without JavaScript.

## Preview

Run `python3 -m http.server 8765 --directory docs`, then visit http://localhost:8765.

## Publish

In repository Settings → Pages, select GitHub Actions as the source. Push to `main` or run the Pages workflow. Expected project URL: https://hexapode.github.io/benchcoding/.

The fictional benchmark values in the article are illustrative. Source links are included beside the relevant claims. No FTP credentials or private conversation transcripts belong in this repository.

## Editorial guide

Read [writting.md](writting.md) before revising reader-facing text. It records the user’s preferences, examples, and sources, and should grow with future feedback.
