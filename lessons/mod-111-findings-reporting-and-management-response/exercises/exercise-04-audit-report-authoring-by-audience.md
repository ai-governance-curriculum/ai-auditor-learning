# exercise-04: Audit Report Authoring by Audience

**Estimated effort:** 4 hours

## Objective

Author four distinct audit reports — a SOC 2 Type II report, an ISO/IEC 42001 certification audit report, an SR 11-7 MRM validation report, and an internal audit report under the IIA Global Internal Audit Standards — all documenting the **same engagement findings** but each carrying the shape, vocabulary, and skepticism language of its own standard. Readers should be unable to tell the four reports are about the same underlying engagement without comparing them.

## Prerequisites

- Chapter [`04-audit-report-shapes-and-opinion-types-by-audience.md`](../04-audit-report-shapes-and-opinion-types-by-audience.md)
- `mod-110` chapters on the engagement shapes referenced
- Access to:
  - AICPA SSAE 18 / AT-C 105 / AT-C 205; AICPA Trust Services Criteria (2017 with 2022 points-of-focus revision); AICPA SOC 2 reporting guides including DC Section 200 description criteria
  - ISO/IEC 42001:2023 and ISO/IEC 17021-1:2015
  - Federal Reserve SR 11-7 (2011) and OCC 2011-12
  - IIA Global Internal Audit Standards (2024)
  - ISA 705 / AU-C 705 / SSAE opinion-modification vocabulary

## Scenario

**Northstar Credit Partners** (introduced in exercise 03) is a consumer lender using an AI-enabled credit-decisioning model and a GenAI-assisted customer-service agent. The AI/ML service runs on a dedicated internal SaaS platform maintained by Northstar's "ML Platform" team; several enterprise customers of Northstar's partner-bank division also consume the same platform under a service-organisation arrangement. Northstar carries four relevant engagements:

- **SOC 2 Type II** — Northstar's "ML Platform" service organisation, examination period 2026-07-01 → 2027-06-30, Trust Services Criteria: Security, Availability, Processing Integrity, Confidentiality.
- **ISO/IEC 42001 recertification** — Northstar's AIMS, following initial certification in 2024.
- **SR 11-7 MRM validation** — the credit-decisioning model (ICFR path via the Current Expected Credit Loss computation).
- **Internal audit engagement on AIMS and AI risk management** — scoped under the IIA Global Internal Audit Standards.

### The engagement findings (same across all four reports)

**Finding A.** Pre-deployment bias-evaluation control failed on 4 of 27 sampled resume-ranker releases (same as exercise 02). Note: the resume ranker is not the credit-decisioning model; it is out of SR 11-7 scope but in SOC 2, ISO 42001, and internal audit scope.

**Finding B.** The credit-decisioning model's challenger-model benchmark is itself a GenAI-assisted scenario generator; the auditor cannot obtain evidence that the scenario set is representative of recessionary conditions. The ECL computation feeds the financial statements; 14% of pre-tax income. This is in SR 11-7 scope and (indirectly, via financial-reporting path) relevant to any ICFR-touching attestation.

**Finding C.** GenAI-assisted customer-service agent does not route UDAAP-category drafts to compliance review (same as exercise 03). In ISO 42001 and internal-audit scope; outside strict SOC 2 TSC scope but relevant to Processing Integrity depending on description boundary; outside SR 11-7 scope.

Management responses are attached to each finding per chapter 3; assume Finding A's CAP is acceptable, Finding B's CAP is in dispute, Finding C's response is cosmetic and the auditor has declined to close.

## Deliverables

### 1. SOC 2 Type II report — Section I (Independent Service Auditor's Report) (~1,200 words)

Author Section I of the SOC 2 report. Must include:

- Addressee.
- Report title.
- Scope paragraph identifying the service organisation, the system name, the examination period, and the Trust Services Criteria.
- Management's responsibility paragraph.
- Service auditor's responsibility paragraph with professional-skepticism language.
- Inherent-limitations paragraph adapted for AI content.
- Opinion paragraph with the correct modification given Findings A (exception on a control) and C (likely out-of-boundary, handle correctly).
- Signature block (firm name, city, state, date).

### 2. ISO/IEC 42001 certification audit report excerpt (~1,500 words)

Author the key sections of the ISO/IEC 42001 recertification audit report:

- Audit summary (scope, dates, team, type).
- Scope confirmation statement.
- Findings by ISO/IEC 42001 clause for Findings A and C, in CCCER shape with ISO/IEC 17021-1 classification (major / minor / observation / OFI).
- Audit team recommendation to the certification body's committee (recommend, recommend with conditions, decline).
- Opportunities for improvement.

Do not include Finding B — the credit-decisioning model's challenger-model issue — as it is more naturally an MRM concern; note its exclusion with reasoning in the scope section.

