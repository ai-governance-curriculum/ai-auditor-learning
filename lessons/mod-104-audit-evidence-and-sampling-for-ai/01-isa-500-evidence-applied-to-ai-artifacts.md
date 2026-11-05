# ISA 500 / AU-C 500 Applied to AI Artifacts — Sufficient, Appropriate, and Defensible

## Motivation

Every audit opinion is made of evidence. **ISA 500 — Audit Evidence** (IAASB) and its mirror **AU-C 500 — Audit Evidence** (AICPA) set the professional standard the AI Auditor is held to: the auditor must obtain *sufficient appropriate* evidence to reduce audit risk to an acceptably low level and to support the conclusion in the report. "Sufficient" is the measure of *quantity*; "appropriate" is the measure of *quality* — composed of *relevance* (does this evidence address the criterion being tested?) and *reliability* (how much faith does the source warrant?). A deviation between the subject matter and the criteria is a finding only if the evidence that demonstrates the deviation is itself sufficient and appropriate; otherwise the auditor has an opinion resting on sand.

AI changes none of this. What AI changes is *what the artifacts look like*, *how easy they are to alter without detection*, and *how often the evidence a manager hands over is derivative rather than original*. A screenshot of a Grafana dashboard is not a replacement for the underlying trace-store query; a model card's eval table is not a replacement for the eval-run artifact with its seed, decoding config, and dataset hash. This chapter installs the ISA 500 evidence discipline, then translates it onto the specific AI artifacts the auditor will be handed in the field: model weights, training and evaluation datasets, eval run artifacts, inference logs, prompt / retriever / tool traces, decoding configs, guardrail configs, monitoring dashboards, incident records, change-management records, vendor attestations.

## ISA 500 in one page, restated

ISA 500 paragraph 6 requires: "The auditor shall design and perform audit procedures that are appropriate in the circumstances for the purpose of obtaining sufficient appropriate audit evidence."

The standard's load-bearing distinctions:

- **Sufficiency** — the measure of the *quantity* of audit evidence. Affected by the auditor's assessment of the risk of material misstatement (higher risk → more evidence needed) and by the quality of the evidence (higher quality → less quantity needed).
- **Appropriateness** — the measure of the *quality* of audit evidence, i.e., its *relevance* and *reliability* in providing support for the conclusion.
- **Relevance** — the logical connection with, or bearing upon, the purpose of the audit procedure and, where appropriate, the assertion under consideration. Evidence may be relevant to one assertion and not another; evidence over the design of a control is not evidence over its operating effectiveness.
- **Reliability** — influenced by source and nature, the circumstances in which it is obtained, and the controls over its preparation and maintenance. ISA 500 paragraph A31 lists generalisations on reliability (restated by AU-C 500 paragraph A32 in essentially identical form):
  1. Evidence from *independent sources outside the entity* is more reliable than evidence from the entity.
  2. Evidence from entity-internal sources is more reliable when the related controls, including over preparation and maintenance, are effective.
  3. Evidence obtained *directly by the auditor* (e.g., observation of control operation, re-performance, independent re-run) is more reliable than evidence obtained indirectly or by inference.
  4. Evidence in *documentary* form (paper, electronic, other) is more reliable than evidence obtained orally.
  5. Evidence from *original* documents is more reliable than from photocopies, facsimiles, screenshots, or documents that have been digitised, filmed, or otherwise transformed.

Those five generalisations, applied to AI artifacts, are the backbone of this chapter.

## The five generalisations on reliability — AI translations

### 1. Independent external sources beat entity sources

