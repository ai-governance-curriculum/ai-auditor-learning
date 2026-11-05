# The ForHumanity IAAIS Engagement — Auditing Against the FHCA Criteria

## Motivation

ISO 42001 (chapter in `mod-105`) and the EU AI Act (chapter 1) are *mandatory-ish* regimes — the first through market demand for certification, the second through regulation for EU market entry. ForHumanity's **Independent Audit of AI Systems (IAAIS)** sits beside them as a **voluntary, multi-dimensional audit** that pools AI Ethics, AI Trust, Algorithm Bias & Discrimination, Privacy, and Cybersecurity audit criteria into a single engagement.

For many organisations IAAIS answers a different question from ISO 42001: not "does your management system operate?" but "does this specific AI system, as it is used in the world, hold up under a published, auditable set of criteria?". That difference shapes everything about the engagement — the subject matter is the AI system plus its context of use, the criteria are the **ForHumanity Certified Auditor (FHCA) criteria set**, and the evidence is drawn from the deployer and provider jointly.

The auditor arrives as a **FHCA-credentialled lead** with a team of **Certified Auditors of AI Systems (CAAIS)** — nomenclature current at authoring time but subject to revision in the ForHumanity scheme. <!-- needs-research: confirm current ForHumanity credential names (FHCA / CAAIS / predecessor acronyms), audit scheme versions, and governance structure at reading time; ForHumanity has revised nomenclature multiple times in the 2023–2026 window -->

This chapter is the auditor's shape for an IAAIS engagement: the scheme's position in the audit market, the five criteria-area shape, the engagement sequence, the FHCA report, and the reconciliation points with the other audit shapes in this module.

## Where IAAIS fits in the market

IAAIS is designed to be **portable** — one engagement whose output is useful to more than one audience:

- **Regulators** — US state attorneys general (NYC LL144 overlap, Colorado SB 24-205, Illinois AIVIA), EU authorities (as supporting evidence under the AI Act), Canadian privacy commissioners, UK ICO.
- **Boards and audit committees** — a third-party opinion that is not an ISO certificate (the board has that too) but reaches further into the AI-system's behaviour.
- **Procurement counterparties** — downstream deployers who want a signal about an upstream provider that is less heavy than a SOC 2 but more domain-specific.
- **Public-facing accountability** — some IAAIS engagements are published; some are restricted; the auditor's engagement letter defines distribution.

IAAIS **is not** a conformity-assessment under the EU AI Act, a certification under ISO 42001, or an attestation under SSAE / ISAE. It is an **assurance engagement** of its own kind, with its criteria published by ForHumanity and its auditor conduct subject to the ForHumanity scheme rules.

## The five criteria-area stack

An IAAIS engagement is organised around **five criteria areas**, each a self-contained workpaper set:

### AI Ethics

The provider / deployer's published ethical commitments and principles; the operationalisation of each principle into verifiable controls; the exception-handling mechanism when principles conflict; the governance of the principles (who owns them, how are they updated, how are they enforced).

Audit test shape: for each stated principle, a traceability trail from the principle text to at least one control, at least one piece of evidence of operation, and at least one named role accountable; principles with no operational linkage are findings; principles that generate no exceptions in a reasonable period may be either genuinely absolute or genuinely performative — the auditor must distinguish.

### AI Trust

How the AI system builds **justified trust** with its users and affected parties. This is the broadest of the criteria areas and reaches into: user-facing transparency (the AI is identified as AI; capability and limitation disclosures; disclosure of automated decision-making); meaningful explanations where decisions affect people; feedback and redress channels; the lived user experience; contestability for consequential decisions.

Audit test shape: samples of actual user interactions (where ethical review and consent permits); the user-facing material exactly as it reaches users (not the internal spec); the volume and disposition of redress / complaint traffic; evidence the organisation responds to feedback, not just records it.

### Algorithm Bias and Discrimination

The provider / deployer's bias-and-discrimination controls across the AI system's life cycle: training-data bias examination; model-level bias testing (selection rate, impact ratio, calibration-by-group, equal-opportunity and equalised-odds where applicable); deployment-time bias monitoring; incident response for bias claims; alignment with applicable anti-discrimination law.

