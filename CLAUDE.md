# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A one-page site for «Институт Мискатоник», a Russian-language discussion circle in Belgrade, served at https://misk.club by GitHub Pages. It is an institute, not a book club — never call it «книжный клуб». Meetings have a list of discussion topics, not a set book. All site copy is in Russian.

## Hard constraints

- Plain HTML + CSS only. No JavaScript, no build step, no backend, no external requests (no web fonts, CDNs, embeds, analytics). Interactive behaviour must come from HTML/CSS alone.
- The site must stay readable on both desktop and mobile; check both widths after any layout change.

## Deployment

- GitHub Pages serves the `docs/` folder of the `master` branch of `xdefrag/misk.club` (legacy branch build, no Actions). Pushing to `master` publishes. Everything the site needs lives in `docs/`; files outside it (like this one) are not published.
- `docs/CNAME` binds the custom domain; removing or renaming it, or the repo, while DNS still points at GitHub leaves the domain open to takeover. `docs/.nojekyll` disables Jekyll processing.
- DNS is at Porkbun: four apex A records to GitHub Pages plus `www` CNAME to `xdefrag.github.io`.

## Commits

Commit messages are in English and follow Conventional Commits (`feat:`, `fix:`, `chore:`, `docs:`, `revert:` …), even though the site copy and conversation are in Russian.

## Previewing

No tooling to install. Open `docs/index.html` in a browser, or render screenshots headlessly:

```
chromium --headless --hide-scrollbars --window-size=1440,900 --screenshot=/tmp/desktop.png file://$PWD/docs/index.html
chromium --headless --hide-scrollbars --window-size=390,844  --screenshot=/tmp/mobile.png  file://$PWD/docs/index.html
```

Headless screenshots only capture the window, so use a tall `--window-size` height to see the whole page.

## Design

Minimal, following https://brutalist-web.design/ literally: one narrow column of plain text and a single image (the poster, `docs/afisha.jpg`). The owner rejected, in order, bookish designs (templated, too prim) and a loud poster-style layout with coloured full-width sections, giant type and buttons — do not drift back toward either.

- No sections, navigation, cards, buttons or decoration. A heading, the poster, a few paragraphs.
- Always dark: background `#111`, text `#ddd`, and one accent, the poster's green `#2bff80`, used only for the h1 and links (visited links stay green). No light variant.
- Typography follows that site's scale but is sans-serif throughout (the owner rejected the serif body): Helvetica/Arial stack, 21px base, line-height 1.5 in a 34em column, headings at line-height 1 (h1 5rem, shrinking on narrow screens, with «Институт» as a smaller `<small>` line above «Мискатоник», like "Guidelines for" on that site; h2 2.25rem). No font files.
- Styling is done with Tachyons utility classes in the HTML (https://tachyons.io/docs/), so the owner can edit content without touching CSS. `docs/tachyons.min.css` is v4.12.0 vendored locally — never link it from a CDN. `docs/style.css` holds only what Tachyons lacks (21px base, text colour, the green accent, `lst-square`/`lsp-outside`); keep it that small and prefer a Tachyons class over a new rule.
- The topics list copies the list on that site: `<ul class="f4 mt0 pl0-ns pl3 lst-square lsp-outside">` — square bullets that hang outside the column on wide screens.
- Links are plain underlined hyperlinks. No buttons: nothing on the page is a form action.
- Copy is short and direct, written to the reader in the informal «ты».

## Emblem and icons

The club emblem is a cyan line drawing on black: a ring-tailed lemur on the roof of a pagoda (a reference to Nick Land's teleoplexy; the lemur and the fact that it stands on a pagoda are both essential). It is used only as the favicon; the owner does not want it on the page itself, so do not add it to the layout.

- `brand/emblem-source.png` — the approved artwork (owner-generated raster, 1254px).
- `brand/emblem.svg` — vector trace of it (Recraft vectorizer; ~1 MB, 1200+ paths, so it is a master file, not something to serve). `brand/` is outside `docs/` and is not published.
- `docs/favicon.ico` (16/32/48), `docs/favicon.png` (192), `docs/apple-touch-icon.png` (180) — rendered from the SVG, cropped square to the artwork and recoloured from the artwork's cyan to the site accent `#2bff80`. The masters in `brand/` stay cyan.

To regenerate: `rsvg-convert -w 2508 -h 2508 brand/emblem.svg`, crop `2080x2080+214+164`, tint (`-colorspace Gray -auto-level`, then `+level-colors black,#2bff80` after resizing), resize. For the `.ico` sizes, thicken the lines first (`-morphology Dilate Disk:7 -level 0%,70%`) or they vanish when shrunk.

## Updating for a new meeting

Only `docs/index.html` and the poster change per meeting:

1. Replace `docs/afisha.jpg` with the new poster (square; the `alt` text should restate what the poster says).
2. Update the `<h2>`, the `<time datetime>` line, the «Темы» list (one `<li>` per topic) and the «Место / Цена» paragraphs.
3. Update `og:description` and the `<meta name="description">` date in `<head>`.

## Content status

The page is one block of text about the next meeting. Rules and a separate price section were removed at the owner's request; do not bring them back unasked.

- Venue is Чердак Чая (tea house), Belgrade, Despota Đurđa 5; map and directions links point to Yandex, Google and the venue's Telegram post.
- Price is 500 dinars plus tea, with a link to the venue's menu.
- The only contact is the owner's Telegram, `t.me/xdefrag`.
- The topics list holds a single «TBA» item until the owner supplies topics.
