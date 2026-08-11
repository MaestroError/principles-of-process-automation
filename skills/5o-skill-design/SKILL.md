---
name: 5o-skill-design
description: Designs and audits agent skills using the Five O principles — Objective, Occurrence, Order, Option, Observation. Use this whenever someone is writing, packaging, or fixing a skill: a SKILL.md, a reusable workflow they want an agent to pick up on its own, instructions bundled with reference files or scripts. Trigger on "write a skill for", "turn this into a skill", "my skill never triggers", "Claude ignores my skill", "review my SKILL.md", "improve this skill's description", or when someone keeps re-explaining the same workflow and wants it captured once. Especially useful when a skill fires on the wrong things, gets loaded and then ignored, works only on the examples it was written against, or eats the context window. Not for writing a system or agent prompt — that is 5o-automation-prompt. Not for running, grading or benchmarking evals, or for automated description tuning — hand those to skill-creator once the design is settled.
---

# Skill Design with the Five O Principles

A skill is a **process specification that must first decide whether it applies — and then run in a harness you have never seen.**

Those two clauses are what separate a skill from a prompt, and they are why this needs its own treatment. A prompt is always loaded; a skill has to be chosen, out of a hundred others, on the strength of one paragraph. And a prompt runs where you deployed it; a skill runs wherever someone installs it, with tools you cannot enumerate.

Everything else a skill needs — a defined result, conditions for acting, dependency logic, failure paths, self-reporting — it needs for the same reasons any delegated process does. The Five O dimensions are how you find what you left out before someone installs it and never notices it isn't working.

## Two modes

**Audit** — a skill exists and misbehaves. Work out which dimension is missing; the symptom usually names it. Do this whenever a skill already exists, even when the user asks you to "improve" or "tidy" it.

**Write** — build a skill from a described workflow, a transcript of work already done, or a rough intent.

Both end the same way: the skill directory, plus a short coverage table.

**In write mode, look for the workflow that already happened.** If the conversation contains the work being captured — steps taken, tools used, corrections the user made, formats they rejected — extract from that before asking anything. What someone actually did is better evidence than what they say they do, because the corrections are in it.

**And when it is not a skill they need, say so and stop.** Instructions for one agent in one deployment are a prompt, and `5o-automation-prompt` is the better tool — nothing here about triggering or disclosure applies. Something that will only ever run once is neither. Running, grading or benchmarking an eval set is `skill-creator`'s job; come back here for the design and hand it over for the machinery. Adapting these steps to a request that is nearly this shape produces something that looks like a skill and works like a wish.

### Symptoms point at dimensions

| Symptom | Usually missing |
|---|---|
| Never fires, even on obvious cases | **Occurrence** — description written in the author's vocabulary, not the user's |
| Fires on adjacent things it should not touch | **Occurrence** — no boundary, no stated non-uses |
| Two skills both fire and fight | **Occurrence** — overlapping scope, and no statement of which wins |
| Loaded, then largely ignored | **Objective** — the instructions restate what the model already does |
| Works on the examples it was built against, fails elsewhere | **Objective** — rules encode the example rather than the reason |
| Eats the context window; everything gets slower | **Order** — no progressive disclosure, all of it in the body |
| Reference files half-read, instructions half-applied | **Order** — nested references, or a long file with no contents list |
| Output shape differs every run | **Objective** — no checkable result and no template |
| Produces a bad answer instead of declining | **Option** — no way to say "this skill does not apply here" |
| A bundled script fails and the model quietly improvises | **Option** — no failure path for the skill's own machinery |
| Works in one product, breaks in another | **Harness** — assumed a capability that install does not have |
| Nobody can tell whether a change helped | **Observation** — no evals, or evals that pass without the skill |

## Ground it in the harness first

Do this before writing or auditing anything, because it decides which instructions are writable.

**A skill is written once and executed in places you cannot see.** Claude Code, a desktop app, a web chat, the API, somebody's own agent framework. Subagents exist in some and not others. So do a display, a browser, a writable skill directory, network access, and every named tool. An instruction that assumes one of these does not fail loudly on the installs that lack it — the model reads it, cannot do it, and improvises.

- **Name the harnesses the skill must survive.** Ask, if it matters and you cannot tell. Then write instructions that degrade rather than break.
- **A capability-dependent instruction needs its fallback in the same breath.** Not in a section at the end that a reader may not reach.
- **Assume a read-only install.** A skill that writes into its own directory works on the author's machine and nowhere else.
- **Never name a tool you cannot be sure exists.** A missing capability is a finding — say what it blocks and what would fix it. Do not write the instruction you wish were executable.
- **State your assumptions in the handback**, not only inside the files. The user may read only your message.

