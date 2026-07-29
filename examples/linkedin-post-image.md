# LinkedIn Post Image — Automation Spec

Context: solo operator · organic text posts · any image type.

---

## Objective

**Produce a visual that earns attention without costing credibility — or correctly decide none is needed.**

- **Measured by:** tracked newsletter subscriptions per post, via unique link in the first comment.
- **Scope:** one still image on an organic text post. Out: carousels, document posts, video, banners, article/newsletter headers.
- **Constraints:** no fabricated data · no rendered text unless verified correct · no real likenesses or unlicensed marks · legible at mobile thumbnail size · must not overstate the post's claim.
- **Trade-offs:** ≤15 min production. Legibility has a hard floor; novelty does not.
- **Stop criteria:** no image is a valid output. Three candidates failing the credibility bar → ship text-only. Skip entirely if an image would dilute the claim.

---

## Occurrence

- **Trigger:** post text is final.
- **Readiness:** one identifiable core claim · format confirmed as text post · generation tooling within quota · visual-constraint file accessible.
- **Authorisation:** permission to depict client / employer / NDA-covered material.
- **Window:** close to publish.
- **Classify archetype at trigger:**

| Archetype | Image must |
|---|---|
| Framework / concept | Show structure — diagram, not mood |
| Result / data | Show the real number |
| Build log / artifact | Show the real thing |
| Opinion / argument | Carry tone; often typographic |
| Personal reflection | Often **no image** |

---

## Order

**Flow:** final text → extract core claim → classify archetype → select route → generate candidates → screen → select → export → attach.

**Sharing:** generation credits · operator attention (the bottleneck).

**Fit:** image, hook, and first-comment link must compose. Image must not restate the hook verbatim.

**Concurrency:** three candidates generated in parallel, not serially.

**Complete when:** exported at current feed spec and passing the thumbnail test, *or* the no-image decision is recorded with its reason.

**Route priority:**

| # | Route | Use for |
|---|---|---|
| 1 | Real artifact — screenshot, output, actual diagram | Build logs, results, frameworks |
| 2 | Structured diagram, rendered from structure | Framework / concept |
| 3 | Typographic card, real typesetting | Opinion, argument, quote |
| 4 | Generative image | Atmosphere, metaphor, when nothing real exists |
| 5 | No image | Reflection; anything an image dilutes |

**Function allocation:**

| Step | Acq | Anal | Dec | Act |
|---|---|---|---|---|
| Extract core claim | 10 | 10 | 5 | — |
| Classify archetype | 10 | 10 | 5 | — |
| Select route | 10 | 10 | 5 | — |
| Construct prompt | — | 10 | 7 | 10 |
| Generate candidates | — | — | 10 | 10 |
| Screen failures | 10 | 7 | 7 | 7 |
| **Select final** | 10 | 7 | **1** | — |
| Export and attach | 10 | 10 | 10 | 7 |

---

## Option

**Variants:** the five routes above, in priority order.

**Exceptions:**

| Condition | Response |
|---|---|
| Rendered text garbled | Switch to route 3 with real typesetting — do not re-roll |
| Won't render legibly at thumbnail | Downgrade to abstract / textural |
| Generation quota exhausted | Route 1 or 5 |
| Three attempts fail the bar | Route 5 |

**Recovery / safe stop:** text-only publication. 15-minute timebox is a hard trigger, not a guideline.

**Disengage:** if image posts underperform text-only on a rolling basis, turn the automation off.

**Manual exercise:** periodically build one end to end by hand.

---

## Observation

**Record per post:** archetype · route · candidate count · elapsed time · shipped with image or text-only · prompt used · tracking link ID.

**Judge:**

| Term | Signal |
|---|---|
| Proportional | Subscriptions from this post vs. rolling baseline |
| Integral | Image vs. text-only, and per-archetype/per-route conversion, over ≥20 posts |
| Derivative | Candidate rejection rate over time — needs no attribution, moves first |

**Revise:** prompt library updates from what shipped, not what was attempted. Archetype→route mapping updates from per-archetype conversion. Both are files.

**External scan:** LinkedIn feed image dimensions · whether images still affect reach.

---

## Invariants

- **Ownership:** self. Prompt library and archetype→route mapping exist as files, not memory.
- **Objects:** post text · core claim · archetype · route · prompt · candidates · final export · log record.
- **Resources:** generation credits · operator attention · 15-minute budget · visual-constraint file.
- **Failure domain:** routes 3 and 4 may share one generation API. Only routes 1 and 5 are independent.
