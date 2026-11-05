# Regulator-Facing Submission Shapes

## Motivation

Some engagement outputs reach regulators. The shape the regulator requires is not the same as the shape the audit committee wants to see; nor is it the same across regulators. Filing an EU AI Act Article 73 serious-incident notification in the shape of a SOC 2 exception summary does not satisfy the obligation. Filing an SR 11-7 validation finding in free-text prose does not fit the Fed's supervisory channel. The auditor's job is to prepare content so the regulated entity can file it correctly, and to understand where the auditor's role ends and the entity's (and counsel's) begins.

This chapter walks four submission shapes the AI auditor is likely to see — the EU AI Act Article 73 serious-incident notification, the OSCAL (Open Security Controls Assessment Language) representation for US federal audiences, SR / SAR letters and MRM-channel supervisory language for Fed-regulated institutions, and the FDA 483-observation-response shape where adapted for AI SaMD — plus the counsel-boundary that determines what the auditor writes and what counsel writes.

## The entity–auditor–counsel triangle

Regulator-facing submissions typically involve three parties.

- **The regulated entity.** Files the submission. Signs the attestation. Faces the regulator's enforcement power.
- **The auditor.** Produces audit-report content that the entity attaches as an exhibit, or performs specific testing the regulation refers to.
- **Counsel.** Drafts privileged assessments, advises on disclosure obligations, handles the submission's legal content (including the entity's rights, the scope of the admission, the preserved defences).

The auditor does not write the regulated entity's legal filings. The auditor does not opine on the regulator's likely response. The auditor does not negotiate directly with the regulator outside specific designation agreements (notified-body, certification-body, Fed-examiner-with-institution-present).

Auditors who drift into legal advice create liability for themselves (unauthorised practice of law; independence violation) and for the entity (privilege waiver; disclosure overreach). The posture is: **the auditor prepares the audit exhibit, writes the auditor's cover letter if customary, and otherwise defers to counsel and management.**

## EU AI Act Article 73 — serious-incident notification

**Legal basis.** Regulation (EU) 2024/1689, Article 73.

### Who notifies

The **provider** of a high-risk AI system shall notify any **serious incident** to the market surveillance authority of the Member State where the incident occurred. Deployers may also be in scope under certain Article 26 obligations.

### What is a serious incident

Article 3 defines "serious incident" to include incidents that directly or indirectly lead to:

- the death of a person, or serious damage to a person's health;
- a serious and irreversible disruption of the management or operation of critical infrastructure;
- infringement of obligations under Union law intended to protect fundamental rights;
- serious damage to property or the environment.

### When

The Act prescribes notification timing bands:

- **Immediately** after the provider has established the causal link (or its reasonable likelihood) between the AI system and the serious incident, and in any event:
- **Not later than 15 days** after awareness, in the general case.
- **Shorter** windows where the incident involves death of a person or a widespread infringement (per Article 73) — immediately and not later than 2 days.<!-- needs-research: confirm final Article 73 timing bands and narrower cases at reading time; the trilogue text has specific deadlines. -->
- **Longer** windows may apply for certain subcategories of incident where the full picture requires further investigation; see Article 73's final text.

### What is in the notification

Article 73 and the implementing-act / guidance texts prescribe content including:

- Provider identity and contact.
- Description of the incident (date, location, consequences).
- Identification of the AI system (name, version, intended purpose, serial / batch identifier, EU database registration reference).
- Description of the deployer and the use context.
- Suspected causal link between the incident and the AI system.
- Immediate corrective actions taken.
- Information to the deployers and other affected parties.

Additional reporting may follow as the investigation proceeds (follow-up report, final report).

### The auditor's role

- Where the auditor identified the incident during an engagement, the auditor's finding content (condition, evidence trail, causal link assessment) supports the entity's notification. The entity (with counsel) writes the notification; the auditor's finding is referenced or attached.
- Where the auditor's post-market monitoring review (`mod-108` chapter 5) identifies that notification obligations were missed, the auditor raises a finding on the missed obligation — the auditor does not freelance the notification itself.
- The auditor may be asked to review a draft notification for factual accuracy on the AI-system technical content; the auditor does so against evidence, not as drafting counsel.