- **Beats entity:** a Sigstore-verified signature on the model artifact tying the weights to the build pipeline that produced them; a model-registry record held in a service separate from the model-training service, maintained by a party independent of the ML team (e.g., infra-platform or security); third-party red-team or bias-audit reports authored by a firm with no relationship to the model owner; regulator notices and third-party conformity-assessment reports; Hugging Face / provider-held public cards for GPAI models; W3C / NIST published reference datasets used in eval.
- **Weaker (entity-internal):** the model owner's own model card hosted on their wiki; training logs written to a filesystem the model owner controls; a `metrics.json` committed by the model owner.
- **Audit takeaway:** when the engagement needs to opine on a metric claim, try to secure a path to external corroboration (independent re-run; third-party eval; signed-build attestation) before accepting the entity-internal metric as sufficient on its own.

### 2. Entity-internal evidence is more reliable with effective controls over preparation

- **Beats weaker entity evidence:** eval metrics produced by a CI pipeline where the pipeline definition is in Git, the runner is ephemeral, the model artifact is content-addressed, the dataset is content-addressed, and the metric is logged through a WORM channel (MLflow with retention-locked backing store; a trace store with append-only guarantees). The control environment over the metric's preparation is itself auditable, and the auditor can test those controls.
- **Weaker:** eval metrics pasted into a Google Doc by a model owner on their own laptop, with no record of the run, seed, config, or dataset hash.
- **Audit takeaway:** when the engagement scope includes both operating effectiveness and metric reliability, test the controls over metric *preparation* (CI pipeline, registry, trace store) first; strong controls over preparation let the auditor accept entity-internal metrics with fewer independent re-runs.

### 3. Auditor-obtained evidence beats indirect

- **Beats indirect:** the auditor independently re-runs the eval against the registered model artifact with the registered dataset and the registered decoding config, and compares the result; the auditor directly queries the trace store with a query the auditor authored and pins to the workpaper; the auditor observes the on-call team work a simulated incident.
- **Weaker (indirect):** management's verbal assertion that the eval was run; management's screenshot of the dashboard; a management-authored summary of the incident count for the period.
- **Audit takeaway:** for the assertions that carry the opinion, build the engagement budget to perform at least one auditor-direct procedure (independent re-run, direct query, observation of the control in operation). This is the single procedure that most upgrades the appropriateness of the evidence. Chapter 6 operationalises the re-run as a reproducibility bundle.

### 4. Documentary beats oral

- **Beats oral:** written policy; signed attestation; logged event; committed config; recorded ticket; signed memo of understanding; email with substantive content preserved under the organisation's records-retention policy.
- **Weaker:** conversation. Interview notes are evidence of *the interview*, not of the control.
- **Audit takeaway:** interviews are planning and corroboration tools, not primary evidence. Every substantive control assertion made in an interview is to be reduced to a documentary artifact the auditor can inspect. If the artifact does not exist, the finding is that the artifact does not exist.

### 5. Original beats transformed

- **Beats transformed:** the Git object (commit, tag, signed tag) rather than a screenshot of a diff view; the trace-store record rather than a dashboard screenshot; the signed-tag object rather than a release-notes page; the IAM policy JSON rather than a spreadsheet "export"; the raw eval run artifact (the output file, with the seed and config) rather than a pasted table.
- **Weaker:** the screenshot, the export, the "copy-pasted into a workpaper" value, the printed page scanned back in.
- **Audit takeaway:** when the original is reachable, never accept the transformed. The originals produced in an AI pipeline are *more* original than most financial-audit documentary evidence (content-addressed artifacts, Git-signed tags, cryptographic attestations); failing to work with the original when it exists is a professional-skepticism failure the engagement quality reviewer will flag.

## The AI artifact catalogue — relevance and reliability one artifact at a time

For each artifact the auditor will meet in the field, the questions are the same: *what criterion can this artifact support?* and *how reliable is it under ISA 500?* The table below is the working catalogue for this module; chapter 4 expands it into the engagement-level evidence inventory the workpaper carries.

### Model weights

