# EU AI Act (Regulation (EU) 2024/1689) — Articles to Auditable Criteria, Harmonised Standards, and the GPAI Code of Practice

## Motivation

The EU AI Act — **Regulation (EU) 2024/1689**, published in the Official Journal 12 July 2024, in force from 1 August 2024 with staggered application dates through 2026–2027 — is the first *binding* horizontal AI regulation. Unlike NIST AI RMF or ISO/IEC 42001, non-conformity carries administrative fines (up to EUR 35 million or 7% of global turnover for prohibited practices; lower tiers for other breaches). The AI Auditor's criteria translation is therefore dual-purpose: to support the organisation's own conformity *self-assessment* (the default Article 43 route for most Annex III high-risk systems) and to support any *third-party* conformity assessment (notified-body audits under Article 43 and Annex VII for the narrow set that requires it). This chapter walks the key Articles, points at the **harmonised standards** being developed by CEN/CENELEC JTC 21 that give presumption of conformity under Article 40, and layers in the **EU AI Office GPAI Code of Practice** for the general-purpose AI obligations in Articles 51–55. <!-- needs-research: confirm the current application dates, harmonised-standard publication status, and GPAI Code of Practice version at reading time; this area changes quarterly through 2025–2027 -->

## The Act's shape, briefly

- **Title I** — subject matter, scope, definitions.
- **Title II** — prohibited AI practices (Article 5).
- **Title III** — high-risk AI systems (Articles 6–49); the bulk of the Act and the bulk of the audit surface.
- **Title IV** — transparency obligations for certain AI systems (Article 50).
- **Title V** — general-purpose AI models (Articles 51–56), including systemic-risk GPAI (Article 55).
- **Title VI** — measures in support of innovation (sandboxes).
- **Title VII–XII** — governance (AI Office, Board, advisory forum), databases, post-market monitoring, confidentiality, penalties, final provisions.

Key annexes the auditor works with directly: **Annex I** (Union harmonisation legislation that triggers high-risk scope), **Annex III** (standalone high-risk use cases), **Annex IV** (technical documentation content), **Annex VII** (Annex VII conformity assessment based on quality management system and technical documentation assessment).

## Scope classification — the gate before criteria

An EU AI Act audit begins with scoping: which of the organisation's AI systems fall into *prohibited* (Article 5), *high-risk* (Article 6 + Annex III or Article 6(1) safety-component path via Annex I), *limited-risk / transparency-only* (Article 50), or *minimal-risk* (not regulated as to AI-specific obligations beyond general law). The scoping work is an analyst-tier deliverable (`ai-governance-analyst`, L15) that the AI Auditor *consumes and tests*, not a product of the audit.

Scoping criteria the auditor must still author:

```
Criterion ID:             C-AIACT-SCOPE-01
Source:                   Articles 2, 3, 5, 6, 50, 51 — scope and classification definitions.
Statement:                The organisation documents a classification for each AI system in its inventory against the EU AI Act categories (prohibited / high-risk / transparency / minimal / GPAI model / systemic-risk GPAI), with a reasoned analysis citing the Article and Annex evidence, and updates the classification when material changes to use, model, or regulation occur.
Evidence:                 AI system inventory with EU AI Act classification column; classification analyses per system; change-log of reclassifications.
Procedure:                Inspect inventory; challenge sampled classifications against Annex III use-case descriptions; verify reclassification on sampled changes.
Measurable attributes:    (a) coverage — % of inventory with documented classification; (b) defensibility — % of sampled classifications surviving challenge; (c) reclassification timeliness.
Owner:                    Second line (AI governance + legal).
Residual judgment:        The high-risk / transparency boundary (e.g., emotion-recognition under Article 50 vs. use-case-specific high-risk) is the frequent misclassification point.
```

## High-risk AI systems — Articles 9–15

The core providers'-obligation set for high-risk systems. Each Article decomposes into multiple criteria.

### Article 9 — Risk management system

