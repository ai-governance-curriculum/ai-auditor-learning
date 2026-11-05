# FDA GMLP and PCCP — The Audit Path for AI/ML-Enabled SaMD

## Motivation

AI/ML software that meets the FDA definition of a **medical device** — software intended for use in the diagnosis of disease or other conditions, in the cure, mitigation, treatment, or prevention of disease, or intended to affect the structure or any function of the body — is regulated by the **FDA Center for Devices and Radiological Health (CDRH)**. Software that is itself a device is termed **Software as a Medical Device (SaMD)**; software included as an embedded component of a hardware device is **Software in a Medical Device (SiMD)**.

AI/ML in medical devices imports two complications the FDA regime addresses specifically:

- **Adaptivity.** Many ML models update on the basis of post-market data. Traditional device law conceives of a device as **locked** after clearance; a model that updates is, under the traditional interpretation, a new device needing a new submission. The FDA's **Predetermined Change Control Plan (PCCP)** mechanism — authorised by Section 3308 of the Food and Drug Omnibus Reform Act of 2022 (FDORA) and operationalised by the 2024 guidance — allows the manufacturer to pre-authorise a bounded envelope of changes without re-submission.
- **Quality system expectations specific to ML.** Traditional device quality-system regulations (21 CFR Part 820, replaced on effective date by the harmonised Quality Management System Regulation — QMSR — aligned to ISO 13485:2016) apply to AI/ML devices but do not natively address data-handling and model-training activities. The FDA's **Good Machine Learning Practice (GMLP) for Medical Device Development** guiding principles, published jointly with Health Canada and the UK MHRA (and now with a growing group of international regulators), fill the gap.

The auditor arrives here as an **internal auditor over the manufacturer's quality system**, as a **notified-body auditor under ISO 13485** (for EU MDR convergence; see chapter 9 for the EU route), as a **third-party auditor under FDA's Accredited Persons / 510(k) Third Party Review program** where applicable, or as **the sponsor-side quality and regulatory affairs auditor** preparing a submission for FDA review. This chapter is the auditor's shape across those positions: the GMLP principles as audit criteria, the PCCP adequacy test, the submission-pathway evidence (Q-Sub / 510(k) / De Novo / PMA), the QMSR / 21 CFR Part 820 integration, and the post-market reporting under 21 CFR Part 803.

## The submission pathway — pre-market context

Before the GMLP / PCCP audit shapes have meaning, the auditor must know the device's submission pathway.

- **Class I (low risk).** Mostly exempt from pre-market notification; general controls apply.
- **Class II (moderate risk).** Pre-market notification via **510(k)** — demonstrates substantial equivalence to a legally marketed predicate device. AI/ML SaMD frequently routes here, with specific FDA guidance on 510(k) for AI/ML.
- **Class III (high risk).** Pre-market approval (**PMA**) — demonstrates safety and effectiveness through valid scientific evidence.
- **De Novo.** Novel devices for which no predicate exists; ends with classification into Class I or II and establishment of special controls.
- **Breakthrough Devices.** Expedited path for devices addressing unmet medical needs; AI/ML devices often use it.
- **Pre-Submission (Q-Sub).** Pre-submission meeting with CDRH to align on submission content, PCCP scope, clinical-performance evidence; a strong Q-Sub record is audit-relevant because it shows the FDA's own view of the submission's shape.

For the auditor, the pathway fixes the specific submission's content expectations. A 510(k) submission requires a specific content set (21 CFR 807.87 and FDA's AI/ML-specific 510(k) content guidance); a De Novo submission requires a different content set; PCCP evidence has specific requirements layered on each pathway.

Audit-test shape: the submission dossier, the pre-submission record (Q-Sub minutes, FDA feedback), the Determination Letter (clearance, approval, grant), any post-decision correspondence.

## The GMLP guiding principles — audit criteria

The GMLP **10 guiding principles** (initially published October 2021 jointly with Health Canada and MHRA; the growing international alignment includes additional regulators) are the operational AI/ML quality criteria:

