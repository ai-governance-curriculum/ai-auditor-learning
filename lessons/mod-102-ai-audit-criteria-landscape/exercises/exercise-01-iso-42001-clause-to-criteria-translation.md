# exercise-01: ISO/IEC 42001 Clause-to-Criteria Translation

**Estimated effort:** 3 hours

## Objective

Translate a *clause range* of **ISO/IEC 42001:2023** plus a small set of **Annex A** controls into a working set of auditable criteria using the chapter-1 template. The deliverable is a criteria register (table or structured Markdown) a Stage-2 certification auditor could lift into their fieldwork plan.

## Prerequisites

- Chapter [`01-what-makes-a-criterion-auditable.md`](../01-what-makes-a-criterion-auditable.md).
- Chapter [`02-iso-42001-clauses-and-annex-a-to-criteria.md`](../02-iso-42001-clauses-and-annex-a-to-criteria.md).
- A working copy of **ISO/IEC 42001:2023** (purchased from ISO or obtained through institutional access). The exercise does *not* reproduce the standard text; cite clause numbers and the auditee's own words.
- Chapter [`01-third-line-scope-and-boundaries.md`](../../mod-101-audit-position-and-independence/01-third-line-scope-and-boundaries.md) for the role boundary with the architect (L50) and analyst (L15).

## Scenario

**Clarivista Health** is a fictitious US-based health-tech company deploying a clinical-decision-support AI product used by nursing teams in long-term-care facilities. It is in its first ISO/IEC 42001 certification cycle; the certification body is scheduled to perform Stage-1 in 90 days. Clarivista's CAIO and AIMS owner are your contacts; a second-line AI governance analyst has produced a draft AIMS documentation set. Clarivista's internal audit function (three auditors, one newly designated AI Auditor — *you*) is engaged to perform an **internal audit under clause 9.2** in advance of Stage-1 readiness.

The in-scope clauses for this exercise:

- **Clause 4** — Context of the organisation (4.1 external/internal issues; 4.2 interested parties; 4.3 AIMS scope; 4.4 AIMS requirements).
- **Clause 5** — Leadership (5.1 leadership and commitment; 5.2 AI policy; 5.3 roles, responsibilities, authorities).
- **Clause 6.1** — Actions to address risks and opportunities (6.1.1 general; 6.1.2 AI risk assessment; 6.1.3 AI risk treatment; 6.1.4 AI system impact assessment).

Plus **Annex A** controls in these families (pick at least three controls from each family):

- Policy and organisational.
- AI system life cycle (requirements, design, verification/validation).
- Data for AI systems.

## Deliverables

1. **Criteria register** — a table or structured Markdown with one row per criterion, using every field of the chapter-1 template:
   - Criterion ID (stable, e.g. `C-42001-6.1.2-01`).
   - Source clause or Annex A control, with precise citation.
   - Statement (testable, present-tense, single-assertion).
   - Evidence (expected artifacts, named concretely).
   - Procedure (inquiry / observation / inspection / re-performance; sampling basis if applicable).
   - Measurable attributes (how the criterion is scored).
   - Source hierarchy (per ISA 500 analogy — rank the expected evidence).
   - Owner (first/second line, named role or function).
   - Residual judgment (where professional skepticism remains).
   - Period (point-in-time or period-of-coverage).
2. **Coverage note** (~300 words). Enumerate which sub-clauses you *did not* translate and why — exclusions must be defensible. Flag any sub-clauses where the standard is ambiguous enough that your criteria carry more professional judgment than you are comfortable with.
3. **Role-boundary note** (~200 words). State explicitly what the AI Auditor is *not* producing (the architect's control library; the analyst's raw crosswalk). Reference the corresponding roles (`senior-ai-governance-architect` L50, `ai-governance-analyst` L15).

## Minimum volume

- At least **12 criteria** across clauses 4–6.1 (do not spread thinner than that).
- At least **9 criteria** across the Annex A selection (three per family).
- At least **three measurable** criteria somewhere in the set (do not author only procedural).
- At least **one criterion** that requires an auditor's expert under ISA 620 analogy — flag it explicitly.

## Starter guidance

- Start with clause 4.3 (scope). A weak scope definition propagates into every downstream clause. Make it the first criterion.
- For clause 5.2, do not duplicate ISO 27001 policy criteria — focus on what is AI-specific (AI purpose, applicable regulatory landscape for Clarivista's clinical-decision-support context, communication to clinical users).
- For clause 6.1.2, separate the *process* criterion (is there a process) from the *execution* criterion (has it been executed in the period on the AI systems in scope). Split criteria produce clearer findings.
- For clause 6.1.4 impact assessment, cross-reference to ISO/IEC 42005 (impact assessment guidance). Do not write criteria that fight the ISO/IEC 42005 method — align.
- For Annex A data-governance controls, remember Clarivista is a clinical-decision-support product: PHI handling and HIPAA posture ride along; flag it in the residual-judgment column but do *not* expand criteria into HIPAA — overlay comes in exercise 04.
- Keep evidence names concrete. "Documentation" is not an evidence name; "AI policy v1.3 approved 2026-03-11" is.

## Acceptance criteria

The deliverables are accepted when:

- Every row of the criteria register uses the full chapter-1 template; no field is blank.
- Every statement is a single assertion in present tense, auditable by a documented procedure.
- Every criterion names a specific source clause with sub-clause or Annex A control ID; no "Clause 6" without a sub-clause.
- The register contains the minimum volume stated above.
- At least three measurable criteria carry tolerance / method / population explicitly.
- At least one auditor-expert-dependent criterion is flagged and the expert scope named.
- The coverage note names excluded sub-clauses and defends each exclusion against the audit scope.
- The role-boundary note names the architect's control library as an input and the analyst's crosswalk as an input, with the auditor's deliverable distinct from both.
- No regulatory standard, clause number, or Annex A control is invented or misnamed; where you are not sure, mark `<!-- needs-research: ... -->`.

## Stretch goals

- Add a **sampling plan** column that for each criterion names the sampling population (e.g., Clarivista's AI systems, model versions deployed in period, risk-register entries) and a sampling basis (judgmental / statistical, sample size rationale) per ISA 530 analogy.
- Produce a **second register** of Annex A controls Clarivista could reasonably exclude from the Statement of Applicability, with specific justifications a Stage-1 auditor would accept.
- Add a **readiness traffic-light** column (ready / partial / not ready) with a one-line evidence basis per row, so the engagement memo to Clarivista management can be produced directly from the register.
- Draft the **clause 9.2 internal audit report** section that the register would populate — without executing fieldwork, structure the report shape.
