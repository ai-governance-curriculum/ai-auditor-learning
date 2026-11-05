# A Continuous-Audit Operating Model for AI

## Motivation

Point-in-time audits leave gaps. An ISO/IEC 42001 surveillance audit confirms the AIMS state over a few days once a year. An SR 11-7 validation locks in the model's state at the time of review. A SOC 2 Type II examination tests operating effectiveness over a window and reports after the window closes. In the intervals between these examinations, the production AI environment keeps changing — new models release, prompts shift, retrievers point at new corpora, guardrails get tuned, upstream providers push silent updates to foundation-model behaviour. Many of the controls the auditor cares about operate continuously; testing them at a point is testing the easiest moment to pass.

Continuous audit is the response: an operating model where evidence is produced continuously by the systems being audited, consumed continuously by the audit function, and exceptions trigger human review rather than waiting for the next scheduled visit. The audit committee gets a current view instead of a stale annual one; the audit function detects deterioration early instead of after it has aged into an incident.

This chapter walks the operating model, the evidence pipelines that feed it, the continuous-controls-monitoring layer, the exception-based human review process, and the dashboard reporting shape the audit committee consumes.

## Continuous audit vs continuous monitoring vs continuous assurance

Three terms get used interchangeably but mean different things.

- **Continuous monitoring** is a management activity. The first line owns operational monitoring; the second line (risk / compliance) owns risk monitoring. Monitoring produces signals management uses to run the business.
- **Continuous audit** is an audit activity. The internal audit function (third line) independently collects and analyses evidence continuously to produce assurance. Continuous audit relies on management's monitoring where possible but does not substitute for it with its own view.
- **Continuous assurance** is the outward-facing product. The audit committee and, where applicable, external stakeholders (regulators, customers under SOC-for-AI, notified bodies under EU AI Act post-market monitoring) receive continuous assurance outputs — attestations, dashboards, trend reports — derived from continuous audit activity.

The IIA Institute of Internal Auditors has written on continuous auditing since the mid-2000s; the practice is mature in financial controls and is still building out for AI controls. ISACA's Continuous Auditing and Continuous Monitoring guidance offers a frame the AI auditor can adapt. The 2024 revision of GAGAS does not use the term "continuous audit" but recognises ongoing monitoring data as evidence for performance audits.<!-- needs-research: confirm current IIA practice-guide and ISACA white-paper titles at reading time; the IIA Practice Guide on Continuous Auditing has been revised multiple times. -->

## Evidence pipelines — the input layer

Continuous audit requires evidence pipelines. Each pipeline is an automated feed from a source system into the audit function's evidence store. The AI-audit-specific pipelines the engagement lead builds and maintains:

### Eval-run artifacts

- **Source.** The MLOps pipeline's evaluation stage — pre-release evaluations (accuracy, fairness, robustness, safety, red-team suites) and ongoing (post-release) evaluations.
- **Artifact.** Eval report JSON / Parquet with dataset references, metric values, methodology version, and signed run manifest.
- **Audit use.** Verify that the eval ran, that it ran against the required datasets, that the metric thresholds the AIMS requires were met, and that any failure triggered the required review.
- **Verification.** Signature chain from the CI runner to the artifact store; signed with Sigstore / cosign; hash referenced in the model-registry entry.

### Trace-store queries

- **Source.** The production inference trace store (OpenTelemetry / Arize / Langsmith / internal). For LLM systems, traces include prompt, retrieval, tool calls, completion, and feedback.
- **Artifact.** Query results against sampled windows of traces.
- **Audit use.** Reperform fairness, safety, or performance claims on a sample of real production traffic; validate that logging is complete per the AIMS record retention requirement; detect shifts in prompt / tool usage that suggest unapproved changes.
- **Verification.** Query provenance (query text, run time, query signer); result size and distribution checks; retention of the result set in the audit evidence store.

### Guardrail-metric dumps

- **Source.** Production guardrail services (prompt-injection filters, PII filters, toxicity classifiers, content-policy classifiers).
- **Artifact.** Per-request metric counts and sampled flagged-request records.
- **Audit use.** Verify guardrail operating effectiveness continuously — are the filters firing where they should; are they causing excessive false positives; have thresholds been changed without controlled change management.
- **Verification.** Service-to-audit-store signature; change-history for threshold configuration.

### Drift-monitor outputs

- **Source.** Production drift monitors (feature drift, label drift, prediction drift, embedding-space drift, per-cohort performance monitors).
- **Artifact.** Drift reports and alerts.
- **Audit use.** Verify that the organisation's monitoring requirement (ISO/IEC 42001 §9.1; SR 11-7 ongoing monitoring; post-market monitoring obligations) is operating; verify that drift that exceeded thresholds triggered the defined response.
- **Verification.** Monitor-to-audit-store signature; alert routing records; change-history for monitor configuration.

### SIEM AI signals

