# The Five O Principles of Process Automation

*A domain-neutral grammar for specifying, automating, and evolving any process — regardless of whether its operators are human, mechanical, algorithmic, or artificial.*

---

## Preface: what this document is and is not

This document states five principles that together form a **minimum complete specification** for an automatable process. It is not a methodology, a notation, or a maturity model. It is a grammar: a small set of dimensions that any process must define before it can be delegated to an operator that is not the person who designed it.

The claim is not novelty. Every one of the five dimensions has been studied for decades under different vocabularies — as setpoints in control theory, start events in workflow notation, dependencies in coordination theory, graceful degradation in human factors, and event logs in process mining. The claim is **synthesis and portability**: these traditions have never been reconciled into a single, memorable, cross-domain checklist, and practitioners consequently apply one tradition's rigor while inheriting another tradition's blind spots. A control engineer rarely thinks about function allocation. A business analyst rarely thinks about requisite variety. A prompt engineer rarely thinks about either.

The Five Os are therefore offered as an **interoperability layer** between mature disciplines, not as a replacement for any of them. Where a discipline offers greater rigor for a given dimension — Petri nets for Order, STPA for Occurrence, process mining for Observation — the Five O framework's job is to tell you that you need it, not to substitute for it.

A caution stated up front, because it governs everything below: **the Five Os are a grammar, not a guarantee.** A process can satisfy all five dimensions completely and still be a bad process, because completeness of specification says nothing about the wisdom of what was specified. This is the enduring force of Hammer's (1990) directive to *obliterate rather than automate*: an automation that flawlessly executes an obsolete objective is a more efficient way of being wrong.

---

## 1. What is a process?

> **A process is a bounded transformation: a set of interrelated activities that consume inputs and produce an intended result, performed by one or more operators, repeatably enough that its structure can be described independently of any single execution.**

Four elements of this definition do real work.

**Bounded.** A process has a beginning and an end. Work that has no defined completion is not a process but a *practice* or a *state*. Continuous control loops qualify only because each control cycle is itself a bounded transformation.

**Transformation.** Something must change. A process that consumes inputs and produces nothing distinguishable from the inputs is waste, and should be eliminated rather than automated.

**Operator-agnostic.** The definition deliberately does not say *who* performs the activities. This is the load-bearing move for domain neutrality. Historically, automation theory has recognised that the division of labour precedes and shapes mechanization — Adam Smith (1776) observed that machines which abridge labour originate in the division of labour itself, and Babbage systematised this into what Pasquinelli (2024) calls a labour theory of automation: the structure of human work becomes an abstract machine before it becomes an actual one. If a process is properly specified, reassigning it between a clerk, a script, a PLC, and an LLM agent is a *deployment decision*, not a redesign.

**Repeatably describable.** A one-off act is not a process. Automatability requires that the structure recur even when the particulars vary.

### The completeness claim

The five principles correspond to five questions that must be answerable before a process can be delegated:

| Dimension | Question | Phase |
|---|---|---|
| **Objective** | What result counts as success, within what boundaries? | Setup |
| **Occurrence** | Under what conditions may execution begin or continue? | Setup |
| **Order** | What must be true before what, and what may proceed in parallel? | Execution |
| **Option** | What happens when reality diverges from the nominal path? | Execution |
| **Observation** | What evidence does execution produce, and how does that evidence change the process? | Evolution |

**Setup** (Objective, Occurrence) establishes the control boundary. **Execution** (Order, Option) encodes the operational logic. **Evolution** (Observation) closes the loop back onto Setup.

The framework's assertion is that these five are *jointly sufficient* for specification and *individually necessary*: remove any one and a distinct, well-documented class of failure becomes available. Those failure classes are named in each section below.

### Three running cases

To demonstrate that the principles are not artefacts of any one domain, the same three cases are traced through all five:

- **Case L — Legal.** Enterprise NDA intake, review, negotiation, and execution. Operators: paralegal, counsel, clause-extraction model, e-signature platform.
- **Case I — Industrial.** Temperature control of a batch chemical reactor within a production run. Operators: PID controller, safety interlock, panel operator.
- **Case D — Digital/AI.** An agentic system that triages inbound customer support requests and drafts or executes resolutions. Operators: LLM agent, backend APIs, support engineer.

---

## 2. Objective — What is the goal, and what are its boundaries?

> **The Objective is the complete definition of success: the intended result, the boundary of legitimate action, and the trade-offs the process is authorised to make.**

### The Rule

An Objective is insufficiently specified until it states four things: the **intended value** delivered and to whom; the **scope boundary** — what is explicitly outside this process; the **non-negotiable constraints** — the absolute must-nots; and the **acceptable trade-offs** among cost, time, quality, and flexibility. It must also state **stop criteria**: the conditions under which abandoning the objective is the correct outcome.

### Grounding

In control theory the Objective is the **setpoint** — the reference value against which the measured process variable is compared to produce the error signal that drives corrective action (Åström & Murray, 2008). Without a reference, feedback is meaningless; there is nothing to be an error *from*. This is the mathematical form of the principle, and it applies to any closed-loop system regardless of substrate.

In management systems, ISO 9001:2015's process approach requires that process design begin from organisational context, interested parties, scope, objectives, and intended outputs, with risk-based thinking applied throughout. The Objective is not a slogan but a specification artefact.

Two literatures explain why the *boundary* half of the principle matters as much as the *goal* half. First, Reijers and Limam Mansar (2005), surveying redesign heuristics, work from a four-dimensional model of process performance — **time, cost, quality, flexibility** — which they call the **devil's quadrangle**, because "improving upon one dimension may have a weakening effect on another." Their example: adding reconciliation tasks improves quality of service at the cost of timeliness. A redesign that does not name its permitted trade-off will make one silently. Second, and more sharply, an autonomous system given a setpoint without rigid boundaries will minimise its error signal by whatever means its environment permits — including means that damage variables nobody thought to measure. The boundary is what prevents the optimiser from exploiting the specification.

