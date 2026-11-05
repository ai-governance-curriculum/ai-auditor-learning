# Auditing Clause 8 — Operation and the AI Life Cycle

## Motivation

Clause 8 is where plans meet production. Clause 6 defined the processes; clause 8 operates them. **Clause 8.1** addresses operational planning and control — the organisation implements, controls, and documents the processes planned under clause 6. **Clauses 8.2–8.4** cover operational AI risk assessment, operational AI risk treatment, and operational AI system impact assessment. Running through all of clause 8 and heavily instrumented by Annex A is the **AI system life cycle** — design, development, verification, validation, deployment, operation and monitoring, decommissioning — which Annex A's life-cycle-control family makes testable control objective by control objective.

Clause 8 is where the auditor confirms that the AIMS actually governs the AI the organisation ships. A clause 8 audit that only looks at the procedures is a documentation audit, not an operation audit; the auditor must reach the running systems, the pipelines, the trace stores, and the production configs.

## Clause 8.1 — operational planning and control

**Requirement.** The organisation shall plan, implement, and control the processes needed to meet AIMS requirements and to implement the actions determined in clause 6, by establishing criteria for the processes, implementing control in accordance with the criteria, keeping documented information as evidence that the processes have been carried out as planned, controlling planned changes and reviewing consequences of unintended changes, and ensuring outsourced processes are controlled or influenced.

**Audit test.** Request the operational-planning document(s): the documented processes that execute the clause 6 plans, the criteria for those processes, the records produced, and the change-control mechanism. Walk one planned action from clause 6 (e.g., a risk-treatment plan for a specific risk) through operational execution:

1. The plan references an operational process.
2. The process has documented criteria (inputs, steps, approval, outputs).
3. Records show the process executed during the audit period.
4. Changes to the process are controlled (versioning, approval).
5. Where the process is outsourced (e.g., third-party red-team), there is an outsourcing control (contract, SLA, evidence-sharing requirement, periodic review).

**Common defects.** Plans without a named operational process. Processes without documented criteria. Records of execution missing or episodic. Outsourced processes with no governance (vendor red-team contracted, but no requirement for the vendor to provide artifacts the AIMS can retain).

## Clauses 8.2, 8.3, 8.4 — operational AI risk, treatment, impact assessment

These three clauses are the operational mirror of 6.1.2, 6.1.3, 6.1.4. The audit tests mirror chapters 4 and 5 but at the execution level:

- **8.2 (operational AI risk assessment).** The organisation *runs* risk assessments at the defined cadence and triggers (per the 6.1.2 procedure) and the outputs flow into the risk register. The auditor samples the register, looks at what new assessments were performed in the audit period, and checks trigger execution.
- **8.3 (operational AI risk treatment).** The organisation *implements* treatments per the risk-treatment plan from 6.1.3 and the SoA. The auditor samples controls from the SoA (chapter 6) and tests operation.
- **8.4 (operational AI system impact assessment).** The organisation *conducts* impact assessments per the 6.1.4 procedure. Covered in chapter 5.

Clause 8 is where many Annex A life-cycle controls land in evidence — the operation evidence the chapter-6 SoA walk needs comes from clause 8 execution.

## The AI life cycle — the audit frame

The AI system life cycle is the backbone of clause 8 and of Annex A's life-cycle control family. The eight life-cycle stages the auditor walks:

1. **Requirements and specification.** The AI system's intended use, performance criteria, data requirements, oversight model, constraint set.
2. **Design.** Architecture, algorithmic choice, data strategy, evaluation strategy, risk-mitigation design.
3. **Development.** Training, fine-tuning, prompt engineering, retriever configuration, tool integration, pipeline implementation.
4. **Verification.** Does the system do what it was designed to do? Unit testing, integration testing, correctness testing.
5. **Validation.** Does the system do what the use case requires? Performance evaluation on representative data; fairness evaluation; safety evaluation; red-teaming.
6. **Deployment.** Release decision, deployment configuration, rollout plan, user communication, instructions-for-use publication.
7. **Operation and monitoring.** Live operation, monitoring, incident detection and response, drift detection, human-oversight execution.
8. **Decommissioning.** Retirement, data retention/deletion, model-artifact retention, communication to users.

Each stage has one or more Annex A controls (typically named "AI system life cycle — [stage]" or similar), and the auditor's clause 8 test walks these controls in sequence for sampled AI systems.

## Auditing each life-cycle stage

### 1. Requirements and specification

