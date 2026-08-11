# Skill scaffold

Two parts, and the split matters: a **worksheet** organised by the five dimensions, which is yours and never ships, and a **skeleton** organised by the reader's task, which is what you deliver.

Filling the worksheet into headed sections and calling that the SKILL.md is the failure this asset exists to prevent.

---

## Part 1 — Directory

```
skill-name/
├── SKILL.md              required. Loads whole, every time. Keep it short.
├── references/           loaded only when needed. One level deep from SKILL.md.
│   └── *.md              contents list on anything over ~100 lines
├── assets/               used in output — templates, skeletons, boilerplate
├── scripts/              executed, not loaded. For fragile or repetitive steps.
└── evals/
    ├── evals.json        behaviour cases
    └── fixtures/         input files the cases need
```

Only `SKILL.md` is required. Add a directory when something needs to live there, not to look complete — an empty `scripts/` is a promise the skill does not keep.

Split `references/` by domain rather than by size. Four platforms means four files, so one loads per run.

---

## Part 2 — Worksheet (yours; does not ship)

Answer before writing. Blanks here become defects later.

**Objective**
- What does the model get wrong without this skill? (If you cannot name it, stop — you do not yet know whether the skill is needed.)
- What is this skill *not* for?
- Where two goods conflict, which wins?

**Occurrence**
- What does a user type when they need this? Their words, casual and abbreviated. List five.
- What must be present before it can work? What if it is not?
- What near-misses must *not* fire it? List three that share vocabulary with it.
- Which neighbouring skill wins on overlap?
- What shapes do real requests take? Does the skill say something about each?

**Order**
- What belongs in the body, and what only loads when needed?
- Which steps are fragile enough to need an exact command or a script?
- Which are open enough that a script would make things worse?
- Is there anything checkable, where a validator loop beats instruction?

**Option**
- What are the words that let this skill hand back?
- What happens when its own script fails or a reference is missing?
- What does it do with a request that half fits?
- Which harnesses lack something it wants, and what does it do there instead?

**Observation**
- Which assertions would fail without the skill? Those are the only ones worth writing.
- Which trigger cases fire it, and which near-misses must not?

**Ownership**
- Who maintains it? What breaks it when the world changes?

---

## Part 3 — SKILL.md skeleton (ships)

Structure follows the reader's task. The headings below are a starting shape, not a form — rename, merge, and drop them to fit the work.

```markdown
---
name: [lowercase-hyphenated; no "claude" or "anthropic"]
description: [Third person. What it does, then when to use it — in the words a
  user would type, including the casual phrasing. Then the boundary: what it is
  not for, and which neighbour wins on overlap. Slightly pushy; the common
  failure is not firing when it would have helped. Under 1024 characters.]
---

# [Title]

[One or two sentences: what this is for, and the thing it exists to prevent.
No heading. Nothing the model already knows.]

## [Before you start / Establish X first]

[Whatever must be true or known before the work begins — inputs, context,
capabilities. And what to do when it is not: the words that permit handing
back. Most skills are missing this section entirely.]

## [The work — named after what the reader is doing]

[The instructions. Imperative. Reasons attached in a clause, not a paragraph.
Prose where judgement is needed; lists and tables for reference material.
Exact commands where a step is fragile, and a note that varying them breaks
something specific.]

## [Cases / When it goes differently]

[The shapes real requests take, and what changes for each. Include the one
where the answer is to stop.]

## [Output shape]

[A template if the format is fixed, a sensible default plus latitude if not.
One or two input/output pairs if the style is easier shown than described.]

## Before you deliver

[Numbered checks. Each should catch a defect that is cheap now and expensive
later — not a restatement of the instructions above.]

## Reference

- `references/x.md` — [what is in it, and when it is worth reading]
```

---

## Part 4 — Evals

Two kinds, kept apart. Trigger evals test whether the skill fires; behaviour evals test what it does once it has.

`evals/evals.json`:

```json
{
  "skill_name": "skill-name",
  "evals": [
    {
      "id": 0,
      "name": "descriptive-name-not-eval-0",
      "prompt": "What a real user would actually type, with their specifics in it",
      "expected_output": "One or two sentences on what a good run looks like",
      "assertions": [
        "One behaviour each, objectively checkable, and would fail without the skill"
      ],
      "files": ["evals/fixtures/whatever-it-needs.md"]
    }
  ]
}
```

Trigger cases are a flat list of `{"query": "...", "should_trigger": true|false}`. Keep the negatives as near-misses — an obviously unrelated query tests nothing.

For running, grading, and benchmarking these, hand off to `skill-creator` if it is installed. If it is not, the set is still worth writing: it is a design artefact before it is a test suite.
