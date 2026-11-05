# Auditing Drift, Quality, Safety-Signal, and Injection-Detection Pipelines

## Motivation

Chapter 1 fixed the shape of the monitoring plan. This chapter opens the pipelines themselves. For a GenAI deployment, the signals that most often surface a real problem — before users complain, before a regulator writes, before a journalist reports — are the ones watching for drift, quality regression, safety-monitor hits, near-miss patterns, cost / latency anomalies, and jailbreak / prompt-injection attempts. The organisation almost always runs these through one or more off-the-shelf tools: **WhyLabs / whylogs**, **Evidently AI**, **Alibi Detect**, **Fiddler AI**, **Arthur AI**, **Holistic AI**, and a handful of vendor dashboards.

The auditor does not re-architect these pipelines. The authoring sits with `ai-risk-engineer` (L25) and the ML-platform team. The auditor tests the pipelines as *evidence sources*: can the operation of each signal be reperformed, does the signal's output drive the register update it claims to drive, and does the organisation's threshold-trip pattern match the auditor's own independent threshold-trip computation.

This chapter is where the ISA 500 / ISA 520 evidence discipline from `mod-104` meets the tooling the organisation chose. It is also where the auditor confronts the specialist-reliance boundary: when a signal's statistical definition is deep enough that the auditor cannot reperform directly (membership-inference audits, calibrated drift tests, high-dimensional embedding distance), ISA 620 specialist-use applies and the auditor records both the specialist and the specialist's work.

## The six signal families

The auditor's first workpaper is an inventory of the six signal families and the pipelines in the organisation that emit each. Not every organisation runs every family; the plan-coverage test from chapter 1 identifies which families should be present.

### 1. Data and feature drift

Drift is the headline signal in classical ML and still matters for retrieval, routing, embedding, and feature-driven decision systems around LLMs. Three canonical sub-signals:

- **Covariate drift** — the input distribution shifts (new user demographics, seasonality, product launch).
- **Label drift** — the ground-truth distribution shifts (regulatory change reclassifies a category, an upstream workflow changes).
- **Concept drift** — the relationship between inputs and labels shifts (fraud patterns evolve, the underlying phenomenon changes). Concept drift is the hardest to detect because label delay is often long.

Common tooling and what each produces:

- **whylogs (WhyLabs)** — open-source dataset profiling that writes compact profiles to WhyLabs for reference / production comparison. Drift surfaces as a profile-to-profile distance against a reference profile.
- **Evidently AI** — open-source reports and tests for data drift, target drift, data quality, prediction drift. Produces both HTML reports and a JSON test-result object.
- **Alibi Detect** — open-source library (Seldon) implementing published drift-detection tests (MMD, KS, chi-squared, classifier-based drift, LSDD, learned kernels). More statistically explicit than the dashboard-oriented tools.
- **Fiddler AI**, **Arthur AI** — commercial observability platforms that embed drift detection with model-performance context and lineage.

Audit tests:

- **Reference-set provenance.** The drift comparison requires a reference distribution. The auditor requires the reference to be pinned (hash, date, size) and the rationale for the pin documented. A reference set that was last refreshed before the current model version is a trace defect.
- **Statistical test disclosure.** Which test is the pipeline running (KS, chi-squared, PSI, MMD, classifier-based)? What is the p-value / divergence threshold? Is there multiple-testing correction? A pipeline running an unnamed "Evidently default" or a KS test across many features without correction will emit false alarms and desensitise operators — a finding on test specification.
- **Reperformance.** For a sampled time window, re-run the drift test with the documented configuration against the documented reference. Confirm the result matches the dashboard. Deltas indicate pipeline drift from configuration.
- **Threshold link to action.** A drift alert that does not trigger either a model re-train, a data-quality incident, or a documented acceptance (with signature) is a monitoring-without-analysis finding (chapter 1).

### 2. Quality regression

Quality metrics depend on the task. Auditor expectations by deployment shape:

- **Classification** — per-class accuracy, per-class recall / precision, subgroup slices (see `mod-107` chapter 5).
- **Regression** — RMSE / MAE by stratum, calibration (reliability diagrams, ECE).
- **Retrieval / RAG** — grounding rate, citation precision, hallucination rate against a graded set, MRR against a held-out query set. <!-- needs-research: cite the common RAG eval harness the organisation uses (RAGAS, TruLens, Ares) at reading time -->
- **Open-ended generation** — LLM-as-judge quality on a graded rubric, human-annotator agreement as a cross-check (see `mod-106` chapter 4 on calibration methodology).
- **Agentic systems** — task-success rate on held-out tasks, trajectory length, tool-call-success rate.

Audit tests:

- **Metric definition.** The dashboard's metric name is not the definition — the auditor demands the code or query that computes it and compares to the plan definition.
- **Held-out set hygiene.** Is the quality eval run against a held-out set, not the training or fine-tuning set? For LLM-judge evals, which judge model, which prompt, which rubric? Is the judge independently evaluated for bias (chapter 6 reliability tests)?
- **Baseline comparison.** Every quality metric should have a documented baseline — the prior version's score, the pre-deployment acceptance threshold, a published benchmark number for the task. A metric with no baseline is a chart.
- **Regression-threshold origin.** The threshold at which regression triggers action — e.g. "a 2-point drop in task success on the held-out benchmark" — must come from the methodology, not from vendor-default. See chapter 1 "threshold defensibility."
- **Reperformance.** Re-run a sampled quality metric against the documented held-out set and compare. ISA 620 specialist-use if the metric is statistically deep.

### 3. Safety-monitor signals

Safety monitors are the production counterparts of the red-team program (`mod-107` chapter 3) and the guardrail program (`mod-107` chapter 7). They emit *rates* (per request, per 1k requests, per day) of:

- **Refusal / abstention.** The model declined to answer. A sudden rise or fall is both a quality signal and a safety signal.
- **Guardrail hit.** An input or output guardrail classifier fired. Common tools: **Llama Guard 3 / 4**, **ShieldGemma**, **OpenAI Moderation**, **AWS Bedrock Guardrails**, **Azure AI Content Safety**, **Anthropic Constitutional Classifiers**, **Lakera Guard**, **Arthur Shield**, **Robust Intelligence**, **HiddenLayer**.
- **Policy-violation.** A policy-rule layer (regex / rule / LLM-as-policy) fired.
- **Tool-use-denied.** An agent attempted a tool call that the allow-list / permission layer denied.
- **PII / sensitive-category emission.** An output passed through a Presidio or classifier gate and was redacted or blocked.
- **CSAM / NCII classifier hit.** Rate of classifier triggers on either input or output.
- **CBRN-category refusal / override attempt.** For systems with CBRN policy coverage.

Audit tests:

- **False-positive / false-negative evidence.** For each classifier guardrail in the production pipeline, the auditor requires the published or vendor-stated operating characteristics. If the operating point in production is not documented ("we run Llama Guard 3 with the default threshold"), that is a configuration-management finding.
- **Rate-baseline.** The guardrail hit rate for yesterday is uninterpretable without a baseline. The plan should state the historical rate distribution and the rate at which a change is action-worthy.
- **Sampling-and-replay.** Safety-monitor logs should support deferred review — a sample of flagged outputs is reviewable by a qualified reviewer. The auditor verifies the sample-and-review cadence is operating.
- **Guardrail-off-target.** A guardrail that fires frequently on benign input (low precision) desensitises operators; one that misses obvious adversarial input (low recall) is operationally useless. The auditor cross-tests the production classifier against a held-out adversarial / benign set and reports the operating point.

### 4. Near-miss signals

Near-misses are the leading indicator the aviation-safety analogue has taught the broader safety community to take seriously. An AI near-miss is any event where a harm was averted but a boundary was approached. Patterns:

- **Guardrail-fired-then-user-retry.** The user obtained the same harmful result on a second attempt by rephrasing.
- **Tool-call-denied-then-user-escalation.** The agent attempted a disallowed action and the user complained or escalated.
- **Moderation-queue-backlog growth.** Review queue grows faster than reviewers can clear it.
- **Reviewer-override of safety-monitor.** A human reviewer overturned a safety-monitor signal — in either direction.
- **Policy-exception requests.** The number of exception requests opened by product teams.

Audit tests:

- **Taxonomy existence.** The plan enumerates the near-miss event types the organisation tracks. Without a taxonomy, near-misses are not captured.
- **Volume and trend.** The auditor pulls near-miss counts for the period and compares to prior periods. A declining trend without a documented explanation (maturing controls, release cadence slowing) is suspicious.
- **Near-miss-to-incident ratio.** The ratio is organisation-specific; a sudden shift is a signal.
- **Near-miss-to-register trace.** Near-miss patterns should feed the register's likelihood column or the control-effectiveness assessment. A near-miss trend with no register effect is a trace break.

### 5. Cost and latency anomalies

Operational metrics are not merely SRE concerns — they are AI-safety signals when a cost-per-request spike reflects prompt amplification, infinite-tool-loop patterns, or an external attempt to exhaust the budget (an AI-specific DoS). Patterns the auditor should expect:

- **Cost-per-request P95 / P99.**
- **Token-per-request distribution** with an alert on long tails.
- **Tool-call-count-per-request** with an alert on runaway agents.
- **Latency P95 / P99 by endpoint** with alerts on drift.
- **Error-rate by error class** with alerts on class-specific upticks.

Audit tests:

- **Metric-to-cause linkage.** A cost anomaly without an investigation record is undiagnosed. The plan should state the investigation procedure.
- **Runaway-agent detection.** Agentic systems should have an upper bound on tool-call count and / or token budget; the enforcement of that bound should be logged and reviewed. An unbounded-tool-call pattern is a resilience and safety finding.
- **Adversarial-cost framing.** The organisation should recognise cost / latency anomalies as a potential OWASP LLM04 "Model Denial of Service" signal, not only an SRE signal. <!-- needs-research: confirm current OWASP LLM Top 10 numbering at reading time — the 2023/2024/2025 lists have renumbered — verify LLM04 Model DoS reference -->

### 6. Jailbreak and prompt-injection detection

Prompt-injection and jailbreak are not one-time risks resolved at pre-deployment; they are a continuous measurement obligation. The pipelines combine:

- **Classifier-based detection** — Llama Guard 3's jailbreak category, Lakera Guard, Robust Intelligence prompt-injection models, Anthropic Constitutional Classifiers' jailbreak heads.
- **Signature-based detection** — regex / keyword rules against known patterns from the garak, PyRIT, promptfoo, HarmBench jailbreak corpora.
- **Behavioural detection** — anomalous tool-call sequences, anomalous output patterns.
- **Indirect-injection detection** — content-provenance checks on retrieved documents, injection-pattern checks in tool outputs.

Audit tests:

- **Coverage against OWASP LLM01.** The detection pipeline should be mapped to OWASP LLM Top 10 LLM01 "Prompt Injection" (and the 2025 list's "Direct Prompt Injection" / "Indirect Prompt Injection" split if adopted). A finding against any sub-category of LLM01 that is not watched is an Article 15 cybersecurity defect for high-risk systems. <!-- needs-research: confirm OWASP LLM Top 10 2025 structure and numbering at reading time -->
- **Attack-corpus refresh.** The signature / classifier corpus must be refreshed on a documented cadence. Static corpora are quickly obsolete.
- **Red-team-replay.** The production detection pipeline should be re-tested against the organisation's red-team corpus on a documented cadence; results feed the register (see `mod-107` chapter 3).
- **Indirect-injection coverage.** For systems that retrieve from the web, email, or user-uploaded documents, the pipeline must detect injection in retrieved content, not only in user prompts. A pipeline that only inspects user input misses the agentic-system threat model.

## Tool-specific evidence shapes

The auditor does not need to be an operator of every tool, but should be able to request and read the evidence each tool produces. A short reference:

| Tool | Published artefact the auditor requests | What the artefact evidences |
|------|----------------------------------------|-----------------------------|
| whylogs / WhyLabs | Profile files (`*.bin` / Parquet); WhyLabs project history; constraint-violation logs | Reference-vs-production distribution comparison; alert history |
| Evidently AI | Report JSON / HTML; test-suite JSON | Drift / quality / data-quality panel results with per-test outputs |
| Alibi Detect | Detector configuration (YAML / JSON); test-run outputs (p-values, distances) | Named statistical test with explicit output |
| Fiddler AI | Model-monitoring export; alert-event export; traffic-profile export | Model performance + drift + explainability on common telemetry |
| Arthur AI | Monitor configuration; alert feed; model-card integration | Performance + fairness + drift integrated view |
| Holistic AI | Governance-platform audit reports; bias-audit reports | Fairness + explainability + governance roll-ups suitable for board packs |
| Classifier guardrails (Llama Guard / ShieldGemma / etc.) | Model card; operating-point configuration; per-request classifier score logs | Published FPR / FNR and production operating point |
| Vendor platform guardrails (Lakera / Arthur Shield / Robust Intelligence / HiddenLayer) | Vendor dashboard export; alert-event feed; vendor attestations | Vendor-managed detection with provider-attested coverage |

A row where the organisation cannot produce the "artefact" column is a tool that is running but not evidenced for audit — a Clause 7.5 documented-information finding and a `mod-104` ISA 500 evidence sufficiency finding.

## Example — reperforming an Evidently drift report

The auditor should expect to work in a notebook or small script to reperform a drift metric. The following sketch is the kind of reperformance pattern the workpaper references rather than a production pipeline.

```python
# Reperformance sketch — compare auditor-run drift vs. the dashboard value.
# Replace paths / column names with the engagement's actual artefacts.
import pandas as pd
from evidently import Report
from evidently.presets import DataDriftPreset

reference = pd.read_parquet("audit_evidence/reference_profile_2025Q3.parquet")
current = pd.read_parquet("audit_evidence/production_sample_2025W38.parquet")

report = Report(metrics=[DataDriftPreset()])
run = report.run(reference_data=reference, current_data=current)
auditor_result = run.dict()

# Compare drift share and per-column p-values to the dashboard export.
# A delta of more than numerical tolerance is a pipeline-configuration finding.
```

The specifics (Evidently version, preset vs. explicit per-column tests, p-value threshold, reference window) belong in the workpaper; the auditor does not improvise them. The reperformance confirms the organisation's claim rather than replacing it.

## Threshold-breach reperformance across families

Chapter 1 established the threshold-breach reperformance step. In this chapter the auditor executes the reperformance against each signal family — at minimum:

- One drift reperformance (Alibi Detect MMD or chi-squared recomputation against pinned reference).
- One quality reperformance (held-out set recomputation with the plan's metric definition).
- One safety reperformance (classifier operating-point verification against a held-out benign / adversarial set).
- One near-miss volume reperformance (count-level re-aggregation against the raw event store).
- One cost / latency reperformance (P95 recomputation from raw request logs).
- One jailbreak / injection reperformance (re-run of a documented adversarial subset against production detection).

Each reperformance becomes a workpaper row: metric name, auditor-computed value, dashboard-reported value, delta, materiality assessment.

## The risk-signal contract

The `ai-risk-engineer` (L25) risk-signal contract is the documented interface between monitoring and the risk register. The contract declares:

- **Signal name** and canonical definition.
- **Source pipeline** (tool, computation).
- **Register row(s)** the signal updates and the update rule (score change, control-effectiveness refresh, review-trigger).
- **Breach semantics** — what constitutes a breach, over what window.
- **Owner** who signs off breach-driven updates.
- **Review cadence** for the contract itself.

The auditor's contract-level tests:

- **Contract exists.** The contract is a document, not implicit. Absent contract → finding against Clause 9.1 "methods," Article 72 "plan," and the `mod-107` chapter 2 register-trace discipline.
- **Contract is versioned.** New signals and new register rows should bump the contract; silent evolution is a change-management defect.
- **Contract is cross-referenced.** The monitoring plan references the contract; the register methodology references the contract. One-sided references are a trace break.
- **Contract is executed.** For a sampled breach event the auditor verifies the register update matches the contract's update rule.

## When ISA 620 specialist-use applies

For signals whose statistical depth exceeds what a generalist auditor can reperform, ISA 620 (Using the Work of an Auditor's Expert) applies. Typical loci in this chapter:

- Calibrated drift tests where the test choice is itself a modelling question (classifier-based drift, MMD with learned kernels).
- Guardrail-classifier operating-point reperformance requiring held-out evaluation data of material size.
- Membership-inference / privacy-adjacent monitoring (see `mod-107` chapter 6).
- Fairness-subgroup regressions with intersectional slicing (see `mod-107` chapter 5).

Where ISA 620 applies the auditor records the specialist's identity, competence, objectivity, scope of work, and the auditor's evaluation of the specialist's output. The specialist's work is not treated as a substitute for the auditor's judgement; it is evidence the auditor takes responsibility for.

## Common failure modes

- **Reference-set-stale.** The drift reference predates the current model version and is no longer a meaningful comparator.
- **Guardrail-off-the-shelf-with-no-configuration-record.** The classifier threshold in production is unknown, uncaptured, and therefore unauditable.
- **Metric-definition-dashboard-divergence.** The dashboard's metric name matches the plan; the computation does not.
- **Near-miss-not-taxonomised.** Near-misses are discussed informally; no event taxonomy or capture pipeline exists.
- **Cost-and-latency-treated-as-SRE-only.** Cost anomalies are investigated for billing reasons; the AI-safety and OWASP LLM04 angle is unseen.
- **Injection-detection-input-only.** User-input prompt-injection is monitored; retrieved-content injection is not.
- **Vendor-platform-opaque.** The vendor dashboard is used but the raw event feed is not captured by the organisation, defeating audit reperformance.
- **Contract-absent.** Monitoring and the register are operated by different teams with no written interface.

## Summary

- Six signal families — drift, quality, safety-monitor, near-miss, cost / latency, jailbreak / injection — are the inventory the auditor expects the plan to cover for a GenAI deployment.
- The common tool landscape — whylogs / WhyLabs, Evidently AI, Alibi Detect, Fiddler AI, Arthur AI, Holistic AI, classifier and vendor guardrails — produces named evidence artefacts the auditor requests.
- Reperformance per family converts dashboard numbers into audit evidence; ISA 620 specialist-use applies where statistical depth demands it.
- The `ai-risk-engineer` (L25) risk-signal contract is the documented interface between monitoring and the register; it is itself an audit subject.
- Common failure modes concentrate at the interface — stale references, undocumented operating points, metric-definition drift, missing contract — more than at the raw-pipeline level.
- Chapter 3 picks up the incident-response program that consumes the breaches this chapter identifies.
