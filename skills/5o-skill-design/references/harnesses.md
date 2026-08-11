# What varies between installs

Read when a skill depends on subagents, scripts, a browser, a display, network access, or writing to disk — which is most skills that do anything.

A skill is written once and runs wherever someone installs it. The install decides what exists. Nothing below fails loudly: the model reads an instruction it cannot carry out, and improvises.

## Contents

- The eight things that vary
- How to write against them
- The declaration

---

## The eight things that vary

**Subagents.** Present in some products, absent in others. Any instruction to "spawn one per case and run in parallel" needs a serial fallback, and the fallback is usually fine — slower, less independent, still useful.

**A display or browser.** Anything that opens a viewer, a report, or a local server assumes someone can see it. The fallback is a static file plus a path, and it should be the *default* rather than the exception, because more installs lack a display than have one.

**A writable skill directory.** Frequently read-only. A skill that caches state, writes logs, or edits its own files beside SKILL.md works on the author's machine and nowhere else. Write to a working directory the harness gave you.

**Shell and interpreters.** Some installs have a shell, some have a sandboxed one on a different filesystem from the file tools, some have none. Where the shell and the file tools see different paths, a script that hands a path to the user is handing them a path they cannot open.

**Network access.** Often absent or allowlisted. A skill that installs a package at run time will work until it does not, and the failure arrives in the middle of someone's task.

**Named tools.** Tool names differ between products and change over time. A skill that says "use `WebSearch`" is wrong wherever that is called something else. Describe the capability — "search the web" — and let the model find its tool.

**Bundled scripts.** Whether they can be executed at all, and in what interpreter. Also whether their dependencies are present, which is a separate question and the one that actually bites.

**Sibling skills.** A skill that hands off to another — as this one does to `skill-creator` for eval machinery — cannot assume it is installed. Say what to do if it is not, which is usually "do the reduced version yourself".

---

## How to write against them

**Put the fallback in the same breath as the instruction.** Not in a compatibility section at the end. A reader who has what they need skips one clause; a reader who does not gets the answer where they were already looking.

> "Spawn a subagent per case. Without subagents, run them yourself one at a time and say that you did."

**Prefer a capability description to a tool name.** "Search the web" survives a rename; `WebSearch` does not.

**Make the thin version the default where you can.** A static HTML file written to disk works everywhere, including where a server would have worked. Choosing the portable option costs a little and removes a whole class of breakage.

**Check the dependency, not just the script.** "If the script errors because a package is missing, say so and stop" is a real instruction. Assuming pip will work is not.

**A missing capability is a finding.** Name it, say what it blocks, and say what would fix it. Do not write the instruction you wish were executable, and do not quietly drop the one that needed the tool.

**Watch for the harness-specific section that grows.** When a skill accumulates three of them, that is the honest cost of the assumptions it made, and it is usually a signal to rewrite the instruction to need less rather than to document each variant.

---

## The declaration

When you cannot establish what the harness has, say what you assumed — in the handback itself, not only in the files, because the user may read only your message.

> "Written assuming a filesystem, a shell, and no display. The packaging step is the part that breaks if that is wrong."

A stated assumption gets corrected before it ships. An unstated one ships.