- **Relevant to:** the identity assertion — "the model deployed in production is the model the eval was run on". The deployment-provenance assertion under EU AI Act Articles 11–12 (technical documentation, record-keeping). The change-management assertion ("no unapproved model changes were deployed in the period").
- **Reliability** — as *entity-produced* artifact, highly variable. Reliable when: the weights are content-addressed (e.g., SHA-256 of the artifact matches the registry record), the registry record is signed (Sigstore, in-toto attestation, GPG-signed tag), and the chain from build pipeline → registry → deployment can be reconstructed from immutable logs. Unreliable when: the weights live only on a developer workstation, the registry is write-wherever, or the "registered" artifact can be overwritten under the same identifier.
- **Procedure:** compute the hash of the deployed artifact; reconcile to the registry; reconcile the registry record to the build pipeline's attestation; reconcile the build pipeline to the Git commit the model owner claims. Any break in that chain is a scope gap or a finding.

### Training, fine-tuning, and evaluation datasets

- **Relevant to:** data-quality and data-governance assertions (ISO/IEC 42001 Annex A controls on data; EU AI Act Article 10); the eval-validity assertion (the eval set is representative, is not contaminated by the training set, and has suitable ground-truth); the fairness and robustness assertions (the eval set covers the protected classes and distribution shifts the organisation has committed to).
- **Reliability** — as *entity-internal*, elevated when the dataset is content-addressed (hash of the dataset manifest + all shards), the datasheet (per Gebru et al.) is pinned to the version, and license / consent / lawful-basis evidence is linked per record or per cohort.
- **Procedure:** verify the dataset hash matches what the eval run consumed; inspect the datasheet; sample records against the claimed lawful-basis or consent artifact; inspect the train/eval overlap check if the organisation runs one (contamination-scan output is itself evidence).

### Eval run artifacts

- **Relevant to:** the metric-claim assertion ("fairness disparity ≤ X on dataset Y", "pass@k ≥ Z on benchmark B", "toxicity rate ≤ W on red-team catalog C"). This is the single most common AI claim the auditor will test.
- **Reliability** — elevated when the run artifact carries, in one bundle: model artifact hash, dataset hash, prompt template hash (for LLM evals), decoding config (temperature, top-p, max tokens, stop sequences), evaluator version (code hash), judge model hash (for LLM-as-judge), seeds, and the full per-item outputs, not only the aggregate. If the evaluator is stochastic (sampling, LLM-judge), elevated further when the run was repeated with different seeds and the variance is reported.
- **Procedure:** re-run the eval from the artifact bundle with the same inputs and compare outputs; if the evaluator is stochastic, re-run with the stated seeds and reconcile; if the re-run does not reconcile, pursue the delta before concluding on the metric claim. Reproducibility bundle shape is covered in chapter 6.

### Inference logs and trace-store queries

- **Relevant to:** operating-effectiveness assertions over the live system — throughput, latency, failure modes, blocked requests, policy-triggered interventions, human-review rates. Many EU AI Act Article 12 (automatic logging) and ISO/IEC 42001 Annex A operational-monitoring controls land here.
- **Reliability** — elevated when the trace store is append-only or versioned, the retention honours the organisation's record-retention policy, the auditor can author and run queries directly against the trace store (not a derived report), and the query itself is pinned to the workpaper (query text + timestamp + result hash). The strongest form is an auditor-written query stored in the audit file and re-runnable on a subsequent engagement.
- **Procedure:** author the query; have the engagement specialist (ISA 620, chapter 3) peer-review the query; run it against the trace store; pin the result file (with a hash) in the workpaper; record the timestamp, the user who executed the query, and the view used.

### Prompt / retriever / tool traces

- **Relevant to:** application-level assertions for retrieval-augmented and agentic systems — the retriever surfaced the correct context; the tool call targeted the correct function with the correct arguments; the prompt template in production matches the governance-approved template; no prompt-injection intervention was bypassed.
- **Reliability** — elevated when the trace captures the full I/O path (query → retriever results → re-ranker scores → final context → prompt → model output → tool calls → tool responses) with content hashes at each hop and a correlation ID; the prompt template version is pinned by hash; the tool-registry version is pinned.
- **Procedure:** sample traces (sampling discipline per chapter 2); inspect against the criterion; re-run a small number end-to-end to validate the trace completeness; reconcile against the governance-approved prompt template and tool registry.

