# Integrated Management-System Audits — ISO/IEC 42001 with 27001, 27701, 9001, 13485, 14971

## Motivation

Mature organisations rarely hold just one management-system certification. A regulated medical-device maker typically holds ISO 13485 (QMS), applies ISO 14971 (medical-device risk management) through 13485, maintains ISO/IEC 27001 for information-security obligations under IEC 62304 and 62366, extends to ISO/IEC 27701 for GDPR, and is now adding ISO/IEC 42001 for the AI features in the device. A SaaS vendor may hold ISO 9001 and ISO/IEC 27001 and now adds ISO/IEC 42001. Where the same certification body audits multiple standards for the same client, the audit can be *integrated* under ISO/IEC 17021-1 clause 9.1.5.1 — fewer audit days than running each audit independently, shared evidence for shared controls, a single opening/closing meeting and audit team span.

The integration opportunity is attractive but it is also an audit-methodology stress test. Shared controls have genuinely common ground (document control, access control, incident management) but also genuinely distinct requirements (ISO 13485's design controls are not ISO/IEC 42001's AI life-cycle controls, even where they look similar). ISO/IEC 42001 Annex D is explicit about integration, and the auditor's job is to navigate the integration defensibly — testing each standard's requirements, leveraging shared evidence where appropriate, keeping distinct requirements distinct.

This chapter positions the AIMS audit against adjacent MS audits, shows where integration works, and shows where it does not. It is the delta between the AI-only `ai-evaluation-engineer` (L35, release-assurance methodology inside the second line) and the AI-only `senior-ai-governance-architect` (L50, who designs the AIMS) on the one hand, and the integrated-audit reality the external auditor meets in regulated organisations on the other.

## The adjacent management systems

### ISO/IEC 27001 — Information Security Management System (ISMS)

ISO/IEC 27001:2022 is the dominant information-security MS standard, with Annex A controls spanning organisational, people, physical, and technological controls (93 controls in the 2022 revision). <!-- needs-research: verify the 2022 Annex A grouping and control count against the as-published standard -->
Virtually every AI-enabled organisation of any size holds or pursues ISO/IEC 27001.

### ISO/IEC 27701 — Privacy Information Management System (PIMS)

ISO/IEC 27701 extends ISO/IEC 27001 to privacy — adding requirements on PII controllers and processors and extending Annex A with privacy-specific controls. Widely used as a GDPR / privacy-compliance evidence layer.

### ISO 9001 — Quality Management System (QMS)

ISO 9001:2015 is the horizontal QMS standard, following Annex SL like the others. Used across sectors as a baseline quality posture; also a prerequisite for several sector-specific systems.

### ISO 13485 — QMS for Medical Devices

ISO 13485:2016 is a QMS standard specific to medical devices, with substantial additional requirements beyond ISO 9001 (regulatory requirements, risk-management integration, traceability, controlled documentation of devices). Required or de-facto required for medical-device makers globally.

### ISO 14971 — Risk Management for Medical Devices

ISO 14971:2019 is the risk-management standard for medical devices — not a management-system standard but a process standard — referenced by ISO 13485 and by regulatory regimes (FDA, MDR, IVDR, PMDA, NMPA). For AI-enabled medical devices, 14971 is the primary risk-management reference even where ISO/IEC 42001's clause 6 is also applied; FDA/Health Canada/MHRA GMLP guiding principles cross-reference 14971 and 13485. <!-- needs-research: confirm the current status of ISO/TR 24971 (guidance on 14971), any 14971:2019 amendments, and AAMI consensus reports on AI/ML in medical devices (e.g., AAMI CR34971) -->

## Where controls overlap — and where they diverge

Integration opportunities cluster around four control families:

### Overlap — document control

ISO/IEC 42001 clause 7.5, ISO/IEC 27001 clause 7.5, ISO 9001 clause 7.5, ISO 13485 clause 4.2. All require documented information to be controlled: version, approval, availability, protection, retention.

**Integration test:** can one document-control procedure satisfy all? Usually yes. Audit by: verify the procedure covers all applicable MS; verify all MS-relevant documents are under the procedure; reconcile a sample from each MS's document set against the procedure.

