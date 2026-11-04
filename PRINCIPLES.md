# The Five O Principles of Process Specification

*A universal framework for stating how a process operates or is required to operate, independent of the kind of entity performing it.*

---

## Preface: purpose and limits

The Five Os identify five dimensions to consider when specifying a process: **Objective, Occurrence, Order, Option, and Observation**. Two cross-cutting requirements make those dimensions concrete: **ownership and authority**, and **objects and resources**.

The framework supports understanding existing work, designing new work, coordination, delegation, assessment, and revision. Automation is one application. A specification can describe a process performed entirely by people, entirely by AI or machines, or by a combination, using the same core terms.

These are obligations on a **specification**, not instructions for choosing an implementation. Stating a requirement does not establish that any particular operator can satisfy it. An operator-independent specification supports a transition between implementations; it does not guarantee interchangeability. Capabilities, interfaces, authority, resources, and evidence must be assessed for each implementation.

The claim is synthesis and portability, drawing on quality management, control theory, coordination theory, workflow formalisation, human factors, and socio-technical design. These disciplines provide deeper methods where needed. Five O helps identify the questions; it does not replace those methods or claim that five headings prove completeness.

---

## 1. Process, specification, and shared terms

> **A process is a related set of activities through which inputs, resources, and conditions contribute to an outcome, including changing something, maintaining a condition, or preventing an unwanted change.**

A process may be finite, recurring, or continuous. A one-time undertaking may contain a process worth specifying. Boundaries remain essential: state what the specification covers, what it excludes, and how it relates to surrounding work. Continuous processes need operating and suspension conditions even when they have no scheduled completion.

A **process specification** states how a process operates or is required to operate, at a declared scope and level of detail. It is distinct from a single execution and from the implementation used to carry it out.

### Descriptive and prescriptive specifications

- **Descriptive:** records how the process currently operates. Unknowns and observed departures remain visible; missing controls must not be invented to make the description look complete.
- **Prescriptive:** states how the process is required to operate. Requirements must be distinguishable from assumptions, examples, recommendations, and unresolved decisions.

A document may contain both, provided each statement's status is clear. An intended change is not evidence of current practice. An existing practice is not automatically a requirement.

### Roles and assignments

The canonical definitions are in [TERMS.md](./TERMS.md). In brief:

| Term | Responsibility |
|---|---|
| **Operator** | Performs a specified activity, including gathering information, interpreting, deciding, or acting. |
| **Process owner** | Holds responsibility for the process as a whole, with defined authority over requirements, performance, and revision. |
| **Escalation recipient** | Receives a situation that the current operator cannot resolve within its capability or authority. |
| **Role assignment** | Maps a role to the entity filling it: a person, team, organizational unit, machine, software system, or AI agent. |

These roles are distinct even when one entity fills several. An escalation recipient is not necessarily the process owner or a hierarchical superior. It must possess the capability, authority, or resources required for the particular situation. No core role is inherently human.

Functional ownership within the process does not, by itself, settle organizational accountability. The surrounding governance specification identifies who answers for conduct, how authority is granted and limited, and who may change or withdraw it. A particular context may require a human or organizational owner; the universal framework does not prescribe one.

### Coverage and proportionality

| Dimension | What the specification must make explicit |
|---|---|
| **Objective** | Outcomes, boundaries, constraints, trade-offs, and criteria for success or justified termination. |
| **Occurrence** | Conditions for beginning, continuing, suspending, resuming, and ending activity. |
| **Order** | Dependencies, state transitions, coordination, discretion, and completion conditions. |
| **Option** | Permitted alternatives and responses to deviation, unavailable dependencies, and unresolved situations. |
| **Observation** | Evidence, evaluation responsibility, and the route from findings to revision. |

Consider every dimension, but scale detail to purpose, complexity, uncertainty, and consequence. A justified statement of non-applicability is preferable to invented machinery. Continuous trend monitoring may be irrelevant to a short, one-time process; a completion check may be enough. An unspecified exception response is a gap, not an implicit permission to improvise without limits.

Coverage is a review scaffold. It does not prove that requirements are exhaustive, consistent, feasible, correct, or desirable. Domain-specific requirements may be needed within or alongside these dimensions.

### Three running cases

These examples illustrate the same vocabulary across different assignments. They are specification examples, not validated operating procedures.

- **Case M — Manual.** Library loans handled entirely by people using paper records. Roles: lending clerk, lending supervisor, and library services manager.
- **Case A — AI.** Research records assessed and routed entirely by AI agents. Roles: record assessor, specialist assessor, and collection steward. The collection steward holds bounded process ownership; no human approval or human escalation is assumed within this process.
- **Case X — Mixed.** Equipment maintenance coordinated by a monitoring system, technician, and maintenance supervisor.

