# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Static marketing + legal site for **Backdrop Me**, an Android wallpaper-maker app. Two hand-written HTML pages with inline CSS/JS — no build system, no dependencies, no tests, no framework.

- `index.html` — bilingual (EN/中文) landing page
- `privacy-policy.html` — bilingual privacy policy
- `assets/` — app icon, Galaxy Store badges, device screenshots (`assets/shots/_zhtest.html` is a gitignored render artifact; leave it alone)

## Deployment

Published via **GitHub Pages** at `https://chinalwb.github.io/backdrop-me/`. Pushing to `main` deploys the site — there is no staging environment. Preview locally by opening the file directly or `python3 -m http.server`.

This repo was renamed from `backdrop-legal` in June 2026. A separate stub repo, `chinalwb/backdrop-legal`, exists solely to redirect the old Pages URLs (the privacy policy URL registered with the Galaxy Store listing pointed there). Do not delete or repurpose that repo.

## Bilingual content — the key convention

Every user-facing string on `index.html` exists twice, wrapped in paired spans:

```html
<span class="t" lang="en">English text</span><span class="t" lang="zh">中文文本</span>
```

CSS hides the inactive language (`html.zh` class on the root element toggles it). The language is auto-detected from `navigator.language` and persisted in `localStorage` under `bm_lang`, applied by an inline script before first paint to avoid a flash. **Any copy change must update both the `lang="en"` and `lang="zh"` spans.**

`privacy-policy.html` uses a different pattern: the full English document followed by the full Chinese document (separated by `<hr>`). Keep both halves in sync, including the effective date.

## Download links appear in multiple places

The Galaxy Store URL (`https://galaxystore.samsung.com/detail/com.chinalwb.backdrop`) and the direct-APK link (`https://github.com/chinalwb/backdrop-me/releases/latest/download/BackdropMe.apk`) each appear several times across `index.html` (nav button, hero CTA, final CTA, footer). The APK link uses `releases/latest`, so publishing a new GitHub release with an asset named exactly `BackdropMe.apk` updates all download buttons automatically — no site edits needed. If either URL ever changes shape, update every occurrence.

## Privacy policy accuracy

The policy describes a two-tier opt-in analytics model (Mixpanel: anonymous usage events, with a separate opt-in for caption text; both off-by-app-consent flows). It is a legal document referenced by the app's store listing — changes must reflect what the app actually does, and the effective date must be bumped in both language sections.