**Divergence:** retention periods differ by regime. ISO 13485 requires retention for the lifetime of the device plus regulatory-defined period; ISO/IEC 42001 record-retention is organisation-defined; ISO/IEC 27701 inherits GDPR constraints. The integrated procedure must honour the strictest applicable period.

### Overlap — change management

ISO/IEC 42001 clause 6.3 and 8.1, ISO/IEC 27001 Annex A change management, ISO 9001 clause 6.3, ISO 13485 clause 7.3 design changes.

**Integration test:** can one change-management procedure satisfy all? Partially. Change management in general (for policies, procedures, assets) can be common. But *AI-specific* changes (model-version updates, prompt-template changes, retriever-config changes, guardrail changes) need AI-specific gates that the generic procedure usually does not have.

**Divergence:** ISO 13485 design controls (clause 7.3) have specific activities (design and development planning, design inputs, design outputs, design review, design verification, design validation, design transfer, design changes, design file) that AI life-cycle control must map into *for the medical-device case*. The organisation may need two change-management flavours: one generic, one 13485-specific-with-AIMS-overlay.

### Overlap — incident management

ISO/IEC 42001 clause 10 + Annex A incident controls, ISO/IEC 27001 Annex A incident controls, ISO 13485 clause 8.2 feedback / customer complaints, ISO 9001 clause 10.2 corrective action.

**Integration test:** can one incident / nonconformity register serve all? Usually yes, with tagging. The register captures incidents regardless of which MS they map to; tags identify the applicable regimes; the handling flow honours the strictest.

**Divergence:** mandatory reporting obligations. ISO 13485 carries FDA MDR / MedDev / MDR / IVDR reporting obligations. ISO/IEC 42001 carries EU AI Act Article 73 serious-incident reporting for high-risk systems. ISO/IEC 27701 carries GDPR Article 33 breach notification. The register is shared; the reporting flows are distinct and the auditor tests each.

### Overlap — risk management

ISO/IEC 42001 clause 6.1.2 / 6.1.3 (with ISO/IEC 23894), ISO/IEC 27001 clause 6.1.2 / 6.1.3 (with ISO/IEC 27005 guidance), ISO 9001 clause 6.1 (risk-based thinking), ISO 13485 with ISO 14971 (medical-device risk management).

**Integration test:** can one risk-management framework serve all? Only partially. The procedural shape is similar (identify, analyse, evaluate, treat, monitor, review) but the risk-source taxonomies and criteria differ substantively.

- Information-security risk is to information assets.
- AI risk (23894) is to AI-system behaviour and its downstream consequences.
- Medical-device risk (14971) is to patient safety (acceptable risk = benefits outweigh residual risk; the 14971 risk-management file is a specific regulatory artifact).

**Divergence:** 14971 has its own concept of risk-acceptance (hazards, hazardous situations, harms, severity, probability of occurrence of harm, risk-control measures, risk-benefit analysis) that is not reducible to the AIMS 6.1.2 risk-assessment process. For AI-enabled medical devices, the 14971 risk-management file drives; the AIMS 6.1.2 outputs feed the 14971 file where they identify AI-specific hazards; the AIMS impact assessment (6.1.4) is distinct from the 14971 risk-management file. <!-- needs-research: confirm the integration pattern recommended by FDA GMLP, MDCG guidance on AI/ML medical devices, and AAMI consensus reports; the integration pattern has been actively evolving in 2024–2026 -->

## The integrated audit under 17021-1

### Audit planning

ISO/IEC 17021-1 clause 9.1.5.1 permits combined and integrated audits where the CB has competence in each applicable standard and the client's MS supports integration. The audit plan reflects:

- One audit team (with competence spanning each standard; AIMS competence per ISO/IEC 42006 and sector competence per the applicable sector-specific IAF documents).
- One opening / closing meeting with scope covering all standards.
- A single sampling plan where populations overlap.
- A single finding register with each finding mapped to its applicable standard(s).
- Audit-day calculation that may reduce total days under the CB's integration policy (not simply the sum of each standard's days; typical integration discount is in a defined range).

### The AIMS-specific audit-day consideration

