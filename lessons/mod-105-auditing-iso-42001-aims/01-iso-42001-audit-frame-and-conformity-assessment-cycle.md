# The ISO/IEC 42001 Audit Frame — Clauses, Annex A, and the Conformity-Assessment Cycle

## Motivation

The auditor has arrived in the conformity-assessment lane of the AI assurance market. The subject matter is an **AI Management System (AIMS)** — the organisation's declared process for governing every AI system it operates. The criteria are **ISO/IEC 42001:2023**, a horizontal ISO management-system standard following the Annex SL High-Level Structure. The audit shape is prescribed: certification-body audits run under **ISO/IEC 17021-1:2015** (horizontal conformity-assessment-body requirements) with the AIMS-specific overlay in **ISO/IEC 42006** (requirements for AIMS certification bodies). Internal audits reuse the ISO/IEC 42001 clause map but run under IIA Standards 2024 and clause 9.2 of the standard itself.

This chapter installs the frame: what the standard looks like, how a 17021-1 certification cycle sequences across four phases, where the audit-day calculation lives, and what the engagement letter will say the auditor is doing. The subsequent chapters drill into each clause. Keep the frame nearby — it is the map the auditor returns to every time the fieldwork threatens to drift.

## ISO/IEC 42001 at a glance

ISO/IEC 42001:2023 is organised in two halves.

**Clauses 4–10 — the management-system requirements** (Annex SL harmonised structure, shared with ISO/IEC 27001, ISO 9001, ISO 14001, ISO 13485):

- **Clause 4 — Context of the organisation.** Determine external/internal issues, interested parties, scope of the AIMS, and the AIMS as a process-based system.
- **Clause 5 — Leadership.** Top-management commitment, AI policy, roles and responsibilities.
- **Clause 6 — Planning.** Actions to address risks and opportunities (6.1), including AI risk assessment (6.1.2), AI risk treatment (6.1.3), and AI system impact assessment (6.1.4). AI objectives (6.2). Planning of changes (6.3).
- **Clause 7 — Support.** Resources, competence, awareness, communication, documented information.
- **Clause 8 — Operation.** Operational planning and control (8.1), operational AI risk assessment (8.2), operational AI risk treatment (8.3), operational AI system impact assessment (8.4).
- **Clause 9 — Performance evaluation.** Monitoring, measurement, analysis and evaluation (9.1); internal audit (9.2); management review (9.3).
- **Clause 10 — Improvement.** Continual improvement (10.1); nonconformity and corrective action (10.2). <!-- needs-research: confirm 10.1/10.2 ordering versus the as-published ISO/IEC 42001:2023 text; the 2023 publication swaps the Annex SL default order -->

**Annex A — reference controls (normative).** A catalogue of control objectives and controls (life-cycle, data, third-party, information-for-interested-parties, system-use, impact, oversight). The organisation selects from this catalogue in response to its risk assessment and documents the selection in a **Statement of Applicability (SoA)** per clause 6.1.3.

**Annex B — implementation guidance (informative).** Guidance per control.

**Annex C — AI-related organisational objectives and risk sources (informative).** A reference list to feed risk assessment and objectives-setting.

**Annex D — integration with other ISO management-system standards (informative).** The explicit integration hooks to ISO/IEC 27001, 27701, ISO 9001, ISO 13485, ISO 14971.

### The ISO/IEC 42001 family

ISO/IEC 42001 is one star in a growing SC 42 constellation. Three others matter in every AIMS audit:

- **ISO/IEC 23894:2023 — Guidance on risk management for AI.** The method standard behind clauses 6.1.2 / 6.1.3; the auditor tests whether the organisation's risk-management process is consistent with 23894, since 23894 is informative but widely adopted as the AIMS risk-method reference. See chapter 4.
- **ISO/IEC 42005 — AI system impact assessment.** The method standard behind clause 6.1.4; cross-referenced in the standard's text. See chapter 5.
- **ISO/IEC 42006 — Requirements for bodies providing audit and certification of AIMS.** The AIMS-specific overlay on ISO/IEC 17021-1, including the AIMS audit-day calculation table. <!-- needs-research: confirm ISO/IEC 42006 publication status and current Annex A audit-day table at reading time; the standard was progressing through DIS/FDIS in the 2024–2026 window -->

The auditor is expected to read all four in combination.

## ISO/IEC 17021-1 — the horizontal conformity-assessment frame

ISO/IEC 17021-1:2015 (with amendments) is the requirements standard for bodies that certify management systems. Its obligations shape every certification-body AIMS engagement:

