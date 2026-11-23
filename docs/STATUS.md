# STATUS — cpinan.github.io

_Last updated: 2026-11-22 · branch `main` · 0 uncommitted files_

## Next action

Eyeball the live page (https://cpinan.github.io/#projects) for the two new cards (TvRadio, Last Ascent) and confirm the Last Ascent / TvRadio chips are right.

## State

- **Static HTML, no build step, no dependencies.** Push to `main` and GitHub Pages serves it.
  Every page inlines its own CSS and SVG; nothing loads from another origin.
- **`index.html` is both the site root and the portfolio/CV**, and is the developer-website URL
  that Play listings and AdMob's `app-ads.txt` crawler resolve to. It must stay a real page —
  never a redirect.
- **`#projects` has 16 Play cards, all linked**, matching the 16 apps on the Play developer page
  as of 2026-11-22 (pushed in `af02951`, live and byte-identical). Hero stat says 16, `sec-note`
  says "all sixteen are live". Newest cards: TvRadio (`com.carlospinan.tvradio`) and Last Ascent
  (`com.cpinan.lastascent`, source project `~/Projects/TowerRPG`). Cards use the `cover pad` +
  gradient + 192px icon pattern from `assets/icons/`; Parabolazo reuses its landing page's inline SVG.
- **`index.html` has a `#donate` section** linking to `/donate/` (seven payment options; QRs are
  Corta Spam's). `/corta-spam/donate/` still exists and is app-specific; neither links to the
  other.
- **`#open-source` covers every public repo the account authored** — eleven featured plus
  fifty-two by theme, equal to the 63 non-fork repos GitHub reported on 2026-11-22
  (104 public, 184 stars; page says "180+").
- **Hardcoded facts that go stale in `index.html`**: hero stats (14+ years, 2B+ users, 100+
  repos, **16** apps on Google Play), per-repo star counts on the 11 featured cards (not rechecked
  on 2026-11-22), the "63 written by me" / "other 52" counts. Play Console stats (installs,
  ratings) are deliberately not shown.

## In flight

Nothing in flight. `stat-calculator/privacy.html` (Firebase Analytics + Crashlytics disclosure,
dated 6 November 2026, commit `9f1010d`): confirm the shipped app build really includes both SDKs.

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

- **Not yet eyeballed in a browser:** the new TvRadio and Last Ascent cards (gradients, icon crop,
  chip wrap). Only local and live HTTP 200s and the byte-diff were checked on 2026-11-22; a
  page-inspection JS call was blocked by the browser tool.
- **Card blurbs/chips are partly inferred.** Last Ascent's "Godot 4" chip comes from
  `~/Projects/TowerRPG/godot/`; TvRadio's KMP/Compose/Media3/Chromecast chips from its README.
  Alpaca's "card skins and streaks" and Cuy Push's "Godot 4/GDScript" were inferred earlier.
- **One public repo vanished since 2026-10-09** (64 → 63 non-fork). Not identified; the page links
  no dead repo.
- **The `/donate/` QR codes are Corta Spam's**, copied byte-for-byte. Regenerate
  `donate/yape-qr.png` and `donate/plin-qr.png` if other apps' donations should go elsewhere.
- **Parabolazo has no public GitHub repo**, so no "Source" link. Confirm whether it stays closed.
- **Old Console entries not shown on purpose:** Turbo Race (`com.carlospinan.turborace`, removed
  by Google) and LOL Champions (suspended). Policy tasks show "2 issues" on the Console home —
  not investigated.

## Do not redo

- **The Flexhire blog post is deliberately not in this repo.** Saved to
  `~/Documents/blog/flexhire-nine-apps.md`, unpublished; the repo is public. Its "eight/nine apps"
  numbers are now wrong (site says 16) — re-check before submitting. `index.html` stays the source.
- **The LinkedIn post series is deliberately not in this repo.** Drafts, `PLAN.md` and donation
  block live in `~/Projects/LinkedinPosts/` (not a git repo). User asked twice to keep them local.
  Do not move under `docs/` or commit.
- **Every LinkedIn post links `https://cpinan.github.io/donate/`**, which also has a nav link from
  the portfolio — keep both current together.
- **Play app list reconciled with the cards on 2026-11-22** from the public developer page
  (16 apps). Console showed 16 total on 2026-11-06 incl. 1 removed, 1 suspended — those are not on
  the public page. Package ids: `dev.pinan.pocketkit`, `com.cpinan.alpacacards`,
  `com.carlospinan.cuypush`, `com.cpinan.perudriving`, `com.carlospinan.perulaborcalc`,
  `com.carlospinan.huellitasaldia`, `com.carlospinan.tvradio`, `com.cpinan.lastascent`.
  Fast way to list the public page: navigate to it, then JS-collect `a[href*="details?id="]`.
  The Console app list is a lazy, paginated table: `get_page_text` returns only the sidebar.
- **Do not re-diff the site against the GitHub API from scratch** unless it has been a while —
  last done 2026-11-22 (all 63 non-fork repos linked).
- **MiniApps has no wide cover art.** `assets/pokewheel-cover.png` there is the 512px icon
  renamed, hence the `cover pad` + gradient pattern.
- **`<code>` has no CSS rule in `index.html`.** Tried in a repo description and removed.
- **Icons are copied from local project folders, not downloaded from Play** (`sips -z 192 192`).
  Sources: CartaBlanca `docs/assets/v03/icon/play_icon.png`, Sokoban `store/graphics/icon_512.png`,
  PeruDriving `docs/play/assets/icon-512.png`, PeruLaborCalc `docs/listing/assets/icon-512.png`,
  TvRadio `docs/store/graphics/icon_512.png`, TowerRPG `art/store-refresh/play_app_icon_512.png`.
- **BSD sed on macOS:** use `sed -i ''`; plain `sed -i` fails.
