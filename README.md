# cpinan.github.io

**Live site: <https://cpinan.github.io/>**

GitHub Pages site: my **portfolio / CV**, in English and Spanish, plus the landing
pages and privacy policies for every app. Static HTML only — no build step, no
dependencies. Push to `main` and GitHub Pages publishes it at that URL within a minute
or two.

Preview it locally with a server, not `file://` — asset paths are absolute:

```sh
python3 -m http.server 8777    # then open http://127.0.0.1:8777/?lang=es
```

Each app gets a folder with two pages:

| file | purpose |
| --- | --- |
| `<app>/index.html` | Landing / marketing page. What the app does, feature list, support email. |
| `<app>/privacy.html` | Privacy policy. The URL pasted into the Play Console listing. |

## Shortcuts

| App | Landing page | Privacy policy | Play listing |
| --- | --- | --- | --- |
| Corta Spam | [/corta-spam/](https://cpinan.github.io/corta-spam/) | [/corta-spam/privacy.html](https://cpinan.github.io/corta-spam/privacy.html) | `org.carlospinan.cortaspam` |
| Piano Solfeo | [/piano-solfeo/](https://cpinan.github.io/piano-solfeo/) | [/piano-solfeo/privacy.html](https://cpinan.github.io/piano-solfeo/privacy.html) | not public yet |
| Retro 3D Maze | [/retro-3d-maze/](https://cpinan.github.io/retro-3d-maze/) | [/retro-3d-maze/privacy.html](https://cpinan.github.io/retro-3d-maze/privacy.html) | `com.carlospinan.maze3d` |
| Stat Calculator | [/stat-calculator/](https://cpinan.github.io/stat-calculator/) | [/stat-calculator/privacy.html](https://cpinan.github.io/stat-calculator/privacy.html) | `com.cpinan.pokemmostats` |
| Turbo Race | [/turbo-race/](https://cpinan.github.io/turbo-race/) | [/turbo-race/privacy.html](https://cpinan.github.io/turbo-race/privacy.html) | `com.carlos.pinan.turborace.godot` |
| Peru Combi Rush | — | [/peru-rush-combi-privacy.html](https://cpinan.github.io/peru-rush-combi-privacy.html) | `com.carlos.pinan.perucombirush.godot` |
| Piano Flashcards *(renamed)* | redirect → Piano Solfeo | redirect → Piano Solfeo | — |

Site root — the portfolio: <https://cpinan.github.io/>

Live pages the portfolio links out to, **served from other repos**, not this one:

| What | URL |
| --- | --- |
| Turbo Race, playable web build | <https://cpinan.github.io/turbo-race-godot/> |
| Mis Mascotas, memorial PWA | <https://cpinan.github.io/mis-mascotas/> |
| Building Tempest, 19-chapter tutorial | <https://cpinan.github.io/Tempest-Jetpack-Compose/tutorial.html> |

Those paths are owned by their own project sites — creating a folder of the same
name here would be dead content that never gets served.

## What each file is

### Root

- **`index.html`** — Site root, and the **portfolio / CV page**, in English and
  Spanish. Sections: hero headline (drawn from the LinkedIn profile — Staff Engineer
  at Meta, WhatsApp media infrastructure), *What I do* (four areas), *Apps on Google
  Play* (cover image, description, Play link, landing page, privacy policy), *Open it
  in a browser* (things with a live URL — the Turbo Race web build, the Mis Mascotas
  PWA, the Tempest tutorial), *Repositories I wrote* (the ten worth reading, then an
  *Also on GitHub* block grouping the other 49 self-authored repos by theme — forks are
  excluded, and repos that follow a book, course or someone else's game say so
  inline), an experience timeline and a contact block. This is also
  the **developer website** URL that the Play Console listings and AdMob's
  `app-ads.txt` crawler resolve to, so it has to stay a real page — it must not become
  a redirect again.

  **Both languages live in this one file.** Every translated string is a
  `<span class="en">` next to a `<span class="es">`; CSS on `html[data-lang]` hides one
  set, and the EN/ES switch in the top bar flips the attribute, persists the choice in
  `localStorage` and writes `?lang=` to the URL. First visit picks Spanish when
  `navigator.language` starts with `es`. Never split this into two files — edit the
  pair of spans together, or the two languages drift apart.

  Facts on this page are hardcoded and go stale: the star counts in the repo list, the
  hero stats (14+ years, 2B+ users, 95+ repos, 5 apps on Google Play), and the job
  history. Update them when an app goes live or is pulled, or when a role changes.
  Piano Solfeo is listed **without** a Play link because its listing is not public yet
  — add one when it is.

  The playable Turbo Race build is **not** in this repo: the Godot web export lives
  in its own `turbo-race-godot` repo and GitHub Pages serves it at
  `/turbo-race-godot/`. That project site owns the path — adding a folder of the
  same name here would be dead content that never gets served. The `turbo-race/`
  folder here is the app's landing page and policy, and links out to it.

- **`assets/`** — the only images on the site. `covers/` holds 880 px-wide JPEGs
  downscaled from each app's 1024×500 Play feature graphic (plus `tempest.jpg`, a
  strip composed from four screenshots, and `brickbreaker.gif`, the demo GIF from
  that repo). `icons/` holds 192 px PNG app icons. `turbo-race/` holds the four
  screenshots used on the Turbo Race landing page. Sources live in each app's own
  project folder — regenerate rather than edit these in place.
- **`app-ads.txt`** — Required by Google Play / AdMob to authorize the AdMob
  publisher ID (`pub-8297579382369512`) to sell inventory in the apps. Must stay
  at the domain root and be reachable as plain text. Do not delete or rename.
- **`peru-rush-combi-privacy.html`** — Privacy policy for **Peru Combi Rush**, a
  Godot driving game. Predates the folder-per-app convention, so it sits at the
  root as a single bilingual (EN/ES) page. Covers AdMob advertising ID, Firebase
  Analytics + crash logs, and optional Google Play Games sign-in. Last updated
  28 July 2026. The Play listing points at this exact URL — keep the filename.

### `corta-spam/` — Corta Spam (open-source call blocker, Android)

- **`index.html`** — Landing page, Spanish-first with English subtitles. Explains
  the rule engine (blocked/allowed numbers, wildcard patterns, country matching,
  quiet hours, repeat-call rules, bundled offline spam list), the own call log,
  the stats, JSON backup, and the experimental auto-responder. Links to the MIT
  source at [github.com/cpinan/Corta-Spam](https://github.com/cpinan/Corta-Spam).
- **`privacy.html`** — Bilingual ES/EN policy. The headline claim: the app does
  not declare the internet permission, so it cannot make a network request, and
  it opts out of Android auto-backup. No ads, no tracking. Last updated 8 August 2026.

### `piano-solfeo/` — Piano Solfeo (sight-reading and music theory, Android)

- **`index.html`** — Landing page in Spanish with an English summary section.
  Eight practice modes (treble/bass clef notes, chords, intervals, scales, circle
  of fifths, theory, interactive keyboard), Do-Re-Mi vs C-D-E naming, streaks,
  optional daily reminder, fully offline.
- **`privacy.html`** — Bilingual ES/EN policy. No accounts, no ads, no analytics;
  practice history stays on the device. Last updated 7 August 2026.

### `piano-flashcards/` — legacy redirect folder

The app was renamed from *Piano Flashcards* to *Piano Solfeo*, but the old
privacy URL was already live in the Play listing and elsewhere. Both
**`index.html`** and **`privacy.html`** are identical stub pages: a canonical
link plus a meta-refresh to `https://cpinan.github.io/piano-solfeo/privacy.html`,
with a one-line note that the app changed its name. No content of their own.
Keep them until the old URL is provably unreferenced.

### `retro-3d-maze/` — Retro 3D Maze (maze screen saver / game, Android)

- **`index.html`** — Landing page in English, styled after a mid-90s desktop UI
  to match the app. Describes the four modes (screen saver, play, live wallpaper,
  Android Daydream), the eleven maze algorithms, five sizes, runtime-drawn texture
  packs plus custom images, and the map/hint/autopilot features. Also states the
  ad placement up front (banner under the settings dialog; interstitial only on
  return from a maze, every third time; none during play, wallpaper or screen saver).
- **`privacy.html`** — Bilingual EN/ES policy. Covers AdMob, the advertising ID,
  and the EEA/UK consent flow reopenable from *Ad privacy* in settings. No
  accounts, no analytics, no crash reporting. Last updated 9 August 2026 — the
  most recently revised policy on the site.

### `stat-calculator/` — Stat Calculator (Pokémon stat calculator, Android)

- **`index.html`** — Landing page in English. All nine generations (DVs/Stat Exp
  for Gen I–II, IVs/EVs/natures from Gen III), 1,025 Pokémon with base stats
  cached from [PokéAPI](https://pokeapi.co) for offline use, build comparison,
  20 saved builds, formula reference, six languages. Carries the unofficial
  fan-project disclaimer (not affiliated with Nintendo, Game Freak, Creatures Inc.
  or The Pokémon Company).
- **`privacy.html`** — Bilingual EN/ES policy. Ad-supported: sets out what the ad
  SDK collects, plus the Android backup behaviour. No accounts, no analytics;
  builds stay on the device. Last updated 8 August 2026.

### `turbo-race/` — Turbo Race (endless runner, Android + web)

- **`index.html`** — Landing page in English, dark neon palette matching the game.
  Four screenshots, the Play listing's feature copy (tilt or joystick, three
  difficulties, Play Games leaderboards, 20 achievements), and the rewrite story:
  originally cocos2d-x/C++ (source still public at
  [BTEndlessTunnel](https://github.com/cpinan/BTEndlessTunnel)), now Godot 4.7 with
  statically typed GDScript. Links out to the playable WebAssembly build at
  `/turbo-race-godot/`.
- **`privacy.html`** — Bilingual EN/ES policy, copied from `privacy-policy.html` in
  the `turbo-race-godot` project repo and translated into Spanish here. Covers
  AdMob (advertising ID, EEA/UK consent form) and optional Play Games sign-in; best
  score per difficulty and the mute flag stay on the device. Last updated 15 July
  2026 — carried over from the source policy, whose wording is unchanged.

  The source repo still serves its own copy at `/turbo-race-godot/privacy-policy.html`.
  If the policy ever changes, **both** have to be updated.

## Conventions

- **Folder per app**, lowercase kebab-case, matching the app name. New apps follow
  this; only Peru Combi Rush predates it.
- **`index.html` = landing, `privacy.html` = policy.** Play Console gets the
  `privacy.html` URL.
- **Bilingual policies.** Every policy carries both English and Spanish, in full,
  in one page — two `<h1>` sections rather than two files, so a single URL serves
  both audiences.
- **Self-contained pages.** All CSS is inlined in a `<style>` block; decorative
  icons are inline SVG. Nothing is loaded from another origin — no CDN stylesheets,
  fonts, scripts or hotlinked images. Photographic assets are committed under
  `assets/` and served from this domain, so the pages render identically offline.
- **Styling follows the app.** Each page reuses its app's palette, so the policy
  looks like it belongs to the thing that linked to it.
- **A dated "Last updated" line** in each policy. Update it whenever the app's
  data collection changes — that date is what a reviewer checks.
- **URLs are permanent.** Once a path is in a Play listing it cannot be moved.
  Renaming an app means adding a redirect stub at the old path (see
  `piano-flashcards/`), never deleting it.

## Editing

```bash
# preview locally
python3 -m http.server 8000     # then open http://localhost:8000

# publish
git add . && git commit -m "..." && git push
```

Pages go live within a minute or two of the push. Verify the real URL afterwards —
a page that renders locally can still 404 if the path or the branch is wrong.
