# Delivery plan

## Strategy and contract coverage

Deliver the [specified game](SPEC.md) through five independently verifiable capability increments. The architecture remains a browser-only domain/controller/presentation application. The first phase is a playable classic round, not a framework skeleton or the complete enhanced game. Later phases preserve the preceding usable game and add a coherent feature area.

| Phase | Useful delivered outcome | Version | Included contracts | Explicit later scope |
| --- | --- | --- | --- | --- |
| 1 — Playable classic | Play, score, advance levels, pause, lose and restart a classic round. | 0.1.0 | G-01/G-02/G-04; G-03 basic motion/spawn/no-kick rotation; G-07 default interval locking; applicable Q-01. | 7-bag, Hold/preview, ghost, kicks, hard drop, penetrator, settings and persistence. |
| 2 — Modern play | Manage supply/Hold and use consistent ghost, SRS kicks and hard drop. | 0.2.0 | Complete G-03/G-05; G-06 default always-show and following-policy hard drop; G-07 hard-drop interaction; Q-01 regressions. | Penetrator; alternative/configurable policies and ghost modes; persistence. |
| 3 — Penetrator play | Earn/spend bonuses and descend through the stack with safe landing, preview and locking. | 0.3.0 | G-08; penetrator interactions with G-05/G-06/G-07 and rendering. | Configurable settings and persistence. |
| 4 — Session configuration | Use all six controls, dynamic/hide ghost modes and both alternative locking policies in one session. | 0.4.0 | C-01 session scope; complete configurable G-05/G-06/G-07; configuration schema and live application. | URL/cookie restoration and writes. |
| 5 — Persistent configuration | Open, share and reload configured games with independent URL/cookie precedence and resilient writes. | 1.0.0 | Complete C-01/configuration child and Q-01; whole accepted gameplay regression. | None within accepted project scope. |

The classic increment uses independent uniform random pieces, no next/Hold slots or bonus UI, and no settings controls. It still implements the accepted default full-gravity-interval lock delay. A later feature's absence is an honest phase scope limit; it is not a failed earlier-phase exit. Current documents describe the complete intended game.

## Phase 1 — Playable classic

Outcome: a complete classic game with fixed defaults, keyboard play and meaningful score/level/game-over feedback. This is the smallest useful product: special supply, prediction, alternate locks and persistence are independent enhancements.

| Milestone | Capability and dependencies | Demonstration and exit evidence |
| --- | --- | --- |
| 1.1 — Falling piece loop | Pin/build the TypeScript app and check isolated browser capability, implement board/piece geometry and regular falling/movement/rotation, connect Canvas and input. Starts from accepted preparation. | Both browsers show controllable falling pieces on the real app path; deterministic collision/gravity tests pass. Browser preflight is complete before browser-dependent work. The demo exposes movement/focus usability for a human continue/amend/simplify/stop decision. |
| 1.2 — Complete classic rounds | After 1.1, add interval locking, clear/spawn/game-over, score/level, pause/restart and usable HUD/help. | A scripted round clears/scores/levels, ends and restarts; pause/blur and lock-boundary tests pass; static build, controls guide and version are ready. Preserve 1.1 interactions. |
| 1.3 — Phase review | Dedicated final review after both delivery milestones complete/close. | Cross-milestone code review, classic acceptance/regression and build evidence, blocker repairs, phase report/HANDOFF and release-message readiness. |

Full-interval timing belongs here because it is the accepted default feel of the baseline; no alternative policy controls are required. The two delivery milestones distinguish a controllable loop from complete round lifecycle without delaying initial browser integration. They do not justify adding independent enhanced features.

## Phase 2 — Modern play

Outcome: the classic game gains supply management and placement aids. These features share active-piece/queue/projection contracts but remain split into two integrated milestone outcomes.

| Milestone | Capability and dependencies | Demonstration and exit evidence |
| --- | --- | --- |
| 2.1 — Supply and Hold | After Phase 1 integration/release, add 7-bag, one-piece next preview, Hold and their UI. | Bag/queue and empty/occupied/blocked/repeated Hold cases pass; a player can plan and exchange pieces in both browsers. Review feedback can amend/simplify the control/display before placement aids grow. |
| 2.2 — Placement assists | After 2.1, add canonical regular landing and always-visible ghost, full SRS tables, hard drop following interval lock. | Ghost/hard-drop equality, wall/floor/top kicks, blocked rotations, zero-distance drops and no deadline refresh pass; entire modern round runs on both browsers. Update help/version/static package. |
| 2.3 — Phase review | Dedicated final review after 2.1/2.2 complete/close. | Verify modern interactions and classic regression, inspect code separately from test execution, repair blockers and retain report/HANDOFF/release-message readiness. |

One milestone combines each tightly related user outcome; additional milestone fragmentation would create handoffs between features whose useful validation depends on integration. Configurable variants remain outside this increment.

## Phase 3 — Penetrator play

Outcome: a bounded earned ability with one coherent lifecycle across collision, bonus accounting and preview/drop.

| Milestone | Capability and dependencies | Demonstration and exit evidence |
| --- | --- | --- |
| 3.1 — Earned penetrator ability | After Phase 2 integration/release, implement bonus earn/spend/activation, lowest-valid traversal and safe locks, shared ghost/hard-drop behavior, Hold exclusion and white/symbol presentation. | The blocking-shelf/lower-cavity fixture passes for gravity, ghost and drop; transient overlap cannot lock; invalid activation spends nothing; cap/Hold/mode-reset/white rendering pass. Both browsers demonstrate earning/spending and readable active mode. Usability evidence informs continue/amend/simplify/stop. Update guide/version/static package. |
| 3.2 — Phase review | Dedicated final review after 3.1 completes/closes. | Review activation-to-lock atomicity, shape/cavity edge cases and prior modern regression; repair blockers and retain report/HANDOFF/release-message readiness. |

