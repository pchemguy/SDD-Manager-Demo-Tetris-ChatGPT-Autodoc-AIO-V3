# Repository layout

## Status and ownership

This is the intended physical allocation of the logical components in [DECOMPOSITION](DECOMPOSITION.md) and delivery boundaries in [PLAN](PLAN.md). Development documents, repository policies and the bundled plugin exist; application, test, dependency and build paths below are planned until their implementation tasks create them. A listed path is not a completion claim.

| Logical owner | Intended source | Intended checks / fixtures | Placement rule |
| --- | --- | --- | --- |
| Browser composition | `src/main.ts`, root `index.html` | `tests/integration/startup.test.ts`, real-app browser smoke | Assemble adapters/controller/views here; no gameplay rule or storage precedence in the entry. |
| D1 geometry/pieces | `src/domain/pieces.ts`, `geometry.ts`, `rotation.ts`, `landing.ts` | `tests/domain/geometry.test.ts`, `rotation.test.ts`, `landing.test.ts`; `tests/fixtures/boards.ts` | Domain-only imports. Landing is shared by active gravity/drop and view projection. |
| D2 supply | `src/domain/supply.ts` | `tests/domain/supply.test.ts`; deterministic random fixtures | Own bag/queue behavior; injected samples, no browser/global random reads. |
| D3 transition/state/time | `src/domain/types.ts`, `game.ts`, `timing.ts` | `tests/domain/game.test.ts`, `timing.test.ts`, `hold.test.ts`, `penetrator.test.ts` | One authoritative state; timing is factored only where cohesive. Board mutations remain in validated transitions. |
| D4 progression | `src/domain/progression.ts` | `tests/domain/progression.test.ts` | Pure scoring/level/gravity calculation, not a second score store. |
| C1 schema/resolver | `src/config/schema.ts`, `resolve.ts` | `tests/config/schema.test.ts`, `resolve.test.ts` | Schema owns legal values/defaults; resolve owns precedence. Reuse the same types in controls/adapters. |
| C2 settings coordinator | `src/config/service.ts` | `tests/config/service.test.ts`; in-memory/failing ports | Own selected values and persistence effects; no board knowledge. |
| S1 session | `src/session/controller.ts`, `view-model.ts` | `tests/session/controller.test.ts`, `view-model.test.ts` | Compose ordered time/actions/settings and read-only view data; do not repeat D1 rules. |
| V1/V2 presentation | `src/ui/board.ts`, `panel.ts`, `styles.css` | `tests/ui/panel.test.ts`; browser Canvas/focus/status checks | Canvas and DOM read state and call controller actions only. |
| A1 input/time | `src/browser/input.ts`, `clock.ts` | `tests/browser/input.test.ts`, session fake-clock checks | Own listeners/repeat observations/disposal, not lock deadlines. |
| A2 persistence | `src/browser/cookies.ts`, `url.ts` | `tests/browser/persistence.test.ts`; real-origin browser reload checks | Narrow raw browser access and serialization; no copied setting-resolution rules. |
| Integrated browser acceptance | `playwright.config.ts`, `tests/e2e/` | `classic.spec.ts`, `modern.spec.ts`, `penetrator.spec.ts`, `settings.spec.ts`, `persistence.spec.ts` | Primary Chromium and managed Firefox use the actual served application; deterministic rule fixtures remain in test support. |
| Tooling/static distribution | `package.json`, `package-lock.json`, `tsconfig.json`, `vite.config.ts`, `vitest.config.ts` | Typecheck/unit/build and browser runner configuration | Pin actual selected tooling with the first implementation task; no runtime framework/backend. |

Files in the same table row can be combined or factored when implementation establishes better cohesion; substantive ownership changes update this layout and affected task scopes before use. Do not create speculative empty modules. `src/domain` cannot import session/config/browser/ui code. Config depends on typed ports, and concrete browser adapters are wired at composition. Tests may import public domain/session interfaces; production source never imports tests.

## Tests and reproducible execution

`tests/fixtures/` owns deterministic boards, piece supplies, clock inputs and adapter doubles. Unit/integration tests use Vitest and TypeScript. Browser tests use Playwright with the matching managed binaries and finite launch/action/process deadlines. A test-only harness may exercise injected complex fixtures, but it does not replace acceptance on the served production application. Never expose a public state-mutation backdoor merely to make browser tests convenient. Browser tests may supply deterministic random observations through their isolated environment.

The first tooling task establishes and documents planned scripts `npm run typecheck`, `npm test`, `npm run build` and `npm run test:e2e`, plus the local dev/preview command and browser provisioning instructions. These commands are not runnable/verified yet. Keep scripts compatible with Windows CMD and the repository shell policy; use Node entry points for platform-specific child-process selection rather than assuming PowerShell exists.

`dist/` owns generated static production output only. Keep `.browser-cache/`, `test-results/`, `playwright-report/`, coverage output, temporary profiles and local dependency directories ignored and out of the static bundle. An absolute dedicated browser path is configured for each environment; do not adopt the user's personal browser/profile. Ignore `*.tkn` and retain the existing credential convention; credentials cannot enter fixtures, builds or reports.

## Documentation and release artifacts

| Area | Owner and location |
| --- | --- |
| Brief/design/contracts | `docs/dev/PROJECT.md`, `ARCHITECTURE.md`, `DECOMPOSITION.md`, `SPEC.md` and `spec/` children. |
| Strategy/placement/executable work | `docs/dev/PLAN.md`, `layout.md`, `TASKS.md`; the task list is the sole implementation checkbox owner. |
| Preparation records/QC | `docs/dev/DOCS_TASKS.md`, `DOCS_PREPARATION.md`, `HANDOFF.md` and adjacent SPEC/PLAN/TASKS review reports. |
| Milestone/phase implementation evidence | `docs/dev/reports/phases/<phase-id>/<milestone-id>.md` and `PHASE-REPORT.md`. |
| Full implementation evidence | `docs/dev/reports/IMPLEMENTATION-REPORT.md`, produced by the final phase review. |
| User/developer usage | Root README and `docs/USER-GUIDE.md`, `docs/DEVELOPMENT.md` when their capability/tooling exists. |
| Version/distribution/release message | Version in root `package.json`; locked metadata aligned where relevant; generated `dist/`; root `RELEASE-NOTES.md` as the final release body. |
| Governing policy/plugin/manual provenance | Preserve root policy/disclosure files, `.agents/plugins/sdd-manager/` and `docs/ai-logs/` with their existing ownership. |

Each assigned milestone boundary task owns its report and HANDOFF update; each phase review owns its phase report and release-message preparation. Reports are evidence, not runtime assets or another source of executable checkboxes. Keep actual binary/cache artifacts untracked; retain concise commands, versions, hashes and findings in owning reports. Root AGENTS navigation points to current design/placement/task owners as they become available, and only advertises validated commands as runnable.
