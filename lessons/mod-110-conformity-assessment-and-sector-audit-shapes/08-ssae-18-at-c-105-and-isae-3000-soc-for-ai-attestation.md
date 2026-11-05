# SSAE 18 / AT-C 105 / ISAE 3000 — The SOC-for-AI Attestation Engagement

## Motivation

ISO 42001 (`mod-105`) delivers a certificate. The EU AI Act Article 43 (chapter 1) delivers a CE-marking decision. The IAAIS (chapter 3) delivers a scheme-governed audit report. The **SSAE 18 / AT-C 105 attestation**, the **ISAE 3000 (Revised) assurance engagement**, and the derived **SOC 2** service-organisation reports deliver a different artefact — an **independent accountant's examination report** on management's assertion about subject matter, prepared under the IAASB international assurance framework or the AICPA US attestation framework.

For AI controls, the market is calling this emerging shape **SOC for AI**. It reuses the SOC 2 Type II structure (period-of-coverage, Trust-Services-Criteria-style control categories, management's description, auditor's opinion on design and operating effectiveness) and extends it with AI-specific criteria — a crosswalk that the AICPA's Assurance Services Executive Committee and practitioner firms have been building out. <!-- needs-research: confirm the current AICPA SOC-for-AI criteria publication (whether as an extension of the Trust Services Criteria, a new description-criteria publication, or a standalone attestation framework) at reading time; the ASEC publication pipeline continues to evolve -->

The auditor arrives here as the **examining accountant** — a CPA firm (US) or an accounting firm operating under IFAC-member-body rules (international). The engagement type is an **attestation engagement**, not a certification, and the rules that govern it are the IAASB and AICPA standards stack from `mod-101`. This chapter is the auditor's shape for a SOC-for-AI engagement: scoping the description, the criteria, the two kinds of effectiveness, authoring the report, and the integration with the AICPA SOC 2 framework the market is extending.

## The standards stack — attestation in one place

### IAASB — international

- **International Framework for Assurance Engagements.** Defines the three-party relationship (responsible party, intended users, practitioner), five elements of an assurance engagement (three-party relationship, subject matter, criteria, evidence, written conclusion), and the two levels of assurance (reasonable, limited).
- **ISAE 3000 (Revised) — Assurance Engagements Other Than Audits or Reviews of Historical Financial Information.** The horizontal standard for all non-financial-statement assurance engagements. Prescribes planning, risk assessment, evidence, documentation, written representations, and conclusion.
- **ISAE 3402 — Assurance Reports on Controls at a Service Organisation.** The SAS-70 / SOC 1 international analogue; narrow to controls relevant to user organisations' internal control over financial reporting.
- **ISA 500, 530, 620, 320, ISQM 1, ISQM 2.** The supporting ISA/ISQM stack (evidence, sampling, use of experts, materiality, firm quality management, engagement quality reviews).

### AICPA — US

- **AT-C 105 — Concepts Common to All Attestation Engagements.** The base of the AT-C codification.
- **AT-C 205 — Assertion-Based Examination Engagements.** Positive-opinion examination.
- **AT-C 210 — Review Engagements; AT-C 215 — Agreed-Upon Procedures Engagements.** Limited-assurance and procedural engagements.
- **SOC 1 / SOC 2 / SOC 3 — Attestation reports on controls at service organisations.** SOC 1 covers controls relevant to user organisations' financial reporting; SOC 2 covers the Trust Services Criteria (security, availability, processing integrity, confidentiality, privacy); SOC 3 is a general-use summary of SOC 2.
- **SSAE 18.** The umbrella SSAE that codifies the AT-C sections.
- **AICPA Code of Professional Conduct.** Independence and ethics.

### SOC for AI — the shape emerging

SOC for AI is executed under AT-C 105 + AT-C 205 (US) or ISAE 3000 (Revised) (international), on **AI-specific subject matter and criteria**. The AICPA has signalled a dedicated criteria set that extends the Trust Services Criteria for AI-specific control categories. Pending full publication, practitioners execute against **the client's own control framework** — one crosswalked to NIST AI RMF 1.0 (with the GenAI Profile, NIST AI 600-1), ISO 42001, or a firm-specific framework — provided that framework meets AT-C 105 / ISAE 3000 **criteria suitability** (relevance, completeness, reliability, neutrality, understandability). <!-- needs-research: confirm the AICPA's SOC-for-AI criteria publication at reading time, including whether it is a formal Trust Services Criteria extension, a new description criteria set, or a related set; practitioner firms have been executing SOC-for-AI engagements against their own criteria crosswalks pending formal publication -->

## Scoping the engagement

The auditor's scoping memo fixes:

