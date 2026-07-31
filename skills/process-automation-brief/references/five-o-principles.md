# The Five O Principles — condensed reference

The framework this brief feeds. Read when you need to understand *why* a decision area matters, or when a user asks about the reasoning.

These principles come from quality standards, business process management, control engineering, safety analysis, and research on how people and machines work together. They apply the same whether the work is done by a person, a machine, or an AI.

**A process is work that changes something.** It has a start and an end, takes something in, produces something out, and repeats in a describable way. The definition deliberately says nothing about *who* does the work — that is why a well-described process can move between a clerk, a script, and an AI without redesign.

---

## Before anything: should it exist?

Most failed automation is not badly built. It is built to do the wrong thing faster. Ask what the work is really for — not how it is done today. The answer often deletes half the steps.

---

## 1. Objective — what does success look like, and where are the limits?

Four things, or it is not finished:

- The result, and who it is for
- What is **not** included
- What must never happen, even if breaking that rule is faster
- What may be traded, and down to what floor

Plus: **when is stopping the right answer?** A process with no way to fail cannot stop, so it will keep going when it should not.

**Failure if skipped:** the system runs fast in the wrong direction. A capable operator — a person under pressure, or an AI — will exploit any gap the objective did not close.

## 2. Occurrence — when is it allowed to start?

Four separate conditions, each of which fails differently:

- **Trigger** — the event proposing a run
- **Readiness** — data, resources, preconditions present
- **Permission** — authority to act, checked at run time
- **Window** — when acting is right, and when it is too early or too late

Not acting, acting wrongly, and acting at the wrong moment are three distinct failures. Treating them as one hides two.

**The variety limit:** the trigger must distinguish every situation needing a different response. If reality produces six cases and the trigger sees one, four will be handled badly. This is arithmetic, not bad luck.

## 3. Order — what has to happen before what?

Not a step list — a dependency map. Three kinds:

- One task needs what an earlier task produced
- Two tasks need the same limited thing
- Several tasks each build part of one thing, and the parts must fit

Specify dependencies, not steps. Over-specifying method locks out better approaches and breaks on every small change. Be precise about *what* must happen; rarely about *how*.

**Function allocation is per step, not per system.** For each step ask four separate questions: who collects the information, who interprets it, who decides, who acts? A good design is often fully automatic at collecting and fully human at deciding.

**Failure if skipped:** the process breaks at the joins, not the steps.

## 4. Option — what happens when things go wrong?

Deviation is normal running, not an edge case. Three kinds of answer: **alternative routes**, **exceptions**, **recovery** (safe state, escalation, or stop).

**Stopping must be a real option.** Without it the process does something wrong rather than nothing.

Two rules that sound opposed and are not:

- **Fail loudly.** Never let the system quietly work around a problem. A retry that succeeded, a fallback that produced usable output — say so. Automation hides trouble by working harder, until it cannot, and by then it is expensive. A quiet success is a discarded warning.
- **Hand over slowly.** Step down through levels rather than dropping out. Pass on what was attempted, what happened, and what is needed — not an error code.

**The hard truth:** the better the automation, the worse the people behind it get at the job. They lose practice and they stop paying attention — human vigilance on a quiet system fades after about half an hour. So the most reliable systems need *more* practice built in, not less.

## 5. Observation — how do you see what happened, and how does that change things?

Three duties; most implementations do only the first.

- **Record** — enough to reconstruct a run months later
- **Judge** — against intent and against the objective
- **Change** — a real route by which findings alter the process

Three time frames: what is wrong now; what is slightly wrong every time (needs redesign, not a fix); what is getting worse (the earliest warning, and the least often built).

Then look **outside**: has the world changed in a way that makes the process pointless? A process can run perfectly against reasons that stopped being true.

---

## Two checks across all five

**Ownership.** Every principle needs a name against it — who changes the goal, who authorises a run, who owns each handover, who picks up an escalation and whether they are there at 3am, who reads the evidence and what they may change. The most common real failure is an escalation path ending in an unowned queue. An unowned gap does not stay neutral; blame circulates and nothing gets fixed.

**Objects and resources.** Name what the process acts on and what it consumes. The check that catches the most: **if the fallback needs the same thing that just broke, there is no fallback.** Count independent failure domains, not alternatives. Often the only truly independent option is doing nothing.

---

## Four rules worth carrying

1. **Say what must happen, not how.** Exact about the result, loose about the method.
2. **Where a human decides, say so.** Naming the judgement point is a result, not a failure — it tells you what to build.
3. **Check the measure does not fight the rule.** If you measure clicks but forbid exaggeration, the measure wins over time. Decide which has priority.
4. **Deal with problems where they start.** Catching something a week later in another team fixes nothing at source.

---

## What the framework does not do

It does not tell you whether the process is worth doing — only forces the question. It is not a notation. It does not replace domain expertise where a step is genuinely dangerous. And it does not tell you whether people will accept how the work has been divided.
