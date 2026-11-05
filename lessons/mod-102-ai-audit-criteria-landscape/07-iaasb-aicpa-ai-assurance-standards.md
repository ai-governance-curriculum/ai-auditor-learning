# The IAASB AI Assurance Standards Pipeline and the AICPA SOC-for-AI Work

## Motivation

The methodology standards for external AI assurance are catching up to the frameworks the assurance is being issued against. The **IAASB** has a non-financial-information assurance stack that today rests on **ISAE 3000 (Revised)** by analogy, with new standards landing (notably **ISSA 5000** for sustainability assurance in late 2024, and ongoing IAASB work on technology-related subject matters). The **AICPA Assurance Services Executive Committee (ASEC)** has been developing AI-specific trust services criteria and SOC-for-AI exposure drafts. The AI Auditor practising external attestation needs to know (a) what is published and in force, (b) what is in exposure or consultation and may apply before the engagement is reported, and (c) where the standard remains immature and professional judgment under the general framework still carries the engagement. This chapter is the state-of-the-pipeline map and the professional-judgment survival guide.

## Baseline that is in force today

Before the pipeline, the baseline the AI Auditor can cite without ambiguity:

- **IAASB International Framework for Assurance Engagements** — elements of an assurance engagement, two levels of assurance.
- **ISAE 3000 (Revised)** — the methodology standard for assurance on subject matter other than historical financial information. AI engagements live here by default.
- **ISA 500 (evidence)**, **ISA 530 (sampling)**, **ISA 620 (auditor's expert)**, **ISA 320 (materiality)** — applied by analogy as named in ISAE 3000.
- **ISQM 1 and ISQM 2** — firm quality management.
- **AT-C 105 (common concepts)**, **AT-C 205 (examination)**, **AT-C 210 (review)**, **AT-C 215 (AUP)** — AICPA attestation stack.
- **QM 1 and QM 2** — US firm quality management.
- **AICPA Trust Services Criteria** (security, availability, processing integrity, confidentiality, privacy) — underlies SOC 2 and the family of SOC reports.

For an AI engagement delivered today, the report cites ISAE 3000 or AT-C 205, the criteria (per chapters 2–5), and any applicable AT-C sub-standard. That is defensible without any new AI-specific standard.

## IAASB — what is in motion

### ISSA 5000 — General Requirements for Sustainability Assurance Engagements

Issued by the IAASB in **November 2024** and effective for engagements with periods beginning on or after 15 December 2026 (with earlier adoption permitted), **ISSA 5000** is the IAASB's first topic-area assurance standard for sustainability information. It was written to be *framework-agnostic* and *subject-matter-agnostic enough* that practitioners expect substantial read-across to AI assurance engagements where the subject matter sits at the overlap (environmental impact of model training, GenAI energy reporting, AI-driven ESG metrics). <!-- needs-research: confirm ISSA 5000's final effective date, applicability, and any IAASB guidance on AI subject matter at reading time; the IAASB continues to publish non-authoritative guidance alongside the standard -->

Practical implication for the AI Auditor: for engagements covering AI-adjacent sustainability subject matter (training carbon footprint, GenAI energy intensity, model-lifecycle emissions), ISSA 5000 may be the most proximate IAASB standard — and even for pure-AI engagements, its evidence and criteria discipline refines the ISAE 3000 by-analogy baseline.

### IAASB thought leadership on technology-related subject matter

The IAASB publishes staff thought leadership, consultation papers, and (occasionally) non-authoritative guidance on technology-related subject matters, including AI. Watch:

- **IAASB Discussion Paper / Consultation Paper(s) on AI assurance** — the IAASB Board has signalled work on an AI-specific standard-setting agenda; pipeline items evolve. <!-- needs-research: confirm active IAASB AI-related projects, exposure drafts, and board papers at reading time -->
- **Non-authoritative guidance on applying ISAE 3000 to emerging subject matter** — periodically published and cited in engagement workpapers as evidence of the methodology applied.

Treat IAASB thought-leadership documents in the workpaper as **evidence of due professional care**, not as citeable methodology standards. The citeable standard remains ISAE 3000 until a specific AI standard is issued.

## AICPA — what is in motion

### AICPA Trust Services Criteria extensions for AI

The **Assurance Services Executive Committee (ASEC)** has been developing AI-specific trust services criteria and/or SOC-for-AI exposure drafts to layer over the existing Trust Services Criteria. <!-- needs-research: confirm the current state of AICPA SOC-for-AI exposure drafts and any published AI-specific Trust Services Criteria at reading time; the AICPA ASEC has consulted repeatedly on this across 2023–2026 -->

Practical implication: a SOC 2 report issued today over an AI service organisation uses the existing TSC (security, availability, processing integrity, confidentiality, privacy); AI-specific criteria are typically added as **Additional Suitable Criteria** per AT-C 105, drawn from NIST AI RMF / ISO/IEC 42001 / the service organisation's framework. Once AICPA publishes AI-specific TSC, the engagement can cite the TSC directly.

### SOC for AI reports

AICPA has signalled the development of **SOC for AI** reports — analogous to SOC 2 but with AI-specific criteria. The engagement form (examination under AT-C 205), the responsible-party assertion, and the auditor's conclusion remain the same; the criteria layer is the point of innovation. <!-- needs-research: confirm whether AICPA has published SOC for AI as a finalised engagement product or is still in exposure at reading time -->

### AICPA AI-related practice guidance

The AICPA Center for Audit Quality and ASEC periodically publish practice guides for auditors on AI-related subject matters (use of AI by the preparer; use of AI by the auditor). Workpaper treatment: cite as professional-literature reference where applicable, but not as substitute for the codified AT-C stack.

## Where the standard is immature — professional judgment carries the engagement

Four kinds of immaturity recur. Each is manageable, but each must be documented in the workpaper and in the report.

### Immaturity 1 — No AI-specific methodology standard

ISAE 3000 / AT-C 205 are generic. There is no AI-specific analogue of (e.g.) ISAE 3410 (GHG) that a regulator would expect to see cited. The workpaper documents application of ISA 500 / 530 / 620 / 320 by analogy and the specific adaptations for AI subject matter (re-performance of eval metrics, use of auditor's expert on ML / red-team, materiality adopted for the subject matter). The report cites ISAE 3000 explicitly, references the criteria, and (where applicable) references ISSA 5000 if the subject matter has a sustainability overlap.

### Immaturity 2 — Suitable criteria still forming

The criteria landscape is moving: ISO/IEC 42001 is stable; EU AI Act harmonised standards are still being issued; NIST AI RMF revisions and the GenAI Profile are updated; AICPA AI-specific TSC is in exposure. The engagement letter names the criteria precisely (framework + version + applied clauses), the report discloses the criteria status, and the workpaper carries the criteria-suitability assessment under ISAE 3000.A45 / AT-C 105 criteria requirements. When criteria are *specifically developed* by the responsible party, the engagement discloses this and tests suitability explicitly.

### Immaturity 3 — Measurement methods still forming

For measurable criteria (fairness, robustness, calibration, hallucination, adversarial vulnerability), methods and benchmarks evolve rapidly. The engagement letter names the methods the responsible party uses; the workpaper tests method appropriateness; the report describes method limitations where they would affect the user's understanding. The practitioner's expert (ISA 620 by analogy) is the usual vehicle to assess method suitability.

### Immaturity 4 — No regulator with final interpretive authority

For voluntary frameworks (NIST, ISO/IEC 42001 outside certification), no regulator issues binding interpretations; divergent practice among firms will exist. For the EU AI Act, interpretations will develop through the AI Office, national competent authorities, and courts over 2025–2030. Workpaper carries the firm's interpretation and the citations supporting it; the audit opinion holds the practitioner's view.

## The auditor's expert — standard-adjacent but engagement-critical

Few engagements of material AI subject matter run without an **auditor's expert** under ISA 620 by analogy. The expert's scope must be documented at engagement acceptance: what the expert will assess (model architecture; evaluation methodology; red-team coverage; privacy posture; security posture), what the expert will not, how the auditor will review the expert's work, and how the auditor's conclusion will reference the expert (or not, where the expert's work is a component of the practitioner's own basis for conclusion).

For AI engagements, the frequent expert roles:

- **ML/AI architecture SME** — model selection, training pipeline, deployment architecture, inference-stack security.
- **Evaluation methodology SME** — eval suite design, judge-vs-human calibration, statistical significance, sampling.
- **Red-team / adversarial ML SME** — threat model, suite coverage against NIST AI 100-2, MITRE ATLAS, OWASP LLM Top 10.
- **Privacy engineering SME** — training-data provenance, de-identification, memorisation risk, downstream privacy.
- **Security engineering SME** — authentication / authorisation of model APIs, prompt-injection, model-extraction / theft, supply chain.

ISA 620 (and AT-C 105 .45 reliance rules) apply to each: competence, capability, objectivity; scope; review.

## SOC 2 with AI-specific additional criteria — the common engagement shape today

Until SOC for AI is a published AICPA product, the common service-organisation engagement for an AI provider is a **SOC 2 Type II** report over the existing TSC with **Additional Suitable Criteria** drawn from NIST AI RMF, ISO/IEC 42001, or the provider's documented control framework. Report form:

- Management's assertion identifies the TSC plus the Additional Suitable Criteria.
- Independent service auditor's report issues a positive-assurance opinion.
- Description of the system includes the AI subject matter boundaries (model(s), inference service, training stack if in scope).
- Description of controls and tests of controls includes AI-specific controls (training-data governance, eval, red-team, guardrails, monitoring, incident response).

The deployer (user organisation) reads the report under its own third-party assurance program. Expect deployers to request *additional* AI-specific controls as scoping conversations mature.

## Independence considerations as the standards mature

Each AICPA / IAASB standard carries independence rules the firm must comply with. For AI engagements specifically:

- **No management decisions** by the audit firm about model design, training-data selection, eval methodology, incident response. Advisory projects adjacent to the engagement create self-review threats; evaluate case-by-case under the **IESBA International Code of Ethics** / AICPA Code / local-jurisdiction equivalents.
- **AI tools used by the audit team** (document-review LLMs, workpaper-summarisation AI) have their own professional-skepticism and quality implications; firm QM policies increasingly specify use and retention.
- **Auditor's expert objectivity** — the expert is subject to the same independence posture as the auditor for the aspects of the work the auditor relies on.

## Practical workpaper discipline (today's state)

For an AI-assurance engagement issued under current standards:

- **Engagement letter** cites ISAE 3000 (Revised) or AT-C 105 + AT-C 205; identifies framework criteria with version; identifies auditor's expert(s) and scope; identifies level of assurance; identifies intended users.
- **Planning memo** documents materiality for the subject matter (ISA 320 analogy), risk of material misstatement, use-of-expert plan.
- **Criteria-suitability workpaper** records the five-part suitability test for each applied framework, with specifically-developed criteria flagged.
- **Fieldwork workpapers** apply ISA 500 / 530 analogues; sampling rationale documented; re-performance documented; expert work documented.
- **Reporting workpaper** confirms the report form matches the level of assurance; AT-C 205 / ISAE 3000 report language used verbatim where mandatory.
- **ISQM 1 / QM 1 artefacts** — engagement acceptance, quality reviewer (where required), engagement quality review under ISQM 2 / QM 2.

## When the pipeline lands — what changes

Three plausible near-term shifts the AI Auditor should plan for:

- **AICPA publishes SOC for AI** — SOC 2 engagements with AI subject matter migrate to SOC for AI; transitional-period guidance governs cutover.
- **IAASB issues an AI-related standard or amends ISAE 3000** — workpapers cite the specific standard; AI-specific materiality / evidence patterns gain codification.
- **EU AI Act harmonised standards fully published** — JTC 21 standards cited in the OJ give presumption of conformity; audit evidence can rest on the harmonised standard directly.

None of these are reasons to postpone engagements today. They are reasons to design workpapers with explicit method citations so future-cycle re-work is modest.

## Summary

- Today's AI-assurance baseline is **ISAE 3000 (Revised)** + supporting ISAs by analogy (IAASB) or **AT-C 105 + AT-C 205** + applicable Trust Services Criteria (AICPA), with firm-wide **ISQM 1/2** or **QM 1/2** quality management.
- **ISSA 5000** (IAASB sustainability assurance, effective 15 December 2026) is the most recent IAASB topic-area standard; its evidence and criteria discipline reads across to AI-adjacent subject matter.
- **AICPA Trust Services Criteria with AI-specific additions** are the current SOC 2 shape for AI service organisations; a formal **SOC for AI** engagement product is in the AICPA pipeline.
- Where standards are immature, the engagement runs on documented professional judgment under the general framework; the workpaper explicitly carries the application-by-analogy rationale.
- The **auditor's expert** under ISA 620 by analogy is a near-constant feature; scope, competence, objectivity, and review of the expert's work are documented at acceptance and throughout fieldwork.
- The AI Auditor should design workpapers today so pipeline standards (SOC for AI, IAASB AI standards, EU harmonised standards) can be cited at cutover with minimal re-work.