- **The responsible party and the engaging party.** Usually the same for SOC-for-AI (the company engages its own attestation); may differ in some structures.
- **The intended users.** Named in the engagement letter — specific customers, regulators, general-use (SOC 3-equivalent).
- **The period of coverage.** Type I = point-in-time (design only); Type II = period of time (design + operating effectiveness).
- **The subject matter.** For SOC-for-AI, the AI control environment covering specified AI systems or the AI program as a whole — scope must be defined with the same precision ISO 42001 scope is defined (which systems; which life-cycle stages; which business processes).
- **The criteria.** Publicly available criteria meeting suitability tests — the client's control framework with named external references (NIST AI RMF, ISO 42001, ISO/IEC 23894, NIST AI 600-1 for GenAI, GPAI Code of Practice, company-specific framework). Criteria must be described, formally adopted by the client, and available to intended users.
- **The level of assurance.** Reasonable (the SOC 2 default) vs. limited.

## The description, the criteria, and the two kinds of effectiveness

The SOC 2 shape — which SOC for AI inherits — distinguishes **four** test objects:

1. **Management's description** of the system / service / AI control environment. The auditor evaluates whether the description is **fairly presented** — complete, accurate, not misleading, consistent with the criteria.
2. **Design of controls.** The auditor evaluates whether the controls, if operating as described, would meet the criteria. Design effectiveness can be tested in a Type I (point-in-time) report.
3. **Operating effectiveness of controls.** Over the period, did the controls operate as designed. Operating effectiveness requires a Type II report (period of time; typically three to twelve months).
4. **The criteria themselves.** The auditor evaluates (and discloses) whether the criteria are **suitable** — relevant, complete, reliable, neutral, understandable.

The auditor's workpapers and report address each of these in named sections.

## AI-specific control categories to expect in the description

The client's SOC-for-AI control framework typically names control categories along these lines (variations across firms and clients):

### Governance and oversight

- Executive sponsor / board oversight; AI policy; roles and responsibilities; training and awareness; ethics principles operational.

### Risk management

- AI risk assessment per ISO 23894 or NIST AI RMF; AI system impact assessment per ISO 42005 or equivalent; risk register; residual-risk acceptance.

### Data governance and quality

- Data inventory; provenance; consent and lawful basis; retention; quality and representativeness testing; bias examination; feature engineering controls.

### Model lifecycle

- Model development procedures; training and validation separation; model registry; model signing and versioning; release gate; deprecation and retirement.

### Model evaluation and testing

- Pre-deployment evaluation; red-team; adversarial testing; robustness testing; cybersecurity testing (AI-specific threats).

### Deployment and inference

- Deployment controls; guardrails; input/output filtering; access controls; rate limiting; monitoring.

### Monitoring and incident management

- Performance monitoring; drift detection; alerting; incident classification and response; CAPA; near-miss recording.

### Privacy and data protection

- Privacy-by-design; DPIA; data-subject-rights fulfilment; cross-border transfer; special-category data handling.

### Security and resilience

- Information security (ISO 27001 / SOC 2 Security TSC); AI-specific threat defence; model-weight protection; supply-chain security; business continuity and disaster recovery for AI services.

### Third-party AI and supply chain

- Vendor due diligence; contract terms; ongoing monitoring; SBOM / ML-BOM.

### Transparency and user-facing communications

- AI disclosure; user-facing documentation; model cards; system cards; capability and limitation disclosure.

### Human oversight

- Human-in-the-loop controls; override design; automation-bias mitigation; competence of oversight personnel.

### Change management

- Change-control process; impact assessment on changes; deployment authorisation; retraining governance.

Each category contains specific controls (typically 3–15 per category), each with a stated objective, a description, and a frequency.

## Test design across design and operating effectiveness

### Design effectiveness

For each control the auditor evaluates whether the control, as described, could meet the control objective and (through objectives) the criteria.

Procedures: inquiry of the control owner; inspection of the policy, procedure, and standard; observation of the control's structural fit (does the described workflow route to the described review?); walk-through of a single example from start to end.

If design is adequate, Type I can be issued. Type II continues with operating effectiveness.

### Operating effectiveness

For each control the auditor tests a **sample** of operation over the period — the number and nature of operations depending on the frequency and risk of the control. Test procedures:

- **Inquiry.** Weak evidence; corroborated by other procedures.
- **Observation.** Moderate; limited to point-in-time.
- **Inspection.** Document the artefact the control produced; stronger than inquiry.
- **Reperformance.** Re-execute the control on an evidence item; strongest for controls whose operation is deterministic.

For AI-specific controls, procedures include:

- **Model-evaluation reperformance (ISA 500 deep dive).** Re-run a specific evaluation protocol on a current model and compare to the client's reported result. Interface with `mod-104` evidence-reliability work.
- **Drift-monitoring reperformance.** Compute the drift metric the client's monitoring uses, over the auditor's independent window, on the auditor's access to the data.
- **Guardrail reperformance.** Submit crafted inputs through the client's inference endpoint and verify the guardrail triggers.
- **Incident-walk reperformance.** Pick a reported incident; walk from detection to escalation to closure to CAPA; verify every claimed artefact.

### Sample size and sampling

ISA 530 / AT-C 105 sampling rules apply. Typical SOC-for-AI sample sizes track SOC 2 conventions:

- Daily / continuous controls — larger samples (25+).
- Weekly / monthly — scaled by frequency.
- Quarterly / annual — often tested in full for the period.
- Judgmentally selected or risk-weighted samples for controls over material populations.

Where the auditor relies on the **client's own evidence** (a SOC 2 from an upstream vendor; a model-evaluation report produced by the client's internal red-team), the auditor's reliance is subject to ISA 500 reliability assessment and (where the evidence was produced by a specialist) ISA 620 / AT-C 105 reliance on experts (`mod-101` chapter 8).

## Written representations

ISAE 3000 and AT-C 105 require **written representations** from the responsible party at engagement completion. For SOC-for-AI typical representations:

- Management has provided all information and access the auditor requested.
- Management has disclosed all deficiencies in design and operating effectiveness known to management.
- Management has disclosed all incidents and complaints during the period.
- Management has not become aware, between the period end and the report date, of events affecting the auditor's conclusion.
- Management has disclosed the use of service organisations and third-party AI vendors, with the controls the client operates to address vendor controls.

Representations are evidence; their absence is a scope limitation; where management cannot or will not provide them, the auditor modifies the opinion.

## The report shape — AT-C 205 / ISAE 3000

The SOC 2 / SOC-for-AI report has a canonical structure:

1. **Independent Service Auditor's Report** (or Independent Accountant's Examination Report).
   - Addressee (intended users).
   - Scope and description of the system / AI control environment.
   - Service organisation's responsibilities and criteria.
   - Service auditor's responsibilities.
   - Inherent limitations.
   - **Opinion** — the positive-assurance conclusion on management's description, suitability of control design, and (for Type II) operating effectiveness.
   - Restricted-use paragraph (SOC 2) or general-use allowance (SOC 3).
   - Signature, firm, date.
2. **Management's Assertion.**
3. **System Description** prepared by management.
4. **Description of Tests of Controls and Results** (Type II). For each control: the control description, the auditor's procedure, the result (operated effectively / exceptions noted). Exceptions are reported with specific descriptions and management responses.
5. **Other Information** (unaudited, if included) and glossaries.

The **opinion paragraph** uses prescribed wording:

For AT-C 205 reasonable assurance, Type II:

> *In our opinion, in all material respects, management's description fairly presents the AI control environment that was designed and implemented throughout the period [...], the controls stated in the description were suitably designed throughout the period to provide reasonable assurance that the service organisation's control objectives [or applicable criteria] would be met if the controls operated effectively, and the controls operated effectively throughout the period to meet the applicable criteria.* <!-- needs-research: verify exact wording prescribed by AT-C 205 for a SOC 2 Type II positive opinion at reading time; the precise phrasing is normative -->

Where exceptions exist that are material, the auditor issues a **modified opinion** (qualified, adverse, or disclaimer).

## Independence and ethics

The auditor is subject to the IESBA Code of Ethics (international) or AICPA Code of Professional Conduct (US), including the independence sections. The relevant threats:

- **Self-review.** The firm has consulted on the client's AI control framework and now attests to it. Prohibited; the firm separates teams or declines one engagement.
- **Self-interest.** The firm's revenue depends on the client. Standard SOC 2 posture: the engagement is one of many; the firm can deliver an adverse opinion if warranted.
- **Advocacy.** The firm is marketing AI services and has incentive to advocate for its client's AI maturity. Mitigated by firm-level quality management.
- **Familiarity.** Long-tenured engagement team. Rotation considered.
- **Intimidation.** Not typically material in SOC 2 but recorded.

The engagement letter captures the firm's independence representation under ISQM 1 and the engagement-specific threats under AT-C 105 / ISAE 3000.

## SOC 2 crosswalk — the common client posture

Many clients' SOC-for-AI engagements layer on top of an existing SOC 2. The auditor coordinates:

- **Subject matter.** SOC 2's Security TSC covers much of the security, confidentiality, and availability dimensions; SOC-for-AI focuses on the AI-specific dimensions on top.
- **Timing.** A combined SOC 2 + SOC for AI report issued together; or SOC-for-AI as a separate report with reference to the SOC 2.
- **Evidence reuse.** Controls that are in scope for both are tested once; reports reflect the shared evidence.
- **Trust Services Criteria extension.** As AICPA formalises SOC-for-AI criteria (typically as a TSC extension or related criteria set), the integration tightens.

