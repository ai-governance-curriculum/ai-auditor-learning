# Auditing the Guardrail Program

## Motivation

Guardrails are the runtime barrier between an LLM / agentic system and the harms its unmoderated output would cause. They are the production equivalent of the red-team catalogue (chapter 3): where red-teaming proves a harm *can* happen in principle, guardrails prevent the harm from happening in production. For the auditor the guardrail programme is the single most visible risk-management artefact to the end user — the guardrail's refusal, redaction, or tool-blocking behaviour is what an affected individual experiences directly.

The auditor's job is to test the *architecture* of the guardrail programme against OWASP LLM Top 10 risks, to validate the *calibration evidence* (false-positive / false-negative rates) of classifier guardrails, to confirm vendor-guardrail controls where the organisation has outsourced parts of the stack, and to trace guardrail findings back to the register and the monitoring plan.

As elsewhere, guardrail authoring sits with `ai-risk-engineer` (L25). The auditor tests sufficiency and reliability.

## The three-layer guardrail architecture

A canonical guardrail architecture has three layers; the auditor tests each separately.

### Input guardrail

Operates on the user's (or document's, or tool's) input before the model sees it:

- **Pattern-based input filters.** Regex / allowlist / denylist for known malicious input patterns.
- **Classifier input filters.** An ML classifier that scores the input for adversarial intent (jailbreak, injection, abuse).
- **Policy-based input routing.** Routes high-risk inputs to a stricter model, a human reviewer, or a block response.
- **Context contamination detection.** Detects indirect-prompt-injection candidates in retrieved documents or tool outputs.

Audit tests:

- **Coverage.** Each OWASP LLM Top 10 category that applies to the input path is addressed.
- **Latency budget.** The input guardrail adds a measured latency; the budget is declared and monitored.
- **Bypass audit.** For a sample of blocked inputs, the auditor confirms the block is correct; for a sample of allowed inputs, the auditor confirms allowance is defensible.
- **Logging.** Input-guardrail decisions are logged (with privacy considerations — the raw input may contain PII, so retention policy matters).

### Output guardrail

Operates on the model's output before the user sees it:

- **Content classifier.** PII, CSAM, NCII, hate, self-harm, violence, sexual content, political-content classifiers.
- **Grounding check.** For RAG systems, whether the output is supported by the retrieved context; chapter 1 of mod-108 covers the production monitoring overlap.
- **Policy check.** Scope-of-use check — did the user ask something the system's policy says it won't answer.
- **Structural check.** Output is well-formed per the schema the downstream expects.
- **Safe-completion.** Output is a safe-refusal where the input triggered a refusal rule.

Audit tests:

- **Classifier coverage.** The content-classifier portfolio covers the harm model's content-based harms.
- **Calibration.** Each classifier has reported FPR / FNR on a representative sample; see the calibration section below.
- **Refusal-rate drift.** The monitor watches for refusal-rate drift and alerts on anomalies (`mod-108`).
- **Logging.** Output-guardrail decisions are logged alongside the input and the model output.

### Tool guardrail

Operates on the agentic system's tool-use plan before the tool fires:

- **Allow-list of tools and parameters.** The system cannot call tools not on the allow-list, cannot call tools with arguments outside the declared schema.
- **Dangerous-action confirmation.** Destructive / financial / network-egress tool calls require a confirmation step (user-in-the-loop or policy-engine confirmation).
- **Rate limiting.** Per-tool, per-session, per-user rate limits.
- **Egress policy.** Tools whose execution talks to outside systems are gated against a declared egress allow-list.
- **Sandboxing.** Code-execution tools run in a sandbox with declared permissions.

Audit tests:

- **Allow-list present and reviewed.** The allow-list is version-controlled and reviewed on a cadence.
- **Confirmation enforced.** Dangerous actions require confirmation in deployed code (not just policy).
- **Egress constraints enforced.** Tools' network calls are verifiable to the allow-list.
- **Sandbox evidence.** Code-execution tools have a documented sandbox with declared permissions and escape-testing evidence.
- **Red-team linkage.** AgentDojo / InjecAgent findings against the deployment have corresponding tool-guardrail updates.

## The OWASP LLM Top 10 coverage test

For each OWASP LLM Top 10 category, the auditor expects guardrail coverage:

| OWASP LLM | Risk | Expected guardrail coverage |
|-----------|------|------------------------------|
| LLM01 | Prompt injection (direct + indirect) | Input classifier; context-contamination detection; tool allow-list |
| LLM02 | Sensitive information disclosure | Output PII classifier; output content classifier; policy refusal |
| LLM03 | Supply-chain | Model-and-component SBOM; vendor attestation (`mod-109`) |
| LLM04 | Data / model poisoning | Training-data provenance; model-integrity verification (Sigstore / Cosign on model artefacts) |
| LLM05 | Improper output handling | Structural-check output guardrail; sanitisation of outputs before downstream systems |
| LLM06 | Excessive agency | Tool allow-list; dangerous-action confirmation; blast-radius limits |
| LLM07 | System-prompt leakage | Output classifier for system-prompt tokens; policy refusal |
| LLM08 | Vector / embedding weaknesses | Retrieval-poisoning detection; embedding-model provenance |
| LLM09 | Misinformation | Grounding check; disclaimer / uncertainty expression in output |
| LLM10 | Unbounded consumption | Rate limits; cost caps; quota enforcement |