The deepest critique of naive Objective-setting remains Hammer's (1990). Ford's North American accounts payable function employed more than 500 people; the initial objective was to rationalise the process, install new systems, and cut headcount by some 20% — to around 400. On discovering that Mazda ran an equivalent function with a total of five people, Ford recognised the objective itself was wrong. The old rule was "We pay when we receive the invoice." The reengineered rule was **"We pay when we receive the goods."** Ford instituted invoiceless processing: receiving checks arriving goods against an online purchase-order database, matching three data items rather than the previous fourteen, and the system issues payment with no invoice ever generated. The result was a 75% headcount reduction — not the 20% a conventional automation programme would have delivered. The lesson generalises: **the most common automation failure is the uncritical inheritance of a legacy objective.**

### Across the three cases

| | Objective as commonly stated (weak) | Objective properly specified |
|---|---|---|
| **L — NDA** | "Review NDAs faster." | Execute a mutually acceptable NDA within 3 business days, with zero deviations from the confidentiality-term and governing-law playbook without counsel approval; scope excludes NDAs attached to master agreements; speed may be traded for accuracy but never for playbook compliance; stop and escalate if the counterparty rejects a non-negotiable clause twice. |
| **I — Reactor** | "Keep the reactor at temperature." | Hold vessel temperature at 185 °C ± 2 °C for the 40-minute hold phase; never exceed 210 °C under any condition; overshoot is preferred to undershoot up to 195 °C; abort the batch and vent if the ±2 °C band cannot be held for 90 consecutive seconds. |
| **D — Support** | "Automate support tickets." | Resolve or correctly route 100% of inbound tickets within 15 minutes of receipt; never issue a refund above $200 or make a statement about contractual liability; deflection rate may be traded against customer-satisfaction score down to a floor of 4.2/5; hand to a human whenever confidence in intent classification falls below threshold. |

### Failure mode if ignored

**Misaligned automation.** The system optimises the wrong variable, at speed. Legacy inefficiency is encoded rather than removed — Hammer's "paving the cow paths." Where the operator is a capable optimiser, unbounded objectives additionally invite specification gaming.

### Review questions

1. What value is delivered, to whom, and how would an outsider verify it was delivered?
2. What is explicitly *out* of scope?
3. What must never happen, even if it would achieve the goal faster?
4. Which of cost, time, quality, flexibility may be sacrificed, and to what floor?
5. Under what conditions is *not completing* the correct outcome?
6. If we were designing this from a blank sheet today, would this objective exist at all?

---

## 3. Occurrence — Under what conditions may execution begin or continue?

> **The Occurrence is the complete set of conditions — event, state, data, resource, and authority — that must hold for the process to be permitted to act.**

### The Rule

Occurrence is not merely *when*. It is the conjunction of a **trigger** (the event or state change that proposes execution), **readiness** (the data, resources, and preconditions that must be present), **authorisation** (the permission under which action is legitimate), and a **timing window** (the period within which acting is correct). A process should never run blindly; each of these four can independently make execution wrong.

### Grounding

The distinction between **open-loop and closed-loop** activation is foundational. An open-loop (feedforward) trigger is independent of process state — a boiler on a timer heats regardless of building temperature and cannot compensate for disturbance. A closed-loop trigger is state-dependent: the thermostat fires on deviation from setpoint (Åström & Murray, 2008). Most brittle automations are open-loop triggers imposed on closed-loop realities.

Process notation makes the composite structure explicit. BPMN 2.0 formalises initiation through typed **start events**; CMMN 1.1 introduces the **sentry**, which explicitly combines an *event part* and a *condition part* — a direct notational admission that trigger and readiness are separate things that must both hold.

Safety analysis supplies the failure taxonomy. Leveson's STPA (Leveson, 2011; Leveson & Thomas, 2018) classifies unsafe control actions into four kinds: a control action *not provided* when needed; provided when it *causes a hazard*; provided at the *wrong time or in the wrong order*; and applied for *too long or stopped too soon*. Three of these four are Occurrence failures, and they are not reducible to one another — which is why "when does it start" is too weak a formulation.

The depth limit on Occurrence design comes from cybernetics. Ashby's (1956) **Law of Requisite Variety** — "only variety can destroy variety" (§11/11) — holds that a regulator can compensate for disturbance only insofar as its own range of distinguishable responses matches the range of disturbances the environment can produce. Ashby's own illustration is exact: a press photographer facing twenty subjects distinct in exposure and distance needs a camera with at least twenty distinct settings. Applied to triggering, this means a system's sensing and trigger logic must be at least as differentiated as the situations it must tell apart. Conant and Ashby (1970) sharpen this further: every good regulator of a system must be a model of that system. A trigger condition is, in miniature, a model of the environment; where that model is coarser than reality, false positives and missed signals are not bugs but arithmetic.

### Across the three cases

**L — NDA.** *Trigger:* document arrives in the legal intake mailbox. *Readiness:* it is actually an NDA and not a superseded draft; counterparty entity is identified and not on the sanctions list; the requesting business unit is named. *Authorisation:* requester is entitled to initiate a contracting action. *Window:* not during a live M&A quiet period, where a separate process governs.

**I — Reactor.** *Trigger:* charge complete and agitator confirmed running. *Readiness:* thermocouple redundancy healthy, coolant loop pressurised, vessel level within band. *Authorisation:* batch record released by QA. *Window:* the hold phase, and only after ramp completes — heating applied at the wrong phase is a distinct hazard from heating not applied at all.

**D — Support.** *Trigger:* new ticket created. *Readiness:* customer account resolved, entitlement verified, conversation history retrieved, required backend APIs responding. *Authorisation:* the agent's action scope for this customer tier. *Window:* not while a related incident is open, where responses must be centrally coordinated.

### Failure mode if ignored

**Blind or brittle activation.** The process fires on incomplete state, fires when it should not, fires at the wrong moment, or fails to fire at all. Where environmental variety exceeds trigger variety, this is systematic rather than occasional (Ashby, 1956).

### Review questions

1. What event proposes execution — and is that event closed-loop or open-loop with respect to actual state?
2. What must be *present and true* for action to be safe, beyond the trigger firing?
3. Under whose authority does this run, and is that authority checked at runtime?
4. Is there a period during which acting would be wrong even though the trigger is valid?
5. Can the trigger logic distinguish every situation that requires a different response? If not, where does it collapse distinct cases?
6. Which is worse here — a false start or a missed start — and does the design reflect that asymmetry?

---

## 4. Order — What must be true before what?

> **The Order is the dependency structure of the process: what must precede what, what may proceed concurrently, where flows must synchronise, what completion means, and which operator holds each step.**

