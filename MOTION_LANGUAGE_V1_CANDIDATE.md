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
- Examples: title to HOME fade and content-only entrance for mode detail / encyclopedia / records / settings.
- Overlay roots are not animated on iOS PWA; only visible child content may animate.
- Closed screens must be removed from rendering with hidden/display:none rather than being left transparent.

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

## State-Isolation Rules
These rules were added after D13–D15 iOS PWA regressions.
- A closed screen must not remain interactive or renderable behind another screen.
- Child elements may never override the hidden state of a closed parent screen.
- Overlay close is immediate at the state level; no delayed close timer may be allowed to bleed into the next screen.
- Entry animation is decorative only and never owns application state.
- HOME ambient animation pauses whenever an overlay is active.
- Restored screens must appear in their stable state first; resume must not replay full entry animation.

## Cold Start / Resume Rules
D16 candidate lifecycle contract:
- Cold Start: show the title screen.
- Normal background resume: preserve the current screen without routing through title.
- Same-session WebKit reload/discard: restore HOME, selected battle mode, mode detail, encyclopedia, records, or settings from sessionStorage.
- Screen-state persistence is session-only. Do not store current screen in long-term localStorage.
- Missing or corrupt resume state fails closed to the title screen.
- Restoring a screen must not replay UI SE or haptics.
- Web-only limitation: a browser/PWA cannot perfectly distinguish every user force-quit from every OS/WebKit process discard if the platform preserves session data. D16 uses sessionStorage as the safest practical approximation and must be verified on iPhone PWA.

## Performance Rules
- Prefer transform and opacity.
- Do not create large continuous particle DOM systems.
- At most two visually strong animation systems should compete at once.
- Hidden HOME ambient animation pauses behind overlays.
- No animation may intentionally delay command/state acceptance.
- Reduced-motion and in-game Motion OFF must disable nonessential animation.
- Final layered illustration motion must be designed for mobile GPU budgets and tested on iPhone Safari/PWA.

## Current D16 Timing Tokens
- Press: 110 ms
- Feedback: 190 ms
- Panel entry: 280 ms
- World crossfade: 700 ms

## Art Direction
Movement should feel like modern Japan overlapped by the supernatural: quiet fog, night air, restrained gold reflection, distant yokai presence. Avoid futuristic HUD motion, excessive gacha-style sparkle, constant full-screen flashing, and movement that competes with command readability.

## Audio / Haptic Boundary
Current SE remains temporary timing-validation audio. UI will emit semantic interaction categories rather than bind final sounds directly. Formal BGM/SE production remains a later stage after gameplay states and combat flow are concrete.
