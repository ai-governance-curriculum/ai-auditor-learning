# ISO/IEC 42001:2023 — Clauses 4–10 and Annex A to Auditable Criteria

## Motivation

ISO/IEC 42001:2023 is the first horizontal management-system standard for AI, and it is the one the audit market has consolidated around for conformity audits — accredited certification bodies run it through ISO/IEC 17021-1 + 42006, and internal audit functions use it as the backbone of AIMS internal audits under clause 9.2. The standard was written as a *harmonised* ISO management-system standard (HLS Annex SL), which means its clauses 4–10 are intentionally generic. The audit value is in translating that generic structure into AI-specific, testable criteria — and in pulling the **Annex A** controls plus the **Statement of Applicability** across the same translation. This chapter is the clause-by-clause and Annex-A translation playbook.

## The standard's shape, briefly

- **Clauses 4–10** — the management-system requirements, following the Annex SL High-Level Structure shared with ISO/IEC 27001, ISO 9001, and the rest of the ISO MS family: Context, Leadership, Planning, Support, Operation, Performance Evaluation, Improvement.
- **Annex A (normative)** — a catalogue of controls the organisation selects from when deciding how to treat identified AI risks, documented in a Statement of Applicability (SoA).
- **Annex B (informative)** — implementation guidance for the Annex A controls.
- **Annex C (informative)** — potential AI-related organisational objectives and risk sources to consider.
- **Annex D (informative)** — considerations for integration with other management systems (ISO/IEC 27001, 27701, 9001, 13485, etc.).

The clauses are *procedural* obligations ("the organization shall..."); the Annex A controls are *procedural plus measurable* control objectives supporting risk treatment. Both halves must be translated.

> **Scope guardrail.** This module teaches *criteria translation*. Running the audit of the AIMS (stage-1 and stage-2, nonconformity grading, certification recommendation) is covered in `mod-105-auditing-iso-42001-aims`. Do not pre-empt it here.

## Clause-by-clause translation guide

The convention below: each clause gets one or two illustrative criteria in the template from chapter 1. Full translation across every sub-clause is the exercise work; this guide models the discipline, not the bulk.

### Clause 4 — Context of the organisation

Issue: organisations frequently paper this clause with a generic statement that does not identify AI-specific internal / external issues, stakeholders, or scope.

```
Criterion ID:             C-42001-4.1-01
Source clause:            4.1 — determine external and internal issues relevant to the AIMS and its ability to achieve intended outcomes.
Statement:                The organisation documents AI-specific external issues (regulatory landscape by jurisdiction of operation, applicable sector standards, third-party AI dependencies) and internal issues (AI maturity, data posture, talent, legacy system coupling) and reviews them on a defined cadence.
Evidence:                 Context analysis document with AI section; cadence-of-review log; stakeholder register with AI-specific entries (regulators, impacted groups, workforce, suppliers).
Procedure:                Inspect context analysis; trace one external and one internal issue through to an AIMS objective or risk register entry; inquire of AIMS owner on cadence.
Measurable attributes:    AI-specific entries present (y/n); review within defined cadence (y/n); traceability to objective or risk entry (y/n).
Owner:                    Second line.
Residual judgment:        Guard against generic re-use of ISO 27001 context analysis with "AI" bolted on.
```

Clause 4.3 scope-definition translation is especially audit-material: the organisation is required to determine the boundaries and applicability of the AIMS. For AI, this means naming AI systems in and out of scope with a defensible inclusion / exclusion rule — often the hardest workpaper to produce in the first audit cycle.

### Clause 5 — Leadership

The usual trap is a signed AI policy with no evidence of leadership *commitment* beyond the signature. Translate 5.1 into criteria that look for allocation of resources, assignment of accountability, communication of the policy, and management participation in the management review under 9.3 — not just a policy artifact.

```
Criterion ID:             C-42001-5.2-01
Source clause:            5.2 — top management shall establish an AI policy.
Statement:                The AI policy is approved by top management, references the organisation's AI purpose, commits to applicable requirements (incl. legal/regulatory), commits to continual improvement of the AIMS, and is communicated within the organisation and to interested parties as appropriate.
Evidence:                 Policy document with approval evidence; policy-communication records (intranet post, training enrolment, supplier contract clauses); policy version history.
Procedure:                Inspect policy; verify communication to a sampled population of staff and relevant suppliers; interview top-management representative.
Measurable attributes:    Required elements present (y/n per element); communication reach (fraction of sampled staff who received the policy).
Owner:                    First line (communication) + second line (policy ownership).
Residual judgment:        Freshness: is the policy consistent with the current AI system inventory and current law, or is it a 2023 artifact in a 2026 landscape?
```

Clause 5.3 — roles, responsibilities and authorities — translates to a criterion on a named RACI across the AIMS, often mapped to a role catalogue including `ai-governance-analyst` (L15), `ai-risk-engineer` (L25), `ai-evaluation-engineer` (L35), `senior-ai-governance-architect` (L50), and the **internal audit function reporting outside the AIMS owner** per ISO/IEC 42001 clause 9.2 and the IIA Standards.