<!-- needs-research: confirm the OWASP LLM Top 10 edition number and category phrasing at reading time; the Top 10 has had multiple revisions since 2023 release -->

The auditor builds the coverage table from the organisation's architecture documentation and tests each row with an evidence sample.

## The classifier-guardrail calibration test

Output classifiers are only as good as their calibration. The auditor expects, for each deployed classifier:

- **Declared tool identity and version.** Which model (Llama Guard 3 / 4, ShieldGemma, OpenAI Moderation, Constitutional Classifiers, Anthropic claude-moderation, Google Perspective API, Azure Content Safety, AWS Comprehend content moderation, custom-trained classifier) and the exact version / revision. <!-- needs-research: confirm Llama Guard version (3 vs 4), ShieldGemma release state, and Constitutional Classifiers public availability at reading time -->
- **Calibration dataset.** The organisation has a representative calibration set — a benchmark the classifier is tested against, with ground-truth labels, covering the deployment's harm categories.
- **Reported FPR and FNR per category.** False-positive rate (benign inputs misclassified as harmful) and false-negative rate (harmful inputs missed) per category, not just aggregate.
- **Threshold choice.** The classification threshold for block / allow is documented, and the trade-off between FPR and FNR at that threshold is reported.
- **Re-calibration cadence.** Classifiers are re-calibrated on a cadence (per model update, per declared period).
- **Adversarial robustness.** Chapter 4's adversarial-ML discipline applies to classifiers; the auditor confirms the classifier has been tested against TextAttack / jailbreak prompts.

### The FPR / FNR trade-off audit

Classifier guardrails sit on an operating curve. A classifier at 95% recall has some false-positive rate; at 99% recall, more. The auditor tests:

- **The organisation's chosen operating point.** Explicit, reviewed, signed.
- **The user-experience impact.** High FPR degrades the user experience (over-refusal); the organisation has declared an FPR budget and the monitor watches for over-refusal.
- **The safety consequence.** High FNR allows harmful content through; the monitor watches for FNR drift.
- **The per-category operating points.** Child-safety categories often operate at higher recall (even at higher FPR) than lower-severity categories; the auditor confirms the differential is justified.

### The chapter-5 fairness-of-classifier test

Classifiers have fairness properties: a hate-speech classifier that flags African-American English as hate at higher FPR than general English has a fairness problem of its own. The auditor runs the chapter-5 subgroup-breakdown analysis on the classifier's error profile where protected-class information is available in the calibration set.

## The vendor-guardrail test

Many organisations use commercial guardrail platforms — Lakera, Arthur, Robust Intelligence, Calypso AI, HiddenLayer, Protect AI, and others — either as the full guardrail layer or as a supplementary classifier. The auditor's vendor-guardrail tests are a specific application of `mod-109`'s third-party programme:

- **Vendor identity and contract.** Record the vendor, the contracted service, and the SLA.
- **Vendor attestations.** SOC 2, ISO 27001, ISO 42001 if available, the vendor's own red-team / robustness / fairness evidence.
- **Scope.** What the vendor's classifier covers and does not cover; where the vendor's scope leaves gaps the organisation must plug with internal controls.
- **Calibration data exchange.** Whether the vendor provides per-deployment calibration data on the organisation's representative traffic (or only generic benchmark data).
- **False-positive / false-negative evidence.** Vendor-produced or independently measured.
- **Data-handling terms.** User inputs sent to the vendor for classification — is PII handled, where is data stored, retention period, sub-processor list.
- **Model-change notification.** The vendor pushes updates to its classifier; the organisation's monitoring detects behaviour change and the contract commits the vendor to advance notice.
- **Exit plan.** If the vendor deprecates, mis-prices, or fails attestation, the organisation can replace them without a safety gap.

<!-- needs-research: confirm which vendors are active and at what tier at reading time — the vendor list in this chapter is representative, not exhaustive, and the market moves quickly -->

A vendor-guardrail that is undocumented in the organisation's architecture is a supply-chain finding (and feeds `mod-109`).

## The classifier portfolio — what to recognise

The current landscape includes:

