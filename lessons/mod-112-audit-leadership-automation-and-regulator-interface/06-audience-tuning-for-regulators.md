# Audience-Tuning for Regulators

## Motivation

The posture in chapter 5 is cross-regulator. The *content* of a regulator interface is not. Regulators differ in their statutory authority, their technical depth, their enforcement toolkit, their preferred document formats, their examination cadence, their appetite for voluntary disclosure, their coordination with other regulators, and their speed. A finding written for the Federal Reserve's model-risk function reads differently than one written for the EU AI Office, the UK AI Safety Institute, the FDA Center for Devices and Radiological Health, or the CNIL. An audit function that produces one-shape content across every audience gets caught out on all of them.

This chapter walks the regulator landscape the AI auditor is likely to interface with as of 2026, with notes on each regulator's authority, scope, posture, and content expectations. It is a survey; each regulator warrants deeper study where the engagement actually touches that regulator's jurisdiction.

## EU — the AI Act regulatory architecture

The EU AI Act (Regulation (EU) 2024/1689) created a layered supervisory structure.

### EU AI Office

**Where it sits.** Within the European Commission (DG CNECT).

**Scope.** The AI Office has specific competence for general-purpose AI (GPAI) models, including systemic-risk GPAI, under Articles 88–94 and related provisions. The Office also coordinates across Member State market surveillance authorities for cross-border matters.<!-- needs-research: confirm exact AI Office competence and the current list of designated roles at reading time; the Office is young and its scope is still being operationalised. -->

**Posture.** Technical; policy-informed; coordinating across the European AI Board (EAIB) and national authorities. Content expectations tend toward structured documentation (Article 53 obligations for GPAI providers; copyright and training-data transparency; risk-assessment and incident-reporting for systemic-risk models).

**Audit interface.** Providers of GPAI and systemic-risk GPAI models may be asked for internal documentation, model cards, evaluation evidence, systemic-risk assessment, and incident history. The audit function's prior work on model-card accuracy (`mod-106`), risk classification (`mod-103`), and systemic-risk-adjacent evaluation supports the provider's engagement with the Office.

### National competent authorities (NCAs)

**Where they sit.** Each Member State designates one or more NCAs to act as market surveillance authorities under the AI Act. Many Member States have assigned the data-protection authority or an existing sector regulator; some have created new bodies.<!-- needs-research: as of reading time, verify each Member State's designated NCA; this is being actively published Member State by Member State. -->

**Scope.** Enforcement of the AI Act for AI systems other than GPAI models — primarily high-risk systems under Annex III and the related conformity-assessment obligations.

**Audit interface.** NCAs can request the Annex IV technical documentation, the post-market monitoring records (Article 72), the serious-incident notifications (Article 73), and evidence of registered status (Article 71).

### Member State data-protection and sector authorities

These regulators pre-date the AI Act and continue under their own frameworks, with increasing overlap on AI.

- **CNIL (France).** Highly active on AI governance; publishes guidance on AI and GDPR; participates in enforcement where AI touches personal data.
- **ICO (UK).** AI-specific guidance on data protection in AI systems; audits around AI use of personal data; publishes decisions.
- **Garante per la protezione dei dati personali (Italy).** Active on AI (notable interventions on generative AI services in 2023–2024).
- **BfDI / Landesdatenschutzbehörden (Germany).** Federal and state DPAs with AI-adjacent oversight.
- **AEPD (Spain), Autoridad Catalana de Protección de Datos**, **DPC (Ireland)** (lead authority for many multinational providers under GDPR), and others.

**Content expectations.** GDPR-shaped: Article 35 DPIA, Article 22 automated-decision analysis, Article 6 / 9 lawful basis, data-subject-rights handling, Article 32 security of processing. For AI-adjacent inquiries, DPAs often request model-card-like documentation on training data, purpose, retention, and specific protective measures.

### Notified bodies

**Where they sit.** Designated conformity-assessment bodies under the AI Act's Annex VII / Article 43 route for high-risk systems that require third-party conformity assessment. Notified bodies are themselves supervised by designation authorities and assessed by national accreditation bodies.

**Audit interface.** Notified bodies audit providers of high-risk AI systems for conformity with Annex III / Section 2 requirements. The audit function of the provider produces evidence; notified-body auditors have specific designation-agreement authority to receive. See `mod-110` for the conformity-assessment-process landscape.

