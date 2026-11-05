# External-Auditor Coordination

## Motivation

AI audit work is rarely performed in isolation. The internal AI audit function sits beside external financial auditors (who may rely on internal audit's work for financial-reporting-relevant AI), SOC auditors (who may incorporate the internal function's work into their SOC examinations), ISO certification-body auditors (who audit the AIMS), notified bodies (who assess conformity under the AI Act), IAAIS-designated auditors (who perform specific external assurance), and the entity's regulators (who may rely on external auditor work). Each of these externals operates under its own standards and reliance rules. A senior AI auditor who runs the internal function knows where those rules intersect and manages the coordination deliberately rather than by accident.

Done well, external-auditor coordination reduces duplicate work, speeds examination, and increases the regulator's and audit committee's confidence in the overall assurance picture. Done poorly, it produces misalignment between internal and external views, invalidates the external's ability to rely, triggers scope disputes mid-engagement, and in the worst case compromises the independence of either the internal or the external function.

This chapter walks the standards that govern external auditor reliance on internal audit, coordination with notified bodies and certification bodies, coordination with SOC auditors, and the IAAIS-designated-auditor interface.

## ISA 610 — the external auditor using the work of internal auditors

### The standard

**International Standard on Auditing (ISA) 610 (Revised 2013)**, issued by the IAASB, governs the external financial auditor's use of the work of internal auditors in a financial-statement audit. It has two principal modes:

- **Using the work of the internal audit function** — the external auditor evaluates the function and then uses specific work the function has performed.
- **Using internal auditors to provide direct assistance** — the external auditor uses internal auditors as members of the audit team, under the external auditor's direction, supervision, and review. (Some jurisdictions restrict or prohibit direct assistance; the PCAOB rules for US public-company audits differ — see below.)

### Prerequisites the external auditor evaluates

Before using the work of the internal audit function, ISA 610 requires the external auditor to evaluate:

- The function's **objectivity** — organisational status; policies safeguarding objectivity from bias, conflict of interest, undue influence.
- The function's **competence** — resources, training, professional qualifications, experience.
- The function's **systematic and disciplined approach** — documented methodologies, quality control, peer review.

If the function fails any of these, the external auditor cannot rely on its work.

### What the external auditor evaluates in specific work

Where the function passes the evaluation, the external auditor still evaluates the specific work the external auditor is proposing to use:

- The work was properly planned, performed, supervised, reviewed, and documented.
- Sufficient appropriate evidence was obtained to enable the function to draw reasonable conclusions.
- Conclusions drawn are appropriate.
- Reports issued by the function are consistent with the work performed.

### Where AI audit work matters for ISA 610

Financial-reporting-adjacent AI is where the internal AI function's work most directly affects the external auditor's engagement:

- **Models feeding financial statements.** Expected credit loss models (IFRS 9 / CECL under ASC 326), insurance reserving models, fair-value estimation models, revenue-recognition models with AI components, inventory-valuation models, impairment-testing models.
- **AI-driven internal controls over financial reporting.** AI used in SOX 404 / internal-control-over-financial-reporting (ICFR) processes — AI-assisted journal-entry review; AI-based reconciliation; AI-driven fraud detection; AI-enabled close activities.
- **AI governance of financial-reporting systems.** The AIMS or model-risk framework applied to financial-reporting models; approval and change management for these models.

The internal function's work on these areas is, if the function is objective, competent, and systematic, work the external auditor can rely on under ISA 610. The senior AI auditor's job is to make that work available in the shape the external auditor can efficiently use.

### Documentation the external auditor expects

- The function's scope and authority (audit charter).
- The function's methodology.
- The function's quality-assurance programme.
- Engagement workpapers (for the specific engagements being relied on).
- Findings slates and management responses.
- The function's status reports.

The external auditor will test the function's work (at the engagement level) with reperformance, inspection, and inquiry.

### Communication between internal and external

The external auditor communicates its planned reliance to the audit committee (`mod-111` chapter 5 on report shapes). The audit committee signs off. The internal function then formalises the coordination — joint planning meetings, shared risk-assessment inputs, agreed scope, timetable, and workpaper exchange.

## PCAOB AS 2605 — external auditor reliance in a PCAOB-regulated audit

