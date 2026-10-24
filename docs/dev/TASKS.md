# Implementation tasks

The [PLAN](PLAN.md) owns phase/milestone outcomes; [SPEC](SPEC.md), its [geometry](spec/GEOMETRY.md) and [configuration](spec/CONFIGURATION.md) children own acceptance; [layout](layout.md) owns paths. All implementation work below is planned and unchecked. Preparation tasks are separate in DOCS_TASKS.md.

## Shared execution and boundary obligations

Each delivery task includes meaningful tests of its own behavior, applicable regression, documentation and required blocker repairs. For behavior changes, establish the intended failing test before implementation, then verify the result. Expected paths are scoped ownership guidance, not a requirement to create empty files. Execution requires the accepted package/integration, eligible phase tracking, environment and an authorized range.

Each milestone boundary identified below folds whole-capability code review, focused tests/regressions, blocker repair, committed report and HANDOFF into its final implementation task. That task depends on all earlier tasks in its milestone and cannot complete without the folded evidence. A phase review is separate and always executes after delivery milestone completion/verified closure. Every report includes Findings/Blockers and TODO (None when empty); only eligible noncritical code issues may be deferred with impact, options, rationale and owner.

After a complete phase review, the coordinator verifies/publishes explicit default-branch integration and the requested matching version/tag/release before an authorized successor starts. The review task prepares release notes but cannot claim later publication. Whole-package preparation QC and implementation authorization are separate prerequisites; no implementation objects are activated by this document.

## Phase 1 — Playable classic

- [ ] Phase 1 — Playable classic
    - [ ] Milestone 1.1 — Falling piece loop
        - [ ] T-001 — Establish the pinned toolchain and isolated browser preflight
            Depends on: None. Contracts: Q-01; PLAN Phase 1 enabling gate.
            Scope: Root package/lock/tool configs, test runner configuration and docs/DEVELOPMENT.md. Establish typecheck/unit/build/e2e commands and owned ignored browser/cache/report paths.
            Evidence: Run a minimal real served page through pinned Playwright Chromium and managed Firefox, with repeated context/page/input/Canvas/teardown cycles and whole-process deadlines. Record versions, paths, successful checks or exact blockers; do not complete on download/launch alone.
        - [ ] T-002 — Implement regular geometry and falling transitions
            Depends on: T-001. Contracts: G-01 initial state; G-03 basic motion; G-04 gravity cadence; geometry matrices.
            Scope: src/domain/types.ts, pieces.ts, geometry.ts, supply.ts and initial game/timing behavior; focused domain tests. Use classic independent uniform supply and no-kick rotations.
            Evidence: Deterministic spawn/motion/collision/orientation and gravity-step fixtures pass; rejected commands preserve state. Keep locking/clear/progression deferred to milestone 1.2 without inventing enabled features.
        - [ ] T-003 — Connect the controllable falling loop to the browser
            Depends on: T-001, T-002. Contracts: G-02 input/focus; G-03 basic motion; Q-01 initial presentation.
            Scope: src/main.ts, src/session/controller.ts, view-model.ts, src/browser/input.ts, clock.ts and src/ui board/panel/styles; keyboard/Canvas integration and brief usage help.
            Evidence: Both target browsers show and control falling pieces using the real app path; focus return, repeat suppression, bounds and resource disposal pass. Demonstrate movement responsiveness for human steering.
            Milestone exit: perform whole-capability code review separately from test execution, run applicable regressions, repair blockers, and include `docs/dev/reports/phases/1/1.1.md` plus refreshed HANDOFF with this task result and initial checkbox in its completion commit. Report the milestone demonstration/feedback and any human steering; do not invent a usability trial or waive acceptance.
    - [ ] Milestone 1.2 — Complete classic rounds
        - [ ] T-004 — Implement safe interval locking and complete round lifecycle
            Depends on: T-003. Contracts: G-01; G-07 interval default.
            Scope: src/domain/game.ts and timing.ts; domain fixtures for supported contact, atomic merge/clear/spawn, blocked spawn and restart.
            Evidence: Observe intended failing tests before rule changes; verify contact/deadline/off-support/exact-time behavior, simultaneous one-to-four-line clears and no partial spawn/lock corruption.
        - [ ] T-005 — Integrate score, level and gravity progression
            Depends on: T-004. Contracts: G-04; G-01 counter effects.
            Scope: src/domain/progression.ts and its game/view consumers; progression and multi-lock integration tests.
            Evidence: Clear scoring uses pre-clear level; 9-to-10-lines boundary, zero-line scoring, gravity floor and new-piece cadence pass without timer/input regressions.
        - [ ] T-006 — Complete pause, status and classic distribution
            Depends on: T-004, T-005. Contracts: G-02 lifecycle; G-01; applicable Q-01.
            Scope: Session/input/UI pause/resume/blur/restart and full classic HUD/help; classic e2e, docs/USER-GUIDE.md, developer instructions and package version 0.1.0.
            Evidence: Both browsers complete scored/levelled/ended/restarted rounds and pause/focus scenarios. Type/unit/build checks pass; static assets contain no runtime service dependency. Demonstrate the complete baseline and prepare its distribution evidence.
            Milestone exit: perform whole-capability code review separately from test execution, run applicable regressions, repair blockers, and include `docs/dev/reports/phases/1/1.2.md` plus refreshed HANDOFF with this task result and initial checkbox in its completion commit. Report the milestone demonstration/feedback and any human steering; do not invent a usability trial or waive acceptance.
    - [ ] Milestone 1.3 — Phase review
        - [ ] T-007 — Review, test and report Phase 1
            Depends on: T-003, T-006 and every delivery milestone in Phase 1 completed/closed with verified readback. The special review milestone does not depend on its own closure.
            Scope: cross-milestone code review, relevant rule/controller/browser regressions, all Phase 1 exits in PLAN, build/version/distribution checks, blocker repairs and complete release-message preparation at root RELEASE-NOTES.md.
            Evidence: retain exact reviewed sources, environments/commands/outcomes and limits in `docs/dev/reports/phases/1/PHASE-REPORT.md`; carry milestone findings and eligible TODOs forward. Include HANDOFF and this task result/initial checkbox together. Close/read back the review issue/milestone only after verified publication; subsequent integration/release effects remain pending until observed.

