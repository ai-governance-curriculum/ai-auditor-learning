# exercise-01: ISO/IEC 42001 Clause-by-Clause Audit Procedure

**Estimated effort:** 3 hours

## Objective

Author the **clause-by-clause audit procedure workbook** the engagement team will use at Stage-2 against an ISO/IEC 42001:2023 AIMS. For each clause (4–10), produce an inspection-ready set of auditor procedures that an audit team member could execute without re-reading the standard — with requirements, evidence expectations, procedures, measurable attributes, and grading notes pinned to specific clause sub-paragraphs.

This is the Stage-2 workbook, not a theoretical exercise. The deliverable is intended to be carried into a real engagement and must survive peer review and independent-reviewer QA.

## Prerequisites

- Chapters [`01`](../01-iso-42001-audit-frame-and-conformity-assessment-cycle.md), [`02`](../02-nonconformity-grading-under-iso-17021-1.md), [`03`](../03-auditing-clause-4-and-5-context-scope-leadership-policy.md), [`04`](../04-auditing-clause-6-planning-risk-assessment-and-objectives.md), [`07`](../07-auditing-clause-8-operation-and-the-ai-life-cycle.md), [`08`](../08-auditing-clause-9-performance-evaluation-internal-audit-and-management-review.md), [`09`](../09-auditing-clause-10-nonconformity-corrective-action-and-improvement.md).
- `mod-102` chapter 2 — ISO/IEC 42001 clauses translated to criteria (template reference).
- `mod-104` chapter 1 — ISA 500 evidence discipline.
- Access to the ISO/IEC 42001:2023 standard (or your organisation's licensed copy) for reading the as-published clause text.

## Scenario

**Alcyon Insurance Group** is a mid-cap property-and-casualty insurer running its first ISO/IEC 42001 certification cycle. Its AIMS covers 11 AI systems: 4 underwriting models, 3 claims-triage models, 2 fraud-detection models, 1 customer-support assistant, 1 agent-productivity copilot. Scope is US (5 states) and EU (Ireland and Netherlands). The Alcyon risk function (second line) owns the AIMS; internal audit (third line) reports to the Audit Committee. Stage-1 was conducted six weeks ago and the Stage-1 report is on file.

You are leading the Stage-2 audit team. You have two weeks to prepare the clause-by-clause audit workbook for the fieldwork opening on 2026-11-30.

## Requirements

1. **Produce one workbook section per clause** (4.1, 4.2, 4.3, 4.4, 5.1, 5.2, 5.3, 6.1.1, 6.1.2, 6.1.3, 6.1.4, 6.2, 6.3, 7.1, 7.2, 7.3, 7.4, 7.5, 8.1, 8.2, 8.3, 8.4, 9.1, 9.2, 9.3, 10.1, 10.2). Each section carries:

   ```
   Clause:                 e.g., 6.1.2 AI risk assessment
   Standard text (brief):  Paraphrase of the as-published requirement (cite the paragraph).
   Audit criteria:         The testable statements (chapter 2 of mod-102 template).
   Expected evidence:      The specific artifacts the auditor expects to see.
   Audit procedures:       Numbered procedures (inspection, interview, observation, re-performance).
   Measurable attributes:  What the procedure measures (pass/fail, counts, percentages).
   Sampling note:          If applicable — how the sample is drawn.
   Grading notes:          What an isolated lapse grades; what a pattern grades; what a total absence grades.
   Workpaper refs:         Where the executed procedure lands in the engagement file.
   ```

2. **Pin each procedure to a specific clause sub-paragraph.** Vague procedures ("review the AI policy") are not acceptable; "Inspect the AI policy document against clause 5.2(a)–(d) completeness and (i)–(iii) communication requirements" is.

3. **Produce a one-page sampling-strategy annex** for the Stage-2 workbook covering: the AI system population (11 systems), the stratification strategy, the sample size per clause or per Annex A family (cite the Stage-1 plan).

4. **Produce a one-page interview-schedule annex** listing the interviews required to execute the workbook — role, purpose, the clauses the interview supports, and the expected duration.

5. **Produce a one-page "watch list" annex** capturing the Stage-1 areas-of-concern the Stage-2 workbook should reconfirm closure of (assume Stage-1 raised: a thin context analysis at 4.1 — observation only; a GPAI usage not reflected in 4.3 scope — material; and a management-review minute missing one required 9.3.2 input — observation only).

## Starter guidance

- The clause 5.2 policy walk in chapter 3 is the reusable *procedural shape* — one fixed checklist per clause element, present/absent/weak with evidence reference.
- Clause 6 procedures are the longest (risk assessment, treatment, SoA, impact, objectives) — budget workbook space accordingly.
- Every "inspect" procedure should name the artifact *and* the test applied to the artifact (completeness, consistency, traceability, freshness).
- Every "interview" procedure should name the interviewee's role, the questions, and the corroborating documentary evidence the auditor will request against the answer.
- Every "observation" procedure should name the control operation being observed and the specific attributes to record.
- Pin grading notes to chapter 2 patterns (major: absent, total breakdown, significant doubt, aggregation; minor: isolated lapse, sporadic deviation, documentation gap with underlying operation).
- Where the as-published standard text is unclear or you need to defer to a reader-time check, use `<!-- needs-research: ... -->` rather than invent.

## Acceptance criteria

The deliverable is accepted when:

- Every clause from 4.1 to 10.2 has its own workbook section with the fixed template.
- Every procedure references a specific sub-paragraph of ISO/IEC 42001 (not "clause 6" but "clause 6.1.2").
- Grading notes are present and align with chapter 2 definitions.
- The sampling annex names the stratification variables and the per-clause/family sample sizes.
- The interview annex has at least one interview per functional area: AIMS owner, top-management rep, internal audit lead, first-line ML lead (sampled), first-line product-engineering lead (sampled), compliance / privacy lead.
- The watch-list annex walks each Stage-1 area-of-concern to a specific workbook section for reconfirmation.
- No clause-level procedure is "inspect the <artifact>" with no test specified.
- `<!-- needs-research -->` placeholders appear where the as-published standard or a referenced auxiliary standard legitimately needs reader-time verification.

## Stretch goals

- Author the **workbook for the Annex A SoA sample** (which controls, drawn from which of the Annex A families, applied to which AI systems) and a per-control procedure template. Cross-reference to exercise-02.
- Author a **daily-standup template** the audit team uses to walk the workbook's day-by-day coverage, flagging aggregation candidates and watch-list reconfirmations.
- Propose the **evidence-request list** that goes to Alcyon three days before fieldwork opens, aligned to the workbook sections. Format as a professional information-request letter.
- Draft the **independent-reviewer handoff memo** — a one-pager that tells the independent reviewer under 17021-1 clause 9.5 how to trace from the clause workbook, through the evidence inventory, to the finding register. This is the artifact that most reduces independent-reviewer friction.
