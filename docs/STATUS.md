# STATUS — cpinan.github.io

_Last updated: 2026-08-27 · branch `main` · 0 uncommitted files_

## Next action

Add the Pocket Kit row to the README *Shortcuts* table — it is the one app with a folder
here but no row, and it was skipped only because its `applicationId` is not recorded
anywhere in this repo.

## State

- **Static HTML, no build step, no dependencies.** Push to `main` and GitHub Pages serves
  it. Every page inlines its own CSS and SVG; nothing loads from another origin.
- **Nine app cards in `#projects`, ordered live-first.** Seven carry a Play link; **Pocket
  Kit** and **Huellitas al Día** sit at the end with a gradient-and-icon cover and no link.
- **Bendiciones went live on Play 2026-08-27** (`com.cpinanbuenosdias.app`) — card has the
  Play link and a real cover, landing page has a download button.
- **Huellitas al Día has a landing page and a policy here, but is not on Play.** Its copy
  is drawn from the app repo's `STORE.md` / `docs/STATUS.md`, and states two limits out
  loud because the app does: no backup, and the derived schedule covers dogs and cats only.
- **`index.html` is both the site root and the portfolio/CV**, and is the developer-website
  URL that Play listings and AdMob's `app-ads.txt` crawler resolve to. It must stay a real
  page — never a redirect.
- **Facts in `index.html` are hardcoded and go stale**: hero stats (14+ years, 2B+ users,
  95+ repos, **7** apps on Google Play), the repo star counts, and the *"seven are live and
  two are on their way"* section note. All three move together when an app ships.

## In flight

Nothing in flight. Working tree clean, everything pushed.

## Verify

There is no test suite — this is a static site. What actually proves it:

```bash
python3 -m http.server 8777    # then open http://127.0.0.1:8777/?lang=es
```

Then, after pushing, confirm the real URLs rather than the local ones:

```bash
curl -s -o /dev/null -w "%{http_code}\n" https://cpinan.github.io/<app>/
```

## Open questions

- **Pocket Kit's `applicationId` is unknown.** Nothing in this repo records it — grepping
  `pocket-kit/privacy.html` only turns up `com.android.vending.BILLING`. It blocks the
  README row above. Get it from the app project, do not guess it.
- **Huellitas al Día was not submitted to Play as of 2026-08-27.** The app lives in the
  private `huellitas-al-dia` repo (local path `~/Projects/VeterinariosApp`); its own
  `docs/STATUS.md` is the source of truth for release state, not this file. When the
  listing goes public: add the Play link, swap the gradient cover for a real
  `assets/covers/` image, move the card up with the live ones, bump the hero stat to 8 and
  rewrite the section note to *"eight are live and one is on its way"*.
- **No `tools/verify.sh` in this repo**, and none is warranted — there is nothing to build
  or test. The commands above are the raw ones.

## Do not redo

- **Do not split `index.html` into one file per language.** Both languages live in that one
  file as paired `<span class="en">` / `<span class="es">`; CSS on `html[data-lang]` hides
  one set. Editing the pair together is what keeps them from drifting.
- **Do not create a `turbo-race-godot/` folder here.** That path is owned by the project
  site of the same name and is already served from its own repo — a folder here would be
  dead content that never gets served. Same for `mis-mascotas/`.
- **Do not move or rename `peru-rush-combi-privacy.html`.** It sits at the root, predating
  the folder-per-app convention, because that exact URL is registered in the Play listing.
- **Do not delete `piano-flashcards/`.** Both files are redirect stubs for the app's old
  name, and the old privacy URL is already published. Deleting them 404s a live address.
- **Do not curl the live URL straight after a push and conclude it failed.** GitHub Pages
  took ~40 s on 2026-08-27 — two polls returned 404 before the third returned 200. Retry
  in a loop before investigating.
- **Do not hand-build cover images.** They are downscales of each app's 1024×500 Play
  feature graphic, and `sips` does it in one line — the result is 880×429, so declare that
  height on the `<img>` rather than the 430 the older covers use:
  `sips -Z 880 -s format jpeg -s formatOptions 82 <feature>.png --out assets/covers/<app>.jpg`
- **Do not add a second handoff file.** This path, `docs/STATUS.md`, is the only one.