**Evidence.** Requirements documents, intended-use statements, instructions-for-use drafts, acceptance criteria, data requirements.

**Audit test.** Sample AI systems released in the audit period. For each: inspect the requirements artifact. Verify it defines: purpose, intended-use context, performance criteria with thresholds, data requirements (volume, provenance, quality), oversight expectations, and the constraint set (what the system shall *not* do). Verify the requirements are approved under the organisation's governance (not just the ML team's internal documents).

**Common defects.** Requirements captured only as user stories in a backlog; no documented intended-use boundary; no "shall not" constraints; approval not evident.

### 2. Design

**Evidence.** Design documents, architecture diagrams, algorithmic-choice rationale, data-strategy document, evaluation-strategy document.

**Audit test.** Inspect the design artifact. Verify alignment with the requirements. Verify the design documents the evaluation strategy (what will be tested and how) — this is the handoff into clauses 8 verification/validation and into the second-line evaluation function (`ai-evaluation-engineer` L35, `model-evaluation-engineer` L30 in the broader role map).

**Common defects.** Design document is a system diagram only, no algorithmic-choice rationale; evaluation strategy entirely implicit; design predates requirements (reverse chronology — ML team built first, documented later).

### 3. Development

**Evidence.** Data lineage records, training-run artifacts, fine-tuning logs, prompt-template histories, retriever configurations, tool-integration records, pipeline-as-code commits.

**Audit test.** For each sampled system: reconcile the production model artifact (hash) to a registry record; reconcile the registry record to a training run (if applicable) or to the foundation-model version and fine-tune lineage; verify the prompt templates and retriever configs in production were produced by the development pipeline and are approved. Chapter 4 of `mod-104` on evidence applies at full depth here.

**Common defects.** Production model artifact not reconcilable to a specific training run or build pipeline; prompt templates edited outside the development pipeline; retriever-configuration drift between development and production.

### 4. Verification

**Evidence.** Unit-test coverage, integration-test records, correctness-test results, pipeline-check logs.

**Audit test.** Verification is often well-controlled in mature engineering organisations because it mirrors standard software QA. The auditor's test confirms the AI-specific verification exists (e.g., tests that verify prompt-template rendering, retriever-context pass-through, tool-call-argument shapes) and that failures block release.

### 5. Validation

**Evidence.** Evaluation reports, benchmark results, red-team reports, fairness analyses, robustness analyses, calibration analyses.

**Audit test.** For each sampled system: inspect the validation evidence. Verify the evaluation covers the performance criteria from requirements. Verify a release decision was made on the basis of validation outcomes — not a timeline pressure. Verify independent validation where the organisation's policy requires it (second-line validation vs. first-line self-evaluation).

The auditor here benefits significantly from specialist support (`mod-104` chapter 3). Judging whether a fairness evaluation is substantively adequate requires domain depth; the auditor tests process adherence while the specialist tests substantive adequacy.

**Common defects.** Validation that only covers accuracy; no fairness or robustness evaluation; "validation" produced by the model team with no independent check; release decision pre-dated the validation (validation documented after launch).

### 6. Deployment

**Evidence.** Release-decision records, deployment manifests (IaC), rollout plans, user communications, instructions-for-use published.

**Audit test.** For each sampled system released in the period: inspect the release-decision record (named approver, decision basis, residual-risk statement). Reconcile the deployment to the manifest in the IaC repo and to the model-registry record. Verify user-facing information (instructions for use, system documentation) is published per the organisation's policy and, for EU AI Act high-risk systems, per Article 13 transparency and Article 16 obligations. <!-- needs-research: verify current article numbering and deployer-obligation text in the as-adopted EU AI Act -->

**Common defects.** Release decision in Slack or verbally agreed; deployment manifest edited outside IaC; instructions for use not published or out of date.

### 7. Operation and monitoring

**Evidence.** Production telemetry, monitoring dashboards and underlying queries, alerting-rule definitions, incident tickets, drift-detection outputs, human-oversight records (reviewer actions, override logs).

**Audit test.** This is the densest Stage-2 workload for most engagements. For sampled systems:

- Operation evidence: production traces available for the audit period; retention honours the organisation's record-retention policy; model-version tags present in traces.
- Monitoring: metrics defined, dashboards present, underlying queries retrievable (reach for the query, not the screenshot — `mod-104` chapter 1).
- Alerting: rules defined, fired in the period (or not — silence is also data), triage records available.
- Incidents: inspect tickets for incidents involving the system; cross-check with clause 10 corrective action handling.
- Drift: drift-detection runs configured, results available, decisions made on results.
- Human oversight: where the system is high-impact, inspect reviewer-action logs and override patterns.

