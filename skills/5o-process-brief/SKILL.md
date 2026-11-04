---
name: 5o-process-brief
description: Develop a concise process brief from a rough description, intended change, or requirements through a focused interview. Use for scoping or clarifying manual, AI-operated, machine-operated, or mixed processes before writing a full specification. Also supports automation ideas; does not implement the process or write the full specification.
---

# Process Brief

Produce a concise brief capturing the observations, decisions, and open questions needed to specify a process. Preserve the user's purpose and role assignments; do not turn a documentation request into an automation project.

## Establish status and scope

Determine whether the user wants a **descriptive** brief of current practice, a **prescriptive** brief of intended behavior, or a labeled combination. Infer this when clear; ask when it changes the work. A missing control in a descriptive brief is an observed gap, not permission to invent a requirement.

A process may be finite, recurring, or continuous, and may change something or maintain a condition. Start with the boundary and intended outcome rather than assuming repeated execution or a produced artifact.

## Capture the decision areas

| Area | What to establish |
|---|---|
| Objective | Outcome or maintained condition, beneficiary, scope, constraints, trade-offs, and acceptable endings. |
| Occurrence | Trigger, prerequisites, authority, timing, and conditions for continuing, pausing, resuming, and ending. |
| Order | Activities, essential dependencies, permitted concurrency, state changes, and completion conditions. |
| Roles | Operators, decision rights, process owner, and situation-specific escalation recipients. |
| Option | Alternatives, exception responses, unresolved states, and escalation/handover conditions. |
| Observation | Evidence, evaluation responsibility, review appropriate to duration, and authority to revise. |
| Objects and resources | Inputs, outputs or maintained conditions, relevant identities and states, required or consumed capacity. |

**Operator** means the entity performing an activity, including interpreting or deciding. **Process owner** holds bounded responsibility and authority for the whole process. **Escalation recipient** receives situations beyond an operator's capability or authority. **Role assignment** maps each role to a person, team, organizational unit, machine, software system, or AI agent.

No core role must be human. Do not add human approval to AI-only work or assume unlisted work is automatic in a manual process. Preserve explicit human-only or machine-only constraints when supplied. Functional ownership does not establish organizational accountability; record the surrounding governance and authority limits when relevant.

## Interview only meaningful gaps

Extract what the user already supplied. Ask at most three questions per round using an available question tool or ordinary conversation. Offer concrete alternatives from the situation when useful. Do not require a particular tool name or invent facts to end the interview.

Every question should clarify outcome or boundary, work, conditions, resources, responsibility, evidence, or a material uncertainty. No fixed round count is needed. Stop when the brief can represent the supplied decisions and remaining gaps without pretending unknowns are settled.

For prescriptive work, challenge an apparently unnecessary process once with a concrete alternative, then respect the user's answer. For descriptive work, record the apparent problem and distinguish any recommendation from observed practice.

Watch for scope that combines separate outcomes, independently triggered work, different process owners, incompatible completion conditions, or unrelated exceptions. Propose named subprocesses when this helps. Recommend which to specify first with a reason and write the brief for the agreed boundary; list the rest as out of scope. Complexity and word count alone do not prove there is more than one process. Preserve a whole-process boundary when requested, using a concise overview and explicit child references if needed.

## Checks worth asking about

- No acceptable response when the intended path cannot continue. Suspension or termination may need active maintenance of a safe condition.
- A fallback depends on the resource that would have failed. Doing nothing is not automatically independent or safe.
- An escalation names no capable, authorized, available recipient, acknowledgment condition, or bounded response to non-resolution.
- A measure rewards breaking a rule and precedence is unresolved.
- Distinct situations cannot be distinguished before a decision depends on them. Classification may occur after intake.
- Material substitutions or deviations leave no evidence useful for assessment.
- An observation or recommendation is being presented as an agreed requirement.

An escalation recipient need not be the process owner or a person. Record the triggering limit, recipient's capability and authority, transferred evidence/actions/state/request, acknowledgment and responsibility conditions, and fallback for unavailable or unresolved transfers. Do not create indefinite escalation loops.

## Write the brief

Use `assets/brief-template.md`. Save it as Markdown in the user's requested location, or a suitable project location when unspecified.

Aim for no more than 1000 words of body text, including table content. This is an authoring budget, not a universal limit on process scope. If needed, tighten repetition or separate a summary from supporting material; do not silently discard requirements or force an artificial split. Honor a different user-requested length.

- Record decisions and observations, not interview transcripts.
- Label requirements, observations, assumptions, recommendations, and `OPEN:` items.
- Identify who resolves each open item and what is blocked while it remains unresolved.
- Keep role names separate from assignments and state authority limits where material.
- Avoid unsolicited implementation design. Retain user-supplied systems or methods when they are actual constraints or current facts.
- Explain non-applicability rather than inventing monitoring, approval, or escalation machinery.
- Add a few concrete recommendations where findings support them; do not fill a quota with generic advice.

Close by identifying whether the brief is ready for specification and what remains unresolved. For descriptive work, completeness means faithful coverage of what is known, not inventing controls that current practice lacks.

## References

- `assets/brief-template.md` — output structure; keep it proportionate.
- `references/five-o-principles.md` — self-contained framework and shared terms; read for the underlying reasoning or a difficult boundary question.