### 3. SR 11-7 validation report (~1,500 words)

Author the SR 11-7 MRM validation report for the credit-decisioning model:

- Executive summary with overall validation finding and recommended rating.
- Model inventory entry.
- Conceptual soundness assessment (brief; focus on scenario-generation methodology).
- Ongoing monitoring assessment (brief).
- Outcomes analysis.
- Governance, policies, and controls assessment.
- Finding B in CCCER shape with deficiency / significant deficiency / material weakness classification, with explicit application of PCAOB AS 2201's reasonable-possibility test given the 14%-of-pre-tax-income exposure.
- Validator's conclusion and rating under the bank's rating scale.
- Reference to attached management response.

Findings A and C should not appear in the SR 11-7 report; note briefly in the scope section that they are addressed in parallel engagements.

### 4. Internal audit report under the IIA Global Internal Audit Standards (~1,500 words)

Author the full internal audit report covering all three findings:

- Executive summary with overall engagement opinion (the IAF's methodology).
- Engagement background and scope.
- Objectives and methodology.
- Findings A, B, and C in CCCER shape with the IAF's own rating vocabulary (H / M / L or equivalent) — not the external schemes' vocabulary.
- Management action plans attached.
- Overall engagement opinion (satisfactory / needs improvement / unsatisfactory) supported by the findings.
- Distribution list.

### 5. Cross-report consistency note (~400 words)

Write a short internal note from the engagement partner (external) / Chief Audit Executive (internal) explaining:

- How the four reports stay consistent on the facts while using different shapes and vocabularies.
- Where each report cross-references the others (if any).
- How the opinion modifications (qualified / unqualified / major / needs-improvement / etc.) correspond across the four shapes for the same underlying facts.
- What each report's reader is asked to do with it.

## Starter guidance

- **Vocabulary discipline.** No "material weakness" in the ISO report. No "minor nonconformity" in the SOC 2 report. No "satisfactory" in the SR 11-7 report. Each standard's vocabulary is prescribed.
- **Opinion modification follows a decision rule.** Chapter 4's decision rule: exception → material? → pervasive? → unmodified / qualified / adverse / disclaimer. Apply the rule mechanically; then write the opinion sentence.
- **Scope statements matter.** Finding C is in the ISO AIMS scope but ambiguous for SOC 2 TSC; the SOC 2 scope paragraph needs to handle this crisply, and if the finding sits inside the description, the opinion must reflect it. Be explicit about the boundary.
- **Professional-skepticism language.** Each standard has its own expected phrases ("reasonable assurance," "sufficient appropriate evidence," "planned and performed," "obtained an understanding of," "our audit included consideration of…"). Do not paraphrase these into a generic voice.
- **Dates and signatures.** Every report has required dates — report date, subject-matter-period date, management-assertion / representation date. Get them right.
- **Inherent-limitations language for AI.** Each report's limitation paragraph should acknowledge AI-specific limitations (statistical variability, non-stationarity, limits on reperformance where training data is not re-accessible) without undercutting the opinion.

## Acceptance criteria

The deliverables are accepted when:

- Each report uses only its own standard's vocabulary; no cross-vocabulary smuggling.
- Each report's scope statement is specific about AI boundaries (model / version / environment / period).
- Each report's opinion follows the materiality-and-pervasiveness decision rule and the correct opinion type is explicitly selected.
- Skepticism-language patterns are present where the standard expects them.
- Findings common to multiple reports are stated consistently on facts across the reports, but classified in each report's own vocabulary.
- The SR 11-7 report applies PCAOB AS 2201 reasonable-possibility reasoning for Finding B's material-weakness assessment.
- The ISO/IEC 42001 report classifies per ISO/IEC 17021-1 and defends the classification on the clause's own criteria.
- The SOC 2 report correctly handles Finding C — either bringing it into the examination with an exception or explicitly stating the description-boundary exclusion.
- The internal audit report uses the IAF's rating vocabulary and does not borrow from the external schemes without noting it as a methodology choice.
- The cross-report consistency note defends the opinion-modification choices across the four shapes and would survive a committee reader's cross-check.

## Stretch goals

- Author the **management's assertion** (SOC 2 Section II) and the service-organisation's **system description** (Section III, abbreviated) for the SOC 2 report.
- Author the **ISO/IEC 42001 certificate text** that would issue (if any) following your audit team recommendation, including scope, standard version, validity, and any listed restrictions.
- Add an **SR 11-7 supervisor-facing cover note** that the institution's MRM function would use when the validation report is tabled at examination — understanding that the note is written by the institution, not the validator, and the validator reviews for technical accuracy.
- Draft an **ISAE 3000 reasonable-assurance opinion** on a specific AI claim (e.g., "the resume ranker's pre-deployment bias-evaluation control was operating effectively during the examination period") — as a fifth report added to the set.
