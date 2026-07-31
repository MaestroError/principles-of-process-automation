---
name: process-automation-brief
description: Turns a rough automation idea into a decision-complete brief through a short structured interview. Use this whenever someone describes something they want to automate — a workflow, a repetitive task, an approval chain, a content pipeline, a data handoff, an AI agent — and has not yet nailed down the decisions a builder would need. Trigger on phrases like "I want to automate...", "can we build something that...", "I keep doing X manually", "we should have a bot that...", or when someone asks for help scoping, specifying, or planning an automation. Also use when a user has a vague automation idea and asks what questions they should be answering. This produces the brief that feeds automation planning — it does not produce the technical spec itself.
---

# Process Automation Brief

Your job is to turn a rough idea into a **decision-complete brief**: a short document that captures every decision a builder would otherwise have to guess at.

You do this by interviewing, not by interrogating. Most people arrive with a clear picture of the happy path and no picture at all of the edges — what must never happen, who gets woken up when it breaks, what "done" means, when *not* doing the work is the right answer. Those edges are where automations fail, and they are what this brief exists to capture.

The brief you produce is **not** a technical specification. It records intent and decisions. A separate planning step turns it into a spec. Keeping that boundary clean is what makes this useful — if you find yourself designing the implementation, you have gone too far.

## What a complete brief needs

These are the decision areas. You are not asking about all of them — you are checking which ones the user has already settled, and asking only about the gaps.

| Area | What must end up decided |
|---|---|
| **Purpose** | What result is actually wanted, for whom, and why it matters. Not the current steps — the outcome. |
| **Boundary** | What is explicitly out of scope. What must never happen even if it would be faster. |
| **Trade-offs** | What may be sacrificed — speed, cost, quality, coverage — and down to what floor. |
| **Trigger and readiness** | What starts it. What must already be true, present, and permitted before acting is safe. Whether there is a time when acting would be wrong. |
| **Dependencies** | What genuinely depends on what. What is contended — the same person, budget, API, or machine needed by two things at once. What "finished" means. |
| **Human role** | Which decisions stay with a person, and why. Who reviews, approves, or gets escalated to. |
| **Failure and stopping** | What happens when the main path is blocked. What the safe stop is. Whether stopping is even allowed. |
| **Evidence** | How anyone would know it worked. What gets recorded. Who looks, and what they can change. |
| **Ownership** | Who owns the outcome. Who is allowed to change the rules. Who is actually available when it escalates. |

A brief that leaves **Failure and stopping**, **Human role**, or **Ownership** blank is not finished. Those three are the ones people never volunteer and always need.

## How to run the interview

### Step 1 — Read the idea properly first

Before asking anything, work out what the user has already told you. People often specify more than they realise. Extract it, and only ask about what is genuinely missing or ambiguous.

Asking someone a question they already answered is the fastest way to lose them.

### Step 2 — Challenge the premise, once

The most expensive automation failure is building something that works perfectly and should not exist. If the idea looks like it is automating around a broken process rather than fixing it — a workaround for a bad handoff, a report nobody reads, a manual step that exists because of an old constraint — say so **once**, briefly, with a concrete alternative.

Then respect the answer and move on. You raise it, they decide, you build the brief they asked for. Pressing twice makes you an obstacle rather than a help.

Skip this entirely when the purpose is obviously sound. Most ideas are fine.

### Step 3 — Interview in rounds of at most three questions

Use the `AskUserQuestion` tool. Ask **no more than three questions per round.** More than three at once and answer quality drops sharply. A follow-up is a new round, not a fourth question — if you want to dig into an answer, ask it in the next round.

Each question needs 2–4 concrete options drawn from the user's actual situation, not generic ones. If you think one option is right, put it first and mark it "(Recommended)". People are far better at choosing between real alternatives than at answering open questions, and the options themselves teach them what the decision even is.

**There is no round limit.** Someone may arrive with nothing more than a wish, and turning a wish into something buildable can take many rounds. Stopping early to hit a count produces a brief full of invented decisions, which is worse than a longer conversation.

What keeps a long interview from wandering is not a budget — it is **focus**. Every question you ask should be earning one of these three things:

1. **What work has to be done.** The actual steps and decisions, what depends on what, what "finished" means.
2. **What resources it needs.** Data, systems, access, money, time, and — most often forgotten — whose attention.
3. **Who is responsible for each job.** Not "the team". A role or a name, for every piece of work and every failure path.

If a question is not pinning down work, resources, or responsibility, do not ask it. That is the test. Interesting context that changes nothing is the main way these interviews get long without getting better.

A useful order, collapsed wherever the user has already answered:

1. **Purpose and boundary** — what it is for, what is out of scope, what must never happen
2. **The work** — what actually happens, what depends on what, what "done" means
3. **Resources and human role** — what it needs, what is contended, which decisions stay with a person
4. **Failure and stopping** — what happens when it breaks, what the safe stop is
5. **Responsibility and evidence** — who owns each part, who is on the other end of an escalation, how anyone knows it worked

Stop when work, resources, and responsibility are pinned down well enough that a builder would not have to guess.

### Step 3b — Watch the scope while you interview

A brief that will not fit in 1000 words is not a long brief. **It is more than one automation.**

Watch for these while interviewing. Any two together mean the scope has outgrown a single process:

- More than one trigger that starts genuinely different work
- More than one owner for the core outcome
- More than one definition of "finished"
- Distinct groups of output that no single person consumes
- A step whose failure has nothing to do with the other steps' failures

When you see it, say so and propose a split. Name the subprocesses in plain terms, then **recommend which one to automate first**. Good first candidates are high-volume, well-understood, and have a clean handoff at the edge — the boring one is usually right. Something that unblocks the others is also a good pick.

Then write the brief **for that one subprocess**, and list the others as named, deliberately out of scope. A small automation that ships beats a complete brief that never gets built, and the split is easier to see now than after someone has spent three months on it.

### Step 4 — Watch for the failures people do not see coming

While interviewing, look for these. They are the ones worth spending a question on, because users almost never raise them:

- **No stop condition.** The process has no way to conclude "not this time". It will do something wrong rather than nothing.
- **A fallback that shares a failure with the primary.** The backup plan needs the same API, service, or person that just broke.
- **An escalation into nobody.** The failure path ends at a queue, an inbox, or a role with no name against it.
- **A measure that fights a rule.** They want to maximise something the constraints forbid — clicks versus accuracy, speed versus review.
- **A trigger too coarse for the cases.** Reality produces six situations; the trigger sees one.
- **Silent degradation.** Retries and fallbacks are planned, but nothing records that they happened.

You do not need to ask about all of these. Ask about the ones that plausibly apply, and put the rest in the recommendations.

### Step 5 — Write the brief

Use `assets/brief-template.md`. Save it as a markdown file where the user can get at it.

**Hard ceiling: 1000 words of prose.** Not a target to aim near — a limit. Count before you deliver, and count the same way every time: **body text only, excluding markdown table pipes, headings markup, and any word-count note you add.** Otherwise "1000 words" means whatever the counting method happened to be that day.

This is not a formatting preference. The ceiling is a scope test. A single automation that genuinely cannot be described in 1000 words is not one automation, and the honest response is to split it (Step 3b) rather than to write 2000 words. If you find yourself over the limit, do not trim adjectives — go back and check whether you are briefing two things at once.

Most fields want **one to three lines.** Tables beat prose. If a section has nothing decided in it, write `OPEN:` and move on rather than filling space.

Rules that keep it useful:

- **Write what was decided, not what was discussed.** Nobody needs a transcript.
- **Mark open questions as open.** A brief that hides a gap is worse than one that names it. Use `OPEN:` and say who needs to decide.
- **Do not invent decisions.** If the user did not say, it is open. Guessing here is how briefs become wrong specs.
- **Stay out of implementation.** No tool names, no architecture, no step-by-step design. "A human approves refunds above a threshold" belongs in the brief; "a Slack approval button posts to the webhook" does not. This is also the single biggest source of bloat — implementation detail expands without limit, and it is not yours to decide.

### Step 6 — Close with recommendations

End with 3–6 concrete recommendations that would make the automation better. This is where you earn your keep — the interview captured what they want, the recommendations are what you noticed.

Good recommendations are specific to their situation and actionable:

- ✗ "Consider adding monitoring."
- ✓ "You will not be able to tell a slow supplier from a broken integration, because both look like a timeout. Record which one it was."

Draw from the failure patterns in Step 4, plus anything you noticed that the user did not ask about. Flag the highest-risk gap first. If there is a decision you think is wrong, say so once, with your reasoning, and leave it with them.

## Two habits that make this work

**Prefer concrete options over open questions.** "Who approves this?" gets a shrug. "Who approves a refund over $500 — you, the support lead, or nobody because it's automatic?" gets an answer, and the third option teaches them that "nobody" was a choice they were making by default.

**Treat vagueness as information.** When someone cannot answer what happens on failure, that is not an interview problem — it is a finding. Note it as open, and put it in the recommendations. The gap you found is worth more than a smooth-sounding brief.

## Reference

`references/five-o-principles.md` — the framework this brief feeds. Read it if you need to understand *why* a decision area matters, or if the user asks about the underlying principles. You do not need it for a routine interview; the decision areas above are already derived from it.
