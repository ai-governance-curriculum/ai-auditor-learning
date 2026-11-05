# NIST AI RMF 1.0, the Playbook, and the GenAI Profile — to Auditable Criteria

## Motivation

The **NIST AI Risk Management Framework 1.0** (January 2023) is the dominant *voluntary* AI-risk framework in North America and the de-facto reference the US federal government, state regulators, and many enterprise control libraries cite. Unlike ISO/IEC 42001, it is not a management-system *conformity* standard — there is no NIST AI RMF certification, and the framework is deliberately outcomes-oriented rather than prescriptive. That makes it a *richer source of criteria* than a certification standard would be: the framework states outcomes, the **AI RMF Playbook** suggests actions, and the **NIST AI 600-1 Generative AI Profile** (July 2024) adds GenAI-specific risks and action items. The AI Auditor's work is to translate those outcomes into testable criteria, and to translate the Playbook's suggested actions into evidence expectations. This chapter walks the GOVERN / MAP / MEASURE / MANAGE spine and the GenAI Profile overlay.

## The framework's shape

- **Core functions**: GOVERN, MAP, MEASURE, MANAGE. Each has **Categories** and **Subcategories** (the testable layer).
- **Trustworthy and responsible AI characteristics**: valid-and-reliable, safe, secure-and-resilient, accountable-and-transparent, explainable-and-interpretable, privacy-enhanced, fair-with-harmful-bias-managed. These are the *attributes* the Core is supposed to produce.
- **AI RMF Playbook** — a companion document that proposes concrete actions for each Subcategory. The Playbook is not normative; it is the richest source of *suggested evidence* for criteria translation.
- **NIST AI 600-1 Generative AI Profile** (July 2024) — maps GenAI-specific risks (confabulation, dangerous or violent content, data privacy, environmental impacts, harmful bias / homogenisation, human-AI configuration, information integrity, information security, intellectual property, obscene / degrading / abusive content, value chain and component integration) to the Core and adds suggested actions.
- **Crosswalks** — NIST publishes crosswalks between the AI RMF and ISO/IEC 42001, ISO/IEC 23894, OECD AI Principles, Executive Order (EO) 14110 (and successors), and other instruments. <!-- needs-research: at reading time confirm the current set of NIST-published crosswalks and the status of EO 14110 or successor executive actions, since federal AI executive orders have been issued and reissued across 2023–2026 -->

The Core is organised by Subcategory IDs — e.g., **GOVERN 1.1, MAP 2.3, MEASURE 2.11, MANAGE 4.1** — which is the primary citation unit for criteria. Keep the Subcategory ID in the criterion `Source` field so your crosswalks (chapter 5) are mechanical.

## GOVERN — governance and culture

GOVERN is the function most easily confused with an ISO/IEC 42001 clause audit. The distinction: GOVERN categories address *outcomes* (policies in place, accountability allocated, workforce diversity-and-expertise considered, risk management integrated), where ISO/IEC 42001 clause 5 addresses *process obligations*. For criteria translation, GOVERN Subcategories are closer to what a US regulator (SR 11-7, OMB M-24-10 / M-25-21 CAIO offices, NAIC) will ask about than clause 5 of ISO/IEC 42001 is.

Representative Subcategories to translate:

- **GOVERN 1.1** — Legal, regulatory, and risk management requirements are understood, managed, and documented.
- **GOVERN 2.1** — Roles, responsibilities, and lines of communication related to mapping, measuring, and managing AI risks are documented and clear to individuals and teams throughout the organisation.
- **GOVERN 4.1** — Organisational practices are in place to foster a critical-thinking and safety-first mindset when designing, developing, deploying, and using AI systems.
- **GOVERN 5.1** — Organisational policies and practices are in place to collect, consider, prioritise, and integrate feedback from those external to the team.
- **GOVERN 6.1** — Policies and procedures are in place to address AI risks and benefits arising from third-party entities.

