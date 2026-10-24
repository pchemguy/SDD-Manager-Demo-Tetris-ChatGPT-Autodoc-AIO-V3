# Browser Tetris

## Purpose and intended users

Build a single-player browser Tetris game for desktop keyboard players. Provide a responsive, understandable classic game, then useful bounded increments toward the complete gameplay and configuration scope below. The game runs entirely in the browser and needs no account or server-side game service.

## Intended outcome and scope

Players move and rotate falling tetrominoes, clear full lines, earn score, advance through increasing gravity speeds, and restart after game over. The complete game includes Hold, a ghost projection, 7-bag randomization, SRS wall kicks, hard drop, a next-piece preview, pause/resume, and visible controls and game status.

The default locking policy gives a grounded piece one full gravity interval before locking. A configurable alternative locks on a failed downward attempt. Hard drop follows the general policy unless its separate immediate-lock option is selected.

A penetrator bonus changes the current piece so it can descend through occupied cells without removing them. Its eventual lock placement must be inside the board and clear of settled cells. Hard drop and ghost projection use the same lowest valid penetrator landing. A four-line clear awards one bonus, capped at three; activation spends one. Render the active penetrator entirely white, use nonwhite regular-piece colors, and display one side-panel symbol per available bonus.

The side panel controls ghost visibility (hidden, dynamically hidden above the midline, or always shown), hard-drop availability, next preview, hard-drop locking, general locking, and Hold availability. Session configuration is a useful intermediate increment. The complete game persists each setting independently using explicit URL value, then cookie, then default precedence. Setting changes update both sources. Explicit valid URL values are saved even when equal to defaults; omitted parameters retain their cookies.

## Proposed gameplay decisions for confirmation

These recommendations resolve choices left open by the description. They are proposals until the project brief is accepted.

| Concern | Proposed behavior and reason |
| --- | --- |
| Ghost at the midline | Use the topmost occupied cell of the projected piece. Show in dynamic mode only when all projected cells are in the lower half; hide a straddling projection. On a 20-row visible board, rows 10–19 are the lower half using zero-based indexing. This gives one stable, conservative visibility rule. |
| Grounded timer | Start on first contact with support, using the gravity interval at that contact. Horizontal moves, rotations, repeated blocked inputs and delayed hard drops do not restart it while support remains. Leaving support cancels it; becoming grounded again starts a new interval. Pause freezes elapsed game time; resuming never causes catch-up locking. |
| Failed-down policy | A blocked automatic gravity step or soft-drop attempt locks a clear, supported piece. A hard drop that follows this policy relocates it; the next failed downward attempt locks it. Immediate hard-drop locking overrides the delay. |
| Penetrator activation and Hold | Activation is one-way until lock and requires a bonus, an active nonpenetrator piece, and a valid landing at or below it. Reject ineligible activation without spending. Disable Hold while penetrator mode is active, so its state cannot be stored or transferred. Otherwise allow Hold once per spawned piece. |
| Penetrator motion and lock safety | Compute the lowest clear, in-board placement at or below the piece, ignoring intervening blockers. Gravity may cross overlapping rows and stops at that target; hard drop goes directly there. Never merge a transient overlapping piece into the board. Lateral moves and rotations must produce a clear, in-board placement with a reachable valid landing; reject unsafe changes. Activation cannot be toggled off inside the stack. |
| Bonus accounting | Spend only on successful activation; award after a successful four-line clear, including one made by a penetrator, with saturation at three. A new game resets bonuses. |
| Live setting changes | Ghost, next preview, hard-drop availability and Hold availability update immediately. Locking-policy changes take effect on the next spawned piece, keeping the current timer predictable; explain that timing in the controls. Disabling Hold preserves the stored piece for later re-enabling. |
| Invalid configuration | Validate each source independently. An invalid URL value falls back to a valid cookie, then default, without poisoning another setting. Use the first occurrence of a duplicated parameter deterministically. Invalid values are not saved as cookies. Preserve unrelated URL parameters and the fragment. Storage or URL-update failure leaves the current game usable. |
| Defaults and pause | Always show ghost; enable hard drop, next preview and Hold; use full-interval locking and hard drop following it. Provide manual pause and pause on lost page focus, requiring explicit resume. Ignore gameplay hotkeys while a settings control has focus. |

Exact key bindings, scoring values, speed progression, cookie names and test vectors belong in the behavioral specification. They may be selected during design provided they preserve these accepted gameplay decisions; newly discovered material conflicts must be surfaced before implementation.

## Delivery and technical direction

Propose TypeScript, a Canvas board and ordinary HTML side-panel controls, with static production assets and no application framework. This keeps game rendering small while retaining labelled, keyboard-operable settings. Compared with a board built from DOM cells, Canvas centralizes drawing; a framework would add tooling without a current component-complexity need. Keep gameplay independently testable from rendering, time and persistence.

Start with the smallest sensible playable classic baseline. Add the complete scope through bounded capability increments; do not require every enhancement before the first playable release. Use semantic versioning, beginning with planned baseline version **0.1.0**, and advance versions for delivered increments toward **1.0.0** when the complete accepted scope is verified. Publish a GitHub release, matching tag and release notes after each implemented phase is verified and integrated. Documentation preparation alone produces no product release.

Chromium is the primary automated browser target and Playwright-managed Firefox the secondary target, using dedicated installations and isolated profiles under the repository browser policy. Headless interaction and rendering are sufficient. Verify provisioning and representative execution before browser-dependent implementation; a download or launch alone does not establish application acceptance. Respect the execution host's shell policy.

## Proposed boundaries and quality goals

Keyboard desktop play, clear rules and repeatable automated checks take priority. Use labelled settings, visible focus and readable text for score, level, bonuses and status. Canvas accessibility is limited; a complete nonvisual gameplay interface is outside the proposed scope.

Multiplayer, backend leaderboards, accounts, audio, mobile touch controls, additional game variants and deployment to a particular hosting provider are proposed non-goals. Persistence stores configuration only, not an in-progress game. An installed static build should make no third-party runtime requests. No commercial branding or official affiliation is implied.

There is no game implementation yet. Success means the classic baseline is playable independently, each increment preserves it, and the complete result meets the agreed gameplay and persistence behavior in both declared browsers.
