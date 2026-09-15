# STATUS — cpinan.github.io

_Last updated: 2026-09-15 · branch `main` · 0 modified files, 1 untracked dir_

## Next action

Decide whether Pocket Kit or Huellitas al Día ships next — when either gets a Play link, add the
card's `play` link, bump the hero stat from 8 to 9, and rewrite the projects `sec-note` ("eight
are live" → "nine are live and one is on its way").

## State

- **Static HTML, no build step, no dependencies.** Push to `main` and GitHub Pages serves it.
  Every page inlines its own CSS and SVG; nothing loads from another origin.
- **`index.html` is both the site root and the portfolio/CV**, and is the developer-website URL
  that Play listings and AdMob's `app-ads.txt` crawler resolve to. It must stay a real page —
  never a redirect.
- **Ten app cards in `#projects`, ordered live-first.** Eight carry a Play link (Parabolazo added
  2026-09-15); Pocket Kit and Huellitas al Día sit at the end with a gradient-and-icon cover and
  no link.
- **`parabolazo/index.html` now links Google Play** instead of saying "coming soon" — it had
  shipped but the landing page hadn't been updated to say so.
- **`index.html` has a `#donate` section** (animated gradient border + bobbing ☕, respects
  `prefers-reduced-motion`) and a nav entry, linking to `/donate/`. Previously nothing on the
  site linked there.
- **`/donate/` lists seven payment options**: Yape/Plin QRs, GitHub Sponsors, Ko-fi, PayPal,
  Revolut (`revolut.me/carlosgd80`), Wise (`wise.com/pay/me/carlosp4173`), Monzo
  (`monzo.me/carlospinanindacochea`) — the last three added 2026-09-15.
- **`/corta-spam/donate/` still exists and is app-specific.** Same layout, same QR images, copy
  naming Corta Spam. Both pages are live; neither links to the other.
- **`#work` skills grid**: the cross-platform card is now "Cross-platform, iOS & backend" and
  also claims FastAPI/Python backend work and cloud deployment (chips: React, React Native,
  Flutter, iOS/Swift, KMP, FastAPI, Cloud).
- **`#open-source` covers every public repo the account authored** — eleven featured plus
  fifty-two by theme, equal to the 63 non-fork repos the GitHub API reports as of 2026-09-15
  (104 public repos total, 178 stars). `godot-skyroads` and `CustomModForPokeMMO` were the two
  missing and were added under a new "Godot & game modding" theme group.
- **Hardcoded facts that go stale in `index.html`**: hero stats (14+ years, 2B+ users, 100+
  repos, **8** apps on Google Play), per-repo star counts, the "63 written by me" / "other 52"
  counts, and the *"eight are live and two are on their way"* note. Verified against the GitHub
  API 2026-09-15 — all correct as of that date.

## In flight

- `.claude/` — untracked, appeared 2026-08-31, still undecided. Local Claude Code settings, not
  site content. Decide whether to commit it or add it to `.gitignore`; it is not blocking
  anything.

## Verify

There is no test suite — this is a static site. What actually proves it:

```bash
python3 -m http.server 8777    # then open http://127.0.0.1:8777/?lang=es
```

After pushing, check the real URL and confirm deployed bytes match disk:

```bash
curl -s https://cpinan.github.io/donate/ -o /tmp/live.html && diff donate/index.html /tmp/live.html && echo identical
```

## Open questions

- **The `/donate/` QR codes are Corta Spam's, copied byte-for-byte.** If donations for the other
  apps should land in a different account, regenerate `donate/yape-qr.png` and `donate/plin-qr.png`.
- **Pocket Kit's `applicationId` is unknown.** Nothing in this repo records it; grepping
  `pocket-kit/privacy.html` only turns up `com.android.vending.BILLING`. Get it from the app
  project, do not guess.
- **Huellitas al Día was not on Play as of 2026-08-29.** App lives in the private
  `huellitas-al-dia` repo (`~/Projects/VeterinariosApp`); its own `docs/STATUS.md` rules on
  release state.
- **Parabolazo has no public GitHub repo**, so its open-source card has no "Source" link (unlike
  Corta Spam). Confirm whether it's meant to stay closed-source before adding one.
- **No `tools/verify.sh`**, and none is warranted — nothing to build or test.

## Do not redo

- **The Flexhire blog post is deliberately not in this repo either.** Written 2026-08-31 for the
  job search, saved to `~/Documents/blog/flexhire-nine-apps.md`. This repo is public and the post
  is unpublished. It is a fill-in sheet for Flexhire's form (title, summary, categories,
  subcategories, content) and every fact in it was read out of `index.html`, so `index.html`
  stays the source — do not let the draft and the site drift. It predates the Parabolazo card and
  the "eight apps" count, so re-check its numbers before submitting.
- **The LinkedIn post series is deliberately not in this repo.** Eight drafts (seven Play apps
  plus the Tempest code post), a `PLAN.md` calendar and a reusable donation block live in
  `~/Projects/LinkedinPosts/`, which is not a git repo. The user asked twice to keep them local.
  Do not move them under `docs/`, and do not commit them.
- **Every LinkedIn post links `https://cpinan.github.io/donate/`.** That page now also gets a
  direct nav link from the portfolio itself, so keep both current together.
- **Do not re-diff the site against the GitHub API from scratch** unless it's actually been a
  while — done 2026-09-15 across all repo pages (`/users/cpinan/repos?per_page=100`, 104 public,
  63 authored non-fork, 178 stars). Two authored repos were missing from the site and both were
  added; every star count already on the page was right.
- **MiniApps has no wide cover art.** `assets/pokewheel-cover.png` in that repo is the 512px icon
  renamed, not an 880×430 cover — hence the `cover pad` + gradient pattern.
- **`<code>` has no CSS rule in `index.html`.** Tried inside a repo description and removed; it
  renders in the browser default monospace.
- **Parabolazo's project card reuses its landing page's inline SVG hero** as the cover image
  instead of a new `assets/covers/*.jpg` + `assets/icons/*.png` pair, because no such assets
  exist for that app. Follow the same approach for Pocket Kit/Huellitas only if they also lack
  real cover art when they ship.