## Integration with other audit shapes

- **ISO 42001 (`mod-105`).** Many clients run both ISO 42001 certification and SOC for AI. The ISO 42001 AIMS *is the quality-management system* for AI; SOC for AI is an attestation on controls that the AIMS operates. They reinforce rather than substitute.
- **EU AI Act (chapter 1).** SOC for AI evidence can feed the Article 17 QMS audit but does not substitute for the Article 43 conformity assessment; the Conformity Assessment is a product-level regulatory decision, SOC is an entity-level attestation.
- **IAAIS (chapter 3).** IAAIS is scheme-governed by ForHumanity; SOC for AI is attestation-framework-governed by IAASB/AICPA. They can run alongside for different audiences.
- **SR 11-7 (chapter 5).** SOC for AI does not substitute for a bank's internal model validation; validation is operational effective challenge, SOC is third-party attestation.
- **FDA GMLP (chapter 6).** SOC for AI does not substitute for medical device submission content; a SaMD manufacturer cannot produce a SOC report instead of a 510(k).
- **NAIC (chapter 7).** Some insurers report SOC-for-AI to their DOI as supporting evidence of their governance posture.

## Common failure modes

- **Criteria not suitable.** Client's framework not externally referenced; auditor cannot defend criteria suitability under AT-C 105 / ISAE 3000.
- **Description incomplete.** System description omits material components or systems; auditor must require description amendment before concluding fair presentation.
- **Scope mismatch.** Engagement letter scopes certain AI systems; description extends to others; or vice versa.
- **Operating-effectiveness samples thin.** Sample sizes too small for the control frequency; auditor's conclusions are not supportable.
- **Vendor controls not addressed.** SOC 2's vendor-controls sections exist; SOC-for-AI client relies on upstream vendor controls (foundation-model provider's practices) but does not address them in its description; auditor's opinion coverage is incomplete.
- **Red-team evidence self-produced without ISA 620 reliance.** Red-team report is written by the client's team; auditor accepts without reliability assessment; evidence quality low.
- **Exceptions suppressed.** Engagement team identifies an exception in control operation; management requests that the exception be omitted from the Description of Tests of Controls; auditor must include it (with management response if appropriate).
- **Opinion language non-standard.** Auditor varies the prescribed opinion wording; peer review or examination challenges the report.
- **Restricted-use paragraph missing.** SOC 2 reports are typically restricted; auditor's report is distributed as if general-use; firm quality-management issue.
- **Dual ISO 42001 / SOC posture confused.** Client's ISO certification body and SOC auditor exchange findings informally; auditor must maintain independence from certification-body audits.

## When the auditor uses SOC for AI

The engagement-shape chooser (chapter 9) returns to SOC for AI when:

- the client needs an **attestation-framework** engagement — one that invokes IAASB / AICPA standards and the practitioner's professional firm quality management;
- the intended audience includes **customers and procurement counterparties** familiar with the SOC-2 shape;
- the client already operates SOC 2 and wants to extend it to AI;
- the client needs an engagement that is **general-purpose** (feeds multiple audiences without being specific to one regulator) and can be delivered on a **recurring attestation cadence**.

## Summary

- SOC for AI is an attestation engagement under AT-C 105 + AT-C 205 (US) or ISAE 3000 (international), with the AICPA's SOC 2 shape extended to AI-specific control categories; the AICPA's ASEC continues to formalise SOC-for-AI criteria as a TSC extension or related publication.
- The auditor evaluates four objects: management's description (fair presentation), design of controls (adequacy if operating as described), operating effectiveness (over the Type II period), and criteria suitability (relevance, completeness, reliability, neutrality, understandability).
- Expected AI-specific control categories in the description: governance, risk management, data governance, model lifecycle, model evaluation, deployment, monitoring, privacy, security, third-party AI, transparency, human oversight, change management.
- Test design: inquiry, observation, inspection, reperformance; AI-specific reperformance includes model-evaluation, drift-monitoring, guardrail, and incident-walk procedures; samples scaled to control frequency and risk; ISA 500 reliability assessment and ISA 620 reliance on specialists apply.
- Report structure: independent auditor's report (opinion in prescribed wording), management's assertion, system description, description of tests of controls and results (Type II), other information; restricted-use paragraph for SOC 2 shape.
- Independence and ethics: self-review threat on frameworks the firm consulted on; standard SOC 2 posture on self-interest, advocacy, familiarity, intimidation; engagement-letter capture.
- SOC for AI integrates with ISO 42001 certification, EU AI Act conformity, IAAIS, SR 11-7, FDA GMLP, and NAIC; chapter 9 defends the combination against the client's audience and regulatory classification.
