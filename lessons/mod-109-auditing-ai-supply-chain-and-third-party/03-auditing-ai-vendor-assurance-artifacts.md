# Auditing AI-Vendor Assurance Artifacts

## Motivation

Organisations rely on their AI vendors' third-party assurance artifacts — SOC 2 Type II reports, ISO/IEC 27001 certifications, ISO/IEC 42001 certifications, ForHumanity IAAIS reports, PCI DSS attestations of compliance, HITRUST CSF certifications, and emerging SOC 2 + AI reports — to short-circuit vendor diligence. The reasoning is reasonable: the vendor has been audited by an independent firm, the report is the audit evidence, the organisation inherits assurance. The reasoning is also incomplete. An assurance report is a *scoped assertion*: it asserts specific controls, at specific entities, over a specific period, with specific carve-outs, dependent on specific user-entity controls. The delta between what the report asserts and what the organisation needs is the audit's entire subject.

The common failure is to receive a report, verify it's current, file it, and record "SOC 2 Type II: present" in the vendor row. That is "paper reliance" — the auditor's third-party-risk cousin to "paper diligence" from chapter 2. SR 23-4 and ISO/IEC 42001 both expect something more: the organisation must assess whether the report actually covers the services the organisation consumes, whether carve-outs matter, whether user-entity controls are designed and operating, whether bridge letters cover the gap between the report period and today, and whether the vendor's assurance scope aligns with the AI system's actual risk footprint.

This chapter is the auditor's shape for reperforming the organisation's reliance. The deliverable is not an opinion on the vendor's auditor's work (the auditor is not re-auditing the vendor); the deliverable is an opinion on whether the organisation's reliance on the report is defensible for the use the organisation is making of the vendor.

## The assurance-artifact landscape

The auditor should expect to see a mix of the following, varying by vendor type and maturity:

- **SOC 2 Type II.** AICPA SSAE 18 Trust Services Criteria report — Security (mandatory), plus any of Availability, Processing Integrity, Confidentiality, Privacy. "Type II" = period of coverage (typically 6 or 12 months) with design-and-operating-effectiveness opinion. Independent CPA firm as service auditor. The most common vendor artefact.
- **SOC 2 + AI.** The AICPA has introduced additional AI-focused criteria and example controls intended to layer over SOC 2; some vendors publish SOC 2 reports with AI-specific controls integrated or as an addendum. <!-- needs-research: confirm the current AICPA guidance on SOC 2 + AI (TSP-section additions, AICPA-published trust services description for AI, or whatever the current branding is) at reading time -->
- **SOC 1 Type II.** Internal-control-over-financial-reporting report. Relevant for AI vendors whose services sit in the financial-reporting path (e.g., an AI-driven revenue-forecasting vendor consumed by a public company). Not common for most AI vendors.
- **SOC 3.** Public summary of SOC 2 — not an audit-grade artefact for reliance.
- **ISO/IEC 27001 certification.** Information-security-management-system certification. Statement of Applicability (SoA) and Annex A controls applied. Recertification every three years with surveillance in intervening years. Certificate + SoA are the artefact pair.
- **ISO/IEC 42001 certification.** AI management system certification (`mod-105` is the auditor's deep dive from the AIMS auditor side). Appearing on vendor-provided artifact walls as the AI-specific analogue to ISO 27001.
- **ISO/IEC 27701.** Privacy-information-management-system extension to 27001; relevant for vendors who process personal data at scale.
- **ForHumanity IAAIS (Independent Audit of AI Systems) report.** ForHumanity's audit-criteria framework for AI systems, applied by ForHumanity-trained auditors; publicly available as a criteria set. A ForHumanity report is an attestation against the IAAIS criteria at the audited scope. <!-- needs-research: confirm ForHumanity IAAIS criteria publication status and the current list of audited vendors that publish an IAAIS report at reading time -->
- **PCI DSS Report on Compliance (RoC) or Attestation of Compliance (AoC).** For AI vendors whose services touch cardholder data (rare but increasing — e.g., fraud-scoring vendors).
- **HITRUST CSF certification.** Healthcare-flavoured aggregation of multiple criteria sets (HIPAA, NIST CSF, ISO 27001, etc.); relevant for vendors whose services touch PHI.
- **CSA STAR (Security, Trust, Assurance & Risk).** Cloud Security Alliance's cloud-provider assurance programme; Level 1 self-assessment (low reliance), Level 2 third-party attestation (moderate reliance).
- **Vendor-authored security whitepapers and CAIQ (Consensus Assessments Initiative Questionnaire).** Vendor-asserted controls; not audit-grade but useful for scoping.
- **Pentest reports.** Vendor-commissioned pentest summary; useful for a specific control test.
- **AI-specific disclosures.** Model cards, system cards, safety-evaluation results, red-team reports — not audit artefacts, but often part of the vendor's assurance folder; see `mod-106` for auditing their content and chapter 1 for auditing their provenance.

The organisation does not need every artefact from every vendor. The chapter's premise is: for each artefact relied on, the auditor tests whether the reliance is defensible.

## Scope adequacy — the first test

The most common failure of assurance reliance is scope mismatch. The SOC 2 the vendor published covers the vendor's SaaS control plane but the organisation is consuming a vendor-operated inference endpoint whose infrastructure sits in a different cloud-provider region under a different operations team. The report is authentic; the reliance is misplaced.

The auditor's scope-adequacy test:

- **System description reperformance.** Every SOC 2 Type II report has a Section 3 (the "system description"), which the service auditor opines on in Section 2. The auditor reads Section 3 and asks: does this system description cover the services the organisation uses? Pin the specific product names, the specific regions, the specific infrastructure components. A SOC 2 covering "the Acme Inc. hosted inference platform in the US East region, excluding the Acme Research cluster used for model training" does not cover the organisation's reliance on Acme's EU-hosted inference for a European AI Act system.
- **Service boundary.** The description names the services in scope. Vendors often publish a SOC 2 for the general platform and operate sub-services outside the boundary (a model-evaluation service, a long-context endpoint, a fine-tuning service). The auditor confirms each service the organisation consumes falls inside the scoped boundary.
- **Trust Services Criteria (TSC) coverage.** The SOC 2 covers Security (always) plus a subset of Availability, Processing Integrity, Confidentiality, Privacy. The organisation's reliance must map to the included criteria. A vendor SOC 2 that covers only Security cannot be the basis for an availability-SLA claim.
- **ISO 27001 SoA alignment.** For ISO 27001-based reliance, the auditor reads the Statement of Applicability. Controls marked "not applicable" with a justification may still be relevant to the organisation's use; the auditor tests the justification.
- **ISO 42001 scope statement.** For ISO 42001 reliance, the vendor's certificate has a scope statement naming which AI activities and which AI systems are covered. A certificate whose scope is "chatbot development, EU-based deployments" does not necessarily cover the vendor's underlying foundation-model training operation.
- **PCI DSS merchant / service-provider level and scope.** PCI reliance requires the organisation to match its own card-data-environment (CDE) to the vendor's scoped CDE.
- **HITRUST certification level** (r2, i1, or e1, each with different depth) and the scoped boundary.
- **ForHumanity IAAIS scope.** IAAIS reports scope to the audited AI system, not to the vendor's whole business; the auditor identifies which system was audited and compares to the organisation's consumption.

The auditor's workpaper per artefact includes a *scope-vs-use delta* paragraph. Where the delta is non-trivial, the artefact is partially supporting the organisation's reliance — the auditor records the implications, including which parts of the organisation's inherent risk are *not* covered by the vendor's assurance.

## Carve-outs — the second test

Assurance reports frequently carve out — i.e., exclude — portions of the vendor's service that rely on subservice organisations. The SOC 2 convention offers two methods:

- **Carve-out method.** The subservice organisation's controls are excluded from the report; the report states which controls are the responsibility of the subservice; the organisation relying on the report must separately obtain assurance over the subservice (by reading *that* vendor's SOC 2, for example).
- **Inclusive method.** The subservice organisation's controls are included in the report; a single report covers both.

The carve-out method is overwhelmingly common. For AI vendors, the subservice organisations are usually (a) the underlying cloud provider (AWS / GCP / Azure), (b) specialist subservice providers (data-labelling vendors, moderation vendors, foundation-model providers in the case of wrapper SaaS), and (c) in some cases, the vendor's data-centre operator.

The auditor's carve-out test:

- **Identify every subservice carve-out.** Section 3 of the SOC 2 lists them. The auditor records each.
- **For each carve-out, the complementary subservice organisation controls (CSOCs).** The report specifies what controls the subservice is expected to perform. The organisation relying on the report must have evidence that the subservice performs them.
- **Chain of assurance.** Walk the carve-out to the subservice's own assurance artefact. A vendor relying on AWS for infrastructure must point the organisation at AWS's SOC 2 / ISO / PCI artefacts; the organisation relies on *those* for the carved-out controls.
- **Multi-hop carve-outs.** An AI vendor that uses OpenAI or Anthropic as a foundation-model subservice is relying on OpenAI's / Anthropic's own assurance posture. The organisation using the AI vendor is therefore two hops into the assurance chain. The auditor walks both hops.