ISO/IEC 42006 Annex A audit-day table is the AIMS baseline. For integrated audits, the CB applies its documented integration-discount policy, which must comply with ISO/IEC 17021-1 clause 9.1.5.1 and relevant IAF mandatory documents. <!-- needs-research: confirm the applicable IAF MD at reading time for integrated-audit audit-day calculation -->

### The audit report

An integrated-audit report can take two shapes:

1. **Single integrated report.** One report naming all standards, with findings mapped to each. Simpler for the client; requires care in writing to keep standard-specific findings traceable.
2. **Linked separate reports.** One report per standard, cross-referencing shared findings. Simpler for the CB's accreditation submissions; adds report-management overhead.

The CB's documented practice governs. The auditor confirms the choice at engagement planning.

## ISO 13485 + ISO/IEC 42001 — the medical-device specific case

Medical-device makers with AI-enabled devices face the densest integration. The pattern:

- **ISO 13485 governs the QMS.** The device life cycle (design controls under 7.3, production and service provision under 7.5, control of monitoring and measuring equipment under 7.6, measurement, analysis, and improvement under clause 8) is the primary life-cycle backbone.
- **ISO 14971 governs device risk management.** The risk-management file is the regulatory artifact.
- **ISO/IEC 42001 governs the AI-specific management system.** The AIMS scope covers AI-specific requirements the device-wide QMS does not fully address — AI data governance, AI model monitoring, AI impact assessment on affected persons beyond patient safety alone (e.g., operators, downstream clinicians, affected communities for population-health tools).
- **FDA GMLP guiding principles** reference 13485 and 14971; the AIMS is complementary rather than substitute. <!-- needs-research: confirm the current state of FDA's AI/ML device guidance, PCCP guidance, and any formal recognition of ISO/IEC 42001 as a consensus standard -->

The auditor on an integrated 13485 + 14971 + 42001 audit must:

- Test design controls (7.3) in 13485 shape with AI-system additions (what verification and validation activities are AI-specific).
- Test the 14971 risk-management file for completeness and traceability against the 13485 design file.
- Test the AIMS's 6.1.2 risk assessment for AI-risk-source coverage *beyond* patient safety — including impacts on operators, impacted populations, and societal effects where the device is deployed at scale.
- Confirm the AIMS's 6.1.3 SoA includes Annex A controls that are *not* duplicates of 13485 design controls (they are additional, not alternative).
- Test the AIMS clause 10 nonconformity process alongside the 13485 CAPA process and the regulatory reporting flows.

## ISO/IEC 27001 + 27701 + 42001 — the data-heavy SaaS case

The more common integration: ISO/IEC 27001 (ISMS) + ISO/IEC 27701 (PIMS) + ISO/IEC 42001 (AIMS), typically with one CB auditing all three annually.

The pattern:

- **27001 governs information security.** The ISMS SoA covers 27001 Annex A controls.
- **27701 extends 27001.** The PIMS adds privacy-specific controls and PII controller/processor obligations.
- **42001 governs AI.** The AIMS adds AI-specific controls on data, life-cycle, impact, and use.

Shared controls where integration most clearly reduces audit effort:

- Document control.
- Access control (information-security basis).
- Change management (information-security basis).
- Incident management (shared register with mandatory-reporting divergence).
- Supplier management (27001 and 42001 both have supplier controls; privacy-specific supplier controls in 27701).

Distinct areas where integration does not substitute:

- AI data governance (42001 Annex A data-management controls include AI-specific concerns — representativeness, bias, label quality — not in 27001 or 27701).
- AI system impact assessment (42001 6.1.4) — not addressed in 27001 or 27701, even where DPIAs are performed under 27701.
- AI life-cycle controls (42001 Annex A) — not addressed as such in 27001 or 27701.

## Audit methodology notes for the integrated engagement

### Sample sharing with care

A sampled AI system may be in scope for all three standards. The auditor can share evidence across the audit but must still test each standard's specific requirements. A model-registry record is 42001 evidence (model versioning), 27001 evidence (configuration management), and 27701 evidence (processing records) — but confirmation that the record exists is not confirmation that each standard's requirements for what it contains are met.

