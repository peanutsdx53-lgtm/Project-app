# YokaiBattlefield Art Presentation Architecture V0.1 — CANDIDATE

Status: parallel UI/UX candidate only. This does not change Formal Current, T9, T10, or mainline Authority.

## Goal
Keep title, HOME, and battle-mode illustrations visually distinctive while making every illustration replaceable without rewriting UI/state logic.

## Screen Roles
- TITLE: first-contact illustration for the whole game. Must communicate modern Japan + yokai + large-scale conflict without belonging to one battle mode.
- HOME: commander base / hub. Neutral enough to receive all battle modes and auxiliary HOME functions.
- KANTO: Kanto-specific visual identity, geography, urban form, local atmosphere, and relevant yokai motifs.
- EAST-WEST: a distinct east-versus-west visual language. Do not reuse the Kanto composition with recoloring.
- WESTERN: foreign/Western-yokai incursion visual language. Distinct silhouette, architecture, sky, palette, and supernatural motifs.

## Stable Replacement Slots
The runtime should reference stable paths only:
- assets/art/title.webp
- assets/art/home.webp
- assets/art/mode-kanto.webp
- assets/art/mode-eastwest.webp
- assets/art/mode-western.webp

Replacing an illustration at the same path must not require changes to navigation, save/resume state, button logic, text, or Motion Language.

## Separation Rules
- No UI labels, mode names, buttons, or explanatory text may be baked into background art.
- UI typography and interaction remain HTML/CSS.
- Art may change independently of UI.
- If an art file is unavailable, the existing CSS fallback background must remain usable.
- Illustration loading must not delay command acceptance.

## Composition Rules
- 16:9 landscape master.
- Prefer at least 1672x941 for current iPhone testing; final masters may be larger.
- Preserve safe visual space for HOME mode controls near the lower area and selected-mode copy on the left.
- Avoid placing critical visual subjects directly under permanent UI.
- Art should support subtle crop/cover changes across landscape devices.

## Regional / Mode Identity Rule
A mode illustration must not be differentiated only by color grading.
Use a combination of:
- recognizable geography / urban morphology / climate / vegetation / coast or mountain character,
- locally appropriate architectural cues,
- yokai or supernatural motifs associated with the place or battle premise,
- distinct foreground/midground/background composition.

The Hokkaido/Okinawa studies established the required degree of visual differentiation even though those are not current HOME mode slots.

## Motion Compatibility
Future art should be separable conceptually into foreground / midground / distant world / atmosphere / yokai-presence layers when useful.
Current Motion Language V1 remains responsible for fog, restrained light breathing, slow parallax, selection feedback, and crossfade timing.

## Current Temporary Mapping
- title.webp: temporary large-torii / all-world-yokai concept.
- home.webp: temporary neutral command-base waterscape.
- mode-kanto.webp: temporary Tokyo Bay / Kanto concept.
- mode-eastwest.webp: temporary Kansai-oriented east-west contrast concept.
- mode-western.webp: temporary blood-moon / foreign-yokai incursion concept.

All five are TEMPORARY and intentionally replaceable after encyclopedia and in-game yokai art direction becomes clearer.