### The Rule

Order is not a list of steps. It is the encoded resolution of dependencies. Specify the *dependency graph* rather than the *step sequence*: over-specifying sequence removes legitimate concurrency and makes the process brittle, while under-specifying it permits incoherent states. Order must additionally assign each step to an operator at a defined level of autonomy.

### Grounding

**Coordination theory** provides the conceptual core. Malone and Crowston (1994) define it in one line: *"Coordination is managing dependencies between activities."* The definition implies a distinction the rest of this principle rests on — between the work that directly produces the intended result, and the additional work of making that production interlock. Automation programmes characteristically optimise the former and neglect the latter, then fail at the seams. Crowston (1997) applies this to process design; Malone et al. (1999) give the three-way dependency classification used here:

| Dependency | Arises when | Order must therefore specify |
|---|---|---|
| **Flow** | "one activity produces a resource that is used by another activity" | That downstream work waits until the upstream output **exists** (prerequisite), **has been made available** (accessibility), and is **usable by the consuming activity** (usability) — Malone et al.'s own decomposition of flow |
| **Sharing** | "multiple activities all use the same resource" | Scheduling and contention handling — first-come/first-serve, priority order, budgeted allocation, managerial decision, or bidding |
| **Fit** | "multiple activities collectively produce a single resource" | Standardisation and integration rules ensuring the independently produced parts compose |

**Formal workflow theory** explains why sequence alone is inadequate. Van der Aalst's (1998) application of Petri nets to workflow management models processes in terms of *states*, *enabling conditions*, concurrency, synchronisation, and **soundness** — the property that a process can always terminate properly with no dangling work. The workflow patterns literature (van der Aalst et al., 2003; Russell et al., 2016) catalogues the control-flow constructs a naive linear list cannot express: parallel split and synchronising merge, discriminators, multiple instances, cancellation regions, deferred choice. If your Order can express only "then," it cannot express most real processes.

**Function allocation** determines who executes each node. Early treatments posed this as a binary — which tasks suit humans, which suit machines — a framing now understood as too coarse to design with. Its successors are essential. Sheridan and Verplank (1978) introduced a **ten-level continuum of automation**, from the computer offering no assistance through to the computer deciding and acting while ignoring the human entirely. Parasuraman, Sheridan and Wickens (2000) then made the decisive refinement: automation level is not a single property of a system but is set **independently across four stages** — information acquisition, information analysis, decision selection, and action implementation.

This yields the practical rule: **assign a level of automation per stage, per step — never per system.** A well-designed process is routinely level 10 at information acquisition, level 4 at decision selection, and level 1 at exception handling. "Is this process automated?" is the wrong question; the framework replaces it with a matrix.

A final note: coordination need not be explicit. **Stigmergic** coordination — where operators coordinate through traces left in the shared work itself rather than through direct communication — is a legitimate and often superior mechanism, observed in biological systems and in large-scale distributed human work such as Wikipedia editing (Rezgui, Crowston & Jullien, 2018). Automated systems can exploit this by writing state into the artefact rather than into a message bus.

### Across the three cases

**L — NDA.** *Flow:* clause extraction cannot begin until the document is OCR'd and identified; signature cannot execute until both redline approval and internal counter-approval exist. *Sharing:* counsel's attention is the scarce resource, requiring a prioritised queue. *Fit:* the executed PDF, the CLM metadata record, and the obligations register must be mutually consistent. *Allocation:* extraction at level 10, playbook deviation judgement at level 4 (system proposes, counsel approves), novel-clause negotiation at level 1.

**I — Reactor.** *Flow:* ramp precedes hold precedes cooldown; the safety interlock's authority precedes all of them and is not sequenced but *superordinate*. *Sharing:* a shared coolant header across vessels demands allocation logic. *Fit:* the batch record must reconcile with process historian data for release. *Allocation:* loop control at level 10, batch abort at level 6 (system acts after a bounded veto window), deviation investigation at level 1.

**D — Support.** *Flow:* intent classification precedes tool selection precedes action; entitlement check precedes any account mutation. *Sharing:* rate-limited backend APIs and the human escalation queue. *Fit:* the customer-facing reply, the ticket record, and any account change must tell the same story. *Allocation:* retrieval at level 10, refunds under $50 at level 7 (act and inform), refunds above that at level 5 (act only on approval).

### Failure mode if ignored

**Coordination failure.** The process breaks at the joints rather than at the steps — work proceeds on stale inputs, resources deadlock, independently correct outputs fail to compose, and no operator is accountable for the seam. Where allocation is unspecified, responsibility gaps open exactly where judgement is most needed.

### Review questions

1. What are the flow, sharing, and fit dependencies — and which are currently managed only by someone remembering?
2. What may legitimately run in parallel that the current design serialises?
3. Where must concurrent branches synchronise, and what happens if one never arrives?
4. What does *complete* mean, formally? Can the process reach a state from which it can neither proceed nor properly terminate?
5. For each step, what level of automation applies at each of acquisition, analysis, decision, and action?
6. Is coordination carried by explicit messages, or by traces in the shared artefact — and is that deliberate?

---

## 5. Option — What happens when reality diverges from the nominal path?

> **The Option is the designed response to deviation: the variants, exception paths, recovery procedures, escalation routes, and safe-stop states that govern the process when the primary path is unavailable.**

### The Rule

Deviation is a normal operating state, not an edge case. A process must specify three distinct classes of response: **variants** (legitimate alternative routes to the same objective), **exceptions** (handling for conditions outside assumption), and **recovery** (return to a consistent state, escalation to a more capable operator, or safe stop). Crucially, the process must degrade *gracefully* — stepping down through progressively lower levels of automation — rather than abdicating abruptly.

### Grounding

Ashby's law again sets the theoretical floor: no regulator can destroy more variety than it possesses (Ashby, 1956). Since no designer can enumerate the variety of an open environment, every real automation will encounter states it cannot handle. The Option dimension is therefore not defensive programming; it is the acknowledgement of a proven structural limit. Escalation to a human is the standard mechanism for importing variety the system does not have.

The literature that matters most here is Bainbridge's (1983) *Ironies of Automation* — the single most important paper in this framework, and the one most often ignored by builders of automation. Bainbridge observed that designers automate the routine and predictable portion of work precisely because they can, and leave to the human operator exactly the residue they could not anticipate. This produces a set of compounding ironies:

- **The designer's ironies.** Bainbridge names two. First, the designer who regards the operator as "unreliable and inefficient" is themselves a major source of operating problems — "designer errors can be a major source of operating problems." Second: "the designer who tries to eliminate the operator still leaves the operator to do the tasks which the designer cannot think how to automate." The residue is, by construction, the hardest part of the job.
- **Skill degradation.** "Physical skills deteriorate when they are not used, particularly the refinements of gain and timing. This means that a formerly experienced operator who has been monitoring an automated process may now be an inexperienced one." And the moment of takeover is the worst possible moment: "when manual take-over is needed there is likely to be something wrong with the process, so that unusual actions will be needed to control it, and one can argue that the operator needs to be *more* rather than less skilled, and *less* rather than more loaded, than average."
- **The vigilance problem.** The limit is specific, not vague: "it is impossible for even a highly motivated human being to maintain effective visual attention towards a source of information on which very little happens, for more than about half an hour." Any design that assumes sustained human monitoring of a reliable system is assuming something people cannot do.
- **Cold context on takeover.** Bainbridge anticipates the situation-awareness literature directly. The operator's working knowledge of process state "takes time to build up" — manual operators would arrive "quarter to half an hour before they are due to take over control, so they can get this feel for what the process is doing." Under automation, "the operator who has to do something quickly can only do so on the basis of minimum information."
- **Loss of situation awareness.** Endsley (1995) defines situation awareness as perception of the elements in the environment, comprehension of their meaning, and projection of their future state. Endsley and Kiris (1995) then demonstrated the automation consequence experimentally: operators of a fully automated system suffered measurably worse post-failure decision times than those at *intermediate* levels of automation, attributed to loss of SA under passive information processing. When automation disconnects, the human is thrust into control with *cold context* — unaware of what the system was attempting, why it stopped, or what the state now is.

  This is the strongest empirical warrant in the framework for the rule below: **intermediate automation levels preserved situation awareness where full automation destroyed it.** Stepping down is not a design preference; it is the measured difference between an operator who can recover and one who cannot.

Bainbridge closes with the irony that matters most for deciding where to invest: **"it is the most successful automated systems, with rare need for manual intervention, which may need the greatest investment in human operator training."** The better the automation, the more the residual human role costs to maintain.

#### A necessary correction: degrade the level, not the performance

The term *graceful degradation* is used loosely in automation writing, and Bainbridge explicitly attacks it: "'Graceful degradation' of performance is quoted in 'Fitts Lists' of man-computer qualities as an advantage of man over machine. This is **not** an aspect of human performance to be aimed for in computers, as it can raise problems with monitoring for failure; **automatic systems should fail obviously.**" Her reason is concrete: "automatic control can 'camouflage' system failure by controlling against the variable changes, so that trends do not become apparent until they are beyond control."

This is a real constraint on the Option principle, and it resolves into a distinction the framework must make explicit:

- **Degrading performance quietly is forbidden.** A system that absorbs a developing fault by working harder, while its outputs still look nominal, is hiding the failure until it is unrecoverable. Bainbridge is right, and this is the more common failure in software automation, where retries and fallbacks routinely mask a deteriorating dependency.
- **Degrading the level of automation explicitly is required.** Endsley and Kiris's result stands: handing control to a human who has been out of the loop produces worse outcomes than keeping them at an intermediate level. Stepping down is correct — provided the step-down is *announced*, not silent.

**The two combine into one rule: fail obviously, hand over gradually.** The transition must be loud and the handover must be warm. An automation that degrades quietly violates Bainbridge; one that disconnects abruptly violates Endsley and Kiris. Most real systems manage to do both.

The design consequence is therefore precise: **an automation that throws an error and abdicates has not implemented Option; it has implemented abandonment.** Compliant Option design requires (a) stepping down through automation levels rather than dropping out, and making each step visible rather than silent, (b) handing over a full **reasoning trace** — what was attempted, what state obtains, what specifically is required — so the receiving operator inherits situation awareness rather than a stack trace, and (c) keeping skills warm. Bainbridge's own prescription for (c) is direct: "allow the operator to use hands-on control for a short period in each shift. If this suggestion is laughable then simulator practice must be provided."

Two further sources broaden the dimension. Process flexibility research (van der Aalst et al., 2009) shows that real processes require *several distinct* flexibility mechanisms — by design, by deviation, by underspecification, by change — rather than a single notion of alternate path; CMMN exists as a standard precisely because much work is case-based and cannot be pre-sequenced at all. And the NIST AI Risk Management Framework (NIST, 2023) adds, for AI-operated processes, that response, recovery, and the ability to *disengage or deactivate* a system behaving inconsistently with its intended use are required controls, not optional features.

### Across the three cases

**L — NDA.** *Variant:* if the counterparty insists on their paper, switch to the reverse-review playbook rather than failing. *Exception:* an unrecognised clause type suspends automated redlining and routes to counsel with the extracted text, the playbook rule it could not match, and the negotiation history. *Recovery:* if e-signature fails, fall back to a manual countersignature path; if the counterparty is added to the sanctions list mid-negotiation, hard stop and notify compliance. *Anti-irony measure:* counsel reviews a sampled 5% of fully automated NDAs to retain feel for playbook drift.

**I — Reactor.** *Variant:* if the primary coolant loop degrades, transfer to the secondary at reduced ramp rate. *Exception:* on thermocouple disagreement, drop from closed-loop control to operator-supervised manual with both readings displayed — a step down, not a disconnect. *Recovery:* an unrecoverable excursion triggers a controlled abort and vent, a designed safe state rather than a halt. *Anti-irony measure:* periodic simulator runs and scheduled manual-mode operation, standard practice in process industries for exactly Bainbridge's reasons.

**D — Support.** *Variant:* if the knowledge base lacks an answer, search resolved tickets before escalating. *Exception:* on low classification confidence, the agent does not guess — it asks one clarifying question, then escalates. *Recovery:* on backend API failure, acknowledge to the customer with a realistic ETA rather than failing silently; on detection of anomalous behaviour, disengage the agent for that queue entirely (NIST, 2023). *Handover quality:* escalation carries the agent's interpretation, actions taken, tools called, and the specific blocking condition — not "escalated to human."

### Failure mode if ignored

