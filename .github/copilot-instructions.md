<!-- Copilot / AI agent instructions for the Fall2025 `about-me` static site -->
# Project Overview

This repository is a small static website (landing + directory) built with plain HTML, CSS and light JavaScript. The site uses Bootstrap (local + CDN links), Google Fonts, and includes `three` as a dependency in `package.json` (not currently referenced in the source files). Primary files to inspect: `index.html`, `main.js`, `stylesheet.css`, `directory.html`, and `package.json`.

# What to prioritize
- Keep changes minimal and consistent with the current static-site structure — there is no build pipeline or bundler configured.
- Prefer edits to `index.html` and `stylesheet.css` for UI changes; `main.js` contains small DOM behavior (scroll-to-top button) and should remain simple.
- Preserve Bootstrap usage and class naming conventions already present (e.g., `.landing`, `.old-hero`, `.cardd`, `.my-card`, `.ogcomp`).

# Key patterns & examples
- Hero background: the hero image is implemented via CSS pseudo-element in `stylesheet.css`: `.landing header ::before { background-image: url("bridgeday.jpeg"); }`. Use that for full-bleed backgrounds rather than inserting additional img tags.
- Floating/positioned illustration: `index.html` renders an image with class `ogcomp` and the stylesheet uses transforms (`transform: translate(80%, -30%)`) to position it — reuse that pattern for similar art assets.
- Card pattern: `.my-card` uses `background-color: #282727` and rounded/overflow styles. Match these utilities when adding new cards.
- Button pattern: `.button` in CSS sets sizing and border radius for large hero CTA buttons — keep sizing consistent when adding hero CTAs.

# Small but important project-specific notes (explicit examples)
- `main.js` expects an element with id `scrollToTopBtn` and toggles its visibility. Currently `index.html` does not include an element with `id="scrollToTopBtn"` — consider adding the element or guarding `main.js` against missing elements (e.g., early return if `getElementById` is null).
- `index.html` includes both `css/bootstrap.min.css` (local) and a CDN link for Bootstrap. Maintain both only if intentional; otherwise prefer the CDN or remove the duplicate local link.
- Fonts: `index.html` uses Google Fonts and duplicates `preconnect` for the same domains — keep lightweight and remove exact duplicates if cleaning up.
- `package.json` lists `three` as a dependency. There is no import/use of Three.js in the current files — if introducing 3D content, import from `node_modules` or switch to CDN usage depending on whether a build step is added.

# Developer workflows (how to run/test locally)
- Static preview (recommended quick): Use VS Code Live Server or serve via Python:
  - `python3 -m http.server 8000` and open `http://localhost:8000` in the browser.
  - Or `npx serve` (if `serve` is available) after `npm install`.
- If using Node dependencies (for `three`), run:
  - `npm install` to populate `node_modules`.
  - There is no build script — if you add a bundler (Vite/webpack), add `scripts` to `package.json` and document them here.

# Conventions for changes
- CSS: keep class-first approach (no CSS-in-JS). Reuse existing variables (e.g., `--nav-height`) and avoid global resets that alter layout unintentionally.
- JS: DOM queries should guard against missing elements. Keep behavior unobtrusive and scoped to IDs/classes present in `index.html`.
- Assets: referenced images include `bridgeday.jpeg`, `computer_480.png`, and `static.jpg` (commented). Check `index.html` and `stylesheet.css` when adding/removing assets.

# Integration / external dependencies
- Google Fonts and Figlet are loaded via script/link tags in `index.html`.
- Bootstrap is included via both local and CDN link tags; be careful when upgrading versions.
- `three` is listed in `package.json` — decide whether to include from CDN (easy) or import from `node_modules` (requires a bundler).

# When to ask the repo owner
- If you plan to add a build step (bundler, transpiler, or module imports) — confirm whether `three` should be included via `npm` or CDN.
- If a new JS behavior is visible only on certain pages (e.g., `directory.html`) confirm whether to split `main.js` or conditionally initialize scripts per page.

# Example quick fixes you can apply safely
- Add a defensive-null check to `main.js` to avoid JS errors when `#scrollToTopBtn` is missing.
- Remove duplicate `preconnect` entries in `index.html` (one set is enough).
- Consolidate Bootstrap inclusion to the CDN if there is no local `css/bootstrap.min.css` file present in the repo.

If anything in this guidance is unclear or you'd like the file to enforce stricter rules (formatting, linting, CI checks), tell me which direction and I'll update the instructions. 