Mandates a continuous, iterative risk-management system across the AI system's life cycle: risk identification, analysis, evaluation, residual-risk mitigation, testing, and documentation of risk acceptance. Criteria translation points:

- Is the RMS *documented* and *operated* (both halves).
- Is it *continuous* — re-executed on material change, not one-off.
- Does it address *reasonably foreseeable misuse* (Article 9(2)(b)), not just intended use.
- Does the organisation **test** against the RMS output under Article 9(8).

The RMS is the Article most directly parallel to ISO/IEC 23894 and ISO/IEC 42001 clauses 6.1–6.2, and the **harmonised standard** likely to deliver presumption of conformity is built on those ISO standards. Author criteria that the ISO-aligned evidence satisfies.

### Article 10 — Data and data governance

Addresses training, validation, and test datasets: relevance, representativeness, bias examination, appropriate data governance and management practices. Criteria translation points:

- Dataset *datasheets* exist and cover the Article 10 topics.
- Dataset-level *bias examination* is performed and documented.
- Data-governance practices address data collection, preparation, labelling, annotation.
- Special-category data (GDPR Article 9) processed for bias detection under Article 10(5) is handled under the strict safeguards named in the Act.

### Article 11 — Technical documentation

Annex IV lists the required content of the technical documentation: system description, element description, computing resources, data, risk-management system, validation and testing, standards applied, declaration of conformity, and so on. The AI Auditor's criteria translation essentially restates Annex IV as a checklist, one criterion per element.

```
Criterion ID:             C-AIACT-11-TECHDOC-01
Source:                   Article 11 + Annex IV — technical documentation.
Statement:                The technical documentation for each high-risk AI system includes every element required by Annex IV points 1–9 at the level of detail required to enable national competent authorities and notified bodies to assess compliance, is drawn up before the system is placed on the market or put into service, and is kept up to date throughout the system's life cycle.
Evidence:                 Technical documentation package; version control; update log tied to material changes.
Procedure:                Inspect the documentation against the Annex IV checklist; verify dates against the market-placement date; trace updates to change records.
Measurable attributes:    (a) Annex IV coverage (% of required elements present); (b) completeness of each element against the Act's description; (c) freshness vs. last material change.
Owner:                    First line (provider engineering) with second-line review.
Residual judgment:        The frequent failure is "point 2 — detailed description" written at marketing-brochure level rather than at auditor level.
```

### Article 12 — Record-keeping

Automatic logging of events over the system's lifetime, appropriate to the intended purpose. Criteria cover log scope, retention, access, and traceability sufficient to support post-market monitoring and incident investigation (Articles 72, 73). Cross-check with Annex III use-case-specific record-keeping requirements (e.g., biometric identification systems).

### Article 13 — Transparency and provision of information to deployers

Instructions for use, system capabilities and limitations, intended purpose, performance characteristics by cohort, known or foreseeable circumstances that may cause risk, human-oversight arrangements, maintenance, expected life cycle. One criterion per bullet in Article 13(3).

### Article 14 — Human oversight

Design and development of high-risk systems to enable natural persons to oversee them during use. Criteria translate the oversight capabilities Article 14(4) lists: understand capacities and limitations, detect and address anomalies, interpret system output, decide not to use / override / reverse. For GenAI-heavy workflows this overlaps NIST GenAI Profile "human-AI configuration" risk.

### Article 15 — Accuracy, robustness, and cybersecurity

The headline *measurable* criteria of the Act. Article 15(2) requires that the organisation **declare** accuracy, robustness, and cybersecurity levels in the instructions for use; Article 15(4) mandates resilience to errors and attacks over the life cycle; Article 15(5) addresses cybersecurity against adversarial AI attacks (data poisoning, model poisoning, model evasion, confidentiality attacks, flaws). Criteria translation here is where the measurable-criterion discipline from chapter 1 dominates: define metric, method, population, tolerance, tolerance basis.