- **Llama Guard (Meta).** Open-weights content-safety classifier; Llama Guard 3 and 4 released by Meta AI; licence per Meta terms. Commonly deployed as output filter on open-weights LLMs.
- **ShieldGemma (Google).** Open-weights safety classifier from Google DeepMind. <!-- needs-research: confirm ShieldGemma release state at reading time -->
- **OpenAI Moderation API.** Managed service; multi-category classifier.
- **Constitutional Classifiers (Anthropic).** Published research shape where classifier is trained from a constitution; auditor confirms public availability and licence terms at reading time. <!-- needs-research: confirm Constitutional Classifiers public availability / API surface at reading time -->
- **Google Perspective API.** Toxicity classifier at scale; one of the oldest.
- **Azure AI Content Safety.** Managed classifier; multi-category.
- **AWS Bedrock Guardrails.** Managed guardrail layer.
- **NVIDIA NeMo Guardrails.** Open-source framework for multi-step guardrails.
- **Guardrails AI, LLM Guard, Lakera Guard, Arthur Shield, Robust Intelligence, Calypso AI, HiddenLayer, Protect AI.** Open-source frameworks and commercial platforms the organisation may reference.

The auditor should recognise these by name and, more importantly, know which test shape applies to each (open-weights classifier → reperform FPR/FNR directly; managed API → read the vendor's published data and request per-deployment calibration; framework → test the configured policy).

## The guardrail-evasion test

Guardrails are themselves a red-team target. The auditor confirms the red-team programme (chapter 3) includes:

- **Jailbreak attempts against the output classifier.** Prompts that elicit harmful content past the classifier.
- **Encoding / obfuscation attacks.** Base64, leet-speak, Unicode confusables used to defeat regex or classifier matching.
- **Indirect-injection via retrieval.** Documents that defeat input-guardrail detection.
- **Multi-turn attacks.** Attacks that split the harmful request across conversation turns; the input guardrail may miss the intent on any single turn.
- **Tool-use manipulation.** Attacks that trick the agent into making tool calls the allow-list would block if posed directly.

For each class, the auditor records the last-run date, the attack-success-rate, and the mitigation closure (chapter 3's triage pattern).

## Logging, observability, and incident interface

A guardrail programme is only useful if its decisions are observable. The auditor tests:

- **Per-decision logging.** Each guardrail decision (input filter, output filter, tool filter) is logged with input / output / decision / reason / classifier-version / timestamp.
- **Retention.** The log is retained for the declared period; privacy considerations may require redaction before long-term storage.
- **Alerting.** Metric-driven alerts: refusal-rate drift, allow-rate drift, high-severity block spikes, vendor-classifier error-rate spikes.
- **Incident interface.** Guardrail breaches route to the incident channel (`mod-108`) within the declared response window.
- **Replay.** Decisions are replayable for post-hoc analysis (the input and the classifier state can be re-run to reproduce the decision).

A guardrail that cannot be replayed is a forensic weakness; the auditor reports it as a `mod-104` evidence finding.

## Linkage to the register, the red-team programme, and the monitoring plan

As with every chapter in this module, guardrail findings must cross-reference:

- **Register.** Each OWASP LLM Top 10 risk has a register row (chapter 2) that cites the guardrail as its control.
- **Red-team programme.** Chapter 3's coverage matrix has rows that specifically test the guardrails.
- **Adversarial-ML programme.** Chapter 4's attacks include attacks against classifiers in the guardrail layer.
- **Fairness programme.** Chapter 5's subgroup analysis is applied to each classifier.
- **Privacy programme.** Chapter 6's PII-pipeline is one of the guardrails.
- **Monitoring plan.** `mod-108`'s metrics include guardrail refusal-rate / allow-rate / drift.

A guardrail finding that does not land in all the places above is itself a traceability finding.

## Common failure modes

- **One guardrail layer only.** Input but no output, or output but no tool guardrail.
- **Vendor classifier with no calibration data.** The organisation trusts the vendor's generic numbers for its own traffic.
- **Classifier FPR not measured.** The programme reports FNR (safety) but not FPR (over-refusal / UX cost).
- **Thresholds drift silently.** Classifier threshold is tuned by a team member without the review / sign-off per chapter 2.
- **Tool allow-list diverges from code.** The documented allow-list no longer matches the production code.
- **Guardrail decisions not logged.** The programme cannot replay or audit.
- **System-prompt treated as a guardrail.** The system prompt is not a security boundary; relying on it instead of classifier / policy enforcement is a design finding.
- **Per-user bypass undocumented.** Admin / internal-user accounts bypass guardrails without a traceable authorisation record.
- **Chapter-5 fairness not applied to classifier.** The hate-speech classifier is deployed without subgroup-error analysis.

## Summary

- Guardrail architecture has three layers — input, output, tool — each separately tested for coverage, calibration, and logging.
- OWASP LLM Top 10 coverage is the completeness grid; each category must have a documented guardrail control.
- Classifier guardrails are tested for FPR / FNR per category, operating-point sign-off, and re-calibration cadence; subgroup error-profile analysis applies.
- Vendor guardrails are a `mod-109` third-party sub-engagement — attestation, scope, data-handling, exit plan.
- Guardrails are a red-team target; chapter 3 must test guardrail evasion directly.
- All decisions are logged, retained per policy, alertable, and replayable; absence of these is a `mod-104` evidence finding.
- Findings cross-reference to the register, the red-team tracker, the adversarial-ML programme, and the monitoring plan.
