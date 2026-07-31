# Automation Brief: Incident response and postmortem

**Status:** Ready for planning

**In one line:** Handle production incidents from alert through resolution and postmortem publication.

---

## Purpose

**Result wanted:** Incidents get to the right responder fast, customers hear about it, and the postmortem actually gets written.
**For whom:** The on-call engineers, the support team, and customers on the status page.
**Why now:** ~12 incidents a month. Paging is manual and slow at night. Roughly half of postmortems are never written.
**Should it exist:** Confirmed.

## Boundary

**In scope:** Production incidents on customer-facing services, from alert to published postmortem.
**Out of scope:** Internal tooling outages, planned maintenance, security incidents (separate process, legal involvement).
**Must never happen:** No customer communication goes out without a named human approving the wording. No incident is closed without a severity recorded.
**Trade-offs allowed:** Paging speed matters more than paging precision — a false page at 3am is cheaper than a missed one.

---

## The work

**What happens:** A monitoring alert fires → severity is assessed → the right on-call is paged → the responder acknowledges and investigates → if customer-facing, support drafts a status page update and someone approves it → the incident is resolved and closed → within five working days a postmortem is drafted, reviewed, and published to the engineering wiki → action items are tracked to completion.

**Depends on what:**

| This | Needs this first | Why |
|---|---|---|
| Paging | Severity assessed | Severity determines who is paged and how hard |
| Status update | A human approves the wording | Hard rule |
| Postmortem draft | Incident closed with a timeline | Nothing to write from otherwise |
| Action item tracking | Postmortem published | Items come out of the postmortem |

**Can run at the same time:** Investigation and customer communication run in parallel once severity is known.
**"Finished" means:** For the response part — incident closed with severity recorded. For the postmortem part — published and action items filed. For the action items — all closed or explicitly dropped.

---

## Resources

**Inputs:** Monitoring alerts, the on-call rota, incident timeline, customer impact assessment.
**Outputs:** Pages, status page updates, a closed incident record, a published postmortem, tracked action items.
**Needs access to:** Monitoring, paging system, status page, engineering wiki, issue tracker.
**Contended:** The on-call engineer's attention during an incident. The engineering manager's review time for postmortems.

---

## Responsibility

| Job | Who | Notes |
|---|---|---|
| Owns incident response | Platform on-call | Rota, 24/7 |
| Owns customer communication | Support lead | Business hours; escalates to duty manager at night |
| Owns postmortems | Engineering manager | Business hours only |
| Owns action item completion | Team leads | Whoever owns the affected service |
| Can change the rules | Head of Engineering | |

---

## When it goes wrong

**Other routes:** If paging fails, fall back to the group chat channel and then to phone. If the status page is down, post to the support inbox auto-reply.
**Known exceptions:** No on-call assigned → page the engineering manager. Severity unclear → treat as high and downgrade later. Postmortem not drafted in five days → escalate to Head of Engineering.
**Safe stop:** For response — none, an incident cannot be abandoned. For postmortems — an incident may be explicitly marked "no postmortem required" by the engineering manager.

---

## Evidence

**Success looks like:** Time to acknowledge under 5 minutes; time to customer communication under 30 minutes for customer-facing incidents; postmortem completion rate above 90%.
**Recorded each run:** Alert time, page time, acknowledge time, severity, customer impact, resolution time, postmortem published date, action items opened and closed.
**Reviewed by:** Head of Engineering, monthly.

---

## Open questions

| Question | Who decides | Blocking? |
|---|---|---|
| OPEN: whether action item tracking should chase owners or just report staleness | Head of Engineering | no |

---

## Recommendations

1. **Postmortem completion is a people problem, not a tooling one.** Half are missing today; automating the reminder will not change that on its own.
2. **The paging fallback chain shares a failure domain** — group chat and the paging system are both third-party SaaS.
3. **"Severity unclear → treat as high"** will produce false high-severity pages. Accept that or define a middle case.