### Clause 6 — Planning

Clause 6.1 is the AIMS risk and opportunity engine — 6.1.2 risk assessment, 6.1.3 risk treatment, 6.1.4 AI system impact assessment (cross-referenced to ISO/IEC 42005 for method). Clause 6.2 is AI objectives. Clause 6.3 is planning of changes.

Criteria translation points:

- **6.1.2** requires a *process*, not just a one-off assessment. Author criteria on inputs, outputs, cadence, re-execution triggers.
- **6.1.3** requires a Statement of Applicability — see Annex A section below.
- **6.1.4** AI system impact assessment under ISO/IEC 42005 has its own criteria shape. For deployer organisations and for EU AI Act Article 27 fundamental-rights impact assessments, the two overlap substantially; one artifact can satisfy both if the criteria are authored to the superset.
- **6.2** objectives must be measurable, monitored, and have a plan — the ISO/IEC 42001 analogue of SMART criteria. Reject vague objectives at translation time.

```
Criterion ID:             C-42001-6.2-01
Source clause:            6.2 — AI objectives shall be measurable, monitored, communicated, updated, and subject to a documented plan with resources, responsibilities, and timelines.
Statement:                Each documented AI objective has (a) a measurable success metric, (b) a monitoring cadence and owner, (c) communication evidence, (d) a plan with named resources, responsibilities, and completion date.
Evidence:                 Objectives register; monitoring records; communication records; objective-level implementation plans.
Procedure:                Inspect the objectives register; for sampled objectives, trace to monitoring records and plan; inquire of owners.
Measurable attributes:    % of objectives with all four elements present.
Owner:                    Second line (AIMS owner).
Residual judgment:        Check whether objectives are hostage to vanity metrics ("number of AI projects reviewed") rather than outcomes ("residual-risk level for in-scope systems").
```

### Clause 7 — Support

Support covers resources (7.1), competence (7.2), awareness (7.3), communication (7.4), documented information (7.5). For AI specifically:

- **7.2 competence** translates to named competencies for roles touching AI (model development, evaluation, operation, audit) with evidence of competence (training, certification, experience). This is where the role-to-credential map in `mod-101` becomes the auditable fact.
- **7.5 documented information** translates to document and record control — for AI, that includes model cards, datasheets, run logs, evaluation reports, incident tickets, and management-system records.

### Clause 8 — Operation

Clause 8 governs operational planning and control (8.1), AI risk assessment execution (8.2), AI risk treatment execution (8.3), and AI system impact assessment execution (8.4). It is the clause where the ISO/IEC 42001 standard pushes into the AI life-cycle — which is why the Annex A controls, which are dominated by life-cycle control objectives, operate alongside clause 8.

Criteria translation here should cover the handoff between risk-assessment outputs (clause 6) and operational execution (clause 8). The audit test is whether risk items raised in 6.1.2 actually route to treatment plans and controls executed under 8.3 and recorded under 7.5. The frequent finding is "risk register entries exist but no treatment plan traces back to them".

### Clause 9 — Performance evaluation

Clause 9 contains monitoring, measurement, analysis and evaluation (9.1), internal audit (9.2), and management review (9.3).

- **9.1** criteria cover what is monitored (AIMS performance, process effectiveness, Annex A control effectiveness), how, by whom, at what cadence, how analysed, how reported.
- **9.2** criteria cover the internal audit programme — scope, frequency, method, independence of auditor from area audited, reporting, action tracking. This is where the AI Auditor is *auditing an AI Auditor* if the organisation has one; see `mod-101` chapter 6 for independence posture.
- **9.3** criteria cover the management-review inputs (clause 9.3.2 lists required inputs in substance) and outputs (9.3.3), the cadence, and that outputs feed decisions on the AIMS.

### Clause 10 — Improvement

Clause 10 covers nonconformity and corrective action (10.1) and continual improvement (10.2). Criteria translation focuses on whether nonconformities raised (internal or external) feed root-cause analysis and corrective action plans with closure evidence, rather than disappearing into a tracker. The audit test is usually by sampling: pull N nonconformities from the prior audit cycle and trace them through to closure.

## Annex A — control catalogue and the Statement of Applicability

Annex A to ISO/IEC 42001 is a catalogue of controls organised by control objective. The organisation is not required to adopt every control — it is required to document a **Statement of Applicability** that identifies, for each control, whether it is applicable and the justification for inclusion or exclusion. The SoA is thus the tightest single audit document in the whole AIMS: for a large AI portfolio, it typically runs 30–60 pages.

### SoA criteria translation

Three families of criteria apply to the SoA:

1. **Completeness** — every Annex A control is addressed (included or excluded with reasoned justification). No silent omissions.
2. **Justification quality** — exclusion justifications are specific to the organisation's risk profile and reference risk-assessment outputs, not boilerplate.
3. **Traceability** — each included control traces to (a) a documented implementation, (b) evidence of operation in the audit period, and (c) a risk-register entry it treats.

