# EU AI Act Articles 43 and 44 — Notified-Body Conformity Assessment

## Motivation

The EU AI Act (Regulation (EU) 2024/1689) is the first horizontal product-safety regulation for AI. For a **high-risk AI system** under Article 6 and Annex III — biometric identification, safety components in critical infrastructure, education, employment, essential services, law enforcement, migration, administration of justice and democratic processes — placing the system on the EU market requires a **conformity assessment** before the CE marking is affixed. The assessment can be internal (Annex VI) or third-party by a **notified body** (Annex VII), and for several categories a notified-body assessment is mandatory.

The auditor arrives in this lane as a notified-body auditor or as a consultant preparing a provider for one. The shape is unlike an ISO 42001 certification: the subject matter is a **product** (the AI system), the criteria are **essential requirements** encoded in Chapter III Section 2 of the Act, the evidence shape is the **technical documentation** of Annex IV plus the **quality management system** of Article 17, and the output is a **CE-marking decision** that attaches liability under EU product-safety law.

This chapter is the auditor's shape for executing an Article 43 or 44 conformity assessment: the lane selection (internal vs. third-party; Annex VI vs. Annex VII), the essential-requirements test (Articles 9 through 15), the quality-management test (Article 17), the technical-documentation test (Annex IV), and the surveillance-and-re-assessment regime after the certificate issues. The chapters in `mod-105` cover the horizontal ISO 42001 management-system audit; this chapter sits beside it, covering the EU-AI-Act *product-conformity* audit.

## The conformity-assessment lanes

Article 43 governs conformity assessment for Annex III high-risk AI systems. Article 44 governs the special case of **Annex III point 1** (biometrics), and Article 40 feeds both through the **presumption of conformity** that arises when the provider follows a harmonised standard published in the Official Journal.

### Internal control — Annex VI

For most Annex III high-risk systems *other than* those covered by sectoral regulation listed in Annex I Section A (which routes through the sectoral assessment regime), the provider may self-attest through the **internal-control procedure of Annex VI**. The provider verifies that its quality-management system meets Article 17, that the technical documentation meets Annex IV, and that the system has been designed and developed in conformity with Chapter III Section 2. The provider signs the **EU declaration of conformity** per Article 47 and affixes the **CE marking** per Article 48.

The notified body does not enter. The auditor arriving at an Annex VI provider is therefore either an internal-audit function, a pre-market readiness consultant, or the provider's attestation auditor — not a notified-body auditor. The evidence shape still follows Annex IV and Articles 9–17; the decision shape is the provider's declaration, not a certificate.

### Third-party by a notified body — Annex VII

For Annex III point 1 systems (biometric identification and categorisation of natural persons; real-time or post remote biometric identification) **and** for any Annex III high-risk system where the provider has *not* applied the harmonised standards (or applied them only in part), Article 43 requires the **Annex VII** procedure — assessment of the quality management system and assessment of the technical documentation by a notified body.

The notified body is designated under Article 28 and operates under the horizontal **Regulation (EU) 2019/1020** on market surveillance and compliance of products, and under its designation requirements from Article 31 of the AI Act. Its audit output is a **Union technical documentation assessment certificate** (Annex VII point 4.6) valid for up to four years, plus ongoing surveillance under point 5.

### Sectoral products — Annex I Section A

If the AI system is a safety component of a product already regulated by a listed Union harmonisation legislation (machinery, toys, radio equipment, lifts, pressure equipment, medical devices under MDR / IVDR, in-vitro diagnostics, personal protective equipment, recreational craft, cableways, appliances burning gaseous fuels), the AI Act's conformity assessment is **integrated into the existing sectoral conformity assessment** under Article 43(3). The sectoral notified body audits against the sectoral directive *and* the AI Act essential requirements as part of the same decision.

The auditor's lane-selection workpaper must resolve this first. Getting the lane wrong means the audit output does not correspond to a conformity-assessment decision the market surveillance authority will accept.

## The essential-requirements criteria — Chapter III Section 2