### The standard

**PCAOB Auditing Standard AS 2605 (Consideration of the Internal Audit Function)** applies to audits of public companies (and certain other PCAOB-regulated engagements) in the US. It is similar in substance to ISA 610 but carries the PCAOB's inspection regime and specific restrictions.<!-- needs-research: confirm the current PCAOB standard number for consideration of internal auditors; the PCAOB renumbered standards and AS 2605 may be recited as "AS 2601" or similar in some materials. The Reorganization project assigned AS No. 65 to this content; practitioners reference it as AS 2605 following the 2015 reorganization. -->

### Differences from ISA 610

- **Direct assistance posture.** PCAOB rules are more restrictive on internal auditors providing direct assistance in certain areas, particularly internal-control-over-financial-reporting testing under AS 2201.
- **Documentation retention.** The external auditor's documentation is subject to PCAOB inspection; the internal function's cooperation is both expected and documented.
- **Communication to the audit committee.** Specific PCAOB rules on audit committee communication (AS 1301) define what must be communicated about reliance on internal audit.

### AI-audit-specific implications

- For PCAOB-regulated issuers, the external auditor's reliance on internal AI audit work for ICFR purposes flows through AS 2201 (The Audit of Internal Control Over Financial Reporting That Is Integrated With An Audit of Financial Statements).
- The internal function's testing of AI controls over financial reporting must meet the external auditor's reliance criteria — the senior internal AI auditor designs the engagement with the external auditor's reliance in mind.
- PCAOB inspection teams may inspect the external auditor's reliance decision; the internal function's work can become visible in that inspection record.

## IIA alignment — the function's own posture for external reliance

The IIA Global Internal Audit Standards address external-auditor coordination:

- The CAE communicates with the external auditor to coordinate work.
- The internal function makes its workpapers available where appropriate.
- The function does not surrender independence or integrity to accommodate the external auditor's convenience.<!-- needs-research: cite the exact IIA Standard governing coordination with external auditors at reading time; prior Standard 2050 covered this and has been consolidated into the Global Standards. -->

The CAE's annual plan reflects the planned external-auditor coordination. The audit committee reviews the plan.

## Coordination with notified bodies

### The notified body's authority

Notified bodies are designated by EU Member State designation authorities to perform third-party conformity assessments under EU regulations. Under the AI Act, notified bodies perform Annex VII (quality-management-system-based) conformity assessment for specified high-risk systems (`mod-110`).

### The audit interface

Unlike financial audit reliance, notified-body coordination is not primarily about one body relying on another's work. The notified body conducts its own audit under its designation. The internal AI audit function:

- Provides the notified body with the technical documentation (Annex IV) and quality-management-system evidence the notified body requires.
- Prepares management for the notified body's audit interviews and observations.
- Does not substitute for the notified body's own testing but may support it where the notified body accepts internal audit work as evidence of operating effectiveness under its scheme.
- Tracks notified-body findings in parallel to internal findings (see chapter 5 on regulator-finding registers).

### Ongoing surveillance

Notified bodies perform surveillance audits on cycle (typically annual). The internal function:

- Remediates prior notified-body findings before the surveillance audit.
- Maintains the operating evidence the notified body will inspect.
- Produces the continuous-audit output (chapter 2) relevant to the notified body's scope.

### Scope boundaries

Notified bodies operate strictly within their designation. The notified body does not audit systems or processes outside the scheme — the internal function's work may cover much broader scope. The internal function keeps the scope mapping explicit so neither party operates outside its authority.

## Coordination with ISO/IEC 17021-1 certification bodies

### The certification body's authority

Certification bodies accredited under ISO/IEC 17021-1 (and the scheme-specific requirements, including ISO/IEC 42006 for AIMS certification) audit management systems. For AIMS, the certification-body audit produces the ISO/IEC 42001 certification.<!-- needs-research: confirm ISO/IEC 42006's publication status at reading time; scheme-specific requirements for AIMS certification are in standardisation. -->

### The audit interface

- **Stage 1 (readiness review).** The certification body reviews documentation, often remotely, and identifies gaps.
- **Stage 2 (initial certification audit).** On-site audit of the AIMS in operation.
- **Surveillance audits** (typically annually).
- **Recertification** (typically every three years).

