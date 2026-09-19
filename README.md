# Shrimp's Distant Horizons

A floating, draggable **parallax horizon** window for Foundry VTT scenes, with layered
depth terrain and a table of draggable Points of Interest (towers, mines, caves, ruins...)
that GMs can place on the horizon and reveal to players over time.

![Screenshot](docs/screenshot.png)

## Status — v0.1.0 (prototype)

This first release ports the working **UI and interaction prototype** into a loadable
Foundry module: the window, layer controls, POI table, day/night toggle, GM/Player view,
compact docking, and custom-image layer uploads all work exactly as tested. It is **not
yet wired to real Foundry scene/canvas data** — nothing here is read from or saved to
your actual scenes yet.

**What ships pre-populated vs. blank:**
- The 6 horizon **layers** come with sensible default terrain (a mix of mountains, forest
  and hills) so there's something to look at immediately — edit, reorder, or replace any
  of them from the Layers panel.
- **Points of Interest start empty.** POIs are scenario-specific, so nothing is placed for
  you — use "+ Add POI" to place your own.

**Roadmap** (not in this release):
- Persist each scene's horizon/POI configuration in scene flags, so it saves and loads per-scene
- Let a POI link to an actual Journal Entry, opening it on click
- Sync GM/Player state and view-lock over Foundry's socket layer instead of local-only state
- Use `game.settings` for any world-level defaults

## Installing in Foundry VTT

**Manifest URL** (after you've pushed this to GitHub — see below):

```
https://raw.githubusercontent.com/shrimp381/shrimps-distant-horizons/main/module.json
```

In Foundry: **Add-on Modules → Install Module**, paste that URL into the **Manifest URL**
field, and click **Install**. Then enable it from your world's **Manage Modules** list.

Once enabled, open a scene and look in the **Notes** controls group (the same toolbar
group journal pins live in, on the left-hand side of the canvas) for a mountain-range
icon — click it to show or hide the Distant Horizons window.

## Project structure

```
shrimps-distant-horizons/
├── module.json              Foundry module manifest
├── scripts/
│   └── distant-horizons.js  All UI logic (esmodule)
├── styles/
│   └── distant-horizons.css
├── assets/
│   ├── shrimp-logo.png
│   ├── forest-hand-1.png
│   └── forest-hand-2.png
├── docs/
│   └── screenshot.png
├── LICENSE
└── README.md
```

---

## Publishing this to GitHub

These are the exact steps to get this folder onto GitHub as a repository Foundry can
install from. You only need a free GitHub account and Git installed on your computer
(`git --version` in a terminal to check).

### 1. Create the repository on GitHub

1. Go to [github.com/new](https://github.com/new).
2. **Repository name:** `shrimps-distant-horizons` (matches the folder name and the `id`
   in `module.json` — keeping these identical avoids confusion later).
3. Set it to **Public** (Foundry needs to fetch the manifest and files over a public URL).
4. **Do not** tick "Add a README" or ".gitignore" — this folder already has them.
5. Click **Create repository**. Keep the page open — it shows the exact remote URL you'll
   need in step 3 below.

### 2. Fill in your GitHub username

Before pushing, open `module.json` and `README.md` in this folder and replace every
`YOUR_GITHUB_USERNAME` with your actual GitHub username (4 places in `module.json`, 2 in
this README).

### 3. Push this folder to GitHub

Open a terminal, `cd` into this folder (the one containing `module.json`), then run:

```bash
git init
git add .
git commit -m "Initial release: v0.1.0 prototype"
git branch -M main
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/shrimps-distant-horizons.git
git push -u origin main
```

If you're prompted for a password, GitHub no longer accepts your account password for
this — use a [Personal Access Token](https://github.com/settings/tokens) instead (or set
up the GitHub CLI / SSH keys, which avoids the prompt entirely).

### 4. Create a Release with a `module.zip` attached

Foundry's package installer (and the `download` field in `module.json`) expects a
zipped copy of the module attached to a GitHub Release — not the repository itself.

From inside this folder:

```bash
zip -r module.zip module.json scripts styles assets docs LICENSE README.md -x ".*"
```

Then on GitHub:

1. Go to your repo → **Releases** (right-hand sidebar) → **Create a new release**.
2. **Tag:** `v0.1.0` (must match the `version` in `module.json`).
3. **Release title:** `v0.1.0 — Initial prototype`.
4. Drag `module.zip` into the "Attach binaries" box at the bottom.
5. Click **Publish release**.

The `download` URL in `module.json` (`.../releases/latest/download/module.zip`) will now
resolve automatically to this file, and stays correct for every future release you tag
`latest` — no need to edit it again.

### 5. Verify the manifest is reachable

Paste this into a browser (with your username filled in) — it should show the raw JSON,
not a 404:

```
https://raw.githubusercontent.com/YOUR_GITHUB_USERNAME/shrimps-distant-horizons/main/module.json
```

That URL is what you (or anyone else) pastes into Foundry's **Install Module → Manifest
URL** field.

---

## Updating the module later

Whenever you make changes locally:

```bash
git add .
git commit -m "Describe what changed"
git push
```

If the change should count as a new version Foundry users can upgrade to:

1. Bump `"version"` in `module.json` (e.g. `0.1.0` → `0.2.0`).
2. Commit and push that change.
3. Re-zip (`zip -r module.zip ...` as above) and create a **new** GitHub Release tagged
   to match (e.g. `v0.2.0`) with the new `module.zip` attached.

Foundry checks the `manifest` URL's `version` field against what's installed and offers
an update when they differ, then downloads whatever the `download` URL points to — which
is always your latest release's `module.zip`.

## Listing it on Foundry's official package directory (optional)

Once you're happy with a release, you can submit the module at
[foundryvtt.com/community/manage-packages](https://foundryvtt.com/community/manage-packages)
using the same manifest URL from step 5 above. That makes it searchable from inside
Foundry's own module browser rather than requiring the manifest URL to be pasted in by
hand.