## Phase 2 — Modern play

- [ ] Phase 2 — Modern play
    - [ ] Milestone 2.1 — Supply and Hold
        - [ ] T-008 — Implement 7-bag supply and stable next preview data
            Depends on: T-007. Contracts: G-03 complete supply; G-05 preview.
            Scope: src/domain/supply.ts and queue/view consumers; seeded/scripted supply tests.
            Evidence: Every aligned bag is a permutation; refill, bag boundaries, peek and consumption preserve order. Existing classic lifecycle remains green.
        - [ ] T-009 — Implement one-use Hold exchanges and spawn behavior
            Depends on: T-008. Contracts: G-05; G-01 blocked entering spawn.
            Scope: src/domain/game.ts Hold state/transitions and domain Hold tests.
            Evidence: Empty/occupied exchanges, no double use, reset after lock, canonical spawn, policy/cadence reset, queue counts and blocked entering spawn pass.
        - [ ] T-010 — Integrate Hold and next preview controls and panels
            Depends on: T-008, T-009. Contracts: G-02 Hold keys; G-05; Q-01.
            Scope: Session/input/view model and UI Hold/next slots; modern e2e and usage guidance.
            Evidence: Both target browsers demonstrate queue/Hold planning and correct keyboard behavior; rendering does not consume supply. Recheck classic play and disposal.
            Milestone exit: perform whole-capability code review separately from test execution, run applicable regressions, repair blockers, and include `docs/dev/reports/phases/2/2.1.md` plus refreshed HANDOFF with this task result and initial checkbox in its completion commit. Report the milestone demonstration/feedback and any human steering; do not invent a usability trial or waive acceptance.
    - [ ] Milestone 2.2 — Placement assists
        - [ ] T-011 — Implement canonical regular landing and ghost rendering
            Depends on: T-010. Contracts: G-06 default always-show; geometry landing.
            Scope: src/domain/landing.ts, view-model projection and src/ui/board.ts; landing/ghost fixtures and browser rendering checks.
            Evidence: Projected placement is the final reachable clear row on empty/stacked boards, respects occupied-cell geometry and remains legible when coincident. Rendering consumes the domain result.
        - [ ] T-012 — Implement complete ordered SRS rotations
            Depends on: T-011. Contracts: G-03 rotations; spec/GEOMETRY.md.
            Scope: src/domain/rotation.ts and game transformation acceptance; full table-driven orientation/kick tests.
            Evidence: All eight orientation transitions for each kick family, first-valid ordering, I-specific wall/floor behavior, O stability, ceiling rejection and completely blocked rotations pass. Grounded support/timer handling remains correct.
        - [ ] T-013 — Integrate delayed hard drop and modern acceptance
            Depends on: T-011, T-012. Contracts: G-06; G-07 default hard-drop following policy.
            Scope: Domain/controller/input hard drop and modern browser tests; guide/help, package version 0.2.0 and static build.
            Evidence: Hard drop equals ghost landing, reaches contact without premature locking, preserves cadence/deadline on zero-distance/repeated drops and preserves Hold/supply rules. Both browsers pass the complete modern round and classic regression.
            Milestone exit: perform whole-capability code review separately from test execution, run applicable regressions, repair blockers, and include `docs/dev/reports/phases/2/2.2.md` plus refreshed HANDOFF with this task result and initial checkbox in its completion commit. Report the milestone demonstration/feedback and any human steering; do not invent a usability trial or waive acceptance.
    - [ ] Milestone 2.3 — Phase review
        - [ ] T-014 — Review, test and report Phase 2
            Depends on: T-010, T-013 and every delivery milestone in Phase 2 completed/closed with verified readback. The special review milestone does not depend on its own closure.
            Scope: cross-milestone code review, relevant rule/controller/browser regressions, all Phase 2 exits in PLAN, build/version/distribution checks, blocker repairs and complete release-message preparation at root RELEASE-NOTES.md.
            Evidence: retain exact reviewed sources, environments/commands/outcomes and limits in `docs/dev/reports/phases/2/PHASE-REPORT.md`; carry milestone findings and eligible TODOs forward. Include HANDOFF and this task result/initial checkbox together. Close/read back the review issue/milestone only after verified publication; subsequent integration/release effects remain pending until observed.