Then ask the reverse question, as with any agent: **what can be done to it through what it reads.** If the skill directs the model to open files, fetch pages, or process tickets, that content can contain instructions. The skill is the right place to settle this once, because the skill is what gets installed and trusted — and it should name the manipulations that would actually work against this skill rather than warning about prompt injection in general.

Related, and easy to skip: **a skill must not surprise the person who installed it.** It is adopted on the strength of its description and then runs without being re-read. What it does should not exceed what its description implies.

## The five dimensions, applied to a skill

### Objective — what the skill adds that the model does not already have

The context window is a shared budget. Every paragraph competes with the conversation, the other skills, and the user's actual request, so the test for each one is: **would the outcome differ if this were deleted?** Explaining what a PDF is, or how libraries work, costs tokens and dilutes the sentences that were load-bearing. Only write what the model does not already know.

Three omissions to look for:

- **No scope exclusion.** What the skill is *not* for is half of what makes it precise, and it is also what stops it fighting its neighbours.
- **No trade-off with a named winner.** Thorough and fast, general and specific — if you do not resolve it, each run resolves it differently.
- **No stated baseline failure.** What does the model get wrong without this skill? If you cannot answer, you do not yet know whether the skill is needed, and you have nothing to measure it against.

### Occurrence — the description field is the trigger

This is the dimension with no prompt analogue, and the one that decides whether any of the rest of your work ever runs. Undertriggering is invisible: nothing errors, the skill simply never loads, and nobody finds out for months.

Four separate things, which fail differently:

- **Trigger phrases** — the words a user actually types. Casual, abbreviated, misspelled, and framed around their problem rather than your solution. Writing the description in the author's vocabulary is the standard failure: a skill about "spreadsheet normalisation" never fires on "this csv is a mess".
- **Readiness** — what must be present before the skill can do its work, and what it does when that is missing.
- **Boundary** — the near-misses that must *not* fire it. A description with only positive cases will overtrigger, and negative cases are where descriptions get their precision.
- **Competition** — which neighbouring skill wins when both could apply. State it rather than leaving it to chance.

Write the description in the third person, and make it slightly pushy — the common failure mode is skills not firing when they would have helped, not skills firing too eagerly.

Then the **variety check**: enumerate the shapes of request that will actually reach this skill, and confirm it says something about each. If real requests come in six kinds and the skill addresses one, four get handled by improvisation. Run this yourself even when the user has already listed cases — their list is at the level *they* cared about, which is rarely the level the skill operates at.

### Order — progressive disclosure is a dependency graph

What must be in context before what. This is a design decision, not a filing convention.

- **Keep the body short** — under about 500 lines, and shorter is better. It loads whole, every time the skill fires.
- **Keep references one level deep from SKILL.md.** A file referenced from a referenced file tends to get previewed rather than read, and half-read instructions are worse than absent ones because they look applied.
- **Give anything over about 100 lines a contents list**, for the same reason.
- **Split by domain, not by size.** If a skill covers four platforms, four reference files means only the relevant one loads.

Then **match freedom to fragility.** Where a sequence is exact and unforgiving — a migration, a packaging step, an order-dependent transform — give a script or an exact command, and say plainly not to vary it. Where judgement is the work, give prose and room. The failure runs both ways: prose for a fragile sequence produces silent corruption, and a rigid script for an open problem produces something worse than the model would have done alone.

Beyond that, **be precise about what must be true and loose about how.** If you are describing keystrokes, you have gone too far. Where a task is genuinely multi-step and skippable steps have consequences, a checklist helps; where correctness is checkable, a validator loop — run it, fix what it says, run it again — is worth more than any amount of instruction.

### Option — what the skill does when it does not fit

The dimension skills omit almost universally, and the direct analogue of giving an agent permission to produce nothing: **a skill needs permission to hand back.**

A skill that fires on a request just outside its scope, and has no exit, will stretch to cover it — confidently, because the model has been told this is the right tool. Give it the words: *"If the file is not a spreadsheet, say so and stop rather than adapting these steps."*

Three more:

- **When the skill's own machinery fails** — a bundled script errors, a reference file is missing, a dependency is not installed — say what to do. Silent improvisation around a broken script is the worst available outcome, because the output looks normal.
- **Partial applicability.** Do the part that fits and name the part that does not. Most requests are partly in scope.
- **Degradation in a thin harness.** Not "this needs subagents" but what to do instead when there are none.

And require the skill to say when it degraded. A model's fallback output is fluent — it looks exactly like its clean output — so a fallback nobody was told about is invisible.

### Observation — evals are the skill's observation layer

Three obligations; most skills stop before the first.

- **Record** — what the skill produced, in a form comparable across versions. This is what makes the next edit an improvement rather than a guess.
- **Judge** — against the baseline of not having the skill. An assertion that passes with and without the skill is measuring the model, not your work. This single check invalidates most eval sets.
- **Change** — evals that live in the skill directory, so the next person to edit it can rerun them.