**Common defects.** Monitoring present but no analysis — dashboards exist but no decisions trace to them; alerting rules defined but never fire during the period and no one notices; drift-detection configured but results ignored; human-oversight records thin or missing.

### 8. Decommissioning

**Evidence.** Decommissioning plan, data-retention/deletion records, model-artifact archival, user communication, SoA update, inventory update.

**Audit test.** Sample AI systems decommissioned in the audit period (or confirm none were, per the inventory). For each: inspect the decommissioning plan (defined trigger for decommission, user-notification plan, data-handling plan); inspect execution records (data deleted or retained per plan, model artifacts archived per record-retention policy, SoA entry updated to reflect the system is no longer in scope, inventory updated).

**Common defects.** Systems "decommissioned" by the ML team without AIMS-level record; data retention handled ad hoc; system still appears in the inventory months after decommissioning; SoA not updated.

## Documented information per the life cycle

Annex A includes controls on technical documentation and on information for interested parties. The auditor walks the end-to-end documentation set for a sampled system: requirements, design, data documentation (datasheet), model documentation (model card), evaluation reports, deployment manifest, operation evidence, incident records, change records. Gaps in the chain are findings against the relevant Annex A control(s) and typically against clause 7.5 documented information.

## Interaction with the EU AI Act

Where the organisation operates EU AI-Act high-risk systems, clause 8 execution overlaps substantially with the EU AI Act Article 9 risk management system, Article 10 data governance, Article 11 technical documentation, Article 12 record-keeping (logging), Article 13 transparency, Article 14 human oversight, Article 15 accuracy, robustness, and cybersecurity, and Article 16 obligations. <!-- needs-research: confirm article numbering and the precise obligation text at reading time -->
The AIMS clause 5.2 commitment to applicable requirements means that deployment of a high-risk system without the Article 11 technical documentation file is both an EU AI Act exposure and an AIMS clause 5.2 finding; chapter 5 covered the Article 27 parallel for impact assessment.

## GPAI usage under clause 8

If the organisation uses GPAI (enterprise ChatGPT, Copilot, Claude, Gemini) in its business or product, that usage is in clause 8 scope if it is in scope under clause 4.3. The auditor tests:

- Usage inventory (registry of GPAI uses, prompt templates, data classes allowed).
- Acceptable-use enforcement (DLP, logging of GPAI I/O, review of outputs).
- Provider governance (contract terms, data-processing addendum, vendor change notification).
- Impact assessment on the usage (chapter 5).
- Supplier-management evidence per the third-party Annex A control family.

GPAI usage treated as "below the AIMS radar" is a major 4.3 and 8.1 finding when scope captures it.

## Common failure modes

- **Documented procedures without operation evidence.** The AIMS defines the process; production shows the process was not run.
- **Operation evidence without analysis.** Monitoring data exists, dashboards exist, no decisions trace back to the data.
- **Release decisions made outside the AIMS.** Model team releases; release decision never flows through the governance committee that the policy says is responsible.
- **Prompt and retriever configuration drift.** Development-pipeline artifact and production runtime disagree; no reconciliation control.
- **Decommissioning only in engineering, not in AIMS.** System retired from code, not retired from inventory/SoA.
- **GPAI usage out of the AIMS.** Covered above.
- **Human-oversight claims without logs.** Policy requires human review for high-risk decisions; no reviewer-action log exists or the log shows rubber-stamp patterns.

## Summary

- Clause 8 is operation — the clause 6 plans running on actual AI systems.
- The AI life cycle (requirements, design, development, verification, validation, deployment, operation and monitoring, decommissioning) is the audit backbone, with Annex A life-cycle controls making each stage testable.
- The auditor's Stage-2 time concentrates on operation and monitoring (stage 7), where live-system evidence (traces, queries, alerts, incidents, drift, human-oversight records) is most dense.
- Documented information per the life cycle (requirements, datasheets, model cards, evaluation reports, deployment manifests, instructions for use, incident records) is walked end-to-end for each sampled system.
- EU AI Act obligations (Articles 9–16) and GPAI usage must be tested where in scope under clause 4.3 and committed to under clause 5.2.
- Findings cluster around the gap between documented procedures and operational execution — policies intact, operation evidence missing, monitoring without analysis, release decisions outside the governance pathway.
