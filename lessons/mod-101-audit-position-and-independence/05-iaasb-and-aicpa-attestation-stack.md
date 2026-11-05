# The IAASB + AICPA Attestation Stack for AI Assurance

## Motivation

The moment an AI audit becomes an **external attestation** — a SOC for AI report, a bespoke AI-assurance report, an EU AI Act Article 43 third-party conformity assessment delivered through a firm practising under ISAE 3000 — the applicable rulebook is no longer the IIA Standards. It is the IAASB framework (international) or the AICPA attestation framework (US). Reports under these frameworks carry legal and contractual weight the IIA-governed internal audit report does not. Mis-citing the framework, or executing the engagement at the wrong level of assurance, can void the report. This chapter installs the external-assurance methodology layer AI Auditors use when the engagement is attestation.

## The IAASB framework in one diagram

The **International Auditing and Assurance Standards Board (IAASB)** issues standards used by professional-accountancy firms for audits, reviews, and other assurance engagements. The relevant parts of the stack for AI assurance:

- **International Framework for Assurance Engagements** — defines the elements of an assurance engagement (three-party relationship, underlying subject matter, suitable criteria, sufficient appropriate evidence, written assurance report) and the two levels of assurance (reasonable and limited).
- **ISAE 3000 (Revised) — Assurance Engagements Other than Audits or Reviews of Historical Financial Information.** The methodology standard for AI-assurance engagements. Covers planning, materiality, evidence, written representations, reporting, documentation. Applicable to both reasonable- and limited-assurance engagements on non-financial subject matter.
- **ISAE 3402** — Assurance Reports on Controls at a Service Organisation. The IAASB analogue to AICPA SOC 1; relevant when an AI audit crosses the service-organisation line.
- **ISAE 3410 / 3420 / 3400 series** — subject-matter-specific standards (GHG, pro-forma, prospective financials); ISAE 3000 remains the default for AI engagements without a bespoke subject-matter standard.

Within an ISAE 3000 engagement, the following supporting ISAs are applied by analogy (ISAE 3000 explicitly contemplates reference to relevant ISAs):

- **ISA 500 — Audit Evidence.** Sufficiency and appropriateness of evidence; relevance, reliability, source hierarchy. For AI, this is what makes "the eval metrics in the model card" either sufficient-and-appropriate evidence or not (reliability of source, auditor re-performance, corroboration).
- **ISA 530 — Audit Sampling.** Statistical and judgmental sampling. For AI, this governs how you sample inference logs, training data records, incident-response tickets, and any other populations that are too large to test in full.
- **ISA 620 — Using the Work of an Auditor's Expert.** When the engagement needs expertise the firm does not have — e.g., a specialist ML engineer to assess model architecture choices, a specialist statistician to challenge calibration evidence — this is the standard that governs scoping, independence, competence, and use of the expert's work.
- **ISA 320 — Materiality in Planning and Performing an Audit.** Although ISAE 3000 does not require an exact financial materiality calculation, the materiality discipline (materiality for the subject matter, for performance, for evaluating misstatements) is applied by analogy for AI engagements — notably when the AI-attestation report's audience is a regulator reading "material misstatement" as the threshold for enforcement.

### ISAE 3000 structural beats

An ISAE 3000 engagement, mapped to AI:

1. **Acceptance and continuance** — can the firm perform the engagement under independence, competence, resources, and criteria-suitability tests?
2. **Agreeing terms of engagement** — engagement letter identifies the subject matter, the criteria, the responsible party, the intended users, the level of assurance (reasonable / limited), and the applicable framework (ISAE 3000, plus any sector-specific standard).
3. **Planning** — understand the subject matter, risk of material misstatement, materiality, overall engagement strategy.
4. **Performing the engagement** — risk assessment, evidence gathering, including the auditor's expert work under ISA 620 by analogy.
5. **Forming the conclusion and reporting** — assurance report with the conclusion in the form prescribed by ISAE 3000. Reasonable-assurance conclusion uses positive language ("in our opinion, [subject matter] is fairly stated, in all material respects, in accordance with [criteria]"); limited-assurance conclusion uses negative language ("nothing has come to our attention that causes us to believe...").
6. **Documentation** — workpaper requirements per ISAE 3000, inspected in firm quality review and by the firm's regulator.

## The AICPA attestation framework

The **AICPA (American Institute of Certified Public Accountants)** maintains the US attestation framework, codified in the Statements on Standards for Attestation Engagements (SSAEs) and reorganised under the **AT-C** clarified codification:

