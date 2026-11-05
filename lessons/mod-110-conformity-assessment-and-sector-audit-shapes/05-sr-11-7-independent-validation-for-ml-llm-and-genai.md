# SR 11-7 — Independent Validation Adapted for ML, LLM, and GenAI Models

## Motivation

The US Federal Reserve's **Supervisory Letter SR 11-7** and its OCC parallel **OCC Bulletin 2011-12** — jointly titled **Supervisory Guidance on Model Risk Management** — are the controlling standard for model governance at Fed-supervised and OCC-supervised institutions (large banks, bank holding companies, savings associations). Issued in 2011 and never numerically superseded, SR 11-7 is the lingua franca of US-bank **Model Risk Management (MRM)**. Non-bank regulated institutions (asset managers, insurers, broker-dealers, fintechs with bank-like supervision, and increasingly non-US financial regulators) have adopted SR-11-7-shaped frameworks as *de facto* practice.

SR 11-7 introduces three concepts the auditor returns to on every engagement:

1. **Effective challenge.** Model risk should be managed "with a critical analysis by objective, informed parties" — an independent-validation function with the authority, incentives, and competence to challenge model use.
2. **Three elements of validation.** Every model needs conceptual soundness evaluation, process verification, and ongoing monitoring, with outcomes analysis to complete the assessment.
3. **Model definition and tiering.** A model is a "quantitative method, system, or approach" producing an output; model risk is tiered by use, complexity, and consequence.

For ML, LLM, and GenAI systems used at Fed-supervised institutions — credit models, fraud models, AML/CTF models, trading models, customer-service LLMs, underwriting LLMs, compliance-automation LLMs — SR 11-7 remains the controlling guidance. **SR 23-4** (interagency guidance on third-party relationships, `mod-109` chapter 2) extends SR 11-7's reach to vendor-provided AI, and specific supervisory letters (SR 23-5, SR 22-3, SR 20-6) and the 2024 interagency reaffirmation have re-emphasised SR 11-7's application to ML/AI without replacing it. <!-- needs-research: confirm the current state of interagency AI/ML model-risk guidance at reading time, including any specific letter or clarifying guidance published after SR 11-7 that supplements the ML/AI treatment -->

The auditor arrives here as **the independent-validation function**, as the **internal auditor over MRM**, or as an **independent third-party model validator** retained by the bank. This chapter is the auditor's shape for the SR 11-7 engagement adapted to ML/LLM/GenAI: the model-inventory and tiering test, the three elements of validation, effective challenge, and the governance posture around the validation report.

## The SR 11-7 object: what is a model?

SR 11-7 defines a **model** as a "quantitative method, system, or approach that applies statistical, economic, financial, or mathematical theories, techniques, and assumptions to process input data into quantitative estimates." The key features are:

- **Input data** (observed or constructed).
- **A theory/technique layer** (statistical, economic, financial, mathematical; by extension, machine-learning architectures and language-model generation).
- **An output** (quantitative estimate or decision aid).

Under this definition, ML models for credit scoring, fraud detection, AML transaction monitoring, risk ratings, and marketing are clearly in scope. **LLMs** are in scope when used to produce outputs that influence financial decisions — automated adverse-action letter generation, automated underwriting narrative drafting, extraction of financial quantities from unstructured text, Q&A on regulated content. **GenAI** productivity tools used purely for internal convenience (meeting summaries) are typically out of scope; GenAI used in a customer-facing or risk-decision path is in scope.

Audit-test shape: for each AI/ML system claiming to be out of scope, the bank must produce a documented scoping analysis against the SR 11-7 definition. The auditor reperforms the scoping against the actual use; "out of scope" is a defensible position only when the system does not produce outputs that influence a decision reached in the definition.

## The model inventory

SR 11-7 requires a comprehensive **model inventory** maintained by MRM. The inventory records, at minimum:

- Model identity (name, version, model-ID).
- Purpose and intended use.
- Tier (risk ranking; see below).
- Owner (business line), developer (technology/data-science team), validator.
- Approved uses and prohibited uses.
- Life-cycle status (development, active, retired, suspended).
- Validation status (last validation, next validation, findings status).
- Dependencies (upstream models, data sources, infrastructure).

For ML/LLM/GenAI additions:

- Model family / foundation-model identity (e.g., GPT-4o-2024-08-06, Claude 3.5 Sonnet, Llama-3 70B fine-tune v2.3).
- Training-data lineage (dataset identity, provenance, consent basis, retention).
- Fine-tuning or adaptation history.
- Guardrail / filter layer identity and versions.
- Deployment infrastructure.

The inventory is the engagement's **sampling frame**. The auditor reperforms it with three sweeps (akin to the vendor sweeps of `mod-109` chapter 2): procurement / expense reconciliation, identity-and-access-management reconciliation (API-key issuance, model-registry access), and engineering-team interview. Shadow models — ones in production but not inventoried — are structural findings.

## Model tiering

SR 11-7 expects **tiering** that proportionalises MRM scrutiny by risk. Typical tiering factors:

- **Materiality / consequence.** The size of the decisions the model influences; dollar impact; customer impact.
- **Complexity.** The opacity of the method; model interpretability; dependency chain depth.
- **Use intensity.** Volume of decisions per period; coverage of the decision.
- **Regulatory sensitivity.** Credit models under FCRA / ECOA / Reg B; AML models under BSA; fair-lending exposure; consumer-protection exposure.

ML/LLM/GenAI uplifts to the tiering:

- **Opacity uplift.** Neural models have less interpretable internals than linear regressions; an LLM output path is further obscured; the tiering methodology should weight opacity.
- **Change velocity uplift.** Vendor GPAI model changes (model-version swaps) and self-training updates increase model-risk velocity; the tiering should trigger shorter validation cycles or ongoing-monitoring intensity.
- **Data-contamination uplift.** LLMs are trained on uncontrolled corpora; the possibility of contamination with task-relevant data (e.g., the bank's own prior adverse-action decisions) elevates risk of memorisation and leakage.
- **Hallucination / confabulation uplift.** LLMs can produce confident outputs disconnected from input; a tier escalation for LLM use is defensible if the output is consumed as fact.
- **Adversarial exposure uplift.** Public-facing LLM endpoints face prompt injection and jailbreak attempts; the tiering should reflect customer-facing vs. internal-only.

Audit-test shape: the tiering methodology document (does it cover these ML/LLM-specific factors?); application of the methodology to each sampled model (does the tier assigned in the inventory match the auditor's independent application?); escalation logic (does the methodology name triggers for tier change, including LLM-specific triggers like vendor model-version swap?).

## The three elements of validation

### 1. Conceptual soundness

SR 11-7's first validation element asks whether the model is **appropriate for its intended use** given the theory, technique, data, and assumptions. For traditional models this is a review of the statistical or mathematical form; for ML/LLM, the analogue is review of the architecture, training procedure, and fitness-for-purpose.

ML-adapted conceptual-soundness tests:

- **Choice of architecture.** Was the architecture family (gradient-boosted tree, deep neural, transformer fine-tune, RAG over foundation model, agent on tool-use loop) defended against alternatives?
- **Training data appropriateness.** Does the training data match the operational data distribution in population, time, and feature definitions? Covariate shift between train and prod is a conceptual-soundness red flag.
- **Label quality.** For supervised ML, are labels reliable? For LLMs with preference training, is the RLHF signal well-calibrated to the operational decision?
- **Input features / prompts.** Are features (for ML) or prompts (for LLM) complete and non-leaking?
- **Assumptions.** What assumptions underlie the model's validity (e.g., stationarity, independence, representativeness)? For LLM use, the assumption that retrieval returns the relevant chunk; the assumption that the model's output is grounded.
- **Benchmarks.** Comparison to simpler models (logistic regression, rule-based, keyword-match) — is the complex model demonstrably better, or does its additional risk not buy enough performance?
- **Fit-for-purpose for the specific decision.** A model that performs well on a research benchmark may not perform well on this bank's specific decision environment.

### 2. Process verification

Process verification tests whether the model is **implemented as intended**. The developer's claim about what the model is must match what the production code and infrastructure actually do.

ML-adapted process-verification tests:

- **Code review.** Model pipeline code; feature-engineering code; preprocessing code; postprocessing code. The validator reperforms the pipeline on a known input and verifies output.
- **Build reproducibility.** From the same data, code, and seeds, the same model is produced. For large LLMs, bit-for-bit reproducibility is infeasible; the validator tests procedural reproducibility (the training recipe is sufficient to reproduce a model with equivalent distributional properties).
- **Data-pipeline integrity.** Training, validation, and test splits are disjoint and not mutually contaminated; feature values at inference match feature values at training; transform functions are consistent.
- **Deployment correspondence.** The model artifact in production is the one that was trained and validated; model signing / provenance evidence attests to this (chapters cross-ref `mod-109` chapter 6).
- **Guardrails and filters.** Pre/post inference layers (prompt-injection filters, PII filters, refusal classifiers, output-grounding checks) are present, configured, and operational.
- **Integration with decisioning.** The model's output reaches the decision layer in the form the model was validated to produce; downstream code does not alter the output in untested ways.

### 3. Outcomes analysis

The third element compares the model's actual performance in production against **expected performance** from development. This is the operational-monitoring plank and connects tightly to `mod-108` chapter 2 (monitoring-evidence audit).

ML-adapted outcomes-analysis tests:

- **Operational performance tracking.** Accuracy, calibration, AUC, PR, business KPIs — tracked per period with alerting on drift.
- **Fairness monitoring.** Per-group performance maintained over time; comparisons to reference periods; triggers for formal re-examination.
- **Hallucination / grounding metrics (LLM).** Factuality tests; grounding-score; abstention-rate; retrieval-hit-rate for RAG.
- **Benchmark comparison refresh.** Periodic re-benchmarking against simpler alternatives to confirm continued incremental value.
- **Backtest against held-out operational periods.** For models that score on past data (credit, fraud), continued predictive validity against new vintages.
- **Challenger-model comparison.** A challenger model is maintained alongside the champion to produce comparison evidence.

### Ongoing monitoring

SR 11-7 insists validation is continuous, not point-in-time. The validator must specify:

- **Monitoring metrics and thresholds.**
- **Review cadence** — monthly, quarterly, annually, dependent on tier.
- **Re-validation triggers** — threshold breaches, upstream vendor model changes (for GPAI providers' vendor swaps), material changes in the business environment, periodic.
- **Governance escalation** — where monitoring findings escalate when thresholds are breached.

## Effective challenge

SR 11-7's conceptual core is **effective challenge**: validation must be performed by parties who are *objective* (independent of model development and use), *informed* (competent to challenge the specific model), and *influential* (their findings must have consequence — remediation, use restriction, retirement).

Audit-test shape:

- **Independence.** The validator does not report to the model developer or the business user; the validator's compensation and career are not contingent on the model's continued use.
- **Competence.** The validator's team includes competence in the specific ML/LLM/GenAI techniques; for frontier-model use, the validator can bring external expertise (SR 11-7 contemplates use of external experts).
- **Authority.** The validator can require remediation; the validator can withhold approval; the validator's findings have a recorded path to resolution.
- **Incentives.** The validator is not financially dependent on the business line whose model is being validated; the validation function is funded as a cost of MRM, not as a chargeback from the business.

Effective challenge is the aspect SR 11-7 enforcement most often focuses on; a validation function with high throughput and no findings is a red flag.

## Model-risk governance

SR 11-7 extends validation into a governance structure:

- **Policy and procedures.** An approved model-risk-management policy, with procedures for model development, validation, approval, monitoring, change management, retirement.
- **Roles and responsibilities.** Named roles: model developer, model owner, model user, model validator, MRM function head, senior-management risk committee.
- **Internal audit.** Internal audit covers the MRM function itself — not the individual models, but the function's adherence to policy and operation of effective challenge. SR 11-7 is explicit that internal audit's role is oversight of MRM, not duplication of validation.
- **Board reporting.** MRM reports to senior management and the board; LLM-era reporting typically includes an AI-specific attestation on top of traditional model-risk reporting.
- **Vendor models.** SR 23-4 attaches to vendor-provided models; the MRM function evaluates vendor diligence, contract terms, and ongoing monitoring; vendor validation does not substitute for the bank's own validation but can be relied on where diligence supports it.

## The validation report

The engagement output is the **validation report**. SR 11-7 does not prescribe a template; the typical structure that supervisory examiners expect:

1. **Scope and objective.** Model identity, use, tier, validation period, validation activities performed.
2. **Conceptual soundness.** Findings on data, method, assumptions; benchmark comparisons; limitations.
3. **Process verification.** Findings on code, pipeline, deployment, guardrails.
4. **Outcomes analysis.** Operational performance; drift; fairness; business impact; monitoring adequacy.
5. **Overall validation conclusion.** Approved for use with or without conditions; not approved; approved with remediation on specified timeline.
6. **Limitations.** Model risks the validator identifies that are accepted by the business; evidence of acceptance.
7. **Findings and remediation.** Each finding with severity, owner, due date, closure criterion.
8. **Appendices.** Workpapers, data analyses, supporting technical content.

The report is signed by the lead validator and approved per the MRM function's authority structure; it is retained for examination and for the next validation cycle.

## Integration with other audit shapes

- **SR 23-4 (`mod-109` chapter 2).** Vendor-model engagements weave SR 11-7 (for the model itself) with SR 23-4 (for the vendor relationship).
- **EU AI Act (chapter 1).** A Fed-supervised institution operating in the EU may have a model simultaneously subject to SR 11-7 and to EU AI Act Article 43; the audits complement rather than substitute.
- **NAIC (chapter 7).** Insurers adopt SR-11-7-shaped frameworks because of the NAIC Model Bulletin's parallel expectations; chapter 7 picks up the insurer-specific overlay.
- **FDA GMLP (chapter 6).** Healthcare-fintech institutions touching SaMD-adjacent products may face both SR 11-7 and FDA GMLP; chapter 9 defends the shape choice.
- **SOC-for-AI (chapter 8).** The bank's own control attestation for AI may rest on an SSAE 18 SOC-for-AI report; SR 11-7 validation does not substitute but can feed the SOC.

## Common failure modes

- **Scoping LLMs out as "not models".** Bank treats LLMs as productivity tools; a customer-facing LLM producing adverse-action narratives is a model under SR 11-7 regardless of label.
- **Shadow models.** ML artifacts in production but not in the inventory; credit-decision shadow analytics are a frequent finding.
- **Tiering stale under vendor-swap regime.** Tier assigned based on first-period use; vendor swaps model versions; tier is not re-evaluated.
- **Conceptual soundness ignored for "black-box" models.** The validator declares the model unassessable and defers to performance; SR 11-7 requires conceptual-soundness evaluation regardless of opacity.
- **Process verification perfunctory.** Code review is a sampling of files; pipeline reperformance is not attempted; production correspondence is not demonstrated.
- **Outcomes analysis absent for small-volume models.** "We don't have enough data to monitor" is not a defence; the validator must declare how monitoring will happen and on what cadence.
- **Monitoring runs but produces no action.** Thresholds are breached and the breach is logged; no remediation follows; the "effective challenge" plank fails.
- **Validation findings closed by assertion.** Developer asserts remediation; validator closes without retest; next cycle shows the issue persisted.
- **Vendor model relied on without own validation.** Vendor's validation accepted at face value; SR 11-7 requires the bank's own validation for its own use context.
- **Internal audit duplicates model validation.** Internal audit should oversee MRM function; duplicating model-level validation is a resource misuse and a signal that effective challenge is not working at the validation layer.

## Summary

- SR 11-7 (with OCC 2011-12) is the controlling model-risk-management guidance at US-bank-supervised institutions; non-bank financial regulators and non-US financial regulators have adopted SR-11-7-shaped frameworks as *de facto* practice.
- The guidance centres on effective challenge (objective, informed, influential validation), the three elements of validation (conceptual soundness, process verification, outcomes analysis), ongoing monitoring, and a model-inventory with tiering proportional to risk.
- ML/LLM/GenAI adaptations preserve the shape and add specific factors — architecture choice defence, training-data appropriateness, guardrail testing, hallucination / grounding metrics, vendor-model-swap triggers, customer-facing adversarial exposure.
- The validation report presents scope, the three elements, overall conclusion, limitations accepted by the business, and findings with remediation; it is signed and retained for examination.
- SR 11-7 interfaces with SR 23-4 (vendor models), EU AI Act Article 43 (dual-regulated systems), NAIC (insurer parallel), FDA GMLP (healthcare-fintech), and SOC-for-AI (chapter 8 attestation); chapter 9 disposes of combinations by engagement shape.
- Common failure modes include scoping LLMs out, shadow models, stale tiers under vendor-swap, perfunctory process verification, outcomes analysis absent for small-volume models, and validation findings closed by assertion rather than retest.
