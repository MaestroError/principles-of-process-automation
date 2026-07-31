# The Five O Principles of Process Automation

**Five questions you must answer before you automate anything — in business, law, engineering, or anywhere else.**

These principles work the same whether the work is done by a person, a machine, or an AI.

Nothing here is new. It comes from decades of work in quality standards, business process management, control engineering, safety analysis, and research into how people and machines work together. What is new is putting it all in one short list that anyone can use. You should not have to read forty papers to design a process well. That is the point of this document.

---

## What is a process?

**A process is work that changes something.**

It has a start and an end. It takes something in and produces something out. And it happens more than once, in a way you can describe — otherwise it is just a one-off task.

Notice what this leaves out: **who does the work.** This matters more than it looks. If you describe a process properly, you can move it between a clerk, a script, a machine, and an AI without redesigning it. Choosing who does the work becomes a separate decision, made later.

---

## First, ask if it should exist

Before anything else: **should this process exist at all?**

Most failed automation projects are not badly built. They are built to do the wrong thing faster. Someone takes a process that grew by accident over ten years and makes it run in seconds. Now the company is wrong at speed.

So ask what the work is really for. Not how it is done today — what result you actually need. Very often the answer changes the whole design, and sometimes it deletes half the steps.

---

# The Five Principles

## 1. Objective — what does success look like, and where are the limits?

A goal on its own is not enough. An objective is only finished when it says four things:

- **The result** you want, and who it is for.
- **What is not included.** The edges matter as much as the middle.
- **What must never happen** — even if breaking that rule would be faster or cheaper.
- **What you are willing to trade.** Speed for quality? Cost for flexibility? Say which, and say how far.

Then add one more thing that most people forget: **when is stopping the right answer?** A process that has no way to fail cannot stop. So it will keep going when it should not.

**If you skip this:** the system runs fast in the wrong direction. And if whoever does the work is clever — a person under pressure, or an AI — they will find the gaps you did not think to close. An unclear goal with no limits is an invitation.

**Ask yourself:** What am I really trying to achieve? What is out of scope? What must never happen? What am I allowed to sacrifice, and down to what level? When should this stop instead of finish?

---

## 2. Occurrence — when is it allowed to start?

This is not simply "when". Four separate things must be true:

- **The trigger.** The event that says "maybe now".
- **Readiness.** The data, files, approvals, and resources that must already be there.
- **Permission.** Who allows this to run, and is that checked at the time?
- **The time window.** When acting is right — and when it is too early or too late.

Each of these can fail on its own, and they fail differently. Not acting is one problem. Acting when you should not is another. Acting at the wrong moment is a third. Treating them as one thing hides two of them.

There is also a limit worth knowing. **Your trigger must be able to tell apart every situation that needs a different answer.** If the real world produces six kinds of case and your trigger only sees "something arrived", you will handle four of them badly. This is not bad luck. It is arithmetic.

**If you skip this:** the process runs on half the facts, or at the wrong moment, or does not run at all when it should — and nobody notices, because nothing visibly broke.

**Ask yourself:** What starts this? What must be true and present before it is safe to act? Who says it may run? Is there a time when acting would be wrong even though the trigger fired? Can my trigger tell my cases apart?

---

## 3. Order — what has to happen before what?

Order is not a list of steps. It is a map of what depends on what. There are three kinds of dependency:

- **One task needs something an earlier task produces.**
- **Two tasks need the same limited thing** — a person, a machine, a budget, an API.
- **Several tasks each build part of one thing,** and the parts have to fit together.

Write down the dependencies, not the steps. If you write every step, you lock out better ways of working and the whole thing breaks whenever something small changes.

Order also decides **who does each part, and how much freedom they have.** This is not one setting for the whole system. For each step, ask four separate questions: who collects the information, who works out what it means, who decides, and who acts? A good design is often fully automatic at collecting and fully human at deciding. "Is this automated?" is the wrong question. The real answer is a grid.

**If you skip this:** the process breaks at the joins, not in the steps. Work starts on old data. Two jobs fight over the same resource. Two correct outputs do not fit together. And nobody owns the gap between them.

**Ask yourself:** What truly depends on what? What could run at the same time that I am doing one after another? What does "finished" actually mean? For each step — who collects, who judges, who decides, who acts?

---

## 4. Option — what happens when things go wrong?

Things go wrong constantly. That is normal running, not a rare event.

You need three kinds of answer:

- **Other routes** to the same result.
- **Exceptions** — what to do when reality does not match your assumptions.
- **Recovery** — return to a safe state, pass it to someone who can help, or stop.

That last one carries the most weight. **Stopping must be a genuine option.** If your process has no way to say "not this time", it will do something wrong rather than nothing.

Then there are two rules that sound like opposites and are not.

### Fail loudly

Never let the system quietly work around a problem. If it tried three times and the third worked, say so. If it fell back to a worse method and still produced something usable, say so.