```
Criterion ID:             C-NIST-GOVERN-6.1-01
Source:                   NIST AI RMF 1.0 GOVERN 6.1 — third-party risk policies and procedures.
Statement:                The organisation has documented policies and procedures for AI third-party risk that (a) define the taxonomy of AI third parties (foundation-model providers, inference APIs, data vendors, labelling vendors, evaluation vendors, deployers / sub-processors), (b) define pre-engagement due diligence for each, (c) define contractual requirements (data use, security, incident notification, IP), and (d) are operated in the audit period with evidence of application to new and renewed engagements.
Evidence:                 Third-party AI policy; vendor inventory with AI classification; due-diligence workpapers for sampled engagements; executed contracts for sampled engagements.
Procedure:                Inspect policy; sample engagements from the vendor inventory; trace due diligence and contract to the policy.
Measurable attributes:    (a) policy covers all four elements (y/n per element); (b) sampled engagements comply (%).
Owner:                    Second line (procurement + AI governance).
Residual judgment:        Guard against the common finding that *renewed* contracts are not re-assessed under the AI-specific policy and silently carry pre-AI terms.
```

## MAP — context and risk identification

MAP governs the identification and documentation of context, intended use, actors, risks, impacts, and benefits before an AI system is built or deployed. This is where the **AI system impact assessment** lives on the NIST side (MAP 1, MAP 3, MAP 5); it overlaps heavily with ISO/IEC 42005 impact assessments and EU AI Act Article 27 fundamental-rights impact assessments.

Representative Subcategories to translate:

- **MAP 1.1** — Intended purposes, potentially beneficial uses, context-specific laws, norms and expectations, and prospective settings are understood and documented.
- **MAP 2.3** — Scientific integrity and TEVV (test, evaluation, verification, validation) considerations are identified and documented.
- **MAP 3.4** — Processes for operator and practitioner proficiency with AI system performance and trustworthiness characteristics are defined, assessed, and documented.
- **MAP 5.1** — Likelihood and magnitude of each identified impact are assessed.

Criteria translation for MAP generally lands as a composite criterion over the *impact assessment* artifact: either the organisation's ISO/IEC 42005-aligned impact assessment, the EU AI Act Article 27 FRIA (if applicable), or a bespoke template. One well-constructed impact assessment can be the evidence for multiple NIST MAP Subcategories; the crosswalk register in chapter 5 keeps that explicit.

## MEASURE — measurement, testing, and evaluation

MEASURE is the richest source of **measurable criteria** in the framework. Categories cover identification of methods (MEASURE 1), measurement of trustworthy characteristics (MEASURE 2 — accuracy, robustness, fairness, explainability, privacy, safety, security, environmental impact), tracking emerging risks (MEASURE 3), and evaluating measurement effectiveness (MEASURE 4).

Representative Subcategories to translate:

- **MEASURE 1.1** — Appropriate methods and metrics are identified and applied.
- **MEASURE 2.3** — AI system performance or assurance criteria are measured qualitatively or quantitatively and demonstrated for conditions similar to deployment setting(s).
- **MEASURE 2.6** — AI system is evaluated regularly for safety risks.
- **MEASURE 2.7** — AI system security and resilience are evaluated and documented.
- **MEASURE 2.11** — Fairness and bias — are evaluated and documented.
- **MEASURE 4.1** — Measurement approaches for identifying AI risks are connected to deployment context(s) and informed by input from domain experts and other end users.

The audit test pattern for a MEASURE criterion is almost always: inspect the measurement plan → inspect the measurement artifact → re-perform on a sample → compare to documented threshold → trace any deviation to remediation. This is the ISA 500 / ISA 530 shape applied to AI evaluation evidence.

Worked example — MEASURE 2.7 security-and-resilience:

```
Criterion ID:             C-NIST-MEASURE-2.7-01
Source:                   NIST AI RMF 1.0 MEASURE 2.7 — AI system security and resilience evaluated and documented.
Statement:                For each AI system in scope, the organisation has (a) executed a security-and-resilience evaluation against a documented threat model (e.g., NIST AI 100-2 adversarial ML taxonomy, MITRE ATLAS, OWASP ML Top 10, OWASP LLM Top 10 as applicable), (b) retained evaluation artifacts (plan, test vectors, results, findings, remediation), (c) addressed findings with tracked remediation or risk-acceptance evidence, and (d) re-tested after material changes to model or deployment.
Evidence:                 Threat model document; evaluation plan; test vectors / adversarial suite references; evaluation results; finding tickets; remediation / risk-acceptance evidence.
Procedure:                Inspect threat model and plan; re-perform a sampled subset of adversarial / red-team tests (requires auditor's expert); verify finding closure.
Measurable attributes:    (a) threat model current (y/n); (b) evaluation executed in period (y/n); (c) findings with closure or acceptance (%); (d) re-test after material change (y/n per material change).
Owner:                    First line (safety / security teams) with second-line (release assurance) verification.
Residual judgment:        The threat model shapes the test coverage; a narrow threat model that produces "no findings" is a frequent false pass.
```

## MANAGE — risk prioritisation, response, and recovery

MANAGE covers risk prioritisation (MANAGE 1), response and recovery (MANAGE 2), third-party-risk response (MANAGE 3), and ongoing monitoring and change management (MANAGE 4). It is the function closest to ISO/IEC 42001 clauses 6.1.3 (risk treatment), 8.3 (operational risk-treatment execution), and 10.1 (nonconformity and corrective action).

Representative Subcategories to translate:

- **MANAGE 1.3** — Responses to the AI risks deemed high priority are developed, planned, and documented.
- **MANAGE 2.3** — Mechanisms are in place and applied to sustain the value of deployed AI systems.
- **MANAGE 4.1** — Post-deployment AI system monitoring plans are implemented, including mechanisms for capturing and evaluating input from users and other relevant AI actors.

MANAGE 4.1 is the natural anchor for **post-market monitoring criteria** that cross to EU AI Act Article 72 and to sector obligations (SR 11-7 ongoing monitoring, FDA PCCP change control). Hold a single criterion statement and tag it to all three sources in the crosswalk.

## The AI RMF Playbook — turning suggested actions into evidence expectations

The Playbook sits next to the Core. For each Subcategory it lists **About**, **Actions**, **Transparency and Documentation**, and **References**. The criteria translator's main use for the Playbook is the **Actions** list: the suggested actions are the pool from which to draw *expected evidence* for a criterion.

Translation discipline: an auditable criterion does *not* restate every Playbook action verbatim (the Playbook is non-normative). Instead, the criterion names the outcome and the auditor uses the Playbook as a *reference list of evidence candidates* at fieldwork — if the organisation's evidence package matches many Playbook actions, the criterion is well-supported; if it matches none, the organisation and the auditor need to discuss suitable alternative evidence before the engagement proceeds.

## NIST AI 600-1 Generative AI Profile — the GenAI overlay

The **GenAI Profile** (NIST AI 600-1, July 2024) is organised around twelve GenAI-specific risks and proposes actions keyed to the Core Subcategories. The practical audit use: for any engagement whose scope includes a generative AI system, add a *GenAI overlay* of criteria to the baseline NIST criteria set. The GenAI risks the auditor should hold criteria on:

- **Confabulation** (hallucination) — evaluation methodology and tolerance; grounding evidence; user disclosure.
- **Dangerous or violent recommendations** — content-safety classifier posture; red-team coverage.
- **Data privacy** — training-data provenance; PII handling; model inversion / memorisation risk.
- **Environmental impacts** — training and inference energy / carbon measurement.
- **Harmful bias and homogenisation** — eval sets; fairness measurement across identified segments; mitigation evidence.
- **Human-AI configuration** — human oversight controls (UI, review, override) — overlaps EU AI Act Article 14.
- **Information integrity** — provenance / watermark / content credentials.
- **Information security** — prompt-injection, jailbreak, tool-call abuse.
- **Intellectual property** — training-data IP posture, output IP posture, licensing.
- **Obscene, degrading, or abusive content** — safety classifiers, red-team coverage, incident-handling.
- **Value chain and component integration** — upstream provider posture, model-card inheritance, ML-BOM.
- **CBRN information / capability uplift** — covered selectively depending on system and jurisdiction.

