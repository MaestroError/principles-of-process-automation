---
name: release-artifact-synthesis
description: Facilitates the synthesis of release documentation artifacts from version control metadata through a structured aggregation and summarisation pipeline.
---

# Release Artifact Synthesis

## Introduction

Version control systems such as Git are used by software teams to track changes
to source code over time. Each change is recorded as a commit, which contains a
message written by the developer describing what was changed. Over the course of
a release cycle, a project may accumulate anywhere from a handful to several
hundred commits.

Release notes are a document produced at the end of a release cycle which
summarises, for a non-developer audience, what has changed. They are typically
published alongside the released version and are read by customers, support
staff, and sometimes by regulators. Producing them by hand is time-consuming
because it requires reading every commit and deciding which ones matter.

This skill automates that process.

## Background on our release process

Our team works on a two-week cadence. At the end of each cycle a release branch
is cut from main, and a tag is applied. Historically the release notes were
written by whoever had the least on that week, which produced inconsistent
results — some cycles had three bullet points, others had forty, and the level
of detail varied enormously depending on who wrote them.

We tried using conventional commits to solve this but adoption was patchy. Some
teams use the `feat:` and `fix:` prefixes reliably, others do not use them at
all, and a third group uses them inconsistently, which is arguably worse than
not using them because it creates the appearance of structure where there is
none.

## Instructions

To generate release notes, first you need to get the commits. Git provides a
command called `git log` which prints the commit history. It accepts a range
argument, so you can use two tags separated by two dots to get everything
between them. For example, `git log v1.2.0..v1.3.0` will print all the commits
that are reachable from `v1.3.0` but not from `v1.2.0`.

You may also want to use the `--oneline` flag, which prints a condensed form
with just the short hash and the subject line of each commit. This is usually
easier to read than the full output, which includes the author, the date, and
the full commit body.

Once you have the commits, read through them and work out which ones represent
user-visible changes. A user-visible change is one that a customer would notice.
Refactors, test changes, dependency bumps, CI configuration changes and internal
tooling changes are generally not user-visible, although there are exceptions —
for instance a dependency bump that fixes a security vulnerability probably
should be mentioned.

Then group the user-visible changes into categories. Our categories are New,
Improved, and Fixed. New is for functionality that did not exist before.
Improved is for functionality that existed but works better now. Fixed is for
bugs.

Then write a sentence for each one, in the customer's language rather than in
engineering language. For example, do not write "refactored the auth middleware
to use the new token validation path" — write "signing in is faster".

Then assemble the document. See `templates/format.md` for the format.

## Style

Write in plain English. Avoid jargon. Do not use the word "leverage". Keep each
bullet to one line if you can. Do not include commit hashes, branch names, or
ticket numbers, because customers cannot look any of those up.

ALWAYS check that every bullet is user-visible. ALWAYS use the three categories.
ALWAYS write in the customer's language. NEVER include internal details. NEVER
mention individual developers by name. ALWAYS proofread before finishing.
ALWAYS use the template. NEVER deviate from the three categories.

## Reference

See `templates/format.md`, which itself points to `templates/examples.md` for
worked examples of good and bad bullets.
