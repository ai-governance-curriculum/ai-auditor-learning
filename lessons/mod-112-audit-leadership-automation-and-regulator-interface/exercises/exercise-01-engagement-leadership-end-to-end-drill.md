# exercise-01: Engagement Leadership End-to-End Drill

**Estimated effort:** 3 hours

## Objective

Lead an AI audit engagement from acceptance through archive for a realistic scenario. Produce the engagement letter, the work programme, the team deployment plan, the supervision plan, the scope-decision log entry for a mid-engagement change, the engagement-quality review note, and the closing-meeting agenda. Demonstrate that the engagement would withstand external quality assessment.

## Prerequisites

- Chapter [`01-leading-an-ai-audit-engagement.md`](../01-leading-an-ai-audit-engagement.md).
- Reading access to:
  - IIA Global Internal Audit Standards (2024) — Domain IV and Domain V.
  - IAASB ISAE 3000 (Revised) and ISQM 1.
  - ISO/IEC 17021-1 (and ISO/IEC 42006 where it applies) for AIMS engagements.
  - `mod-101` (independence), `mod-102` (criteria), `mod-103` (planning), `mod-104` (evidence and sampling), `mod-111` (findings / reporting).

## Scenario

**Company.** HarborPath Mutual, a mid-sized US property-and-casualty insurer, ~$3.2B premiums written, licensed in 23 states. HarborPath has been running an AI-assisted underwriting-triage model (`triage-score-v5.0`) for personal auto renewals since 2024-10 and recently extended the same model family to small-commercial auto renewals (`triage-score-v5.1`) in 2026-07. Both models are Class II under the NAIC Model Bulletin (where adopted at state level) and receive state DOI attention in Colorado and California.

**You.** The engagement lead inside HarborPath's internal audit function. Your CAE has approved a joint integrated engagement (ISO/IEC 42001-aligned AIMS audit *plus* an SR-11-7-shaped model risk review of `triage-score-v5.x`), to be conducted in Q1–Q2 2027. The engagement is planned for ~900 total hours across the engagement team.

**Known constraints.**

- The external financial auditor (a national firm) plans to rely on your work under ISA 610 / AICPA AT-C 105 for ICFR purposes where `triage-score-v5.x` affects reserving. A formal reliance evaluation is expected before fieldwork concludes.
- The California DOI has signalled an informal market-conduct review that will likely cover `triage-score-v5.0` in Q3 2027; any findings you produce will be read by that team.
- Your technical specialist pool is lean: one senior data scientist seconded from the risk function (independence constraints apply), one external contractor engaged for fairness-adjacent testing, and your administrative support is shared across three engagements.

## Deliverables

### 1. Engagement memorandum (~1.5 pages)

Draft the engagement memorandum the CAE will approve. Include:

- Engagement objective (stated in the shape of the audience's expected opinion type).
- Scope (systems, period, controls, locations).
- Explicit out-of-scope boundary statements.
- Criteria (ISO/IEC 42001 clauses; SR 11-7 sections; HarborPath AIMS policy references; any contractual commitments — invent plausibly, and flag anything you cannot verify with `<!-- needs-research: ... -->`).
- Team deployment (lead; technical specialists and their independence posture; independent reviewer; administrative support; planned hours per role).
- Milestones with entry / exit criteria.
- Dependencies (external-auditor coordination; CA DOI timing; third-party reliance decisions).
- Independence statement (yourself and each team member against each criterion; secondment rotation lock-out for the seconded data scientist).

### 2. Engagement work programme (~1 page)

Produce the work programme table that will drive fieldwork:

- At least 10 procedures covering both the AIMS (ISO/IEC 42001 clauses 5–10) and the model risk (SR 11-7 validation elements: conceptual soundness; ongoing monitoring; outcomes analysis).
- For each procedure: criterion reference, procedure description, evidence form expected, hours budgeted, preparer role, reviewer role.
- A change-control statement (threshold at which procedure changes require lead approval).

### 3. Daily / weekly supervision plan (~0.5 page)

Describe the operating rhythm:

- Daily stand-up structure, attendees, cadence.
- Weekly status content and distribution list.
- Review-point workflow for each workpaper (signatures, review notes, resolution).
- How you will supervise the technical specialists' work at a professional-skepticism standard, including the "second look" protocol for specialist conclusions you cannot fully evaluate first-hand.

### 4. Scope-decision log entry — mid-engagement change (~0.5 page)

Mid-engagement scenario (invent plausibly): the product team announces, three weeks into fieldwork, that `triage-score-v5.2` (expanded to tenant-insurance lines) will release to production in 2027-05 — before your fieldwork ends but after your current scope was set. Produce the scope-decision log entry documenting:

- Request, date, requester.
- Impact analysis (hours; team capacity; dependencies).
- Your decision (include in scope / defer to next engagement / out of scope) with reasoning.
- Sponsor acknowledgement path.
- Impact on budget and timeline.
- Impact on the external-auditor-reliance posture.

### 5. Engagement-quality review note (~0.5 page)

Role-swap: you are now the EQR reviewer, independent of the engagement team. Produce the EQR note before the report issues. Include:

- Three specific judgements the engagement lead made that you tested against the standard — one you concurred with, one you asked for additional work on, one you left as an open note the lead must resolve.
- Your conclusion on whether the engagement can issue.
- Your documentation of your independence as reviewer.

### 6. Closing-meeting agenda and walk-through notes (~0.5 page)

Produce the closing-meeting materials:

- Attendee list (named roles) with reasoning for inclusion / exclusion.
- Agenda with time boxes.
- A walk-through script for one finding (any plausible finding from your work programme) covering CCCER plus management response and CAP.
- Minutes template showing what will be captured and signed.

## Starter guidance

- The engagement is a joint integrated engagement. The memorandum should make clear how the ISO 42001 and SR 11-7 outputs are reconciled (one engagement, two reporting shapes, or one combined report with annex — decide and justify).
- The seconded specialist introduces a real independence question. Cite `mod-101` and state the specific rotation lock-out and the specific procedures the specialist may not perform.
- The external-auditor reliance in ISA 610 / AT-C 105 shape puts your work under external review. Design your work programme assuming the reliance partner will inspect procedure design.
- The California DOI signal should shape documentation discipline more than scope — anticipate that your findings may be visible to the DOI.
- Do not treat the EQR note as a formality. The EQR note is where external QA often finds holes; write it with the professional-skepticism posture the standard requires.

## Acceptance criteria

The deliverables are accepted when:

- The engagement memorandum states the audience's expected opinion type, specifies scope with explicit out-of-scope boundaries, cites criteria at clause level (or carries `needs-research`), composes a team with explicit independence posture per member, and names milestones with entry/exit criteria.
- The work programme contains at least 10 procedures covering both AIMS and SR 11-7 elements, with full field population per procedure and a change-control threshold.
- The supervision plan describes a daily and weekly cadence, a review-point workflow with signatures, and a specialist "second-look" protocol.
- The scope-decision log entry documents the request, impact, decision, reasoning, sponsor acknowledgement, and external-auditor impact — and the decision is defensible on its stated basis.
- The EQR note demonstrates independent review by surfacing concurred, remediated, and open judgements, with reviewer independence documented.
- The closing-meeting materials include named attendees with inclusion reasoning, a time-boxed agenda, a complete walk-through script for one CCCER-structured finding, and a minutes template.
- Independence considerations for the seconded specialist are specifically addressed — rotation lock-out and constrained procedures — not treated as a formality.
- No citation is invented; unverified citations carry `needs-research`.

## Stretch goals

- Author the **draft engagement letter** (~0.5 page) the CAE will send to HarborPath senior management, including scope, deliverables, independence statement, and the committee's acknowledgement line.
- Draft the **mid-engagement status update** the audit committee will see at its next meeting while the engagement is still in fieldwork — one-page summary content per chapter 8's shape.
- Draft the **external-auditor reliance package** (a short memo and an exhibit list) the external financial auditor would receive to begin its ISA 610 / AT-C 105 reliance evaluation of your function and this engagement.
- Produce the **archive manifest** that will be stored at engagement close, enumerating workpaper IDs, their classification, retention category, and access rules.
