# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A one-page site for the Russian-language book club «Мискатоник» (Институт Мискатоник), served at https://misk.club by GitHub Pages. All site copy is in Russian.

## Hard constraints

- Plain HTML + CSS only. No JavaScript, no build step, no backend, no external requests (no web fonts, CDNs, embeds, analytics). Interactive behaviour must come from HTML/CSS alone.
- The site must stay readable on both desktop and mobile; check both widths after any layout change.

## Deployment

- GitHub Pages serves the `docs/` folder of the `master` branch of `xdefrag/misk.club` (legacy branch build, no Actions). Pushing to `master` publishes. Everything the site needs lives in `docs/`; files outside it (like this one) are not published.
- `docs/CNAME` binds the custom domain; removing or renaming it, or the repo, while DNS still points at GitHub leaves the domain open to takeover. `docs/.nojekyll` disables Jekyll processing.
- DNS is at Porkbun: four apex A records to GitHub Pages plus `www` CNAME to `xdefrag.github.io`.

## Previewing

No tooling to install. Open `docs/index.html` in a browser, or render screenshots headlessly:

```
chromium --headless --hide-scrollbars --window-size=1440,900 --screenshot=/tmp/desktop.png file://$PWD/docs/index.html
chromium --headless --hide-scrollbars --window-size=390,844  --screenshot=/tmp/mobile.png  file://$PWD/docs/index.html
```

Headless screenshots only capture the window, so use a tall `--window-size` height to see the whole page.

## Design

Brutalist poster style, modelled on the club's own event posters (`docs/afisha.jpg`): a photo, acid green, a plain grotesque, information stated bluntly and large. Earlier bookish directions (cream paper and serifs; cloth-binding cover) were rejected by the owner as templated and too prim — do not drift back toward them.

- Three colours only, defined as custom properties in `docs/style.css`: `--green` (sampled from the poster), black, white. Sections alternate these as full-width blocks.
- One system font stack (Helvetica/Arial); no font files.
- The wordmark in the header is sized in `vw` to span the viewport. Its width depends on the fallback font, so re-check for clipping at desktop and mobile widths if the name or size changes.
- Copy is short and direct, written to the reader in the informal «ты».

## Updating for a new meeting

The `#vstrecha` section in `docs/index.html` is the only part that changes per meeting:

1. Replace `docs/afisha.jpg` with the new poster (square; the `alt` text should restate what the poster says).
2. Update the heading, `<time datetime>`, the date/time line and the «Читаем / Где / Цена» rows.
3. Update `og:description` and the `<meta name="description">` date in `<head>`.

## Placeholders still in the site

Real values have not been supplied for: the book, the venue address and directions, the price (shown as `000`, currency unknown), and the links marked `CHANGE_ME` (Telegram, map). The venue name «ЂЂ» and the address `hello@misk.club` are guesses. Ask the owner rather than inventing replacements.