## US — the federal and state regulatory landscape

The US does not have a comprehensive federal AI regulation (as of 2026). AI oversight runs through sector regulators, state laws, and enforcement under existing statutes.

### US AI Safety Institute (AISI)

**Where it sits.** Within the National Institute of Standards and Technology (NIST), Department of Commerce.

**Scope.** Technical safety evaluation of frontier models; developing evaluation methodologies; providing input to policy-makers. Not a regulator in the enforcement sense; a technical-standards and evaluation body.<!-- needs-research: confirm US AISI's current authorities and the status of any voluntary commitments the institute administers at reading time; its role is evolving. -->

**Audit interface.** Frontier-model providers may have voluntary commitments to US AISI around pre-deployment evaluation. The audit function's evidence of evaluation methodology, red-team records, and pre-deployment testing supports the provider's reporting.

### Food and Drug Administration (FDA)

**Where it sits.** Health and Human Services. Center for Devices and Radiological Health (CDRH) governs medical devices; Center for Drug Evaluation and Research (CDER) governs drugs; the Digital Health Center of Excellence coordinates across.

**Scope for AI.** AI-enabled Software-as-a-Medical-Device (SaMD); AI components of hardware devices; AI use in clinical trials; AI in drug development is an emerging area.

**Regulatory shape.** 21 CFR 820 Quality System Regulation (and the forthcoming QMSR aligning to ISO 13485); 21 CFR Part 11 electronic records; evolving guidance on Good Machine Learning Practice (GMLP), Predetermined Change Control Plans (PCCPs), and transparency.

**Audit interface.** FDA inspections of device manufacturers may encounter AI-specific content. Form 483 observations and response (see `mod-111` chapter 7). The audit function supports the manufacturer's quality system records (design controls, V&V, risk management per ISO 14971, CAPA) as evidence of compliance.

### Federal Reserve, OCC, FDIC

**Where they sit.** Federal Reserve System; Office of the Comptroller of the Currency (Treasury); Federal Deposit Insurance Corporation. Together they supervise banks and bank holding companies.