```
Criterion ID:             C-42001-SoA-01
Source:                   Clause 6.1.3 + Annex A — Statement of Applicability.
Statement:                The SoA addresses every Annex A control; for each applicable control, the SoA names the implementation owner, the risk-register entries it treats, and the evidence of operation; for each excluded control, the SoA states a specific justification referencing the AI system scope or risk profile.
Evidence:                 SoA document; linked risk register; linked control-implementation descriptions; sample evidence of operation.
Procedure:                Walk the SoA control-by-control; for a sampled set of applicable controls, trace to implementation and evidence; for a sampled set of excluded controls, challenge the justification.
Measurable attributes:    (a) coverage completeness (all controls addressed); (b) applicable controls with traced implementation and evidence (%); (c) excluded controls with specific (non-boilerplate) justification (%).
Owner:                    Second line (AIMS owner).
Residual judgment:        Focus skepticism on excluded controls — the audit history is that boilerplate exclusions mask uncovered risks.
```

### Individual Annex A controls — criteria translation shape

The Annex A control families are AI-life-cycle-oriented: policy and organisational; AI system life cycle (requirements, design, verification, validation, deployment, operation, monitoring, decommissioning); data; third party and customer; information for interested parties; use of AI systems; AI impact and oversight. Annex B provides implementation guidance for each. <!-- needs-research: confirm the exact grouping and numbering of Annex A control families at reading time; ISO/IEC has been publishing supporting standards (e.g., ISO/IEC 42005, ISO/IEC 42006) through 2024–2026 that cross-reference Annex A and may be used in audits -->

A translation-friendly pattern per Annex A control:

- **Control objective** — the "what" at a policy level. Rarely testable as-is.
- **Implementation** — the "how" the organisation chose. Testable as a procedural criterion (is it documented, approved, assigned).
- **Operation evidence** — the artifacts generated by running the control. Testable as a measurable or procedural criterion depending on the control.
- **Effectiveness indicator** — the outcome that indicates the control is achieving the objective. Testable as a measurable criterion when the organisation has set one.

Worked example (data-quality control, common Annex A content):

```
Criterion ID:             C-42001-AnnexA-DQ-01
Source:                   ISO/IEC 42001 Annex A data-management control objective — "the organisation defines and documents data-quality requirements for AI systems and verifies that data meets them before use in training or inference".
Statement:                For each AI system in scope, the organisation documents data-quality requirements (completeness, accuracy, representativeness, labelling consistency, provenance, consent/licensing), verifies the training and evaluation datasets against them, and retains evidence of verification results prior to release of the model.
Evidence:                 Data-quality requirements document; dataset datasheets; verification reports; release-gate records showing the verification was a release precondition.
Procedure:                Inspect requirements; for sampled AI systems, inspect datasheets and verification reports; re-perform a subset of the verification on an independent sample of the dataset (requires auditor's expert).
Measurable attributes:    (a) requirements defined per system (%); (b) datasheet present (%); (c) verification report present (%); (d) verification result within defined tolerance (%).
Owner:                    First line (data / ML team) with second-line (eval / release-assurance) verification.
Residual judgment:        For datasets originating from third-party providers, external evidence (contractual datasheets) ranks higher than internal re-labelling; preserve the external artifact.
```

Repeat the pattern across the Annex A controls in scope.

## Integration with adjacent ISO management systems

ISO/IEC 42001 Annex D flags integration with ISO/IEC 27001 (information security), ISO/IEC 27701 (privacy information management), ISO 9001 (quality), ISO 13485 / ISO 14971 (medical devices), and others. For organisations that already hold ISO 27001 certification, the AIMS audit may be executed as an integrated management-system audit, with shared evidence for shared controls (access control, incident management, document control).

Criteria translation discipline: a shared control is only *once* an auditable criterion for the integrated audit, not two separate criteria with duplicated evidence. The SoA explicitly notes integration where applicable; the audit report notes which controls were tested under which standard.

## From translation to Stage-1 and Stage-2 shape (handoff)

This chapter produces the *criteria* — the testable statements. The actual audit *execution* against those criteria (Stage-1 readiness audit on documentation; Stage-2 implementation audit on operation; sampling across the AI system population; non-conformity grading) is covered in `mod-105-auditing-iso-42001-aims` and in the ISO/IEC 17021-1 + 42006 conformity-assessment-body stack (`mod-101` chapter 6). Keep the module boundary clean: finish the criteria here, then the next modules test against them.

## Summary

- ISO/IEC 42001 clauses 4–10 are generic Annex SL management-system clauses; they become auditable only after AI-specific translation using the template from chapter 1.
- Annex A plus the Statement of Applicability is the densest source of controls — the SoA itself gets three families of criteria (completeness, justification quality, traceability).
- Each Annex A control decomposes into objective → implementation → operation evidence → effectiveness indicator; translate down to the testable layer.
- Data-quality, life-cycle-stage, impact-assessment, and third-party controls are the Annex A areas where measurable criteria (not just procedural) dominate.
- Integration with ISO/IEC 27001 / 27701 / 9001 and sector management systems is explicit in Annex D; shared controls get single criteria statements, not duplicates.
- The criteria produced here feed the audit execution in `mod-105`, not this module.
