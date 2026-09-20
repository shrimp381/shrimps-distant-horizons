# Shrimp's Distant Horizons

A floating, draggable **parallax horizon** window for Foundry VTT scenes, with layered
depth terrain and a table of draggable Points of Interest (towers, mines, caves, ruins...)
that GMs can place on the horizon and reveal to players over time.

![Screenshot](docs/screenshot.png)

## Status — v0.1.1 (prototype)

This first release ports the working **UI and interaction prototype** into a loadable
Foundry module: the window, layer controls, POI table, day/night toggle, GM/Player view,
compact docking, and custom-image layer uploads all work exactly as tested. It is **not
yet wired to real Foundry scene/canvas data** — nothing here is read from or saved to
your actual scenes yet.

**v0.1.1** fixes the docked (compact) window spanning the full width of the screen and
passing behind the hotbar, sidebar and any popped-out windows. It now measures Foundry's
real scene-controls column, sidebar and hotbar and docks the strip between them, sitting
above the hotbar and **centred**, with equal breathing room on both sides for other
modules' own toolbar buttons or panels.

It also adds:
- **Free Dock** (Settings → Docking) — drag the docked strip to any position on your own
  screen instead of the auto-centred spot, using the small handle above it. This is a
  per-browser preference (a client-scoped Foundry setting), not shared with other players.
- A **resizable window** — drag the bottom-right corner while undocked to grow it; it
  won't shrink smaller than its shipped default size.

## Installing in Foundry VTT

**Manifest URL** (after you've pushed this to GitHub — see below):

```
https://raw.githubusercontent.com/Shrimp381/shrimps-distant-horizons/main/module.json
```

In Foundry: **Add-on Modules → Install Module**, paste that URL into the **Manifest URL**
field, and click **Install**. Then enable it from your world's **Manage Modules** list.

Once enabled, open a scene and look in the **Notes** controls group (the same toolbar
group journal pins live in, on the left-hand side of the canvas) for a mountain-range
icon — click it to show or hide the Distant Horizons window.