Two kinds, and mixing them is a common error:

- **Trigger evals** test Occurrence only: would this skill fire on this request? Half should-fire, half should-not — and the should-not cases must be genuine near-misses, sharing vocabulary with the skill while needing something else. An obviously-unrelated negative case tests nothing.
- **Behaviour evals** test everything else: given that it fired, did it do the right thing?

Write the evals **before** the body. It forces you to name the failure the skill exists to fix, which is the same question as Objective's baseline, and it stops you documenting a problem you imagined.

For running, grading, and benchmarking them, and for automated description optimisation, hand off to the `skill-creator` skill if it is available — that machinery is its job, not this skill's. If it is not available, the eval set is still worth writing: it is a design artefact before it is a test suite.

### Ownership — across all five

Brief, but real. Who maintains this skill. What happens to it when the tool it wraps changes, or the product it assumes gets reorganised. Whether a bundled script is a dependency somebody must keep alive. A skill with no owner is not neutral — it rots quietly and keeps firing.

## Writing it

**The test is whether the finished skill respects the principles, not whether it displays them.** A SKILL.md organised into five headed sections named after the dimensions is a form: it buries the instruction that matters under scaffolding, and produces a paragraph per dimension whether or not that dimension needed one. The five are your checklist. The reader gets an outline shaped by their task.

*This skill is the exception that proves it — its subject is the framework, so the dimensions are its reader's task. Yours almost certainly is not, so do not copy the shape.*

- **Say why, in one clause.** A model given the reason behind a constraint applies it sensibly to cases you did not foresee; a bare rule gets applied literally and fails at the edges. But the reason is a clause, not a paragraph — two sentences of persuasion means you have started arguing with a reader who is not there.
- **Be sparing with emphatic capitals.** A skill where everything is ALWAYS and NEVER is one where nothing is. Reserve them for the genuinely non-negotiable few; the contrast is what makes those register.
- **Prefer the imperative** for instructions, and prose over heavy formatting for anything requiring judgement. Save lists and tables for reference material — cases, prohibitions, output shapes.
- **Use one term for one thing.** Field, box, element, control: pick one. Inconsistent vocabulary makes the model guess whether you meant something different.
- **Avoid anything that dates.** No "as of this version", no "until the new API ships". If old behaviour needs recording, put it in a clearly-marked section at the end rather than woven through.
- **Say each thing once.** A rule repeated in four places is not four times as binding; it is noise, and the copies drift until they contradict each other.
- **Show, where the output has a house style.** A couple of input/output pairs convey a format faster than three paragraphs describing it.

Use `assets/skill-scaffold.md` for the directory layout and a SKILL.md skeleton.

## The coverage table

Close with a compact table. Its job is not to summarise the skill — the reader has the skill. Its job is to force you to state, for each dimension, **what is still missing**.

| Dimension | Gap or risk left open |
|---|---|
| Objective | [what is still unresolved — or "covered"] |
| Occurrence | |
| Order | |
| Option | |
| Observation | |

Keep the cells to a clause. Name real gaps, including ones the skill cannot fix: a harness you could not test against, a trigger phrase you are unsure about, an eval you could not make discriminating. "Not applicable" is a claim, and it is almost always wrong for Option and Observation.

Mark it clearly as design documentation, not part of the skill.

## Before you deliver

1. Does the description contain words a user would actually type, not the author's?
2. Does it state what the skill is not for, and which neighbour wins on overlap?
3. Would deleting any paragraph change an outcome? Cut what would not.
4. Is every instruction executable in every harness named — or does it carry a fallback?
5. Can the skill decline? Find the words that permit handing back.
6. Is the body short, references one level deep, long files given a contents list?
7. Is freedom matched to fragility — exact where exactness matters, loose where judgement does?
8. Do the evals separate trigger from behaviour, and would any of them fail without the skill?
9. Is any rule stated more than once? Cut the copies.
10. Is the skill organised by the user's task rather than by the five dimensions?

## Reference

- `assets/skill-scaffold.md` — directory layout and a SKILL.md skeleton. Use when writing.
- `references/skill-patterns.md` — weak and strong phrasings for each dimension, including description rewrites. Read when writing, or when an audit finds a gap you need to fill well.
- `references/harnesses.md` — what actually varies between installs, and the fallback for each. Read when a skill depends on subagents, scripts, a browser, a display, or writing to disk.
- `references/five-o-principles.md` — the underlying framework, for when you need the reasoning or the user asks.

This skill's own `evals/` is worth a look as a worked example: `evals.json` holds behaviour cases with fixtures, `trigger-evals.json` holds the should-fire and should-not-fire pairs, and the near-misses in it are the part worth copying.
