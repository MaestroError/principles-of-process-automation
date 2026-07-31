# Automation Brief: Supplier invoice intake and routing

**Status:** Blocked on open questions

**In one line:** Take invoices arriving by email, check them against the purchase order, and route them to the right approver.

---

## Purpose

**Result wanted:** Invoices reach the correct approver within one working day of arrival, with duplicates caught before anyone sees them.
**For whom:** The finance team, and suppliers currently waiting weeks to be paid.
**Why now:** ~400 invoices a month, current routing takes 4–9 days, and a duplicate payment of £40k went out last year.
**Should it exist:** Confirmed. Challenged on whether the delay is really in routing rather than approver response — it is both, but routing is the part finance controls.

## Boundary

**In scope:** Supplier invoices arriving at the shared finance mailbox that reference a purchase order.
**Out of scope:** Expense claims, card spend, invoices with no purchase order (these go to manual handling), payment execution itself, and any change to supplier bank details.
**Must never happen:** No invoice is ever routed or paid twice. No payment is prepared for a supplier whose bank details changed within 30 days.
**Trade-offs allowed:** Speed may be traded for certainty on the duplicate check — that check may never be skipped to hit a time target.

---

## The work

**What happens:** Invoice arrives by email → matched to a purchase order → duplicate check → routed to the approver who owns that budget line → approver approves or queries → approved invoices go to the payment run.

**Depends on what:**

| This | Needs this first | Why |
|---|---|---|
| Routing | Purchase order matched | Approver is determined by the budget line on the PO |
| Routing | Duplicate check passed | A duplicate must never reach an approver |
| Payment run inclusion | Approval recorded | Out of scope for this automation but constrains "finished" |

**Can run at the same time:** Matching and duplicate checking are independent of each other.
**"Finished" means:** Invoice is routed to a named approver, or parked with a stated reason.

---

## Resources

**Inputs:** Invoice emails and attachments, purchase order records, the budget-line-to-approver mapping.
**Outputs:** Routed invoices, parked invoices with reasons, a decision record per invoice.
**Needs access to:** Finance mailbox, accounting system of record.
**Contended:** The finance team is four people; two handle invoice intake.

---

## Responsibility

| Job | Who | Notes |
|---|---|---|
| Owns the outcome | Dana (Controller) | |
| Can change the rules | Dana | |
| Approves an invoice | Whoever owns the budget line | **See open questions — the mapping is not current** |
| Picks up escalations | **OPEN** | |

---

## When it goes wrong

**Other routes:** Manual routing by the intake team, using the same accounting system.
**Known exceptions:** No matching purchase order → park for manual handling. Duplicate suspected → park and notify. Supplier bank details changed recently → park, do not route.
**Safe stop:** **OPEN — see below.**

---

## Evidence

**Success looks like:** Median time from arrival to approver under one working day; zero duplicate routings.
**Recorded each run:** Match result, duplicate check result, approver routed to, parking reason if parked.
**Reviewed by:** Dana, weekly.

---

## Open questions

| Question | Who decides | Blocking? |
|---|---|---|
| OPEN: the delegation-of-authority matrix dates from 2021 and does not map budget lines to current people. Routing cannot be specified without it | Dana + CFO | **yes** |
| OPEN: when both intake staff are away, who picks up escalations? There is currently no cover | Dana | **yes** |
| OPEN: is stopping allowed? If the automation cannot route safely, may it park everything and do nothing, or must it always route somewhere? | Dana | **yes** |
| OPEN: invoice volume is an estimate; nobody has measured it | Dana | no |

---

## Recommendations

1. **The 2021 authority matrix is the real blocker.** Automating routing onto an out-of-date mapping builds a fast machine for asking the wrong person.
2. **The duplicate that got through was a re-sent PDF**, not a repeated invoice number. Checking the number alone would not have caught it.
3. **A touchless-percentage target would fight the duplicate rule.** If that measure is introduced, state that the rule wins.
