# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

`dndtools` — a collection of D&D utilities, each built as a standalone HTML page, deployed to GitHub Pages.

All pages should be in French, as this is the main language used in my games.

## Stack constraints

Standalone HTML/CSS/JS. No framework, no bundler, no package manager, no build step. Do not introduce npm, a framework, or a transpiler without asking first — the absence of a toolchain is deliberate, and Pages serves the repo contents as-is with no build stage.

Each tool is a self-contained page: its markup, styles, and script live together and the page works when opened on its own.

Static hosting only — no server-side code, no request-time redirects, no environment secrets. Anything dynamic runs in the browser, and persistence means `localStorage` or the URL.

## Deployment

Deployed to GitHub Pages from `okaa-pi/dndtools`, served at `https://okaa-pi.github.io/dndtools/`. 

Three constraints follow from that, and all three fail *only* in production while working fine locally:

- **The site lives under the `/dndtools/` subpath, not the domain root.** Root-absolute paths (`/style.css`, `/tools/foo.html`) resolve against `okaa-pi.github.io` and 404. Use relative paths throughout.
- **Pages serves from Linux; macOS is case-insensitive.** A link to `Spells.html` for a file named `spells.html` loads locally and 404s live. Match filename case exactly.
- **Jekyll ignores files and directories beginning with `_`.** Add a `.nojekyll` file at the repo root to disable Jekyll processing if any such names are used.

## Local development

Serve over HTTP rather than opening files from disk — it matches how Pages behaves, and `file://` breaks ES modules and `fetch` of local files:

```bash
python3 -m http.server 8000
```

## Testing

There is no test framework. Verify changes by opening the affected page in a browser and exercising it.