### Common failure modes

- **Over-reliance on the 15-day window.** The Act requires "immediately" where the causal link is established; the 15-day deadline is an outer bound, not a comfort zone.
- **Content gaps.** Notifications filed without the enumerated content elements receive follow-up requests and may undermine the provider's position.
- **Scope disputes.** Provider disputes that an incident is "serious" within Article 3 to avoid filing; the auditor's independent view on the classification matters.
- **No linkage to the EU database entry.** Article 71 database registration and Article 73 notification are coordinated; omitting the database reference is a tell.

## OSCAL — Open Security Controls Assessment Language

**Standard.** NIST's OSCAL is a set of formats for representing control catalogues, profiles, system security plans, assessment plans, assessment results, and plan-of-action-and-milestones (POA&M) in machine-readable form (XML, JSON, YAML). OSCAL is maintained by NIST and used across the U.S. federal cybersecurity and supply-chain-assurance context — FedRAMP has adopted OSCAL for submissions; DoD CMMC has adopted OSCAL for assessments.<!-- needs-research: confirm the current OSCAL version (v1.x) and the current FedRAMP OSCAL submission requirements at reading time; both have moved quickly. -->

### Where OSCAL touches AI audit

- **FedRAMP-authorised AI/ML services.** An AI service pursuing FedRAMP authorisation submits its System Security Plan, assessment results, and POA&M in OSCAL form. The auditor's (3PAO's) report is encoded in the OSCAL Assessment Results (AR) model.
- **NIST AI RMF overlays.** The NIST AI RMF's profiles may be represented in OSCAL where an agency chooses to formalise AI controls at the OSCAL layer.
- **AI-specific sector submissions.** Some federal agencies may require OSCAL-encoded evidence of AI-control conformance alongside the main cybersecurity authorisation.

### OSCAL model highlights for the auditor

- **Catalog** — the authoritative set of controls (e.g., NIST SP 800-53 Rev 5).
- **Profile** — a tailoring of the catalogue for a specific baseline or use.
- **System Security Plan (SSP)** — the system's documentation against the profile.
- **Assessment Plan (AP)** — the auditor's planned procedures.
- **Assessment Results (AR)** — the auditor's findings and observations in the standard form.
- **Plan of Action and Milestones (POA&M)** — the remediation tracker.

### The auditor's role

- Encode findings in the AR model's required fields (finding identifier, target of the finding, observation, risk, recommendation, status).
- Represent POA&M entries in the standard form so the agency can consume and track.
- Honour the form's cross-references between findings, observations, and risks — the OSCAL schema enforces linkage.

### Common failure modes

- **Free-text in OSCAL fields.** The auditor writes a long narrative in a field meant for a short identifier. The agency's tooling cannot consume it.
- **Missing linkage.** Finding present but not linked to the observation that produced it; POA&M present but not linked to the finding it addresses.
- **Schema-version mismatch.** OSCAL is actively evolving; the submission must match the schema version the agency has accepted.
- **AI-specific content shoehorned into cybersecurity fields.** AI-specific controls that do not map to SP 800-53 categories are forced into inappropriate places; where no profile addresses them, the auditor documents the gap explicitly rather than mis-mapping.

## SR / SAR letters and MRM supervisory channels

**Context.** Federal Reserve supervisory communication with state-member banks, bank holding companies, and other regulated institutions runs through SR letters, Section 4(m) supervisory letters, Matters Requiring Attention (MRA), Matters Requiring Immediate Attention (MRIA), and the examination report. For MRM specifically, SR 11-7 remains the anchor.

### Shapes relevant to the AI auditor

- **Validation report** — the primary MRM artefact. Internal; delivered to the Model Risk Committee and the CRO.
- **MRM program report to supervisor** — aggregated program state tabled during examination.
- **MRA / MRIA** — supervisor-issued, not auditor-issued. The auditor's findings may become supervisor MRAs when the supervisor concurs.
- **SAR (Suspicious Activity Report) — distinct from SR letters** — a regulatory filing under the Bank Secrecy Act for suspected financial crimes. If an AI system's output flags suspected money-laundering activity, the SAR filing is a separate, non-auditor process; the auditor's finding on the SAR process is an audit finding, not a SAR filing.<!-- needs-research: ensure the latest FinCEN SAR filing guidance is referenced at reading time; the SAR system is FinCEN-administered under 31 CFR 1020. -->