**Brittleness compounding into catastrophe.** The system runs efficiently until first contact with an unmodelled disturbance, then fails abruptly onto an operator who has neither the practice nor the situation awareness to recover. The failure is not the exception; it is the handover.

### Review questions

1. What are the legitimate alternative routes to this objective, and are they designed or improvised?
2. For each dependency in Order, what happens if it is not satisfied?
3. Does the system step down through automation levels, or does it drop out?
4. What exactly does the receiving operator see at the moment of handover — and could they act on it without further investigation?
5. What is the safe stop state, and is stopping actually available as an outcome?
6. Can this system be disengaged, and by whom, without a deployment?
7. If this automation runs flawlessly for a year, will anyone still be able to do it manually?

---

## 6. Observation — What evidence does execution produce, and how does that evidence change the process?

> **Observation is the requirement that a process render itself legible: emitting evidence sufficient to determine what happened, judge it against the Objective, and revise the process itself.**

### The Rule

Observation has three obligations, and most implementations satisfy only the first. **Record**: emit semantically meaningful, complete, trustworthy event data. **Judge**: compare actual behaviour against the intended model and against the Objective. **Revise**: feed the resulting findings into a loop that actually changes the specification. Logging without conformance checking is passive. Conformance checking without a revision loop is theatre.

### Grounding

The **control-theoretic form** of Observation is the feedback controller. A PID controller computes the error between setpoint and measured variable and corrects on three distinct time horizons (Åström & Murray, 2008), which translate directly into process terms:

- **Proportional** — response to the *current* magnitude of deviation. Organisationally: immediate intervention when a metric breaches threshold. Too much gain oscillates; too little is unresponsive.
- **Integral** — response to *accumulated* past error. This term exists because proportional control leaves a residual steady-state error. Organisationally: the chronic friction that no single incident justifies fixing but that costs enormously across thousands of iterations. Correcting the integral term means structural redesign, not intervention.
- **Derivative** — response to the *rate of change* of error, anticipating future deviation. Organisationally: leading indicators and predictive intervention before the process fails.

Most organisational monitoring is purely proportional. The integral and derivative terms name the two most commonly missing feedback capabilities.

The **evidence form** of Observation is best specified by the Process Mining Manifesto (van der Aalst et al., 2011), whose guiding principles are unusually well suited to this dimension: event data should be treated as **first-class citizens**, not incidental exhaust; log extraction should be **driven by questions**, not by what happened to be instrumented; events should be **relatable to model elements**, enabling conformance checking rather than mere counting; models are **purposeful abstractions**, so no single model serves all questions; and process mining should be a **continuous** activity, not a one-off project. Observation therefore imposes a data-quality obligation: an event log that cannot be tied to model elements cannot support diagnosis, only description.

The **organisational form** of Observation is environmental scanning, and it is fractal — the same requirement applies to a script, a department, and a corporation. Observation must serve three distinct functions, of which most implementations supply only the second: dampening oscillation between adjacent processes; monitoring and optimising current operations; and scanning the *external environment* for changes that invalidate the process's premises. A process that monitors only its own internal metrics is blind in exactly the dimension that determines whether it should continue to exist.

Finally, Observation is where the framework closes: its output is an input to Objective. This is what makes Five O a loop rather than a checklist.

### Across the three cases

**L — NDA.** *Record:* cycle time by stage; which playbook clauses were most often challenged; deviation approvals and by whom; escalation reasons. *Judge:* conformance of actual negotiation paths against the intended playbook — a divergence that recurs is not non-compliance, it is a signal that the playbook is wrong. *Revise:* quarterly playbook amendment driven by the top challenged clauses; S4 scanning for regulatory changes that invalidate standard terms.

**I — Reactor.** *Record:* full process historian trace at control-loop resolution. *Judge:* proportional (excursion alarms), integral (slow drift in achieved hold temperature across batches indicating fouling or sensor degradation), derivative (rate-of-rise trending toward interlock). *Revise:* controller retuning, maintenance scheduling, and periodic re-examination of whether the setpoint itself is still optimal for the product.

**D — Support.** *Record:* per-ticket trace of intent classification, confidence, tools called, actions taken, escalation reason, and outcome. *Judge:* conformance of actual agent trajectories against intended flows; deflection rate against the CSAT floor named in the Objective; escalation-reason clustering. *Revise:* the highest-frequency escalation reason is the next thing to build; a rising rate of a previously-rare failure mode is a derivative signal; a shift in inbound topic mix is an S4 signal that the product changed.

### Failure mode if ignored

**Stagnation and undetected drift.** The process suffers chronic steady-state error nobody attributes to it, and continues executing correctly against premises that have quietly become false. Because open-loop processes fail silently rather than loudly, this failure mode is typically discovered by its consequences.

### Review questions

1. Could you reconstruct what happened in a single execution six months later, from the evidence alone?
2. Can events be tied to specific elements of the process model, or only counted?
3. Which metrics correspond to proportional, integral, and derivative response — and are all three present?
4. What is the mechanism by which an observation changes the specification, and what is its lead time?
5. Who reads this, and what are they authorised to change?
6. What would tell you that this process should no longer exist?

---

## 7. Cross-cutting invariants

The five principles are dimensions of a process. Two further conditions are not dimensions but **invariants**: they must be specified *within every one of the five*, and a Five O specification is incomplete without them. Making them cross-cutting rather than a sixth O is deliberate — they are not a stage of the process, they are properties every stage must possess.

### Invariant I — Ownership and Authority

> **Every O must name who owns it and under what authority it acts.**

The governance literature is unambiguous that specification completeness without institutional accountability does not survive contact with an organisation. Spanyi (2015) makes the operational case that consistent and sustainable execution requires defined ownership and active management practice, not merely a documented process. The NIST AI RMF (2023) makes this a formal requirement for AI-operated processes: documented roles and responsibilities, executive accountability, feedback channels from affected parties, and the authority to disengage a misbehaving system.

Concretely, this means every O carries an owner and an authority statement: who may change the **Objective**; who authorises an **Occurrence**; who owns each node and each hand-off in the **Order**; who is on the receiving end of each **Option** escalation, and are they staffed at that hour; who reads the **Observation** output and what are they empowered to change.

The most common real-world failure is an escalation path terminating in a queue nobody owns.

### Invariant II — Objects and Resources