---

## 2. Objective — Specify outcomes and limits

> **State the intended outcome or maintained condition, its scope, the constraints on legitimate action, permitted trade-offs, and criteria for success or justified termination.**

### Required content

Identify the value or condition sought and its beneficiary; what is included and excluded; what must not happen; which priorities may be traded and within what limits; and how success, partial completion, suspension, or termination is assessed. Keeping a condition stable can be the objective. Producing a new artifact is not required.

For a descriptive specification, distinguish the stated objective from observed incentives and actual outcomes. For a prescriptive specification, resolve conflicts between measures and constraints rather than leaving operators to choose silently.

Ask whether the process should exist before preserving its present shape. Hammer's (1990) redesign argument is relevant here: an inherited procedure can obscure the actual outcome required. Specifying the inherited steps more precisely does not establish their value.

### Grounding

Control theory provides the distinction between a reference condition and measured behavior (Åström & Murray, 2008). Quality management connects intended outputs with context, boundaries, and resources (ISO 9001:2015). Process redesign highlights trade-offs among time, cost, quality, and flexibility (Reijers & Limam Mansar, 2005). These are useful foundations; an organizational objective need not be reducible to a numeric setpoint.

### Across the cases

- **M:** lend an eligible item to an eligible member with a traceable due date. Do not lend reference-only items. Queue speed never overrides eligibility. An unresolved eligibility question may end in a recorded refusal or pending review.
- **A:** produce a source-supported collection of research records. Unsupported claims cannot be marked verified. Coverage may be reduced to preserve evidential quality. Unresolved records remain explicitly pending or excluded; completion does not require every record to be accepted.
- **X:** maintain equipment within its approved operating condition. Availability may be reduced to meet inspection requirements. Equipment cannot be returned to service without the required release.

### Failure if omitted

**Unclear or conflicting success.** Operators pursue different outcomes, optimize a measure at the expense of a constraint, or continue when termination is justified.

### Review questions

1. What outcome or maintained condition is sought, for whom, and how can it be assessed?
2. What is outside the boundary? What must never happen?
3. Which trade-offs are allowed, with what limits and precedence?
4. What counts as success, partial completion, suspension, or justified termination?
5. Are we specifying needed work or preserving an inherited procedure without examining it?

---

## 3. Occurrence — Specify conditions for activity

> **State the events, states, prerequisites, authority, and timing conditions under which activity begins, continues, pauses, resumes, or ends.**

### Required content

Distinguish a **trigger** proposing activity, **readiness** making it possible and appropriate, **authorization** making it legitimate, and a **timing window** making it timely. State which conditions must remain true and what changes require suspension or reassessment. If a condition is not applicable, explain why.

Identify situations requiring different treatment and where they are distinguished. Classification may belong after admission in Order; the initial trigger does not have to classify every case. What matters is that a required distinction is available before the decision depending on it.

### Grounding

BPMN start events and CMMN sentries distinguish events from enabling conditions. Safety analysis also separates action not provided when needed, action provided in an unsafe context, wrong timing or ordering, and inappropriate duration (Leveson, 2011; Leveson & Thomas, 2018).

Ashby's (1956) requisite variety and Conant and Ashby's (1970) regulator argument motivate checking whether available distinctions and responses fit relevant environmental variation. They do not establish a numerical failure rate from a count of case types alone.

### Across the cases

- **M:** a member requests a loan; the clerk has the item and current paper membership record; the lending rules authorize the loan; the desk is open. Pause if eligibility cannot be established.
- **A:** a record arrives in the intake collection; its source and provenance are accessible; the assessor has permission to update the collection; processing occurs before the collection deadline. Suspend affected work if source access or required authority is lost.
- **X:** a service interval or condition alert initiates assessment; equipment identity and condition history are available; isolation authority is confirmed. Work resumes only when the specified access and safety conditions hold.

### Failure if omitted

**Inappropriate activation or continuation.** Work starts without prerequisites, continues after conditions change, occurs too early or too late, or fails to start when needed.

### Review questions

1. What proposes activity, and what additional conditions permit it?
2. Which conditions must remain true, and when are they reassessed?
3. What permits suspension, resumption, and ending?
4. Where are materially different cases distinguished before action depends on that distinction?
5. What is the response to missing information or an uncertain condition?

---

## 4. Order — Specify dependencies and decision rights

> **State what depends on what, which state transitions are permitted, how concurrent work coordinates, and which roles may perform and decide each part.**

### Required content