- **Clause 5 — Impartiality and independence.** The certification body must manage conflicts; auditors who consulted on the AIMS cannot certify it (chapter 7, `mod-101`).
- **Clause 6 — Liability and financing.** Not directly audit-shaping, but relevant to engagement letter terms.
- **Clause 7 — Resource requirements.** Competence of auditors and technical experts; AIMS-specific competence is layered by ISO/IEC 42006.
- **Clause 8 — Information requirements.** What the CB communicates to clients, to the public, and on certificates.
- **Clause 9 — Process requirements.** The audit cycle itself:
  - **9.2 Audit planning and execution.**
  - **9.3 Initial certification** — Stage-1 (9.3.1.2) and Stage-2 (9.3.1.3) audits.
  - **9.4 Conducting audits** — including nonconformity grading (9.4.8) that chapter 2 operationalises.
  - **9.5 Decision on certification** — independent reviewer, certification decision.
  - **9.6 Maintaining certification** — surveillance (9.6.2 and 9.6.3), recertification (9.6.3), scope changes, suspension/withdrawal.
  - **9.7 Appeals; 9.8 Complaints.**
- **Clause 10 — Management system requirements for certification bodies.** The CB operates its own MS covering document control, records, internal audit, management review, corrective action.

The AIMS auditor does not need to memorise every clause, but must know *which 17021-1 clause their current fieldwork lives under*: a Stage-2 opening meeting is under clause 9.4.3, a finding is under clause 9.4.8, the certification recommendation is under clause 9.5.

## ISO/IEC 42006 — the AIMS-specific overlay

ISO/IEC 42006 refines 17021-1 for AIMS. The parts that shape fieldwork:

- **AIMS-specific competence requirements.** Auditors need demonstrable competence in ISO/IEC 42001 clauses and Annex A controls, AI risk management (ISO/IEC 23894), AI system impact assessment (ISO/IEC 42005), AI life-cycle, applicable sector regulation, and the technical artifacts the audit will inspect (model cards, eval reports, trace stores). Technical experts under 17021-1 clause 7.2.5 supplement the lead auditor where domain depth is required (medical devices, financial services, biometrics).
- **Audit-time calculation.** 42006 Annex A provides the AIMS audit-day table used to derive Stage-1, Stage-2, surveillance, and recertification durations as a function of effective-personnel count, AI system count, AIMS maturity, and risk uplift factors. <!-- needs-research: confirm final structure of 42006 Annex A at reading time and whether a separate IAF mandatory document amends it -->
- **Impartiality uplifts.** The AIMS market has significant consulting overlap (firms that help build the AIMS and firms that certify it); 42006 tightens 17021-1 clause 5 around AIMS-specific conflicts.
- **Multi-site AIMS sampling.** Where the AIMS operates across sites with similar processes, 42006 refines the 17021-1 multi-site sampling rules for AI-specific populations.
- **Certification scope wording.** The text that appears on the certificate must name the AIMS scope in terms a reader can verify against the client's SoA and AI system inventory.

## The four-phase certification cycle

A full initial-certification engagement is **four phases over three years**: Stage-1, Stage-2, two annual surveillance audits, and recertification opening the next cycle.

### Stage-1 — documentation review and readiness

Under ISO/IEC 17021-1 clause 9.3.1.2, Stage-1 exists to:

- audit the client's management-system documentation;
- evaluate site-specific conditions and undertake discussions with client personnel to determine Stage-2 preparedness;
- review the client's status and understanding of requirements, particularly identification of key performance / significant aspects, processes, objectives, and operation of the MS;
- collect information on scope, processes, locations, and related statutory and regulatory aspects;
- review allocation of resources for Stage-2 and agree Stage-2 details;
- provide a focus for Stage-2 planning;
- evaluate whether internal audits (clause 9.2) and management reviews (clause 9.3) have been planned, performed, and substantiate readiness.

For AIMS the Stage-1 documentation set is: AI policy (5.2), AIMS scope (4.3), interested parties (4.2), AI risk-assessment procedure (6.1.2), risk-treatment plan and SoA (6.1.3), impact-assessment procedure (6.1.4), AI objectives (6.2), roles and responsibilities (5.3), operational planning (8.1), performance evaluation plan (9.1), internal audit programme (9.2), management-review agenda and minutes (9.3), nonconformity-and-corrective-action procedure (10.2). Stage-1 also sets the Stage-2 sampling strategy across the AI system inventory and the SoA.

Stage-1 output: a Stage-1 report with documentation observations, areas-of-concern that may become nonconformities at Stage-2, readiness conclusion, and the agreed Stage-2 plan. Chapter 10 walks the Stage-1 report template.

### Stage-2 — implementation audit

Stage-2 under 17021-1 clause 9.3.1.3 evaluates whether the AIMS is *implemented* and *effective*. The auditor walks every clause 4–10 requirement with evidence of implementation, samples the AI system population per the Stage-1 plan, tests SoA controls, interviews first-line engineering, second-line governance, top management, and internal audit, grades nonconformities per clause 9.4.8, and produces a certification recommendation. Chapter 10 is the Stage-2 execution chapter.

