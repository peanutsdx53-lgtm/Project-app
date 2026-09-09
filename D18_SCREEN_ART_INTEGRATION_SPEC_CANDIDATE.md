# YokaiBattlefield D18 Screen / Art Integration Spec — CANDIDATE

Status: parallel UI/UX candidate only. This does not change Formal Current, T9, T10, or mainline Authority.

## Purpose
Define the stable screen/art boundary for the current prototype so title, HOME, and battle-mode illustrations can be replaced later without changing navigation, state persistence, Motion Language, or gameplay logic.

## Core rule
Art is replaceable content. UI and application state must not be baked into illustration files.

- Text, buttons, selected-state frames, version labels, prompts, settings, and mode descriptions remain HTML/CSS.
- Background illustration files may be replaced independently.
- Art replacement must not require changes to screen IDs, session state, lifecycle logic, viewport stabilization, or navigation behavior.
- A missing or failed art asset must fail closed to a dark fallback background; controls must remain readable and usable.

## Stable art slots
Current candidate paths:

- `assets/art/title.webp`
- `assets/art/home.webp`
- `assets/art/mode-kanto.webp`
- `assets/art/mode-eastwest.webp`
- `assets/art/mode-western.webp`

These paths are interface slots, not final art identity. The images currently prepared for them are TEMPORARY_ART and may be replaced later.

## Screen roles

### Title
Role: the entrance to the whole game, not a battle-mode screen.
- Uses the dedicated title slot.
- Must communicate the overall premise: modern Japan, yokai, territorial / strategic conflict, supernatural overlap.
- Title logo, tagline, and tap prompt remain separate from the art.
- Final title art should reserve a quiet central field for the logo.

### HOME — neutral state
Role: the commander's common base / hub before a battle mode is selected.
- Uses the dedicated HOME slot.
- Must not visually belong only to Kanto, Kansai, Hokkaido, Okinawa, or any single mode.
- Mode buttons and utility functions remain in a fixed layout.

### HOME — battle mode selected
Selecting a mode updates UI state immediately and crossfades the background to that mode's art slot.

- Kanto -> `mode-kanto.webp`
- East-West -> `mode-eastwest.webp`
- Western Yokai -> `mode-western.webp`

The UI layout must not move just because the art changes.

### Mode detail
Mode detail keeps the selected mode's illustration as spatial continuity and places a dark readability layer over it.
- Only the selected mode is presented.
- Other mode buttons are not shown inside the detail panel.
- Returning to HOME restores the same selected-mode state.

### Encyclopedia / Records / Settings
These are global HOME functions, not battle areas.
- They appear as overlays/panels.
- The previously visible HOME scene may remain underneath as context, but must be sufficiently dimmed.
- Closed panels are `hidden/display:none` and cannot remain interactive or visible behind HOME.

## Regional individuality requirement
A mode image must not be a palette swap of another region.

Regional identity should be built from a combination of:
- terrain and coastline / basin / mountain form,
- cityscape and settlement density,
- climate and season,
- vegetation,
- architecture and recognizable regional visual language,
- lighting / weather,
- yokai with relevant geographic, folkloric, or narrative association.

Examples: Kanto, Kansai, Hokkaido, and Okinawa should be recognizable as substantially different spaces even if all use the same overall visual style.

## Layout safe zones
Current prototype UI assumes:
- upper-left / left-center quiet zone for selected mode title and description,
- bottom-center band for three mode controls,
- bottom-right band for encyclopedia / records / settings,
- central title-screen quiet zone for logo.

Temporary art may violate these zones; final art should be composed with them in mind rather than covered afterward with heavy opaque panels.

## Motion contract
Current single-raster images are temporary. Final art should be compatible with later layer separation:

1. far background / sky,
2. terrain / city,
3. focal yokai or supernatural presence,
4. mist / cloud / atmospheric layer,
5. foreground framing layer,
6. optional light / supernatural FX layer.

Not every image needs all layers. Motion must follow Motion Language V1:
- L0 Ambient only for slow environmental life,
- L3 for mode-to-mode world crossfade,
- no animation may delay state acceptance.

## Performance / quality target
- 16:9 source composition.
- Temporary minimum: 1672 x 941.
- Later production target should be chosen after iPhone GPU/memory tests; higher resolution is allowed but not automatically better.
- Avoid low-resolution full-screen raster upscaling.
- Prefer optimized WebP/AVIF where browser support and quality are acceptable.
- Do not preload an unlimited future art library at startup; title and HOME should take priority, mode art can be staged/cached.

## Current implementation boundary
D17 remains the stable live runtime while the D18 art slots are prepared.
D18 may be promoted only after all required art-slot files exist and title -> HOME -> mode selection -> mode detail has been regression-tested on iPhone PWA.
