# SPEC review report

## Current gate

State: **Ready for PLAN authoring**. Review owner: sdd-specify, 2026-10-24. Scope: SPEC and its geometry/configuration children; not whole-package QC or implemented-game acceptance. No remaining confirmed blocker.

Reviewed final states:

- `SPEC.md` SHA-256 `2de3f038a4ac2c3bd6bdec19bbd543e4d582765b211c5dc0d42ecccfaf8bf9a5`
- `spec/GEOMETRY.md` SHA-256 `796ad69a51b007e0b65a60ca87dfe8ad8c3b2fb7a4a8110d08f0da4c6b754307`
- `spec/CONFIGURATION.md` SHA-256 `2d4ce95c7cae084bd88e0d8d2bdf3cc00a6d18712d00cb4d7c52e26b4923cf64`

Governing accepted states:

- `PROJECT.md` SHA-256 `111827f3a0a641f7a469cf822d0c5d190c4ef84fb07503c9e6e32f5fb3c76993`
- `ARCHITECTURE.md` SHA-256 `1a64abae8e667ec2a9debab2706c6ac07ee7b7de6855f49e0ff199ea0cbc5745`
- `DECOMPOSITION.md` SHA-256 `19d2c8c915b4df18b7fee2a16d8226b59ab3e3e524bb8e6fb5dfe5980969eef8`

Acceptance basis is the user's PROJECT approval and subsequent autodoc document preapproval, recorded separately in DOCS_PREPARATION. No executable game or browser checks were run for this document-only gate.

## Initial review

Initial SPEC root SHA-256: `4f3616c14aa2b0a153761c33ce1ad8c8f57f2692681732cb09bba7bf93437190`. Compared all accepted PROJECT capabilities/decisions with the three specification nodes and the D1–D4/C1–C2/S1/V1–V2/A1–A2 responsibility map. Manually checked timer/event ordering, Hold supply effects, traversal/landing invariants, midline examples, complete six-setting source/write matrix, scope/non-goals and objective failure acceptance. Geometry tables are normative project data; this review does not certify affiliation with or complete compliance to any commercial ruleset.

| Contract group | Design owner / consumers | Coverage result |
| --- | --- | --- |
| G-01, G-03, G-04; geometry | D1–D4 with S1/V1/V2 | Board/spawn/rotation/supply, atomic clear/score/progression and top-out have objective examples and one authoritative owner. |
| G-02, G-07 | S1/A1 and D3; V2 policy notice | Input ordering, repeat, focus, pause, lifecycle cleanup, cadence and per-piece locking snapshots are coherent. Focus return needed clarification; see SPEC-F01. |
| G-05, G-06 | D1–D3, S1, V1/V2 | Hold/preview consumption, projected occupied-cell midline and hard-drop/ghost equality are explicit. |
| G-08 | D1/D3/D4 with V1/V2 | Bonus spend/award/cap, white rendering, safe final lock and transient-overlap constraints match the accepted proposal. |
| C-01; configuration child | C1/C2/A2/S1 | All six values/defaults, precedence, invalid/duplicate sources, omitted cookies, explicit defaults, independent writes and reload acceptance are covered. |
| Q-01 | Browser adapters and presentation | Static distribution, textual status/controls, reproducible tooling and both isolated browsers are explicit; game acceptance remains planned. |

| Finding | Location / consequence | Owner / correction | Disposition |
| --- | --- | --- | --- |
| SPEC-F01 | Q-01 and G-02 excluded gameplay keys in focused controls without specifying a keyboard route back to play; a player could appear stuck after Start/settings. | sdd-specify: require a focusable labelled board, Start focus return, and keyboard/click return from controls. | Resolved in Revision 1. |

The child split keeps geometry and external setting representation independently navigable without repeating their normative tables in the root. No material design change, invented service, unresolved product decision or additional scope is needed.

## Revision 1

Added focus-entry/return guarantees in Q-01 without changing accepted hotkey exclusions or gameplay timing. Rechecked G-02 and presentation responsibilities against the amended text, plus parent/child links, headings, independent setting semantics and root-state preservation. The final reviewed hashes above identify the corrected state. SPEC-F01 is resolved; no other confirmed issue remains. Local link/heading/diff checks accompany publication. PLAN may consume these contracts; implementation and whole-package QC remain unperformed.
