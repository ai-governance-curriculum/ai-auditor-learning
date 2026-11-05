# exercise-06: IAASB AI Assurance Pipeline + AICPA SOC-for-AI — Standards Read

**Estimated effort:** 2 hours

## Objective

Read the **currently published IAASB and AICPA assurance literature** relevant to AI attestations and produce (a) a concise standards map, (b) a professional-judgment notebook for the specific areas where the standard is immature, and (c) an engagement-letter paragraph suite for a representative AI examination that cites the current standards precisely. The focus is *read and apply*, not design; this exercise sharpens the methodology layer the rest of the module depends on.

## Prerequisites

- Chapter [`07-iaasb-aicpa-ai-assurance-standards.md`](../07-iaasb-aicpa-ai-assurance-standards.md).
- Chapter [`05-iaasb-and-aicpa-attestation-stack.md`](../../mod-101-audit-position-and-independence/05-iaasb-and-aicpa-attestation-stack.md).
- **Live** IAASB and AICPA resources to pull at reading time:
  - IAASB: International Framework for Assurance Engagements; ISAE 3000 (Revised); ISAE 3402; ISA 500, 530, 620, 320; ISQM 1, ISQM 2; **ISSA 5000**; any IAASB consultation paper or exposure draft referencing AI assurance.
  - AICPA / ASEC: AT-C 105, 205, 210, 215; Trust Services Criteria; QM 1 / QM 2; **any published or exposed AI-specific criteria or SOC-for-AI materials**; the AICPA Code of Professional Conduct Independence section.
- One completed criteria register from exercises 01–03 of your choice (as the backdrop for the engagement-letter paragraphs).

## Scenario

**Northfield Trust Partners** is a fictitious mid-tier US CPA firm. Its Assurance Practice is evaluating an engagement opportunity with **Lexora Financial Analytics**, a GenAI-enabled financial-analytics service provider. Lexora wants an examination-level report its enterprise customers can rely on. The firm's partner is weighing three possible engagement forms:

- **A** — a **SOC 2 Type II** with AI-specific Additional Suitable Criteria.
- **B** — a bespoke **AT-C 205 examination** over Lexora's AI safety-and-governance program, with criteria drawn from NIST AI RMF 1.0 + the GenAI Profile and Lexora's own control framework.
- **C** — a **limited-assurance ISAE 3000** engagement for a European customer that wants a report under IAASB methodology rather than AICPA.

You are the manager drafting the methodology-stack recommendation and the engagement-letter paragraphs for each option.

## Deliverables

1. **Standards map** (~500 words, structured list acceptable) — for each option A/B/C:
   - The primary standard(s) cited.
   - The supporting standards applied by analogy (ISA 500 / 530 / 620 / 320; AT-C 105 .25 etc.).
   - The firm quality-management standards that apply (ISQM 1/2 or QM 1/2).
   - The level of assurance and the reporting-language shape.
   - The criteria source and the suitability test under the standard's paragraph.
2. **Pipeline notebook** (~500 words). For each of the four "immaturity" areas in chapter 7 (no AI-specific methodology standard; suitable criteria still forming; measurement methods still forming; no regulator with final interpretive authority), describe:
   - What Lexora's engagement would do today under the existing framework.
   - What would change once the pipeline items land (IAASB AI standard, AICPA SOC for AI, EU harmonised standards).
   - What the workpaper citation strategy should be *now* to minimise re-work when the pipeline lands.
3. **Engagement-letter paragraph suite** — draft the following paragraphs for Option B (AT-C 205 bespoke examination) so the partner can turn them into a signed letter:
   - Subject matter paragraph.
   - Criteria paragraph, citing both the baseline NIST framework and the specifically developed Lexora criteria, and testing suitability under AT-C 105 .25.
   - Responsibility paragraph (responsible party's; auditor's).
   - Inherent-limitations paragraph that names AI-specific limits (eval-method constraints, auditor's expert reliance, point-in-time vs. period subject matter).
   - Reporting paragraph describing the AT-C 205 positive-assurance conclusion.
   - Auditor's-expert paragraph under the ISA 620 analogue.
4. **Independence memo** (~400 words) addressing the AICPA independence posture under the Code of Professional Conduct for an AI examination, specifically flagging:
   - The self-review risk if the firm has previously advised Lexora on its control framework or eval methodology.
   - The management-decision line (what the firm cannot opine on if the firm's consulting side has made model-design, dataset-selection, or incident-response decisions).
   - The firm's use of AI tools (document-review LLMs, workpaper-summarisation AI) during the engagement and how that interacts with the firm's professional-skepticism policy.

## Minimum volume

- Standards map must reference at least **10 distinct standards** across the three options.
- The pipeline notebook must cover all **four** immaturity areas.
- The engagement-letter paragraph suite must contain all **six** named paragraphs.
- The independence memo must address all **three** named sub-topics.

## Starter guidance

- The standards map's value is precision, not length. One sentence per cited standard describing what it does for the engagement.
- For Option A (SOC 2 + AI-specific additions), remember that AICPA Trust Services Criteria remain the primary criteria; AI-specific criteria are *Additional Suitable Criteria* under AT-C 105. Do not mis-cite.
- For Option C (ISAE 3000 limited), the conclusion language is negative-form; do not slip into AT-C 205 positive-form prose.
- The criteria paragraph must apply all five AT-C 105 .25 suitability tests when the engagement uses specifically developed criteria, and must disclose the criteria in the report.
- The inherent-limitations paragraph is where you preserve honesty about AI methodology constraints — this is also where the professional-skepticism posture lives in writing.
- For the auditor's-expert paragraph, do not try to *contract* the expert in the engagement letter; the expert's role is described (to intended users) and the auditor's reliance arrangements are governed by firm policy and the ISA 620 analogue.
- The independence memo should name specific **threats** (self-interest, self-review, advocacy, familiarity, intimidation) per the IESBA Code structure and cite the AICPA Code's parallel sections where applicable.

## Acceptance criteria

The deliverables are accepted when:

- The standards map references at least 10 standards accurately and names each standard's role in the engagement.
- The pipeline notebook covers all four immaturity areas with a "today" / "post-pipeline" / "citation strategy" structure.
- The engagement-letter paragraph suite contains all six paragraphs; the subject-matter, criteria, and reporting paragraphs are consistent with AT-C 205 for Option B.
- The criteria paragraph cites AT-C 105 .25 and applies all five suitability tests.
- The inherent-limitations paragraph names at least three AI-specific limits.
- The independence memo names all five IFAC threat categories and the AICPA Code of Professional Conduct section(s) that bind the firm; the AI-tools-used-by-auditor sub-topic cites the firm's QM 1 policy by reference.
- Any reference to the current state of pipeline items (ISSA 5000 effective date; AICPA SOC-for-AI exposure draft status; IAASB AI-related projects) is marked `<!-- needs-research: ... -->` and the live source named.

## Stretch goals

- Produce the **three-way comparison table** of Options A/B/C across dimensions: level of assurance, standards stack, auditor-expert footprint, reporting audience, auditor-independence posture, cost shape.
- Draft the **partner's internal acceptance memo** justifying engagement acceptance under firm quality-management policy, naming the engagement partner, engagement quality reviewer, and expert leads.
- Write the **report "Other matters" paragraph** describing the immaturity of AI assurance standards in a form the firm is comfortable including in a distributed report.
- Draft the **client management-representation letter** for the AT-C 205 engagement, listing the AI-specific representations the responsible party will make.
