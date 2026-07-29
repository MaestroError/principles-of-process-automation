# Case 01 — Specification as Interrogation

**Event.** Applying the Five O principles to a small, familiar process (creating an image to attach to a LinkedIn post) in order to test the framework.
**Duration.** One working session.
**Outcome.** The specification exercise changed the design of the automation three times before any of it was built.

---

## What happened

The intent was to test the framework by specifying a process the operator already performs by hand and knows well. The expectation was that the framework would *document* the process. What it actually did was **interrogate** it.

At three separate points, writing the specification produced a question the existing design could not answer. Each question forced a design change, and one of them changed the objective itself. None of these were errors in the process being specified — they were things the operator knew but had never had to make explicit, and which turned out to be wrong once explicit.

The finding this case records is that **the framework's primary output is not the specification. It is the set of questions the specification cannot be completed without answering.** A dimension you cannot fill in is not a gap in the document; it is a defect in the process, surfaced.

---

## The initial automation

What would have been built without the framework — the intuitive design, stated honestly:

> **When I finish a LinkedIn post, generate an image with an AI image model and attach it.**
>
> - **Objective** — have an image on every post.
> - **Occurrence** — when I'm working on a post.
> - **Order** — post text → write prompt → generate → attach.
> - **Option** — if it looks bad, re-roll the prompt.
> - **Observation** — check the likes.

This is a complete, buildable automation. It is also wrong in four ways that are invisible until you try to write the five dimensions down.

---

## The three questions

### Question 1 — *What evidence would tell you this is working?* (Observation)

The specification demanded a feedback loop. The honest answer was that there wasn't one: LinkedIn engagement is dominated by posting time, topic, network activity, and algorithmic variance, and attributing any of it to the image is close to impossible at solo posting volume. The first draft of the spec recorded this as a limitation of the domain.

**It was not a limitation of the domain. It was a missing design element.**

The resolution: **put a trackable newsletter subscription link in the first comment of every post.** Subscriptions are attributable, discrete, and directly meaningful — unlike likes, which measure whether someone was mildly entertained while scrolling.

This closes the loop properly. Over time, posts can be compared on a real conversion outcome, correlated with their text *and* their image treatment, and the common ground behind the high performers extracted and fed into subsequent posts.

Two things about this are worth recording.

First, the change slotted into a dependency the specification had **already identified**. The Order section listed a *fit* dependency requiring that "the image, the post's opening hook, and any link or first comment must compose." The mechanism that fixes Observation was already named as an object in Order — the specification had mapped the surface before anyone knew what it was for.

Second, and more significantly: **fixing Observation improved Objective.** The original intended value was "increase stop-scroll rate and dwell time" — real, but unmeasurable. With a tracked conversion available, the objective can be restated as something the process can actually be held to. This is precisely the behaviour the framework claims for itself — that Observation closes back onto Objective rather than terminating in a dashboard — and it occurred here without being sought.

### Question 2 — *Who decides, at what level of autonomy?* (Order)

Filling in the function-allocation matrix produced a step that could not be assigned above level 1: selecting the final image. The aesthetic and credibility judgement involved is not specifiable in advance, and no amount of prompt engineering moves it.

The first instinct was to record this as a place the framework strained.

**On reflection, it is the framework working.** Marking the boundary of human judgement is one of its jobs. A framework whose only success condition is full automation would either lie about this step or omit it; one that exposes it produces a better design, because the correct architecture follows immediately — *build the system that produces a strong shortlist, never the one that picks.* Everything around the level-1 step gets automated to 7–10, and the human is placed exactly where they add value rather than everywhere or nowhere.

**Revised understanding:** specifying where human judgement remains necessary is a first-class output of the framework, not a residue left over after automation. Exposing a weakness and enforcing an efficiency are the same act.

### Question 3 — *Why is the specification longer than the process?*

The finished spec takes longer to read than the automation takes to run, which initially looked like evidence that the framework is disproportionate for small processes.

**The diagnosis was wrong.** The length was caused by an under-bounded **Objective**. The process as scoped covered *any* image type — real artifact, diagram, typographic, generative, or none — for *any* post type. That is a genuinely general automation, and a general automation legitimately requires a robust specification.

The framework did not inflate the spec. The unbounded objective did, and the spec length is an accurate signal of scope rather than overhead. Narrow the Objective to one post archetype and one production route and the specification collapses to a page.

This is itself a useful property: **specification length is a diagnostic.** If a spec feels disproportionate to the process, the first thing to check is whether the Objective is doing too much.

> **Corrected by later test — see `examples/linkedin-article-share-image.md` §7.** This claim was tested directly by specifying a deliberately narrow version of the same process. It did *not* collapse: 2,325 words against 2,994. What narrowing actually changed was **density** — prose about judgement became decision tables. The corrected claim: objective scope determines *what proportion of a specification can be written as rules rather than as guidance*, and that ratio, not word count, predicts automatability. The original claim is left standing above because the correction is the more useful finding.

---

## The final automation

> **When a post's text is final, decide whether an image serves it — and if so, produce a shortlist for me to choose from, using the most credible available route.**
>
> - **Objective** — a visual that earns attention without costing credibility with a technical audience. Shipping *no image* is a valid successful outcome. Measured against tracked newsletter subscriptions, not likes. Hard constraints: no fabricated data, no garbled text, legible at mobile thumbnail size. Timebox: 15 minutes.
> - **Occurrence** — fires on *final text*, not on "started drafting." Requires one identifiable core claim, and classifies the post's archetype (framework / result / artifact / opinion / reflection) — because different archetypes require structurally different visuals, and a single undifferentiated trigger cannot supply that variety.
> - **Order** — claim → archetype → route → three candidates generated in parallel → automatic screening → **human selection (level 1)** → export → attach, with the tracked subscription link in the first comment as a required composing artifact.
> - **Option** — real artifacts and screenshots first, generation last. Garbled text switches route rather than re-rolling. Text-only publication is the always-available safe stop, and the only fallback with no external dependency.
> - **Observation** — tracked subscriptions per post as the attributable outcome; candidate rejection rate as a leading indicator that needs no attribution; periodic comparison across archetype and route; findings written back into the prompt library and the archetype→route mapping, both of which exist as files rather than in the operator's head.

Four substantive differences from the initial version — an inverted objective, a classifying trigger, an inverted route priority, and a closed measurement loop — **all produced before implementation, by the act of writing the specification.**

---

## What this case establishes

1. **The framework earns its keep in questions, not documentation.** Every design change here originated in a dimension that could not be completed, not in a review of a finished spec. The value arrives during writing.

2. **An unanswerable dimension is a finding.** "There is no feedback loop here" is not a limitation to be recorded and accepted. It is a defect with a design response — in this case, a single trackable link.

3. **Marking human judgement is an output, not a failure.** The framework's job includes saying where automation stops. Doing so produced the correct architecture rather than an incomplete one.

4. **Specification length diagnoses objective scope.** A spec disproportionate to its process indicates an Objective covering too much, not a framework imposing too much.

5. **The loop closes as claimed.** Observation fed back into Objective unprompted — the measurement constraint improved the goal definition. This is the framework's central structural claim, and it held under its first test.

---

*Related: [`examples/linkedin-post-image.md`](../examples/linkedin-post-image.md) — the full specification produced during this session.*