> **Every O must name the objects it acts upon and the resources it consumes.**

A process specification that does not identify its objects is not executable; one that does not identify its resources is not schedulable. This is what ISO 9001:2015 means by determining the inputs required and outputs expected of each process, and what the WfMC Workflow Reference Model (Hollingsworth, 1995) captures by treating human and IT resource assignment as a first-class element of process definition alongside control flow.

Concretely: what object does the **Objective** transform, and what state must it reach; what data and resources must be present for **Occurrence**; what resources are contended in the **Order**'s sharing dependencies; what resources does an **Option** path require — and are they available precisely when the primary path has failed, which is often when they are not; what objects and events does **Observation** record, with what identity and what semantics.

The most common real-world failure here is a fallback path that depends on the same resource whose failure triggered it.

---

## 8. Applying the framework

The Five O framework is best used as a **front-end completeness test and design-review scaffold**, not as a replacement for domain methods. In practice:

1. **Interrogate the Objective before anything else** — including whether the process should exist. This is the Hammer step, and skipping it makes everything downstream efficient waste.
2. **Specify Occurrence as trigger + readiness + authorisation + window**, and check each against STPA's four unsafe-control-action classes.
3. **Model Order with the lightest notation that preserves the real dependencies** — Cherns's minimal critical specification: precise about *what* must be done, rarely about *how*. A dependency graph on paper is often enough; reach for BPMN when flow needs to be shared, DMN when decisions should be separated from flow, CMMN when work is genuinely case-based, and Petri-net soundness analysis when concurrency is complex enough that informal reasoning is unreliable.
4. **Design Options for deviation classes, not for specific bugs** — variant, exception, recovery — and design the handover, not just the trigger for it.
5. **Define Observation as an evidence model** before implementation, driven by the questions you will need to answer, rather than instrumenting whatever is convenient afterward.
6. **Sweep the two invariants across all five**, naming an owner and the objects/resources for each.
7. **Pilot, measure, check conformance, and return to step 1.**

### Metrics by dimension

Automation programmes routinely report a single figure — hours saved — which is uninformative about whether the automation is sound. A layered metric set follows directly from the framework:

| Dimension | What to measure |
|---|---|
| Objective | Outcome achievement; constraint violations; realised trade-off position against declared floors |
| Occurrence | Trigger precision and recall; false starts; readiness failures; authorisation failures; timing violations |
| Order | Cycle time and waiting time; rework loops; synchronisation failures; conformance to intended dependency logic |
| Option | Exception frequency by class; recovery success rate; escalation rate; handover quality; time-to-human-competence after handover |
| Observation | Event completeness and semantic quality; conformance-check coverage; time from signal to specification change |
| Invariants | Unowned escalation paths; unstaffed authority; resource contention incidents; fallback paths sharing a failure domain with the primary |

### What the framework does not give you

Stated plainly, because a framework that does not name its limits invites misuse:

- **It does not tell you whether the process should exist.** It only forces the question (Hammer, 1990).
- **It does not itself tell you how much formalisation is appropriate** — but the socio-technical literature does, and the framework should defer to it. Cherns's (1976) second principle, **minimal critical specification**, states the rule in two halves: "no more should be specified than is absolutely essential," and, positively, "identify what is essential." His operational test is the one to apply to a Five O specification: *"While it may be necessary to be quite precise about what has to be done, it is rarely necessary to be precise about how it is to be done."* He adds the diagnosis that matters — "it is a mistake to specify more than is needed because by doing so options are closed that could be kept open. This premature closing of options is a pervasive fault in design," including because over-specification "helps designers to get their own way."

  Applied here: **Objective, Occurrence and Option should be specified tightly; Order should be specified only to the depth of its real dependencies.** A dependency graph is critical specification; a step-by-step script usually is not.
- **It is not a notation.** It tells you what must be specified, not how to express it.
- **It does not resolve the socio-technical question.** Trist and Bamforth (1951) documented what mechanisation did to the social structure of coal-getting: introducing machines to the coal face "caused the appearance of a new order… bringing fractionation of tasks, extension of sequence, role and shift segregation, small group disorganization and inter-group dependence." Their conclusion is the founding statement of socio-technical design — that a method must be reworked "so that a social as well as a technological whole can come into existence," by "restoring responsible autonomy to primary groups" and giving each "a satisfying sub-whole as its work task." Cherns (1976) turned this into nine design principles — compatibility, minimal critical specification, the socio-technical criterion, multifunctionality, boundary location, information flow, support congruence, design and human values, and incompletion — and Clegg (2000) extended them. Three bear directly on this framework and are used above: minimal critical specification (§8), the socio-technical criterion (below), and information flow. A fourth, **support congruence** — "systems of social support should be designed so as to reinforce the behaviors that the organization structure is designed to elicit" — the Five Os do not address at all. A process can be perfectly specified and still be defeated by an incentive that rewards the opposite behaviour.

  Cherns's **socio-technical criterion** also sharpens both Option and Observation: "variances, if they cannot be eliminated, must be controlled as near to their point of origin as possible," because when correction happens in a separate department long after the event, "the correction of the variance becomes a long loop, which is a poor design for learning." And his **information flow** principle states the rule the Observation dimension needs: information should go "in the first place to the point where action on the basis of it will be needed" — not upward by default.

  A Five O specification can therefore be logically complete and still distribute discretion, visibility, and accountability in a way that people will not sustain.

  One finding of theirs bears directly on the Ownership invariant. At the longwall face, dependencies ran one way and no group owned the seams between shifts; the result was not resolution but **mutual scapegoating** — "as the fillers do not exist as a responsible whole; they, as a group, are not there to take the blame, and the individual filler can always exempt himself… nothing is resolved and no one feels guilty." An unowned dependency does not stay neutral. It becomes a place where blame circulates and no correction occurs. That was observed in 1951 in a coal mine, and it is what an escalation path terminating in an unowned queue produces today.
- **It does not substitute for domain rigor.** Where a dimension is safety-critical, use the discipline built for it.

---

## 9. Summary

