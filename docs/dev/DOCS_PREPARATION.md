# Main documentation preparation record

## Current control

- Mode: autodoc/onepass, selected by the user's project request on 2026-10-24.
- Scope: complete browser Tetris project including all requested gameplay, penetrator, configuration and persistence capabilities; simplest sensible baseline first.
- Approval basis: The user approved PROJECT and its proposed decisions in the current conversation (2026-10-24). Autodoc preapproves subsequent document checkpoints ARCHITECTURE through TASKS; it does not accept unresolved material product choices.
- Tracking: enabled for preparation and implementation by root AGENTS.md. Publication: push and read back each owned commit.
- Next boundary: DOCS-008 closure readback, then stop before DOCS-009; advance requires new direction.
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
| DOCS-005 | `docs/dev/SPEC.md` SHA-256 `2de3f038a4ac2c3bd6bdec19bbd543e4d582765b211c5dc0d42ecccfaf8bf9a5`; `docs/dev/spec/GEOMETRY.md` SHA-256 `796ad69a51b007e0b65a60ca87dfe8ad8c3b2fb7a4a8110d08f0da4c6b754307`; `docs/dev/spec/CONFIGURATION.md` SHA-256 `2d4ce95c7cae084bd88e0d8d2bdf3cc00a6d18712d00cb4d7c52e26b4923cf64`; `docs/dev/SPEC-REVIEW-REPORT.md` SHA-256 `c5ff49a17bbc5e411de2dd3cd5d5ed86392e3a27964f8ca5a5dff4ea592afc30`. Acceptance basis: autodoc preapproval after user acceptance of PROJECT. Scoped conformance/ownership review, local-link and heading checks passed; applicable adjacent report records substantive findings and readiness. |
| DOCS-006 | `docs/dev/PLAN.md` SHA-256 `df101b37fc2c4daf1e36c795597352d8f009c2b61fc4ef4cf199da6cb3066992`; `docs/dev/PLAN-REVIEW-REPORT.md` SHA-256 `0762c194e713feb20e0189f2c2042369c3dcec5ac30329f4b9abcb03e4959e61`. Acceptance basis: autodoc preapproval after user acceptance of PROJECT. Scoped conformance/ownership review, local-link and heading checks passed; applicable adjacent report records substantive findings and readiness. |
| DOCS-007 | `docs/dev/layout.md` SHA-256 `092fb569553466ff5b46e908b0407a0ec589b1e7f723f3da07b4eb91f174b353`; `docs/dev/PLAN.md` SHA-256 `e62a1e1ed5012bfe3f3778846d9ad929bd62f1ffab245c9ffb236936cc05c9d5`; `docs/dev/PLAN-REVIEW-REPORT.md` SHA-256 `11cd5d59e4128bd8c4c4118bfd130021854778f311aa8b035aa8db8bb76ce1c4`; `AGENTS.md` SHA-256 `9993b1396c1d7f94e4b44ddcedca3eebff5de23caecd034b53bcf9a680d08054`. Acceptance basis: autodoc preapproval after user acceptance of PROJECT. Scoped conformance/ownership review, local-link and heading checks passed; applicable adjacent report records substantive findings and readiness. |
| DOCS-008 | `docs/dev/TASKS.md` SHA-256 `07d3f8a0a1c20e8aa3b5c58df324497f2375d3b8d98112f3a96e0b77f15e441c`; `docs/dev/TASKS-REVIEW-REPORT.md` SHA-256 `2e298fc07fd8a92675a4767a7605e47ec8af86ab865b19b99b61a8f7ab70e6a0`; `docs/dev/HANDOFF.md` SHA-256 `59553942a5cd680a25017c78df93e5d4c1c1cc5ef1211b3f03a22315438dff3d`; `AGENTS.md` SHA-256 `c69e142ac085699739467b8ed7cd868b8631676b5a12c3d0dae9e7937d1f5cb8`. Acceptance basis: autodoc preapproval after user acceptance of PROJECT. Scoped conformance/ownership review, local-link and heading checks passed; applicable adjacent report records substantive findings and readiness. |
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

All preparation tasks preceding DOCS-008 have published commits and verified issue closures. Publish/read back the present DOCS-008 completion, then close/read back issue 8. Stop after this closure, before DOCS-009. DOCS-009 and documentation milestone 1 remain open. Whole-package QC, preparation integration and implementation remain outside this range.