### The auditor's role

- Write the validation report to the standard (chapter 4) with classifications per chapter 2.
- Support the MRM function's engagement with the supervisor — be available for examiner questions; produce workpapers on request within the institution's supervisor-cooperation protocol.
- Do not freelance supervisor communications. If the supervisor asks the auditor a question outside the institution's presence, the auditor's firm's protocol governs (often: the auditor confirms the question and defers substantive answer until the institution and its counsel are informed).

### Common failure modes

- **Direct auditor-supervisor side channel.** Prohibited outside the institution's visibility. Erodes trust and creates privilege and independence issues.
- **Auditor language that pre-empts supervisor classification.** Writing "this is an MRIA-level issue" claims the supervisor's authority; the auditor rates findings, the supervisor rates matters.
- **Pass-through of internal validation findings into supervisor correspondence.** Some validations contain internal-only candour the institution would not include in supervisor-facing text; the auditor's write-up anticipates both audiences.

## FDA 483 observation response — adapted for AI SaMD

**Standard.** FDA Form 483 is issued at the close of an FDA inspection of a regulated manufacturer (device, drug, biologic, food). It lists the investigator's observations of apparent violations of regulations. The manufacturer's response to a 483 is a critical regulatory interaction.

### Where AI auditors encounter the 483 shape

- **AI-enabled Software-as-a-Medical-Device (SaMD)** — devices subject to 21 CFR 820 QSR / 21 CFR Part 11 electronic records, with the AI/ML components covered by evolving FDA guidance on Good Machine Learning Practice (GMLP) and Predetermined Change Control Plans (PCCPs).
- **Inspection follow-ups** — FDA investigators may inspect a device manufacturer's AI-development processes; observations may touch AI-specific controls.
- **Auditor-prepared responses** — an audit function or external consultant may support the manufacturer in preparing the 483 response.

### 483 response shape

A 483 response (typically filed within 15 business days to be considered by the FDA when the Establishment Inspection Report is prepared):

