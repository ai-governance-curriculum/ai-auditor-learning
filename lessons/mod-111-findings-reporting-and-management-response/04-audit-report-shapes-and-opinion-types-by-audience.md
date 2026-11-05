# Audit Report Shapes and Opinion Types by Audience

## Motivation

Findings and management responses are inputs; the **report** is the engagement's output. Each engagement shape prescribes a specific report structure, a specific opinion vocabulary, and specific language elements the auditor must include. The audience that consumes the report (a regulator, a certification body, a procurement team, a prospect, a litigation team, the public) reads it through the lens of the framework it was issued under. The auditor writes the report so that the right audience can rely on it; writing one report that pretends to serve all audiences compromises every audience.

This chapter walks the eight report shapes the AI auditor is most likely to issue — ISAE 3000, AT-C 105, SOC 2 Type II, ISO/IEC 42001 certification, EU AI Act Article 43 conformity assessment, SR 11-7 validation, NYC LL144 bias-audit summary, and an internal audit report under IIA Global Internal Audit Standards. For each, it covers the structural sections, the opinion vocabulary, the skepticism-language expectations, and the AI-specific adaptations the report has to carry.

## The structural tension — form and substance

Every report balances **form** (the structure required by the standard) and **substance** (the specific findings of this engagement). The standard constrains the form so readers can navigate. The auditor fills the substance within that form. AI content expands the substance (model cards, eval methodology, data-governance evidence, drift monitoring) but does *not* let the auditor invent new report shapes. Auditors who improvise form — a "custom AI audit report" — produce artefacts that no audience can place.

## ISAE 3000 — international attestation on non-financial subject matter

**Standard.** International Standard on Assurance Engagements 3000 (Revised), "Assurance Engagements Other than Audits or Reviews of Historical Financial Information," published by the IAASB. Governs assurance engagements over subject matter such as sustainability reports, controls over a non-financial process, and increasingly AI-system claims.

### Report shape

- **Addressee.** The engaging party (typically management or governance of the auditee).
- **Title.** Clear reference to "Independent assurance report" distinguishing it from a consulting report.
- **Subject matter identification.** Precise description of what is being assured — the AI system name and version, the period or point in time, the specific claims.
- **Criteria.** Named and referenced. ISAE 3000 requires suitable criteria (relevance, completeness, reliability, neutrality, understandability).
- **Inherent limitations.** Describes limits that affect the subject matter (e.g., inherent statistical variability in AI model performance).
- **Respective responsibilities.** Management's responsibility for the subject matter; practitioner's responsibility for the assurance.
- **Summary of work performed.** Sufficient to understand the nature, timing, and extent of procedures — without being an audit methodology manual.
- **Practitioner's conclusion / opinion.** The core sentence.
- **Signature, date, and firm address.**

### Reasonable vs limited assurance

ISAE 3000 distinguishes:

- **Reasonable assurance.** "In our opinion, [subject matter] is fairly stated, in all material respects, in accordance with [criteria]." Equivalent to an audit-level opinion.
- **Limited assurance.** "Based on the procedures performed and evidence obtained, nothing has come to our attention that causes us to believe that [subject matter] is not fairly stated, in all material respects, in accordance with [criteria]." The language is deliberately negative in form.

Opinion modifications follow ISA 705 analogues: unmodified, qualified, adverse, disclaimer.

### AI-specific adaptations