```
Criterion ID:             C-AIACT-15-ROBUSTNESS-01
Source:                   Article 15(4) — robustness of high-risk AI systems.
Statement:                The organisation documents the technical and organisational measures taken to achieve robustness against errors, faults, and inconsistencies that may occur within the system or the environment, including measures against feedback loops in systems that continue to learn after placing on the market; measures include technical redundancy, fail-safe design, and documented testing with measurable robustness metrics against a defined method.
Evidence:                 Robustness test plan; test results; method references; redundancy and fail-safe design descriptions; update / retraining governance evidence for learning-after-deployment systems.
Procedure:                Inspect plan, results; re-perform sampled robustness tests under auditor's expert; verify redundancy / fail-safe in deployment configuration.
Measurable attributes:    Robustness metric values vs. declared level per Article 15(2); test coverage against threat model.
Owner:                    First line (engineering) with second-line (release assurance).
Residual judgment:        Feedback-loop risk is the auditor's most common blind-spot on continually learning systems; cross-check Article 72 post-market monitoring.
```

## Provider / deployer / importer / distributor obligations — Articles 16–29

Each actor role carries its own obligation set. The AI Auditor translates the role that applies to the organisation under audit — frequently *both* provider (for in-house AI systems placed on the market) and deployer (for third-party AI systems used in operations). Each actor relationship is a separate audit sub-scope with its own criteria:

- **Providers (Articles 16–22)** — carry Articles 9–15 plus quality-management system (Article 17), document retention (Article 18), automatically generated logs (Article 19), corrective actions and duty of information (Article 20), cooperation with authorities (Article 21).
- **Deployers (Article 26 and related)** — operating instructions, human oversight in deployment context, input-data suitability, monitoring and logging, fundamental-rights impact assessment where required by Article 27.
- **Importers and distributors (Articles 23, 24)** — verification obligations before placement on EU market.
- **Authorised representatives (Article 22)** for non-EU providers.

Criteria for deployers often collapse into "operate under the provider's instructions, document the deployment context, monitor outputs, log usage, perform the FRIA where required" — map each to its Article number.

## Conformity assessment, declaration, and CE marking — Articles 43–48

Article 43 sets the conformity-assessment routes for high-risk systems: in most cases the provider executes **internal control** (Annex VI self-assessment); for a narrow set (e.g., biometric-identification systems in Annex III point 1), **third-party conformity assessment** by a notified body under Annex VII applies. The audit shape for notified-body work is covered in `mod-110-conformity-assessment-and-sector-audit-shapes`; this module authors the criteria both routes test.

Criteria at this layer:

- A documented conformity-assessment procedure exists per system and matches the applicable Annex VI or Annex VII route.
- The **EU declaration of conformity** (Article 47) exists, is signed, is up-to-date, and references all Union harmonisation legislation the system is subject to.
- **CE marking** (Article 48) is affixed where required.
- **Registration** in the EU database (Article 71) is executed before market placement.

## Transparency obligations — Article 50

Even where a system is not high-risk, Article 50 imposes transparency obligations: natural persons informed of interacting with AI; AI-generated content labelled as artificially generated; emotion-recognition and biometric categorisation disclosures; deepfake disclosures. Criteria translation is straightforward (disclosure present, in a form the user can perceive, before or at the point of interaction) but the exceptions (law enforcement etc.) must be modelled precisely.

## General-purpose AI models — Articles 51–56 and the GPAI Code of Practice

Title V distinguishes **GPAI models** (Article 51) from **GPAI models with systemic risk** (Articles 51 + 55). Obligations differ:

- **GPAI (all)** — technical documentation (Article 53 + Annex XI), information to downstream providers (Article 53 + Annex XII), copyright compliance (Article 53(1)(c)), training-data summary (Article 53(1)(d)).
- **Systemic-risk GPAI (Article 55)** — model evaluation including adversarial testing, risk assessment and mitigation, serious-incident tracking and reporting, cybersecurity protection.

