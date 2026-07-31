# Automation Spec: Vendor security questionnaire drafting

**Status:** Ready to build

**In one line:** Draft answers to inbound vendor security questionnaires from our existing policy library, for a human to review before anything is sent.

---

## Objective

**Result:** A draft response to each questionnaire question, each answer traceable to a specific source document, ready for the security lead to review.
**Measured by:** Proportion of drafted answers accepted by the reviewer without edits; time from questionnaire receipt to sent response.

**In scope:** Questionnaires arriving from prospective customers during procurement.
**Out of scope:** Regulatory filings, audit responses, anything from an existing customer's legal team, and any questionnaire mentioning a specific incident.

**Must never happen:**
- No answer is ever sent without the security lead approving it.
- No answer asserts a control or certification we do not hold.
- No answer is drafted from general knowledge — every answer traces to a document in the policy library.

**Trade-offs, with floors:** Coverage may be traded for accuracy without limit. A questionnaire returned half-drafted with the rest marked unanswerable is a good outcome; a fully drafted one containing an unsupported claim is a failure.

**Stop criteria:** If the policy library does not cover a question, the answer is "no source found" — not an inferred answer.

---

## Occurrence

**Trigger:** A questionnaire arrives in the security review queue.
**Readiness:** The questionnaire is parsed into discrete questions; the policy library is reachable; the requesting deal is identified.
**Authorisation:** Drafting is unrestricted. Sending requires the security lead.
**Window:** None — drafts can be prepared at any time.

**Cases the input can take:** standard SIG-style questionnaire; a free-form list of questions in an email body; a spreadsheet with mixed questions and evidence requests; a questionnaire containing questions about a named security incident (out of scope, must be routed to the security lead untouched).

---

## Order

**Dependencies:** A question must be classified before it is answered — evidence requests are handled differently from policy questions. Every answer requires a located source before it is drafted.

**Automation levels:**

| Step | Collect | Interpret | Decide | Act |
|---|---|---|---|---|
| Parse questionnaire | auto | auto | auto | auto |
| Classify each question | auto | auto | auto | auto |
| Locate source in library | auto | auto | auto | auto |
| Draft answer | auto | auto | auto | auto |
| Approve and send | auto | human | human | human |

---

## Option

**Variants:** If no exact source exists, look for an adjacent policy and draft with an explicit note that it is adjacent, not direct.
**Exceptions:** Question about a named incident → do not draft, route whole questionnaire to security lead. Question needing a legal opinion → mark as legal review. Evidence request (asking for a document rather than an answer) → list the document name, do not attach.
**Recovery / safe stop:** Return the questionnaire partially drafted, with unanswered questions clearly marked. Always available.

---

## Observation

**Recorded per run:** Question count; answers drafted; answers marked no-source; answers drafted from an adjacent rather than direct source; reviewer edits per answer.
**Judged by:** Reviewer edit rate now; which question types consistently have no source (a library gap, not a drafting failure) accumulated; rising edit rate trending.

---

## Ownership

Security lead owns approval and the policy library. Nobody else may approve.
