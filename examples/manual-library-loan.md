# Process Specification: Paper-based library loan

**Kind:** Prescriptive, illustrative. **Version:** 1.
**Boundary:** From a loan request at the lending desk to an issued loan, recorded refusal, or pending request. All activity, ownership, escalation, and review roles are performed by people using paper records. No software execution is assumed.
**Authority source:** The library's approved lending policy. Local values below are example requirements.

## Objective

Lend an eligible item to an eligible member with a traceable due date. Include ordinary circulating items; exclude reference-only and restricted items. Do not release an item without eligibility and a completed loan record. Queue speed cannot override those requirements.

Success is an authorized loan with item/member identifiers and a due date recorded before release. A recorded refusal under policy or pending eligibility review is also an acceptable ending. This specification does not require lending every requested item.

## Occurrence

A member requests a loan while the lending desk is open. The clerk has the item, membership evidence, and current paper register. The approved lending policy authorizes the clerk to issue loans only when its eligibility conditions hold.

Reassess eligibility if the member or item record changes before release. Suspend issuance if required records are missing or contradictory. Resume after the relevant facts and authority are confirmed. At closing, unresolved requests become recorded pending requests; the item remains in library custody.

## Order

| Activity | Prerequisite | Responsible role | Acceptance condition |
|---|---|---|---|
| Establish eligibility | Item and membership records available | Lending clerk | Both meet policy, or a dispute is identified. |
| Decide disputed eligibility | Escalation acknowledged | Lending supervisor | Policy-grounded decision with reason recorded. |
| Record loan | Eligibility confirmed | Lending clerk | Item, member, due date, and clerk identity recorded. |
| Release item | Complete loan record | Lending clerk | Register and item custody agree. |

Different requests may be checked concurrently, but only one clerk may update a particular register entry at a time. Clerks share the paper register in arrival order; the supervisor resolves contention. A request's state is received, checking, pending, refused, or issued. Only confirmed eligibility permits checking/pending → issued.

## Option

If eligibility is uncertain, do not infer it from the length of the queue. Transfer the dispute using the contract below. If the paper register is unavailable, hold issuance pending restoration; memory is not an authorized replacement. A disputed loan cannot be issued as a fallback.

**Escalation contract:** The lending supervisor is the recipient for disputed eligibility and may interpret the policy but cannot waive its exclusions. During opening hours, the supervisor acknowledges verbally and initials the paper request within 15 minutes. The clerk supplies item/member records, checks performed, the conflicting facts, and the decision needed. Responsibility for the eligibility decision transfers on acknowledgment; the clerk retains item custody until authorized release.

If the supervisor is absent or the dispute remains unresolved at closing, the clerk marks the request pending, records the reason and the next open-desk review date, and retains the item. No repeated transfer loop or promised loan is created. A member may withdraw the request, which closes it without issuing the item.

Record disputed decisions, missing records, and held requests in the exception book for the weekly review. These do not each require an immediate call to the process owner.

## Observation

The paper loan register and exception book are the evidence. Entries identify the request, relevant item/member records, disposition, date, responsible clerk, and any supervisor decision. Keep them accessible to the reviewing roles for the retention period established by library record policy; a missing retention rule is a governance gap to resolve before adoption.

The supervisor checks unresolved requests on the next open-desk day. The process owner reviews pending age and repeated eligibility disputes weekly, and changes in these patterns monthly. Continued disagreement with library policy triggers reassessment of the procedure rather than an unauthorized change to eligibility.

## Roles, resources, and revision

| Role | Assignment | Authority and availability |
|---|---|---|
| Activity operator | Lending clerk on the desk rota | Check and issue within lending policy; present during desk hours. |
| Escalation recipient | Lending supervisor on duty | Resolve disputed eligibility within policy; use the Option contract. |
| Process owner | Library services manager | Review performance and revise desk procedure within approved policy; weekly review. |

The library's governing body retains authority over lending policy and wider organizational accountability. The owner cannot waive restrictions reserved to that body. The owner dates procedure revisions and briefs clerks and supervisors before they take effect.

Objects are items, member records, requests, and loan/exception entries. Resources are clerk and supervisor capacity, secure item custody, the paper register, and lending policy. Missing required resources prevent issuance; holding an item still requires safe custody.

## Open assessment item

Confirm the applicable record-retention rule and sufficient clerk/supervisor coverage before using this illustrative specification. Their presence in the document does not establish actual availability.