## Phase 3 — Penetrator play

- [ ] Phase 3 — Penetrator play
    - [ ] Milestone 3.1 — Earned penetrator ability
        - [ ] T-015 — Implement capped bonuses and validated activation
            Depends on: T-014. Contracts: G-08 bonus/activation lifecycle; G-05 Hold exclusion.
            Scope: Domain bonus accounting and active-mode state; activation/clear/Hold tests.
            Evidence: Only four-line locks award, count saturates at three, successful activation spends exactly one, failures spend nothing, Hold is rejected while active and restart resets mode/bonuses.
        - [ ] T-016 — Implement penetrator traversal and safe grounded locking
            Depends on: T-015. Contracts: G-08 traversal/transforms; G-07 support; geometry landing.
            Scope: src/domain/landing.ts, geometry/rotation acceptance and game/timing transitions; cavity/traversal fixtures.
            Evidence: Scan every lower origin, cross occupied rows without deletion, stop at the lowest clear placement, reject unsafe lateral/rotation candidates and never merge overlap. Activation cancels contact timing only if support is lost; no-landing rejection/invariant fallback is safe.
        - [ ] T-017 — Connect penetrator projection and hard-drop behavior
            Depends on: T-016. Contracts: G-06/G-08 shared projection/drop.
            Scope: Canonical landing consumers in game/view model; integrated ghost/drop/lock tests and focused browser fixture coverage.
            Evidence: The O/shelf fixture yields regular y=8 and penetrator y=18; higher cavities above an unavailable bottom also agree across gravity/ghost/drop. Preview visibility never changes the chosen target or settled cells.
        - [ ] T-018 — Complete penetrator presentation and usable ability integration
            Depends on: T-015, T-016, T-017. Contracts: G-08 rendering/indicators; G-02 activation key; Q-01.
            Scope: UI white active/settled penetrator cells, nonwhite regular palette, one-symbol-per-bonus indicator, active-mode text, B hotkey; browser acceptance, guide and version 0.3.0.
            Evidence: Both browsers demonstrate bonus earning/spending, immediate indicator updates, safe lock/mode reset and Hold rejection. Review ability readability, all shapes and prior modern gameplay; build the static distribution.
            Milestone exit: perform whole-capability code review separately from test execution, run applicable regressions, repair blockers, and include `docs/dev/reports/phases/3/3.1.md` plus refreshed HANDOFF with this task result and initial checkbox in its completion commit. Report the milestone demonstration/feedback and any human steering; do not invent a usability trial or waive acceptance.
    - [ ] Milestone 3.2 — Phase review
        - [ ] T-019 — Review, test and report Phase 3
            Depends on: T-018 and every delivery milestone in Phase 3 completed/closed with verified readback. The special review milestone does not depend on its own closure.
            Scope: cross-milestone code review, relevant rule/controller/browser regressions, all Phase 3 exits in PLAN, build/version/distribution checks, blocker repairs and complete release-message preparation at root RELEASE-NOTES.md.
            Evidence: retain exact reviewed sources, environments/commands/outcomes and limits in `docs/dev/reports/phases/3/PHASE-REPORT.md`; carry milestone findings and eligible TODOs forward. Include HANDOFF and this task result/initial checkbox together. Close/read back the review issue/milestone only after verified publication; subsequent integration/release effects remain pending until observed.

