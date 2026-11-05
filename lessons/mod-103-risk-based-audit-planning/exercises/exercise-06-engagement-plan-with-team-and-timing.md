# exercise-06: Engagement Plan with Team, Timing, and Coordination

**Estimated effort:** 2.5 hours

## Objective

Convert a chapter-4-style scope memo into a complete engagement plan under chapter 6, covering team composition, timing, logistics, information-request list, interview schedule, evidence-request shape, escalation path, and kickoff / closing meeting agendas. Then author the chapter-7 CAE-facing briefing that would surround the engagement — the AI-audit workstream input into one quarterly audit-committee report and the one event-driven escalation memo the engagement produced during fieldwork.

## Prerequisites

- Chapter [`06-engagement-plan-authoring.md`](../06-engagement-plan-authoring.md)
- Chapter [`07-audit-committee-and-cae-coordination.md`](../07-audit-committee-and-cae-coordination.md)
- Chapter [`04-scoping-a-single-ai-system-engagement.md`](../04-scoping-a-single-ai-system-engagement.md)
- Either exercise-04 (external AT-C 205) or exercise-05 (internal clause-9.2) as the engagement whose plan this exercise authors

## Scenario

Pick one of the following to be the subject engagement. The plan you author will reflect the engagement type you pick.

- **Option A** — The AT-C 205 examination of **StreetGuide / PathFind** from exercise-04. Big-4 or mid-tier firm; external assurance posture. Audit committee of interest: the engaging party's management-plus-advisory-board (no SEC audit committee).
- **Option B** — The internal-audit variant of the AIMS audit at **Meridian Logistics** from exercise-05 (E-C). Internal audit function reporting to the Meridian Audit Committee; CAE based in Rotterdam.

Both options share the planning facts below, adapted to the engagement:

- Engagement is approved in the FY27 plan (exercise-02-style outcome).
- Lead AI Auditor is a senior practitioner (level 45, this track).
- The engagement team has two audit staff available but has not yet confirmed a specialist roster.
- An ISA 620 ML specialist is required; a legal specialist is needed for regulatory classification (Colorado AI Act applicability for Option A; EU AI Act classification challenge for Option B).
- The firm's / function's EQR pool has two candidates; one has prior involvement with the client (Option A) or with the business unit (Option B).
- Fieldwork window: 6 calendar weeks; report due 10 weeks from kickoff.

## Mid-engagement complication — pick one

Introduce *one* of these into the engagement for the chapter-7 escalation memo requirement:

- **M-1** — Two weeks into fieldwork, the responsible party refuses to produce inference-log extracts citing a "live legal matter". Legal counsel has been engaged but will not clarify timeline.
- **M-2** — The ISA 620 ML specialist discovers mid-engagement that they held a six-month consulting engagement with the subject system's team 20 months ago. They did not flag it at acceptance.
- **M-3** — A regulator opens an inquiry into the responsible party on a subject-matter-adjacent concern (DPA inquiry for Option B; EEOC Charge for Option A). The regulator asks whether an audit is in progress.

## Requirements

1. **Engagement plan** — in the chapter-6 nine-element structure. Deliver:
    - Team-composition table with named roles, credentials, hours, and the independence-check outcome for each role (including the ISA 620 specialist and the EQR candidates)
    - Full-week timeline Gantt (Markdown-table or ASCII) covering pre-engagement → fieldwork → prelim findings → factual clearance → reporting → post-issuance
    - Logistics plan (on-site days, secure-environment access provisioning, confidentiality posture)
    - Information-request list with at least 40 line items in the chapter-6 §4 shape (ID, criterion, artifact, owner, due, format, status)
    - Interview schedule covering chapter-6 §5 roles, with per-interview duration and preparation requirements
    - Evidence-shape conventions and explicit rejection posture
    - Escalation path per trigger with decision owner and channel
    - Kickoff-meeting agenda and closing-meeting agenda, each with attendees, outputs, and minute template
2. **Quarterly audit-committee briefing input** — the one-to-two-page AI-audit section of the quarterly CAE report that would land during the fieldwork window. In the CAE's voice; chapter-7 §3.2 shape.
3. **Event-driven escalation memo** — the chapter-6 §8 / chapter-7 §3.3 escalation memo for the complication you chose. Include trigger description, immediate impact, recommended action, decision owner, communication channel, and the information the audit committee needs (or does not yet need) to know.

## Starter guidance

- Team composition: the EQR is **not** on the engagement team; if your two EQR candidates both have independence issues, you escalate rather than accept a flawed EQR.
- Independence check per team member: pre-engagement, pre-acceptance. Do not defer to "will confirm later".
- ISA 620 scoping: name the specialist's procedures, the auditor's direction, and the auditor's use of the work (adoption vs. re-performance vs. reliance-with-disclosure).
- IRL: 40 items is a floor. Aim for clarity per item — "eval suite config YAML for model version X.Y as deployed between D1 and D2" beats "all eval evidence".
- Interview schedule: ML engineers and product owners have the tightest calendars; book first.
- Evidence rejection: screenshots, verbal confirmations, post-sample-date-backfilled documents.
- Escalation path: every trigger named in chapter 6 §8 should appear, with the specific decision owner for *this* engagement type.
- Kickoff and closing: do not leave agenda items out. The responsible party reads these in advance.
- For the quarterly CAE briefing input, write in the CAE's voice and keep it enterprise-level — do not slip into practitioner-detail. The AI Auditor's job in exercise-02 was to feed the CAE; same discipline here.
- For the escalation memo, the recommended action must fit the chapter-6 §8 pattern for that trigger. A regulator inquiry (M-3) runs through legal counsel; a mid-engagement independence failure (M-2) is a documented remove-and-replace plus consideration of rework; evidence refusal (M-1) can rise to a scope limitation under ISAE 3000 paragraph 73 (Option A) or an internal audit charter escalation (Option B).

## Acceptance criteria

- The engagement plan contains every chapter-6 element.
- Team composition names credentials, hours, and independence-check outcome per role; the EQR independence constraint is addressed, not ignored.
- The IRL has at least 40 items, each with artifact, owner, due date, format, and criterion traceability.
- The interview schedule covers top management, first-line engineers, second-line governance, and prior internal audit.
- The escalation path addresses at least five chapter-6 §8 triggers with named decision owners.
- The kickoff and closing agendas are executable, not abstract.
- The quarterly CAE briefing is in the CAE's voice, keeps to enterprise language, and stays within the two-page cap.
- The escalation memo matches the chapter-6 §8 / chapter-7 §3.3 pattern for the chosen complication, including whether the audit committee is informed now, later, or at the next quarterly cycle.
- The engagement-type-specific standards (AT-C 105 / 205 for Option A; IIA Standards 2024 for Option B) are correctly cited.
- No fabricated law-firm names, specific statute numbers not previously cited, or firm-independence rulings.

## Stretch goals

- Author a **debrief and lessons-learned template** the engagement team will complete after issuance, feeding the audit function's quality-assurance programme (IIA Domain II; ISQM 1 for external engagements).
- Produce the **external-assurance-map update** the CAE would publish after this engagement closes, showing how the engagement affects reliance decisions on neighbouring engagements in the next cycle.
- Draft a **change-management memo** for the approved plan if the mid-engagement complication forces the audit function to drop or delay another engagement in the FY27 plan — in the chapter-7 §3.3 shape.