For each, write one or two criteria using the template. Many of these are *measurable* criteria with method dependence; cite the method the organisation used (e.g., which jailbreak taxonomy, which content-safety classifier, which hallucination benchmark) and treat it as a measurable-criterion method citation.

```
Criterion ID:             C-NIST-GENAI-INFOSEC-01
Source:                   NIST AI 600-1 GenAI Profile — information security risk; cross-reference MEASURE 2.7, MANAGE 2.3.
Statement:                For each generative AI system in scope, the organisation measures susceptibility to prompt-injection, jailbreak, and tool-call abuse against a documented adversarial suite (e.g., OWASP LLM Top 10 categories; Microsoft / Google / Anthropic / open-source red-team benchmarks named in the plan) at a defined cadence and after material deployment change, and retains the test artifacts and finding register.
Evidence:                 Adversarial test plan; suite version references; run logs; findings; remediation or risk-acceptance.
Procedure:                Inspect plan; re-perform a sampled subset (auditor's expert); trace findings to remediation.
Measurable attributes:    (a) suite cadence met (y/n); (b) findings addressed (% within target time).
Owner:                    First line (safety / security) with second-line verification.
Residual judgment:        Suite coverage matters more than pass rate — guard against vendors "passing" a narrow benchmark they tuned against.
```

## Crosswalks that NIST publishes (and that you should re-use, not re-author)

NIST maintains crosswalks between the AI RMF and other instruments. The AI Auditor should **consume** these rather than hand-author equivalents:

- **AI RMF ↔ ISO/IEC 42001** — Subcategory-by-clause crosswalk.
- **AI RMF ↔ ISO/IEC 23894** — AI risk-management guidance crosswalk.
- **AI RMF ↔ OECD AI Principles**.
- **AI RMF ↔ EO 14110 / successor EOs ↔ OMB M-24-10 / M-25-21** — federal-agency obligations on AI risk management, AI inventory, and CAIO duties for US federal use cases. <!-- needs-research: confirm the live federal EO and OMB guidance at reading time -->

Treat the NIST-published crosswalks as *pre-built input* to the crosswalk register you build in chapter 5. The `ai-governance-analyst` (L15) can refresh them; the auditor validates their current applicability.

## Where NIST does not get you all the way

Cases where AI RMF criteria need supplement before they are suitable for an attestation engagement:

- **No conformity level.** NIST does not define "conformance"; you cannot "fail an AI RMF audit" in the way you can fail ISO/IEC 42001 certification. Criteria you author must set their own pass/fail logic explicitly.
- **No sector specialisation.** AI RMF is deliberately sector-agnostic. For banking, healthcare, insurance, government, you overlay sector criteria (chapter 4).
- **Playbook is not normative.** You cannot cite the Playbook as a *must-do*; use it as an evidence-candidate list only.
- **GenAI Profile risks evolve.** The twelve risks listed are a point-in-time cut. For engagements covering frontier GenAI, add criteria on capabilities and risks not covered in NIST AI 600-1 only when supported by a defensible reference (e.g., the EU AI Office GPAI Code of Practice for systemic-risk models — chapter 4).

## Summary

- The NIST AI RMF 1.0 Core (GOVERN / MAP / MEASURE / MANAGE) is organised by Subcategory; use the Subcategory ID as the stable citation in criteria.
- GOVERN maps closest to governance and policy criteria; MAP to impact-assessment criteria; MEASURE is the richest source of measurable-metric criteria; MANAGE maps closest to risk-response and post-deployment monitoring criteria.
- The AI RMF Playbook is non-normative — use its suggested actions as an *evidence-candidate list*, not a mandatory checklist.
- The GenAI Profile (NIST AI 600-1) adds twelve GenAI risk areas; add a GenAI overlay of criteria whenever a generative system is in scope.
- NIST publishes crosswalks to ISO/IEC 42001, ISO/IEC 23894, OECD, and US federal instruments — consume them rather than re-authoring.
- NIST criteria need sector overlay (chapter 4) and explicit pass/fail logic before they support an attestation conclusion.