### Surveillance (years 2 and 3)

ISO/IEC 17021-1 clause 9.6.3 requires surveillance at least once per calendar year except in the recertification year. Surveillance scope: clauses 9.2 and 9.3 outputs since the last audit; corrective actions on prior findings; changes to the AIMS (scope, new/retired AI systems, new sites, regulatory landscape); risk-register and SoA updates; monitoring outputs; complaints and incidents; a sample of AI systems and SoA controls. Surveillance can raise nonconformities within its scope; scope-limited findings still bind the certification.

### Recertification (end of year 3)

Recertification is a full re-audit at Stage-2 depth, informed by three years of findings and improvements, with a three-year trend review on management-response reliability. Decisions: recertify, recertify with corrective-action plans, suspend, withdraw.

## The internal-audit variant

Internal AIMS audits under ISO/IEC 42001 clause 9.2 reuse the same clause map but run under IIA Standards 2024. They are not certification activities, so no certificate is issued; they are typically annual at full scope (sometimes quarterly thematic); they are subject to the CAE's independence posture, not 17021-1 clause 5; and they feed Stage-1 readiness by providing the documented evidence of clause 9.2 operation that the certification body will inspect. The internal audit opinion goes to the Audit Committee, not to an accreditation body.

## What stays constant across variants

Regardless of whether the engagement is Stage-1, Stage-2, surveillance, recertification, or internal, four things stay constant and drive the auditor's day-to-day work:

1. **The clause-4–10 map.** Each clause is a set of requirements the organisation must meet; each requirement is an audit criterion; each criterion needs sufficient appropriate evidence per ISA 500 / AU-C 500 (`mod-104` chapter 1).
2. **Annex A and the SoA.** The organisation's control selection is in the SoA; every included control needs evidence of implementation and operation; every excluded control needs a defensible exclusion justification.
3. **Nonconformity grading.** Findings are graded major / minor / OFI per ISO/IEC 17021-1 clause 9.4.8 (chapter 2); the certification decision follows the grading.
4. **Professional skepticism.** The AIMS is largely documentary; the auditor's job is to reach *through* the documents to operation evidence, and to challenge when the paper does not match the practice.

## How this module is structured

The next ten chapters follow that constant work, layered on the four-phase shape:

- **Chapter 2** — nonconformity grading rigour, because every subsequent clause audit ends in a grading decision.
- **Chapters 3–9** — clause-by-clause and Annex A audit mechanics.
- **Chapter 10** — Stage-1 and Stage-2 execution, report authoring, certification decision.
- **Chapter 11** — integrated audits with ISO/IEC 27001 / 27701 / 9001 / 13485 / 14971.

## Common failure modes with the frame itself

- **Skipping the frame and diving to Annex A.** Annex A is easier to test than clause 6 planning, and auditors sometimes front-load it. The result is a technically-rich but clause-shallow audit the CB's independent reviewer will reject.
- **Treating Stage-1 as a dress rehearsal.** Stage-1 is a formal audit with its own report. Clients and auditors who treat it as "pre-work" produce Stage-2 plans without sampling strategy and discover mid-fieldwork that scope was never agreed.
- **Mis-reading the Annex SL clause order against ISO/IEC 42001.** The 42001 2023 publication departs slightly from the vanilla Annex SL ordering in clause 10. Read the as-published text, not the Annex SL template.
- **Ignoring 42006 competence requirements.** A lead auditor without demonstrable AI-domain competence fails the 42006 competence obligation; the certification issued is contestable on appeal.
- **Confusing certification scope with AIMS scope.** The AIMS scope is the organisation's declared boundary (clause 4.3). The certification scope is the subset the certificate attests to. They are often not identical — the certificate wording must be exact.

## Summary

- ISO/IEC 42001:2023 is an Annex SL management-system standard with clauses 4–10 plus Annex A controls; the organisation declares control selection in a Statement of Applicability.
- Certification-body audits run under ISO/IEC 17021-1 with the AIMS-specific overlay in ISO/IEC 42006, across a four-phase cycle: Stage-1 (documentation/readiness), Stage-2 (implementation), two annual surveillance audits, recertification.
- Stage-1 and Stage-2 are both formal audits; Stage-1 produces a Stage-2 plan and a readiness conclusion, Stage-2 produces nonconformity grading and a certification recommendation.
- Internal AIMS audits under clause 9.2 reuse the clause map but run under IIA Standards 2024; they feed Stage-1 readiness but are not certification activities.
- Constants across every variant: the clause-4–10 map, Annex A and the SoA, nonconformity grading rigour, and professional skepticism.
- The next ten chapters drill into each of these in sequence, ending in Stage-2 execution and integrated-audit considerations.
