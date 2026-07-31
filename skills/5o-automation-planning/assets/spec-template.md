# Automation Spec: [process name]

**From brief:** [brief name/date] · **Status:** [Ready to build | Blocked on open items]

**In one line:** [what this does]

---

## Objective

**Result:** [stated so someone could verify it happened]
**For whom:** [who receives it]
**Measured by:** [the observable outcome]

**In scope:** [what this covers]
**Out of scope:** [what it deliberately does not]

**Must never happen:**
- [prohibition, not preference]

**Trade-offs, with floors:**
| May be sacrificed | Down to | Never below |
|---|---|---|
| [dimension] | [floor] | [hard limit] |

**Stop criteria:** [conditions under which not completing is the correct outcome]

---

## Occurrence

| | |
|---|---|
| **Trigger** | [the event proposing a run] |
| **Readiness** | [what must be present and true first] |
| **Authorisation** | [under whose authority; checked at run time?] |
| **Window** | [when acting is correct; when it would be too early or too late] |

**Cases the trigger must tell apart:**

| Situation | How it is recognised | Different handling |
|---|---|---|
| [case] | [signal] | [what changes] |

*If the trigger cannot distinguish these, classification is a step in Order — not an error handler.*

---

## Order

**Dependencies:**

| This | Requires | Kind | Handled by |
|---|---|---|---|
| [step] | [what must exist first] | [produced-by / shared-resource / must-fit] | [the rule that enforces it] |

**May run concurrently:** [what need not be serialised]

**Finished means:** [a checkable condition]

**Automation level per step** — who collects, interprets, decides, acts:

| Step | Collect | Interpret | Decide | Act |
|---|---|---|---|---|
| [step] | [auto/human] | [auto/human] | [auto/human] | [auto/human] |

**Human decision points and why they stay human:**
- [decision] — [reason]

---

## Option

**Variants, in priority order:**

| # | Route | Use when | Depends on |
|---|---|---|---|
| 1 | [route] | [condition] | [what it needs] |

**Exceptions:**

| Condition | Response | Recorded as |
|---|---|---|
| [condition] | [what happens] | [the flag raised] |

**Recovery and safe stop:** [the fallback state — and confirmation stopping is allowed]

**Independent failure domains:**

| Route | Depends on | Independent of primary? |
|---|---|---|
| [route] | [dependency] | [yes/no] |

*If no route is independent, say so. The only fully independent option is usually doing nothing.*

**Handover contents** — what a human receives when it steps down: [what was attempted, current state, what is specifically needed]

**Practice:** [any deliberate manual exercise to keep skills warm — or "not required, low consequence"]

---

## Observation

**Recorded each run:** [fields — including retries, fallbacks, route switches, not only failures]

**Judged by:**

| Horizon | Signal | Response |
|---|---|---|
| Now | [per-run] | [immediate action] |
| Accumulated | [what is slightly wrong every time] | [redesign trigger] |
| Trending | [what is getting worse before it breaks] | [early warning] |

**Revision route:** [how a finding actually changes this spec, and who may change it]

**External check:** [what would indicate this process should no longer exist]

---

## Ownership

| Responsibility | Who | Availability |
|---|---|---|
| Owns the outcome | [name/role] | |
| May change the objective | [name/role] | |
| Authorises a run | [name/role] | |
| Receives escalation | [name/role] | [hours; cover when away] |
| Reads observation output | [name/role] | [what they may change] |

---

## Resources

**Acts on:** [objects] · **Consumes:** [systems, quota, budget, attention]

**Contended:** [what two things need at once, and how that is resolved]

**Support congruence:** [any measure that fights a rule, and which takes priority]

---

## Open items

| Item | Who decides | Blocking build? |
|---|---|---|
| [OPEN: ...] | [who] | [yes/no] |

## Risks to watch during build

1. [specific, with what to look for]
2. [...]