A single delivery milestone is justified because bonuses, traversal and presentation must meet together for the earned ability to be usable and safe. It is divided into bounded implementation tasks; splitting separate lifecycle fragments into multiple milestones would not produce independently useful pen gameplay.

## Phase 4 — Session configuration

Outcome: all six controls work live, including selected versus effective policy notices, without persistence.

| Milestone | Capability and dependencies | Demonstration and exit evidence |
| --- | --- | --- |
| 4.1 — Six session settings | After Phase 3 integration/release, establish typed schema/defaults, alternative lock semantics, immediate/next-spawn application and labelled settings UI. | Each legal value, midline-straddling ghost, disabled hard drop/Hold, retained Hold slot, policy changes during pause/grounding, next-spawn snapshots and input-focus exclusions pass. Both browsers demonstrate settings changing without timer resets. Update guide/version/static package. |
| 4.2 — Phase review | Dedicated final review after 4.1 completes/closes. | Cross-setting and penetrator/classic regression, code review, blocker repairs and report/HANDOFF/release-message readiness. |

A single milestone retains the one configuration-panel outcome; separate milestones for individual switches would fragment schema, current/effective settings and combined acceptance. Cookies/URL writes remain independent of session controls and belong in Phase 5.

## Phase 5 — Persistent configuration

Outcome: restoration, sharing and reload work while persistence failures leave the game playable. Depends on the complete session settings schema/application.

| Milestone | Capability and dependencies | Demonstration and exit evidence |
| --- | --- | --- |
| 5.1 — Restore independent settings | After Phase 4 integration/release, add URL/cookie read adapters, per-setting resolver and startup writes for valid explicit URL values. | All six precedence routes, mixed sources, explicit defaults, omitted cookies, invalid/duplicate values and denied reads pass in deterministic checks and real served-origin reload tests. Demonstrate saved/default/URL combinations so the human can amend confusing behavior. |
| 5.2 — Persist edits and finish distribution | After 5.1, write each user change independently to cookie and replacement URL, preserve unrelated parameters/fragment, handle independent failures and complete distribution/docs. | Round trips cover every setting; one failed write does not prevent the other or in-memory play. Both browsers pass all delivered gameplay/settings/reload acceptance; version 1.0.0, static build and complete user/developer guide are ready. |
| 5.3 — Phase review | Dedicated final review after 5.1/5.2 complete/close. | Review all accepted contracts and regressions; aggregate milestone/phase findings and eligible deferred TODOs into the final implementation report; verify build, report/HANDOFF and final release-message readiness. |

Two milestones separate source resolution from edit propagation and external failure handling; each has concrete browser evidence. The final milestone is not a container for unrelated product capabilities: all gameplay and controls are already delivered.

## Common milestone, phase and release gates

Each delivery milestone requires whole-capability code review, focused tests and relevant prior regression, blocker repair, a committed milestone report and refreshed HANDOFF. TASKS assigns these obligations to the final implementation task unless both lifecycle thresholds require a separate milestone-review task. The final task depends on the milestone's other work. The dedicated single-task phase review milestone is always retained and excluded from delivery counts.

A phase review starts only after delivery milestone completion and verified closure. Fix bugs and every SPEC/PLAN violation before the boundary closes; only noncritical code issues consistent with all exits may be retained as explicitly justified TODOs. Reports distinguish code review from testing, retain exact checks/environment/limits and include a TODO section even when empty. The last phase review also produces the final implementation/TODO aggregation report.

After a complete verified phase, explicitly integrate into the actual default branch, verify the merged result, push/read back and publish its requested versioned GitHub release. Prepare full release notes at root RELEASE-NOTES.md, use the release workflow's exact default-branch release commit/tag boundary, and verify tag/source/version/body and provider publication. These post-phase operations do not belong to an earlier delivery task and cannot be claimed from local phase review alone. Publish the phase release before starting its authorized successor. Do not create future-phase hosted objects early.

Before implementation, accepted preparation still needs whole-package QC and verified published integration. Implementation is selected separately. Within authorized work, each task's result/evidence/initial checkbox shares its owning commit; every commit is pushed/read back before progression. Project tracking uses native phase milestones and task issues with verified associations/closures.

## Risks and verification strategy

The earliest enabling work pins Node/TypeScript/Vite, unit-test and Playwright dependencies with a lockfile and establishes bounded commands. Use deterministic injected time/supply for rules and adapter-failure tests for configuration. Do not install dependencies or browsers during documentation preparation. Browser provisioning and repeated page/input/render/teardown diagnostics follow BROWSER_DEV_POLICY.md; a required-browser failure blocks dependent browser tasks/phase exits, while truly independent work may proceed only within authorized dependencies.

At every phase exit, test the real built/served application in isolated Chromium and managed Firefox, plus relevant type/unit/build checks. Keep owned caches, binaries, reports and temporary browser state outside production/tracked source. Preserve Windows CMD compatibility in developer scripts; Linux execution does not establish tested Windows behavior. Capture both achieved and missing environment evidence.

The main correctness risks are divergent landing algorithms, timer resets through input/configuration, overlapping penetrator locks and precedence/write failures that affect unrelated settings. Their domain/adapter boundaries and phase-specific acceptance above give them early tests and integrated rechecks. No unresolved design decision is required to derive TASKS. Physical source/test ownership belongs in layout.
