# Configuration and persistence

This child of [SPEC](../SPEC.md) owns C-01. C1/C2 resolve selected settings; A2 supplies cookie/URL access; S1 applies gameplay timing.

## Schema

Matching is case-sensitive. No whitespace trimming, case folding or numeric/Boolean coercion is applied. Each cookie has a separate name; no serialized all-settings blob is used.

| Setting / HTML control | URL parameter | Cookie | Legal values | Default | Application |
| --- | --- | --- | --- | --- | --- |
| Ghost visibility / select | `ghost` | `tetris_ghost` | `hide`, `dynamic`, `show` | `show` | Immediate |
| Hard drop / checkbox | `hardDrop` | `tetris_hardDrop` | `off`, `on` | `on` | Immediate availability |
| Next preview / checkbox | `next` | `tetris_next` | `off`, `on` | `on` | Immediate |
| Hard-drop lock / select | `hardDropLock` | `tetris_hardDropLock` | `follow`, `immediate` | `follow` | Next active spawn |
| General lock / select | `lock` | `tetris_lock` | `failed`, `interval` | `interval` | Next active spawn |
| Hold / checkbox | `hold` | `tetris_hold` | `off`, `on` | `on` | Immediate availability |

Before persistence is delivered, the same schema/defaults and session effects apply, but source loading and browser writes are absent. Selected locking policies and active-piece effective policies must be distinguished in a concise notice when different. Next spawn includes a new piece entering via Hold. Changing a setting never restarts the active timer, advances paused time, mutates the settled board or clears the Hold slot. A new game retains selected settings and applies their locking policies immediately to its first piece.

## Resolution on startup

For each setting independently, select the first URL occurrence with that exact parameter name. Decode it using normal URL query parsing. If it is a legal value, use it and attempt to save it in its corresponding cookie, including when it equals the default. Do not consult a later duplicate to rescue an invalid first occurrence.

If the parameter is absent or invalid, use the corresponding cookie if readable and legal. Otherwise use the default. An empty string is invalid. Cookie lookup uses the first exact named cookie in the browser's readable cookie sequence; malformed or undecodable cookie values are invalid. A failed read is treated as unavailable for only that source. Unrecognized parameters/cookies do not affect game settings.

An omitted parameter never causes a cookie to be overwritten with a default. Invalid URL values are not saved to cookies. Do not erase invalid cookie values during fallback; later valid explicit URL values or user changes may replace them. Startup does not add omitted query parameters or normalize an invalid URL. Resolve all settings before starting the first active piece.

## User changes and writes

A valid user selection updates memory and its control immediately, then independently attempts both cookie and URL write operations. Selecting a value equal to the existing/default value still performs these writes. Reject an invalid programmatic setting update without changing selection or either source. Never apply a cookie/URL write failure as a reason to undo the valid in-memory selection.

Write only that setting's cookie, with the exact schema value, `Path=/`, `Max-Age=31536000`, `SameSite=Lax` and `Secure` on HTTPS. Cookies are origin/browser-specific; cross-device persistence is outside scope. No sensitive/session game state is stored. Where browser APIs permit readback, detect a denied cookie write and expose a concise persistence-unavailable status.

Use History replacement to update the current URL without navigation or an additional history entry. Replace all occurrences of the changed setting's parameter with one canonical occurrence. Preserve all unrelated parameters and their decoded values, including duplicate unrelated keys, plus the path and fragment; byte-for-byte query encoding/order preservation is unnecessary. A URL write failure must not prevent the cookie attempt, and a cookie write failure must not prevent the URL attempt.

If source access or writes fail, the current game remains usable with resolved/in-memory settings. Show a nonblocking textual persistence status when the failure is detectable. Do not claim that an undetectably blocked browser write succeeded. Retry on a later explicit valid selection; no background retry service or cross-tab synchronization is required. Loading a URL in another tab creates an independent game resolved from that tab's URL and current origin cookies.

## Acceptance matrix

| Scenario | Expected result |
| --- | --- |
| No URL and no cookies | All schema defaults; no startup cookie writes for omitted keys. |
| `ghost=hide` plus cookie `show` | Select `hide`, write `hide` cookie. |
| `ghost=show` plus cookie `hide` | Select explicit default `show`, overwrite cookie with `show`. |
| No `hold` parameter plus cookie `off` | Hold stays off and its cookie is retained. |
| Invalid `lock=fast` plus cookie `failed` | Use `failed`; do not persist `fast`. Other settings resolve independently. |
| Invalid URL and invalid/missing cookie | Use only that setting's default; do not poison other settings. |
| `ghost=bad&ghost=hide` plus cookie `dynamic` | First occurrence invalid; use cookie `dynamic`. |
| Cookie/read access denied, valid `hold=off` | Select `off`; failed persistence is nonblocking. |
| User changes ghost on a URL with unrelated keys/fragment | Update memory, cookie and one ghost parameter; unrelated decoded entries and fragment survive. |
| Either persistence write fails | Attempt the other write; retain selected state and keep playing. |
| Reload after a saved selection | Restore from the explicit URL, or from cookie when that parameter is removed. |

Exercise these rows for every applicable setting, not just the examples named. Mixed-source acceptance must include one valid URL setting, one cookie-only setting, one invalid-URL/valid-cookie setting and one default in the same startup. Real-browser reload tests must verify cookies and replacement URLs on a served HTTP/HTTPS origin, rather than relying solely on mocked adapters or a file URL.
