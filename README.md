# The Five O Principles of Process Automation

**Five questions you must answer before you automate anything.** They work the same whether the work is done by a person, a machine, or an AI.

Most automation that fails is not badly built. It is built to do the wrong thing faster, or it works beautifully until the first surprise and then hands a crisis to someone who cannot pick it up. These five questions are for catching that before you build.

| | |
|---|---|
| **Objective** | What does success look like, and where are the limits? |
| **Occurrence** | When is it allowed to start? |
| **Order** | What has to happen before what? |
| **Option** | What happens when things go wrong? |
| **Observation** | How do you see what happened, and how does that change things? |

Plus two checks that cut across all five: **who owns each part**, and **what it works on**.

---

## Start here

### 📖 [MANIFESTO.md](./MANIFESTO.md)

**Read this first.** Twenty minutes, plain language, no citations. It is the whole framework — the five principles, what goes wrong when you skip each one, the questions to ask yourself, and the honest limits.

A few things in there that people tend to find worth the read on their own:

- Why **a process that cannot fail cannot stop** — and so will do the wrong thing rather than nothing
- Why **your backup plan is not a backup plan** if it needs the thing that just broke
- Why **the better your automation gets, the worse the people behind it get at the job** — and what to do about it
- Why **a quiet success is a warning you threw away**

If you read one file in this repository, read that one.

---

## Use it with your AI agent

Three skills apply the framework so you do not have to hold it all in your head. They chain — idea to brief to spec to prompt — but each one works on its own.

| Skill | Takes | Gives back |
|---|---|---|
| **[`5o-process-automation-brief`](./skills/5o-process-automation-brief)** | A rough idea, however vague | A decision-complete brief, via a short interview |
| **[`5o-automation-planning`](./skills/5o-automation-planning)** | A brief | A buildable specification |
| **[`5o-automation-prompt`](./skills/5o-automation-prompt)** | A spec, or just a description | An agent or system prompt — and it audits existing ones |

**What they actually do for you:**

The **brief** skill interviews you about the parts you have not thought about yet — what must never happen, who gets woken up when it breaks, whether stopping is allowed. If the answers will not fit in 1000 words, it tells you that you are describing more than one automation and suggests which piece to build first.

The **planning** skill turns that into a spec. It stops and asks about anything that would change the design rather than specifying around a hole, and it never names a tool — what must be true, not which vendor.

The **prompt** skill writes and audits agent prompts. It checks what your agent can *actually* do first, because "escalate to a human" in an agent with no escalation tool is not a control — it just looks like one. It also treats anything the agent reads from outside as an attack surface.

### Installing them

**Claude Code** — copy into your skills directory:

```bash
# Git clone or just download zip from github
git clone https://github.com/MaestroError/principles-of-process-automation.git
cp -r principles-of-process-automation/skills/5o-* ~/.claude/skills/
```

Use `.claude/skills/` inside a project instead if you only want them there. Restart, then just describe what you want to automate — the skills trigger on their own.

**Claude Desktop / Cowork** — same folders work. Point Claude at a skill directory and ask it to save the skill, or drop the folders into your skills location.

**Anything else** — a skill is a folder with a `SKILL.md` and some reference files, all plain markdown. Paste `SKILL.md` in as instructions, or hand the folder to whatever agent framework you use. Nothing here depends on a particular vendor.

### Try it

> "I want to automate our invoice approvals — can you help me work out what we actually need?"

> "Here's our agent prompt. It keeps promising things it shouldn't. What's wrong with it?"

---

## Everything else

**[PRINCIPLES.md](./PRINCIPLES.md)** — the same framework at length, with its sources. Every claim is traced to the literature it came from: control theory, cybernetics, business process management, workflow formalisation, human factors, socio-technical design. Every reference is linked, and most are freely readable. Read this if you want to know *why* a principle holds, argue with it properly, or take it somewhere academic.

**[draft.md](./draft.md)** — the original one-page sketch this grew from. Kept for the record.

---

## What this is, and is not

It is a checklist you can carry, grounded in work that is decades old and mostly forgotten outside its own fields. Nothing in it is new. What is new is having it in one place, in language you do not need a doctorate to read.

It will not tell you whether your process is worth automating — only make you ask. It is not a notation, and it does not replace real expertise where a step is genuinely dangerous. And it will not tell you whether people will accept how you have divided the work.

Answering all five does not make a good process. It makes a *described* one. Whether it should exist at all is still your call — and it is the first question, not the last.

---

## Contributing

Corrections to `PRINCIPLES.md` are especially welcome — if a source says something different from what is claimed, that is worth an issue. The skills carry their own eval sets under `skills/*/evals/`, so behaviour changes can be tested rather than argued about.
