# exercise-06: Reproducibility Bundle for One Independent Replication

**Estimated effort:** 2 hours

## Objective

Design the full reproducibility bundle the audit team needs to independently replicate one management claim about an AI system, and author the `manifest.yaml`, the `run.sh`, the environment-lock file, and the reconciliation workpaper. The deliverable is the complete bundle that chapter 6's one-page checklist would clear, together with the evaluator-code specification the audit team would hand to its ISA 620 specialist.

## Prerequisites

- Chapter [`06-reproducibility-bundles-for-independent-replication.md`](../06-reproducibility-bundles-for-independent-replication.md)
- Chapter [`03-isa-620-using-the-work-of-an-ml-specialist.md`](../03-isa-620-using-the-work-of-an-ml-specialist.md) — for the specialist hand-off
- Chapter [`05-authoring-workpapers-electronic-and-git-tracked.md`](../05-authoring-workpapers-electronic-and-git-tracked.md) — for the companion-repo placement

## Scenario

Pick **one** of the two claims below and build the bundle for it.

### Claim A — Benchmarked accuracy on an in-house model

Organisation: a mid-sized logistics company. Model: a classical-ML delivery-time predictor (`etadiff/xgboost-eta-v4.1`). Claim: "The model's mean absolute error on the 2026-Q3 held-out evaluation set is ≤ 6.5 minutes." Supporting artifacts the engagement has access to:

- The model artifact in an MLflow registry (hashable).
- The 2026-Q3 held-out evaluation dataset, hashed, stored in content-addressed object storage.
- The evaluator Python script `eval/eta_mae.py` in the organisation's `delivery-ml` GitLab repo.
- A `requirements.txt` and a Docker image tag (`delivery-ml-eval:2026.09-r1`) the model owner uses for CI.
- The last run output in MLflow with the aggregate MAE of 6.12 minutes.

The engagement wants to independently reproduce the MAE claim and reconcile.

### Claim B — Refusal-rate delta on a hosted-LLM chatbot

Organisation: a mid-tier bank. System: a customer-service chatbot built on Anthropic's hosted `claude-opus-4-7`. Claim: "Across the audit period 2026-01-01 through 2026-09-30, the refusal-rate delta between the English-language cohort and the French-language cohort was within 2 percentage points on a trailing 30-day basis, except for the window 2026-07-08 through 2026-07-20 (acknowledged exception)." Supporting artifacts:

- The trace-store (BigQuery table `trace_store.chatbot_v2`) with per-request records including the provider-returned `model` identifier, request headers, prompt template SHA, and response text.
- A refusal classifier (`refusal-classifier` in a GitHub repo) that the organisation uses internally to tag refusal responses; hashable.
- The organisation's prompt-template repository (private GitHub).
- A monthly fairness report (PDF) authored by the model owner.
- The chatbot's deployment manifest in the IaC repo (Terraform).

The engagement wants to independently measure the delta on an auditor-selected sample, and to verify the exception window is truly bounded as claimed.

## Requirements

