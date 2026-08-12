# cpinan.github.io

GitHub Pages site serving landing pages and privacy policies for my Android apps.
Static HTML only — no build step, no dependencies. Push to `main` and GitHub Pages
publishes it at <https://cpinan.github.io/>.

Each app gets a folder with two pages:

| file | purpose |
| --- | --- |
| `<app>/index.html` | Landing / marketing page. What the app does, feature list, support email. |
| `<app>/privacy.html` | Privacy policy. The URL pasted into the Play Console listing. |

## Shortcuts

| App | Landing page | Privacy policy |
| --- | --- | --- |
| Corta Spam | [/corta-spam/](https://cpinan.github.io/corta-spam/) | [/corta-spam/privacy.html](https://cpinan.github.io/corta-spam/privacy.html) |
| Piano Solfeo | [/piano-solfeo/](https://cpinan.github.io/piano-solfeo/) | [/piano-solfeo/privacy.html](https://cpinan.github.io/piano-solfeo/privacy.html) |
| Retro 3D Maze | [/retro-3d-maze/](https://cpinan.github.io/retro-3d-maze/) | [/retro-3d-maze/privacy.html](https://cpinan.github.io/retro-3d-maze/privacy.html) |
| Stat Calculator | [/stat-calculator/](https://cpinan.github.io/stat-calculator/) | [/stat-calculator/privacy.html](https://cpinan.github.io/stat-calculator/privacy.html) |
| Turbo Race *(separate repo)* | [/turbo-race-godot/](https://cpinan.github.io/turbo-race-godot/) | — |
| Peru Combi Rush | — | [/peru-rush-combi-privacy.html](https://cpinan.github.io/peru-rush-combi-privacy.html) |
| Piano Flashcards *(renamed)* | redirect → Piano Solfeo | redirect → Piano Solfeo |

Site root: [cpinan.github.io](https://cpinan.github.io/) — hub page linking every app.

## What each file is

### Root

- **`index.html`** — Site root. A hub page listing every app with links to its
  landing page and privacy policy. This is the **developer website** URL that the
  Play Console listings and AdMob's `app-ads.txt` crawler resolve to, so it has to
  stay a real page — it must not become a redirect again.

  Turbo Race is listed here but is **not** in this repo: the Godot web build lives
  in its own `turbo-race-godot` repo and GitHub Pages serves it at
  `/turbo-race-godot/`. That project site owns the path — adding a folder of the
  same name here would be dead content that never gets served.
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

## Conventions

- **Folder per app**, lowercase kebab-case, matching the app name. New apps follow
  this; only Peru Combi Rush predates it.
- **`index.html` = landing, `privacy.html` = policy.** Play Console gets the
  `privacy.html` URL.
- **Bilingual policies.** Every policy carries both English and Spanish, in full,
  in one page — two `<h1>` sections rather than two files, so a single URL serves
  both audiences.
- **Self-contained pages.** All CSS is inlined in a `<style>` block, icons are
  inline SVG. No external stylesheets, fonts, scripts or images — the pages render
  identically offline and there is nothing to break when a CDN moves.
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
