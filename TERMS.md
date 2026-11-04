# Shared terms

These definitions apply throughout the Five O Principles of Process Specification. They describe responsibilities and relationships, independent of whether people, machines, software, or AI fill the roles.

| Term | Definition |
|---|---|
| **Process** | A related set of activities through which inputs, resources, and conditions contribute to an outcome, including changing something, maintaining a condition, or preventing an unwanted change. |
| **Process specification** | A statement of how a process operates or is required to operate, at a declared scope and level of detail. |
| **Descriptive specification** | A specification of observed current practice, including uncertainties and departures from stated rules. |
| **Prescriptive specification** | A specification of required behavior, distinguishing requirements from assumptions, recommendations, examples, and unresolved decisions. |
| **Execution** | A particular occurrence of activity governed by the process. For continuous processes, specify the relevant operating interval or observation boundary. |
| **Operator** | The entity performing a specified activity, including gathering information, interpreting, deciding, or acting. The term does not imply a person or exclude decision-making. |
| **Role** | A defined set of responsibilities and decision rights, with required capabilities and resources. |
| **Role assignment** | The mapping of a role to the entity filling it: a person, team, organizational unit, machine, software system, or AI agent. |
| **Process owner** | The role responsible for the process as a whole, with defined authority over its requirements, performance, and revision. Ownership does not imply unlimited power to change requirements. |
| **Escalation** | Transfer of an unresolved situation beyond the current operator's capability or authority to a designated recipient able and authorized to address it. |
| **Escalation recipient** | The role designated to receive a particular class of escalation, with the required capability, authority, resources, and availability. It need not be the process owner or a hierarchical superior. |
| **Handover** | Transfer of information, work state, and responsibility between roles. Escalation is one kind of handover; ordinary workflow transitions are another. |
| **Authority** | Permission to make specified decisions or perform specified actions, within stated limits and under identified governance. Capability alone does not confer authority. |
| **Object** | Something the process acts on or describes, with an identity and relevant states: for example an item, record, request, or operating condition. |
| **Resource** | A capability, capacity, input, permission, or facility required or consumed by activity. |
| **Safe state** | A condition explicitly judged acceptable for the relevant situation, including any activity required to maintain it. Doing nothing is not necessarily safe. |
| **Implementation** | The concrete assignment of operators, methods, interfaces, and resources used to carry out a specification. |

## Role boundaries

An operator performs an activity. The process owner holds responsibility for the whole process. An escalation recipient resolves a specified class of situations beyond an operator's limits. One entity may fill several roles, but that does not merge their responsibilities or enlarge their authority.

**No core role is inherently human.** A machine or AI may hold bounded process ownership as well as operate or receive escalations. The surrounding governance specification determines organizational accountability, including any requirement for a human or organizational authority. Functional role assignment alone does not transfer that wider accountability.

Avoid using **lead**, **supervisor**, **reviewer**, or **approver** as synonyms for process owner. They are useful local role names when their particular responsibilities and decision rights are defined. Avoid using **operator** as shorthand for the person receiving an escalation: the recipient's role must be explicit.

## Minimum escalation contract

Specify the triggering condition; recipient and required capability and authority; availability; evidence, actions taken, current state, and requested resolution; acknowledgment and responsibility-transfer conditions; and the bounded response to unavailability or non-resolution.

An escalation is not satisfied by naming a destination with the same unresolved limitations. Paths must lead to a decision, a defined pending or maintained safe state, or termination where appropriate, rather than indefinite transfer loops.

## Independence and proportionality

An operator-independent specification supports changes in implementation. It does not guarantee interchangeable operators: capability, authority, interfaces, resources, and evidence need assessment in each implementation.

Apply all five dimensions at a level appropriate to scope, complexity, and consequence. State justified non-applicability and unresolved questions explicitly. A universal vocabulary is not a requirement for identical machinery in every process.
