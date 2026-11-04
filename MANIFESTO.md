# The Five O Principles of Process Specification

**Five questions for stating how a process works or how it should work.**

The same questions apply when the work is performed entirely by people, entirely by AI or machines, or by any combination. They help you describe existing work, design new work, coordinate responsibilities, assess results, and revise requirements. Automation is one possible application.

These principles bring together ideas from quality management, coordination, control theory, workflow design, and human factors. They identify what to make explicit. They do not guarantee that the process is worthwhile or that a particular implementation can carry it out.

---

## What are we specifying?

**A process is a related set of activities contributing to an outcome.** The outcome may change something, maintain a condition, or prevent an unwanted change.

A process can happen once, recur, or continue indefinitely. State its boundary: what work is included, what is outside it, and where it connects to other work. A continuous process needs conditions for operating and pausing even if it has no scheduled finish.

Declare which kind of specification you are writing:

- **Descriptive:** how the process currently works. Record unknowns and departures from stated rules honestly.
- **Prescriptive:** how the process is required to work. Distinguish requirements from assumptions, recommendations, and undecided questions.

If you include both, label them. A desired future state is not a description of current practice.

## Agree on roles before assigning them

An **operator** performs an activity. Gathering information, interpreting it, deciding, and acting are all activities.

A **process owner** holds responsibility for the process as a whole, with defined authority over requirements, performance, and revision.

An **escalation recipient** receives a situation the current operator cannot resolve within its capability or authority. It may be a specialist or a role with different permissions. It need not be the process owner or a hierarchical superior.

A **role assignment** identifies what fills each role: a person, team, organizational unit, machine, software system, or AI agent. No core role has to be human. One entity can fill several roles, but their responsibilities and authority remain distinct.

Ownership here is functional. The surrounding governance determines organizational accountability and any requirement for a human or organizational authority. Assigning an AI a role does not settle those wider questions.

See [TERMS.md](./TERMS.md) for the shared definitions.

## First, ask what the work is for

Before preserving the present steps, ask what outcome is needed and whether the process should exist. A precise specification of unnecessary work still specifies unnecessary work.

---

## 1. Objective — specify outcomes and limits

State:

- **The outcome or condition** sought, and for whom.
- **The boundary:** what is included and excluded.
- **The constraints:** what must not happen.
- **The trade-offs:** which priorities may be sacrificed, and within what limits.
- **The ending criteria:** what counts as success, partial completion, suspension, or justified termination.

An objective can be assessed without being reduced to one number. Where judgment is needed, name the criteria and the role authorized to apply them.

**If omitted:** different operators pursue different outcomes, or a measure rewards breaking a rule.

**Ask:** Could an independent reviewer tell what success means? Which rule wins when priorities conflict? When should the process pause or end?

## 2. Occurrence — specify conditions for activity

Distinguish four things:

- **Trigger:** the event or state proposing activity.
- **Readiness:** the information, resources, and conditions that must be present.
- **Authorization:** the authority permitting action.
- **Timing:** when action is appropriate, too early, too late, or no longer allowed.

Then specify which conditions must remain true, and what permits continuing, suspending, resuming, and ending activity. A valid start does not authorize continuing after the conditions change.

Identify situations requiring different treatment and where they are distinguished. Classification can happen after intake, provided the distinction is available before the decision depending on it.

**If omitted:** work starts on incomplete information, continues without permission, or misses the right moment.

**Ask:** What permits activity now? What change requires reassessment? Where are materially different situations distinguished?

## 3. Order — specify dependencies and decision rights

State what depends on what:

- One activity needs an output from another.
- Several activities need the same limited resource.
- Several outputs must fit together.

Specify required sequencing, permitted concurrency, synchronization, state changes, and completion conditions. A step-by-step procedure belongs here when the method itself is required; otherwise retain freedom over method.

Assign responsibility and discretion. Where relevant, distinguish which role gathers information, which interprets it, which decides, and which acts. Any of those roles can be filled by people, machines, or AI.

**If omitted:** work uses stale inputs, competes for resources, produces incompatible parts, or leaves a handover without clear responsibility.

**Ask:** What must be true before what? What can happen concurrently? Who may decide and act, within what limits? What makes a handover complete?

