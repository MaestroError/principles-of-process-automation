# Composition — parent and subprocess specs

Read this only when the brief genuinely contains more than one process. **A single spec is the normal case and the better default.** Decomposing a process that did not need it adds ceremony, spreads decisions across files, and makes the design harder to hold in one head.

## When to decompose

Two or more of these, actually present — not "it feels big":

- More than one trigger starting genuinely different work
- More than one owner of the core outcome
- More than one definition of "finished"
- Groups of output that no single consumer receives together
- Failure modes with nothing in common — one part breaking says nothing about the others

## The shape

```
parent spec
  ├─ shared gate  (validated once, before any subprocess runs)
  ├─ subprocess A ─┐
  ├─ subprocess B ─┼→ assembly / completion
  └─ subprocess C ─┘
```

The parent owns: the gate, dispatch, aggregation, the safe stop, and any human checkpoint. Subprocesses own their own work and nothing else.

## Six rules that make the levels fit

### 1. The parent's Occurrence is the shared gate

Any precondition needed by two or more subprocesses is validated **once, at the parent, before dispatch**. If it fails, the run exits there and no subprocess starts.

The alternative — each subprocess defending itself — means the same check written three times, three different behaviours for one condition, and an input failure surfacing as a subprocess error. A subprocess should carry no logic for a condition the parent already guaranteed.

### 2. Contracts make the composition explicit

Every subprocess spec opens with four statements:

| | |
|---|---|
| **Guaranteed by parent** | What it may assume without checking |
| **Consumes** | What it takes in |
| **Produces** | What it returns, including the "nothing" case |
| **Escalates** | What it hands back rather than handling |

Without these, "Five O all the way down" produces well-specified pieces that do not connect.

### 3. Classify every failure hard or soft

- **Hard** — halts the run, returns to the human. *No supportable path exists.*
- **Soft** — the run continues carrying a flag. *An optional input was unavailable.*

This is the most useful rule here. Without it each subprocess decides unilaterally whether its own failure is fatal, and gets it wrong in both directions — halting the workflow over a missing nice-to-have, or shipping output whose central claim could not be verified.

Classification belongs to the parent, because only the parent knows what the output is for.

**A third category is easy to miss: quiet success.** A retry that worked, a fallback that produced usable output, a lower-priority route taken. Not failures, and indistinguishable from a clean run. Record and surface these too.

### 4. Human judgement consolidates up; verification stays down

Two rules that look contradictory and are not.

**Judgement moves to the parent.** If the parent has a review step, subprocesses do not each need their own. Asking someone to approve the same artefact twice trains them to stop looking.

**Mechanical checks stay at their origin.** A variance should be caught as near its source as possible; correcting it somewhere else, much later, is a poor design for learning. "Does this output meet the size limit" belongs in the subprocess that produced it. Only genuinely cross-subprocess checks belong at assembly.

Consolidate judgement. Distribute verification.

### 5. Objectives nest but are restated

A subprocess objective is phrased in what that subprocess controls, not in the parent's terms. The parent's objective might be "an approved published post"; the image subprocess's is "a visual that matches the source and does not misrepresent it". A subprocess cannot be held to an outcome it does not control, and an objective it cannot measure is not an objective.

### 6. Observation aggregates upward

Each subprocess observes itself. The parent observes what none of them can — most valuably, **where human corrections land, attributed to the subprocess that produced the thing corrected**. That single measure routes all improvement effort, and it only exists because a parent with a review step exists.

Watch for the congruence trap here: if the parent is measured on "how little the reviewer changes", the measure rewards the reviewer for not looking. Read such measures as trends, never as targets, and pair them with something that would move in the opposite direction if review decayed.

### 7. State each rule once, at the level that enforces it

Decomposition multiplies documents, and the cheapest mistake is to give every child a full copy of every rule. A prohibition then appears in the parent's constraints, the parent's congruence check, the child's contract, the child's objective, and the child's automation grid — five places, five chances to drift, and the next person to edit it will update three.

The rule lives where it is **enforced**. If the parent gate checks it, it belongs to the parent and children reference it. If only one subprocess can enforce it, it belongs there and the parent references it. This is the shared gate applied to text rather than to checks: a rule stated once cannot disagree with itself.

Children should be short. A child spec that repeats most of its parent has not been decomposed — it has been photocopied.

## What to produce

One parent spec plus one spec per subprocess, each using the standard template, with the contract block added at the top of each child. Name the subprocesses in the parent's scope section so the boundaries are visible from either end.

The parent carries: the shared gate, dispatch order, failure classification, cross-cutting rules, the safe stop, and any human checkpoint. Children carry only what is theirs. If you cannot say what a child owns that nothing else does, it is not a subprocess.