The substantive audit criteria are Articles 8 through 15, read in combination with the recitals and the harmonised standards referenced in the Official Journal. The auditor reads each article as a control objective, and tests the provider's implementation as a control.

### Article 9 — Risk management system

A **continuous, iterative risk-management process** running across the entire life cycle of the high-risk AI system. Specifically required: identification and analysis of known and *reasonably foreseeable* risks to health, safety, and fundamental rights; estimation and evaluation of those risks under the system's intended purpose and reasonably foreseeable misuse; evaluation of residual risks against risk-acceptance criteria; adoption of targeted risk-management measures (design, mitigation, residual-risk disclosure to the deployer, training information).

Auditor's test shape: the risk-management procedure document (does it cover identification through residual-risk acceptance?); the live risk register (does every identified risk have an owner, a status, a treatment, and a residual-risk score?); the mapping from risk entries to concrete design decisions (does the mitigation that the register names actually appear in the system's build, and is it tested?); the change-driven re-entry (does a model update, data-pipeline change, or deployed-context change trigger re-running the process?).

The auditor's Article 9 workpaper is organised around **traceability** — every residual risk in the Annex IV technical documentation must trace to an entry in the live risk register and to at least one mitigation that is verified elsewhere in the dossier (Article 10 data governance, Article 14 human-oversight design, Article 15 accuracy/robustness/cybersecurity).

### Article 10 — Data governance

Training, validation, and test datasets must be subject to **data-governance and management practices**: design choices for data collection; data preparation (annotation, labelling, cleaning, aggregation); examination of possible biases that are likely to affect health and safety or lead to discrimination; appropriate measures to detect, prevent, and mitigate those biases; identification of data gaps or shortcomings and how they are addressed; representativeness, correctness, completeness, and statistical properties; data processing allowed under Article 10(5) for bias-detection purposes.

Auditor's test shape: the data-governance procedure; the datasheet for each dataset used (training / validation / test / fine-tune / RLHF / red-team); the bias-examination report (was it performed; against which protected attributes; with what methodology; what residual bias exists; which mitigation was applied); data-provenance evidence (consents, licences, provenance chains); the Article 10(5) legitimate-basis file if the provider processed special-category data for bias testing.

The auditor's Article 10 workpaper interfaces with `mod-104` evidence-reliability work and with `mod-106` model-card-claim auditing; the bias-examination report in particular must be independently assessable (methodology stated, data accessible, results reproducible) — not just signed off by the provider's own team.

### Article 11 and Annex IV — Technical documentation

The provider maintains technical documentation demonstrating compliance **before the system is placed on the market**, kept up to date through the life cycle. Annex IV enumerates the documentation set:

1. General description of the AI system (intended purpose, name and version, provider identity, how the system interacts or can interact with hardware or software not part of the system itself, software/firmware versions, forms in which the system is placed on the market or put into service, description of the hardware on which the system is intended to run, representations of the user-interface, instructions for use for the deployer).
2. Detailed description of the elements and processes for development (methods and steps for development, including pre-trained systems or tools used; design specifications of the system and the rationale and assumptions; description of system architecture including external resources and components; data requirements and provenance and cleaning; validation and testing procedures; cybersecurity measures).
3. Information on monitoring, functioning, and control of the AI system (capabilities and limitations in performance, levels of accuracy for specific persons or groups, overall expected level of accuracy in relation to intended purpose, foreseeable unintended outcomes and sources of risks, human-oversight measures adopted, specifications of input data as appropriate).
4. Description of the appropriateness of the performance metrics.
5. Detailed description of the risk management system per Article 9.
6. Description of relevant changes made by the provider to the system through its life cycle.
7. List of harmonised standards applied in full or in part; where harmonised standards not applied, description of solutions adopted to meet the requirements set out in Chapter III Section 2.
8. Copy of the EU declaration of conformity (Article 47).
9. Detailed description of the system in place to evaluate the AI system performance in the post-market phase (post-market monitoring plan, Article 72).

<!-- needs-research: confirm final numbering of Annex IV sub-points against the Official Journal text at reading time; the Act's trilogue and corrigendum cycle have moved sub-point granularity -->

