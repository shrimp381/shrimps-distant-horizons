# Shrimp's Distant Horizons

A floating, draggable **parallax horizon** window for Foundry VTT scenes, with layered
depth terrain and a table of draggable Points of Interest (towers, mines, caves, ruins...)
that GMs can place on the horizon and reveal to players over time.

![Screenshot](docs/screenshot.png)

**Compatibility: Foundry v13+.**

## Features

- **Parallax terrain horizon.** Six independently configurable depth layers (colour,
  speed, scale, vertical/horizontal offset, enable/disable) built from either procedural
  biomes (mountains, hills, desert) or an image — either a built-in preset or your own
  upload. Layers drag sideways at different speeds to give the horizon a sense of depth.
- **Custom layer & POI images, stored the Foundry way.** Upload your own artwork for any
  layer or POI icon — it's saved through Foundry's own `FilePicker` into the world's Data
  storage, not embedded as bloated inline data. Layer images support optional **seamless
  mirror tiling** (guarantees a jump-free loop for any image) and **tint-to-layer-colour**
  (off keeps the image's own colours, for full-colour art).
- **Points of Interest.** Add, name, resize (S/M/L) and drag-position POIs on any layer,
  each with a built-in icon or your own uploaded image. Each POI tracks a discovery state
  (Hidden / Unknown / Rumored / Discovered) the GM can advance as the party explores, and
  can be locked in place once positioned. Click a POI to centre the horizon on it.
- **Day/Night toggle** — swaps the horizon's lighting mood with one click.
- **9 colour palettes** (Obsidian & Brass, Verdant Camp, Crimson Watch, Arcane Violet,
  Ancient Parchment, Desert Sands, Hellscape, Shadow, Feywild) plus 3 **horizon length**
  presets (Far / Medium / Close) trading drag distance for reach.
- **Compass overlay** — full (cardinal + degrees), simple (cardinal only), or hidden, with
  adjustable opacity and an optional drag hint.
- **GM/Player view preview.** The GM can preview exactly what a connected player's window
  looks like without leaving their own session.
- **View lock** — the GM can lock the horizon's scroll position so players can't drag it
  around themselves.
- **Compact docking.** Collapse the window into a slim strip that docks centred above the
  hotbar, correctly measured against Foundry's own scene-controls, sidebar and hotbar so it
  never overlaps them. **Free Dock** lets you drag that strip to any position on your own
  screen instead of the auto-centred spot.
- **Resizable, repositionable window** with a "reset position" option, on top of Foundry's
  own `ApplicationV2` window lifecycle (position memory, minimize/restore).
- **Saved per scene.** The horizon's terrain layers, POIs, palette, horizon length,
  day/night state and view lock save automatically the moment the GM changes them, and
  persist across reloads. Each scene keeps its own independent horizon setup — a natural
  fit for a multi-leg journey where scenes change as the party travels.
- **Live GM → player sync.** Every change the GM makes — a POI move, a layer edit, a
  palette push, day/night — appears on every connected player's screen immediately, using
  Foundry's own scene-sync mechanism. A player joining partway through the session sees
  whatever's already set up. A player who picks their own palette keeps it until the GM
  deliberately pushes a new one.
- **Permission-gated.** Only a real GM account can see or use the editing controls
  (layers, POIs, settings' GM-only sections) at all — a real player's client never even
  renders that markup, and only a GM can save or push changes.
- **Fully localized** via `game.i18n` — every user-facing string resolves through
  `lang/en.json`; adding another language is a matter of dropping in a new
  `lang/<code>.json` with the same keys.
- **Stays per-browser, by design:** Free Dock's on/off state and dragged position, window
  size/position, and cosmetic display prefs (compass mode/opacity, drag hint, full-colour
  icons) are personal display choices, not part of the shared horizon — they're never
  saved to the scene or pushed to anyone else.

**What ships pre-populated vs. blank (on a scene with no saved setup yet):** the 6 horizon
layers come with sensible default terrain (a mix of mountains, forest and hills) so
there's something to look at immediately. **Points of Interest start empty** — they're
scenario-specific, so nothing is placed for you; use "+ Add POI" to place your own.

## Installing in Foundry VTT

**Manifest URL:**

```
https://raw.githubusercontent.com/Shrimp381/shrimps-distant-horizons/main/module.json
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
│   └── distant-horizons.js  ApplicationV2 app class + hooks (esmodule)
├── templates/
│   ├── window.hbs           Main window PART
│   ├── settings.hbs         Settings dropdown PART
│   ├── layers-info.hbs      Layers-info popup PART
│   ├── layer-row.hbs        Registered partial (one terrain layer row)
│   └── poi-row.hbs          Registered partial (one POI table row)
├── lang/
│   └── en.json               Localization strings (game.i18n)
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

