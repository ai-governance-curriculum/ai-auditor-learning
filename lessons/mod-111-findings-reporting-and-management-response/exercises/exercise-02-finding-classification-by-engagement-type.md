# exercise-02: Finding Classification by Engagement Type

**Estimated effort:** 2 hours

## Objective

Given a single underlying observation about an AI system, classify it correctly across five different engagement shapes — ISO/IEC 17021-1 AIMS audit, SR 11-7 MRM validation, SOC 2 Type II, ForHumanity IAAIS, and NYC Local Law 144 — using each scheme's **own** severity vocabulary. Produce classification rationales that cite the scheme's governing clause or published rule.

## Prerequisites

- Chapter [`02-classifying-findings-across-engagement-shapes.md`](../02-classifying-findings-across-engagement-shapes.md)
- Access to:
  - ISO/IEC 17021-1:2015, especially clause 9.4.9 (nonconformity grading)
  - ISO/IEC 42001:2023
  - Federal Reserve SR 11-7 and OCC 2011-12
  - AICPA SSAE 18, AT-C 105 and AT-C 205, Trust Services Criteria (2017 with 2022 points-of-focus revision)
  - PCAOB AS 2201 (significant deficiency / material weakness definitions)
  - ForHumanity IAAIS (current certification scheme and criteria at reading time)
  - NYC Local Law 144 and 20 RCNY §5-301

## Scenario

**AegisBio Hiring-AI** (introduced in `mod-110` exercise 01) is now a multi-attestation provider. The company operates a resume-screening ranker in the EU and US and has active engagements with:

- A notified body under the EU AI Act Article 43 (Annex VII).
- An ISO/IEC 42001 AIMS certification body (unrelated to the notified body).
- The service-organisation SOC 2 Type II examiner, because AegisBio is a SaaS provider to enterprise customers.
- An independent IAAIS auditor for a US state RFP requirement.
- A NYC LL144 bias auditor for the NYC employer clients' annual rule obligations.

### The underlying observation

Across the current engagement cycle, each engagement's team has independently surfaced the same underlying issue:

> Over the past twelve months, **four of the twenty-seven production model releases** of the resume-screening ranker went to the `prod-us-east` serving environment **without an updated bias evaluation**. The organisation's "Pre-Deployment Bias Evaluation Procedure" (POL-DEP-014 §3) requires a stratified bias evaluation on an updated held-out sample of ≥10,000 rows before every production release. In the four cases, the bias evaluation on file for the release was the prior release's evaluation (3 to 7 months stale, depending on the release). Monitoring telemetry since each release has not surfaced an operating-effectiveness anomaly, but the pre-deployment control did not fire.

The twenty-seven releases include six deployed to NYC employer customers and ten to EU employer customers; the four releases that missed the bias evaluation gate were all in the US, with three to NYC employers.

## Deliverables

### 1. Five classification memos (~250–400 words each)

For each engagement type, write a classification memo covering:

- **Engagement shape and standard.** The shape, the governing standard, the specific clause / rule / scheme text.
- **Classification.** The severity grade under this scheme's vocabulary.
- **Rationale.** Why this grade — tied to the scheme's own definition (e.g., ISO/IEC 17021-1 §9.4.9 second indicator for a pattern of minor nonconformities promoting to major; PCAOB AS 2201 reasonable-possibility test for material weakness; etc.).
- **Report-level consequence.** What the classification means for the certificate / opinion / report — e.g., certificate recommendation blocked; opinion qualification; MRA / MRIA layering; conditional pass under the scheme.
- **What must change before closure under this scheme.**

Write the five memos as if for the engagement-team's own classification workpaper — not for management.

### 2. Cross-scheme reconciliation note (~400 words)

Write a short reconciliation note from the audit-function-leader perspective (chapter 6) explaining:

- How the five classifications relate to one another — the scheme-specific "label" vs. the shared underlying condition.
- Why the organisation should expect different vocabulary and different remediation deadlines from each engagement.
- How a single CAP should be designed to satisfy all five schemes without triggering conflicting demands.
- Which engagement's remediation deadline is the earliest and why that drives the organisation-level plan.

### 3. "Wrong classification" catalogue (~200 words)

List at least five misclassifications that would plausibly be made by inexperienced auditors on this fact pattern — e.g., calling the ISO finding a "material weakness," rating the SR 11-7 issue a "minor nonconformity," characterising the LL144 observation as a "fail." For each, explain the specific definitional error.

## Starter guidance

- **The question is definition-matched to fact.** Do not reach for adjacent schemes' words. Ask what the scheme's clause actually says and whether the fact pattern satisfies it.
- **ISO/IEC 17021-1 §9.4.9 has a pattern indicator.** A series of minor nonconformities on the same requirement promotes to major. Use that indicator explicitly when it applies.
- **SR 11-7 / MRM considers whether the issue has an ICFR path.** Resume-screening ranker is probably not an ICFR model; so material weakness language is likely a category error for SR 11-7 here. But SR 11-7 still has its own severity vocabulary (deficiency / significant deficiency) distinct from the AICPA ICFR framework.
- **SOC 2 operates on controls, not models.** Reclassify the condition as a controls-level question: the pre-deployment bias-evaluation control failed in operating effectiveness for 4 of 27 sampled releases.
- **IAAIS scheme vocabulary varies.** Consult the scheme's current text; do not rely on memory. Where current scheme text is beyond your verifiable knowledge, mark `<!-- needs-research: ... -->` with the specific question.
- **LL144 is not a pass/fail scheme.** It is a disclosure rule. The classification question for LL144 is whether the published bias-audit summary is correctly prepared and published — distinct from whether the control at AegisBio functioned.

## Acceptance criteria

The deliverables are accepted when:

- Each classification memo cites the engagement's standard and the specific clause / rule / scheme text that governs the classification choice.
- Each classification is defended against the standard's own definition, not against an adjacent scheme's definition.
- The ISO classification explicitly addresses the §9.4.9 pattern indicator for repeated same-requirement nonconformities.
- The SR 11-7 classification stays inside the deficiency / significant deficiency / material weakness vocabulary and does not conflate with the SOC 2 vocabulary; the material-weakness path is explicitly tested against reasonable-possibility of material misstatement and set aside if inapplicable.
- The SOC 2 classification distinguishes exception / deficiency, and treats operating effectiveness as the relevant dimension for the Type II report.
- The IAAIS classification uses the scheme-owner's current vocabulary (pass / conditional / fail or the scheme's then-current grades).
- The LL144 classification is framed as a disclosure-rule question, not a severity-of-system question.
- The reconciliation note defends a single CAP design that would close all five schemes' requirements and names the earliest remediation deadline that drives the organisation's plan.
- The "wrong classification" catalogue correctly identifies definitional errors — not just alternative judgements.
- No scheme's vocabulary is borrowed by another scheme without explicit note.

## Stretch goals

- Add a **sixth classification memo** for an internal audit function operating under the IIA Global Internal Audit Standards, picking a rating (H / M / L or an equivalent) and defending it against the IAF's methodology.
- Write a **joint findings-register entry** (chapter 6) that captures the underlying condition once but carries the five scheme-specific classifications side by side.
- Produce a **short briefing** for AegisBio's Chief AI Officer explaining why the same issue has five different labels and what that means for prioritisation — tone professional, not academic, targeted at a senior executive with limited audit literacy.
- Draft the **close-out meeting talking points** for whichever of the five engagements you believe will produce the hardest negotiation, with specific anticipated management pushback and your rehearsed response.
