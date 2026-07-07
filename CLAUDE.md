# CLAUDE.md — Brewing Distilling + AI (the guidebook / framework)

Working instructions for this repo. Its sibling is the main blog at `../ankurnapa.github.io`; this guidebook is the **design source** the blog was restyled to match.

## What this is
A plain-language "AI for brewers and distillers" guidebook. **Static HTML, no build step** (no Jekyll, no bundler). GitHub Pages **project site**: repo `AnkurNapa/brewing-distilling-ai`, branch `main`, served at `https://ankurnapa.github.io/brewing-distilling-ai/`. Edit HTML directly and push; verify live with a `?cb=` cache-buster (Pages CDN lag ~1 min).

## Pages
Each page is self-contained with its own inline `<style>`:
- `index.html` — home (hero, plain-terms, how-it-helps grid, honest closing, **Latest from the blog**).
- `patterns.html` — 23 patterns. `guidebook.html` — chapters 1-6. `literacy.html` — prompts/guide. `case-studies.html`, `glossary.html`.
- `use-*.html` — the six "how it helps" detail pages.
- `chapter-N.html`, `guidebook-print.html`, `guidebook.pdf` — long-form.

## Design system (the canonical teal theme)
- Palette: teal `#00695c`, deep `#06483f`, pink accent `#ff4081` / hero pink `#fd4376`, section `#f0f6f5`, mid `#4dd0c4`, ink `rgba(0,0,0,.87)`, text `#4a4a4a`. Light-only.
- Fonts: Poppins (display) + Open Sans (body) via Google Fonts.
- Components: pill nav (`.pills`/`.pill`) on content pages; `<ul>` nav on `index.html` and `literacy.html`; teal hero; rounded white/section cards; do/don't boxes (`.dd.do` green, `.dd.dont` pink).

## Navigation (keep in sync across ALL pages)
Every page's nav must carry the same destinations, including the **Blog** link to the main blog (`https://ankurnapa.github.io/`). The blog links back with a **Guidebook** nav item. When adding/removing a nav destination, update it on every page (pill nav pages: add an `<a class="pill">`; `index.html`/`literacy.html`: add an `<li>`).

## "Latest from the blog" auto-pull (index.html)
The home page's blog section is **dynamic**: a small client-side script fetches the main blog's RSS feed (`https://ankurnapa.github.io/feed.xml`, same-origin so no CORS), parses the latest 3 `<item>`s, and renders cards. Rules:
- Insert feed values with `textContent` only — never `innerHTML`.
- Validate the item `<link>` scheme (`^https?://`) before assigning to `href`, to block `javascript:`/`data:` URLs.
- The three static cards in the markup are the **no-JS/offline fallback** — keep them reasonable.
- This is client-side, so the live list is not in the served HTML (search engines see the fallback). If SEO-baked HTML is wanted, add a scheduled GitHub Action that regenerates the cards from the feed at build time.

## Relationship to the blog
Sibling sites, cross-linked both ways. The blog matches this guidebook's palette and type. Keep the two visually consistent: if the teal tokens change here, mirror them in `../ankurnapa.github.io/assets/css/style.css` and its post-diagram palette.