Specify essential dependencies without prescribing unnecessary method. A sequence is appropriate where order matters; permitted flexibility should remain explicit where several methods satisfy the same requirements.

| Dependency | Required specification |
|---|---|
| **Flow** — one activity needs another's output | Required input state, availability, and acceptance conditions. |
| **Sharing** — activities need a limited resource | Allocation, priority, or contention resolution. |
| **Fit** — independently produced parts must compose | Interfaces, compatibility checks, and responsibility for reconciliation. |

Identify permitted concurrency, synchronization, state changes, completion conditions, and responsibility at handovers. For relevant activities, distinguish who gathers information, interprets it, decides, and acts. Assign roles and limits of discretion; do not assume any of these functions belongs to a human or machine.

### Grounding

Malone and Crowston (1994) and Crowston (1997) treat coordination as management of dependencies. Workflow theory supplies constructs for parallel work, synchronization, cancellation, and termination (van der Aalst, 1998; van der Aalst et al., 2003; Russell et al., 2016). These provide stronger checks where informal dependency descriptions are inadequate.

Cherns's (1976) minimal critical specification supports precision about essential requirements while retaining freedom over method. This is not a prohibition on detailed procedures: a method belongs in the specification when it is itself an essential requirement. Coordination can also occur through shared work artifacts rather than direct messages (Rezgui, Crowston & Jullien, 2018).

### Across the cases

- **M:** eligibility is confirmed before a loan is authorized; the paper loan record is completed before the item leaves the desk. Clerks share the register under a stated queue rule. The lending supervisor decides disputed eligibility.
- **A:** provenance review precedes acceptance; independent records may be assessed concurrently; synthesis waits for accepted records. The specialist assessor may resolve methodological ambiguity, but only the collection steward may authorize changes within the collection policy's stated limits.
- **X:** isolation precedes inspection; independent checks may run concurrently; release waits for all required results. The technician supplies findings and the maintenance supervisor authorizes return to service.

### Failure if omitted

**Coordination failure.** Work uses stale or incomplete inputs, competes for resources without resolution, produces incompatible parts, or leaves responsibility unclear at a boundary.

### Review questions

1. What truly depends on what? What may proceed concurrently?
2. Which states and transitions are allowed, including cancellation or pending work?
3. What makes an output acceptable to its next consumer?
4. Which roles gather, interpret, decide, and act, within what limits?
5. Who resolves contention, conflicting results, or an incomplete handover?

---

## 5. Option — Specify alternatives and unresolved situations

> **State permitted alternative routes and responses to deviations, unavailable dependencies, and situations beyond an operator's capability or authority.**

### Required content

Specify **variants** for legitimate alternative routes, **exceptions** for departures from assumptions, and **recovery** to an acceptable state. Define the applicable response when no specified route succeeds: pending work, transfer, controlled suspension, or safe termination. An abrupt halt is not always safe; a continuous process may require an active transition to a maintained safe condition.

For each alternative, identify dependencies and shared causes of failure. A route needing an unavailable resource is not a usable fallback for that failure. Do not assume that doing nothing is dependency-free or safe.

Specify which deviations, retries, and substitutions must be recorded or communicated, to which role, and when. Visibility should support decisions rather than indiscriminate notification.

### Escalation and handover contract

Every escalation specifies:

1. The condition exceeding the current operator's capability or authority.
2. The **escalation recipient**, its required capability and authority, and its availability.
3. The information and state transferred: intended outcome, evidence, actions taken, current condition, and decision or action required.
4. How receipt and responsibility are confirmed, within what time or condition limit.
5. The response if the recipient is unavailable, refuses, cannot resolve the situation, or fails to acknowledge.

The recipient may be an AI agent, a machine supervisor, a specialist team, or a person. The process owner receives an escalation only when assigned that role for the relevant situation. A different recipient with the same unresolved limitations does not establish a useful alternative. Escalation paths must not create indefinite transfer loops.

Required capabilities must remain available for exceptional as well as routine activity. State how that availability is checked where it matters. Training, simulation, capability checks, and resource reservations are possible implementations, not universal prescriptions.

### Grounding

Process flexibility research distinguishes several ways to accommodate variation rather than a single fallback mechanism (van der Aalst et al., 2009). Ashby's (1956) variety argument motivates an explicit response to situations beyond the defined repertoire. Human factors research supplies important additional requirements when a handover involves people; those requirements are discussed as an application in §10 rather than imposed on every process.

### Across the cases

