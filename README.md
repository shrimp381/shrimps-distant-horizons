# Shrimp's Distant Horizons

A floating, draggable **parallax horizon** window for Foundry VTT scenes, with layered
depth terrain and a table of draggable Points of Interest (towers, mines, caves, ruins...)
that GMs can place on the horizon and reveal to players over time.

![Screenshot](docs/screenshot.png)

## Status — v0.1.2 (prototype)

This first release ports the working **UI and interaction prototype** into a loadable
Foundry module: the window, layer controls, POI table, day/night toggle, GM/Player view,
compact docking, and custom-image layer uploads all work exactly as tested. It is **not
yet wired to real Foundry scene/canvas data** — nothing here is read from or saved to
your actual scenes yet.

**Compatibility: Foundry v13+.** This module targets Foundry's current (v13) UI going
forward; v11/v12 are no longer the design target (see v0.1.2 below for why that matters).

**v0.1.1** fixed the docked (compact) window spanning the full width of the screen and
passing behind the hotbar, sidebar and any popped-out windows. It measures Foundry's real
scene-controls column, sidebar and hotbar and docks the strip between them, sitting above
the hotbar and **centred**, with equal breathing room on both sides for other modules' own
toolbar buttons or panels.

It also added:
- **Free Dock** (Settings → Docking) — drag the docked strip to any position on your own
  screen instead of the auto-centred spot, using the small handle above it. This is a
  per-browser preference (a client-scoped Foundry setting), not shared with other players.
- A **resizable window** — drag the bottom-right corner while undocked to grow it; it
  won't shrink smaller than its shipped default size.

**v0.1.2** fixes the docked strip collapsing to zero width and snapping to the dead centre
of the screen on **Foundry v13**. v13 substantially restructured the UI landmarks v0.1.1's
centred-docking measurement relied on: `#ui-left` is no longer the narrow toolbar itself
but a much wider layout wrapper (scene controls + scene navigation columns), and `#sidebar`
collapses to zero width until a tab is expanded (the visible strip becomes a child element
instead). Trusting those landmark elements' own bounding boxes — which is what v11/v12
required — wildly overshot on v13, collapsing the available width to nothing. The fix
measures the actual *visible children* of those landmarks instead of the landmarks
themselves, which tracks whatever is really painted on screen on any Foundry version.

**What ships pre-populated vs. blank:**
- The 6 horizon **layers** come with sensible default terrain (a mix of mountains, forest
  and hills) so there's something to look at immediately — edit, reorder, or replace any
  of them from the Layers panel.
- **Points of Interest start empty.** POIs are scenario-specific, so nothing is placed for
  you — use "+ Add POI" to place your own.
