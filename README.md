# Benchcoding

An illustrated essay and small personal blog by Pierre-Loic Doulcet.

The proposal: engineers own measurable objectives, direct agent experiments, understand agent behavior, and independently verify improvements. Public competitions suggest a workflow worth testing inside companies. Internal adoption and performance benefits are hypotheses, not reported results.

## Files

- `docs/index.html`: blog index.
- `docs/blog/benchcoding/index.html`: illustrated article and interactive teaching example.
- `docs/styles.css`: responsive typography and layout.
- `.github/workflows/pages.yml`: publishes only `docs/` to GitHub Pages.

No dependencies, build step, external fonts, analytics, or backend. All figures are inline SVG. Navigation uses relative paths for GitHub project pages. The article remains readable without JavaScript.

## Preview

Run `python3 -m http.server 8765 --directory docs`, then visit http://localhost:8765.

## Publish

In repository Settings → Pages, select GitHub Actions as the source. Push to `main` or run the Pages workflow. Expected project URL: https://hexapode.github.io/benchcoding/.

The fictional benchmark values in the article are illustrative. Source links are included beside the relevant claims. No FTP credentials or private conversation transcripts belong in this repository.

## Editorial guide

Read [writting.md](writting.md) before revising reader-facing text. It records the user’s preferences, examples, and sources, and should grow with future feedback.
