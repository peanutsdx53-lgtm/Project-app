# YokaiBattlefield Motion Language V1 — CANDIDATE

Status: parallel UI/UX candidate only. This does not change Formal Current, T9, T10, or mainline Authority.

## Purpose
Define one shared motion language for title, HOME, auxiliary panels, later battle preparation, and future combat UI. Motion must improve legibility, feedback, atmosphere, and perceived quality without adding input latency.

## Motion Layers

### L0 Ambient
Purpose: make the world feel alive without asking for attention.
- Typical cycle: 6–30 s.
- Examples: fog drift, restrained light breathing, very slow background/parallax movement.
- No gameplay meaning by itself.
- Pause when hidden by an overlay or when motion is disabled.

### L1 Feedback
Purpose: confirm a direct player action immediately.
- Target onset: same frame as input handling.
- Typical duration: 80–220 ms.
- Examples: 1 px press, short gold sheen, selection sigil response.
- Must never wait for animation completion before changing application state.

### L2 Transition
Purpose: preserve spatial/context continuity between UI states.
- Typical duration: 220–360 ms.
- Examples: title to HOME fade, HOME to detail panel, encyclopedia/records/settings panel entrance.
- Different screens may vary direction subtly, but all use the same timing family.

### L3 World Change
Purpose: communicate a change in selected battle/world context.
- Typical duration: 550–800 ms.
- Example: Kanto / East-West / Western battle background crossfade.
- UI selection and labels update immediately; world visual catches up asynchronously.

### L4 Event
Purpose: high-importance game events only.
- Reserved for battle start, objective resolution, colossal events, major front collapse/breakthrough, etc.
- Must not be used for normal menu navigation.
- Audio/haptic synchronization will be specified with the combat event contract later.

## Performance Rules
- Prefer transform and opacity.
- Do not create large continuous particle DOM systems.
- At most two visually strong animation systems should compete at once.
- Hidden HOME ambient animation pauses behind overlays.
- No animation may intentionally delay command/state acceptance.
- Reduced-motion and in-game Motion OFF must disable nonessential animation.
- Final layered illustration motion must be designed for mobile GPU budgets and tested on iPhone Safari/PWA.

## Current D13 Timing Tokens
- Press: 110 ms
- Feedback: 190 ms
- Panel transition: 280 ms
- World crossfade: 700 ms

## Art Direction
Movement should feel like modern Japan overlapped by the supernatural: quiet fog, night air, restrained gold reflection, distant yokai presence. Avoid futuristic HUD motion, excessive gacha-style sparkle, constant full-screen flashing, and movement that competes with command readability.

## Audio / Haptic Boundary
Current SE remains temporary timing-validation audio. UI will emit semantic interaction categories rather than bind final sounds directly. Formal BGM/SE production remains a later stage after gameplay states and combat flow are concrete.
