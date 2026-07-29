# 02 · Image — Subprocess Spec

Parent: [`00-main-workflow`](./00-main-workflow.md)

Two routes to one objective: **harvest** the publisher's designated image, or **design** one from the article title.

## Contract

| | |
|---|---|
| **Guaranteed by parent** | Snapshot present with raw HTML and metadata · page reachable and validated · title and publication available |
| **Consumes** | Snapshot · article title · publication name · declared angle (design route only, from `01`) |
| **Produces** | Image at feed spec + provenance record `{route, source}` — **or** explicit `none` |
| **Escalates (hard)** | Nothing. This subprocess never halts the run |
| **Degrades (soft)** | Returns `none` → parent assembles text-only, flagged · **any tier fallthrough, retry, or route switch is flagged, never silent** |

---

## Objective

**Give the post a visual that matches the article and does not misrepresent its source.**

- **Constraints:** harvest only publisher-designated images · never an image from a different article · do not crop out credits or watermarks · do not evade bot protection · do not upscale · a designed image must not imply it came from the publisher · rendered text must be verbatim and correctly spelled · legible at mobile thumbnail size.
- **Stop:** return `none`. Never a hard failure.

## Occurrence

- **Trigger:** snapshot available (harvest) · declared angle available (design).
- **Route selection at trigger:**

| Condition | Route |
|---|---|
| Designated image present, valid, not a site default | **A — Harvest** |
| Designated image absent, site-default, or below minimum | **B — Design** |
| Both routes exhausted | `none` |

---

## Order — Route A · Harvest

**Candidate precedence:**

| Tier | Source |
|---|---|
| 1 | `og:image` / `og:image:secure_url` |
| 2 | `twitter:image` |
| 3 | `<link rel="image_src">` |
| 4 | JSON-LD `Article.image` |
| — | none → Route B |

**Gates:** ≥640px wide · JPG or PNG · not SVG · resolves to a real image, not a pixel or 404.
**Site-default check:** the same image URL recurring across multiple articles from one domain is a logo, not a featured image → Route B.

| Step | Acq | Anal | Dec | Act |
|---|---|---|---|---|
| Select candidate, tiers 1–4 | 10 | 10 | 10 | 10 |
| Validate gates | 10 | 10 | 10 | 10 |
| Site-default check | 10 | 7 | 7 | 7 |
| Download and resize | — | 10 | 10 | 10 |

## Order — Route B · Design

**Composition:** related illustration + article title + publication attribution.

| Step | Acq | Anal | Dec | Act |
|---|---|---|---|---|
| Derive illustration concept from title + angle | 10 | 10 | **5** | — |
| Source illustration | 10 | 10 | 10 | 10 |
| Compose card — title verbatim, publication credited | — | 10 | 10 | 10 |
| Verify rendered text character-for-character | 10 | **7** | 7 | 7 |
| Export at feed spec | — | 10 | 10 | 10 |

**Constraints specific to this route:**

- Title must be **verbatim** — not paraphrased, not truncated mid-clause.
- Publication must be credited on the card.
- Illustration must be abstract or conceptual — **no depiction of real people, real events, or anything that reads as reportage.** A designed card must be visibly a card, not a photograph, so it cannot be mistaken for the publisher's own imagery.
- No data, charts, or figures — those would be fabricated.

**Complete when:** image exported at feed spec with a provenance record, or `none` returned.

---

## Option

| Condition | Response |
|---|---|
| Tier 1 image 404s or is a tracking pixel | Next tier — **flag the fallthrough** so `04` surfaces it; do not substitute silently |
| All tiers fail | Route B |
| Harvested image below minimum resolution | Route B — do not upscale |
| 403 / bot detection **on the image host** | One retry with conventional UA — **recorded whether or not it succeeds**, then Route B. Do not escalate evasion. (The article page itself was already validated at the parent gate; image assets often sit on a separate CDN that blocks independently) |
| Design route: text renders incorrectly | Typographic-only card, no illustration |
| Design route: illustration source unavailable | Typographic-only card |
| Typographic card also fails | `none` |

**Safe stop:** `none`. Always available, no external dependency.

**Failure domains:** Route A — publisher's server. Route B — illustration source. Independent.

**No level-1 step.** Human checkpoint is the parent's review at `04`.

---

## Observation

**Record:** route taken · winning tier (A) · illustration concept (B) · site-default flag · image dimensions · provenance.

| Term | Signal |
|---|---|
| Proportional | Per-run route-B fallbacks and `none` outcomes |
| Integral | Tier-1 rate by domain · route distribution over ≥20 runs · reviewer rejection rate, route A vs route B |
| Derivative | Rising fetch-failure rate → publishers tightening access |

**Revise:** **per-domain override table** — which domains need a specific tier, which publish site-defaults as `og:image`, which route straight to B. This file is the accumulated intelligence of the subprocess.

Page rendering is not in this table — the parent owns fetch and rendering at its gate.

## Invariants

- **Ownership:** per-domain override table and illustration concept library are files.
- **Objects:** snapshot · candidate list · selected image URL · downloaded image · illustration · composed card · resized export · provenance record.
- **Resources:** image host / CDN · illustration source · ~60s (A) / ~3 min (B). *No page fetching — the parent supplies the snapshot.*