### Finding mapping

Every finding in an integrated audit is tagged with every applicable standard. A finding that the model-registry record lacks a model-version-to-processing-purpose mapping is 42001-relevant (AI data governance), 27701-relevant (processing records), and 27001-relevant (asset management).

### Grading per standard

A finding may grade differently against different standards. A missing model-version tag is a minor under 42001 Annex A data-management controls but might be a major under 27701 because processing records under GDPR require mapping to purposes. The finding is graded per standard.

### Independence and competence

The audit team must have demonstrable competence in each standard (ISO/IEC 42006 for AIMS; equivalent sector-specific documents for 13485 / 27001 / 27701 / 9001). The CB's competence-management system is tested at accreditation inspection; a weak competence case on a single standard undermines the integrated audit.

## How this positions the AI Auditor role

The AI Auditor at this course's L45 is expected to:

- Lead an AIMS-only audit solo.
- Be a competent AIMS team member on an integrated audit led by a 27001 / 13485 / 9001 lead auditor.
- Over time, hold sufficient 27001 competence to lead an AIMS + ISMS integrated audit as a lead.
- Rely on medical-device or sector-specific technical experts for 13485 / 14971 and other sector standards where the auditor's own competence does not cover.

The role delta from adjacent paths:

- **`ai-evaluation-engineer` (L35)** operates release-assurance methodology inside the second line — their output is evidence the AIMS auditor tests. The AI Auditor does not do that engineering work; the AI Auditor audits the AIMS that governs it.
- **`senior-ai-governance-architect` (L50)** designs the AIMS. The AI Auditor audits it from an independence posture (see `mod-101`): the architect and the auditor cannot be the same person on the same AIMS.
- **Sector lead auditors** (ISO 13485, 27001) hold the integrated audit together; the AI Auditor brings AIMS-specific depth.

## Common failure modes

- **Treating 42001 as a subset of 27001.** AI-specific controls on data representativeness, impact assessment, and life-cycle are not addressed in 27001, and integration that reduces them to information-security controls is a finding against the 42001-specific clauses.
- **Treating 42001 impact assessment as a DPIA.** The 42001 impact assessment is broader than privacy; DPIAs under GDPR / 27701 are narrower and do not substitute.
- **Reducing 14971 to the 42001 risk assessment.** For medical devices, 14971 is the primary risk-management reference and 42001 is additive — not the other way around.
- **Single register without reporting-flow divergence.** The integrated nonconformity / incident register is fine; the mandatory-reporting flows (Article 73 EU AI Act; GDPR Article 33; FDA MDR; state and sector obligations) are not integrated and must be tested per regime.
- **Audit team without each standard's competence.** The CB's QA review will catch; accreditation inspection will catch sooner.
- **Audit-day discount inconsistent with IAF policy.** Discounts beyond allowed ranges undermine certification defensibility.

## Summary

- Integrated audits of ISO/IEC 42001 with 27001, 27701, 9001, 13485, 14971 are common in mature and regulated organisations; the ISO/IEC 17021-1 clause 9.1.5.1 integration provision governs.
- Overlap concentrates in document control, change management, incident management, supplier management, and generic risk management; integration can defensibly share controls and evidence here.
- Divergence concentrates in AI data governance, AI system impact assessment, AI life-cycle controls, device-specific risk management (14971), and mandatory-reporting flows; integration cannot substitute these.
- The audit plan under 17021-1 clause 9.1.5.1 covers one team, one scope-spanning opening/closing, a shared sample plan where populations overlap, a single finding register with per-standard tagging, and an audit-day calculation combining ISO/IEC 42006 Annex A for AIMS with the sector documents for each other standard.
- The AI Auditor at L45 leads AIMS-only audits, is a competent AIMS team member on integrated audits, and over time can lead AIMS + ISMS integrations; sector-specific standards (13485, 14971) remain the province of specialists.
- The delta from `ai-evaluation-engineer` (L35) and `senior-ai-governance-architect` (L50) is the independence posture: the auditor tests what the architect designs and what the evaluation engineer executes — the role separation is a 17021-1 clause 5 requirement, not just a preference.