1. **Multi-disciplinary expertise is leveraged throughout the total product life cycle.** Clinical, engineering, data-science, regulatory, QA expertise integrated across requirements, design, validation, monitoring.
2. **Good software engineering and security practices are implemented.** Risk management, software life-cycle processes (IEC 62304), cybersecurity (FDA pre-market and post-market cybersecurity guidance), configuration management.
3. **Clinical study participants and data sets are representative of the intended patient population.** Managed differences across subgroups; representativeness over the deployment population.
4. **Training data sets are independent of test sets.** No leakage; proper separation of development data from the data used for performance evaluation.
5. **Selected reference datasets are based upon best available methods.** Gold-standard reference datasets; label quality; clinical validation.
6. **Model design is tailored to the available data and reflects the intended use of the device.** Appropriate architecture given data and task; acknowledged limitations.
7. **Focus is placed on the performance of the human–AI team.** Human factors; usability; clinician-AI interaction; workflow integration.
8. **Testing demonstrates device performance during clinically relevant conditions.** External validation; robustness to real-world variation.
9. **Users are provided with clear, essential information.** Labelling (indications, limitations, performance); user-facing transparency.
10. **Deployed models are monitored for performance and re-training risks are managed.** Post-market monitoring; change management; re-training risk.

<!-- needs-research: confirm the current count and wording of GMLP guiding principles at reading time; the FDA/HC/MHRA joint publication has been augmented with additional transparency and iteration principles, and additional regulators have joined the alignment -->

Audit-test shape: GMLP is **principles**, not prescribed procedures. The auditor converts each principle into a testable control for the specific device:

- Principle 3 becomes: "The device is validated on a test set whose subgroup distribution matches the intended-use population within a defined tolerance." The test is the population analysis, the subgroup-performance analysis, and the rationale when the match is imperfect.
- Principle 4 becomes: "The test set is held out before the development process began and no information from the test set has been used to tune the model." The test is the data-provenance trail and the data-management process.
- Principle 10 becomes: "Deployed-model performance is monitored with defined metrics, thresholds, and action procedures; re-training risk is managed under the PCCP or a change-control procedure." The test is the monitoring plan and its live execution.

## The PCCP — pre-authorised change envelope

The **Predetermined Change Control Plan** is the manufacturer's pre-submitted envelope of planned future changes. If the plan is adequate, FDA authorises the plan as part of the clearance, approval, or grant decision, and future changes within the plan can be implemented without a new submission.

### PCCP components

The FDA 2024 final guidance on PCCP (Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence/Machine Learning (AI/ML)-Enabled Device Software Functions) specifies three elements:

1. **Description of Modifications.** The specific planned changes — the modifications themselves — stated at a level a reviewer can bound. Examples: re-training on the same input distribution with new data up to a defined volume per period; expansion of indication to an additional patient subgroup pre-identified; algorithmic-threshold adjustment within a declared range.
2. **Modification Protocol.** The methods the manufacturer will follow to implement each described modification — the data management, re-training, re-verification, re-validation, update management, post-market monitoring that will be executed for each change. The protocol is the quality-system procedure for the modification.
3. **Impact Assessment.** The analysis of how modifications may impact the device's safety and effectiveness, benefits and risks, and conformity to specifications and intended use; justification for why the pre-authorised modifications do not require a new submission.

<!-- needs-research: confirm final structure and specific vocabulary from the 2024 PCCP guidance at reading time; the final guidance may have evolved content expectations in places -->

### Audit test for PCCP adequacy

The auditor's PCCP adequacy test:

- **Scope defensible.** The Description of Modifications is specific enough to be auditable — numeric bounds, declared populations, specified algorithmic parameters. A PCCP that allows "model re-training as determined by the manufacturer" is not adequate.
- **Protocol complete.** The Modification Protocol covers every change class in the Description; the protocol references the QMSR / Part 820 procedures the manufacturer will actually execute.
- **Impact assessment grounded.** Impact assessment names the risk categories and provides reasoning from each modification to residual risk on the device's safety and effectiveness. Blanket "no material impact" statements are inadequate.
- **Integration with quality system.** The PCCP cross-references the manufacturer's change-control procedure, design-control procedure, validation procedure, data-management procedure, and post-market surveillance procedure. The QMSR auditor can trace from a PCCP commitment to a QS procedure to evidence of execution.
- **Boundary to new submission.** The manufacturer's procedure describes when a change *exits* the PCCP envelope and *does* require a new submission; the auditor tests this boundary with concrete examples.

A PCCP that would, in effect, permit the manufacturer to replace the model with a different model with different performance is not a PCCP — it is an attempt to escape pre-market review.

### Changes outside the PCCP

Changes outside the PCCP envelope require the normal **change decision** per 21 CFR 807.81(a)(3) (for 510(k)-cleared devices) or equivalent for other pathways. FDA's guidance on "Deciding When to Submit a 510(k) for a Change to an Existing Device" (and its AI/ML-specific revisions) applies.

## The quality system — QMSR / 21 CFR Part 820 integration

AI/ML devices fall under the FDA's quality system requirements. **21 CFR Part 820** has been the controlling regulation for decades; the **QMSR final rule** (effective 2 February 2026) harmonises Part 820 with ISO 13485:2016 and renames it the Quality Management System Regulation. <!-- needs-research: confirm QMSR effective date and the alignment adjustments between the FDA amendments and ISO 13485:2016 at reading time -->

