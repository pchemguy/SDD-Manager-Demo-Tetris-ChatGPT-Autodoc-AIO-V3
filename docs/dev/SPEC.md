# Behavioral specification

## Scope, owners and vocabulary

The game fulfills [PROJECT](PROJECT.md) using the boundaries in [ARCHITECTURE](ARCHITECTURE.md) and [DECOMPOSITION](DECOMPOSITION.md). D1–D4 own game rules, S1 owns ordered browser-session actions, V1/V2 own presentation, and C1/C2 with A2 own settings. This specification describes the complete intended game; PLAN selects the contracts included in each useful delivery increment.

A board has 10 columns and 20 visible rows. Coordinates increase rightward and downward, starting at `(0,0)`. Only occupied tetromino cells count for collision, bounds and midline tests; empty cells in an orientation matrix do not. There are no hidden rows. A placement is **clear** when every occupied cell is in bounds and does not overlap settled cells. Regular support means the next downward placement is not clear. A penetrator's landing/support uses G-08 instead.

The focused [geometry contract](spec/GEOMETRY.md) owns spawn matrices, rotation and kick values. The [configuration contract](spec/CONFIGURATION.md) owns settings encodings and persistence. They are normative parts of this specification.

## G-01 — Classic board and lifecycle

Start/New game creates an empty board, score/lines zero, level 1, no held piece, zero bonuses and a fresh piece supply. The first piece spawns immediately in its canonical orientation and spawn location. Status is running, paused or game over. Each accepted lock merges exactly four cells, removes all completed rows simultaneously, shifts surviving rows downward without changing cell order, fills vacated top rows with empty cells, applies progression/bonus effects, and spawns the next piece atomically.

A blocked spawn ends the game. Keep the settled board and final counters, remove the active piece and stop gameplay time; never truncate an overlapping spawn into the board. Invalid gameplay commands are no-ops with no partial counter, queue or timer changes. New game is available from any status and retains selected configuration. Gameplay commands other than pause/resume/restart are ignored while paused or game over.

Acceptance: a scripted game can move/rotate/drop multiple pieces, clear one through four rows, update progression, reach blocked-spawn game over and restart cleanly. Cleared rows and counters are visible in the next view snapshot.

## G-02 — Keyboard and session time

Use Left/Right for horizontal movement, Down for soft drop, Up or X for clockwise rotation, Z for counterclockwise rotation, Space for hard drop, C or Shift for Hold, B for penetrator activation, and P or Escape for pause/resume. Provide labelled Start/New game and Pause/Resume HTML controls and visible key help. Suppress browser scrolling for handled gameplay keys only when the game input surface is active.

Horizontal/Down inputs act once on keydown. Held horizontal input repeats after 150 ms, then every 50 ms; held Down repeats every 50 ms. Only the most recently pressed horizontal direction repeats; releasing it while the opposite remains held restarts that direction's 150 ms delay. Ignore OS-generated key repeats and duplicate physical keydowns. Rotation, Hold, activation, hard drop and pause act once per physical press. Either alias key releases independently; alias handling must not create duplicate held-input streams.

When a settings/form/button control or editable element has focus, its keys retain normal control behavior and no gameplay hotkeys fire. Page blur or hidden visibility pauses a running game, clears held inputs and requires explicit resume. Pausing freezes gravity and grounded elapsed time. Resume uses a new monotonic clock reference; paused/background time causes no catch-up. Restart/disposal also clears held inputs and releases obsolete listeners/animation resources.

Advance domain time to an input's timestamp before applying that input. At equal times, an expired lock deadline precedes gravity, then the input is processed against the resulting current state. Process elapsed scheduled events in chronological order; a late render frame cannot skip required locks or row clears. Regressing/nonfinite time observations do not advance the game. Rendering cadence cannot change these outcomes.

Acceptance: fixed command/time sequences produce the same result at different rendering cadences. Blur, focused controls, key repeat, pause at a deadline and repeated session creation/disposal do not cause stuck keys, duplicate actions or immediate catch-up locks.

## G-03 — Motion, rotation and piece supply

Horizontal and soft-down moves change one cell per accepted action. Reject out-of-bounds or overlapping regular placements without consuming supply or altering the board. Rotation follows the ordered candidates in the geometry contract; select the first valid candidate and otherwise retain the original placement. There is no 180-degree rotation. Failed inputs do not reset gravity scheduling or grounded elapsed time.