**Scope for AI.** Model risk management (SR 11-7 at the Fed; OCC 2011-12 at the OCC; FDIC's 2017 FIL on model risk at FDIC-supervised institutions); third-party risk (OCC / Fed / FDIC interagency guidance); operational risk, consumer compliance, and fair lending adjacent to AI.

**Posture.** Supervisory — the primary tools are Matters Requiring Attention (MRA), Matters Requiring Immediate Attention (MRIA), consent orders, and formal enforcement actions.

**Audit interface.** MRM-focused engagements produce validation reports (SR 11-7 shape). Examinations inspect the MRM program and specific model validations. The audit function's independent validation work is central; the regulator's examination team reads validation workpapers and interviews the validators.

### Consumer Financial Protection Bureau (CFPB)

**Where it sits.** Consumer Financial Protection Bureau (independent agency).

**Scope for AI.** Fair lending (ECOA, Regulation B) adjacent to algorithmic underwriting; UDAAP (unfair, deceptive, abusive acts and practices) adjacent to AI-driven marketing and decisions; adverse action notices required for credit decisions including algorithmic ones.

**Audit interface.** Examinations of covered institutions may include AI-driven decisioning. The audit function's fair-lending evidence (disparate impact analysis; adverse action notice content; model-input review) supports the institution's examination posture.

### Federal Trade Commission (FTC)

**Where it sits.** Independent federal agency.

**Scope for AI.** Section 5 unfair and deceptive practices; Section 5 unfair methods of competition; specific orders and guidance on AI (including requirements for algorithmic disgorgement in certain cases); deceptive-trade-practice enforcement around AI claims; commercial surveillance and children's privacy (COPPA).

**Audit interface.** FTC investigations may demand training-data provenance, model claims substantiation, advertising review for AI-related claims, and in some cases model-deletion / disgorgement evidence. The audit function's prior work on model-card claim verification (`mod-106`) and training-data provenance (`mod-109`) supports the entity.

### Equal Employment Opportunity Commission (EEOC)

**Where it sits.** Independent federal agency.

**Scope for AI.** Title VII (race, color, national origin, sex, religion), ADEA (age), ADA (disability), GINA (genetic information); AI use in employment decisions (hiring, promotion, discipline, termination) through these statutes; guidance on AI and selection procedures.

**Audit interface.** Charges or systemic investigations may inspect algorithmic selection procedures, validation studies per the Uniform Guidelines on Employee Selection Procedures, four-fifths-rule analysis, and reasonable-accommodation processing. The audit function's fairness audit workpapers support the employer's position.

### Department of Justice (DOJ)

**Where it sits.** Federal executive department.

**Scope for AI.** Civil rights enforcement (through the Civil Rights Division); ADA Title II and Title III; Fair Housing Act in coordination with HUD; antitrust (AI and competition); criminal enforcement where AI-enabled fraud, child-safety violations, or other criminal conduct is involved.

**Audit interface.** Investigations tend to be high-stakes and counsel-led; the audit function operates strictly under counsel's direction.

### Nuclear Regulatory Commission, NHTSA, FAA, and other safety regulators

Where AI touches safety-critical domains (nuclear, automotive autonomy, aviation), the sector's safety regulator governs. Audit interfaces are deeply sector-specific and operate on each sector's established safety-case methodology.

### FDA Device Center — Predetermined Change Control Plans (PCCPs)

PCCPs are a specific FDA mechanism (finalised guidance issued 2024-12) permitting pre-authorised modifications to AI/ML-enabled SaMD without a new submission for each change.<!-- needs-research: confirm FDA PCCP guidance final-publication date and current implementation status at reading time. --> Audit interface: evidence that the change was within the PCCP scope and that the organisation followed its PCCP; where a change was out of scope, evidence that a new submission was filed.

### State insurance regulators (NAIC + state DOIs)

**Where they sit.** Each state has a Department of Insurance; the National Association of Insurance Commissioners (NAIC) is a standard-setting and coordination body for state regulators.

**Scope for AI.** Use of AI in insurance (pricing, underwriting, claims); NAIC's Model Bulletin on AI (2023), state-level adoption varies; market-conduct examinations; prior-approval filings for rates; unfair discrimination prohibitions in state codes.

**Audit interface.** Market-conduct examinations inspect AI use in rating and claims; prior-approval filings for rates that use AI may require specific disclosures. The audit function's fairness and performance evidence supports the insurer's regulatory filings.

### State attorneys general and state AI laws

Multiple states have enacted AI-specific laws:

- **Colorado SB24-205** (AI developer and deployer obligations for high-risk AI).
- **California** (various statutes, including SB-1120 on AI in utilisation review; AB-2013 on training-data transparency).
- **New York** (NYC Local Law 144 for automated employment decision tools; SHIELD Act for data security).
- **Texas** (HB 2060 state agency AI; TRAIGA — Texas Responsible AI Governance Act — depending on enactment state at reading time).
- **Virginia, Connecticut, Illinois, Utah, Washington** have AI-related provisions in consumer-protection, insurance, or employment statutes.<!-- needs-research: confirm the state-by-state AI-law landscape at reading time; this is changing quarterly. -->

**Audit interface.** Attorneys general investigations use state consumer-protection statutes; audit interface patterns resemble FTC inquiries.

### NYC Local Law 144 — specific audit interface

LL144 requires an annual independent bias audit of certain automated employment decision tools used by NYC employers and employment agencies, with the audit summary published. The AI auditor's engagement produces:

- The bias-audit report in LL144's specified shape.
- The published summary content.
- Evidence of the four-fifths-rule analysis per category.
- Methodology notes supporting the result.

The audit function supports the publication's accuracy and the employer's downstream notice-to-candidate obligations.

## UK — post-Brexit AI regulatory posture

### UK AI Safety Institute (UK AISI)

**Where it sits.** Within the Department for Science, Innovation and Technology.

**Scope.** Technical evaluation of frontier models; collaboration with US AISI; development of evaluation tooling (Inspect AI framework).<!-- needs-research: confirm UK AISI's current name, authorities, and the state of any voluntary commitments at reading time; the UK government has restructured its AI governance units repeatedly. -->

**Audit interface.** Analogous to US AISI — voluntary commitments by frontier-model providers; technical evaluation output; audit function's evidence of evaluation methodology and red-team records.

### Information Commissioner's Office (ICO)

**Where it sits.** Independent UK regulator for data protection.

**Scope for AI.** UK GDPR and Data Protection Act 2018 applied to AI systems; specific AI guidance; enforcement powers under DPA 2018.

**Audit interface.** DPIAs; Article 22 analysis; data-subject-rights handling; audit function's evidence of AI-specific data-protection controls.

### Sector regulators

UK's sector regulators (FCA, PRA, Ofcom, MHRA, Ofqual, CMA, EHRC) have each issued AI-adjacent guidance under the UK's "pro-innovation" sector-led approach. The audit function maps each engagement to the relevant sector regulator's expectation.

## Asia-Pacific regulators

### Singapore — IMDA / PDPC

**Where they sit.** Infocomm Media Development Authority (IMDA) and the Personal Data Protection Commission (PDPC); related: AI Verify Foundation.

**Scope for AI.** Model AI Governance Framework (voluntary guidance); AI Verify (testing framework for AI systems); Singapore's Model AI Governance Framework for Generative AI; data-protection obligations under the PDPA.

**Audit interface.** Model AI Governance Framework-aligned assessments; AI Verify testing where the provider participates; PDPC enforcement under the PDPA for AI-adjacent data protection.

### Japan — METI / PPC

**Where they sit.** Ministry of Economy, Trade and Industry (METI); Personal Information Protection Commission (PPC).

**Scope for AI.** AI governance guidelines (METI publishes); APPI (Act on the Protection of Personal Information) at PPC; sector-specific regulation (financial services at FSA, medical devices at PMDA).<!-- needs-research: confirm Japan's current AI regulatory architecture at reading time; Japan is moving on a draft AI Bill. -->

**Audit interface.** Guideline-aligned assessments; APPI compliance for AI processing personal information.

### Korea — PIPC and sector regulators

**Where it sits.** Personal Information Protection Commission (PIPC); Financial Services Commission (FSC); sector regulators.

**Scope for AI.** PIPA (Personal Information Protection Act); Korea's AI Basic Act (enacted / in force per reading time); specific obligations on high-risk AI and transparency.<!-- needs-research: confirm Korea's AI Basic Act status and effective date at reading time; Korea passed an AI framework law in 2024-12. -->

**Audit interface.** AI Basic Act compliance; PIPA compliance for AI processing; sector-regulator engagement where relevant.

### Other Asia-Pacific jurisdictions

**China.** Cyberspace Administration of China (CAC); specific generative-AI and deep-synthesis provisions; algorithmic recommendation provisions; data-outbound-transfer rules. Content expectations are specific and the regulatory stance is distinct.

**Hong Kong.** Office of the Privacy Commissioner (PCPD) with AI guidance; sector regulators including HKMA on AI in banking.

**India.** Multiple threads — Digital Personal Data Protection Act (DPDPA); MEITY's AI advisories; sector-specific guidance; the Digital India Act under drafting.<!-- needs-research: confirm India's AI regulatory status at reading time. -->

**Australia.** Attorney-General's Department coordinates on AI; OAIC (Office of the Australian Information Commissioner) on privacy; sector regulators; voluntary AI Ethics Framework.

## Supranational and standards-adjacent bodies

The AI auditor also interfaces with bodies that are not enforcement regulators but influence or formalise the criteria:

- **OECD.** AI Principles and OECD.AI observatory; policy and measurement framework.
- **UNESCO.** Recommendation on the Ethics of AI (2021); readiness assessment methodology (RAM) for Member States.
- **ISO technical committees** — ISO/IEC JTC 1/SC 42 (Artificial Intelligence) is the primary standards body; publications include ISO/IEC 42001, 23894, 25059, 42005, 24028, 24029, 5338, 5339, and more.
- **CEN/CENELEC JTC 21** — the European standards body developing harmonised standards under the AI Act.
- **BSI (UK), ANSI (US)** — national standards bodies that mirror ISO into national standards or publish their own.
- **IEEE.** Standards (IEEE 7000 series on ethical AI); P7001 Transparency; P7003 Algorithmic Bias; Autonomous and Intelligent Systems certification.
- **NIST.** AI RMF; associated profiles and playbook; genAI Profile.
- **The Frontier Model Forum, Partnership on AI, MLCommons** — industry bodies producing benchmarks and shared evaluation practice.
- **AISIC (Artificial Intelligence Safety Institute Consortium)** — US AISI's industry consortium.

## Audience tuning in practice

With the landscape in view, the auditor tunes four dimensions for each audience.

### Technical depth

Technical regulators (US AISI, UK AISI, FDA CDRH, notified bodies) read technical content directly. The report includes methodology detail, dataset descriptions, statistical results, and reproducibility notes.

Non-technical regulators (consumer agencies, some state DOIs, some AG offices) read for impact. The report leads with the finding's effect on affected parties, with technical detail in appendices.

### Format

- OSCAL for US federal audiences (`mod-111` chapter 7).
- Annex IV / VII shape for EU AI Act audiences (`mod-110`).
- SR 11-7 validation report shape for Fed/OCC/FDIC.
- 483-response shape for FDA post-inspection.
- LL144 published summary shape for NYC.
- Written response letter with exhibit attachments for most consumer / state regulators.

### Language

- **Technical.** Specific methods named; datasets cited; statistical results stated.
- **Regulatory.** The specific statute or clause invoked; the specific obligation; the specific remediation committed.
- **Rights-impact.** The affected population; the harm channel; the measured or estimated footprint.
- **Financial.** For financial-reporting-adjacent AI, the effect on the financial statement assertion.
- **Safety.** For safety-critical AI, the hazard, the harm severity, the mitigation.

The auditor tunes but does not sanitise. Content does not shift to flatter the regulator's expectations; content shifts to speak the regulator's shared vocabulary.

### Cadence

- **Scheduled** (annual LL144 publication; FDA Establishment Inspection Report issuance; ISO/IEC 42001 surveillance audits).
- **Event-driven** (EU AI Act Article 73 serious-incident; FDA MDR 21 CFR 803; Fed MRA / MRIA follow-up; FTC CID response).
- **Ongoing** (GRC-for-AI platform dashboards shared with examiners during open examinations; continuous-audit outputs).

A senior audit function tracks all three cadences across all applicable regulators in one register.

## Cross-regulator coordination

Where the entity is under multiple regulators simultaneously, the audit function:

- Produces one set of underlying evidence and conforms format per audience.
- Avoids inconsistent statements across regulators.
- Flags to counsel any obligation conflict (one regulator's disclosure requirement collides with another's confidentiality expectation; counsel resolves).
- Supports the entity's regulator-coordination function where there is one (often the General Counsel's office or the Chief Compliance Officer).