- **AT-C 105 — Concepts Common to All Attestation Engagements.** The horizontal standard applicable to every attestation. Defines examination, review, and agreed-upon-procedures engagements; sets requirements for independence, due professional care, planning, evidence, documentation, and quality management.
- **AT-C 205 — Assertion-Based Examination Engagements.** The specific attestation-level standard used for reasonable-assurance "examination" engagements — SOC 2, SOC 3, bespoke AI-assurance examinations. Requires written assertion from the responsible party and sets the reporting form.
- **AT-C 210 — Review Engagements.** Limited-assurance analogue.
- **AT-C 215 — Agreed-Upon Procedures Engagements.** Procedures-level engagement where the user takes responsibility for the sufficiency of procedures; auditor reports findings only, no assurance conclusion.
- **AT-C 320 — Reporting on an Examination of Controls at a Service Organisation.** SOC 1 / SOC 2 anchor.

AT-C 105 operates jointly with:

- **ET (Code of Professional Conduct)** — independence rules, including the "Member in Public Practice" rules binding AICPA members.
- **QM 1 / QM 2 — Statements on Quality Management Standards.** The firm-level quality-management system that must exist for attestation work to issue under AICPA rules. (US adoption of IAASB's **ISQM 1 / ISQM 2** in substance.)

For the AI auditor practising in the US under the AICPA framework, the primary pair is **AT-C 105 + AT-C 205** for an examination engagement; the subject matter is the AI-system or AI-management-system assertion the responsible party makes (e.g., "we operated our AI model lifecycle during the period in accordance with [criteria]"), and the report conclusion opines on whether the assertion is fairly stated.

## Common assurance patterns the AI auditor executes

Four patterns worth having in muscle memory:

### Pattern A — Direct-reporting examination over an AI subject matter (AT-C 205 / ISAE 3000)

Example: a Big-4 firm performs an AT-C 205 examination on a bank's AI/ML model governance program against the bank's documented control framework. Report form: positive assurance on whether the control framework was designed and operated to achieve stated control objectives over the period.

### Pattern B — Service-organisation report (SOC 2 / SOC for AI / ISAE 3402)

Example: a foundation-model provider engages a firm to issue a **SOC 2 Type II** report with AI-specific trust services criteria (confidentiality, processing integrity, with AI-specific additional criteria) over the model-inference service. User organisations (deployers) rely on the SOC 2 under their own third-party assurance program. For AI-specific service-organisation work, the AICPA has published or is developing dedicated AI criteria; use the live version. <!-- needs-research: confirm the current state of AICPA SOC-for-AI criteria at reading time — the AICPA Assurance Services Executive Committee has been developing AI-specific trust services criteria; cite the live version the engagement uses -->

### Pattern C — Agreed-upon procedures on specific AI evidence (AT-C 215)

Example: a buyer requests specific procedures (not an assurance conclusion) on a seller's training-data lineage. Firm performs the procedures, reports findings only, buyer takes responsibility for sufficiency. Useful when the buyer wants targeted, documented findings without committing the firm to an opinion.

### Pattern D — EU AI Act Article 43 third-party conformity assessment

Executed by a designated **notified body** under EU AI Act. Not an IAASB or AICPA engagement by framework, but where the notified body is a firm that also practises under ISAE 3000 / AT-C, the firm's quality-management system (ISQM 1 or QM 1) and independence rules extend to the EU AI Act engagement in parallel with the Act's own designation requirements. Expect a cross-citation in the engagement letter and the audit report. Covered in depth in `mod-110-conformity-assessment-and-sector-audit-shapes`.

## Reasonable vs. limited assurance — what changes

The auditor's effort and the report's language both move with the level of assurance:

- **Reasonable assurance** → positive conclusion, higher evidence threshold, more extensive procedures, closer to a financial-statement audit in rigour. The auditor's risk of a wrong conclusion is reduced to an acceptably low level.
- **Limited assurance** → negative-form conclusion, lower evidence threshold, less extensive procedures. The auditor's risk is reduced to an acceptable level but higher than reasonable.

For AI engagements, auditors often start at limited assurance (sustainability-style) for first-year bespoke AI-assurance work when the subject matter is immature, then move to reasonable assurance as management can support a more formal assertion. The engagement letter must name the level; the report language follows the level; mixing them across the engagement is a reporting-standards violation.

## Suitable criteria — the AI-specific trap

ISAE 3000 and AT-C 105 both require **suitable criteria** — relevant, complete, reliable, neutral, understandable. AI subject matter has a recurring criteria problem: the available criteria are evolving, overlapping, and partially conflicting (ISO/IEC 42001 vs. NIST AI RMF vs. EU AI Act vs. internal policy). The auditor's job is to either:

1. Audit against **established criteria** published by a recognised body (ISO/IEC 42001, NIST AI RMF, EU AI Act), *or*
2. Accept **specifically developed criteria** authored by the responsible party, test them for suitability under ISAE 3000.A45 / AT-C 105 criteria requirements, and disclose them in the report.

Criteria that silently mix frameworks without a crosswalk are usually not suitable; call it out in planning and insist on the crosswalk before accepting the engagement. The criteria layer is the focus of `mod-102-ai-audit-criteria-landscape`.

## The auditor's expert — a near-constant feature of AI engagements

Few audit firms have deep in-house ML/LLM expertise across all AI subject matters; most engagements will involve an **auditor's expert** under ISA 620 (or the ISQM 1 / AT-C 105 equivalents). The engagement letter and workpapers must document:

- The expert's competence, capabilities, objectivity.
- Scope of the expert's work (what is the expert doing, what are they not doing).
- The relationship between the auditor and the expert (direct employee of the firm, external contractor, management's expert that the auditor is relying on — the distinction matters because the reliance rules differ).
- Review of the expert's work — the auditor retains responsibility for the conclusion; the expert's work supports but does not substitute for the auditor's judgment.

For AI engagements, common expert roles: ML-engineering expert (architecture review, fine-tuning posture), evaluation-methodology expert (judge calibration, statistical significance), red-team expert (coverage against MITRE ATLAS / OWASP / NIST AI 100-2), privacy-engineering expert, security-engineering expert. The auditor retains the audit opinion; the expert supports it. Audit workpapers show the expert's scope, work, deliverables, and auditor review.

## Example — an AT-C 205 examination of a client's LLM safety program

Scenario: a Big-4 firm is engaged to perform an AT-C 205 examination of a SaaS provider's LLM safety program for the period 1 Jan to 31 Dec. The firm issues a positive-assurance report.

Engagement structure:

- **Framework**: AT-C 105 + AT-C 205. US quality-management: QM 1 + QM 2. Independence: AICPA Code (ET §1.200) + the firm's internal independence policy, confirmed at acceptance.
- **Subject matter**: the client's management assertion that the LLM safety program (content filters, red-team program, incident-response program, monitoring) operated effectively during the period in accordance with the control framework the client has documented.
- **Criteria**: the client's documented control framework, crosswalked by the client to NIST AI RMF 1.0 + GenAI Profile and OWASP LLM Top 10. Auditor assesses suitability under AT-C 105.
- **Risk assessment + planning**: materiality for the subject matter (what misstatement would change the user's decision), risk of material misstatement, overall strategy.
- **Evidence**: inspection of safety configurations, re-performance of a sampled set of red-team attacks, inspection of incident tickets, interview of the safety-team lead. Auditor's expert (red-team methodology SME under ISA 620 analogue) supports the re-performance work.
- **Documentation**: workpapers per AT-C 105 § requirements, including auditor-expert documentation, sampling rationale, and the written representation letter.
- **Report**: positive-assurance conclusion using AT-C 205-prescribed language, cross-referencing the client's assertion and the criteria.

The resulting report is read by the client's enterprise customers as evidence under their third-party risk programs — which is why the methodology layer in this chapter is load-bearing. If the firm had executed informally against "best practice" instead of under AT-C 205, the report would not carry attestation weight.

## Summary

- External AI-assurance engagements run under **ISAE 3000 (Revised)** (IAASB) or **AT-C 105 + AT-C 205** (AICPA) depending on jurisdiction and client posture.
- Supporting standards (ISA 500, ISA 530, ISA 620, ISA 320 by analogy) govern evidence, sampling, auditor's expert, materiality.
- Firm quality management under **ISQM 1 / ISQM 2 (IAASB)** or **QM 1 / QM 2 (AICPA)** is a precondition for issuing reports.
- Choose the level of assurance (reasonable or limited) consciously; report language follows the level.
- AI subject matter requires conscious handling of suitable criteria and the auditor's expert — both are near-constant features of the engagement and both are called out in the engagement letter and workpapers.