Carve-out that goes unexamined is the single most common reliance defect the auditor will find. "AWS covers that" is not enough — the auditor writes a finding naming the specific CSOC, the specific carve-out, and the specific subservice assurance artefact (or its absence).

## Complementary user-entity controls (CUECs) — the third test

Every SOC 2 Type II and most ISO 27001 vendor engagements rely on **complementary user-entity controls** — controls the user (the organisation) must perform in order for the vendor's controls to achieve their objectives. The classic examples:

- Users will maintain appropriate authentication and access controls over their vendor accounts.
- Users will promptly notify the vendor of terminations of personnel who have vendor access.
- Users will configure vendor-provided controls (encryption options, retention options, access-review cadence) per their risk appetite.
- Users will monitor vendor logs made available to them.
- Users will train their personnel in acceptable use of the vendor's services.

For AI vendors specifically, additional CUECs the auditor should expect:

- **Users will configure the per-request training-opt-out flag where the vendor offers it.**
- **Users will not transmit regulated data (PHI, PCI, export-controlled, classified) outside a vendor-provided enclave product.**
- **Users will review moderation / safety-filter decisions and provide feedback via the vendor's feedback channel.**
- **Users will test vendor-provided model updates in non-production before promoting to production (where vendor offers staged rollouts).**
- **Users will not fine-tune using data that violates any applicable ToS / AUP (e.g., CSAM, PII of non-consenting individuals, copyrighted works without licence).**

The auditor's CUEC test:

- **Enumerate the CUECs.** Section 4 of the SOC 2 typically lists them; ISO 27001 vendor controls sometimes carry equivalent user responsibilities. Record all.
- **Design evaluation.** For each CUEC, does the organisation have a corresponding internal control? Named control, named owner, stated procedure. A CUEC with no corresponding internal control is a design-level finding.
- **Operating evaluation.** Sample evidence that the corresponding internal control actually operates. A vendor-logs-review CUEC paired with a "nobody reviews the vendor logs" reality is an operating finding.

A CUEC that the vendor's report flags but the organisation does not operate is a reliance defect as serious as a carve-out oversight. The vendor's assurance is predicated on the user doing something; the user is not doing it; the reliance fails.

## Bridge letters — the fourth test

A SOC 2 Type II covers a specific period in the past (say, July 2024 – June 2025). Today is November. The organisation is relying on the report for a vendor the organisation uses *today*. The gap between the report's "as of" date and the reliance date is the **bridge-letter** gap.

- **Bridge letter definition.** A short vendor-authored (sometimes vendor-and-service-auditor-authored) letter asserting that no material changes have occurred to the control environment between the end of the report period and the bridge-letter date.
- **Reliance limitation.** A bridge letter is vendor-authored, not independently examined. It is weaker evidence than a SOC 2 but is the standard interim artefact.
- **Coverage ceiling.** Bridge letters have a practical shelf life — a bridge letter dated six months after the report's end is still common but becoming stale; a year-old bridge letter without a new SOC 2 is a reliance defect because the vendor is clearly off its reporting cadence.

The auditor's bridge-letter test:

- **Request the bridge letter.** Vendor-provided; many vendors do not provide one until asked.
- **Confirm it covers the current reliance period.** The letter must bridge from the report's end to a date ≥ the current audit period's start. A bridge letter dated two quarters ago leaves a two-quarter gap the auditor must note.
- **Confirm the letter's signatory.** Vendor executive; sometimes the service auditor adds a non-opinion acknowledgement. Signatory authority matters.
- **Changes disclosed.** Any material changes the letter discloses must be assessed — a disclosed change (new subprocessor, new region, incident) may warrant enhanced monitoring in the interim.
- **Interim SOC 2.** If the vendor is on a 6-month SOC 2 cadence, a second report covering H2 may already exist; the auditor prefers the interim report to the bridge letter.