## Phase 4 — Session configuration

- [ ] Phase 4 — Session configuration
    - [ ] Milestone 4.1 — Six session settings
        - [ ] T-020 — Define typed session settings and selected-state ownership
            Depends on: T-019. Contracts: C-01 session scope; configuration schema.
            Scope: src/config/schema.ts, service.ts and typed controller integration; schema/default/invalid-update unit tests. No browser persistence yet.
            Evidence: All six legal value sets/defaults are represented once; selected settings survive restart and invalid programmatic updates are no-ops. Current visibility/availability and future-piece policy ownership remain distinct.
        - [ ] T-021 — Implement alternative locking and next-spawn policy snapshots
            Depends on: T-020. Contracts: G-07 all policies; C-01 application timing.
            Scope: Domain game/timing and controller selected/effective policy application; lock/pause/Hold/config interaction tests.
            Evidence: Failed automatic/soft-down locks, immediate hard-drop override, following-policy behavior, mid-piece setting changes, paused changes and Hold-entering spawns pass. Settings cannot refresh a grounded deadline.
        - [ ] T-022 — Integrate all six live controls and ghost modes
            Depends on: T-020, T-021. Contracts: C-01 session controls; G-05/G-06 variants; Q-01.
            Scope: UI settings/policy notice, view model and availability guards; settings e2e, guide and package version 0.4.0.
            Evidence: Both browsers cover each legal control value, topmost-row 9/10/straddle visibility, hard-drop no-op, Hold disable/re-enable with retained slot/use, next hiding, policy notices and keyboard focus. No cookie/URL effects are claimed.
            Milestone exit: perform whole-capability code review separately from test execution, run applicable regressions, repair blockers, and include `docs/dev/reports/phases/4/4.1.md` plus refreshed HANDOFF with this task result and initial checkbox in its completion commit. Report the milestone demonstration/feedback and any human steering; do not invent a usability trial or waive acceptance.
    - [ ] Milestone 4.2 — Phase review
        - [ ] T-023 — Review, test and report Phase 4
            Depends on: T-022 and every delivery milestone in Phase 4 completed/closed with verified readback. The special review milestone does not depend on its own closure.
            Scope: cross-milestone code review, relevant rule/controller/browser regressions, all Phase 4 exits in PLAN, build/version/distribution checks, blocker repairs and complete release-message preparation at root RELEASE-NOTES.md.
            Evidence: retain exact reviewed sources, environments/commands/outcomes and limits in `docs/dev/reports/phases/4/PHASE-REPORT.md`; carry milestone findings and eligible TODOs forward. Include HANDOFF and this task result/initial checkbox together. Close/read back the review issue/milestone only after verified publication; subsequent integration/release effects remain pending until observed.

## Phase 5 — Persistent configuration