Automation is very good at hiding trouble by working harder. It absorbs a growing fault so smoothly that nothing looks wrong — until it cannot absorb it any more, and by then it is too late to fix cheaply. A quiet success is not a success. It is a warning you threw away.

### Hand over slowly

When the system reaches its limit, it should step down, not drop out.

Going straight from fully automatic to "here, you deal with it" hands someone a problem with no background, at the worst possible moment. Step down one level at a time. And pass on what you were trying to do, what actually happened, and what is needed now — not an error code.

### The hard truth behind both

**The better your automation is, the worse the people behind it become at the job it does.**

They lose practice, because the system handles everything routine. They stop paying attention, because nobody can watch a system that almost never fails — human attention on a quiet screen fades after about half an hour, no matter how motivated the person is. And when it finally does fail, they are asked to do the hardest version of a task they have not done by hand in months, under time pressure.

So the most reliable systems need **more** training and practice for their people, not less. Build in some manual work on purpose. It feels wasteful. It is insurance.

**If you skip this:** the system works beautifully until the first real surprise, then hands a crisis to someone who cannot pick it up.

**Ask yourself:** What are the other routes? What happens if each dependency is not met? Does it step down or drop out? What exactly does the person see when it lands on them — and could they act on it straight away? Can this be stopped, and by whom? If it runs perfectly for a year, will anyone still know how to do it by hand?

---

## 5. Observation — how do you see what happened, and how does that change things?

Observation has three duties. Most teams only do the first.

- **Record.** Keep enough that you could rebuild what happened months later.
- **Judge.** Compare what happened against what you intended, and against the goal.
- **Change.** Have a real route by which what you learn changes the process.

Recording without judging is just storage. Judging without changing is theatre.

Watch three different time frames:

- **What is wrong right now.** Act on it today.
- **What is slightly wrong every single time.** No single case justifies fixing it, but across a thousand runs it costs more than any incident. This one needs a redesign, not a fix.
- **What is getting worse.** A number moving the wrong way before anything has actually broken. This is your earliest warning, and it is the one people least often build.

Then look **outside** the process. The most commonly missed question is whether the world changed in a way that makes the process pointless. A process can run perfectly for a year against reasons that stopped being true.

**If you skip this:** slow decay that nobody notices, because the system keeps reporting success right up until it doesn't.

**Ask yourself:** Could I reconstruct one run six months from now? Am I watching all three time frames? How does a finding actually change the process, and how long does that take? Who reads this, and are they allowed to change anything? What would tell me this process should no longer exist?

---

# Two checks that apply to all five

## Who owns it

Every one of the five needs a name against it.

Who can change the goal? Who allows a run? Who owns each handover in the order? Who picks up an escalation — and are they actually there at three in the morning? Who reads the reports, and are they allowed to act on them?

The most common real-world failure is an escalation path that ends in a queue nobody owns. An unowned gap does not stay neutral. Blame circulates around it and nothing is ever fixed. This was documented in a coal mine in 1951, and nothing about it has changed.

## What it works on

Name the things the process handles and the resources it uses. Without this you cannot schedule it and you cannot hand it to anyone else.

One check here catches more problems than any other: **if your backup plan needs the same thing that just broke, you do not have a backup plan.** Count how many of your alternatives can fail together, not how many alternatives you have. Very often the only truly independent option is doing nothing — which is one more reason to design that option properly.

---

# Four rules worth remembering

**Say what must happen, not how.** Be exact about the result. Be loose about the method. Describing too much closes off better options and makes everything fragile. This is the answer to "how detailed should I be?"

**Where a human decides, say so.** Marking the place where judgement is still needed is a result, not a failure. It tells you exactly what to build — everything around that decision, and not the decision itself.

**Check that your measure does not fight your rule.** If you measure clicks but forbid exaggeration, the measurement will quietly win over time. Decide now which one takes priority, and write it down.

**Deal with problems where they start.** Catching something in another team, a week later, teaches nobody anything and fixes nothing at the source.

---

# What this will not do for you

**It will not tell you whether the process is worth doing.** It only forces you to ask. A process can answer all five questions perfectly and still be a waste of everyone's time.

**It is not a tool or a diagram.** It tells you what must be decided, not how to write it down. Use whatever notation suits you.

**It does not replace real expertise.** Where a step is genuinely dangerous — safety, money, law — use the proper method built for it. These principles tell you that you need one.

**It does not tell you whether people will accept it.** You can describe a process perfectly and still divide the work in a way people will not put up with. How you split control, visibility, and responsibility between people is a real design decision, and this list does not make it for you.

---

# In short

**Five questions:**

1. **Objective** — What counts as success, and what are the limits?
2. **Occurrence** — Under what conditions may it act?
3. **Order** — What must be true before what?
4. **Option** — What happens when reality does not cooperate?
5. **Observation** — What does it tell you, and how does that change it?

**Two checks:** 
- Who owns each part? 
- What does it work on, and what does it use?