# Article-Share Post Image — Automation Spec

Context: solo operator · article-sharing posts · article URL in the first comment.

**In:** final post text · first-comment draft containing the article URL.
**Out:** the article's own featured image, attached — or nothing.

---

## Objective

**Attach the linked article's own designated sharing image to the post.**

Restores the preview card suppressed by placing the link in the first comment.

- **Scope:** article-share posts with the URL in the first comment. Out: original content, multi-article roundups, video, non-article destinations.
- **Constraints:** use only the publisher's designated sharing image · never an image from a different article than the one linked · do not crop out watermarks, credits, or attribution · do not evade bot protection · do not upscale.
- **Trade-offs:** none. If this needs judgement, the input is wrong.
- **Stop criteria:** no designated image · below minimum resolution · fetch blocked · destination ambiguous → publish text-only. Never substitute a generated image.

---

## Occurrence

- **Trigger:** post text final **and** first-comment draft containing the URL exists.
- **Readiness:** exactly one URL · resolves, and final URL after redirects is on the expected domain · fetched page is the article, not a gate or interstitial.
- **Authorisation:** presence of a designated sharing image. Its absence is a no.
- **Window:** **before publish.** Editing a live post degrades distribution. The window does not reopen.
- **Classify page at fetch:**

| Page type | Response |
|---|---|
| Article, designated image present | Primary path |
| Article, no designated image | Screenshot route or stop |
| Paywall / login wall | Screenshot route or stop |
| Consent / interstitial | Retry post-consent or stop |
| JS-rendered, no metadata in raw HTML | Render once, re-evaluate |
| Not an article | Abort — out of scope |

---

## Order

**Flow:** comment draft → extract URL → resolve redirects → fetch → classify page → select candidate → download → validate → resize → attach → *publish* → *post comment*.

**Lifecycle note:** the process consumes the *draft* comment. The published comment can only exist after publish.

**Fit:** image, post text, and comment link must refer to the same article.

**Sharing:** publisher rate limits, only if run in batch.

**Complete when:** image attached at feed spec, *or* text-only decision recorded with reason.

**Candidate precedence:**

| Tier | Source | Confidence |
|---|---|---|
| 1 | `og:image` / `og:image:secure_url` | Designated |
| 2 | `twitter:image` | Designated |
| 3 | `<link rel="image_src">` | Designated, legacy |
| 4 | JSON-LD `Article.image` | Designated |
| 5 | First `<figure>` in article body | **Not designated — human confirms** |
| — | none | Stop criterion |

**Validation gates:** ≥640px wide · JPG or PNG · not SVG · resolves to a real image, not a pixel or 404.

**Site-default detection:** if the same image URL recurs across multiple articles from one domain, it is a site logo, not a featured image. Flag for human decision.

**Function allocation:**

| Step | Acq | Anal | Dec | Act |
|---|---|---|---|---|
| Extract and resolve URL | 10 | 10 | 10 | 10 |
| Fetch and classify page | 10 | 10 | 10 | 10 |
| Select candidate, tiers 1–4 | 10 | 10 | 10 | 10 |
| Select candidate, tier 5 | 10 | 7 | **5** | — |
| Validate dimensions/format | 10 | 10 | 10 | 10 |
| Site-default check | 10 | 7 | **5** | — |
| Resize and attach | — | 10 | 10 | 7 |
| Final glance before publish | — | — | **1** | — |

---

## Option

**Variants:** (a) designated image, tiers 1–4 · (b) body image, tier 5, human-confirmed · (c) screenshot of article hero · (d) no image.
Excluded: generated image — outside this objective.

**Exceptions:**

| Condition | Response |
|---|---|
| 403 / bot detection | One retry with conventional UA — **record the retry whether or not it succeeds**. Still blocked → (c) or (d). Do not escalate evasion |
| Paywall or interstitial | Not the article → (c) or (d) |
| No metadata in raw HTML | Render once headless, re-evaluate → (c) or (d) |
| Image URL 404s or is a tracking pixel | Next tier — **flag the fallthrough**, do not substitute silently |
| Below minimum resolution | (d). Do not upscale |
| Redirect lands on unexpected domain | **Hard stop, human review** |
| Two URLs in the comment | Hard stop — ask which |

**Recovery / safe stop:** publish text-only. Zero external dependency.

**Manual exercise:** retain the pre-publish glance — publishers' designated images sometimes misrepresent their own articles.

---

## Observation

**Record per run:** submitted URL · resolved URL · page classification · winning tier · image dimensions · site-default flag · human override · elapsed time · outcome.

**Judge:**

| Term | Signal |
|---|---|
| Proportional | Per-run failures: blocked fetch, no image, resolution too low |
| Integral | Tier-1 success rate by domain — chronic fallthrough justifies a rule |
| Derivative | Trend in fetch-failure rate — predicts degradation before failure |

**Revise:** maintain a **per-domain override table** — which domains need headless rendering, which need a specific tier, which route straight to (d).

**External scan:** LinkedIn feed image spec · publisher anti-bot posture.

---

## Invariants

- **Ownership:** self. The per-domain override table exists as a file.
- **Objects:** post text · comment draft · raw URL · resolved URL · page HTML · candidate list · selected image URL · downloaded image · resized export · log record.
- **Resources:** network access · optional headless renderer · publisher's server · ~60 seconds.
- **Failure domain:** routes (a), (b), (c) all require reaching the publisher's server. Only (d) is independent.
