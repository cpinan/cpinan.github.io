# STATUS — cpinan.github.io

_Last updated: 2026-11-06 · branch `main` · 0 uncommitted files_

## Next action

Open https://cpinan.github.io/ in a browser and eyeball the four new cards (gradients, icon crop,
chip wrap) once Pages has deployed.

## State

- **Static HTML, no build step, no dependencies.** Push to `main` and GitHub Pages serves it.
  Every page inlines its own CSS and SVG; nothing loads from another origin.
- **`index.html` is both the site root and the portfolio/CV**, and is the developer-website URL
  that Play listings and AdMob's `app-ads.txt` crawler resolve to. It must stay a real page —
  never a redirect.
- **`#projects` has 14 Play cards, all linked**, matching the 14 apps in Production on the Play
  Console as of 2026-11-06 (pushed in `5a60ad6`). Hero stat says 14, `sec-note` says "all
  fourteen are live". New cards (Alpaca Solitaire, Cuy Push, Brevete Perú, Calculadora Laboral)
  and Pocket Kit / Huellitas use the `cover pad` + gradient + 192px icon pattern from
  `assets/icons/`; Parabolazo reuses its landing page's inline SVG.
- **`index.html` has a `#donate` section** linking to `/donate/` (seven payment options; QRs are
  Corta Spam's). `/corta-spam/donate/` still exists and is app-specific; neither links to the
  other.
- **`#work` skills grid**: cross-platform card is "Cross-platform, iOS & backend".
- **`#open-source` covers every public repo the account authored** — eleven featured plus
  fifty-three by theme, equal to the 64 non-fork repos the GitHub API reported on 2026-10-09
  (105 public, 181 stars).
- **Hardcoded facts that go stale in `index.html`**: hero stats (14+ years, 2B+ users, 100+
  repos, **14** apps on Google Play), per-repo star counts, the "63 written by me" / "other 52"
  counts. Play Console stats (installs, ratings) are deliberately not shown.

## In flight

Nothing in flight. `stat-calculator/privacy.html` (Firebase Analytics + Crashlytics disclosure,
dated 6 November 2026) was committed in `9f1010d`; confirm the shipped app build really includes
both SDKs.

## Verify

There is no test suite — this is a static site. What actually proves it:

```bash
python3 -m http.server 8777    # then open http://127.0.0.1:8777/?lang=es
```

After pushing, check the real URL and confirm deployed bytes match disk:

```bash
curl -s https://cpinan.github.io/ -o /tmp/live.html && diff index.html /tmp/live.html && echo identical
```

## Open questions

- **Not yet eyeballed in a browser:** the four new cards (gradients, icon crop, chip wrap) and the
  deployed page after the 2026-11-06 push. Only a local HTTP 200 was checked.
- **New-card blurbs are partly inferred.** Alpaca's "card skins and streaks" and "KMP/Compose"
  come from commit history and `~/Projects/CartaBlanca`, Cuy Push's "Godot 4/GDScript" from
  `~/Projects/Sokoban`; confirm they are right. Brevete Perú's landing page is only a policy page.
- **The `/donate/` QR codes are Corta Spam's**, copied byte-for-byte. Regenerate
  `donate/yape-qr.png` and `donate/plin-qr.png` if other apps' donations should go elsewhere.
- **Parabolazo has no public GitHub repo**, so no "Source" link. Confirm whether it stays closed.
- **Old Console entries not shown on purpose:** Turbo Race (`com.carlospinan.turborace`, removed
  by Google) and LOL Champions (suspended). Policy tasks show "2 issues" on the Console home —
  not investigated.

## Do not redo

- **The Flexhire blog post is deliberately not in this repo.** Saved to
  `~/Documents/blog/flexhire-nine-apps.md`, unpublished; the repo is public. Its "eight/nine apps"
  numbers are now wrong (site says 14) — re-check before submitting. `index.html` stays the source.
- **The LinkedIn post series is deliberately not in this repo.** Drafts, `PLAN.md` and donation
  block live in `~/Projects/LinkedinPosts/` (not a git repo). User asked twice to keep them local.
  Do not move under `docs/` or commit.
- **Every LinkedIn post links `https://cpinan.github.io/donate/`**, which also has a nav link from
  the portfolio — keep both current together.
- **Play Console app list was reconciled with the cards on 2026-11-06** (16 total: 14 Production,
  1 removed, 1 suspended). Package ids: `dev.pinan.pocketkit`, `com.cpinan.alpacacards`,
  `com.carlospinan.cuypush`, `com.cpinan.perudriving`, `com.carlospinan.perulaborcalc`,
  `com.carlospinan.huellitasaldia`. The Console app list is a lazy, paginated table: `get_page_text`
  returns only the sidebar, use `find` or screenshots and page 2.
- **Do not re-diff the site against the GitHub API from scratch** unless it has been a while —
  last done 2026-10-09.
- **MiniApps has no wide cover art.** `assets/pokewheel-cover.png` there is the 512px icon
  renamed, hence the `cover pad` + gradient pattern.
- **`<code>` has no CSS rule in `index.html`.** Tried in a repo description and removed.
- **Icons were copied from local project folders, not downloaded from Play** (`sips -z 192 192`).
  Sources: CartaBlanca `docs/assets/v03/icon/play_icon.png`, Sokoban `store/graphics/icon_512.png`,
  PeruDriving `docs/play/assets/icon-512.png`, PeruLaborCalc `docs/listing/assets/icon-512.png`.