The complete game uses 7-bag randomization: each consecutive bag contains each kind I, J, L, O, S, T and Z exactly once, with a fresh random permutation. Refill without losing or duplicating a kind. The next preview shows exactly the next queued kind in canonical orientation, without consuming it. Supply randomness is injectable for verification; no public seed/URL control is required. A classic delivery increment may use independent uniform kind selection before 7-bag is delivered, as identified in PLAN.

Acceptance: each aligned seven-piece bag is a permutation; bag boundaries and preview reads preserve queue order. Spawn, rotation near walls/floor/ceiling and a fully blocked kick sequence match the geometry fixtures.

## G-04 — Score, level and gravity

A lock clearing 1/2/3/4 lines awards 100/300/500/800 times the level immediately before the clear. A zero-line lock awards zero. Total lines determine `level = 1 + floor(totalLines / 10)` after scoring. Gravity interval in milliseconds is `max(50, floor(1000 * 0.8 ** (level - 1)))`. There are no combo, back-to-back, spin or drop-distance points.

A spawned piece schedules its first automatic downward step one current gravity interval later. Successful movement, soft drop, rotation and delayed hard drop do not restart this cadence. At lock, spawn starts the next piece's cadence using the updated level. Each scheduled gravity step attempts one row; full-interval locking may finish before that next gravity event.

Acceptance: 9 to 10 total lines changes level after scoring at the old level; a subsequent clear uses the new level. Gravity never falls below 50 ms, and changing render cadence or repeated blocked inputs does not change scoring/speed.

## G-05 — Hold and preview

When enabled and the active piece is not a penetrator, allow Hold once before that piece locks. Empty Hold stores the current kind and consumes the next queued kind; occupied Hold exchanges kinds without consuming the queue. The entering piece spawns in canonical orientation/location, with fresh gravity/ground timing and a snapshot of selected locking policies. Hold is then unavailable until a normal post-lock spawn. Failed/disabled Hold changes nothing. A blocked entering spawn ends the game under G-01; the accepted exchange itself remains reflected in Hold/supply.

Hold stores a kind only, never orientation, position, activation or a lock timer. An activated penetrator cannot be held. Disabling Hold preserves its slot and per-piece used state; re-enabling it grants no additional use. Hiding the next preview changes presentation only.

Acceptance: empty/occupied Hold, repeat Hold rejection, lock reset, disabled/re-enabled Hold, active-penetrator rejection and blocked entering spawn preserve the stated queue and slot behavior.

## G-06 — Ghost and hard drop

Compute one canonical projected landing from the active piece. The ghost depicts that exact kind/orientation/placement with an outline or translucent style distinguishable from settled and active cells. When active and ghost coincide, preserve active-piece legibility. White is reserved for penetrators; their ghost uses a distinguishable white outline/translucency, not a nonwhite regular-piece identity.

Always-hide suppresses the ghost; always-show displays any valid projection. Dynamic mode displays it only if its topmost occupied projected row is at least 10. A projection occupying rows 9 and 10 is hidden; one whose topmost row is 10 is shown. Never classify by matrix origin, center or active-piece height. No active piece or no valid landing means no ghost.

Enabled hard drop moves directly to the canonical landing. General locking continues under G-07 unless the active piece's hard-drop policy is immediate, in which case it locks during that same command. Hard drop at an already grounded placement does not restart timing. Disabled hard drop is a complete no-op. Ghost visibility never affects movement or locking.

Acceptance: ghost and hard-drop target match for regular and penetrator pieces, including cavities. Exercise projected rows 9/10, hidden mode, coincident pieces, zero-distance hard drop and both locking policies.

## G-07 — Grounded locking

A new active piece snapshots selected general and hard-drop locking policies, including a piece entering via Hold. Changes to those selected settings affect the next such spawn; current-piece policies are retained and visibly explained.

In interval mode, becoming supported starts a deadline one full current gravity interval after that contact. This includes support discovered immediately after spawn or a move/drop. Lock at the deadline if still supported and the placement is clear. Moves/rotations/blocked attempts and repeated hard drops do not refresh the deadline while support remains. Losing support cancels it; a later contact starts a fresh interval. Pause freezes remaining time. Evaluate support after each successful transformation; use the gravity interval at contact for the entire deadline.

In failed-down mode, a failed automatic or soft-down attempt locks a clear supported piece immediately. Contact alone starts no timer. A following-policy hard drop relocates the piece and waits for the next failed downward attempt, retaining the automatic gravity cadence. The immediate hard-drop policy locks on that command, irrespective of general mode. No policy may lock a transient overlapping penetrator.