- **M:** a clerk passes disputed eligibility to the lending supervisor with the membership record and reason for uncertainty. If no supervisor is available before closing, record the request as pending and retain the item; do not issue the loan on an assumption.
- **A:** an assessor transfers methodological ambiguity to the specialist assessor with source spans and checks already performed. Receipt must be acknowledged within the processing window. If unresolved by the deadline, retain the record as pending and exclude it from the accepted collection. Policy questions go separately to the collection steward within its bounded authority.
- **X:** unavailable equipment access leads to rescheduling only if continued operation is permitted. Otherwise the designated operator maintains the specified safe condition. A handover carries isolation status and incomplete checks; it does not silently release equipment.

### Failure if omitted

**Unresolved deviation or abandoned responsibility.** Work proceeds by unsupported improvisation, transfers into an unowned queue, cycles between recipients, or stops in an unacceptable state.

### Review questions

1. What alternatives are permitted, and are their dependencies available in the relevant failure?
2. What is the acceptable state while a situation remains unresolved?
3. Does each escalation have a capable, authorized, available recipient and a bounded response to non-resolution?
4. What evidence and responsibility move with a handover?
5. How are material deviations made visible without obscuring important signals?

---

## 6. Observation — Specify evidence, evaluation, and revision

> **State what evidence is needed to assess activity and outcomes, who evaluates it, and how findings can lead to changes in the process or its specification.**

### Required content

Observation has three duties: **record** the evidence required for the declared purpose; **judge** it against requirements and intended outcomes; and **revise** through an identified authority and change route when warranted. Findings may justify retaining the current requirements. Observation does not authorize an operator to change them on its own.

Evidence may be a paper record, inspection, measurement, acknowledgment, sample, or event history. State its meaning, relationship to the activity, quality requirements, accessibility, and retention where relevant. Choose evidence from the questions to be answered, rather than requiring a particular logging technology.

For recurring or continuous work, consider immediate deviations, accumulated friction, and trends. For finite work, completion evidence and a closeout review may be sufficient. State why an omitted horizon is not applicable. Specify how changes outside the process that invalidate its assumptions are recognized where that is relevant.

### Grounding

The Process Mining Manifesto emphasizes purposeful models and evidence related to process elements (van der Aalst et al., 2011). Its event-log methods are one implementation of this broader evidence requirement. Control theory provides useful distinctions between current, accumulated, and changing error (Åström & Murray, 2008); these are an analogy for review horizons, not a requirement to implement a PID controller in every process.

### Across the cases

- **M:** paper records identify the item, member, due date, clerk, and exception decision. The library services manager reviews unresolved requests weekly and may revise lending procedure within policy limits.
- **A:** provenance, evidence spans, decisions, transfers, and unresolved reasons remain associated with each record. The collection steward compares results with the declared evidence criteria at closeout and may revise assessment rules only within its assigned authority. A short, one-time collection need not have continuous trend monitoring.
- **X:** inspection findings, release decisions, and condition history support both individual release checks and trend review. The process owner authorizes maintenance-specification changes through the defined approval route.

### Failure if omitted

**Unassessable behavior or undetected drift.** Outcomes cannot be checked, deviations cannot be reconstructed at the required level, or findings have no route to a decision about revision.

### Review questions

1. What questions must the evidence answer, and at what level of reconstruction?
2. Who evaluates it, when, and with what authority to respond?
3. Which review horizons apply to this process, and why?
4. What findings require reassessment of the objective or assumptions?
5. How is a revision authorized, identified, and communicated to affected roles?

---

## 7. Cross-cutting requirements

### Ownership and authority

Within every O, identify responsibility and decision rights. A process owner coordinates responsibility for the whole; activity operators and escalation recipients retain their explicitly assigned duties. Role assignments include the capabilities, permissions, resources, and availability required to fulfil them. The assignment must be assessable, not merely a name in a box.

Spanyi (2015) emphasizes ownership and active management. Trist and Bamforth (1951), Cherns (1976), and Clegg (2000) explain why relationships among work, discretion, information, and responsibility matter. These organizational findings are especially relevant when people fill roles; they do not imply that the abstract roles must be human.

### Objects and resources

Within every O, identify what is acted on, the states that matter, and the resources consumed or required. Include identity and input/output semantics, resource contention, and dependencies shared by alternatives. A process may transform information or maintain a condition rather than produce a physical item.

ISO 9001:2015 and the WfMC Workflow Reference Model (Hollingsworth, 1995) provide related treatments of inputs, outputs, resources, and assignments. Resource availability is a condition to establish, not something a specification guarantees by naming it.

---

## 8. Qualities of a good specification

The Five Os identify topics. The following qualities apply across all of them:

1. **Declared status.** Separate observed practice, requirements, assumptions, recommendations, examples, and unresolved decisions. Identify scope and the applicable version or effective period.
2. **Consistent meaning.** Define important terms, units, identities, and states. Resolve conflicting rules or specify precedence. Check that metrics do not reward violating constraints.
3. **Assessable requirements.** State what evidence could establish satisfaction or violation. Qualitative review is legitimate when its criteria and reviewing role are explicit; not everything requires a numerical threshold.
4. **Essential detail.** Specify outcomes, constraints, dependencies, and decision rights precisely enough for the purpose. Prescribe method only when it is itself required. Do not infer the need to split a process from word count alone.
5. **Explicit uncertainty.** Keep unknowns visible, identify who can resolve them, and state what activity is blocked meanwhile. Document assumptions and the consequence of their failure.
6. **Composition.** Define interfaces and acceptance conditions between subprocesses. State a rule once at the level responsible for it and reference it elsewhere. Reassess conditions that can change after a handover; a prior check is not an eternal guarantee.
7. **Governed revision.** Identify who may change requirements, within what limits, and how changes reach affected roles. Evidence supporting a change is separate from authority to make it.

Completeness is relative to declared scope and purpose. A specification covering all five dimensions can still be inconsistent or infeasible. Review requirements with the relevant domain methods and assess each proposed implementation separately.

---

## 9. Applying the framework

1. Declare the specification's purpose, scope, and descriptive or prescriptive status.
2. Examine the intended outcome and whether the process is needed.
3. Address each O and both cross-cutting requirements at a proportionate level of detail.
4. Assign roles without assumptions about the kind of entity filling them. Check both wholly manual and wholly AI or machine execution for hidden terminology assumptions.
5. Review consistency, evidence, uncertainty, and composition. Record justified non-applicability and unresolved gaps.
6. Assess candidate implementations against capabilities, authority, interfaces, resources, and evidence requirements. A useful specification does not prove feasibility.
7. Compare actual activity with the specification and route findings through the stated revision authority.

Use the lightest notation that expresses the requirements. Prose and tables may suffice; dependency graphs, BPMN, DMN, CMMN, or formal analysis may be appropriate for more demanding cases. These are representation choices, not additional Os.

See [examples/README.md](./examples/README.md) for manual, AI-only, and mixed application examples, and [skills/5o-process-specification](./skills/5o-process-specification) for a reusable authoring workflow.

---

## 10. Specialized application: automation and AI

Automation uses the same specification dimensions and adds implementation-specific questions. The following are **conditional application guidance**, not requirements for every process.

Where functions are divided between people and machines, Sheridan and Verplank (1978) and Parasuraman, Sheridan and Wickens (2000) provide ways to describe degrees of assistance and autonomy separately for information acquisition, analysis, decision, and action. Such a grid can refine role assignments; it is not the definition of Order.

Where an exceptional transfer goes to a person who has been out of the loop, Bainbridge (1983), Endsley (1995), and Endsley and Kiris (1995) highlight skill retention, attention, and situation awareness. Assess what context and practice that recipient needs. An appropriately designed intermediate mode may help; a universal requirement to descend through automation levels would be inappropriate, particularly when an immediate safe transition is required.

Where AI performs activities, the NIST AI RMF (2023) and ISO/IEC 42001:2023 provide additional governance considerations. Actual tools, permissions, uncertainty handling, and untrusted inputs must be assessed in the target environment. A prompt requiring escalation does not create a communication channel or an available recipient.

Automation case studies, including Lacity and Willcocks (2016), are application evidence. They do not demonstrate that Five O is an exhaustive universal theory or that a specified process is automatically implementable. The prompt and skill-design workflows in this repository are specialized applications of the general framework.

---

## 11. Summary

| Principle | Required specification | Failure class |
|---|---|---|
| **Objective** | Outcomes, limits, trade-offs, and acceptable endings | Unclear or conflicting success |
| **Occurrence** | Conditions permitting activity throughout its lifecycle | Inappropriate activation or continuation |
| **Order** | Dependencies, transitions, coordination, and decision rights | Coordination failure |
| **Option** | Alternatives, deviations, escalation contracts, and unresolved states | Abandoned or unresolved responsibility |
| **Observation** | Evidence, evaluation, and authorized revision | Unassessable behavior or undetected drift |

**The Five Os structure how a process is described or prescribed. Their usefulness depends on explicit roles, authority, objects, resources, and specification quality. They support implementation choices without guaranteeing that implementations are feasible or interchangeable.**

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

Automation case evidence belongs to the specialized application in §10. It does not validate a universal completeness claim for process specification. Vendor-reported outcomes without independent verification are not treated as proof of the framework.