For AI/ML, the quality-system clauses the auditor most often tests:

- **Design controls** (820.30 / ISO 13485 clause 7.3). Design inputs (including user needs and intended use), design outputs (specifications), design reviews, design verification (does the design meet the inputs?), design validation (does the device work in the intended use?), design transfer to production, design history file (DHF).
- **Document controls** (820.40 / ISO 13485 clause 4.2).
- **Purchasing controls** (820.50 / ISO 13485 clause 7.4). Vendor evaluation; critical suppliers include foundation-model providers and labelling / annotation vendors in the AI book.
- **Identification and traceability** (820.60 / 820.65 / ISO 13485 clause 7.5.3).
- **Production and process controls** (820.70 / ISO 13485 clause 7.5.1). For software, includes model build and training procedures.
- **Corrective and preventive action — CAPA** (820.100 / ISO 13485 clause 8.5). Non-conformance, root cause, corrective action, effectiveness check; AI/ML drift observations are typical CAPA inputs.
- **Complaint handling** (820.198 / ISO 13485 clause 8.2.2).
- **Servicing** (820.200). Where applicable to the device class.

For AI/ML specifically, the auditor expects the quality system to address:

- **Data quality management.** Procedures for acquiring, annotating, managing, versioning training and test data; aligns to GMLP principles 3–5.
- **Model lifecycle procedures.** Procedures for model training, validation, release, deployment, monitoring, retirement; aligns to IEC 62304 software life-cycle processes with AI-specific additions.
- **Human factors / usability engineering.** IEC 62366 process executed for the human–AI team interaction; aligns to GMLP principle 7.
- **Software of unknown provenance (SOUP).** Open-source libraries, foundation models, and pre-trained components treated as SOUP under IEC 62304, with risk assessment and vendor evaluation.
- **Cybersecurity.** FDA pre-market cybersecurity guidance (Content of Premarket Submissions for Device Cybersecurity) and post-market cybersecurity guidance; threat model, security risk management, SBOM, vulnerability management, coordinated vulnerability disclosure.

## Post-market surveillance — 21 CFR Part 803 and Part 822

Post-market surveillance for devices has two tracks the auditor returns to:

- **Medical Device Reporting (MDR), 21 CFR Part 803.** Reportable events — deaths, serious injuries, malfunctions that could cause or contribute to a death or serious injury if the malfunction were to recur — reported to FDA within defined timeframes (5-day or 30-day depending on category). AI/ML systems can generate reportable events through mis-prediction, mis-classification, hallucination (for generative outputs in clinical contexts).
- **Postmarket Surveillance, 21 CFR Part 822.** Required post-market surveillance for certain Class II and III devices as ordered by FDA.
- **Corrections and Removals, 21 CFR Part 806.** Reports to FDA of corrections or removals of a device initiated to reduce a risk to health.

GMLP principle 10 extends into the post-market regime: deployed models are monitored for performance and re-training risks are managed. The auditor tests the manufacturer's post-market monitoring plan, its execution, and its interface with MDR and Part 806.

## The audit shape — pre-market vs. post-market

### Pre-market audit

The internal auditor or sponsor's quality/regulatory affairs auditor audits the **submission readiness**:

1. **Submission type correctly identified** (510(k), De Novo, PMA, Breakthrough; use of Q-Sub).
2. **Content complete** per the pathway-specific content requirements, including AI/ML-specific sections.
3. **GMLP evidence present** across the 10 principles.
4. **PCCP, if any, adequate** across the three components.
5. **Quality system operates** with design-controls, data-quality-management, model-lifecycle, cybersecurity, human-factors procedures evidenced.
6. **Clinical / performance evidence** meets the pathway's bar.

### Post-market audit

The internal auditor or FDA inspection analogue tests ongoing operation:

1. **Post-market monitoring operating** per plan; drift and performance findings routed through CAPA.
2. **PCCP execution within envelope** — modifications within PCCP are executed per protocol with documented evidence; modifications outside PCCP route to a new submission.
3. **MDR operating** — reportable events are reported within clock; non-reportable events still recorded; Part 806 corrections and removals handled.
4. **Quality system maintained** — CAPA, complaint handling, management review (quality system requires periodic management review of QS performance), training.
5. **Design history file and device master record current** — changes tracked, versions traceable, DMR reflects as-manufactured state.

## Interfaces with other audit shapes

