# mod-105-auditing-iso-42001-aims: Auditing the AI Management System (ISO/IEC 42001) to Certification Shape

**Estimated effort:** 18 hours

## Learning objectives

- Audit ISO/IEC 42001:2023 clauses 4–10 — context, leadership, planning, support, operation, performance evaluation, improvement — as a certification auditor would; identify minor non-conformities, major non-conformities, and opportunities for improvement with ISO/IEC 17021-1 definition rigour.
- Audit the ISO/IEC 42001 Annex A controls, Annex B implementation guidance, and the Statement of Applicability — testing inclusion/exclusion justifications, control-objective coverage, and risk-treatment-plan traceability from risk register through control to evidence.
- Audit the AI policy, AI objectives, AIMS scope, and management commitment — reading the policy against clause 5.2, testing objective measurability against clause 6.2, and confirming scope boundaries against the AI system inventory.
- Audit the AI risk assessment and risk-treatment process (clauses 6.1.2, 6.1.3) against ISO/IEC 23894 guidance and the hands-on evidence the `ai-risk-engineer` role generates.
- Audit the AI system impact-assessment process (clause 6.1.4 / ISO/IEC 42005) and cross-check with EU AI Act Article 27 fundamental-rights impact assessments where applicable.
- Audit operation controls (clause 8) including the AI life-cycle — design, development, verification, validation, deployment, operation, monitoring, decommissioning — against the Annex A life-cycle controls.
- Audit performance evaluation (clause 9) — monitoring (9.1), internal audit (9.2), management review (9.3) — testing that each is functioning rather than paper-based.
- Audit improvement (clause 10) — nonconformity and corrective action, continual improvement — testing closure evidence and root-cause rigour.
- Run a Stage-1 (documentation/readiness) and Stage-2 (implementation) audit in ISO/IEC 17021-1 / 42006 conformity-assessment-body shape, including report authoring, audit opinion, and certification recommendation.
- Position the AIMS audit against adjacent management-system audits (ISO/IEC 27001, 27701, ISO 9001, ISO 14971, ISO 13485) so an integrated audit of a regulated organisation is defensible.

## Structure

- `01-iso-42001-audit-frame-and-conformity-assessment-cycle.md` — the clause map, Annex A, SoA, and Stage-1/Stage-2/surveillance/recertification cycle under ISO/IEC 17021-1 + 42006.
- `02-nonconformity-grading-under-iso-17021-1.md` — major/minor/OFI definitions, grading rigour, and how grading drives the certification decision.
- `03-auditing-clause-4-and-5-context-scope-leadership-policy.md` — context, interested parties, AIMS scope, AI policy, roles.
- `04-auditing-clause-6-planning-risk-assessment-and-objectives.md` — 6.1.2, 6.1.3, 6.2, 6.3 against ISO/IEC 23894.
- `05-auditing-ai-system-impact-assessment-with-iso-42005.md` — 6.1.4 and ISO/IEC 42005 impact-assessment procedure, cross-check against EU AI Act Article 27.
- `06-auditing-annex-a-and-the-statement-of-applicability.md` — SoA completeness, exclusion rigour, and risk-to-control-to-evidence traceability.
- `07-auditing-clause-8-operation-and-the-ai-life-cycle.md` — operational planning, life-cycle controls, decommissioning.
- `08-auditing-clause-9-performance-evaluation-internal-audit-and-management-review.md` — monitoring, internal audit programme, management review.
- `09-auditing-clause-10-nonconformity-corrective-action-and-improvement.md` — root-cause rigour, closure evidence, continual improvement.
- `10-stage-1-and-stage-2-execution-report-and-certification-decision.md` — executing the audit, drafting the report, issuing the certification recommendation.
- `11-integrated-management-system-audits-27001-27701-9001-13485-14971.md` — single-audit shared-control strategy for organisations with multiple certifications.
- `exercises/`: per-exercise prompts aligned to the chapters.
- `labs/`, `quizzes/`: long-form labs and knowledge checks.
- `resources.md`: curated primary references.

## How this module fits the `ai-auditor` track

- **Input from `mod-102`** — criteria translation for ISO/IEC 42001 clauses and Annex A.
- **Input from `mod-103`** — scoping, materiality, and the Stage-1/Stage-2 engagement letter.
- **Input from `mod-104`** — evidence discipline (ISA 500), sampling (ISA 530), specialist use (ISA 620), reproducibility bundles.
- **Output to `mod-110`** — conformity-assessment-body shape at the sector level (EU AI Act Annex VII, FDA GMLP, SR 11-7).
- **Output to `mod-111`** — findings reporting discipline for the Stage-2 audit report.
- **Delta from `ai-evaluation-engineer` (L35)** — release-assurance methodology *inside* the second line, versus this course's *third-line* audit of the whole management system.
- **Delta from `senior-ai-governance-architect` (L50)** — the architect *designs* the AIMS the auditor *audits*; same clause map read from opposite sides of the independence line.
