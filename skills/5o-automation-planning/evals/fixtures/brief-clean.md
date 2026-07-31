# Automation Brief: Candidate screening and rejection

**Status:** Ready for planning

**In one line:** Screen inbound applications against a role's must-have requirements and prepare clear no-matches for human sign-off within 24 hours.

---

## Purpose

**Result wanted:** Every applicant hears back within 24 hours, without the false rejection rate rising.
**For whom:** Applicants, and the hiring managers whose queues are currently clogged with obvious no-matches.
**Why now:** ~700 applications a week, response time currently 6–11 days, candidates dropping out before first contact.
**Should it exist:** Confirmed. Challenged on whether a human sign-off on every rejection makes the automation pointless — no, it moves the cost from judging each application to confirming a prepared decision.

## Boundary

**In scope:** Applications arriving through the public careers page for roles that have structured must-have requirements defined.
**Out of scope:** Internal referrals, anything sourced by the exec search firm, leadership roles, and any req without structured must-haves — all route straight to the hiring manager unscreened.
**Must never happen:** No rejection is ever sent without a named human approving that specific candidate. No bulk-approve. No rejection on any attribute other than the stated must-haves.
**Trade-offs allowed:** The 24h target may slip to 48h if the sign-off queue backs up. Accuracy may not be traded at all.

---

## The work

**What happens:** Application arrives → source is classified → excluded sources route to the hiring manager untouched → remaining applications are checked against the role's must-haves → clear no-matches are queued for human sign-off with the reason shown → everything else goes to the hiring manager's review queue → approved rejections are sent as a templated email.

**Depends on what:**

| This | Needs this first | Why |
|---|---|---|
| Screening | Role has structured must-haves defined | Nothing to screen against otherwise |
| Rejection send | A named human has approved that specific candidate | Legal requirement, non-negotiable |
| Source classification | Application record complete | Determines whether it is screened at all |

**Can run at the same time:** Screening of different applications is independent.
**"Finished" means:** Every application from the period is either in the hiring manager's queue, or rejected with a recorded approver, or explicitly held.

---

## Resources

**Inputs:** Application records, role must-have definitions.
**Outputs:** Routed applications, prepared rejections, sent rejection emails, an audit record per decision.
**Needs access to:** The applicant tracking system — which is also the source of the trigger, the hiring manager queue, and the outbound email.
**Contended:** Ravi's attention. He is the only approver, at roughly 700 applications a week.

---

## Responsibility

| Job | Who | Notes |
|---|---|---|
| Owns the outcome | Ravi (Talent Ops) | |
| Can change the rules | Head of Talent | Must-haves are set per role by the hiring manager |
| Approves each rejection | Ravi | Business hours only; **no named cover when away** |
| Picks up escalations | Head of Talent | |

---

## When it goes wrong

**Other routes:** None that are independent. The tracking system is the trigger, the queue, and the outbound email — every fallback needs the thing that would have broken.
**Known exceptions:** Application with unclassifiable source → treat as excluded, route to hiring manager. Role with no structured must-haves → do not screen. Sign-off queue older than 48h → stop screening, let everything through to the hiring manager.
**Safe stop:** Stop screening and route everything to hiring managers unscreened. Explicitly allowed — a backlog of unscreened applications is recoverable, a wrong rejection is not.

---

## Evidence

**Success looks like:** Median time to first response under 24h; false rejection rate no higher than the pre-launch baseline.
**Recorded each run:** Source classification, screen result, which must-have failed, approver identity, time in sign-off queue, and whether the safe stop was triggered.
**Reviewed by:** Head of Talent, monthly, may change must-have definitions and the screening threshold.

---

## Open questions

| Question | Who decides | Blocking? |
|---|---|---|
| OPEN: no pre-launch baseline for false rejection rate exists yet | Head of Talent | no — measure during shadow run |
| OPEN: whether a recommend-to-human system counts as an automated employment decision tool in NY and the EU | Legal | no — checked in parallel with build |

---

## Recommendations

1. **Ravi is the whole automation.** One approver at 700/week is the throughput ceiling and the single point of failure. Name a deputy before launch.
2. **Run in shadow mode first** to establish the false rejection baseline that does not currently exist.
3. **The 24h target will fight the sign-off rule** under backlog. Decide now which wins — the brief says accuracy, so the target must be allowed to slip.