1. **Scope the bundle.** State the specific assertion the bundle supports, the audit criterion it ties back to (from your engagement's criterion register), the reproducibility shade required (identical / statistical / operational — chapter 6 §What "reproducible" means in audit), and which ISA 500 reliability generalisation(s) the bundle advances.
2. **Author `manifest.yaml`.** Fill in every one of the twelve bundle elements per chapter 6 §The twelve-element bundle schema. Where the scenario does not specify (e.g., exact Docker image digest, exact MLflow URI), use realistic placeholder values clearly marked. For the hosted-model claim (B), explicitly pin: the provider's model identifier, the provider's response-header capture discipline, and the provider SDK version.
3. **Author `run.sh`.** The exact command the auditor runs — including container launch (if used), environment activation, data retrieval from content-addressed storage, evaluator invocation, and output capture. Idempotent; re-runnable from the companion repo clone alone.
4. **Author the environment-lock file** (`requirements.lock` or `env.yaml`) at the level of specificity the engagement needs for identical reproducibility. For the hosted-model claim, include the SDK version pin.
5. **Specify the evaluator code.** For claim A, verify that the organisation's `eta_mae.py` reproduces the claim exactly on a small inspection set (describe the test) *before* trusting it on the full set. For claim B, author the specification for an auditor-authored refusal-rate-delta evaluator (inputs, outputs, formula, edge cases — language-detection confidence threshold, missing-response handling, trailing-window computation).
6. **Specify the specialist hand-off.** Per chapter 6 §Specialist execution under ISA 620, name what the ISA 620 specialist peer-reviews on the manifest, what the specialist executes (if anything), and what the lead auditor evaluates against ISA 620 §12.
7. **Reconciliation workpaper.** Author the short reconciliation workpaper (one page, Markdown) that compares the auditor's re-run output against management's claim. Include: identical/within-band expectation, actual observed delta or MAE, any deltas and their qualitative analysis, and the conclusion on the assertion.
8. **Clear the chapter-6 checklist.** Produce the explicit checklist, marking each item.

## Starter guidance

- Chapter 6 §The twelve-element bundle schema is the template; follow it closely.
- Claim A is the easier shape: deterministic evaluator, in-house model, well-formed environment lock. Focus on the artifact hashes, evaluator-code pinning, env lock, and reconciliation.
- Claim B is the harder shape: hosted model with potential provider mutation, stochastic responses, trailing-window computation, cohort definition. The reproducibility shade is *statistical* for the per-item refusal classification (seeded over classifier non-determinism) and more carefully *operational* over the provider's responses in the historical window (the auditor does not re-call the provider over the period; the auditor re-measures from the trace store's captured responses). State this clearly.
- For claim B, the refusal-rate-delta evaluator needs a clear definition of:
  - How a trace is classified as a refusal (classifier output + score threshold).
  - How the language cohort is assigned (field in the trace store, or a language-detector applied by the auditor).
  - How the trailing-window is computed.
  - How missing records or malformed responses are handled.
- The Docker image digest is content-addressed (e.g., `sha256:deadbeef…`); do not use a floating tag.
- For the hosted-model identifier (claim B), the trace-store's captured `model` field is the pin — not the current state of the provider's model page.
- Where the scenario underspecifies (exact SDK version, exact repo URL, exact BigQuery schema), use `<!-- needs-research -->` or clearly-marked placeholders.
- The reconciliation workpaper is short; a strong one is three or four paragraphs and a decision line.

## Acceptance criteria

The deliverable is accepted when:

- All twelve bundle elements are present and populated with realistic content or clearly-marked placeholders.
- The reproducibility shade is explicitly stated and matches the actual bundle design.
- The `run.sh` is idempotent, re-runnable from the companion-repo clone, and includes output capture.
- The environment-lock file pins versions at the depth the shade requires.
- The evaluator-code section either verifies the organisation's evaluator on an inspection set (claim A) or specifies an auditor-authored evaluator in full (claim B).
- The specialist hand-off names specific review scope (what the specialist checks on the manifest) and the lead auditor's ISA 620 §12 evaluation points.
- The reconciliation workpaper compares auditor result to management claim with named thresholds, deltas, qualitative analysis, and conclusion on assertion.
- The chapter-6 one-page checklist is produced with each item marked.
- For claim B, the hosted-model provider identifier is pinned from the trace-store, the SDK version is pinned, and the operational-vs-statistical reproducibility treatment of provider responses is explicit.
- `<!-- needs-research -->` placeholders are used rather than invented values.
- No fabricated metrics, benchmarks, or vendor identifiers beyond the scenario.

## Stretch goals

- Author the **variance characterisation plan** (claim A: are MAEs stable across seeds and env variants; claim B: how many seeds and classifier restarts are needed to bound the refusal-classifier's variance).
- Draft the **failed-reproduction protocol** — what the engagement does if the auditor's MAE differs from management's by more than the engagement's tolerable delta. Which workpapers are affected; which interviews are convened; how a scope limitation might be invoked.
- Propose a **continuous-reproducibility bundle** — a periodic job that re-runs the bundle each quarter and lands the result in WORM, turning the one-engagement bundle into a standing control.
- For the hosted-model claim (B), author the **provider-deprecation readiness note** — what the engagement does when the provider announces deprecation of `claude-opus-4-7` mid-way through the audit period and the auditor can no longer re-call it. Chapter 6 §Hosted-model and provider-side artifacts has the groundwork.
