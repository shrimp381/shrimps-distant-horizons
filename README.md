# Shrimp's Distant Horizons

A floating, draggable **parallax horizon** window for Foundry VTT scenes, with layered
depth terrain and a table of draggable Points of Interest (towers, mines, caves, ruins...)
that GMs can place on the horizon and reveal to players over time.

![Screenshot](docs/screenshot.png)

## Status — v1.0.0

The window, layer controls, POI table, day/night toggle, GM/Player view, compact docking,
and custom-image layer uploads all work as tested — and as of v1.0.0, the horizon/POI setup
you build is actually **saved and synced**, not just a local-browser prototype anymore (see
below).

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

**v0.1.3** fixes docking after resizing the window. Dragging the resize handle
sets an explicit `width`/`height` directly on the window; docking never cleared
that leftover size, so the "docked" strip stayed pinned at whatever size it had
last been resized to — a tall box sitting mid-screen — instead of collapsing to
its intended slim bottom-hugging strip. Docking now clears the inline size (and
restores it automatically if you undock again), so a resize survives a dock/undock
cycle without leaking into the docked layout.

**v1.0.0** adds the two things that were missing to make this a real, usable module rather
than a local-browser prototype: **your setup now survives reloading Foundry, and it's
actually shared with your players.**

- **Saved per scene.** The horizon's terrain layers, POIs, palette, horizon length, day/night
  state and view lock are saved on the scene the moment you (the GM) change them. Reload
  Foundry, close and reopen the world, switch away and back to the scene — it's all still
  there. Each scene keeps its own horizon, which fits a multi-leg journey where you're
  swapping scenes as the party travels.
- **Live GM → player sync.** The moment the GM changes something — moves or adds a POI,
  edits a layer, flips day/night — every connected player sees it too, no refresh needed.
  A player who joins partway through the session sees whatever the GM has already set up,
  immediately. This uses Foundry's own scene-sync mechanism (the same thing that keeps
  everyone's view of tokens and lighting in sync) rather than a separate custom connection,
  so it's as reliable as the rest of Foundry.
- **Palette sync, with room for a player's own taste.** The GM's colour palette pushes to
  everyone as the starting look — including a player joining partway through. After that,
  a player is free to pick a different palette for themselves without it being overwritten
  by the GM's *other* changes (a POI move, a layer edit, and so on never touch palette).
  Only the GM's *next* deliberate palette change takes over for everyone again.
- Only an actual GM account can save or push changes — a player toggling the local
  "GM preview" button to poke around the panels can't overwrite the real shared setup;
  their edits just stay local to their own browser and vanish on reload, same as before.
- **Stays per-browser, unchanged:** Free Dock and window position/size, the local GM/Player
  preview toggle, and cosmetic display prefs (compass mode/opacity, drag hint, full-colour
  icons). Those are personal display choices, not part of the shared horizon.