- Addresses **each observation** individually.
- States the **immediate correction** taken.
- States the **systemic corrective action** planned (CAPA under the manufacturer's quality system).
- Provides **evidence** that the action has been taken or is under way.
- References the **Quality System** record IDs.
- Is signed by the responsible executive.

For AI-specific observations:

- The response must distinguish correction of the specific device software from systemic correction of the AI/ML development lifecycle.
- The response may reference the manufacturer's PCCP where applicable, demonstrating that the AI-specific change was anticipated or that the change required re-submission.<!-- needs-research: reference the current FDA PCCP guidance at reading time; FDA issued PCCP final guidance in 2024-12 and may issue further supplements. -->
- The response must cover 21 CFR 820 design-control / CAPA requirements as they apply to the AI/ML components.

### The auditor's role

- Where the audit function identified the observation prior to the FDA inspection, the response can reference the audit's prior finding and the planned remediation.
- Where the auditor is supporting the response, the auditor provides evidence that corroborates the correction — not drafting counsel's legal response.
- The auditor's report on the AI/ML quality system that does not meet 21 CFR 820 is itself a finding; whether it becomes a 483 observation is in the FDA investigator's judgement.

### Common failure modes

- **Treating observations as tasks.** Each observation needs a correction *and* corrective action; the response that lists "fixed this record" without naming the systemic change invites additional observations.
- **Overcommitting.** Response promises timelines the manufacturer cannot meet. Missed commitments to FDA have specific consequences.
- **Missing CAPA.** The manufacturer's own quality system requires a CAPA record for the observation; the 483 response must reference the CAPA ID.
- **Not distinguishing the device from the lifecycle.** An AI model change requires lifecycle attention; a one-time retrain fixes the model but not the lifecycle gap.

## Where legal opinion lives (and where it does not)

The regulator-facing submission is where the auditor is most tempted to opine on regulatory posture. The posture is: **the auditor's domain is the facts and the engagement scheme's classification; counsel's domain is regulatory posture, admissions, waiver, preserved defences, and submission strategy.**

### What the auditor does

- Produces audit content — findings, classifications, evidence, workpapers.
- Prepares exhibits in the engagement scheme's shape (ISO, SOC, SR 11-7 validation report, LL144 summary, EU AI Act Annex VII report).
- Reviews the technical accuracy of the entity's draft submission when asked.
- Answers questions the regulator directs through the entity when authorised.
- Participates in supervisor examination under the institution's cooperation protocol.
- For notified-body and certification-body designations, follows the designation agreement for direct regulator interaction.

### What the auditor defers to counsel

- Interpretation of the regulation beyond what the engagement scheme's standard incorporates.
- Advice on whether to self-disclose or self-report.
- Negotiating the regulator's response.
- Privilege strategy.
- Admissions in the submission.
- Litigation holds and preservation obligations.
- Regulatory defence posture.

A clear way to hold the line: the auditor answers technical questions on specific evidence from the engagement; the auditor refers legal questions to counsel without providing an interim view.

## A note on cross-border coordination

AI providers increasingly operate under multiple regulators simultaneously — EU (AI Act, GDPR), US (sector regulators, state laws like Colorado SB24-205, local laws like NYC LL144), UK (regulatory sandbox and sector approaches), Canada (AIDA where enacted), Singapore (Model AI Governance Framework), and others.<!-- needs-research: verify the current state of each jurisdiction at reading time; AIDA, EU AI Act implementing acts, and US state laws are moving fast. -->

The auditor:

- Maps the engagement scheme's output to each regulator's expected shape.
- Does not combine multi-regulator submissions into a single omnibus filing unless specifically designed for that (rare).
- Flags conflicts where one regulator's disclosure requirement collides with another's confidentiality expectation; counsel resolves.
- Tracks across the register (chapter 6) which submissions are due to which regulator on what cycle.

## Interfaces to adjacent chapters

- Chapter 1 (CCCER) produces the audit content that becomes the exhibit.
- Chapter 2 (classification) produces the severity label the regulator reads.
- Chapter 3 (management response) produces the correction-and-corrective-action content that often appears in the regulator-facing submission.
- Chapter 4 (report shapes) produces the audit report that attaches as exhibit.
- Chapter 5 (delivery) covers the delivery channels; this chapter covers the format for the regulator-bound channel.
- Chapter 6 (register) tracks submission obligations alongside finding closures.
- `mod-108` (post-market surveillance, incident reporting) is the signal source that often triggers Article 73 filing shape.
- `mod-112` (audit leadership and regulator interface) consolidates the leadership posture at the regulator layer.

## Summary

- Regulator-facing submissions are owned by the regulated entity and advised by counsel; the auditor produces content in the engagement scheme's shape and defers legal strategy.
- EU AI Act Article 73 serious-incident notifications have prescribed timing (immediate; outer bound of 15 days in the general case; shorter for the most severe categories) and prescribed content; the auditor's finding supports but does not substitute for the entity's notification.
- OSCAL is the US federal standard format for controls assessment artefacts (AP, AR, POA&M); FedRAMP and other federal AI-service submissions encode auditor findings in these models; schema fidelity and cross-reference integrity are the auditor's job.
- Fed MRM / supervisory channels receive validation reports through the institution; MRA / MRIA classifications belong to the supervisor, not the auditor; direct auditor-supervisor side channels are prohibited outside specific protocols.
- FDA 483 observations for AI SaMD require a response addressing each observation with immediate correction, systemic corrective action, evidence, CAPA reference, and PCCP context where applicable — within the FDA's 15-business-day window to be considered in the Establishment Inspection Report.
- The auditor-counsel boundary is explicit: facts and scheme-classification are the auditor's; regulatory posture, disclosure strategy, admissions, privilege, and defence are counsel's.
- Cross-border engagements require per-regulator submission shapes tracked in the register; the auditor flags inter-regulator conflicts for counsel rather than resolving them.
