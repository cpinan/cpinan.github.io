# STATUS — cpinan.github.io

_Last updated: 2026-08-29 · branch `main` · 1 uncommitted file_

## Next action

Decide what to do with the uncommitted donate block in `retro-3d-maze/index.html` — it was
already in the working tree when this session opened and is the only thing not pushed.

## State

- **Static HTML, no build step, no dependencies.** Push to `main` and GitHub Pages serves
  it. Every page inlines its own CSS and SVG; nothing loads from another origin.
- **`index.html` is both the site root and the portfolio/CV**, and is the developer-website
  URL that Play listings and AdMob's `app-ads.txt` crawler resolve to. It must stay a real
  page — never a redirect.
- **Nine app cards in `#projects`, ordered live-first.** Seven carry a Play link; Pocket Kit
  and Huellitas al Día sit at the end with a gradient-and-icon cover and no link.
- **`#web` now holds four cards**: MiniApps (first), Turbo Race web, Mis Mascotas, the
  Tempest tutorial. `.grid.three` wraps the fourth onto a second row — that is fine.
- **`#open-source` covers every public repo the account authored.** Eleven featured entries
  plus fifty in the by-theme list equals the 61 non-fork repos the API reports; the site's
  own repo is one of the fifty.
- **Hardcoded facts that go stale in `index.html`**: hero stats (14+ years, 2B+ users, 100+
  repos, **7** apps on Google Play), the per-repo star counts, the "60/61 written by me"
  and "other 50" counts, and the *"seven are live and two are on their way"* note. Verified
  against the GitHub API on 2026-08-29 — all correct as of that date.

## In flight

- `retro-3d-maze/index.html` — +77 uncommitted lines adding a `<h2 id="donate">` section
  with a `.support` block and a `.btn-row`. Not written this session; it predates it.
  Either commit it or `git checkout --` it.

## Verify

There is no test suite — this is a static site. What actually proves it:

```bash
python3 -m http.server 8777    # then open http://127.0.0.1:8777/?lang=es
```

After pushing, check the real URL rather than the local one, and confirm the deployed bytes
match what is on disk:

```bash
curl -s https://cpinan.github.io/ -o /tmp/live.html && diff index.html /tmp/live.html && echo identical
```

## Open questions

- **Pocket Kit's `applicationId` is unknown.** Nothing in this repo records it — grepping
  `pocket-kit/privacy.html` only turns up `com.android.vending.BILLING`. It blocks the
  Pocket Kit row in the README *Shortcuts* table. Get it from the app project, do not guess.
- **Huellitas al Día was not on Play as of 2026-08-29.** The app lives in the private
  `huellitas-al-dia` repo (local path `~/Projects/VeterinariosApp`); its own `docs/STATUS.md`
  is the source of truth for release state. When the listing goes public: add the Play link,
  swap the gradient cover for a real `assets/covers/` image, move the card up with the live
  ones, bump the hero stat to 8, and rewrite the section note to *"eight are live and one is
  on its way"*.
- **User reported not seeing the MiniApps card on 2026-08-29**, after it was verified live.
  Server side was ruled out — deployed HTML byte-identical to local, icon 200, card present
  six times. Unresolved on the client side; it was never reproduced. If it comes back, the
  card is the first one under *"Open it in a browser"* (`https://cpinan.github.io/#web`),
  below the nine Play cards, and Pages sends `cache-control: max-age=600`.
- **No `tools/verify.sh`**, and none is warranted — there is nothing to build or test. The
  commands above are the raw ones.

## Do not redo

- **Do not re-diff the site against the GitHub API from scratch.** It was done on 2026-08-29
  across both pages of `/users/cpinan/repos?per_page=100` (102 repos, 41 forks, 61 authored,
  174 stars). Exactly two authored repos were missing and both were added. The star counts
  already on the page were all correct — checking them again finds nothing.
- **Do not try to screenshot the live site from here.** The Chrome extension is not
  connected in this environment: `tabs_context_mcp` returns "Browser extension is not
  connected". Verify with `curl` and `diff` instead.
- **MiniApps has no wide cover art.** `assets/pokewheel-cover.png` in that repo is the 512px
  icon under another name, not a 880×430 cover. The card therefore uses the
  `cover pad` + gradient pattern with `assets/icons/miniapps.png` (the pokewheel 192px icon).
- **`<code>` has no CSS rule in `index.html`.** A `<code>` tag was tried inside a repo
  description and removed again — no other entry uses one, and it renders in the browser
  default monospace.