## Summary

- Regulators differ in authority, scope, technical depth, enforcement toolkit, preferred format, cadence, and coordination posture; the AI auditor tunes content per audience without changing the underlying facts.
- EU audiences include the EU AI Office (GPAI and systemic-risk models), national competent authorities (high-risk systems), DPAs under GDPR (AI-touching personal data), and notified bodies (Annex VII conformity assessment).
- US audiences include US AISI (voluntary technical interface), FDA (SaMD), Fed/OCC/FDIC (MRM and banking supervision), CFPB (consumer financial AI), FTC (unfair/deceptive AI practices), EEOC (employment AI), DOJ (civil rights, antitrust, criminal), FDA Device Center (PCCPs), NAIC + state DOIs (insurance), and state AGs under state AI laws.
- UK audiences include UK AISI, ICO, and sector regulators under the pro-innovation sector-led approach.
- Asia-Pacific audiences include IMDA/PDPC (Singapore), METI/PPC (Japan), PIPC + Korean sector regulators, CAC (China), PCPD/HKMA (Hong Kong), MEITY (India), OAIC + sector (Australia).
- Standards-adjacent bodies — OECD, UNESCO, ISO JTC 1/SC 42, CEN/CENELEC JTC 21, BSI, ANSI, IEEE, NIST, Frontier Model Forum, Partnership on AI, MLCommons, AISIC — influence criteria even without enforcement power.
- Audience tuning dimensions: technical depth, format (OSCAL, Annex IV/VII, SR 11-7 shape, 483 response, LL144, written response letter), language register, cadence (scheduled, event-driven, ongoing).
- Cross-regulator coordination preserves consistent facts across audiences, surfaces obligation conflicts to counsel, and supports the entity's regulator-coordination function.