| Principle | Question | Core theory | Failure mode if ignored |
|---|---|---|---|
| **Objective** | What result counts as success, within what boundaries? | Control-theoretic setpoint (Åström & Murray); ISO 9001 process approach; BPR (Hammer); redesign trade-offs (Reijers & Limam Mansar) | Misaligned automation — efficient execution of the wrong goal |
| **Occurrence** | Under what conditions may execution begin or continue? | Open vs. closed loop; BPMN start events; CMMN sentries; STPA unsafe control actions (Leveson); Law of Requisite Variety (Ashby) | Blind or brittle activation — acting on incomplete state, at the wrong time, or not at all |
| **Order** | What must be true before what? | Coordination theory (Malone & Crowston; Crowston); Petri nets and workflow patterns (van der Aalst); function allocation (Sheridan & Verplank; Parasuraman et al.) | Coordination failure — the process breaks at the joints, not the steps |
| **Option** | What happens when reality diverges? | Requisite variety (Ashby); Ironies of Automation (Bainbridge); situation awareness (Endsley); process flexibility; AI risk management (NIST) | Brittleness and catastrophic handover — the operator inherits a crisis with cold context |
| **Observation** | What evidence does execution produce, and how does it change the process? | PID feedback (Åström & Murray); Process Mining Manifesto (van der Aalst et al.); environmental scanning | Stagnation and silent drift — correct execution against premises that became false |
| *Invariant:* **Ownership & Authority** | Who owns this, and under what authority? | BPM governance (Spanyi); NIST AI RMF | Specification without accountability; escalation into an unowned queue |
| *Invariant:* **Objects & Resources** | What does it act on, and what does it consume? | ISO 9001 inputs/outputs; WfMC Workflow Reference Model (Hollingsworth) | Unschedulable processes; fallbacks sharing a failure domain with the primary path |

**The Five O Principles describe the minimum complete specification of an automatable process: why it should exist, when it is permitted to act, how its dependencies govern action, how it responds when reality diverges from the nominal path, and how it observes itself well enough to improve. Their adequacy in practice depends on two cross-cutting conditions: clear ownership and explicit object and resource semantics.**

---

## References

🔓 marks a freely accessible full text.

**Primary literature**

