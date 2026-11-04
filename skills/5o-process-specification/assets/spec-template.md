# Process Specification: [name]

**Kind:** [Descriptive | Prescriptive | Labeled combination]
**Status:** [Supported scope ready | Open facts or decisions remain]
**Version / effective or observation period:** [identifier and period]
**Boundary and sources:** [scope, related processes, sources of facts or requirements]

Label observations, requirements, assumptions, recommendations, and OPEN items. Adapt depth to purpose, complexity, and consequence; explain non-applicability.

## Objective

**Outcome or maintained condition / beneficiary:** [assessable result]
**In scope / out of scope:** [boundaries]
**Constraints:** [hard requirements or observed rules, with status]
**Trade-offs and precedence:** [limits and conflict resolution]
**Success / partial completion / suspension / termination:** [criteria]

## Occurrence

| Condition | Start | Continue | Suspend | Resume | End |
|---|---|---|---|---|---|
| Trigger or state | [condition] | [condition] | [condition] | [condition] | [condition] |
| Readiness | [required data/resources] | [reassessment] | [loss] | [restoration] | [condition] |
| Authority | [permission] | [validity] | [revocation] | [renewal] | [authority] |
| Timing | [window] | [duration] | [limit] | [window] | [limit] |

**Case distinctions:** [which situations need different treatment and where they are distinguished before dependent decisions]

## Order

| Activity or transition | Requires | Dependency kind | Responsible role | Acceptance / completion condition |
|---|---|---|---|---|
| [activity] | [input state or prerequisite] | [flow / sharing / fit] | [role] | [condition] |

**Concurrency / synchronization / contention:** [rules]
**Permitted states and transitions:** [including pending work or cancellation]
**Decision rights:** [which roles gather, interpret, decide, and act where relevant; discretion and authority limits]
**Interfaces:** [input/output meaning and acceptance conditions at boundaries]

## Option

| Variant or exception | Condition | Response and responsible role | Dependencies / shared limitations | Evidence or communication |
|---|---|---|---|---|
| [route / deviation] | [condition] | [response] | [requirements] | [what, to whom, when] |

**Recovery and unresolved state:** [acceptable pending or maintained safe condition; suspension or termination where appropriate]
**Capability availability:** [how essential routine and exceptional capabilities remain available, where material]

### Escalation contracts

| Triggering limit | Recipient | Required capability / authority / availability | Transferred evidence, actions, state, and requested resolution | Acknowledgment and responsibility-transfer limit | Unavailable or unresolved response |
|---|---|---|---|---|---|
| [condition] | [role] | [requirements] | [contents] | [confirmation and bound] | [bounded alternative or maintained state] |

The recipient is not implicitly the process owner or a human. Avoid indefinite transfer loops; do not assume inactivity is safe.

## Observation

**Evidence:** [questions answered; records, inspections, measurements or other evidence; meaning, access, retention where relevant]
**Evaluation:** [role, criteria, timing]
**Horizons:** [current, accumulated, trending, or finite-process closeout; explain non-applicability]
**External reassessment:** [changes invalidating assumptions, where relevant]
**Revision:** [authority and limits, version identification, communication to affected roles]

## Roles, authority, objects, and resources

| Role | Responsibility and decision rights | Assignment | Capability / resources / availability |
|---|---|---|---|
| Process owner | [whole-process authority and limits] | [entity] | [requirements] |
| [activity operator] | [activity and discretion] | [entity] | [requirements] |
| [escalation recipient] | [exception class and authority] | [entity] | [requirements] |

**Governance:** [source and limits of authority; organizational accountability where applicable]
**Objects:** [identities, states, input/output semantics]
**Resources:** [capacity, access, permissions, facilities; allocation and shared dependencies]

Reference role and resource definitions from each O rather than repeating rules. No core role requires a particular entity type. Check whether measures conflict with constraints and resolve precedence.

## Open items and assumptions

| Status | Item | Decision authority | Affected or gated activity |
|---|---|---|---|
| [OPEN / assumption] | [item] | [role] | [effect] |

## Assessment notes

[Specific uncertainties or implementation-assessment needs. Covering the template does not establish completeness, feasibility, or interchangeable operators.]
