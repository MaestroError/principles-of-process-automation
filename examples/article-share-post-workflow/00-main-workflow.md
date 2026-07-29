# Article-Share Post Workflow — Automation Spec (Parent)

Context: solo operator · shares an article as a LinkedIn post · reviews one assembled draft before publish.

**In:** article URL · optional angle instruction.
**Out:** published post + first comment, or a saved draft with reasons.

**Subprocesses:** [`01-post-text`](./01-post-text.md) · [`02-image`](./02-image.md) · [`03-cta-comment`](./03-cta-comment.md) · [`04-assembly-review`](./04-assembly-review.md)

---

## Objective

**Turn an article URL into an approved, published post — with the operator reviewing one complete draft rather than four fragments.**

- **Measured by:** operator edit distance at review (low = the automation is working) · tracked conversions per post.
- **Scope:** single-article share posts. Out: original content, multi-article roundups, non-article destinations.
- **Constraints:** nothing publishes without explicit human approval · no claim the article does not support · link always in the first comment, never in the post body · one run per article.
- **Trade-offs:** ≤10 minutes total operator time. Post-text quality over run speed.
- **Stop criteria:** article unreadable or unsuitable → exit, publish nothing. Reviewer rejects → save draft, stop.

---

## Occurrence

- **Trigger:** operator submits an article URL.
- **Authorisation:** operator initiates; nothing publishes without approval.
- **Window:** the run should complete in one session — a draft assembled against a page fetched days earlier may no longer match it.

### Shared gate — validated once, here

Every condition below is a precondition of two or more subprocesses. It is checked at the parent so no subprocess has to.

| Gate | Failure response |
|---|---|
| URL resolves; final domain after redirects is the expected one | **Exit — human review** |
| Destination is an article, not a tool, PDF, video, or feed | **Exit — human review** |
| Page is not paywalled, login-walled, or consent-gated | **Exit — human review** |
| Article body extractable, ≥300 words — render headless first if the raw HTML is empty | **Exit — human review** |
| Article language is supported | **Exit — human review** |
| URL not already posted (dedupe against run log) | **Exit — human review** |

**A gate failure halts the run before any subprocess starts.** Subprocesses never receive an unvalidated URL and carry no logic for these conditions.

---

## Order

**Flow:**

```
submit URL
  → fetch + validate once  → snapshot {html, extracted text, metadata, title, publication}
  → 01 post-text  ─┬─────────────→ 03 cta-comment ─┐
  → 02 image (harvest route) ─────────────────────┤
       └ 02 image (design route, needs angle) ─────┤
                                                   → 04 assembly-review
                                                     → approve → publish → post comment
```

- **Fetch once.** Both `01` and `02` depend on the page. Fetching twice is a sharing-dependency failure and doubles the load on the publisher.
- **`01` ∥ `02`-harvest** run in parallel — both depend only on the snapshot.
- **`03` waits on `01`** — the CTA must complement the hook, not repeat it (fit dependency).
- **`02`-design waits on `01`** — illustration concept depends on the declared angle. The harvest route does not.
- **`04` waits on all.**
- **Publish precedes comment.** The comment cannot exist before the post does.

**Sharing:** the snapshot (single fetch) · operator attention at review · tracking-service quota.

**Fit:** post text, image, and comment link must all refer to the same article.

**Complete when:** post published with its first comment, *or* draft saved with reasons recorded.

### Function allocation

| Step | Acq | Anal | Dec | Act |
|---|---|---|---|---|
| Fetch and validate | 10 | 10 | 10 | 10 |
| Dispatch subprocesses | 10 | 10 | 10 | 10 |
| Aggregate outputs and flags | 10 | 10 | 10 | 10 |
| **Approve / reject / edit** | 10 | 7 | **1** | — |
| Publish, then post comment | — | 10 | 10 | 7 |

---

## Option

The parent owns every failure that is not local to a single subprocess.

**Hard escalation — halts the run:**

| Condition | Response |
|---|---|
| Any shared gate fails | Exit before dispatch. Report which gate, and why |
| `01` escalates — no supportable angle | Halt. Present the article and the reason; ask the operator for an angle or a decision to skip |
| `01` escalates — operator's requested angle contradicts the article | Halt. Present the contradiction; the operator revises the instruction or overrides |
| `04` fit check fails after operator edits | Return to review with the failing check named |

**Soft degradation — run continues, flag raised at review:**

| Condition | Response |
|---|---|
| `02` returns no image | Assemble text-only. Flag |
| `02` used the design route | Assemble. Flag — designed images warrant a closer look |
| `03` could not generate a tracked link | Use the raw URL. Flag — this post is unmeasured |
| `01` dropped an unverifiable claim | Assemble. Flag which claim and why |

**Recovery / safe stop:** publish nothing. A saved draft with its flags is always available and requires no external service.

**Critical ordering hazard:** if publish succeeds but the comment fails, the post is live with no link. Retry immediately; on second failure alert the operator at once. This is the only state in the workflow that is worse than failing outright.

**Disengage:** the operator can abort at review; rejecting is a first-class outcome, not an error.

---

## Observation

**Record per run:** URL · gate outcome · route taken by `02` · all flags raised · **operator edit diff at review, attributed to the originating subprocess** · approve/reject + reason · elapsed time · tracked link ID.

**Judge:**

| Term | Signal |
|---|---|
| Proportional | Per-run gate failures and escalations |
| Integral | **Edit distance by subprocess over ≥20 runs** — identifies which subprocess to invest in · tier-1 image rate by domain · conversion by angle |
| Derivative | Trend in edit distance; trend in gate-failure rate (publishers tightening access) |

**Revise:** subprocess instructions and libraries update from edit patterns — the parent routes improvement effort to whichever subprocess the operator corrects most.

> Operator edits at review are the highest-value signal in the workflow: attributable, immediate, and per-subprocess. Unlike engagement, they require no inference.

**External scan:** LinkedIn feed image spec and link-in-body penalty · publisher anti-bot posture · tracking service availability.

---

## Invariants

- **Ownership:** operator owns approval and the voice/style file. Every subprocess's instruction set and library exists as a file, not as memory.
- **Objects:** article URL · snapshot · post text · declared angle · claim list · image + provenance · tracked link · comment text · assembled draft · flag set · run log.
- **Resources:** network · publisher's server · illustration source · tracking service · operator attention · ~10 min.
- **Failure domains:** publisher server (gate, `01`, `02`-harvest) · illustration source (`02`-design) · tracking service (`03`) · LinkedIn (publish, comment). Four independent domains; only "save draft, publish nothing" depends on none of them.
