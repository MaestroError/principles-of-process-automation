# The Five O Principles of Process Specification — condensed reference

A universal framework for stating how a process operates or is required to operate. It supports description, design, coordination, delegation, assessment, and revision. Automation is one application.

A process may be finite, recurring, or continuous. Its outcome may change something, maintain a condition, or prevent an unwanted change. State its boundary and interfaces.

## Status and terms

**Descriptive** means observed current practice; preserve unknowns and missing controls. **Prescriptive** means required behavior; distinguish requirements from assumptions, recommendations, examples, and OPEN decisions. Label mixtures.

- **Operator:** entity performing an activity, including gathering information, interpreting, deciding, or acting.
- **Process owner:** role responsible for the whole process, with defined authority over requirements, performance, and revision.
- **Escalation recipient:** role designated to resolve a class of situations beyond an operator's capability or authority. It need not be the owner or a hierarchical superior.
- **Role assignment:** mapping of a role to a person, team, organizational unit, machine, software system, or AI agent.

No core role is inherently human. Keep roles distinct even when one entity fills several. Functional ownership does not settle organizational accountability; the surrounding governance determines that and any human-only requirement. Capability does not itself confer authority.

## Objective

Specify outcomes or maintained conditions, beneficiaries, boundaries, constraints, trade-offs with limits, and criteria for success or justified termination. Resolve conflicts between measures and rules. Ask whether the work is needed before preserving inherited steps.

## Occurrence

Specify trigger, readiness, authorization, and timing. Include conditions for continuing, suspending, resuming, and ending, not only starting. Identify where situations needing different treatment are distinguished before dependent decisions; classification need not happen in the initial trigger.

## Order

Specify dependencies, state transitions, coordination, concurrency, completion, and decision rights. Distinguish flow, sharing, and fit dependencies. Where relevant, identify which roles gather, interpret, decide, and act. Preserve flexibility over method unless a method is itself required. Do not impose an automation-level grid or a human decision point.

## Option

Specify alternatives, exceptions, and recovery to an acceptable state. Check shared dependencies honestly; doing nothing is not necessarily safe or independent. Define which material deviations, retries, and substitutions are recorded or communicated, to whom, and when.

An escalation contract names: the triggering capability/authority limit; recipient and required capability/authority/availability; transferred outcome, evidence, actions, state, and requested resolution; acknowledgment and responsibility-transfer conditions; and a bounded response to unavailability or non-resolution. Avoid indefinite transfer loops. The recipient need not be a human or the process owner.

Maintain capabilities required for exceptional as well as routine operation. Training, simulation, and machine capability checks are implementation choices where appropriate, not universal requirements.

## Observation

Specify evidence, evaluation criteria and responsibility, and the authority and route for revision. Evidence may be paper, inspection, measurement, acknowledgment, sampling, or event history. Consider current deviations, accumulated friction, and trends for ongoing work; a finite process may need completion evidence and closeout instead. Explain non-applicability. Findings do not themselves authorize changes.

## Cross-cutting requirements and quality

Within every O identify ownership/authority and objects/resources. State role assignments, relevant identities and states, resource contention, and shared dependencies. Requirements need declared status, consistent terms, assessable criteria, essential detail, visible uncertainty, compatible interfaces, and governed revision. State rules once at the responsible level and reference them elsewhere; reassess conditions that can change.

Five headings do not prove completeness, correctness, desirability, or feasibility. Scale detail to scope, complexity, uncertainty, and consequence; record justified non-applicability. An operator-independent specification supports transitions without guaranteeing interchangeable implementations. Assess capability, authority, interfaces, resources, and evidence for each implementation.

The core vocabulary must support wholly manual and wholly AI or machine processes unchanged. Specialized applications may add human-factor or automation controls when their actual assignments require them.
