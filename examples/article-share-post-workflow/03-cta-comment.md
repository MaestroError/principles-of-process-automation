# 03 · CTA Comment — Subprocess Spec

Parent: [`00-main-workflow`](./00-main-workflow.md)

## Contract

| | |
|---|---|
| **Guaranteed by parent** | Post text final (runs after `01`) · article URL validated · hook available for fit-checking |
| **Consumes** | Article URL · post hook and body · CTA library · tracking service |
| **Produces** | Comment text containing exactly one tracked link |
| **Escalates (hard)** | Nothing |
| **Degrades (soft)** | Tracking unavailable → raw URL + flag: this post is unmeasured |

---

## Objective

**Carry the link and give a reason to click, without repeating what the post already said.**

- **Measured by:** click-through and tracked conversions per post, segmented by CTA phrasing.
- **Constraints:** exactly one link · must not restate the hook · must not promise more than the article delivers · destination shown must be the destination reached — no misleading link text · comment fits without truncation.
- **Stop:** degrade to a bare link with a minimal CTA. Never omit the link.

## Occurrence

- **Trigger:** `01` has produced final post text.
- **Readiness:** tracking service reachable · CTA library accessible.
- **Window:** the comment is posted immediately after publish, never later — a post that sits without its link loses its first and best distribution window.

## Order

| Step | Acq | Anal | Dec | Act |
|---|---|---|---|---|
| Generate tracked link, campaign = run ID | — | 10 | 10 | 10 |
| Derive CTA angle complementary to hook | 10 | 10 | 10 | 10 |
| Draft comment | — | 10 | 10 | 10 |
| Verify tracked link resolves to the article | 10 | 10 | 10 | 10 |
| Fit check — no hook repetition | 10 | 10 | 10 | 10 |

**Fit:** the comment must add a reason, not echo the hook. If the hook states the problem, the CTA states what the article does about it.
**Complete when:** comment text produced, link verified to resolve to the correct article.

## Option

| Condition | Response |
|---|---|
| Tracking service unreachable | **Raw URL + flag.** Do not delay publish for measurement |
| Tracked link resolves anywhere but the article | Discard the wrapper, use the raw URL, flag |
| Draft repeats the hook | Regenerate once, then fall back to the library's neutral CTA |
| CTA library unavailable | Minimal CTA: one line plus the link |

**Safe stop:** bare link, no CTA copy. The link is the non-negotiable element; the copy is not.

## Observation

**Record:** CTA phrasing used · tracked or raw · link ID · whether fit check triggered a regeneration.

| Term | Signal |
|---|---|
| Proportional | Per-run tracking failures |
| Integral | Conversion by CTA phrasing over ≥20 runs — the CTA library ranks itself |
| Derivative | Rising regeneration rate → CTA library drifting toward the hook style |

**Revise:** CTA library reordered by measured conversion; low performers retired.

## Invariants

- **Ownership:** CTA library is a file.
- **Objects:** article URL · tracked link · link ID · post hook · comment text.
- **Resources:** tracking service · CTA library.
- **Failure domain:** tracking service only — independent of the publisher and of LinkedIn.
