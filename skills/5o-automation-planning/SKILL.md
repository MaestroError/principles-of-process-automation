---
name: 5o-automation-planning
description: Turns an automation brief into a buildable specification organised by the Five O principles — Objective, Occurrence, Order, Option, Observation — plus ownership and resources. Use this whenever someone has a brief, a scoped idea, or a set of requirements for an automation and wants it turned into something a builder can work from. Trigger on "turn this brief into a spec", "plan this automation", "we know what we want, now design it", "write the spec for this workflow", or when a user shares an automation brief and asks what to do next. Also use when someone has a rough plan and wants it checked for gaps before building. This is the step after the brief and before any code — it specifies what must be true, not which tools to use.
---

# Automation Planning

Your job is to turn a brief into a **specification a builder can work from without guessing** — and without you making decisions that were not yours to make.

The brief captured intent and decisions. The spec turns those into structure: what must be true before what, where a human decides, what happens when it breaks, what gets recorded. It is organised by the Five O principles because those five dimensions are jointly what a process needs before it can be safely handed to any operator — a person, a script, or an AI.

Two things this is not. It is not a build plan: no tools, no platforms, no architecture. And it is not a longer brief: if you are restating intent rather than specifying structure, you have not started yet.

## Before you specify: check the brief

Read the brief and establish three things.

**1. Are there blocking open questions?** Briefs carry `OPEN:` items, some marked blocking. A blocking gap is one where the answer changes the design rather than filling a slot — who owns escalation, whether stopping is allowed, which of two conflicting rules wins.

Resolve those **before** specifying. Use `AskUserQuestion`, at most three questions per round, with concrete options drawn from the brief. Specifying around a blocking gap produces a spec that looks complete and is wrong in a way nobody notices until build.

Non-blocking OPENs carry into the spec as named gaps. Do not silently resolve them.

**2. Is this actually one process?** The brief should already be scoped to one. Check anyway — briefs get written optimistically. The signals are the same: more than one trigger starting genuinely different work, more than one owner of the core outcome, more than one definition of "finished", or failure modes with nothing in common.

If it is genuinely one process, write one spec. **That is the normal case and you should prefer it.**

If it is not, produce a parent spec plus a child spec per subprocess — see `references/composition.md` for how contracts between them work. Do not reach for this because the process feels big. Reach for it when the signals above are actually present.

**3. What is missing that the brief did not think to include?** The brief captures what the user knew to tell you. The spec is where the structural gaps get caught — see the checks below.

## Writing the spec

Use `assets/spec-template.md`. Work through the five dimensions in order, because each constrains the next.

### Objective — what counts as success, and what are the limits

Carry the brief's purpose, boundary, and trade-offs into a form that can be checked. The result must be stated so someone could verify it happened. The hard rules must be stated as prohibitions, not preferences. The trade-offs need floors — "speed may drop to 24 hours" not "speed is less important".

Include the **stop criteria**. A process with no defined way to conclude "not this time" will do something wrong rather than nothing.

### Occurrence — under what conditions it may act

Specify four separate things, because they fail differently and a design that merges them hides two:

- **Trigger** — the event proposing a run
- **Readiness** — what must be present and true before acting is safe
- **Authorisation** — under whose authority, and whether that is checked at run time
- **Window** — when acting is correct, and when it would be too early or too late

Then apply the **variety check**: list the situations the real world produces that need different handling, and confirm the trigger logic can tell them apart. If reality has six cases and the trigger sees "something arrived", four get handled wrong. Where the trigger cannot distinguish them, that is a classification step, not an error handler — put it in Order.

### Order — what must be true before what

Specify the **dependency structure, not a step list.** Three kinds of dependency, and each needs a different answer:

| Dependency | Specify |
|---|---|
| One task needs what an earlier task produced | That downstream work waits until the output exists, is available, and is usable |
| Two tasks need the same limited resource | Scheduling, priority, or contention handling |
| Several tasks each build part of one output | The rule that makes the parts fit |

Also specify what may run **concurrently** — over-serialising is the most common avoidable cost — and what "finished" means as a condition someone can check.

Then the **automation level grid**. This is the part most plans get wrong by treating automation as one setting. For each step, decide separately: who *collects* the information, who *interprets* it, who *decides*, who *acts*. A well-designed process is routinely fully automatic at collecting and fully human at deciding. Naming the human decision point is a result, not a failure — it tells the builder exactly what to build around.

**Keep this loose about method.** Be precise about what must be true; rarely about how. Over-specifying method closes off better implementations and makes the whole thing break on small changes. If you are describing clicks, you have gone too far.

### Option — what happens when reality does not cooperate

Deviation is normal running. Specify three classes:

- **Variants** — other routes to the same result, in priority order
- **Exceptions** — named conditions that break the assumptions, each with a response
- **Recovery** — return to a safe state, escalate, or stop

Then apply three checks that catch what plans usually miss:

**The independent-failure check.** For every fallback, ask what it depends on. A fallback that needs the thing that just broke is not a fallback. Count independent failure domains, not alternatives. Very often the only genuinely independent option is doing nothing — which is a reason to specify that option properly, not a reason to be embarrassed by it.

**Fail obviously.** Specify that every degradation is *recorded and surfaced* — retries that succeeded, fallbacks that produced usable output, routes that were switched. A quiet success looks identical to a clean run, and automation hides trouble by working harder until it cannot. This is the difference between noticing a supplier degrading over three weeks and discovering it on the day it stops.

**Hand over gradually.** When the system reaches its limit it should step down through levels, not drop out. Specify what the receiving human is given: what was attempted, what state obtains, what specifically is needed. Not an error code. Someone who has not done this by hand in months is about to do the hardest version of it under time pressure.

Where the process is high-consequence and rarely fails, specify deliberate manual practice. It feels wasteful and it is insurance.

### Observation — what it emits, and how that changes it

Three obligations, and most specs stop after the first:

- **Record** — enough to reconstruct a single run months later, including degradations
- **Judge** — compare actual behaviour against intended behaviour and against the objective
- **Revise** — the actual route by which a finding changes the specification, and who is allowed to make that change

Specify metrics across three horizons, because a spec with only the first is blind in two directions:

- **Now** — what is wrong in this run
- **Accumulated** — what is slightly wrong every time. No single case justifies a fix; across a thousand runs it costs more than any incident. This calls for redesign, not intervention.
- **Trending** — what is getting worse before anything has broken. The earliest available warning, and the one least often built.

Add an **external check**: what would tell you the process should no longer exist? Processes run perfectly for years against reasons that stopped being true.

### Ownership and resources — across all five

Not a section at the end. Every dimension above needs a name against it and a resource list.

**Ownership.** Who may change the objective. Who authorises a run. Who owns each handover in the order. Who receives each escalation — and whether they are available when it happens. Who reads the observation output and what they are permitted to change. An escalation path ending in an unowned queue is the most common real-world failure, and an unowned gap does not stay neutral: blame circulates and nothing gets fixed.

**Resources.** What the process acts on and what it consumes. This is what makes it schedulable and what makes the contention in Order real.

**Support congruence.** Check that the measures do not fight the rules. If the spec measures throughput but forbids skipping a check, the measure will win over time. Name the conflict and state which has priority.

## Say each thing once, at the level that owns it

A rule stated in five places has five chances to drift and one of them will. When you find yourself writing the same constraint twice — in a parent and a child, in Objective and again in Order, in a contract and again in an automation grid — **state it once where it is enforced, and reference it everywhere else.**

The rule belongs at the level that can enforce it. A prohibition the parent checks belongs in the parent; children reference it. A rule only one subprocess can enforce belongs in that subprocess, and the parent references it. This is the same reasoning as the shared gate: a condition validated once cannot disagree with itself.

**Keep the spec proportionate to the process.** A workflow handling twelve cases a month does not need the specification density of one handling twelve thousand. Length should track how much of the process genuinely needs to be pinned down, not how thorough you are willing to look. If a section is long because the process is genuinely intricate, good. If it is long because you restated context, cut it — you are spending the reader's attention on something they already knew, and attention is the scarcest resource a spec has.

The test: could a builder act on this without reading it twice? If not, the problem is usually repetition, not missing detail.

## Before you deliver

Run these checks. Each one catches a defect that is cheap now and expensive later:

1. Every fallback has an independent failure domain, or is marked as sharing one.
2. Every escalation ends at a named role, with availability stated.
3. Stopping is available as a designed outcome.
4. Every step has all four automation levels assigned.
5. Every degradation path is recorded, not just every failure.
6. No blocking OPEN was silently resolved.
7. No tool, vendor, or platform is named.
8. Observation covers now, accumulated, and trending — not just now.
9. No rule is stated in more than one place. Each appears once, where it is enforced.
10. The spec is proportionate — nothing is long because you restated context.

Close with **open items** (what remains undecided and who decides) and **risks** (what you would watch during build). Keep both short and specific.

## Reference

- `assets/spec-template.md` — the single-process spec structure. Use this by default.
- `references/composition.md` — parent and subprocess specs, and the contracts between them. Read only when the brief genuinely contains more than one process.
- `references/five-o-principles.md` — the underlying framework. Read when you need to understand why a dimension matters, or when the user asks.
