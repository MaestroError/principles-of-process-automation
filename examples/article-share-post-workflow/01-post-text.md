# 01 · Post Text — Subprocess Spec

Parent: [`00-main-workflow`](./00-main-workflow.md)

## Contract

| | |
|---|---|
| **Guaranteed by parent** | Snapshot present · article readable, ≥300 words · language supported · URL validated |
| **Consumes** | Article text, title, author, publication · operator angle instruction (optional) · voice/style file |
| **Produces** | Post text (hook + body) · declared angle · claim list with source spans |
| **Escalates (hard)** | Article supports no worthwhile angle · operator's requested angle contradicts the article |
| **Degrades (soft)** | Unverifiable claim → drop the claim, flag it |

---

## Objective

**Convey why this article matters, in the operator's voice, without overstating it.**

- **Measured by:** reviewer edit distance, hook vs. body separately.
- **Constraints:** every claim traceable to a span in the article · no link in the body · hook fits above the "see more" fold · attribute the publication by name · no hashtag padding.
- **Trade-offs:** brevity over completeness. The post is not a summary.
- **Stop:** no supportable angle → escalate.

## Occurrence

- **Trigger:** snapshot available from parent.
- **Readiness:** voice/style file accessible · operator angle instruction read, if supplied.
- **Authorisation:** inherited.

## Order

| Step | Acq | Anal | Dec | Act |
|---|---|---|---|---|
| Extract thesis | 10 | 10 | 10 | 10 |
| Extract 2–3 supporting specifics | 10 | 10 | 10 | 10 |
| Select angle | 10 | 10 | **5** — operator instruction wins if given | — |
| Draft hook | — | 10 | 10 | 10 |
| Draft body | — | 10 | 10 | 10 |
| Verify each claim against source spans | 10 | **7** | 7 | 7 |
| Trim hook to fold | — | 10 | 10 | 10 |

**Flow:** thesis → specifics → angle → hook → body → claim verification → trim.
**Fit:** hook must not be reused by `03`.
**Complete when:** post text produced with a claim list where every claim maps to a source span.

## Option

| Condition | Response |
|---|---|
| Article is thin — few specifics | Short commentary format rather than a summary post |
| Article's thesis is one the operator disagrees with | Draft as critique; flag for review |
| A claim cannot be tied to a source span | Drop the claim, keep the post, flag |
| No angle survives | **Escalate to parent** — do not invent one |

**No safe stop of its own.** This subprocess either produces text or escalates; the parent owns halting.

## Observation

**Record:** angle selected · whether operator instruction was supplied · claims dropped · hook length · edit distance at review, hook and body separately.

| Term | Signal |
|---|---|
| Proportional | Per-run escalations and dropped claims |
| Integral | Edit distance by section over ≥20 runs · conversion by angle type |
| Derivative | Rising edit distance → voice file has drifted from actual voice |

**Revise:** voice/style file and angle library update from the edit diffs.

## Invariants

- **Ownership:** operator owns the voice/style file. It is a file.
- **Objects:** snapshot · thesis · specifics · angle · hook · body · claim list.
- **Resources:** language model · voice file · article text.
