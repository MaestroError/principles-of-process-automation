# Article-Share Post Workflow

A composed automation, specified with the Five O principles **at every level**.

This folder exists to test one claim from `PRINCIPLES.md`: that the framework is fractal — that the same five dimensions apply to a whole workflow and to each of its subprocesses, without modification.

---

## Files

| File | What it specifies |
|---|---|
| [`00-main-workflow.md`](./00-main-workflow.md) | **Parent.** URL in → published post out. Owns the shared gate, dispatch, aggregation, and the safe stop |
| [`01-post-text.md`](./01-post-text.md) | Reads the article, produces post text with a verified claim list |
| [`02-image.md`](./02-image.md) | Produces an image — harvested from the publisher, or designed from the title when none exists |
| [`03-cta-comment.md`](./03-cta-comment.md) | Produces the first comment carrying the tracked link |
| [`04-assembly-review.md`](./04-assembly-review.md) | Assembles one draft, runs fit checks, takes the operator's decision, publishes |

Each of the five is a complete Five O specification. None is a fragment.

---

## The shape

```
                      ┌─────────────────────────────────┐
   article URL ──────▶│  SHARED GATE  (parent Occurrence)│──✗──▶ exit, human review
                      └─────────────────────────────────┘
                                     │ validated snapshot
                    ┌────────────────┼────────────────┐
                    ▼                ▼                │
              01 post-text     02 image (harvest)     │
                    │                │                │
                    ├───────▶ 02 image (design) ◀─────┘
                    │                │
                    ▼                │
              03 cta-comment ────────┤
                                     ▼
                            04 assembly + review
                                     │
                              ┌──────┴──────┐
                           approve        reject
                              │              │
                     publish → comment    save draft
```

---

## What composition required

Applying Five O recursively was not automatic. Six rules had to be established for the levels to fit together, and they are the actual finding of this example.

### 1. The parent's Occurrence is the shared gate

Any precondition needed by two or more subprocesses is validated **once, at the parent, before dispatch.** If the URL doesn't resolve, isn't an article, or sits behind a paywall, the run exits at the gate and no subprocess starts.

The alternative — each subprocess defending itself — means the same check written three times, three different failure behaviours for the same condition, and a URL failure surfacing as an "image error." **A subprocess should not carry logic for a condition the parent already guaranteed.**

### 2. Contracts make the composition explicit

Every subprocess opens with four statements: what it may **assume**, what it **consumes**, what it **produces**, and what it **escalates**. Without these, "Five O all the way down" produces five well-specified processes that don't actually connect.

The contract is where the parent's guarantees and the subprocess's assumptions are made to match. It is the interface.

### 3. Every failure is classified hard or soft

- **Hard** — halts the run and returns to the human. *No supportable angle exists.*
- **Soft** — the run continues, carrying a flag to review. *No image was found.*

This is the single most useful rule discovered here. Without it, every subprocess has to decide unilaterally whether its own failure is fatal, and it will get that wrong in both directions — halting the workflow over a missing image, or shipping a post whose central claim couldn't be verified.

Classification belongs to the parent, because only the parent knows what the output is for.

### 4. The parent's review absorbs the subprocesses' human checkpoints

The general image spec in [`../linkedin-post-image.md`](../linkedin-post-image.md) has a level-1 human decision at its centre. Here, `02` has none — because `04` already puts the assembled draft in front of the operator.

**A subprocess needs its own human checkpoint only if the parent has none, or if the decision cannot wait for assembly.** Duplicating it asks the operator to approve the same image twice, which trains them to stop looking.

### 5. Objectives nest, but are stated in what the subprocess controls

The parent's objective is an approved published post. `02`'s objective is not "a good post" — it is *an image that matches the article and doesn't misrepresent its source.* A subprocess objective phrased in the parent's terms cannot be measured, and a subprocess cannot be held to an outcome it does not control.

### 6. Observation aggregates upward, and the aggregate is the useful part

Each subprocess observes itself. The parent observes something none of them can: **operator edit distance at review, attributed to the originating subprocess.**

That single metric routes all improvement effort — whichever subprocess the operator corrects most is where the next work goes. It is attributable, immediate, and requires no inference about engagement. It only exists because there is a parent with a review step; no subprocess could compute it alone.

---

## Two design findings from this composition

**Adding a route added a failure domain — and that is why it matters.** The image subprocess harvests from the publisher's server, or designs a card from an illustration source. These fail *independently*. In the standalone spec ([`../linkedin-article-share-image.md`](../linkedin-article-share-image.md)) all image routes shared one dependency, so having four of them bought nothing. Route count is not resilience; independent failure domains are.

**The worst state in the workflow is not failure.** It is publishing successfully and then failing to post the comment — a live post with no link, which is worse than not publishing at all. That state is only visible once the ordering constraint (*publish must precede comment*) is written down, and it earns a dedicated response in both `00` and `04`.

---

## Reading order

Start with `00-main-workflow.md` for the shape and the gate. Then read any subprocess — each is self-contained once you have read its contract. `04` is worth reading second if you want to see where every path terminates.

*Related: [`../../cases/case-01-specification-as-interrogation.md`](../../cases/case-01-specification-as-interrogation.md) · [`../../cases/case-02-narrowing-the-objective.md`](../../cases/case-02-narrowing-the-objective.md)*