The internal AI audit function's role:

- Prepares the AIMS evidence the certification body will inspect.
- Conducts internal AIMS audits on cycle (ISO/IEC 42001 §9.2); the certification body reviews the internal audit records.
- Supports management's engagement with the certification body during audits.
- Does not act as the certification auditor — a function that is the internal auditor and the certification auditor is in a scheme-specific conflict.

### Certification-body reliance on internal audit

Certification bodies may consider internal audit evidence when planning their surveillance audits. ISO/IEC 17021-1 limits how much reliance is appropriate — the certification body must perform enough independent sampling to conclude on conformity. Internal audit work supports but does not substitute for certification-body testing.

### Accreditation body oversight

Certification bodies are themselves audited by national accreditation bodies (ANAB, UKAS, DAkkS, and others) that are members of the IAF. Accreditation-body witness audits observe certification-body auditors in action. The internal function is sometimes observed during these witness audits.

## Coordination with SOC auditors (SSAE 18 / ISAE 3402 / SOC 2)

### The standards

**AICPA attestation standards (SSAE 18)** and the **IAASB's ISAE 3402** govern service organisation control reports. **SOC 1 (ICFR-adjacent)**, **SOC 2 (Trust Services Criteria — security, availability, processing integrity, confidentiality, privacy)**, and **SOC 3 (public summary)** are the common report types.

### Where SOC meets AI audit

- **AI service providers** issue SOC 2 Type II reports to customers. The audit function's AI-specific evidence (eval records, model governance, incident handling, monitoring) supports the SOC audit of the service.
- **Entities using AI service providers** rely on vendor SOC reports in their own third-party risk management (`mod-109`).
- **Internal AI controls** in SOC-audited organisations — AI controls over financial reporting fall into SOC 1 scope; AI controls over customer data confidentiality and processing integrity fall into SOC 2 scope.

### SOC auditor reliance on internal audit

SOC auditors (CPA firms under SSAE 18) may use the work of internal auditors under AT-C Section 105 reliance rules, broadly analogous to ISA 610. The internal AI function's work on operating effectiveness of AI controls can contribute to the SOC auditor's conclusion.

### SOC audit of AI service providers — a specific interface

A SOC 2 report on an AI service may incorporate AI-specific control areas:

- **AI change management** (controlled release of model and prompt changes).
- **AI evaluation** (pre-release accuracy, safety, fairness, security evaluations).
- **AI monitoring** (ongoing performance, drift, security).
- **AI incident handling** (detection, response, customer notification).
- **AI data handling** (training data provenance, customer data use, retention, deletion).

The internal audit function of the service provider helps design these controls and produces the operating evidence the SOC auditor tests.

## Coordination with IAAIS-designated auditors (ForHumanity Independent Audit of AI Systems)

### The scheme

The **Independent Audit of AI Systems (IAAIS)** scheme, developed by ForHumanity and partners, offers a specific framework for independent third-party audits of AI systems. Audits produce a pass / conditional / fail outcome in the scheme's shape and are performed by auditors certified under the scheme.<!-- needs-research: confirm the current status, naming, and certification structure of IAAIS / ForHumanity's audit scheme at reading time; the scheme has evolved. -->

### The audit interface

- Scheme-designated auditors conduct the audit under the scheme's criteria.
- The internal audit function supports the engagement with evidence and preparation.
- Classifications are in the scheme's shape (see `mod-111` chapter 2); the internal function cross-references these to its own classification.

## Coordination with privacy and data-protection audit regimes

Where the AI system processes personal data, privacy auditors / DPO audits / DPA-directed audits may overlap with the AI audit:

- **GDPR Article 35 DPIAs** may be prepared or reviewed by the DPO; the AI audit function's impact-assessment work is adjacent and sometimes overlapping.
- **DPA audits** under national data-protection law may inspect AI-specific processing; the internal AI function's evidence supports.
- **Transfer-impact assessments** under GDPR Chapter V for AI involving cross-border transfers.

The AI audit function coordinates with the DPO and the data-protection function to avoid parallel or inconsistent work.

## Coordination with specialised safety and security auditors

