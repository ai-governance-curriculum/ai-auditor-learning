# Auditing OMB Federal-Agency AI Inventory and Third-Party AI Acquisition

## Motivation

US federal agencies and their contractors are subject to an additional regulatory overlay the AI auditor must know how to test. The current Office of Management and Budget (OMB) policy framework for federal AI governance consists of a set of memoranda defining agency-wide AI use-case inventory, AI-use risk management, AI acquisition, and federal AI programme governance. The three memoranda most relevant to this chapter's scope are:

- **OMB M-24-18** — "Advancing the Responsible Acquisition of Artificial Intelligence in Government" (2024). Governs federal agencies' acquisition of AI, including vendor due diligence, contracting terms, risk-management-at-acquisition, and inventory alignment.
- **OMB M-25-21** — the memorandum addressing federal agency AI governance, risk management, and innovation (2025 series). Covers categories of AI-use and the controls attached, with specific attention to rights-impacting and safety-impacting AI.
- **OMB M-25-22** — the memorandum on federal AI acquisition (2025 series) and its interaction with the Federal Acquisition Regulation (FAR).

<!-- needs-research: confirm the exact titles, publication dates, scope, and inter-citation relationships of M-24-18, M-25-21, and M-25-22 at reading time; the federal AI-policy landscape has been under active revision and prior memoranda (M-24-10, "Advancing Governance, Innovation, and Risk Management for Agency Use of AI") may have been superseded, consolidated, or refined; also check whether additional OMB memoranda or OSTP directives in force at the engagement period layer over these three -->

