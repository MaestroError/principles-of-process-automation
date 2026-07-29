# 04 · Assembly & Review — Subprocess Spec

Parent: [`00-main-workflow`](./00-main-workflow.md)

This subprocess is the workflow's single human checkpoint and its escalation endpoint.

## Contract

| | |
|---|---|
| **Guaranteed by parent** | Post text present · image present or explicitly `none` · comment text present or degraded · all flags collected |
| **Consumes** | All subprocess outputs and flags |
| **Produces** | One assembled draft · flag summary · operator decision · edit diff attributed by subprocess |
| **Escalates (hard)** | Nothing — escalations terminate here |
| **Degrades (soft)** | Nothing. If this subprocess cannot run, the workflow has no output |

---

## Objective

**Give the reviewer one complete artifact and everything needed to decide in a single pass.**

- **Measured by:** review time · number of review passes per run (target: one).
- **Constraints:** never publish without explicit approval · every flag surfaced, never buried · **the image preview must render at actual feed thumbnail size**, not full size · the link must be shown by its resolved destination, not its tracking wrapper.
- **Stop:** reject → save draft with reasons, publish nothing.

> Previewing an image at full size lets the reviewer approve something that fails at the size the audience will actually see. The preview must show what the feed shows.

## Occurrence

- **Trigger:** `01`, `02`, `03` have all returned — including soft-degraded returns.
- **Readiness:** flag set complete · feed-fidelity preview renderer available.
- **Authorisation:** the operator is the only party who may approve.

## Order

| Step | Acq | Anal | Dec | Act |
|---|---|---|---|---|
| Collect outputs and flags | 10 | 10 | 10 | 10 |
| Run fit checks | 10 | 10 | 10 | 10 |
| Render preview at feed fidelity | — | 10 | 10 | 10 |
| Surface flags with their reasons | 10 | 10 | 10 | 10 |
| **Approve / edit / reject** | 10 | 7 | **1** | — |
| Capture edit diff by subprocess | 10 | 10 | 10 | 10 |
| Publish, **then** post comment | — | 10 | 10 | 7 |

**Fit checks, all mandatory before presenting:**

1. Post text, image provenance, and comment link all refer to the same article.
2. The comment does not repeat the hook.
3. The link resolves to the article.
4. The image renders legibly at thumbnail size.
5. No link appears in the post body.

**Complete when:** published with its comment, or draft saved with reasons.

## Option

| Condition | Response |
|---|---|
| Operator edits the draft | Capture the diff, **re-run fit checks**, re-present only if a check now fails |
| A fit check fails before presenting | Present anyway, with the failure named — do not silently repair |
| Operator rejects | Save draft and reason. Stop |
| Publish fails | Retain the draft intact. Retry once, then report |
| **Publish succeeds, comment fails** | **Critical.** The post is live with no link. Retry immediately; on second failure alert the operator at once |

**Safe stop:** saved draft. No external dependency.

**Manual exercise:** the level-1 approval here is the only human decision in the workflow and is deliberately not delegable. It is also what allows every subprocess to omit its own human checkpoint.

## Observation

**Record:** flags surfaced · fit-check results · **edit diff attributed to the originating subprocess** · approve/reject + reason · review passes · elapsed review time.

| Term | Signal |
|---|---|
| Proportional | Per-run rejections and fit-check failures |
| Integral | **Edit distance by subprocess over ≥20 runs** — routes improvement effort to whichever subprocess is corrected most · which flags predict rejection |
| Derivative | Rising review time or pass count → assembly quality degrading before rejections appear |

**Revise:** flags that never change a decision are removed — a flag nobody acts on trains the reviewer to skim. Flags that predict rejection are promoted.

## Invariants

- **Ownership:** the operator, exclusively. No delegation of approval.
- **Objects:** post text · image + provenance · comment text · flag set · assembled draft · edit diff · decision record.
- **Resources:** preview renderer · operator attention · LinkedIn publish and comment APIs.
- **Failure domain:** LinkedIn only. Saving the draft depends on nothing.