For US-context engagements, this criteria area aligns with the chapter 4 LL144 bias-audit shape (and with EEOC guidance, OFCCP, ADA, Title VII case law); for EU-context engagements, it aligns with Article 10 data governance and fundamental-rights protections. IAAIS is not the LL144 bias audit (that is chapter 4's distinct statutory engagement), but the two overlap in evidence.

Audit test shape: coverage of protected classes applicable in jurisdiction; the data used for testing and whether it supports reliable bias measurement; statistical methodology with explicit power and multiple-comparisons handling; the mitigation chain from measurement to action to residual-risk acceptance; evidence of post-deployment bias monitoring and incident handling.

### Privacy

The AI system's privacy posture across its life cycle: lawful basis for processing (GDPR / applicable US sectoral laws / state privacy statutes); data minimisation; purpose limitation; retention; data-subject rights operationalisation (access, correction, erasure, portability, objection, restriction); automated-decision-making safeguards (GDPR Article 22 / equivalents); privacy-by-design evidence; third-party data flows; privacy impact assessment / data protection impact assessment (DPIA) coverage.

Audit test shape: end-to-end data-flow map; lawful-basis documentation per flow; data-subject-rights request handling (sample rights requests, test fulfilment); DPIA coverage and update cadence; cross-border transfer controls; integration with Article 10 data governance (EU AI Act) or state-equivalent data-protection laws.

### Cybersecurity

The AI system's cybersecurity posture against AI-specific threats and traditional threats: baseline cyber controls (NIST CSF, ISO 27001, SOC 2 Trust Services Criteria equivalents); AI-specific threats (data poisoning, model poisoning, adversarial examples, prompt injection, model extraction, confidentiality attacks, supply-chain-model threats); incident-response coverage of AI-specific incidents; penetration-testing evidence; third-party-cybersecurity attestation for upstream vendors.

Audit test shape: threat model (ATLAS / OWASP ML Top 10 / specialist frameworks mapped); defence-in-depth evidence for AI-specific threats; red-team or adversarial-test evidence; cyber-incident-response evidence specifically for AI incidents (not generic cyber incidents); the interface with the Article 15 cybersecurity audit under the EU AI Act for systems in that lane.

## The engagement sequence

A typical IAAIS engagement moves through five motions. The sequence is not standardised to the same letter as ISO 17021-1; the ForHumanity scheme allows flexibility but the auditor's engagement letter must pre-commit to a specific plan.

### Motion 1 — Scoping

The scoping motion fixes:

- **The AI system(s) in scope.** A single system or a related set (a product family). Scope-creep across systems is a common failure mode.
- **The jurisdiction(s) of use.** Determines applicable legal frames — NYC LL144, Colorado SB 24-205, Illinois AIVIA, GDPR, CCPA/CPRA, state biometric laws (Illinois BIPA, Texas CUBI), sector regimes.
- **The population of affected persons.** Defines sampling frames for user-interaction, bias, and privacy testing.
- **The criteria version.** Which FHCA criteria set version; which measurement protocols; which thresholds.
- **The intended audience.** Board / regulator / counterparty / public; shapes distribution and redaction.
- **The report shape.** Public summary vs. detailed report; disclosure of findings vs. aggregated score.

### Motion 2 — Readiness and evidence request

The auditor issues the evidence request against the five-criteria stack. The provider / deployer responds; the auditor triages for completeness and schedules fieldwork. A reasonable IAAIS engagement does not survive a request-response round that reveals Ethics and Trust materials are absent — fieldwork is rescheduled rather than attempted on missing evidence.

### Motion 3 — Fieldwork across the five criteria areas

Fieldwork executes in parallel across the five areas, with named leads per area (the FHCA-lead stays overall, with CAAIS leads per area). Each area produces its own findings grid; the lead consolidates into an engagement-level findings register.

### Motion 4 — Corrective-action window and re-test

Unlike ISO certification where findings close after a management-response period, IAAIS **may** include a corrective-action window and re-test depending on scheme rules and engagement letter. If the window is present, findings graded above a threshold must be addressed within a defined period and re-tested; findings below the threshold are reported as-is with management commentary.

### Motion 5 — Report issuance

The FHCA lead signs the report. The report shape is detailed below. For public engagements, the organisation may also publish a summary. ForHumanity's scheme may require a filing of the engagement outcome (depending on scheme version and engagement type).

## The FHCA report shape

The IAAIS report structure is purposely multi-audience. A typical issued report contains:

1. **Scope and criteria statement** — the system, jurisdiction, criteria version, audit period, limitations.
2. **Opinion** — a conclusion per criteria area and an overall opinion; the scheme defines the opinion vocabulary (conforms / partially conforms / does not conform; or a numeric scoring; depending on scheme version).
3. **Findings** — per area, per criterion, severity, management response, re-test status.
4. **Methodology appendix** — sampling, evaluation, test design, use of experts; sufficient for a knowledgeable reader to assess the work.
5. **Signatory block** — FHCA lead and CAAIS team, their independence representations, the engagement firm.
6. **Management assertion** (when the scheme uses an attestation shape) — the organisation's assertion that the subject matter conforms to the criteria; the audit's opinion addresses that assertion.

The report is **not** a certificate. An IAAIS engagement may produce a mark or seal under the ForHumanity scheme; the mark references the specific engagement and criteria version and does not stand on its own as compliance evidence for any statutory regime.

## Interfaces with mandatory regimes

The practical value of IAAIS often comes from how its findings feed mandatory regimes.

- **NYC LL144 (chapter 4).** Algorithm-Bias-and-Discrimination area evidence can be reused in LL144 bias-audit computation, but LL144 has its own form, independence rules, and publication obligations — IAAIS does not substitute.
- **Colorado SB 24-205 (chapter 7).** The Trust, Bias, and Privacy areas feed the deployer's "reasonable care" defence under Colorado's algorithmic-discrimination prohibition for high-risk AI; IAAIS is persuasive evidence but Colorado's implementing rules define the statutory evidence shape. <!-- needs-research: confirm Colorado AI Act implementing rules status and specific "reasonable care" evidence expectations at reading time; the AG's rulemaking continues to progress -->
- **Illinois AIVIA (chapter 7).** The Illinois Artificial Intelligence Video Interview Act's required disclosures and the Illinois AI in Employment Decisions amendments (HB 3773) overlap with IAAIS Trust and Bias areas.
- **EU AI Act Annex III high-risk (chapter 1).** IAAIS evidence may support an Article 43(1) Annex VI self-attestation or complement an Annex VII notified-body assessment; it does not replace either. Providers sometimes use IAAIS to pre-rehearse the Article 43 engagement.
- **ISO 42001 (`mod-105`).** IAAIS ethics, trust, privacy, bias, and cybersecurity findings often feed the ISO 42001 AIMS clause 6 risk register and clause 9 performance-evaluation data; the ISO 42001 audit does not duplicate IAAIS fieldwork but reuses its findings.

A single AI system frequently sits at the intersection of several regimes. IAAIS is the **portable** engagement that produces evidence feeding each.

## Independence and competence

ForHumanity's scheme sets independence and competence requirements for the FHCA lead and the CAAIS team:

- **Independence.** The engagement team cannot have consulted on the subject system within a defined look-back period; cannot have commercial dependencies on the engaging party; must disclose personal, financial, and structural conflicts. The engagement letter captures the independence representation.
- **Competence.** The FHCA lead and the CAAIS specialists hold current ForHumanity credentials; specialist areas (privacy, cybersecurity, data science) are staffed with suitably-credentialled team members or subject-matter experts.
- **Methodology adherence.** Fieldwork follows ForHumanity's audit scheme; deviations are disclosed; the report cannot refer to the ForHumanity scheme without actually adhering to it.

The IAAIS engagement runs under the ForHumanity scheme's governance; appeals and complaints have a defined route (`mod-101` chapter 7 discusses the broader scheme-governance posture for voluntary audits).

## Common failure modes

- **Scope-creep across systems.** Engagement letter named one AI system; fieldwork drifts across a product line; the opinion covers less of each than the client needed.
- **Trust-area theatre.** Trust evidence is marketing copy rather than observation of the user experience; auditor must insist on user-facing artefacts and, where permitted, interaction samples.
- **Bias testing not useful to LL144 or Colorado.** Statistical methodology differs from what the statutory regime requires; IAAIS findings cannot be reused; the client has paid twice.
- **Privacy criteria shallow.** DPIA in the dossier, but no live-system data-flow mapping; the auditor cannot opine on operational privacy posture.
- **Cybersecurity relies on upstream SOC 2.** Upstream SOC 2 does not cover AI-specific threats; IAAIS cybersecurity area must test the client's AI-specific controls, not rest on the vendor's generic cybersecurity attestation.
- **Report shape mismatched to audience.** Board wants a two-page summary; the report is 90 pages; or the regulator wants evidence-level detail; the report is a two-page summary.
- **Independence representation thin.** Engagement team has prior consulting history with the client; the engagement letter does not disclose it; the finding's defensibility is impaired.
- **Criteria version drift.** Fieldwork executed against one FHCA criteria version; report cites another; the audit's claim is ambiguous.

## When the auditor uses IAAIS

The engagement-shape chooser in chapter 9 returns to IAAIS when:

- the client needs a **single engagement for multiple audiences** and no mandatory regime fits alone;
- the client needs a **US-jurisdiction audit** with ethics / trust / bias / privacy / cybersecurity in combination;
- the client is preparing for mandatory regimes and wants a **pre-rehearsal** that produces reusable evidence;
- the client is **publishing** an audit outcome and wants a scheme the public can reference.

IAAIS is often *supplementary* to ISO 42001, EU AI Act conformity, SR 11-7 (chapter 5), FDA GMLP (chapter 6), and SOC-for-AI (chapter 8); chapter 9 defends the combination.

## Summary

- The ForHumanity IAAIS is a voluntary, multi-dimensional assurance engagement across five criteria areas: AI Ethics, AI Trust, Algorithm Bias and Discrimination, Privacy, Cybersecurity.
- The engagement is led by an FHCA-credentialled lead with CAAIS specialists (names current at authoring time, subject to revision in the ForHumanity scheme) and moves through scoping, readiness, five-area fieldwork, optional corrective-action window, and report issuance.
- The report is multi-audience: scope and criteria, opinion per area and overall, findings per criterion with severity and management response, methodology appendix, signatory block, and (where applicable) management assertion.
- IAAIS is portable — findings feed NYC LL144, Colorado SB 24-205, Illinois AIVIA, EU AI Act Article 43 preparations, ISO 42001 AIMS, and sectoral audits; it does not replace any of those mandatory regimes.
- Independence, competence, and methodology adherence are governed by the ForHumanity scheme; the engagement letter captures representations and the scheme's governance route handles appeals.
- The engagement-shape chooser (chapter 9) returns to IAAIS when the audience is multi-stakeholder, the jurisdiction is primarily US, and the client needs a reusable evidence base across regimes.