This chapter is the auditor's shape for testing a federal agency's (or a federal contractor's) compliance with these memoranda. The auditor is not creating the inventory or the acquisition framework; the agency CAIO (Chief AI Officer) and the agency's acquisition / risk / legal functions do. The auditor tests whether the required inventories exist, whether they are complete, whether the acquisition process reflects the memoranda, and whether the risk-management cascade applies where it should.

This chapter is one of two US-federal overlay chapters across the ai-auditor track; the other is `mod-110` (conformity-assessment and sector-audit shapes), which treats agency-specific accreditation and sector-audit structures.

## Who is bound

The memoranda bind US federal agencies directly. Three flow-downs matter for the auditor:

- **Federal contractors supplying AI products or services.** FAR-compliant contracts flow M-24-18 / M-25-22 acquisition terms to contractors; the contractor is bound to the extent of the contract.
- **State and local recipients of federal funds** where federal funds are used to acquire AI; agency-specific subrecipient rules may extend applicability.
- **Grantees** in some AI-adjacent federal grant programmes.

The auditor's first fieldwork step is a **binding-determination** memo: for the organisation under audit, which OMB memoranda apply directly, which apply via contractual flow-down, and which apply because of grant terms. The determination feeds the scoping decision and the engagement letter (`mod-103` chapter 2 shape).

## Agency AI use-case inventory

Each federal agency maintains an **AI use-case inventory** — a structured enumeration of AI used by the agency, with per-use-case metadata. The inventory is public in significant part and is the central transparency artefact for federal AI use.

### Content expectations

The inventory is expected to record, per use case:

- Use-case name and description.
- Agency, sub-agency, office responsible.
- Deployment status (planned, piloted, in use, retired).
- AI-system category (classification; system functions, modalities).
- Mission or business function supported.
- Data types used.
- Whether the use case is **rights-impacting AI** or **safety-impacting AI** per the memoranda's definitions.
- Where applicable, the specific minimum-practices compliance status (pre-deployment testing, impact assessment, ongoing monitoring, etc.).
- Public contact or responsible official.
- Records-retention disposition.
- Retirement date or next review date.

<!-- needs-research: confirm the current field set the OMB-prescribed inventory requires at reading time; the field set evolves and the auditor pins the version in effect at the engagement period -->

### The inventory reperformance

The auditor's test parallels chapter 2's three-sweep pattern, adapted to federal context:

- **Published-inventory comparison.** The agency's publicly-posted inventory is one artefact; the internal inventory used for management is another. The two must reconcile with declared redactions (national-security carve-outs, procurement-sensitive carve-outs) documented and authorised.
- **Procurement sweep.** Pull agency procurement records for the look-back period; filter for AI-related procurements by keyword and vendor; reconcile against the inventory. Procurements of AI not represented in the inventory are findings against the inventory completeness.
- **Use-record sweep.** Pull records of internal AI deployment (System Authorisation to Operate records, FISMA system inventories, data-processing records). Deployed AI not in the inventory is a finding.
- **Component-system sweep.** AI embedded in non-AI systems — a workflow tool that added an AI-recommendation feature — is a frequent omission. The auditor samples major non-AI systems and asks about AI components.
- **GPAI / vendor-API sweep.** Agency use of external GPAI APIs (ChatGPT Enterprise, Claude Enterprise, Gemini for Workspace) under general-services or sole-source procurement may escape the inventory. The auditor sweeps identity / SSO logs for GPAI providers.

Shadow AI in the federal context attracts not only an internal finding but a reporting failure under the memoranda — a particularly sharp finding category.

### Classification: rights-impacting and safety-impacting

M-24-10 / M-25-21 (as applicable) define categories of AI use that attract heightened obligations:

- **Rights-impacting AI** — AI whose use affects determinations of rights, benefits, or significant outcomes for individuals (eligibility determinations, employment decisions, law-enforcement decisions, housing decisions, etc.).
- **Safety-impacting AI** — AI whose use could affect the safety of persons, critical infrastructure, or mission-essential activities.

<!-- needs-research: confirm the definitions in force at reading time and whether the current memorandum has revised the categorisation shape -->

The auditor's test:

- **Classification methodology.** The agency has a documented methodology for classifying use cases into these categories.
- **Application.** The classification applied to each use case is reperformed on a sample; a sampled use case classified "neither" that fits one of the categories is a classification finding.
- **Minimum-practices cascade.** Each classification triggers a minimum-practices set (pre-deployment testing, impact assessment, ongoing monitoring, individual notification, access to appeals / consistent human review). The auditor samples these practices per classified use case.

A use case classified rights- or safety-impacting whose minimum-practices evidence is absent is a specific memorandum-level finding; a classification-off-by-one-category (e.g., safety-impacting marked rights-impacting without the right practices) is a sub-finding.

## Minimum-practices audit for rights- and safety-impacting AI

For each sampled rights- or safety-impacting AI use case, the auditor tests the minimum-practices evidence. The practices typically include:

- **AI impact assessment.** A documented pre-deployment assessment covering intended purposes, expected benefits, potential risks, affected populations, mitigations. The auditor reads the assessment and tests its completeness.
- **Pre-deployment testing.** Documented testing against the use-case's performance and fairness expectations. Where the use case is rights-impacting, fairness testing across protected classes is a specific test the auditor expects.
- **Ongoing monitoring.** Operational monitoring consistent with the shape `mod-108` chapter 1 tests, with federal-specific retention (`mod-108` chapter 1 covers Clause 9.1 + Article 72; federal adds the Federal Records Act, NARA scheduling, FISMA continuous monitoring — the auditor crosswalks all applicable).
- **Human oversight.** Named oversight role; procedures for review before determinations; appeals or review process for affected individuals. The auditor confirms the role exists and operates.
- **Notification.** Where applicable, affected individuals are notified of AI use in a decision affecting them; the notification mechanism is documented and operational.
- **Consistent human review.** Opportunity for a human review of an AI determination; procedure is documented; evidence of exercised reviews is retained.
- **Mitigation of identified risks.** Each risk identified in the impact assessment has a documented mitigation.

Where the memorandum provides for waivers (e.g., for national-security reasons or where the practice would be infeasible), the waiver is documented, authorised at the required level (often agency head or CAIO), and reviewed per the cadence the memorandum sets.

## Acquisition — M-24-18 and M-25-22

The acquisition memoranda govern how the agency contracts for AI. Key provisions the auditor tests:

### Pre-acquisition

- **Market research.** Documented market research on AI alternatives, including commercial options, government-off-the-shelf, and build options.
- **Mission alignment and risk assessment.** Pre-acquisition risk assessment covering performance, fairness, safety, security, privacy, procurement-integrity.
- **Stakeholder engagement.** For rights- or safety-impacting acquisitions, documented engagement with affected stakeholders (public, agency programme offices, oversight bodies).
- **CAIO involvement.** The agency's CAIO is engaged in acquisition decisions over the materiality threshold; the auditor confirms the engagement artefacts.

### Contract terms

- **Required clauses.** FAR clauses as modified or supplemented for AI acquisitions; auditor tests presence and version.
- **Model-provenance clauses.** Training-data sources, model identity and version, change notification, retraining obligations.
- **Performance, fairness, safety, cybersecurity clauses.** Testing obligations, acceptance criteria, remediation duties.
- **Data-use clauses.** Government-data-use for training / improvement, retention, destruction.
- **Rights in data and rights in deliverables.** Who owns prompts / completions / fine-tunes / derivative artefacts; how do agency-specific data-rights categories apply.
- **Delivery of documentation.** Model card, system card, Annex XII-equivalent documentation, SOC 2 / ISO / 42001 artefacts, pentest summaries, red-team summaries.
- **Section 508 / accessibility.** The product is accessible to persons with disabilities per Section 508; AI-specific accessibility concerns are reflected.
- **Audit, inspection, and reporting rights.** Agency right to audit vendor; vendor incident-notification SLA.
- **Flow-down to subcontractors.** Subcontractors bound to equivalent terms.
- **Termination and data-return.** Exit provisions consistent with chapter 2's shape.

### Post-award

- **Acceptance testing.** Vendor-delivered product tested against acceptance criteria; the testing artefact is retained.
- **Operational monitoring.** Agency's ongoing monitoring of vendor performance against the contract.
- **Modifications.** Contract modifications tracked; AI-material modifications (new model version, new data flow) trigger a reassessment.
- **Vendor-reported incidents.** Vendor-notified incidents routed through the agency's incident process.

The auditor's acquisition workpaper per sampled acquisition pairs the SR 23-4 chapter-2 shape with the M-24-18 / M-25-22 clause-by-clause test.

## Section 508 and accessibility

Federal AI acquisitions must comply with Section 508 of the Rehabilitation Act (as amended). The AI-specific concerns:

- **Interface accessibility.** User-facing AI interfaces are accessible to users with disabilities.
- **Alternative access.** Where an AI is the primary interface to a service, alternative paths are available for users who cannot use the AI interface.
- **Model behaviour and accessibility.** Models that produce output (text, images, audio) support the accessibility features the output modality requires.
- **Non-discrimination in outcomes.** The AI does not systematically disadvantage users with disabilities in its determinations.

The auditor tests Section 508 compliance on sampled acquisitions, often referring to the agency's 508 Coordinator or accessibility team for specialist review (ISA 620 analogue in a federal context).

## Reporting cadence

The memoranda prescribe reporting:

- **Annual AI use-case inventory submission.** To OMB / public posting as applicable, with reconciliation to the internal inventory.
- **Significant updates.** Material changes (new category assignment, new rights-impacting use) trigger interim updates.
- **Incident reporting.** Serious incidents routed per the memoranda's reporting requirements, in addition to the agency's existing cybersecurity / privacy incident reporting.
- **Waiver reporting.** Waivers logged and reported per the memoranda's cadence.
- **CAIO reporting.** Agency CAIO reports periodically to agency leadership and OMB on the state of AI governance.

<!-- needs-research: confirm the current reporting cadences and the OMB-specified submission templates at reading time -->

The auditor samples the reporting outputs for the period, checks they were produced on cadence, and reperforms selected content by comparison to the internal inventory and risk-register.

## Federal AI vendor flow-down

Where the organisation is a contractor supplying AI to a federal agency, the auditor tests whether the contract's AI-specific clauses are being met. The contractor-side evidence:

- **Clause-by-clause compliance.** Each AI-specific clause in the contract maps to internal controls; the controls operate.
- **Documentation delivery.** The contract-required documentation (model card, system card, evaluation results, incident reports) is delivered on schedule.
- **Performance against SLA.** Performance and accuracy SLAs met; deviations documented and remediated.
- **Audit response.** Agency audit requests responded to in the timeframe; evidence retained.
- **Flow-down to the contractor's own subcontractors and vendors.** The contractor's upstream AI dependencies (foundation-model providers, cloud providers) are themselves managed consistent with the flow-down expectation. The auditor tests the contractor's upstream management; chapter 2 (SR 23-4) is the generic shape and chapter 5 (GPAI deployer) is the GPAI-specific shape.

Contractor-side findings tie back to the agency's prime contract; serious findings may require disclosure to the contracting officer.

## Interaction with other criteria

The federal AI governance shape layers over, rather than replacing, other criteria the organisation may be subject to:

- **FedRAMP** for cloud services the agency uses.
- **FISMA / NIST SP 800-53** for the information-security control baseline.
- **NIST AI RMF** as the risk-management reference framework (integrated by OMB memoranda).
- **Privacy Act of 1974** for personal-data handling.
- **Section 508** for accessibility.
- **Specific-agency authorities** — DoD, IC-element, HHS, Treasury, etc. have additional AI directives.

The auditor's workpaper per federal engagement maintains a stacking table showing which criteria apply, what evidence supports each, and where findings implicate more than one framework.

## Interaction with chapters 1–6 of this module

- **Chapter 1 (provenance).** The federal AI inventory is the use-case register; each use case is backed by model artefacts whose provenance chapter 1 audits. Where an agency fine-tunes a model, chapter 1's trace-back applies.
- **Chapter 2 (SR 23-4).** SR 23-4 is a US-banking rule, but its five-phase shape is the same backbone the federal acquisition memoranda follow. The auditor runs the chapter-2 workpaper and overlays the M-24-18 / M-25-22-specific clause set.
- **Chapter 3 (assurance).** Agencies rely on SOC 2 / ISO / FedRAMP artefacts the same way other organisations do; chapter 3's scope / carve-out / CUEC testing applies, plus the specific FedRAMP controls.
- **Chapter 4 (malicious artefacts).** Federal agencies' model-ingestion pipelines are tested per chapter 4; additional federal cryptographic-module requirements (FIPS 140) may apply to the signing infrastructure.
- **Chapter 5 (GPAI).** Federal use of GPAI APIs pulls both the chapter-5 Chapter V surface and the M-24-18 / M-25-22 acquisition surface.
- **Chapter 6 (gates).** Federal registries and deployment admission are tested per chapter 6; FISMA continuous-monitoring artefacts overlap.

## Common failure modes

- **Inventory incomplete.** Procured AI, embedded-in-non-AI-system AI, or GPAI-API use not reflected.
- **Classification off.** Rights- or safety-impacting use cases classified as neither; the memorandum's minimum practices never triggered.
- **Minimum practices performed but not evidenced.** Impact assessment conducted in a meeting; no document retained.
- **Waivers used, not logged.** Waivers taken informally without the memorandum-specified authorisation level.
- **Acquisition clauses missing.** FAR-flow-down AI clauses absent from older contracts not yet modified.
- **Documentation delivery not enforced.** Vendor-delivery obligations not tracked; vendor fails to deliver; contract-ending sanction never invoked.
- **Section 508 overlooked.** Accessibility assessment not done or not consulted for AI product acquisitions.
- **Reporting cadence missed.** Annual inventory submission late or incomplete.
- **Shadow GPAI API.** Staff using ChatGPT / Claude / Gemini for government work without agency authorisation; a common finding given rapid consumer-API growth.
- **Contractor flow-down absent.** Contractor's own upstream AI vendors not managed consistent with the prime-contract flow-down.

## Summary

- OMB M-24-18, M-25-21, and M-25-22 (and their predecessor and companion memoranda) form the federal-agency and federal-contractor AI governance overlay — inventory, acquisition, and risk management.
- Agencies maintain AI use-case inventories classified by rights-impacting and safety-impacting categories; the auditor tests inventory completeness via multiple sweeps and classification correctness via reperformance.
- Rights- and safety-impacting AI triggers a minimum-practices set — impact assessment, pre-deployment testing, ongoing monitoring, human oversight, notification, consistent human review, risk mitigation — each of which is tested against evidence.
- Federal AI acquisition tracks the SR 23-4 phases with M-24-18 / M-25-22 clause-specific requirements: market research, mission alignment, contract terms (training-data use, model-provenance, performance / fairness / safety / cybersecurity, Section 508, audit rights, flow-down, termination), acceptance testing, operational monitoring, and modification control.
- Reporting cadence (annual inventory, significant-update interim, incident, waiver, CAIO reporting) is audit-tested by sampling the output and reperforming selected content.
- Contractor-side obligations are tested per the prime contract's AI clauses, with upstream flow-down reperformed per chapters 2 and 5.
- The federal overlay stacks with FedRAMP, FISMA/800-53, NIST AI RMF, Privacy Act, Section 508, and agency-specific directives; the auditor maintains the stacking table in the workpaper.
- Cross-chapter interfaces: chapter 1 (provenance for fine-tuned use cases), chapter 2 (SR 23-4 backbone), chapter 3 (assurance including FedRAMP), chapter 4 (malicious artefacts + FIPS 140), chapter 5 (GPAI), chapter 6 (ingestion gates + FISMA continuous monitoring).