- **Source.** The Security Information and Event Management platform, filtered for AI-relevant signals — prompt-injection detections, data-exfiltration attempts through model outputs, abnormal token-usage patterns, access to model-weights storage, access to training-data stores.
- **Artifact.** SIEM events and correlation rules.
- **Audit use.** Verify security controls on the AI stack; verify incident detection coverage.
- **Verification.** SIEM event chain-of-custody; rule change-history.

### GRC-for-AI exports

- **Source.** The organisation's GRC-for-AI platform (see chapter 3) — risk register entries, control test results, policy acknowledgements, assessment results.
- **Artifact.** Platform export APIs or scheduled dumps.
- **Audit use.** Independent verification of the second-line's risk register and control testing.
- **Verification.** API authentication; export integrity; change-history on the platform side.

### Model-registry provenance

- **Source.** The model registry (MLflow, SageMaker Model Registry, Vertex Model Registry, internal).
- **Artifact.** Model version entries with lineage (training data, training run, evaluation run, approval records, deployment records).
- **Audit use.** Verify every production model has the complete lineage the AIMS requires; identify models deployed without evaluation or approval; verify that model versions in production match the registry's approved set.
- **Verification.** Registry-to-audit-store API; signature on registry entries; reconciliation with production serving infrastructure.

### Sigstore attestation and SBOM

- **Source.** The build and release pipeline's Sigstore / cosign signatures; SBOMs for the serving stack.
- **Artifact.** Signed attestations for build provenance (SLSA level), container images, model weights, and dependencies.
- **Audit use.** Verify integrity of what is running in production; detect unsigned or improperly signed artifacts; verify supply-chain-attestation obligations (`mod-109`).
- **Verification.** Sigstore transparency log; public-key infrastructure for the signers.

Each pipeline is documented with its source, artifact, consumer, retention, and the audit test it supports. The audit function's evidence store is the destination; access to the store is restricted to the audit team.

## Continuous controls monitoring (CCM)

With evidence flowing in, the audit function operates a CCM layer. CCM is a set of automated checks — written in code, versioned in source control, tested like software — that evaluate evidence against criteria and produce exceptions.

A CCM rule has:

- **Criterion reference.** The authority and clause the rule tests against (ISO/IEC 42001 §9.1; AIMS procedure clause; EU AI Act Article 15; contractual SLO).
- **Data source.** The pipeline(s) the rule reads from.
- **Logic.** The check itself — threshold, trend, presence / absence, ratio, cross-reference, reconciliation.
- **Severity.** The exception classification if the rule fails (critical / high / medium / low) tied to the engagement scheme's classification (`mod-111` chapter 2).
- **Action.** What happens when the rule fails — notification, ticket creation, human review assignment, dashboard flag.
- **Owner.** The audit team member responsible for the rule.
- **Change history.** Who changed the rule, when, why.

Typical AI-audit CCM rules:

- "Every production model in the model registry has an evaluation record dated within the AIMS-required window."
- "Every production model's last fairness evaluation shows per-group metrics within the AIMS-defined tolerance, or carries an approved risk acceptance with current expiry."
- "Guardrail services' flag rates are within one standard deviation of the 90-day baseline for each guardrail; drift beyond threshold raises an exception."
- "Every high-risk system per the internal classification has a current impact assessment (AIMS §8.3; EU AI Act Article 27 fundamental-rights impact assessment) with signatures by the required roles."
- "Every incident flagged by the SIEM as AI-related has an entry in the incident register within 24 hours (`mod-108`)."
- "Every vendor model used in production has a current signed attestation and a current third-party-assurance report on file (`mod-109`)."

The rule set is documented in a CCM catalogue that the audit committee can inspect. The catalogue states, for each rule, what it tests, how often it runs, and what the exception trend has been.

## Exception-based human review

Exceptions trigger human review, not automatic failure findings. The lead sets a workflow:

- **Triage.** A junior auditor triages the exception within a defined time (commonly 1–3 business days). The triage records: valid / invalid (data quality issue), severity, next step.
- **Investigation.** Valid exceptions go to investigation. A senior auditor reviews the underlying evidence, performs any needed reperformance, and determines whether the exception represents a finding.
- **Finding development.** Where the investigation confirms a finding, the CCCER cycle (`mod-111`) begins.
- **Resolution.** Exceptions that are not findings close with a documented reason — data-quality correction, threshold adjustment (with justification), or confirmation that the underlying control was operating.

Two anti-patterns are specific to AI continuous audit:

- **Alert fatigue.** Rules that fire too often desensitise the team; the lead measures the alert-to-finding ratio and tunes rules whose ratio drifts.
- **Rule drift.** Rules whose definition is quietly adjusted by the audit team to reduce exception volume. The CCM catalogue's change history is the control; the EQR reviews it.

## Reporting to the audit committee

The audit committee consumes continuous-audit output through a cadence and shape the committee has agreed to. Typical shapes:

- **Monthly dashboard** — exceptions outstanding by severity, exceptions closed, new findings, trend lines on key AIMS metrics, status of open corrective-action plans.
- **Quarterly report** — written narrative covering the dashboard trends, significant findings this quarter, management response and CAP status, audit-plan execution versus plan, resource status.
- **Annual assurance opinion** — the audit function's opinion on the AIMS and the AI risk posture, informed by the continuous-audit data for the year plus the engagement-level work.

Chapter 8 of this module covers audit-committee reporting in depth. For continuous audit specifically, the shape the committee needs is a current view with trend, not a one-time snapshot — the committee wants to see whether the posture is improving or deteriorating against the organisation's own stated targets.

## Change management of the continuous-audit operating model

The continuous-audit operating model is itself a control that needs change management. Changes include:

- **New pipelines** — adding a source system; documented with the evidence it produces and the rules it enables.
- **Changed pipelines** — source-system changes that alter the artifact shape or content; pipelines must be revalidated before results are relied on.
- **New or changed rules** — the CCM catalogue change-history.
- **Severity threshold changes** — require documented approval at a level matching the severity's impact.
- **Retirement** — removing a pipeline or rule requires an articulated reason (criterion is no longer applicable; a better rule replaced this one).

The lead reviews changes against the baseline that the engagement planning assumes — if a continuous-audit rule is retired during an engagement, the engagement's reliance on that rule for assurance has to be reconsidered.

## Independence posture

Continuous audit mixes audit and operations. The operating model has to preserve independence:

- Audit owns the evidence store, the CCM rules, and the exception workflow. Management owns the source systems and their monitoring.
- Audit does not operate management's monitoring — if the CCM rule is finding the exceptions, the audit team does not instruct management to change the underlying system; it raises a finding and leaves the remediation to management.
- Where audit builds tooling that management then uses (the tooling layer in chapter 4), independence requires the lines to be drawn: who owns the tool, who can change the rule set, who consumes the output.
- For attestation firms performing continuous audit as an external service, the firm's independence rules (SEC independence; AICPA independence; IESBA) govern tooling ownership. A firm that both builds the continuous-audit tool and attests on its output is in a non-attestation-service-dependence posture and may fail independence.

## Reliability of the evidence pipelines themselves

A continuous-audit operating model is only as reliable as its pipelines. The lead audits the audit:

- **Pipeline health monitoring.** Each pipeline reports its own health — last run, record count, hash check. Pipelines that fail silently invalidate the rules that depend on them.
- **Sample-level reconciliation.** Periodically, the audit team reperforms a sample of the pipeline's output against the source system to confirm the pipeline is complete and accurate.
- **Access controls.** Who can change pipelines or rules; segregation between rule authors and rule approvers.
- **Backup and restore.** The evidence store has a retention policy, backup, and tested restore.

## A sketch of what one audit function's continuous-audit stack looks like

Illustrative — not a reference architecture:

- Evidence pipelines pull nightly from the MLOps platform (eval artifacts, model-registry provenance), the production observability stack (trace samples, guardrail metrics, drift monitors), the SIEM (AI-tagged events), and the GRC-for-AI platform (control test results, risk register).
- Pipelines land in an audit evidence store (object storage with hashing and signature verification) separate from management's data warehouse. Access is restricted to the audit team.
- A CCM engine runs rules against the evidence store on a defined schedule — most rules daily, some (e.g., model-registry reconciliation) hourly, some (e.g., incident-register reconciliation) near-real-time.
- Exceptions land in the audit team's work-management tool with a triage queue, assignment, and SLA.
- A dashboard surfaces exception counts, trends, and findings-in-development to the audit team; a subset is exposed to the audit committee on the monthly cadence.
- The CCM catalogue, pipeline documentation, and change history are themselves in version control with pull-request-based change management.

A function at this level of operating maturity produces a continuous assurance product that the audit committee and, where applicable, external regulators will trust more than an annual point-in-time view.

## Summary

- Continuous audit is a third-line activity distinct from management's continuous monitoring; it produces independent, continuously-refreshed assurance for the audit committee.
- Evidence pipelines feed an audit evidence store from MLOps, production observability, SIEM, GRC-for-AI platforms, the model registry, and supply-chain attestation systems; each pipeline is documented, verified, and monitored for health.
- Continuous Controls Monitoring is an automated check layer written as code, versioned, and catalogued; each rule names its criterion, data source, logic, severity, action, and owner.
- Exceptions trigger human triage and investigation under a workflow the lead manages; alert fatigue and rule drift are the two anti-patterns the lead watches for.
- The audit committee consumes continuous-audit output on a defined cadence (dashboard, quarterly report, annual opinion); the shape emphasises current state and trend over snapshots.
- The operating model itself requires change management, independence posture, and pipeline-reliability auditing — the audit auditing its own audit.
