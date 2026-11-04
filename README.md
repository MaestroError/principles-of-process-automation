# The Five O Principles of Process Specification

**Five questions for stating how a process operates or is required to operate.**

Use the same core vocabulary for work performed entirely by people, entirely by AI or machines, or by any combination. The framework supports description, design, coordination, delegation, assessment, and revision. Automation is one application.

| Principle | What the specification states |
|---|---|
| **Objective** | Intended outcomes, boundaries, constraints, trade-offs, and acceptable endings. |
| **Occurrence** | Conditions for beginning, continuing, suspending, resuming, and ending activity. |
| **Order** | Dependencies, state transitions, coordination, discretion, and completion conditions. |
| **Option** | Alternatives, exception responses, escalation contracts, and unresolved states. |
| **Observation** | Evidence, evaluation responsibility, and the route from findings to revision. |

Two requirements cut across all five: **ownership and authority**, and **objects and resources**.

Declare whether the specification is **descriptive** (current practice) or **prescriptive** (required behavior). If it includes both, distinguish them. Keep assumptions, recommendations, and unresolved decisions visible.

## Start here

- **[MANIFESTO.md](./MANIFESTO.md)** — the framework in plain language, including questions to ask and limits to its claims.
- **[TERMS.md](./TERMS.md)** — shared definitions of operator, process owner, escalation recipient, role assignment, and related terms.
- **[PRINCIPLES.md](./PRINCIPLES.md)** — the fuller framework, specification-quality criteria, running cases, and sources.
- **[Examples](./examples/README.md)** — fully manual, fully AI, and mixed processes, plus specialized automation applications.

An **operator** performs an activity. A **process owner** holds responsibility for the whole process within defined authority. An **escalation recipient** receives a particular class of unresolved situations. No core role is inherently human, and the recipient need not be the owner. Organizational accountability is defined by the surrounding governance.

## What makes a specification useful

Covering five headings is a starting point. Requirements also need consistent meanings, assessable criteria, appropriate detail, explicit uncertainty, compatible interfaces, and a governed route for revision. A simple process needs a simple specification; a justified statement of non-applicability is better than invented machinery.

An operator-independent specification supports changes in implementation. It does not guarantee that a person, script, machine, or AI can replace another unchanged. Assess capabilities, authority, interfaces, resources, and evidence for each proposed implementation.

## Use it with your AI assistant

Two general authoring skills support the framework. Two specialized skills apply it to AI instructions. Each works independently; a general process brief or specification does not have to lead to an agent prompt.

| Skill | Takes | Gives back |
|---|---|---|
| **[`5o-process-brief`](./skills/5o-process-brief)** | A rough process description or intended change | A concise brief separating decisions, observations, assumptions, and open questions. |
| **[`5o-process-specification`](./skills/5o-process-specification)** | A brief or requirements | A proportionate descriptive or prescriptive specification. |
| **[`5o-automation-prompt`](./skills/5o-automation-prompt)** | An AI-operated process specification or agent instructions | An agent or system prompt, or an audit of an existing one. |
| **[`5o-skill-design`](./skills/5o-skill-design)** | A repeated agent workflow or an existing skill | A skill directory, or an audit of an existing one. |

The **brief** skill asks only about meaningful gaps and preserves unknowns. The **specification** skill makes dependencies, decision rights, exception handling, and evidence explicit without inventing an implementation. Both preserve manual, AI-only, and mixed role assignments. An explicit human-only approval constraint remains a constraint when the user supplies it.

The **prompt** and **skill-design** skills are applications of the framework. They check actual tools and permissions: requiring escalation does not create a communication channel, a capable recipient, or permission to transfer work.

### Installing the skills

For Claude Code, copy the folders into your skills directory:

```bash
git clone https://github.com/MaestroError/principles-of-process-automation.git
cp -r principles-of-process-automation/skills/5o-* ~/.claude/skills/
```

Use `.claude/skills/` inside a project for project-local installation. For another assistant, use its supported skill-loading mechanism or supply the relevant `SKILL.md` and supporting files as instructions.

**Renamed skills:** `5o-process-automation-brief` is now `5o-process-brief`; `5o-automation-planning` is now `5o-process-specification`. Replace older installed folders rather than retaining both versions, so duplicate skills do not compete for the same request. The specialized prompt and skill-design names remain unchanged.

The repository URL retains its original name so existing links continue to work.

### Try it

> "Describe how our paper-based lending desk currently works. Keep unknowns separate from required behavior."

> "Specify this research-record process. All operators, the specialist escalation recipient, and the bounded process owner are AI agents."

> "Turn this maintenance brief into a spec. The monitoring system, technician, and supervisor have different decision rights."

> "Audit this agent prompt against the process specification and its actual capabilities."

## Applications and history

The existing LinkedIn workflows and case studies record the framework's development through automation work. They remain examples of that application rather than universal requirements. [draft.md](./draft.md) preserves the original sketch as historical material.

Automation-specific grounding, including human takeover and levels of assistance, is retained in the [specialized application section](./PRINCIPLES.md#10-specialized-application-automation-and-ai). It does not impose human escalation, manual practice, or an automation grid on every process.

## Limits and contributions

The Five Os are a coverage and design-review scaffold, not a proof of completeness or a substitute for domain expertise. A fully specified process can still be undesirable, inconsistent, or infeasible.

Corrections to the source interpretations and counterexamples to the framework are welcome. Skill evaluation scenarios live under `skills/*/evals/`; they describe observable behavior and do not, by themselves, establish passing results.