## 4. Option — specify alternatives and unresolved situations

State:

- **Variants:** permitted alternative routes.
- **Exceptions:** responses when assumptions do not hold.
- **Recovery:** routes to an acceptable state when the intended path cannot continue.

Name an acceptable pending state, alternative route, controlled suspension, or safe termination when no ordinary route succeeds. Doing nothing is not automatically safe: some conditions require continued activity to remain safe.

Check each fallback's dependencies. A backup needing the resource that just failed is unavailable for that failure too.

### Make escalation a real contract

For every escalation, specify:

1. The condition the current operator cannot resolve.
2. The escalation recipient, its required capability and authority, and its availability.
3. What transfers: intended outcome, evidence, actions taken, current state, and the decision or action required.
4. How receipt and responsibility are confirmed, within what limit.
5. What happens if the recipient is unavailable or cannot resolve it.

A person may escalate to an AI specialist; an AI assessor may escalate to another AI with different permissions; a machine may transfer control to a supervisory system. Naming a different destination is not enough if it has the same unresolved limitations.

Keep transfer paths bounded. They must not become endless circles of recipients returning the same unresolved situation.

### Make important deviations visible

Specify which substitutions, retries, and exceptions are recorded or communicated, to whom, and when. Evidence can reveal a deteriorating dependency even when the final outcome is acceptable. It does not follow that every retry needs an immediate alert.

**If omitted:** operators improvise without limits, work disappears into an unowned queue, or activity stops in an unacceptable state.

**Ask:** What happens when this route is unavailable? Who can actually resolve the exception? What state is maintained while waiting? What if the transfer fails?

## 5. Observation — specify evidence, evaluation, and revision

Observation has three duties:

- **Record:** enough evidence for the declared purpose.
- **Judge:** compare activity and outcomes with requirements.
- **Revise:** identify how findings reach a role authorized to retain or change the requirements.

Evidence can be paper records, measurements, inspections, acknowledgments, samples, or event histories. Choose it from the questions that need answers.

For recurring or continuous work, consider what is wrong now, what accumulates across executions, and what is getting worse. For a short, one-time process, completion evidence and a closeout review may suffice. Explain why a review horizon does not apply rather than inventing monitoring work.

Consider changes outside the process that might invalidate its assumptions. A finding can justify a change, but it does not itself grant authority to make that change.

**If omitted:** nobody can assess what happened, or findings have no route to action.

**Ask:** What evidence establishes satisfaction or violation? Who evaluates it? Who may revise the requirements, within what limits?

---

## Two checks across all five

**Ownership and authority.** Identify who holds each responsibility, which decisions they may make, and what capability and availability the assignment requires. Keep the process owner, activity operators, and escalation recipients distinct even when one entity fills several roles.

**Objects and resources.** Name what the process acts on, the states that matter, and the resources it needs or consumes. Include shared capacity, contested resources, and dependencies shared by alternative routes.

## How a good specification is written

- **Declare status:** observed fact, requirement, assumption, recommendation, example, or unresolved decision.
- **Use consistent meanings:** define important terms and resolve conflicting rules.
- **Make requirements assessable:** identify suitable evidence and evaluation criteria.
- **Specify essential detail:** preserve freedom over method unless the method is required.
- **Keep uncertainty visible:** say who resolves it and what must wait meanwhile.
- **Connect the parts:** define interfaces, acceptance conditions, and responsibility at boundaries. State each rule once and reference it elsewhere.
- **Govern changes:** identify the applicable version, change authority, and how affected roles learn of revisions.

## Limits and the universality test

Five headings do not prove completeness, correctness, feasibility, or value. Apply the depth and domain methods appropriate to the process. Explain non-applicable requirements. Do not promise that a specification makes operators interchangeable: each implementation still needs assessment of capability, authority, interfaces, resources, and evidence.

The core framework passes two tests only when its requirements can be used unchanged to specify:

- A process performed entirely by people.
- A process performed entirely by AI or machines.

The role assignments and implementation details differ. The five dimensions and their meanings do not.

See [the examples](./examples/README.md) for both tests in practice, and [PRINCIPLES.md](./PRINCIPLES.md) for the fuller framework and its sources.