For AI systems in safety-critical or security-critical domains, specialised auditors may be involved:

- **Functional-safety auditors** under ISO 26262 (automotive), IEC 61508 (industrial), IEC 62304 (medical device software), DO-178C (aviation).
- **Cybersecurity auditors** under ISO/IEC 27001 and various sector regimes (NERC CIP, PCI DSS, HIPAA Security Rule).
- **Nuclear / industrial safety** under sector-specific frameworks.

Coordination is bilateral: the AI audit function provides AI-specific evidence relevant to the safety or security audit; the specialised auditor provides safety / security findings relevant to the AI audit.

## Operating rhythm for coordination

The senior AI auditor sustains coordination with externals on a defined rhythm:

- **Annual coordination meeting** — with each primary external auditor; review prior year, discuss current year's plan, agree scope coordination.
- **Quarterly check-ins** — status, issues, upcoming engagements.
- **Pre-engagement coordination** — before an external engagement starts, formalise the work the internal function will produce and the reliance posture.
- **During-engagement coordination** — daily or weekly cadence during an active external engagement; a single named internal counterpart per external engagement.
- **Post-engagement debrief** — what worked; what the external auditor needed that was not available; how to shape the internal function's work differently next time.

## Common failure modes

- **Scope misalignment.** Internal and external auditors cover overlapping but non-identical scope; the external cannot rely because the internal's work does not quite fit, and the internal's findings do not quite match the external's.
- **Methodology mismatch.** The internal function's sampling methodology does not meet the external's reliance requirements.
- **Documentation gaps.** Internal workpapers are not in the shape the external auditor can efficiently review.
- **Objectivity concerns.** The internal function is organisationally positioned in a way that the external auditor cannot defend reliance (reporting line to management instead of the audit committee; secondments that compromise independence; the function is managed by the same executive whose area it audits).
- **Competence gaps.** The internal function does not have the technical specialists the external auditor's work requires.
- **Direct-assistance drift.** Internal auditors acting as direct assistance expand their role beyond what PCAOB / ISA 610 permit.
- **Multi-auditor conflicts.** Several externals (financial auditor, SOC auditor, notified body, certification body) impose inconsistent requirements on the internal function.
- **Confidentiality tension.** External auditors expect access to internal work papers that contain privileged material; counsel resolves.

## Audit committee's role in coordination

The audit committee:

- Approves the external auditor's planned reliance on internal audit.
- Receives separate reports from internal and external auditors so comparisons are possible.
- Resolves conflicts between internal and external views when they arise.
- Monitors the coordination quality as a function-level quality indicator.

## Summary

- Internal AI audit does not operate alone; external financial auditors, SOC auditors, ISO certification bodies, notified bodies, IAAIS-designated auditors, DPA auditors, and specialised safety / security auditors operate alongside.
- ISA 610 (and PCAOB AS 2605 for US public-company audits) governs external financial auditor reliance on internal audit: the external evaluates objectivity, competence, and systematic approach, and then evaluates specific work before relying; the senior AI auditor shapes the internal function's work to support defensible reliance.
- Financial-reporting-adjacent AI (expected credit loss, reserving, fair value, revenue, inventory, impairment, ICFR AI tooling) is where ISA 610 / AS 2605 reliance matters most.
- Notified bodies and certification bodies perform their own audits under their designation / accreditation; the internal function supports with evidence and preparation but does not substitute for the body's independent testing.
- SOC auditors use the internal function's work under AT-C 105 reliance rules; AI service providers' SOC 2 reports often incorporate AI-specific control areas (change management, evaluation, monitoring, incident handling, data handling) the internal function helps design and evidence.
- IAAIS and specialised privacy / safety / security auditors operate on their own scheme criteria; the internal AI function coordinates bilaterally.
- Coordination operates on a defined rhythm — annual coordination meeting, quarterly check-ins, pre-engagement scoping, during-engagement cadence, post-engagement debrief — with the audit committee approving and monitoring the overall coordination quality.
- Common failure modes (scope misalignment, methodology mismatch, documentation gaps, objectivity concerns, competence gaps, direct-assistance drift, multi-auditor conflicts, confidentiality tension) are the senior auditor's recurring work.
