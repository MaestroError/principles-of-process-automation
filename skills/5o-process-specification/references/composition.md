# Composition — parent and subprocess specifications

Use when independently triggered work, distinct outcomes or owners, separate completion conditions, or meaningful interfaces justify decomposition. One specification is preferable when a coherent boundary suffices. Length alone is not a reason to split.

## Responsibility and contracts

The parent specifies the overall outcome, shared admission conditions, coordination, cross-subprocess decision rights, failure consequences, and overall completion or maintained state. Each child specifies its own activities and interfaces. All roles use the same definitions regardless of assignment to people, machines, or AI.

Each child contract states:

| Contract element | Required content |
|---|---|
| Preconditions supplied by parent | What may be assumed, evidence supporting it, and how long it remains valid. |
| Consumes | Inputs, identities, states, and resources. |
| Produces or maintains | Output or condition, acceptance criteria, and partial/no-output cases. |
| Escalates | Unresolved classes, recipient, authority, transfer contents, acknowledgment, and non-resolution response. |

Do not treat an admission check as a permanent guarantee. Revalidate mutable conditions at the point where correctness depends on them, with responsibility for that check explicit. A role assignment or permission can change after dispatch.

## Coordination rules

1. **State shared rules once at the responsible level.** Children reference them. Local requirements remain local.
2. **Specify failure consequences in context.** Distinguish cases that prevent the parent's outcome from cases that allow an explicitly limited result. A blocked child does not implicitly halt all work or transfer to a human.
3. **Place decisions where the required evidence and authority exist.** Consolidate genuinely shared decisions where useful; do not universally move judgment upward or duplicate approval. Local and independent approvals remain where required.
4. **Specify interface checks at the relevant boundary.** Check local output quality near its source and cross-child compatibility at composition. Define acceptance and responsibility transfer.
5. **Express child objectives in what they control.** Connect their acceptance criteria to the parent's outcome without repeating all parent requirements.
6. **Aggregate evidence for the parent's questions.** Attribute deviations and corrections where useful; use evidence appropriate to manual, AI, machine, or mixed execution.
7. **Bound unresolved work and escalation.** Specify acknowledgment, availability, maintained safe/pending states, and termination where appropriate. The process owner is not the default escalation recipient.

## Deliverable

Provide a parent specification and proportionate child specifications or referenced sections. Identify all interfaces in both directions, preserve OPEN items, and explain the actual evidence for decomposition. The contract structure is general; dispatch mechanisms, communication tools, human reviews, and automation levels are implementation-specific choices.
