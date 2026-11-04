---
name: 5o-process-specification
description: Write or review a process specification from a brief, requirements, or a description of current practice using Objective, Occurrence, Order, Option, and Observation. Use for manual, AI-operated, machine-operated, or mixed workflows when the user wants dependencies, conditions, decision rights, exceptions, and evidence made explicit. Specifies behavior without choosing an unsolicited implementation.
---

# Process Specification

Produce a specification that states how a process operates or is required to operate, without making decisions on the user's behalf. The output supports understanding, coordination, assessment, delegation, and revision; it need not lead to automation or code.

## Before specifying

Establish **scope**, **descriptive or prescriptive status**, and what the brief actually settles. Keep observed practice separate from requirements, assumptions, recommendations, and unresolved decisions. A descriptive specification records missing controls as gaps rather than inventing them.

Check `OPEN:` items and unasked structural gaps. For prescriptive work, resolve decisions that materially change behavior before presenting the affected part as ready. Ask at most three questions per round using an available question tool or ordinary conversation. Continue independent specification work where possible. If a blocking decision cannot be resolved, deliver the supported parts with the gated behavior and its decision authority explicit. Do not invent a mapping, threshold, role, or permission.

For descriptive work, unresolved facts remain unknown; they need not prevent documenting the rest of the current process accurately.

Write one specification when one coherent boundary suffices. Decompose only when independently triggered work, separate outcomes or owners, distinct completion conditions, or meaningful interfaces justify it. See `references/composition.md` for parent/child contracts. Document length alone is not a scope test.

## Shared vocabulary

An **operator** performs an activity, including gathering, interpreting, deciding, or acting. A **process owner** holds responsibility for the whole process with defined authority over requirements, performance, and revision. An **escalation recipient** addresses a designated class of situations beyond the current operator's capability or authority. A **role assignment** maps a role to an entity.

Any role may be assigned to a person, team, organizational unit, machine, software system, or AI agent. Do not default decisions or escalations to a human, and do not default unspecified work to automatic execution. Preserve constraints the user explicitly supplies. Functional ownership does not settle organizational accountability; identify governing authority and its limits when relevant.

## Writing the specification

Use `assets/spec-template.md`, adapting detail to purpose, complexity, and consequence. A short finite process, a continuous maintained condition, and a recurring workflow need different depths, not different core vocabulary.

### Objective

State assessable outcomes or maintained conditions, beneficiaries, boundaries, constraints, permitted trade-offs, and criteria for success, partial completion, suspension, or justified termination. Resolve precedence where a metric could reward violating a constraint. Qualitative criteria are legitimate when their evaluation and reviewing role are explicit.

### Occurrence

Distinguish trigger, readiness, authorization, and timing. Cover beginning, continuing, suspending, resuming, and ending activity. State which conditions are reassessed and when. Identify where materially different cases are distinguished before decisions depend on that distinction; classification need not occur in the initial trigger.

### Order

Specify essential dependencies and permitted state transitions. Include flow dependencies (an acceptable earlier output), sharing dependencies (limited resources), and fit dependencies (parts that must compose), where applicable. State permitted concurrency, synchronization, cancellation or pending states, and completion conditions.

Assign responsibilities and decision rights. Where relevant distinguish gathering information, interpretation, decision, and action. Use **roles and authority**, not an automatic/human binary or a mandatory automation-level grid. Preserve a required method when it is a genuine constraint; otherwise leave implementation choices open.

### Option

Define variants, exception responses, and recovery to an acceptable state. A safe condition may require continued activity; do not equate stopping with doing nothing.

Check fallback dependencies against the failures they are meant to address. Mark shared dependencies and residual limitations rather than claiming universal independence.

For each escalation, specify its trigger; recipient and required capability/authority; availability; transferred outcome, evidence, actions, current state, and requested resolution; acknowledgment and responsibility-transfer conditions; and a bounded response to unavailability or non-resolution. Do not assume the recipient is human or the process owner. Prevent indefinite transfer loops.

Specify which material deviations, retries, or substitutions are recorded or communicated, to whom, and when. Do not require immediate alerts for every event. State how essential capabilities remain available where that matters; human practice or machine capability checks are possible implementations, not defaults.

### Observation

Define evidence needed to assess activity and outcomes; its meaning, access, and retention where relevant; the evaluating role and criteria; and the authority and route for revision. Evidence need not be digital logs.

Consider current deviations, accumulated friction, and trends for recurring or continuous work. A one-time process may need only completion evidence and a closeout review. Explain omitted horizons. State what external changes would invalidate assumptions where relevant. A finding does not itself authorize changing a requirement.

### Cross-cutting requirements

For every O, identify responsibilities, authority, objects, relevant states, and resources. Keep the process owner distinct from activity operators and situation-specific escalation recipients. List role assignments with capability and availability requirements. Do not infer organizational accountability from assigning an AI functional ownership.

## Specification quality and composition

- Declare scope, status, version or effective period, and source of requirements.
- Use consistent terms, identities, states, and units; resolve conflicting rules.
- Make requirements assessable with appropriate evidence.
- State each rule once at the level responsible for it and reference it elsewhere.
- Preserve uncertainty and identify who may resolve it and what remains gated.
- Keep interfaces and acceptance conditions explicit; recheck conditions that can change after admission or handover.
- Name governing authority for revision and how changes reach affected roles.
- Assess feasibility separately. An operator-independent specification supports transitions without guaranteeing interchangeable implementations.

Avoid choosing tools, vendors, or architecture unless requested. Keep user-supplied systems and methods when they are requirements, relevant current facts, or real dependencies; neutrality is not permission to erase them.

## Before delivery

1. Does the specification faithfully separate observed practice and required behavior?
2. Are all five dimensions considered, with proportionate detail or justified non-applicability?
3. Are responsibilities, decision rights, resources, and applicable role assignments explicit?
4. Does every escalation have a viable contract and bounded unresolved outcome?
5. Are fallback limitations and safe-state obligations honest?
6. Can evidence establish satisfaction or violation of requirements at the needed level?
7. Are open items preserved with decision authority and affected activity visible?
8. Are terms, interfaces, constraints, and revision rules consistent?
9. Would the core requirements work for wholly manual and wholly AI execution without translating human-only or automation-only terminology?

Deliver supported content with open items and specific risks or implementation-assessment questions. Do not label an unresolved prescriptive specification ready for unrestricted execution. Do not imply that completing the template proves correctness or feasibility.

## References

- `assets/spec-template.md` — single-process structure, adapted proportionately.
- `references/composition.md` — use when parent/child specifications are justified.
- `references/five-o-principles.md` — self-contained framework and vocabulary.