- [ ] Phase 5 — Persistent configuration
    - [ ] Milestone 5.1 — Restore independent settings
        - [ ] T-024 — Implement raw source readers and independent resolution
            Depends on: T-023. Contracts: C-01; configuration startup resolution.
            Scope: src/browser/cookies.ts, url.ts and src/config/resolve.ts; pure source matrices and read-adapter tests.
            Evidence: Resolve all six settings per URL/cookie/default precedence; exact case/value parsing, invalid/empty/duplicate sources, unavailable reads and mixed-source fixtures pass. Raw adapters contain no duplicate precedence policy.
        - [ ] T-025 — Apply startup settings and persist explicit URL selections
            Depends on: T-024. Contracts: Configuration explicit-default/omitted-cookie guarantees.
            Scope: src/config/service.ts startup effects, cookie writer and controller bootstrap; memory/failing-port tests.
            Evidence: Resolve before first spawn, persist valid explicit URL values including defaults, retain cookies for omitted keys, never save invalid URL values and preserve in-memory play when cookie writes fail. Do not normalize/add query values on startup.
        - [ ] T-026 — Integrate real-origin restoration and reload acceptance
            Depends on: T-024, T-025. Contracts: Configuration acceptance matrix; C-01 startup.
            Scope: Browser bootstrap and persistence e2e on served origins; developer/user source-precedence guidance.
            Evidence: Both browsers reload each setting from valid URL and cookie-only sources, exercise mixed/invalid/duplicate cases and explicit-default overwrite/omission retention. No later edit-write behavior is claimed complete.
            Milestone exit: perform whole-capability code review separately from test execution, run applicable regressions, repair blockers, and include `docs/dev/reports/phases/5/5.1.md` plus refreshed HANDOFF with this task result and initial checkbox in its completion commit. Report the milestone demonstration/feedback and any human steering; do not invent a usability trial or waive acceptance.
    - [ ] Milestone 5.2 — Persist edits and finish distribution
        - [ ] T-027 — Persist valid changes to independent cookie and URL sinks
            Depends on: T-026. Contracts: Configuration user-change/write contract.
            Scope: src/config/service.ts, cookies/url adapters and control integration; deterministic write-order and real-browser round-trip checks.
            Evidence: Every valid selection, including reselecting a default, updates memory and attempts both sinks. Cookie attributes, replacement history, one changed-key occurrence and unrelated decoded parameters/fragment preservation pass without navigation.
        - [ ] T-028 — Implement resilient source and write failure feedback
            Depends on: T-027. Contracts: Configuration unavailable reads/writes and recovery; Q-01 status.
            Scope: Persistence adapters/service status and UI nonblocking feedback; denied-read/write and independent-sink failure tests.
            Evidence: One sink failure cannot suppress the other attempt or undo selection; failed reads fall back per setting; detectable denied writes report status. A later valid selection retries without automatic background services or hidden state corruption.
        - [ ] T-029 — Complete persistent-game distribution and full acceptance
            Depends on: T-027, T-028. Contracts: Complete C-01/Q-01 and preserved G-01–G-08.
            Scope: Full persistence/settings/gameplay e2e, production/static packaging, final user/developer guidance and package version 1.0.0.
            Evidence: All six settings complete change/reload/share round trips in both browsers; gameplay, focus, pause, penetrator/Hold/ghost/drop/lock regressions and type/unit/build checks pass. Distribution has no credentials, caches, test-only backdoors or third-party runtime dependency.
            Milestone exit: perform whole-capability code review separately from test execution, run applicable regressions, repair blockers, and include `docs/dev/reports/phases/5/5.2.md` plus refreshed HANDOFF with this task result and initial checkbox in its completion commit. Report the milestone demonstration/feedback and any human steering; do not invent a usability trial or waive acceptance.
    - [ ] Milestone 5.3 — Phase review
        - [ ] T-030 — Review, test and report Phase 5
            Depends on: T-026, T-029 and every delivery milestone in Phase 5 completed/closed with verified readback. The special review milestone does not depend on its own closure.
            Scope: cross-milestone code review, relevant rule/controller/browser regressions, all Phase 5 exits in PLAN, build/version/distribution checks, blocker repairs and complete release-message preparation at root RELEASE-NOTES.md.
            Evidence: retain exact reviewed sources, environments/commands/outcomes and limits in `docs/dev/reports/phases/5/PHASE-REPORT.md`; carry milestone findings and eligible TODOs forward. Include HANDOFF and this task result/initial checkbox together. Close/read back the review issue/milestone only after verified publication; subsequent integration/release effects remain pending until observed.
            Final outcome: also write `docs/dev/reports/IMPLEMENTATION-REPORT.md`, aggregating unresolved/deferred findings from every milestone/phase with provenance, options and owners; assess the complete accepted scope without losing prior resolution evidence.

