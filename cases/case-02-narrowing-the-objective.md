# Case 02 — Narrowing the Objective

**Event.** Specifying a deliberately narrow process (attach a shared article's own featured image to the post) immediately after specifying a broad one (produce any image type for any post type), to test a prediction from Case 01.
**Prediction tested.** That narrowing the Objective would collapse the specification.
**Result.** The prediction partly failed. The failure is the useful part.

---

## The prediction

Case 01 concluded that the general image spec was long because its Objective was unbounded — covering any image type for any post type — and proposed a diagnostic: *specification length tracks the scope of the Objective, not the importance of the process.* It asserted that narrowing the objective would collapse the spec "to a page."

## The measurement

| Spec | Words |
|---|---|
| General — any image type, any post type | 2,994 |
| Narrow — one route, one post archetype | 2,325 |

Shorter, but nowhere near a collapse.

## What actually changed

**Density, not length.**

The general spec spends its words on **prose about judgement** — what "credible to a technical audience" means, when an image dilutes a claim, how to weigh novelty against legibility. The narrow spec spends roughly the same volume on **decision tables**: a six-way page classification, a five-tier candidate precedence with confidence levels, a seven-row exception matrix, explicit validation gates.

Same length. One *describes* a process; the other very nearly *is* one.

**Corrected diagnostic:**

> Objective scope determines what proportion of a specification can be written as **rules** rather than as **guidance**. That ratio — not word count — predicts automatability.

Word count was a proxy that happened to work once and then didn't. The underlying variable is determinacy.

This also explains the allocation matrices. The general spec has a level-1 human decision at its centre; the narrow spec is almost entirely level 10, with two level-5 flags and one level-1 glance retained deliberately. The difference is not engineering quality — it is that bounded objectives make selection criteria **discoverable in the input** rather than resident in someone's taste.

---

## Two further findings

### The dominant hazard changed with the scope

Same framework, same five dimensions, entirely different failure to defend against.

- **General spec:** the risk is producing something mediocre — a credibility cost accumulated slowly.
- **Narrow spec:** the risk is **timing**. Attaching an image after publication means editing a live post, which degrades its distribution. The window closes at publish and does not reopen.

Only specifying Occurrence as *trigger + readiness + authorisation + window* surfaced this. A design treating Occurrence as "when does it start" would have walked into it, because the failure is not *not acting* — it is acting too late, which STPA treats as a separate class for exactly this reason.

**Implication:** hazard class is a property of the scoped process, not of the process family. Re-run Occurrence when you narrow.

### The failure-domain finding recurred

| Spec | Apparent fallbacks | Independent failure domains |
|---|---|---|
| General | 5 routes | 2 — real artifact, no image |
| Narrow | 4 routes | 1 — no image |

Both specs presented a comfortable-looking set of alternatives, and in both cases most of them died together: the general spec's generative and typographic routes may share one API; the narrow spec's three image-producing routes all require reaching the publisher's server.

Appearing independently in two unrelated processes suggests this is not a quirk of either. **Fallback count is not resilience; independent failure domains are.** Worth asking of any Option set: *how many of these fail together?*

Note also that in both cases the only genuinely independent option was **doing nothing** — which is an argument for treating the safe stop as a designed route with real value, rather than as the absence of a result.

---

## Carried forward

1. Replace Case 01's length diagnostic with the **rules-to-guidance ratio**.
2. **Re-run Occurrence when narrowing scope** — the dominant hazard class does not survive the change.
3. Add *"how many of these fail together?"* as a standing question in the Option dimension.
4. Treat the **safe stop as a designed route**, since it is repeatedly the only one with no shared dependency.

*Related: [`examples/linkedin-post-image.md`](../examples/linkedin-post-image.md) · [`examples/linkedin-article-share-image.md`](../examples/linkedin-article-share-image.md)*