A vendor who refuses to produce a bridge letter is a monitoring finding (the vendor's communications hygiene is poor) and a reliance finding (the organisation has no bridge).

## The scope-vs-risk-footprint delta

The deepest test in this chapter is the **scope-vs-risk-footprint delta**. The vendor's assurance scope was designed by the vendor for the vendor's use cases. The organisation's AI system has a *risk footprint* — the harms it could produce, the regulatory obligations it carries, the data classes it touches, the autonomy it exercises. The question is: does the vendor's assurance scope actually cover the organisation's risk footprint, or merely coincide at a few points?

The auditor's test is structured as a matrix. On one axis: the elements of the organisation's AI system's risk footprint — data classes (PII, PHI, PCI, confidential business data, regulated content), harm vectors (fairness, privacy, safety, security, misinformation, IP infringement), regulatory obligations (EU AI Act, HIPAA, GLBA, SOX, state AI laws), operational dependencies (availability, performance, change-management). On the other axis: the controls the vendor's assurance covers.

For each row the auditor assesses whether the vendor's controls address the organisation's need, address it partially, or fail to address it. Cells with "fail" or "partial" are findings or at least residual-risk items the organisation must accept (and reflect in its risk register).

Illustrative gaps:

- **Fairness.** Most vendor SOC 2 reports say nothing about fairness. Reliance on a SOC 2 for a fairness-sensitive use is a false reliance. The organisation needs other evidence (vendor's own evaluation, the organisation's own testing).
- **Jailbreak / prompt-injection robustness.** Most vendor SOC 2 reports say nothing. ISO 42001 touches it via clauses on performance evaluation. Vendor red-team summaries help but are not audit-grade.
- **Training-data provenance.** Most vendor SOC 2 reports say nothing. ISO 42001 may touch it; the vendor's model-card and datasheet (chapter 1) are the actual evidence.
- **Serious-incident reporting (EU AI Act Article 73).** Vendor SOC 2 reports cover security-incident notification generically; they do not necessarily cover AI-specific serious-incident notification on the organisation's EU AI Act clock.
- **Specific use-prohibition compliance.** Vendor assurance rarely attests to "we do not use this service for EU AI Act Article 5 prohibited practices" — that is the organisation's responsibility.

The matrix is the auditor's clearest demonstration that "the vendor has a SOC 2" is not a sufficient reliance claim. The deliverable visibly shows the uncovered footprint and prompts the organisation either to source additional assurance (SOC 2 + AI, ISO 42001, IAAIS, or a vendor-specific attestation) or to accept and track the residual risk in its own register.

## Per-artefact deep-dives

### SOC 2 Type II — practitioner notes

- **Section 2 (service auditor's opinion).** Unqualified / qualified / adverse / disclaimer. Qualified and worse opinions are red flags; the auditor reads the basis for qualification.
- **Section 3 (system description).** Where the scope is written. The auditor reads it closely. A system description that omits the specific service the organisation uses is a scope defect even if the broader SOC 2 looks fine.
- **Section 4 (controls and tests).** Each control has a test-of-operating-effectiveness result; the auditor reads the exceptions. Exceptions that touch the organisation's reliance are concerns; exceptions concentrated in a specific control family (e.g., access review) are concerns.
- **Section 5 (other information, if provided).** Management responses to exceptions; the auditor reads them to understand remediation posture.

### ISO/IEC 27001 — practitioner notes

- **Certificate validity and accreditation.** The certifying body must be IAF/MLA-accredited. A certificate from a non-accredited body is lower-value.
- **Scope statement.** On the certificate face; sometimes elaborated in the SoA.
- **Statement of Applicability (SoA).** Which of Annex A controls are applied, which are excluded with justification. The auditor reads for AI-relevant controls — information-classification, cryptographic controls, secure development, supplier management, change management, incident management.
- **Surveillance-audit results.** ISO certification is a three-year cycle with annual surveillance. The organisation should obtain evidence of the most recent surveillance — if the vendor does not share the surveillance letter, record a monitoring finding.

### ISO/IEC 42001 — practitioner notes

- **Certification body accreditation.** ISO 42001 is young; not all certification bodies are yet accredited to issue it. The auditor checks the accreditation status of the body named on the certificate.
- **Scope statement.** As with ISO 27001, the scope statement on the certificate must match the organisation's reliance. An ISO 42001 scoped to "development of the Acme chatbot" does not cover "the Acme fine-tuning API" unless explicitly included.
- **Statement of Applicability for Annex A (ISO 42001 Annex A).** ISO/IEC 42001's own annexed control catalogue. The auditor reads for the controls that bear on the organisation's reliance — AI impact assessment, data governance, system lifecycle, third-party management of the vendor's own vendors.
- **Interaction with ISO/IEC 42005** (AI system impact assessment) and **ISO/IEC 23894** (AI risk management). Mature vendors cross-reference these.

### ForHumanity IAAIS — practitioner notes

- **Published criteria.** ForHumanity publishes its audit criteria openly; the auditor reads the criteria set applied, as the IAAIS brand covers multiple criteria modules (EU AI Act, children's rights, biometrics, etc.).
- **Scope.** An IAAIS report is scoped to a specific AI system or deployment; reliance for other systems is not supported.
- **Auditor identity.** The attesting auditor is a ForHumanity-trained individual or firm; the auditor verifies independence and competency.

### PCI DSS — practitioner notes

- **AoC vs. RoC.** The Attestation of Compliance is the shareable summary; the Report on Compliance is the detailed artefact. Many vendors share only the AoC, which is adequate for most reliance.
- **Service-provider level.** PCI DSS classifies service providers by transaction volume; the level determines the depth of assessment.
- **Validity.** PCI DSS assessments are annual; an AoC more than a year old is expired.

### HITRUST CSF — practitioner notes

- **Certification level (r2, i1, e1).** r2 is the high-assurance certification; i1 and e1 are intermediate / entry tiers.
- **Scope statement and in-scope criteria.** HITRUST maps to multiple frameworks (HIPAA, NIST CSF, ISO, PCI). The organisation must identify which mapped criteria matter for its reliance.
- **Validity.** Typically 24 months for r2 with an interim assessment at month 12.

## The vendor-assurance workpaper

The deliverable per sampled vendor is an assurance-reliance workpaper:

- **Artefacts list.** Every artefact the organisation holds for this vendor, with retrieval date, SHA hash, and the file-store reference.
- **Scope-vs-use delta per artefact.** One paragraph each.
- **Carve-outs table.** Per artefact, every carve-out with the CSOC and the subservice-assurance pointer.
- **CUECs table.** Per artefact, every CUEC with the corresponding internal control (or its absence) and the operating evidence.
- **Bridge-letter status.** Per artefact with a Type II shape, the bridge-letter status.
- **Scope-vs-risk-footprint matrix.** The deep matrix at the chapter's core.
- **Exceptions noted in the vendor's report.** Each material exception, with the organisation's assessment of impact.
- **Findings register.** Rows for each reliance defect, with the specific criterion (SR 23-4 phase, ISO 42001 clause, internal-policy clause) cited.

## Common failure modes

- **"The vendor has a SOC 2" without reading the SOC 2.** The classic reliance defect.
- **Scope ignored.** The report's scope does not cover the service the organisation consumes.
- **Carve-outs invisible.** The report says AWS is a subservice; nobody has pulled AWS's assurance.
- **CUECs unperformed.** Vendor's assurance depends on user controls the user does not operate.
- **Bridge letter missing or stale.** No coverage from the report's end to today.
- **Expired certifications.** ISO 27001 certificate from a lapsed cycle; PCI AoC past 12 months.
- **Accreditation-weak bodies.** Certificate from a non-IAF/MLA-accredited body.
- **Risk-footprint mismatch unexamined.** The organisation is relying on a SOC 2 for a risk the SOC 2 does not cover.
- **Reliance stated but not reperformed by anyone.** The vendor-risk team filed the artefact; no second line, no internal audit, no procurement has ever read it with this testing lens.
- **AI-specific attestations not sought.** The organisation accepts a generic SOC 2 and does not ask for SOC 2 + AI, ISO 42001, or IAAIS even where the vendor offers them.

## Summary

- Assurance-artifact reliance is a scoped assertion; the auditor tests scope, carve-outs, CUECs, bridge-letter coverage, and scope-vs-risk-footprint delta — not merely the artefact's presence.
- The scope test reads the system-description section and compares to the organisation's actual use; non-trivial deltas narrow the reliance.
- Carve-outs chain the assurance to subservice organisations (often cloud providers, sometimes foundation-model providers); the auditor walks the chain, confirming each CSOC has a corresponding subservice artefact.
- CUECs are user-side controls the vendor's assurance depends on; a CUEC without a matching internal control that operates is a reliance defect.
- Bridge letters cover the gap between the report's as-of date and the reliance period; the auditor demands them and accepts limited reliance when they are stale.
- The scope-vs-risk-footprint matrix is the deepest test — the vendor's scope was designed for the vendor's use cases, and uncovered rows must be either sourced from other assurance or accepted as residual risk in the organisation's register.
- Per-artefact practitioner notes (SOC 2, ISO 27001, ISO 42001, ForHumanity IAAIS, PCI DSS, HITRUST CSF) give the chapter-specific reading pattern for each report type.
- Chapter 2 is the upstream shape (SR 23-4 vendor lifecycle); chapter 5 is the GPAI-provider documentation overlay; chapter 7 is the US-federal-agency overlay.