- The subject matter has to specify the AI system boundary (which model, which data pipeline, which inference endpoint, which deployment environment).
- Criteria often compose (e.g., ISO/IEC 42001 clauses + the organisation's system-card claims + SR 11-7 where applicable).
- Inherent limitations should acknowledge: stochasticity of model outputs, distributional drift risk, limits on reperformance where training data is not re-accessible, non-determinism of generative systems.
- The summary of work includes the evidence shape from `mod-104` and the reperformance shape from `mod-106`.

## AT-C 105 (SSAE 18) — U.S. attestation

**Standard.** AICPA SSAE No. 18, reorganised into AT-C 105 (common concepts), AT-C 205 (examination engagements), AT-C 210 (review engagements), and AT-C 215 (agreed-upon procedures). AT-C 105 is the common platform; AT-C 205 governs the examination engagement for controls and other subject matter and is the U.S. parallel to reasonable-assurance ISAE 3000.

### Report shape (AT-C 205 examination)

- **Title.** Including "Independent Accountant's Report" or similar.
- **Addressee.**
- **Introductory paragraph.** Identifies the subject matter and the responsible party's assertion.
- **Management's responsibility.**
- **Accountant's responsibility.** References the standards (AICPA SSAEs), describes the examination.
- **Inherent limitations.**
- **Opinion.** Expressed on the subject matter or on management's assertion — the practitioner chooses, and must disclose which.
- **Signature, firm location, date.**

### Opinion vocabulary

Unmodified, qualified, adverse, or disclaimer, with definitions analogous to ISAE 3000.

### AI-specific adaptations

Same as ISAE 3000: boundary clarity, composite criteria, limitations-of-inherent-limitations, reperformance shape.

## SOC 2 Type II — trust-services-criteria reporting

**Standard.** AICPA SSAE 18 (AT-C 105 + AT-C 205) with the AICPA's 2017 Trust Services Criteria (TSC), updated in 2022 with "points of focus." SOC 2 is a service-organisation examination; SOC 2 Type II adds operating effectiveness over a period, commonly 6 or 12 months.

### Report sections

- **Section I — Independent Service Auditor's Report.** The opinion.
- **Section II — Management's Assertion.** Service-organisation management's own assertion about the system and its controls.
- **Section III — Description of the System.** Required content per DC Section 200 — services, infrastructure, software, people, data, procedures. For an AI service this includes the model-serving stack, the training/data pipeline where in-scope, and the human-oversight controls.
- **Section IV — Trust Services Criteria and Related Controls / Tests / Results.** The matrix — for each applicable criterion, the controls, the tests performed, the results.
- **Section V (optional) — Other Information Provided by the Service Organisation.** Not covered by the auditor's opinion.

### Opinion vocabulary

Unmodified ("fairly presented, suitably designed, operating effectively"), qualified, adverse, or disclaimer. Modifications list each exception with the criterion and the deviation.

### AI-specific adaptations for a SOC 2 covering an AI service

- The System Description (Section III) identifies the AI boundary: training-data lineage (where in scope), model-registry governance, release-and-promotion controls, inference infrastructure, monitoring, human-in-the-loop controls.
- The TSC-to-control mapping covers the familiar CC categories (control environment, communication and information, risk assessment, monitoring, control activities, logical access, change management, system operations, risk mitigation) and, where applicable, the Processing Integrity, Confidentiality, Availability, and Privacy criteria.
- Carve-out vs. inclusive subservice organisations — the AI service often depends on a foundation-model provider; the SOC 2 must treat the subservice correctly and either carve it out (naming complementary user entity controls) or include it (rare for foundation-model providers).
- Complementary user entity controls — the deployer organisation's own controls (data ingress curation, output monitoring, human review of high-stakes outputs) that the service relies on.

## ISO/IEC 42001 certification report

**Standard.** ISO/IEC 17021-1 governs how a certification body reports; ISO/IEC 17011 governs accreditation of the certification body. The audit evidence tests conformance to ISO/IEC 42001.

### Report shape

- **Title and certificate scope.** Identifies the certified organisation, the AIMS scope (which legal entities, which AI systems, which processes), the certification standard (ISO/IEC 42001:2023), the certification body, the accreditation body.
- **Audit summary.** Dates, locations, audit team, audit type (Stage 1, Stage 2, surveillance, recertification).
- **Scope review.** Confirms the applied scope and any exclusions / justifications.
- **Findings by clause.** For each ISO/IEC 42001 clause audited, the sampled evidence and conclusion.
- **Nonconformities.** Each nonconformity in CCCER shape with classification (major / minor), with reference to the clause and to management's CAP.
- **Opportunities for improvement.** Where raised.
- **Positive findings.** Where the audit protocol surfaces strengths worth noting.
- **Recommendation.** "Recommend for certification" (initial), "recommend continuation" (surveillance), or "recommend corrective action before recommendation."
- **Signature of the audit team leader.**

### Opinion language

ISO certification is binary at the certificate level — the certificate is issued or it is not. The audit report's *recommendation* feeds the certification body's committee decision. There is no "qualified" certificate; there is either a certificate (clean or with minor NCs closed through CAP) or there is not.

### AI-specific adaptations

- Scope statement is unusually critical — "AI Management System covering the design, development, provision, and operation of AI-enabled products within [business unit]." Scope creep or ambiguity makes the certificate unreliable to downstream relying parties.
- The clause-by-clause findings often include AI-specific sub-clauses — 6.1.4 AI risk assessment, 6.1.5 AI risk treatment, 8.3 AI system impact assessment, 8.4 AI system lifecycle, A.5 governance controls, A.6 inter-organisational controls, A.7 resources for AI systems, A.8 impact assessment, A.9 AI system lifecycle, A.10 data for AI systems.<!-- needs-research: confirm the final Annex A control-group labels and numbering for ISO/IEC 42001:2023 at reading time; Annex A was drafted during the standard's preparation and numbering has been stable, but readers should cross-check the standard text. -->
- `mod-105` is the detailed companion for the clause-by-clause testing.

## EU AI Act Article 43 conformity assessment report

**Standard.** Regulation (EU) 2024/1689, Articles 43 and 44, Annex VI (internal control), Annex VII (quality-management-system and technical-documentation assessment by a notified body).

### Report shape (Annex VII)

Three artefacts, covered in `mod-110` chapter 1:

- **QMS audit report.** Against Article 17; findings by Article 17 sub-point; grading analogous to ISO/IEC 17021-1; corrective-action requests; approval of the QMS.
- **Technical-documentation assessment report.** Against Annex IV sub-points; cross-referenced to Articles 9–15; findings and corrective-action requests; approval of the dossier.
- **Certificate.** A "Union technical documentation assessment certificate" per Annex VII point 4.6, listing the provider, the system, the technical-documentation reference, applied harmonised standards, and the validity period (up to four years).

### Opinion language

Certificate issues, or does not. Surveillance (Annex VII point 5) follows and can trigger re-evaluation; substantial modification under Article 43(4) can trigger re-assessment.

### AI-specific adaptations

The entire engagement is AI-specific. See `mod-110` chapter 1 for the deep walkthrough.

## SR 11-7 MRM validation report

**Standard.** Federal Reserve SR 11-7 (2011), OCC 2011-12, FDIC-adopted equivalents.<!-- needs-research: confirm the Fed's current MRM guidance release at reading time — SR 11-7 remains the anchor but has been supplemented by subsequent guidance on AI/ML. -->

### Report shape (effective-challenge validation)

- **Executive summary.** Overall validation finding; residual risk; recommended rating.
- **Model inventory entry.** Identifies the model, the owner, the use, the materiality tier.
- **Conceptual soundness.** Assessment of the model's design — theoretical basis, methodology choice, assumption inventory and support, limitations stated.
- **Ongoing monitoring.** Process design and evidence of performance monitoring, outcome analysis, benchmarking, back-testing.
- **Outcomes analysis.** Comparison of model output to realised outcomes; sensitivity analysis; stress testing.
- **Governance, policies, and controls.** Model-development documentation, change-management, access and authorisation, use controls.
- **Findings.** Deficiency / significant deficiency / material weakness classifications per chapter 2; MRA / MRIA layering where supervisor may step in.
- **Validator's conclusion.** The overall rating under the bank's rating scale.
- **Response.** Management's corrective-action plan attached.

### Opinion language

Supervisory letters, model ratings per the bank's rating scale, and the standard deficiency/significant/material vocabulary. The validator's report is for the Model Risk Committee and the CRO; the supervisor reads it at examination.

### AI-specific adaptations

- LLM and GenAI models stretch the "conceptual soundness" test — the theoretical basis is pretraining plus fine-tuning plus prompting, and the auditor's assessment covers all three.
- "Outcomes analysis" adapts to generative output — human-review sampling, hallucination rate, accuracy against ground-truth benchmarks, fairness metrics; `mod-106` chapter on model-card claim auditing is the detailed companion.
- Challenger models for GenAI are hard; the validator may accept a bounded set of benchmarks rather than an alternate production system. State the acceptance.

## NYC Local Law 144 bias-audit summary

**Standard.** NYC Local Law 144 of 2021 and 20 RCNY §5-301 (DCWP rule). Governs the *publication* of the bias-audit summary; the underlying bias audit is a technical statistical exercise.

### Published summary content

- Date of the most recent bias audit.
- Source and explanation of the data used.
- Selection rates and impact ratios for the categories required by the rule (sex; race / ethnicity; and the specified intersections).<!-- needs-research: confirm the current 20 RCNY §5-301 subgroup list and the required impact-ratio computation formula at reading time. -->
- Distribution date for the AEDT.

### "Opinion" shape

LL144 does not express an opinion. The auditor's responsibility is to perform the calculation per the rule and to attest to its performance; the employer publishes the required summary. The bias-audit report that the auditor delivers to the employer is a separate, more detailed, non-published document that supports the summary and preserves the methodology for defence against DCWP investigations.

### AI-specific adaptations

- Scope statement — which tool, which version, which hiring context.
- Historical data vs. test data vs. categorical data — the rule permits several data shapes with corresponding methodology adjustments; the auditor's report must state which was used and justify the choice.
- Where the data is insufficient for a required subgroup, the summary must say so and the employer's exposure under the rule follows.

## Internal audit engagement report under IIA Global Internal Audit Standards

**Standard.** IIA Global Internal Audit Standards (2024), effective 2025-01-09.<!-- needs-research: confirm the current standard set and the number of the "communicating engagement results" standard at reading time. -->

### Report shape

- **Executive summary.** Brief description of the engagement, overall opinion if the IAF issues one, headline findings.
- **Engagement background and scope.** What was audited, why (link to annual plan and risk-based rationale), what was out of scope.
- **Objectives and methodology.** The engagement's objectives, the testing approach.
- **Findings.** Each in CCCER shape with IAF-defined rating.
- **Management action plans.** Attached per finding.
- **Overall engagement opinion.** Satisfactory / Needs Improvement / Unsatisfactory (or whatever vocabulary the IAF's methodology uses), supported by the findings.
- **Distribution.** Management recipients; audit committee; copies to CAE.

### Opinion vocabulary

IAF-defined. Audit committee charter commonly fixes it.

### AI-specific adaptations

- The IAF may audit the AIMS ahead of external ISO certification, the SR 11-7 validation program, or the organisation's AI risk management function. Engagement objectives frame which.
- Internal findings use the IAF's rating; do not mix with external vocabularies (chapter 2).
- Overall opinion for an AIMS-scope engagement might read: "The AIMS is **Needs Improvement** — the design is substantially complete but operating effectiveness in two control families (pre-deployment governance; post-market monitoring) shows significant gaps."

## Professional skepticism language in the opinion

Every attestation-style opinion carries boilerplate language signalling professional skepticism. Common patterns:

- "Our examination was conducted in accordance with [the standard]. Those standards require that we plan and perform the examination to obtain reasonable / limited assurance about whether [subject matter] is fairly stated / in conformance with the criteria, in all material respects."
- "We believe that the evidence we have obtained is sufficient and appropriate to provide a basis for our opinion."
- "Because of the inherent limitations of [subject matter], [specific limitation phrased]." For AI systems, this limitation is often expanded — e.g., statistical variability; non-stationarity of deployed systems; dependency on data not fully re-accessible.
- "[Firm/practitioner] has complied with the independence and other ethical requirements of the [applicable code of ethics]."

Omitting skepticism language or softening it to be "collaborative" is a report-shape error. The language is what tells the regulator and the court that the auditor took the stance the standard required.

## Opinion-type selection — a decision rule

For attestation engagements (ISAE 3000, AT-C 205, SOC 2), the opinion type follows:

- **Unmodified / unqualified.** The subject matter is fairly stated / controls operated effectively / controls are suitably designed, with no material exceptions.
- **Qualified.** There are exceptions, but they are material only to the specific aspect and the rest of the subject matter is fairly stated. "Except for [specific exception]…".
- **Adverse.** Exceptions are pervasive — the overall subject matter is not fairly stated. Rare; reserved for systemic breakdowns.
- **Disclaimer.** The auditor could not obtain sufficient appropriate evidence to express any opinion. Not a judgement about the subject matter — a judgement about the evidence available. For AI systems, disclaimer may arise when the auditor cannot obtain access to training data or model internals necessary for reperformance.

The decision rule is:

1. Is the exception material? If no → unqualified.
2. Is the exception pervasive? If no → qualified; if yes → adverse.
3. Was the evidence insufficient to form a view at all? If yes → disclaimer.

Materiality and pervasiveness are *judgements*, documented in the audit-conclusion workpaper. The rule is standard across ISA 705, AU-C 705, and the SSAEs.<!-- needs-research: confirm specific paragraph citations in the ISA 705 and AU-C 705 current revisions at reading time. -->

## Common failure modes

- **Wrong report shape.** Issuing a SOC 2 Type II when the engagement was really an ISAE 3000 reasonable-assurance engagement on a bias claim; readers cannot rely on the artefact.
- **Hybrid report.** Combining ISO 42001 certification language with SOC 2 Trust-Services vocabulary. Each audience reads it as the wrong one.
- **Vague opinion.** "The system meets applicable requirements." Does not state the opinion type, the standard, or the criteria.
- **Missing skepticism language.** The opinion reads like a marketing statement; no "reasonable assurance," no "sufficient and appropriate evidence," no independence declaration.
- **Overstating assurance.** Issuing a reasonable-assurance opinion on a scope the procedures only support at limited-assurance level.
- **Scope imprecision.** AI system boundary not stated — ranker, LLM summariser, retriever, RAG index, prompt scaffolding, fine-tuned adapters, or all of the above? Each is a different scope.
- **Mixing aspirational and binding criteria.** Report lists NIST AI RMF as the criterion; the auditor cannot issue an opinion on "conformance with" a voluntary framework without the specific subcategory basis spelled out.
- **Opinion drafted before findings closed.** Text referring to clean findings while the CAP has not yet been evaluated.
- **Omitting dates.** Report, subject matter period, management's assertion date, management's representation letter date — each required and each distinct.

## Interfaces to adjacent chapters

- Chapters 1–3 produced the findings, classifications, and responses the report is built from.
- Chapter 5 covers delivering the report to the various audiences.
- Chapter 6 picks up the register that tracks findings issued in the report through to closure.
- Chapter 7 handles the regulator-facing submission shapes that may accompany or follow the report.
- `mod-110` set up each engagement shape; this chapter is the output artefact for each.

## Summary

- The engagement shape fixes the report structure, the opinion vocabulary, and the skepticism-language expectations; the auditor does not improvise form.
- ISAE 3000 and AT-C 105/205 provide the international and U.S. attestation report shapes, with reasonable vs. limited assurance for ISAE 3000 and examination-level opinion for AT-C 205.
- SOC 2 Type II follows SSAE 18 with its five standard sections; AI boundary and complementary user entity controls deserve explicit treatment.
- ISO/IEC 42001 certification reports are binary at the certificate level; the audit report is clause-by-clause with CCCER findings graded major/minor per ISO/IEC 17021-1.
- EU AI Act Article 43 produces three artefacts — QMS report, TDA report, certificate — per Annex VII.
- SR 11-7 MRM validation reports use the bank's own ratings and the deficiency/significant/material vocabulary, with supervisory layering.
- NYC LL144 published bias-audit summaries are not opinions; they are rule-compliant disclosures.
- Internal audit reports under the IIA Global Internal Audit Standards use the IAF's own vocabulary and overall engagement opinion where methodology defines one.
- Opinion-type selection follows a materiality-and-pervasiveness decision rule shared across ISA 705 / AU-C 705 / SSAE: unmodified, qualified, adverse, disclaimer.
- Professional skepticism language is not decoration — it is the signal to regulators and courts that the auditor took the stance the standard requires.