Auditor's test shape: Annex IV is a checklist, and the auditor walks it top-to-bottom, making a workpaper row per sub-point with the dossier evidence pointer, completeness assessment (complete / partial / absent), and reviewer sign-off. For Annex VII engagements, this walk is the heart of the **technical-documentation assessment** by the notified body.

### Article 12 — Record-keeping (logging)

The high-risk AI system shall technically allow for the **automatic recording of events (logs)** over the life cycle of the system. The logs must enable the identification of situations that may result in the system presenting a risk within the meaning of Article 79 or in a substantial modification. For the biometric categories of Annex III point 1(a), minimum logging requirements are specified (period of each use, reference database, input data for which the search has led to a match, identification of the natural persons involved in the verification of the results).

Auditor's test shape: logging architecture (what is logged, with what granularity, retained for how long, with what integrity protection); correspondence between logs and the deployer-facing evidence the Act requires (Article 26 deployer obligations under the Article 12 logs); an evidence-sample reperformance (pick an incident, request the logs, confirm the logs would support a competent authority request under Article 20).

### Article 13 — Transparency and information to deployers

High-risk systems must be accompanied by **instructions for use** in digital or paper form, including: the identity and contact details of the provider; characteristics, capabilities, and limitations of performance (including intended purpose, level of accuracy including metrics, known or foreseeable circumstances that may lead to risks to health, safety, fundamental rights, performance regarding specific persons or groups, specifications for input data and training data when appropriate, information to enable deployers to interpret output); any known or foreseeable circumstances related to the use of the high-risk AI system in accordance with its intended purpose or under reasonably foreseeable misuse that may lead to the risks referenced; technical capabilities and characteristics to provide information relevant to explain the output; performance regarding specific persons or groups on which the system is intended to be used; specifications for input data as appropriate; where applicable, information to enable interpretation of output; where applicable, the changes to the system and its performance predetermined by the provider; human-oversight measures per Article 14; computational and hardware resources needed, expected lifetime of the system, maintenance and care measures; description of mechanisms included within the system allowing deployers to properly collect, store, and interpret logs per Article 12.