### Decoding configs and guardrail configs

- **Relevant to:** the operating-effectiveness assertion over safety and reliability controls — the production system is running with the governance-approved decoding settings (determinism, temperature caps, max-token limits) and with the governance-approved guardrail suite (input filters, output filters, PII redaction, jailbreak detectors, tool-use allowlists).
- **Reliability** — elevated when the config is Git-tracked, deployed through an infrastructure-as-code pipeline, and the deployed value is auditable at runtime (e.g., a `/_config` endpoint or a snapshot in the trace); reliability drops when the config lives in an ops console editable by anyone with console access.
- **Procedure:** inspect the Git-tracked config at the version the production deployment was cut from; reconcile against the runtime value as retrieved from the system; where both are available, hash-compare; where only runtime is available, reconcile the runtime snapshot to the change log.

### Monitoring dashboards

- **Relevant to:** second-line monitoring assertions — alerting, drift, calibration drift, canary-cohort monitoring, fairness-over-time, latency-SLO, incident-rate.
- **Reliability** — **derivative evidence** (chapter 4). The dashboard is a *view*; the trace store or metrics store underneath is the original. A dashboard screenshot proves only that the view existed at the moment the screenshot was taken.
- **Procedure:** use the dashboard as a map to the underlying query; author or secure the underlying query; pin the query result; the dashboard screenshot may be *corroborative* but is not primary.

### Incident records

- **Relevant to:** incident-management, root-cause-analysis, post-incident-change, regulator-notification, and EU AI Act Article 73 serious-incident-reporting assertions.
- **Reliability** — elevated when the ticket chain is immutable (append-only, or with a visible edit history) and cross-links to the artifact evidence (the model version live at incident, the trace IDs implicated, the change ticket that remediated, the regulator notification sent).
- **Procedure:** inspect the full ticket chain; reconcile to the implicated trace IDs and model versions; verify any mandatory-reporting timeline; corroborate with the communications record (regulator correspondence, customer notifications, status-page history).

### Change-management records

- **Relevant to:** change-control assertions — every production model change (weights, prompt template, retriever config, tool registry, decoding config, guardrail config) is authorised, tested, approved, and recorded.
- **Reliability** — elevated when the change record ties to the artifact hashes on both sides of the change (pre- and post-change), to the approving party's identity, to the testing evidence, and to the deployment timestamp observable in production.
- **Procedure:** select the change-population frame (chapter 2 sampling); for each sample, inspect the ticket, reconcile to artifact hashes, reconcile to deployment evidence, inspect approval identities against the authorisation matrix.

### Vendor attestations

- **Relevant to:** third-party AI assertions — vendor SOC 2 / SOC 3 / ISO/IEC 42001 certificates; vendor model cards; vendor-provided eval reports; vendor security attestations; sub-processor lists under GDPR / DPA.
- **Reliability** — external-source material, in principle more reliable than entity-internal, *but only within the scope the attestation covers*. A vendor SOC 2 scoped to payroll says nothing about the vendor's AI feature. Reliability also drops when the attestation is dated well before the engagement period. Chapter 4 formalises the derivative-vs-original line here; `mod-109` goes deep on third-party assurance.
- **Procedure:** read the attestation's scope and period; reconcile to the controls the engagement is relying on; obtain complementary user entity control (CUEC) listings and confirm the entity executes its side; request bridge letters for periods not covered; where the attestation does not cover the scope in play, pursue separate direct evidence or treat the area as a scope limitation.

## Sufficiency — how much is enough?

ISA 500 does not tabulate "minimum procedures per assertion". Sufficiency is a function of risk, materiality, and the quality already obtained. For AI engagements the practical levers:

