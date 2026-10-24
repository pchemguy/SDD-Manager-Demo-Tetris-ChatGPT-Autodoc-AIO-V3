# Component decomposition

## Ownership map

This document refines [ARCHITECTURE](ARCHITECTURE.md). Components are logical responsibilities, not mandatory classes or one-file-per-component rules. The browser entry composes concrete adapters once; no plugin or service-container framework is required.

| ID / component | Owns and provides | Requires / excludes | Verification seam |
| --- | --- | --- | --- |
| D1 Geometry and pieces | Tetromino cells/orientations, bounds and occupied-cell checks, rotation candidates and canonical landing projection for regular and penetrator modes. | Receives board and piece values; owns no score, timers, DOM or mutable session. | Explicit boards/pieces, including cavities, overlap and boundary rotations. |
| D2 Piece supply | Upcoming queue, regular random supply and 7-bag construction/refill. Returns one next piece and a stable preview. | Receives random samples through a supplied function; no global random or renderer state. | Scripted samples or seeded test generator; bag permutations and queue consumption. |
| D3 Game transition | Authoritative game state and command processing: move, rotate, descend, hard drop, Hold, activate, restart and elapsed time. Commits locks, clears, awards and spawn atomically. | D1, D2 and D4; accepts typed settings and time. No browser or storage reads. | Snapshot-based state fixtures and command/time sequences. |
| D4 Progression | Line-clear score, level and gravity interval calculation. | Pure numeric inputs; no board mutation or timers. | Boundary totals and gravity-floor calculations. |
| C1 Settings schema/resolver | Six typed settings, defaults, legal values, source-by-source parsing and independent precedence. Returns resolved settings plus explicit valid URL selections to persist. | Raw URL/cookie input through ports. No browser globals, timers or board knowledge. | Invalid, omitted, duplicated and explicit-default source fixtures. |
| C2 Settings coordinator | Selected settings, user changes, startup persistence effects and independent write failures. Exposes settings and concise persistence status. | C1 and cookie/URL ports. Owns no domain piece-policy snapshot. | Memory ports with independent read/write failure injection. |
| S1 Session controller | Domain instance, command ordering, active clock reference, held inputs, setting application, restart and disposal. Exposes typed actions and read-only view state. | D3, C2, monotonic clock/input and view ports. No duplicated gameplay rules. | Fake clock and action streams, including pause, blur and exact deadlines. |
| V1 Board renderer | Canvas sizing, settled/active/ghost cell drawing and consistent nonwhite regular/white penetrator styles. | Read-only view state and presentation palette. Does not compute another landing. | Captured view models plus actual-browser render assertions/screenshots. |
| V2 Panel and status | Score, level, line count, next/Hold previews, bonus symbols, session controls, six settings and effective-policy notices. | View state, settings and controller actions; no direct domain mutation. | Label/focus/state assertions through DOM/browser interactions. |
| A1 Input/clock adapters | Key mapping, repeat scheduling, focus exclusions, blur notification and monotonic elapsed-time observations. | Browser event and animation APIs; calls S1 actions. No lock or score decisions. | Owned event listeners, controlled timestamps and disposal checks. |
| A2 Cookie/URL adapters | Raw reads and narrow writes preserving unrelated URL state, cookie serialization and browser error translation. | Document cookie, location and History APIs. No setting precedence. | Real-browser origin/reload checks plus fake API failures. |

## State boundaries

D3 owns settled cells, active piece and activation flag, queue/supply, Hold slot and per-piece availability, score/level/line totals, bonus count, lifecycle status and grounded elapsed/deadline state. D2's supply state is embedded in that authoritative game state rather than mirrored in a panel. D4 derives progression; it does not retain a second mutable score.

C2 owns selected settings. D3 retains an effective locking-policy snapshot for each spawned piece; current visibility/availability settings may change immediately. S1 is the only bridge between them. V2 displays both selected and effective policies when they differ, and enabling/disabling Hold never deletes the stored slot.

The clock adapter reports monotonic time. S1 advances the domain before timestamped gameplay commands, drops paused elapsed time and clears held repeats on blur, pause, restart and disposal. D3 processes scheduled gravity and lock events in time order. Rendering may be coalesced without dropping domain events. Inputs and snapshots must not expose mutable aliases to the authoritative board.

## Design-level interface shape

D1 accepts a board plus `{kind, orientation, x, y, mode}` and returns occupied cells, legal transformation candidates, or a landing placement/absence. D3 accepts a state plus an ordered command and transition context, returning the next state and presentation-relevant effects. Supply samples are explicit transition dependencies; deterministic tests never depend on global random state.

C1 resolves a raw source snapshot to typed settings, source provenance and startup write intents. C2 executes each persistence intent independently and retains in-memory selection when an adapter fails. A2 reports unavailable/failed operations without leaking browser exceptions into gameplay. S1 composes these interfaces and builds one view snapshot containing the domain's projected landing.

Exact enums, input rejection semantics, timer ordering, settings encodings and acceptance belong in SPEC. The design interfaces express responsibilities rather than prescribing a public package API.

## Critical collaborations

A movement/rotation command is checked by D1 and accepted by D3 only as a coherent transition. A penetrator may overlap settled cells during downward traversal, but lateral/rotation candidate acceptance requires a clear, safe placement. D3 never locks without revalidating the final placement. A failed activation or Hold command changes neither bonus count, queue, Hold slot nor lock timer.

For locking, D3 validates the active placement, merges it, clears full rows, calls D4, awards any bonus, consumes D2's next piece and validates spawn. Panels observe only the completed result. The same D1 landing result drives gravity stopping, hard drop and ghost view; V1 applies visibility and drawing without re-solving geometry.

On settings startup, C1 resolves all sources independently; C2 writes valid explicit URL values to cookies. On user change, C2 updates memory and attempts both cookie and URL writes. S1 receives the selected typed settings, applies current-piece availability/visibility and retains existing effective locking policies until the next spawn.

## Review outcome

All architectural responsibilities have one state owner and an explicit consumer. Domain and settings logic can be checked without browser installation. Cross-block coupling is confined to S1 and typed snapshots/ports; adapters do not depend on domain internals. Geometry centralizes shared landing knowledge; no duplicated ghost/hard-drop calculation is introduced. No additional component hierarchy is needed for the accepted scope.
