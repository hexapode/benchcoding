# Benchcoding

A single-page illustrated essay by Pierre-Loic Doulcet.

The proposal: engineers own measurable objectives, direct agent experiments, understand agent behavior, and independently verify improvements. Public competitions suggest a workflow worth testing inside companies. Internal adoption and performance benefits are hypotheses, not reported results.

## Files

- `docs/index.html`: illustrated essay and interactive teaching example.
- `docs/blog/benchcoding/index.html`: redirect for existing article links, preserving fragments and query parameters.
- `docs/styles.css`: responsive typography and layout.
- `.github/workflows/pages.yml`: publishes only `docs/` to GitHub Pages.

No dependencies, build step, external fonts, analytics, or backend. Figures use HTML, CSS, and inline SVG. The essay lives at the site root; in-page links navigate its sections. The article remains readable without JavaScript.

## Preview

Run `python3 -m http.server 8765 --directory docs`, then visit http://localhost:8765.

## Publish

In repository Settings → Pages, select GitHub Actions as the source. Push to `main` or run the Pages workflow. Expected project URL: https://hexapode.github.io/benchcoding/.

The fictional benchmark values in the article are illustrative. Source links are included beside the relevant claims. No FTP credentials or private conversation transcripts belong in this repository.

## Editorial guide

Read [writting.md](writting.md) before revising reader-facing text. It records the user’s preferences, examples, and sources, and should grow with future feedback.