- **Higher inherent-risk band on the universe row** (from `mod-103` chapter 1) → more procedures, more direct procedures, more reliance on external sources where available.
- **Higher residual-risk band or weaker control environment** → more substantive testing, less reliance on test-of-controls, more auditor-direct re-performance.
- **Tighter materiality** (from `mod-103` chapter 3) → smaller tolerable-deviation rate → larger sample sizes (chapter 2), more corroboration.
- **Higher-quality evidence per procedure** (external source; auditor direct; original form) → fewer procedures needed to reach sufficiency.
- **First-year engagement or recent control-environment change** → more baseline evidence, less reliance on prior-period work.

The workpaper records the sufficiency judgment explicitly: at the end of each procedure, the auditor documents whether the evidence obtained is sufficient and appropriate for the conclusion, or whether further work is needed. Chapter 5 operationalises that documentation.

## Professional skepticism — ISA 200 anchored, ISA 500 operated

ISA 200 defines professional skepticism as "an attitude that includes a questioning mind, being alert to conditions which may indicate possible misstatement, and a critical assessment of audit evidence". ISA 500 is where skepticism is *operated* — every piece of evidence is challenged for relevance and reliability before being accepted. For AI, three skepticism prompts the auditor runs on every artifact:

1. **Who produced this artifact, and under what controls?** If the producer is the party being audited and the controls over production are weak, demand corroboration.
2. **Is this the original, or a transformation?** If a transformation, name the transformation and reach for the original.
3. **Does this artifact actually address the criterion, or is it adjacent?** A fairness metric on dataset A does not establish the fairness criterion on the production population unless dataset A is representative of that population; the eval set's datasheet is the connective tissue.

Chapter 7 extends skepticism to tampering detection specifically.

## Common failure modes

- **Accepting screenshots as primary evidence.** Dashboard screenshots, model-card excerpts, "copy-pasted into a workpaper" values are all derivative. Reach for the original.
- **Treating the model card as if it were an attestation.** A model card is self-report. Without CI-produced artifacts behind it, it is entity-internal and uncorroborated.
- **Vendor-attestation scope creep.** Relying on a SOC 2 that does not cover the feature in play. Read the scope.
- **Conflating sufficiency with checklist completion.** The standard asks for *sufficient* evidence given the risk, not that every row of a template is filled. Over-procedure on low-risk rows is as much a methodology failure as under-procedure on high-risk rows.
- **Interview-only evidence for substantive controls.** An interview corroborates a document; it does not replace one.
- **Skipping the reliability generalisation ranking at planning time.** The ranking is a planning tool — if the auditor knows the engagement's key assertions and has mapped reliable artifacts to each at planning time, fieldwork is fast; if the ranking is an afterthought in writeup, fieldwork drifts.

## Summary

- ISA 500 / AU-C 500 demand *sufficient* (quantity) and *appropriate* (relevance + reliability) audit evidence. The five reliability generalisations (external > internal, controlled > uncontrolled, direct > indirect, documentary > oral, original > transformed) are the working heuristic.
- Applied to AI, the generalisations map directly onto the artifact catalogue: model weights, datasets, eval runs, inference logs, prompt/retriever/tool traces, decoding and guardrail configs, dashboards, incident records, change records, vendor attestations. Each has a reliability shape that is strongest when the artifact is content-addressed, controlled in preparation, directly obtainable by the auditor, in original form, and corroborated by an independent source.
- Dashboard screenshots and model-card excerpts are derivative. Reach for the underlying trace-store query, the eval run artifact, the signed build attestation, the Git-tracked config.
- Sufficiency is risk-driven. First-year, high-risk, or weak-control engagements need more direct, more external, more auditor-performed procedures. The reproducibility bundle (chapter 6) is the auditor's strongest single upgrade to evidence appropriateness.
- Professional skepticism is operated procedure-by-procedure: who produced it, is it original, does it actually address the criterion? Chapters 2 (sampling), 3 (specialist use), 4 (inventory and grading), 5 (workpaper), 6 (reproducibility), and 7 (chain of custody) build out the rest of the evidence programme on this foundation.