Auditor's test shape: the instructions-for-use document (does it include every element above, each testable against the system's observed behaviour?); the per-group performance disclosure (is it specific enough to be useful?); the limitation-disclosure (does it name the reasonably-foreseeable-misuse paths?); the computational-resources section (does it match the provider's internal benchmarks?). The auditor tests whether a **deployer could discharge Article 26 obligations using only the instructions-for-use plus the system itself** — if the deployer would have to call the provider to meet Article 26, Article 13 is not satisfied.

### Article 14 — Human oversight

The high-risk AI system shall be designed and developed in such a way, including with appropriate human-machine interface tools, that it can be **effectively overseen by natural persons** during the period in which it is in use. The human-oversight measures shall be commensurate to the risks, level of autonomy, and context of use of the AI system. The provider shall ensure that oversight persons can understand the relevant capacities and limitations of the system, remain aware of automation bias, correctly interpret the system's output, decide not to use or disregard the system, and intervene in the operation or interrupt the system.

For Annex III point 1(a) systems (remote biometric identification), the Act adds specific "two independent persons" verification requirements where applicable.

Auditor's test shape: the human-oversight design document (what interface elements enable each of the enumerated capabilities?); automation-bias mitigation (training materials for the oversight person; UI patterns that counter automation bias; evidence the oversight person can actually override, including latency of the override); for biometric categories, the independent-two-person verification path and its logs. The auditor's Article 14 test reaches into `mod-108` human-oversight evidence auditing and `mod-107` harm-model auditing.

### Article 15 — Accuracy, robustness, and cybersecurity

High-risk AI systems shall be designed and developed to achieve, in the light of their intended purpose, an appropriate level of **accuracy, robustness, and cybersecurity**, and to perform consistently in those respects throughout their life cycle.

- **Accuracy.** The levels of accuracy and relevant accuracy metrics shall be declared in the instructions for use (Article 13).
- **Robustness.** Technical and organisational measures to ensure the system is as **resilient as possible** regarding errors, faults, and inconsistencies that may occur within the system or the environment in which the system operates, including in relation to interactions with natural persons or other systems. Redundancy solutions (backup and fail-safe plans) may be part of this. For systems that continue to learn after being placed on the market, feedback loops that could lead to **biased outputs** must be addressed.
- **Cybersecurity.** The system shall be **resilient against attempts** by unauthorised third parties to alter use, outputs, or performance by exploiting vulnerabilities. Measures to prevent, detect, respond to, resolve, and control attacks shall address AI-specific vulnerabilities including **data poisoning**, **model poisoning**, **model evasion (adversarial examples)**, **confidentiality attacks** (membership inference, model extraction), and **flaws** in the physical infrastructure.

Auditor's test shape: for accuracy, the eval-set methodology (is the test set truly held out; is the metric appropriate to the intended purpose; are the per-group metrics declared; is the expected operational performance bounded by a plausible confidence interval?). For robustness, the robustness-test battery (OOD, perturbation, noise, operational-stress) with evidence. For cybersecurity, the AI-specific threat model (STRIDE / ATLAS / OWASP ML Top 10) mapped to tested controls; evidence of red-team activity covering the AI-specific categories; incident-response evidence.

### Article 16 — Provider obligations (overview)

Article 16 names the provider's obligations in combination: Article 17 QMS, Article 18 record-keeping of logs received under Article 20, Article 19 automatically generated logs, Article 20 corrective action and information duty, Article 21 cooperation with competent authorities, Article 48 CE marking. The Article 43 conformity assessment covers Article 16 through the lens of Articles 9–15 plus Article 17.

### Article 17 — Quality management system

The provider shall put in place a **quality-management system** that ensures compliance with the Regulation. The QMS shall be documented in a systematic and orderly manner in the form of written policies, procedures, and instructions, and shall include at least the following aspects:

- a strategy for regulatory compliance, including compliance with conformity-assessment procedures and procedures for the management of modifications to the high-risk AI system;
- techniques, procedures, and systematic actions for the design, design control, and design verification of the high-risk AI system;
- techniques, procedures, and systematic actions for the development, quality control, and quality assurance of the high-risk AI system;
- examination, test, and validation procedures to be carried out before, during, and after the development of the high-risk AI system, and the frequency with which they have to be carried out;
- technical specifications, including standards, to be applied and, where relevant to those standards, the solutions to be adopted to ensure that the high-risk AI system complies with the requirements set out in Chapter III Section 2;
- systems and procedures for data management, including data acquisition, data collection, data analysis, data labelling, data storage, data filtration, data mining, data aggregation, data retention, and any other operation regarding the data that is performed before and for the purpose of the placing on the market or putting into service of high-risk AI systems;
- the risk management system (Article 9);
- the setting up, implementation, and maintenance of a post-market monitoring system (Article 72);
- procedures related to the reporting of a serious incident per Article 73;
- the handling of communication with national competent authorities, other relevant authorities, including Union institutions, notified bodies, other operators, customers, or other interested parties;
- systems and procedures for record keeping of all relevant documentation and information;
- resource management, including security-of-supply-related measures;
- an accountability framework setting out the responsibilities of the management and other staff with regard to all aspects listed in this Article.

Auditor's test shape: Article 17 is the **management-system dimension** of the conformity assessment. The notified-body auditor walks it the way an ISO/IEC 27001 or 42001 auditor walks the Annex SL clauses — one procedure at a time, with document / interview / observation triangulation. The QMS audit interfaces with the Annex IV technical-documentation audit: the QMS procedures *generate* the Annex IV evidence; a weak QMS produces Annex IV gaps.

## The Annex VII procedure in four motions

The notified-body auditor under Annex VII proceeds in four motions.

### Motion 1 — Application and acceptance

The provider submits an **application** including identity, QMS documentation, list of high-risk AI systems covered, technical documentation per Annex IV, and any analyses of the Union harmonisation legislation to which the systems may also be subject. The notified body verifies the application is complete and that the scope is within its designation.

### Motion 2 — QMS assessment (Annex VII point 3)

The notified body assesses the QMS against Article 17. The assessment includes **document review** of the QMS procedures and **on-site audit** of the implementation. The notified body may perform the audit at the premises where the systems are developed. The assessment concludes with an **approval report** or a **non-conformity statement** identifying what must be corrected before the technical-documentation assessment proceeds.

### Motion 3 — Technical documentation assessment (Annex VII point 4)

The notified body assesses the technical documentation of each high-risk AI system in scope against Annex IV. Where the provider has applied harmonised standards, the notified body verifies the application. Where the provider has not applied them, the notified body assesses whether the solutions adopted meet the Chapter III Section 2 requirements.

If the technical documentation satisfies Annex IV and the system meets Chapter III Section 2, the notified body issues a **Union technical documentation assessment certificate**. The certificate lists the provider, the system, the technical documentation reference, and the validity period (up to four years, Annex VII point 4.6).

### Motion 4 — Surveillance (Annex VII point 5)

Surveillance ensures the provider duly complies with the approved QMS and that the systems continue to conform to Chapter III Section 2. Surveillance includes **periodic audits** (at least once per year) and may include **unannounced audits** of the provider's premises or of the premises of the provider's suppliers. The notified body may require re-evaluation of the technical documentation for a specific system at any time, and will require re-evaluation on **substantial modifications** per Article 43(4).

## Substantial modifications and the re-assessment trigger

Article 3(23) defines a **substantial modification** as a change not foreseen or planned in the initial conformity assessment that affects the compliance of the system with the requirements of Chapter III Section 2 **or** that results in a modification to the intended purpose.

Not every change is substantial. A provider who declared in the Annex IV dossier a **predetermined change management plan** (e.g., scheduled retraining on a defined data distribution, bounded hyperparameter sweeps, known UI iterations) can execute those changes without re-assessment, provided the changes stay within the pre-approved envelope — a mechanism modelled on FDA PCCP (chapter 6) and now naturalised into the AI-Act interpretation.

Auditor's test shape: the provider's change-control procedure (does it distinguish substantial from non-substantial?); the predetermined-change plan (does it describe the envelope with verifiable bounds?); the change log (does each change correspond to a plan entry or trigger a re-assessment request?). This test interfaces with Article 73 serious-incident reporting (`mod-108`) — a serious incident can force a reconsideration of what was "foreseen or planned".

## The conformity-assessment report and CE-marking decision

The notified-body audit output is three artefacts.

1. **The QMS audit report** — findings against Article 17 each dimension, grading (comparable to ISO 17021-1 grading but under the AI Act's criteria), corrective-action requests, approval of the QMS.
2. **The technical documentation assessment report** — findings against Annex IV per sub-point, each cross-referenced to Articles 9 through 15 as applicable, corrective-action requests, approval of the dossier.
3. **The certificate** — issued when both motions conclude positively, listing the provider, the system, the technical-documentation reference, the applied harmonised standards, and the validity period.

With a positive certificate in hand, the provider signs the **EU declaration of conformity** (Article 47), affixes the **CE marking** (Article 48), and registers the high-risk AI system in the **EU database** per Article 71 before placing it on the market.

Where the certificate is refused or withdrawn, the provider cannot affix the CE marking; placing the system on the market would trigger market-surveillance action under Regulation (EU) 2019/1020 and the AI Act's own supervisory regime (Articles 74 onward).

## Reporting obligations that follow the certificate

Once the certificate issues, the clock starts on continuous obligations the auditor returns to at surveillance:

- **Article 20 corrective action.** If the provider considers or has reason to consider that a high-risk AI system placed on the market is not in conformity, the provider shall take the necessary corrective actions, withdraw, disable, or recall the system, and inform the distributors, importers, authorised representatives, and other affected parties.
- **Article 21 cooperation.** The provider shall provide the competent authorities with all information and documentation necessary to demonstrate conformity.
- **Article 72 post-market monitoring.** A documented system for actively and systematically collecting, documenting, and analysing data on the performance of the high-risk AI system throughout its lifetime (`mod-108` chapter 5).
- **Article 73 serious-incident reporting.** Serious incidents shall be reported to the market-surveillance authority of the Member State concerned within specific deadlines (immediately and not later than 15 days in general; shorter for incidents affecting critical infrastructure or involving multiple deaths; longer for systematic patterns), with specific content requirements.

The auditor's surveillance workpaper tracks evidence that each obligation is operating — not evidence that the procedure exists, but evidence that it has executed against actual post-market signal.

## Common failure modes at the Article 43 audit

- **Wrong lane.** Provider self-attests under Annex VI for a system that falls within Annex III point 1, or within an Annex I Section A sectoral regime, or without having applied harmonised standards — placing the CE marking without a valid conformity assessment.
- **Harmonised-standards drift.** Provider declares "applied harmonised standards" without the full application; auditor must verify clause-by-clause.
- **Annex IV skeleton.** Technical documentation is a cover document with pointers rather than a complete dossier; audit reveals gaps in sub-points 2–6 most often.
- **Risk register divorced from design.** Article 9 register exists but mitigations named there do not appear as design elements in Annex IV section 2.
- **Bias examination perfunctory.** Article 10 bias examination conducted on a convenience subset; no evidence against reasonably-foreseeable misuse.
- **Logging retained-but-queryable gap.** Article 12 logs technically generated but not retrievable in time or at the granularity Article 20 or Article 73 require.
- **Instructions-for-use deployer-hostile.** Article 13 text inherits boilerplate from similar products; deployer cannot discharge Article 26 obligations from it.
- **Human-oversight UI-only.** Article 14 oversight exists as a "stop" button but with no latency measurement, no override success logs, no automation-bias training evidence.
- **Cybersecurity generic.** Article 15 covers ISO 27001 security without AI-specific threat-modelling (poisoning, model extraction, adversarial examples).
- **Substantial-modification elision.** Provider routes material model changes through the "predetermined change plan" but the plan does not describe the envelope with verifiable bounds; every change is "pre-approved".
- **Post-market monitoring paper.** Article 72 plan exists; evidence of its execution post-certificate does not.
- **Serious-incident clock missed.** Article 73 notification sent outside the 15-day window or with insufficient content; surveillance finding.

## Interfaces to adjacent chapters and modules

- **Chapter 2 (GPAI with systemic risk)** picks up the Article 50–55 lane for general-purpose models above the systemic-risk threshold.
- **Chapter 9 (engagement shape chooser)** returns to this chapter when the client's scope indicates an EU high-risk Annex III system.
- **`mod-105` (ISO 42001)** is the horizontal AIMS audit that sits beside this one; many providers run both in parallel, with the ISO 42001 AIMS producing the evidence the Article 17 QMS audit tests.
- **`mod-106`** (model and system card claims) feeds the Article 13 and Article 15 testable-claim audit.
- **`mod-107`** (risk management and harm models) feeds the Article 9 audit.
- **`mod-108`** picks up Article 72 post-market monitoring and Article 73 serious-incident reporting.

## Summary

- The EU AI Act's Article 43 conformity-assessment routes are Annex VI (internal control, self-attestation) and Annex VII (third-party notified-body assessment of the QMS and the technical documentation); Article 44 is the biometric subroute; sectoral routing applies where Annex I Section A legislation covers the product.
- The substantive criteria are Articles 8–15: risk management (9), data governance (10), technical documentation (11 + Annex IV), logging (12), transparency and deployer instructions (13), human oversight (14), accuracy / robustness / cybersecurity (15); plus Article 17 QMS as the management-system dimension.
- The Annex VII procedure sequences in four motions — application, QMS assessment, technical-documentation assessment, surveillance — producing three artefacts: QMS audit report, technical-documentation assessment report, Union technical documentation assessment certificate (validity up to four years).
- With the certificate in hand, the provider issues the EU declaration of conformity (Article 47), affixes the CE marking (Article 48), and registers the system in the EU database (Article 71) before market placement.
- Post-certificate obligations the auditor returns to at surveillance: Article 20 corrective action, Article 21 cooperation, Article 72 post-market monitoring, Article 73 serious-incident reporting; and the Article 43(4) substantial-modification re-assessment trigger.