Acceptance: for contact at game time 1000 with interval 1000, the piece remains active at 1999 and locks at 2000. Grounded lateral/rotation/drop commands do not postpone 2000; moving off support cancels it. Pause for arbitrary wall time preserves remaining delay. Exact-deadline input, failed soft-down and automatic failures exercise both policies.

## G-08 — Penetrator lifecycle and bonuses

Clearing exactly four lines in one lock awards one bonus, including a penetrator clear; saturate at three. Spend one bonus only when activating a running, regular active piece with a valid penetrator landing at or below it. Reject no-bonus, repeated, paused, game-over or no-landing activation without changing any state. Activation is one-way until lock or restart; it cannot be toggled off inside the stack. Preserve the current orientation, position, cadence and effective locking policies. Reevaluate support: retain a timer only if support remains, otherwise cancel it under G-07.

A penetrator may overlap occupied cells while descending and does not erase/change them. Its landing is the greatest origin y at or below the current origin for which all occupied cells are clear and in bounds, considering every candidate row rather than stopping at the first obstacle. Downward movement advances one row toward that target even through overlapping intermediate rows and stops there. A hard drop relocates directly there; ghost uses the identical target.

Lateral moves and ordered rotation/kick candidates must produce a clear in-board placement with a valid landing at or below that candidate; reject candidates that do not. Thus a temporarily overlapping piece cannot move sideways or rotate into another overlapping placement. Hold is disabled throughout activation. Gravity cannot advance below the selected lowest valid target. Revalidate before lock; never commit overlapping or out-of-board cells. A violated internal invariant must not corrupt the board: pause the session and show a recoverable restart message rather than silently selecting an unsafe placement.

Render all active penetrator cells white. Render all regular active/settled piece cells with nonwhite kind colors. Locked penetrator cells retain their white appearance; activation ends on lock and the next piece is regular. Display precisely one bonus symbol per available bonus, updating immediately after spend/award. Restart clears all bonuses/activation.

Acceptance fixture: an O piece at x=3, y=0 above blockers at `(3,10)` and `(4,10)` lands at y=8 in regular mode and y=18 in penetrator mode when rows 18/19 at columns 3/4 are empty. Soft traversal leaves the row-10 blockers untouched, and ghost/hard drop agree at y=18. Add a filled floor beneath a higher cavity to prove the algorithm selects the lowest valid placement even when the board bottom is unavailable. Verify invalid activation, Hold rejection, mid-traversal no-lock, unsafe transforms, three-bonus saturation and atomic spend/award.

## C-01 — Configuration behavior

Expose the six controls and source rules in the [configuration contract](spec/CONFIGURATION.md). Visibility and availability settings apply immediately; general/hard-drop locking changes apply on next spawn. Preserve Hold content and usage while disabled. Settings initialization occurs before the first active piece. No saved game is restored.

Acceptance: every legal value is selectable and reflected in selected state; effective-policy notices persist until next spawn. Changes during pause do not advance time. Each setting's restoration/change/reload behavior and invalid-source fallback are checked independently and in mixed-source combinations.

## Q-01 — Presentation, packaging and browser acceptance

Keep score, level, lines, game status, key help, next/Hold slots and bonus indicator readable beside the board. The board has a labelled, keyboard-focusable input surface. Start/New game returns focus to it; players can return from controls by keyboard navigation or clicking the board. Settings have programmatic labels, visible keyboard focus and textual values; status and persistence failures have textual DOM equivalents. Do not rely exclusively on white or color to identify the penetrator ability: include active-mode text. A complete nonvisual gameplay interface, mobile touch and audio are outside scope.

The production build consists of static assets with no backend/account requirement or third-party runtime requests. Provide reproducible dependency/build/test instructions and a version matching each phase's release tag and notes. Pin actual tooling/dependency versions in a lockfile when implemented, rather than claiming an untested setup here. Use isolated Chromium primary and Playwright-managed Firefox secondary under BROWSER_DEV_POLICY.md; headless execution is sufficient. Provisioning checks must cover repeated page/context creation, input, rendering and teardown before dependent application acceptance.

Release acceptance includes actual-app keyboard rounds, row clearing/scoring/game over/restart/pause, delivered feature boundaries, settings/reload interactions when included, and Canvas rendering evidence on both target browsers. Rule tests use deterministic time and supply. Browser-independent tests cannot substitute for these checks. Missing required browser execution blocks the affected phase exit; it does not authorize dropping a target. Reports distinguish planned, executed, failed and blocked checks.