- **ISO 13485 and MDR (EU Medical Device Regulation).** QMSR alignment makes a single ISO 13485 audit nearly sufficient for both FDA and MDR purposes; some differences remain (MDR adds specific post-market clinical follow-up expectations; FDA adds specific AI/ML submission content requirements).
- **EU AI Act (chapter 1).** An AI/ML SaMD on the EU market is subject to both MDR and the AI Act under Article 43(3) — sectoral integration — because medical devices are Annex I Section A regulated products. The notified-body MDR audit absorbs the AI-Act requirements rather than running them in parallel.
- **ISO 14971.** Risk management for medical devices. GMLP principles 2 and 10 integrate with 14971's post-market feedback mechanism.
- **ISO 42001 (`mod-105`).** Some manufacturers have added an AIMS under ISO 42001 even though QMSR / ISO 13485 is their core system; Annex D of 42001 references integration with 13485. The AIMS feeds AI-specific evidence into the QMSR audit.
- **SR 11-7 (chapter 5).** Where a healthcare organisation is also financially-regulated (payer with PBM activities subject to banking supervision; an insurance subsidiary), an AI model can face both FDA and SR 11-7 shaped governance.
- **HIPAA.** All of this interacts with HIPAA (not covered in this chapter) for PHI handling.

## Common failure modes

- **Scoping out of SaMD.** Software whose intended use places it within the device definition is scoped as "clinical decision support — software exempt" under the 21st Century Cures Act Section 3060 exemptions when it does not actually meet the exemption's four criteria; audit must apply the FDA's CDS guidance carefully.
- **Submission pathway wrong.** 510(k) attempted for a device with no suitable predicate; De Novo needed. The sponsor burns months.
- **GMLP evidence by assertion.** Dossier states "aligned with GMLP" without principle-by-principle evidence; audit does not reach the FDA's bar.
- **Data-set leakage.** Test set contaminated with training data; principle 4 violated; clinical performance metrics overstated. Discoverable at audit through data-provenance review.
- **Clinical evidence from the wrong population.** Performance validated on a dataset whose subgroup composition does not match the intended-use population; principle 3 violated.
- **PCCP as blanket authorisation.** Change plan too broad to bind the manufacturer; FDA rejects at submission.
- **PCCP without protocol detail.** Modification Protocol gestures at procedures without binding them to QS procedures; audit cannot trace modification execution to QS operation.
- **Drift observation without CAPA.** Post-market monitoring identifies performance degradation; no CAPA opened; QS requires CAPA for non-conformance.
- **MDR clock missed.** Reportable event identified; report sent after clock; Part 803 violation.
- **Vendor foundation model opaque.** Manufacturer uses a GPAI vendor model; vendor documentation inadequate; principle 6 (model design tailored to data and intended use) cannot be defended.
- **Cybersecurity SBOM absent.** FDA pre-market cybersecurity guidance expects an SBOM; some AI/ML submissions still arrive without one.
- **Human factors gap.** Principle 7 ignored; clinician override pattern not tested; usability problems emerge post-market.

## Summary

- AI/ML software meeting the device definition is regulated by FDA CDRH; submission pathways include 510(k), De Novo, PMA, Breakthrough, with Q-Sub pre-submission meetings; SaMD-specific AI/ML submission content expectations apply.
- GMLP guiding principles (jointly published by FDA, Health Canada, MHRA, with growing international alignment) are the AI/ML quality criteria the auditor converts into testable controls per principle for the specific device.
- PCCP under FDORA Section 3308 allows manufacturers to pre-authorise a bounded envelope of changes without new submissions, with three required components: Description of Modifications, Modification Protocol, Impact Assessment; audit tests adequacy of each and the boundary where changes exit the envelope.
- Quality system under QMSR (harmonising 21 CFR Part 820 with ISO 13485:2016, effective 2 February 2026) integrates GMLP into design controls, document controls, purchasing, production and process controls, CAPA, complaint handling; cybersecurity under FDA pre-market and post-market guidance; human factors under IEC 62366.
- Post-market surveillance through 21 CFR Part 803 MDR, Part 806 corrections and removals, Part 822 postmarket surveillance orders, plus GMLP principle 10's monitoring and re-training risk management.
- Interfaces with EU MDR (via QMSR / ISO 13485 alignment), EU AI Act (sectoral integration under Article 43(3)), ISO 14971 (device risk management), ISO 42001 AIMS (optional AI management-system overlay), SR 11-7 (where a healthcare organisation also faces financial supervision), and HIPAA (PHI handling).
- Common failure modes include scoping-out via mis-applied Cures Act exemptions, GMLP evidence by assertion, data-set leakage, PCCP as blanket authorisation, drift observation without CAPA, MDR clock missed, and cybersecurity SBOM absent.