Ashby, W. R. (1956). *An Introduction to Cybernetics*. London: Chapman & Hall. — 🔓 [Full text (PDF)](https://ashby.info/Ashby-Introduction-to-Cybernetics.pdf)

Åström, K. J., & Murray, R. M. (2008). *Feedback Systems: An Introduction for Scientists and Engineers*. Princeton, NJ: Princeton University Press. — 🔓 [Full text (PDF)](https://www.cds.caltech.edu/~murray/books/AM08/pdf/fbs-public_24Jul2020.pdf)

Bainbridge, L. (1983). Ironies of automation. *Automatica*, 19(6), 775–779. — [ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/0005109883900468)

Cherns, A. (1976). The principles of sociotechnical design. *Human Relations*, 29(8), 783–792. — [SAGE](https://journals.sagepub.com/doi/10.1177/001872677602900806)

Clegg, C. W. (2000). Sociotechnical principles for system design. *Applied Ergonomics*, 31(5), 463–477. — [Semantic Scholar](https://www.semanticscholar.org/paper/Sociotechnical-principles-for-system-design.-Clegg/917ee2db4ff4c5664194b1f0f92b3da18244216e)

Conant, R. C., & Ashby, W. R. (1970). Every good regulator of a system must be a model of that system. *International Journal of Systems Science*, 1(2), 89–97. — [Taylor & Francis](https://www.tandfonline.com/doi/abs/10.1080/00207727008920220)

Crowston, K. (1997). A coordination theory approach to organizational process design. *Organization Science*, 8(2), 157–175. — [INFORMS](https://pubsonline.informs.org/doi/10.1287/orsc.8.2.157) · 🔓 [Author copy (PDF)](https://crowston.syr.edu/sites/crowston.syr.edu/files/orgsci97.pdf)

Endsley, M. R. (1995). Toward a theory of situation awareness in dynamic systems. *Human Factors*, 37(1), 32–64. — [SAGE](https://journals.sagepub.com/doi/10.1518/001872095779049543)

Endsley, M. R., & Kiris, E. O. (1995). The out-of-the-loop performance problem and level of control in automation. *Human Factors*, 37(2), 381–394. — [SAGE](https://journals.sagepub.com/doi/10.1518/001872095779064555)

Hammer, M. (1990). Reengineering work: Don't automate, obliterate. *Harvard Business Review*, 68(4), 104–112. — [HBR](https://hbr.org/1990/07/reengineering-work-dont-automate-obliterate) · 🔓 [Copy (PDF)](https://folk.idi.ntnu.no/thomasos/paper/hammer_reengineering.pdf)

Hollingsworth, D. (1995). *The Workflow Reference Model*. Workflow Management Coalition, Document TC00-1003. — 🔓 [WfMC (PDF)](https://wfmc.org/wp-content/uploads/2022/09/tc003v11.pdf)

Leveson, N. G. (2011). *Engineering a Safer World: Systems Thinking Applied to Safety*. Cambridge, MA: MIT Press. — 🔓 [MIT Press, open access](https://direct.mit.edu/books/oa-monograph/2908/Engineering-a-Safer-WorldSystems-Thinking-Applied)

Leveson, N. G., & Thomas, J. P. (2018). *STPA Handbook*. MIT Partnership for Systems Approaches to Safety and Security. — 🔓 [MIT PSAS (PDF)](https://psas.scripts.mit.edu/home/get_file.php?name=STPA_handbook.pdf)

Malone, T. W., & Crowston, K. (1994). The interdisciplinary study of coordination. *ACM Computing Surveys*, 26(1), 87–119. — [ACM](https://dl.acm.org/doi/10.1145/174666.174668) · 🔓 [PDF](https://dl.acm.org/doi/pdf/10.1145/174666.174668)

Malone, T. W., Crowston, K., Lee, J., Pentland, B., Dellarocas, C., Wyner, G., et al. (1999). Tools for inventing organizations: Toward a handbook of organizational processes. *Management Science*, 45(3), 425–443. — [INFORMS](https://pubsonline.informs.org/doi/10.1287/mnsc.45.3.425) · 🔓 [Author copy (PDF)](https://surface.syr.edu/cgi/viewcontent.cgi?article=1121&context=istpub) *(source of the flow / sharing / fit dependency classification)*

Parasuraman, R., Sheridan, T. B., & Wickens, C. D. (2000). A model for types and levels of human interaction with automation. *IEEE Transactions on Systems, Man, and Cybernetics — Part A*, 30(3), 286–297. — [IEEE / ACM DL](https://dl.acm.org/doi/10.1109/3468.844354)

Pasquinelli, M. (2024). Theories of automation from the industrial factory to AI platforms. *Tecnoscienza*. — 🔓 [Full text (PDF)](https://tecnoscienza.unibo.it/article/download/20010/18150/81313)

Reijers, H. A., & Limam Mansar, S. (2005). Best practices in business process redesign: An overview and qualitative evaluation of successful redesign heuristics. *Omega*, 33(4), 283–306. — [ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S0305048304000854) · 🔓 [Author copy (PDF)](https://hreijers.win.tue.nl/H.A.%20Reijers%20Bestanden/BPRpractices.pdf)

Rezgui, A., Crowston, K., & Jullien, N. (2018). Stigmergic coordination in Wikipedia. *Proceedings of the 14th International Symposium on Open Collaboration (OpenSym '18)*. New York: ACM. — [ACM](https://dl.acm.org/doi/10.1145/3233391.3233543)

Russell, N., van der Aalst, W. M. P., & ter Hofstede, A. H. M. (2016). *Workflow Patterns: The Definitive Guide*. Cambridge, MA: MIT Press. — 🔓 [Pattern catalogue](https://www.workflowpatterns.com/)

Sheridan, T. B., & Verplank, W. L. (1978). *Human and Computer Control of Undersea Teleoperators*. Cambridge, MA: MIT Man-Machine Systems Laboratory. — [Semantic Scholar](https://www.semanticscholar.org/paper/Human-and-Computer-Control-of-Undersea-Sheridan-Verplank/d48b94e6af5093e7cc41e20fa6aca4f3a2d860bb)

Smith, A. (1776). *An Inquiry into the Nature and Causes of the Wealth of Nations*. London: W. Strahan and T. Cadell. — 🔓 [Project Gutenberg](https://www.gutenberg.org/ebooks/3300)

Spanyi, A. (2015). The governance of business process management. In *Handbook on Business Process Management 2* (2nd ed.). Berlin: Springer. — 🔓 [Chapter (PDF)](https://spanyi.com/wp-content/uploads/2015/11/BPM-Governance-Chap_11.pdf)

Trist, E. L., & Bamforth, K. W. (1951). Some social and psychological consequences of the longwall method of coal-getting. *Human Relations*, 4(1), 3–38. — [SAGE](https://journals.sagepub.com/doi/10.1177/001872675100400101)

van der Aalst, W. M. P. (1998). The application of Petri nets to workflow management. *Journal of Circuits, Systems and Computers*, 8(1), 21–66. — 🔓 [PDF](https://users.cs.northwestern.edu/~robby/courses/395-495-2017-winter/Van%20Der%20Aalst%201998%20The%20Application%20of%20Petri%20Nets%20to%20Workflow%20Management.pdf)

van der Aalst, W. M. P., ter Hofstede, A. H. M., Kiepuszewski, B., & Barros, A. P. (2003). Workflow patterns. *Distributed and Parallel Databases*, 14(1), 5–51. — 🔓 [workflowpatterns.com](https://www.workflowpatterns.com/documentation/documents/BPM-06-22.pdf)

van der Aalst, W. M. P., et al. (2009). Process flexibility: A survey of contemporary approaches. In *Advances in Enterprise Engineering I*. Berlin: Springer. — 🔓 [Author copy (PDF)](https://www.vdaalst.com/publications/p460.pdf)

van der Aalst, W. M. P., et al. (2011). Process mining manifesto. In *BPM 2011 Workshops*, LNBIP 99. Berlin: Springer. — 🔓 [IEEE Task Force on Process Mining (PDF)](https://www.tf-pm.org/upload/1580737614108.pdf)

**Standards and frameworks**

International Organization for Standardization (2015). *ISO 9001:2015 — Quality management systems — Requirements*, and the accompanying guidance *The Process Approach in ISO 9001:2015*. — 🔓 [Process approach guidance (PDF)](https://www.iso.org/iso/iso9001_2015_process_approach.pdf)

International Organization for Standardization / IEC (2023). *ISO/IEC 42001:2023 — Artificial intelligence management system*. — [ISO standard page](https://www.iso.org/standard/42001) · 🔓 [Plain-language explainer](https://www.iso.org/home/insights-news/resources/iso-42001-explained-what-it-is.html)

National Institute of Standards and Technology (2023). *Artificial Intelligence Risk Management Framework (AI RMF 1.0)*, NIST AI 100-1. — 🔓 [Full text (PDF)](https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf) · [Framework hub](https://www.nist.gov/itl/ai-risk-management-framework)

Object Management Group. *Business Process Model and Notation (BPMN) 2.0* — 🔓 [omg.org](https://www.omg.org/spec/BPMN/2.0.2/About-BPMN); *Decision Model and Notation (DMN)* — 🔓 [omg.org](https://www.omg.org/dmn/); *Case Management Model and Notation (CMMN)* — 🔓 [omg.org](https://www.omg.org/cmmn/).

**Case evidence**

Lacity, M., & Willcocks, L. (2016). Robotic process automation at Telefónica O2. *MIS Quarterly Executive*, 15(1), Article 4. — [AIS eLibrary](https://aisel.aisnet.org/misqe/vol15/iss1/4/) · 🔓 [LSE Research Online (PDF)](https://eprints.lse.ac.uk/64516/1/OUWRPS_15_02_published.pdf) *(Peer-reviewed case; reports annual returns on investment of up to 200% and identifies capability assessment and adoption management — not scripting alone — as the determinants of success.)*

Vendor-published case studies (IBM/FCT, Celonis/TD SYNNEX, Microsoft/EY, UiPath/One NZ) report large improvements in cycle time and automation rate. These are **vendor-reported and not independently verified**, and are cited here only as directional evidence that outcomes correlate with clear objectives, gated triggers, orchestrated dependencies, designed exception handling, and continuous observation — the pattern the framework predicts.

---

*This document synthesises practitioner experience in code-based and AI-enabled business process automation with the established literature of control theory, cybernetics, business process management, workflow formalisation, human factors engineering, and socio-technical systems design. Where the framework's dimensions correspond to established constructs, that correspondence is evidence of soundness rather than a claim of priority.*