The **EU AI Office GPAI Code of Practice** operationalises Article 56; adherence to the Code provides a path for providers to demonstrate compliance. Criteria translation for a GPAI provider engagement typically draws on the Code's own structure (safety and security, transparency, copyright) as the testable layer, with Article 53 / 55 cited as the regulatory source. <!-- needs-research: confirm the live GPAI Code of Practice version and signatory status at reading time; the Code has been iterated across 2024–2026 -->

## Post-market monitoring and incident reporting — Articles 72, 73

Article 72 requires providers to establish and document a post-market monitoring system. Article 73 requires reporting of serious incidents to the national competent authority within defined time windows. Criteria translation joins the AI Act obligations with the organisation's broader incident-management evidence (ISO/IEC 27035, sector-specific incident regimes such as SR 11-7 ongoing monitoring, FDA MDR for AI/ML SaMD).

## Harmonised standards — presumption of conformity (Article 40)

Where **CEN/CENELEC JTC 21** publishes harmonised standards and the Commission cites them in the Official Journal, conformity with those standards gives **presumption of conformity** with the corresponding Articles. As of authoring, harmonised standards in development include:

- AI risk management (expected to anchor Article 9 compliance).
- Data governance and data quality (Article 10).
- Transparency and information to users (Article 13).
- Human oversight (Article 14).
- Accuracy specifications and measurement (Article 15).
- Robustness specifications and measurement (Article 15).
- Cybersecurity (Article 15).
- Quality management system (Article 17).
- Conformity assessment.

<!-- needs-research: confirm which harmonised standards have been cited in the Official Journal and which remain in development at reading time; the JTC 21 publication pipeline moves quarterly -->

Criteria translation discipline: where a harmonised standard is cited in the OJ and the organisation claims conformity with it, the auditor can translate the *harmonised standard's* clauses into criteria and cite them for both the standard and the Article. Where the harmonised standard is not yet cited, criteria must be authored directly against the Article text.

## Audit posture — self-assessment vs. notified body vs. supervisory authority

The AI Auditor executes EU AI Act criteria work in three distinct postures:

- **Readiness / internal audit** inside a provider or deployer — IIA Standards govern the audit; criteria are authored against Articles / harmonised standards; output is to management and the audit committee.
- **Third-party conformity assessment** by a notified body — ISO/IEC 17065 + the Act's designation requirements govern the audit; criteria are authored against the *applicable Article plus the harmonised standard* where cited; output is the conformity-assessment certificate.
- **External attestation** by an ISAE 3000 / AT-C 205 firm against the organisation's claim of AI Act compliance — the firm's methodology governs; criteria are authored jointly against the Act and the organisation's asserted controls; output is the attestation report.

Mis-aligning posture, criteria, and report form is a recurring finding — surface it at engagement letter rather than discovering it at reporting.

## Summary

- EU AI Act 2024/1689 is binding; scoping each AI system to prohibited / high-risk / transparency / minimal / GPAI / systemic-risk GPAI is the first criteria work.
- High-risk providers' core obligations sit in Articles 9–15 (risk management, data governance, technical documentation, record-keeping, transparency, human oversight, accuracy/robustness/cybersecurity).
- Role-specific obligations (Articles 16–29) differ for provider / deployer / importer / distributor / authorised representative; map each audit sub-scope to the actor role.
- Conformity assessment (Articles 43–48), transparency (Article 50), GPAI and systemic-risk GPAI (Articles 51–56), and post-market monitoring + incident reporting (Articles 72–73) each generate dedicated criteria sets.
- CEN/CENELEC JTC 21 harmonised standards give presumption of conformity under Article 40 once cited in the OJ; align criteria to the harmonised standards where available.
- The EU AI Office GPAI Code of Practice operationalises Articles 53/55 for GPAI providers; use its structure for GPAI engagements.
- Audit posture — internal readiness vs. notified-body conformity assessment vs. external attestation — governs which methodology stack applies; align it at the engagement letter.
