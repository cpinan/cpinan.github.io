# STATUS — cpinan.github.io

_Last updated: 2026-08-31 · branch `main` · 1 modified file, 1 untracked dir_

## Next action

Repoint the uncommitted donate block in `retro-3d-maze/index.html` at the new `/donate/` page
instead of Corta Spam's `DONATE_ES.md`, then commit it or `git checkout --` it.

## State

- **Static HTML, no build step, no dependencies.** Push to `main` and GitHub Pages serves it.
  Every page inlines its own CSS and SVG; nothing loads from another origin.
- **`index.html` is both the site root and the portfolio/CV**, and is the developer-website URL
  that Play listings and AdMob's `app-ads.txt` crawler resolve to. It must stay a real page —
  never a redirect.
- **`/donate/` is the generic donation page**, added and verified live 2026-08-30 (`be3947c`). Yape and Plin QRs
  plus GitHub Sponsors / Ko-fi / PayPal, app-agnostic copy, states that donating unlocks nothing
  in any app. **Nothing on the site links to it yet.**
- **`/corta-spam/donate/` still exists and is app-specific.** Same layout, same QR images, copy
  naming Corta Spam. Both pages are live; neither links to the other.
- **Nine app cards in `#projects`, ordered live-first.** Seven carry a Play link; Pocket Kit and
  Huellitas al Día sit at the end with a gradient-and-icon cover and no link.
- **`#web` holds four cards**: MiniApps, Turbo Race web, Mis Mascotas, the Tempest tutorial.
- **`#open-source` covers every public repo the account authored** — eleven featured plus fifty
  by theme, equal to the 61 non-fork repos the API reports.
- **Hardcoded facts that go stale in `index.html`**: hero stats (14+ years, 2B+ users, 100+ repos,
  **7** apps on Google Play), per-repo star counts, the "60/61 written by me" and "other 50"
  counts, and the *"seven are live and two are on their way"* note. Verified against the GitHub
  API 2026-08-29 — all correct as of that date.

## In flight

- `.claude/` — untracked, appeared 2026-08-31. Local Claude Code settings, not site content.
  Decide whether to commit it or add it to `.gitignore`; it is not blocking anything.
- `retro-3d-maze/index.html` — +77 uncommitted lines adding a `<h2 id="donate">` section with a
  `.support` block and a `.btn-row`. Predates the 2026-08-29 session. Its Yape/Plin button points
  at `https://github.com/cpinan/Corta-Spam/blob/main/DONATE_ES.md`; `/donate/` is now the right
  target. Either fix and commit, or discard.

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
- **Nothing links to `/donate/` yet.** Candidates: the root `index.html`, each app landing page,
  and the maze donate block above.
- **Pocket Kit's `applicationId` is unknown.** Nothing in this repo records it; grepping
  `pocket-kit/privacy.html` only turns up `com.android.vending.BILLING`. Get it from the app
  project, do not guess.
- **Huellitas al Día was not on Play as of 2026-08-29.** App lives in the private
  `huellitas-al-dia` repo (`~/Projects/VeterinariosApp`); its own `docs/STATUS.md` rules on release
  state. When it goes live: add the Play link, swap the gradient cover for a real
  `assets/covers/` image, move the card up, bump the hero stat to 8, rewrite the section note to
  *"eight are live and one is on its way"*.
- **No `tools/verify.sh`**, and none is warranted — nothing to build or test.

## Do not redo

- **The Flexhire blog post is deliberately not in this repo either.** Written 2026-08-31 for the
  job search, saved to `~/Documents/blog/flexhire-nine-apps.md`. This repo is public and the post
  is unpublished. It is a fill-in sheet for Flexhire's form (title, summary, categories,
  subcategories, content) and every fact in it was read out of `index.html`, so `index.html`
  stays the source — do not let the draft and the site drift. Two items were still open when it
  was saved: no 1200×630 featured image, and nobody confirmed whether the Meta role is past or
  present tense.
- **The LinkedIn post series is deliberately not in this repo.** Eight drafts (seven Play apps
  plus the Tempest code post), a `PLAN.md` calendar and a reusable donation block live in
  `~/Projects/LinkedinPosts/`, which is not a git repo. The user asked twice to keep them local.
  Do not move them under `docs/`, and do not commit them.
- **Every post links `https://cpinan.github.io/donate/`.** That is why the page was pushed while
  the drafts were not.
- **Do not re-diff the site against the GitHub API from scratch.** Done 2026-08-29 across both
  pages of `/users/cpinan/repos?per_page=100` (102 repos, 41 forks, 61 authored, 174 stars). Two
  authored repos were missing and both were added; every star count already on the page was right.
- **Do not try to screenshot or curl the live site from a sandboxed session.** The Chrome
  extension is not connected (`tabs_context_mcp` → "Browser extension is not connected") and
  outbound `curl` returns `000`. Verify from a session with network.
- **MiniApps has no wide cover art.** `assets/pokewheel-cover.png` in that repo is the 512px icon
  renamed, not an 880×430 cover — hence the `cover pad` + gradient pattern.
- **`<code>` has no CSS rule in `index.html`.** Tried inside a repo description and removed; it
  renders in the browser default monospace.
- **User reported not seeing the MiniApps card on 2026-08-29** after it was verified live. Server
  side was ruled out — deployed HTML byte-identical, icon 200, card present six times. Never
  reproduced. Pages sends `cache-control: max-age=600`.
