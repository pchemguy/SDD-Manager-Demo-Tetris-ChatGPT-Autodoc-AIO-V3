# Piece geometry and rotation

This child of [SPEC](../SPEC.md) owns geometry for G-01, G-03, G-06 and G-08. D1 is the canonical implementation owner.

## Matrices and coordinates

A dot is empty; a letter is occupied. Spawn origins are `(3,0)` for 3×3 and 4×4 matrices and `(4,0)` for O. Each matrix row below is separated by a slash. Empty matrix cells outside the board do not invalidate a placement; occupied cells do.

| Kind | Canonical spawn matrix | Rotation frame |
| --- | --- | --- |
| I | `..../IIII/..../....` | 4×4 |
| J | `J../JJJ/...` | 3×3 |
| L | `..L/LLL/...` | 3×3 |
| O | `OO/OO` | 2×2, fixed occupied cells |
| S | `.SS/SS./...` | 3×3 |
| T | `.T./TTT/...` | 3×3 |
| Z | `ZZ./.ZZ/...` | 3×3 |

Orientation labels are 0, R, 2 and L clockwise. Generate clockwise cell coordinates in an N×N frame with `(x,y) -> (N-1-y,x)`; inverse rotation generates counterclockwise states. O leaves occupied cells unchanged and uses only offset `(0,0)`. For I/J/L/S/T/Z, test the target orientation at each ordered kick offset below relative to the original origin, accepting the first clear in-board occupied-cell result. There is no negative-row spawn buffer. When every candidate fails, retain all original piece/timer state.

## SRS kick offsets

Offsets use this project's downward-positive y coordinate. The tables define the complete ordered 90-degree kick behavior, including `(0,0)` as the first candidate.

| Transition | J/L/S/T/Z ordered `(dx,dy)` |
| --- | --- |
| 0→R | `(0,0), (-1,0), (-1,-1), (0,2), (-1,2)` |
| R→0 | `(0,0), (1,0), (1,1), (0,-2), (1,-2)` |
| R→2 | `(0,0), (1,0), (1,1), (0,-2), (1,-2)` |
| 2→R | `(0,0), (-1,0), (-1,-1), (0,2), (-1,2)` |
| 2→L | `(0,0), (1,0), (1,-1), (0,2), (1,2)` |
| L→2 | `(0,0), (-1,0), (-1,1), (0,-2), (-1,-2)` |
| L→0 | `(0,0), (-1,0), (-1,1), (0,-2), (-1,-2)` |
| 0→L | `(0,0), (1,0), (1,-1), (0,2), (1,2)` |

| Transition | I ordered `(dx,dy)` |
| --- | --- |
| 0→R | `(0,0), (-2,0), (1,0), (-2,1), (1,-2)` |
| R→0 | `(0,0), (2,0), (-1,0), (2,-1), (-1,2)` |
| R→2 | `(0,0), (-1,0), (2,0), (-1,-2), (2,1)` |
| 2→R | `(0,0), (1,0), (-2,0), (1,2), (-2,-1)` |
| 2→L | `(0,0), (2,0), (-1,0), (2,-1), (-1,2)` |
| L→2 | `(0,0), (-2,0), (1,0), (-2,1), (1,-2)` |
| L→0 | `(0,0), (1,0), (-2,0), (1,2), (-2,-1)` |
| 0→L | `(0,0), (-1,0), (2,0), (-1,-2), (2,1)` |

A classic increment before wall kicks are delivered tests only `(0,0)`, as scoped in PLAN; the complete game uses all listed candidates. This table and frame convention determine the game's behavior without requiring an external rules document. Verification must cover every orientation pair and first-valid candidate ordering, an I-specific wall/floor fixture, O stability, top-bound rejection and a fully blocked sequence.

## Landing

For regular mode, start at the current clear placement and advance downward while the next placement is clear; the last clear placement is the landing. For penetrator mode, examine all origins from current y through the lowest in-bounds origin for that occupied orientation and return the greatest clear y. If none exists, return no landing. Never treat a transient overlapping row as a regular supported/lockable position. Ghost, hard drop and penetrator gravity use this canonical result.
