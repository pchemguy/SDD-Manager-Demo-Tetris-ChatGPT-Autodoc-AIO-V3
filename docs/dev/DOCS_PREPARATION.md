# Main documentation preparation record

## Current control

- Mode: autodoc/onepass, selected by the user's project request on 2026-10-24.
- Scope: complete browser Tetris project including all requested gameplay, penetrator, configuration and persistence capabilities; simplest sensible baseline first.
- Approval basis: The user approved PROJECT and its proposed decisions in the current conversation (2026-10-24). Autodoc preapproves subsequent document checkpoints ARCHITECTURE through TASKS; it does not accept unresolved material product choices.
- Tracking: enabled for preparation and implementation by root AGENTS.md. Publication: push and read back each owned commit.
- Next boundary: proceed through DOCS-008, then stop before DOCS-009.
- Reporting: Standard after Explicit bootstrap; available profiles are Minimal, Standard and Explicit.

## Scope source and decisions

The user requests desktop browser Tetris: classic falling tetrominoes, movement, rotation, clearing, score and increasing speed; Hold, ghost, 7-bag, wall kicks, hard drop, full-gravity-interval default locking; configurable dynamic ghost visibility; penetrator traversal without destruction, valid final placement, lowest-valid hard drop/ghost, four-line bonus awards capped at three, white penetrator and bonus symbols; all six configuration controls; independent URL/cookie/default resolution and persistence on change, preserving cookies for omitted parameters and saving explicit defaults. Session-only settings may precede persistence. Release every implemented, verified and integrated phase with a managed version/tag and notes.

Material choices presented in [PROJECT](PROJECT.md): midline-straddling ghosts; lock timing and resets; penetrator activation, movement, Hold and locking; invalid and duplicated configuration values; live policy changes; proposed technology and non-goals. The user accepted these proposed decisions with PROJECT approval. No new material decision is unresolved. Detailed proposed resolutions are retained in PROJECT rather than duplicated here. No game implementation or release is authorized by documentation acceptance alone.

## Decisions and document evidence

| Task | Evidence / decision basis |
| --- | --- |
| DOCS-001 | All four existing root files retained byte for byte against initial commit 125b90e1e6e456a627acd259d735d244cce82c6c; no root copies needed. Task list, this record and HANDOFF initialized together. Packaged provenance scaffold copied and integrated as described below. |
| DOCS-002 | PROJECT proposal SHA-256 `111827f3a0a641f7a469cf822d0c5d190c4ef84fb07503c9e6e32f5fb3c76993`; Human accepted the exact proposal in commit 5d02e2e6ac3100a36fe2fb26fd35ff37f4b33322 with “Approve”. Reviewed against the complete request for scope, consequential interactions, document boundaries and Markdown/link hygiene. Accepted proposal bytes retained unchanged; defaults and non-goals carry this human acceptance. |
| DOCS-003 | `docs/dev/ARCHITECTURE.md` SHA-256 `1a64abae8e667ec2a9debab2706c6ac07ee7b7de6855f49e0ff199ea0cbc5745`. Acceptance basis: autodoc preapproval after user acceptance of PROJECT. Scoped conformance/ownership review, local-link and heading checks passed; applicable adjacent report records substantive findings and readiness. |
| DOCS-004 | `docs/dev/DECOMPOSITION.md` SHA-256 `19d2c8c915b4df18b7fee2a16d8226b59ab3e3e524bb8e6fb5dfe5980969eef8`. Acceptance basis: autodoc preapproval after user acceptance of PROJECT. Scoped conformance/ownership review, local-link and heading checks passed; applicable adjacent report records substantive findings and readiness. |
| DOCS-005 | Not started; autodoc checkpoint preapproved. |
| DOCS-006 | Not started; autodoc checkpoint preapproved. |
| DOCS-007 | Not started; autodoc checkpoint preapproved. |
| DOCS-008 | Not started; autodoc checkpoint preapproved. |
| DOCS-009 | Not started; outside the selected autodoc stop. |

## Initialization

- Initial root-file set: all four present, so no mixed-state continuation pause applies.
- Preserved: AI_DISCLOSURE.md, SDD-MANAGER.md, AGENTS.md, SKILL_DISCOVERY_PROTOCOL.md; verified exact original Git bytes. Browser and Windows shell policies also retained.
- Package: repository-bundled SDD Manager 0.15.2, pinned in initial commit 125b90e1e6e456a627acd259d735d244cce82c6c. Task/control assets use this source.
- Discovery: no standalone repository skills; bundled SDD Manager routes the main-development workflow. No product code, dependencies or test commands exist yet.
- Execution: Linux Bash, Git 2.51.1 and Node 24.22.1; Python available for supervised publication. Windows-only shell policy does not govern this host.
- Manual provenance: default enabled. Scaffold seeded on design-docs/ai-logs from initial main 125b90e1e6e456a627acd259d735d244cce82c6c in a3b3dfec9883e4baaec3f1b43d1c886fcaa06c3a, then explicitly merged into main in dec6694dce4db88f9d052e6a16f85268433cbe17. Both branches published with exact-ref readback and confirmed cleanup. Both assets match packaged bytes; no conversation transcript created.
- Preparation branch: design-docs/main from published main dec6694dce4db88f9d052e6a16f85268433cbe17.
- Pre-write tracking: native sdd-docs-main milestone 1 and DOCS-001–009 issues 1–9 created from exact packaged definitions, then all identities/content/associations read back before target modifications. All were open at that gate.
- Credentials: supplied token saved only after projection readback; ignored and untracked under *.tkn. No value is recorded here.
- Reset: none; onepass.

## Pending transitions

All preparation tasks preceding DOCS-004 have published commits and verified issue closures. Publish/read back the present DOCS-004 completion, then close/read back issue 4. Continue with DOCS-005 under autodoc preapproval. DOCS-009 and documentation milestone 1 remain open. Whole-package QC, preparation integration and implementation remain outside this range.
