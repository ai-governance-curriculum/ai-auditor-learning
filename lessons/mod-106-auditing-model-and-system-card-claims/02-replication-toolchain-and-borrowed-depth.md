# The Replication Toolchain — Using Borrowed Depth Without Re-authoring It

## Motivation

The auditor is an *independent replicator*, not a researcher. The role runs existing evaluations against the system under audit using tooling the broader AI assurance community has already built. Three peer roles own the depth:

- **`ai-risk-engineer` (L25)** — authors novel attacks, red-team catalogs, threat-model expansions.
- **`ai-eval-engineer` (L30)** — authors application-eval harnesses, plumbs CI/CD for evaluations, curates production trace populations.
- **`model-evaluation-engineer` (L30)** — authors the statistical methodology (CIs, agreement measures, power, effect sizes) the auditor applies downstream.

Frontier depth — novel capability-eval authoring, agentic-safety research — sits with `agentic-safety-engineer` (L40). The AI-auditor's job is to *invoke* those bodies of work, not reproduce them. Overreach wastes audit budget, exceeds the independence posture (an auditor who authors novel attacks against the subject matter is now consulting), and exposes the engagement to competence-attack during QA.

This chapter installs the toolchain the auditor uses out of the box, maps each tool to the claim families from chapter 1, and names the borrowing contract that keeps the replication defensible.

## The toolchain inventory

The AI assurance community has converged on a short list of open-source tools. The auditor should be fluent in invoking each — command-line or Python API — and able to produce a pinned, replicable run artifact. Depth of *why* lives in the peer tracks.

### LLM safety and red-team evaluation

| Tool | Steward | Auditor use |
|------|---------|-------------|
| **garak** | NVIDIA (originated by Leon Derczynski) | Scanner-style LLM probe suite; multiple probe families (DAN jailbreaks, prompt injection, data leakage, toxicity); runs against OpenAI / Anthropic / HF endpoints with JSON report output. Auditor invokes `garak --model_type … --probes …`, archives the JSON, pins the garak release tag. |
| **PyRIT (Python Risk Identification Toolkit)** | Microsoft AI Red Team | Framework for generative-AI red teaming; orchestrates attack prompts and scoring across a target endpoint; persists conversations and scores to a backing store. Auditor runs stock attack strategies and archives the memory DB. |
| **Promptfoo** | Promptfoo project | Prompt / LLM eval runner with YAML configs; the de-facto tool for policy-derived application evals in CI/CD. Auditor consumes vendor's Promptfoo configs and reruns them. |
| **Inspect** | UK AI Security Institute (AISI) | Framework for LLM evals used by AISI itself and increasingly by frontier labs for shared evaluations; supports agent evals, graded scoring, and multi-turn tasks. <!-- needs-research: at reading time confirm the current AISI name (renamed from AI Safety Institute to AI Security Institute in 2025) and the Inspect release the audit should pin --> |

### Adversarial ML

| Tool | Steward | Auditor use |
|------|---------|-------------|
| **ART (Adversarial Robustness Toolbox)** | IBM / Linux Foundation AI & Data (Trusted AI) | Full-stack adversarial-ML library — evasion, poisoning, inference attacks, defences — across TF / PyTorch / sklearn / XGBoost / Keras. Auditor invokes evasion attacks (FGSM, PGD, C&W) against the vendor's reported robustness-budget claims. |
| **TextAttack** | QData (University of Virginia) | NLP adversarial-attack framework; packaged attacks (TextFooler, BERT-Attack, DeepWordBug, PWWS). Auditor replays reported attack success rates against the system under audit. |
| **CleverHans** | Goodfellow et al. (originally Google); now community-maintained | Classic reference adversarial-attack library. Auditor uses it when the subject matter's robustness claim cites a CleverHans attack by name. |
| **Counterfit** | Microsoft (archived upstream) | Automation layer over ART / TextAttack for black-box attacks. Auditor uses it where the vendor explicitly references Counterfit; otherwise prefer ART directly. <!-- needs-research: confirm Counterfit's maintenance status at reading time — Microsoft archived the public repo in late 2023 --> |

### Fairness and explainability

| Tool | Steward | Auditor use |
|------|---------|-------------|
| **Fairlearn** | Fairlearn project (Microsoft-sponsored) | Group-fairness metrics (demographic parity, equal opportunity, equalized odds) and mitigation algorithms. Auditor uses it for metric replication. |
| **AIF360 (AI Fairness 360)** | IBM / LFAI | Broader fairness-metric catalog, including disparate-impact ratio, Theil index, consistency. Auditor cross-checks against Fairlearn for independence. |
| **Holistic AI** | Holistic AI (open-source library plus commercial platform) | NYC LL144-shaped bias-audit toolkit; bundles selection-rate ratio, mean-score-ratio, impact-ratio computation. |
| **SHAP** | Lundberg et al. | Shapley-based explanations. Auditor uses it to reproduce the card's claimed feature-importance explanation or to probe an unexplained decision. |
| **Alibi** | Seldon | Explainability (counterfactuals, anchors, ALE) + outlier / drift detection. |
| **LIME** | Ribeiro et al. | Local surrogate explanations; auditor reproduces card-claimed local explanations. |

### Privacy

| Tool | Steward | Auditor use |
|------|---------|-------------|
| **Opacus** | Meta PyTorch team | DP-SGD trainer; the auditor does not retrain, but inspects the accountant output and the privacy-budget manifest the vendor should produce from Opacus. |
| **TensorFlow Privacy** | Google | DP-SGD trainer for TF; same inspection role as Opacus. |
| **ML Privacy Meter** | NUS Secure and Trustworthy ML group | Membership-inference and attribute-inference attack toolkit; auditor replicates MIA TPR@FPR against the vendor's claimed privacy posture. |
| **Presidio** | Microsoft | PII detection / anonymisation; auditor uses it to test a deployed data-minimisation claim. |

### Supply-chain and provenance

| Tool | Steward | Auditor use |
|------|---------|-------------|
| **Sigstore / Cosign** | OpenSSF / Linux Foundation | Signature verification for model artifacts and eval bundles. Auditor verifies vendor-signed artifacts; see `mod-104`. |
| **Hugging Face Hub metadata & revisions** | Hugging Face | Pin-by-commit for model and dataset artifacts (`revision=`); the auditor's primary artifact-integrity tool when the subject is on HF. |

The claim register from chapter 1 points into this toolchain: a Grade A performance claim on SWE-bench Verified lands in Inspect or the SWE-bench harness; a Grade A refusal claim on HarmBench lands in the HarmBench harness or garak; a Grade A fairness claim lands in Fairlearn or Holistic AI; and so on.

## The borrowing contract

Each tool was built by a peer community. The auditor borrows two things:

1. **Attack / metric / procedure correctness.** The community has validated the attack implementation, the metric definition, the harness scoring. The auditor does not need to re-prove these; attempting to do so is scope-creep and violates the role-depth boundary.
2. **Default configurations.** The tool's defaults encode community judgement about reasonable budget, iterations, sample sizes. The auditor runs defaults first, documents any deviation as a scope restriction.

In return the auditor owes:

- **Pin everything.** Tool version (release tag), model version (commit hash), dataset version, decoding config, seed, environment (OS, Python, CUDA/CPU, driver). An unpinned run is not evidence.
- **Archive the raw artifact.** Not only the summary metric: the entire run log, raw predictions, per-sample scores, evaluator trace.
- **Attribute.** Every finding the auditor reports cites the tool, its version, and (where appropriate) the originating paper. Reviewers who do not see "HarmBench 2024-03 release, run under Inspect vX.Y with greedy decoding seed 42" will push back.
- **Do not fork.** If a tool's behaviour appears wrong, file an upstream bug (or flag as a scope restriction); do not patch and rerun within the audit. A patched toolchain is not "the tool the vendor used" and the delta becomes unprovable.

## The role-depth boundary — what the auditor does NOT do

The auditor:

- Does **not** author novel adversarial payloads. If a new attack is needed to test a claim, the finding is "insufficient tooling to independently verify" or "escalate to `ai-risk-engineer` for attack authoring" — not "I will author the attack on the engagement."
- Does **not** author novel fairness metrics. Fairness-metric authoring and selection *rationale* sit in `ai-risk-engineer` / `model-evaluation-engineer`; the auditor tests whether the vendor's chosen metric fits the obligation (chapter 5).
- Does **not** author novel statistical procedures. Bootstrap, kappa, power analysis land as *applied* methodology (chapter 4); novel estimator design is `model-evaluation-engineer` depth.
- Does **not** author novel red-team catalogs. The auditor runs HarmBench, AIR-Bench, AgentDojo, and the vendor's policy-derived suite; expansion of the catalog is `ai-risk-engineer` work.
- Does **not** run frontier capability elicitation. Autonomous-replication, cyber-offense uplift, biothreat uplift — these are `agentic-safety-engineer` and the vendor's responsible-scaling framework; the auditor reads the resulting report as a claim document.

This is a feature, not a limitation. The auditor's independence depends on not becoming a second-line engineer within the engagement.

## Environment pinning and the replication manifest

Every replication run must produce a manifest that an independent reviewer can read and, in principle, rerun on a different machine with the same result (modulo known nondeterminism). A minimum manifest:

```yaml
replication_manifest:
  engagement: ACME-2026-AIAUDIT-Q4
  claim_id: M-PERF-003
  claim_source: "ACME Falcon-X Model Card v2.1, 2026-09-01, sha256:…"
  target:
    vendor: ACME
    model: falcon-x-7b
    revision: "hf.co/ACME/falcon-x-7b@abc1234"
    endpoint: api.acme.ai/v1/chat (if closed-weights)
    api_version: "2026-10-15"
  tool:
    name: inspect
    version: "0.3.52"
    repo: "github.com/UKGovernmentBEIS/inspect_ai@v0.3.52"
  benchmark:
    name: swe-bench-verified
    revision: "github.com/princeton-nlp/SWE-bench@verified-2024-08"
    sha256: "…"
  decoding:
    temperature: 0
    top_p: 1
    max_tokens: 4096
    seed: 42
  environment:
    os: "Ubuntu 22.04 LTS"
    python: "3.11.9"
    cuda: "12.4 / driver 550.90"
    hardware: "1x A100-80GB (AWS p5.48xlarge, 1 of 8 isolated)"
  judge:
    model: n/a (programmatic grading)
  run:
    started_at: "2026-11-05T14:23:11Z"
    duration_s: 11420
    command: "inspect eval swe_bench_verified --model acme/falcon-x-7b …"
    log_sha256: "…"
  result:
    metric: pass@1
    value: 0.472
    sample_size: 500
    bootstrap_ci_95: [0.432, 0.511]
  delta_vs_claim:
    card_value: 0.487
    delta: -0.015
    delta_within_claim_ci: true
  signed_by: "L. Auditor, CPA; 2026-11-05T15:02:11Z, cosign-sig:…"
```

The replication manifest is a first-class audit workpaper, stored alongside the raw artifact in WORM-compatible storage (see `mod-104`). Every finding that cites a metric result references the manifest ID.

## Nondeterminism — a reality the manifest must disclose

Replicating an LLM eval to two significant digits is rarely possible. Nondeterminism enters from:

- sampling (temperature > 0, top-p, top-k);
- parallel inference on accelerators (floating-point associativity varies with batch composition);
- vendor-side load balancing between model variants on closed-weights endpoints;
- framework updates that change tokenizer or BOS behaviour between benchmark release and replication;
- benchmark revisions (dataset additions, scoring-script fixes).

The auditor's discipline is to pin what can be pinned, declare what cannot, and report the replication delta against the *appropriate noise floor*:

- Greedy decoding + fixed seed + pinned model = delta on the order of 0.1–0.3 pp due to framework-level nondeterminism.
- Sampling decoding = delta on the order of 1–3 pp per run; the auditor runs multiple seeds and reports the mean with a CI.
- Closed-weights API with hidden routing = delta of several pp is common; the auditor is explicit that the metric is "API behaviour on date X," not "model Y behaviour."

The *result-within-claim-CI* test is the primary adjudication (chapter 4 operationalises the statistics). A single-run delta outside the claim CI is not yet a finding; a pattern of out-of-CI runs, or a claim published without a CI, is.

## When a tool is wrong for the claim

Occasionally the vendor's card cites a benchmark or attack that the auditor's chosen tool implements with a known drift. Three disciplines:

1. **Run the exact tool the vendor named first.** If the card says "HarmBench at the 2024-03-01 release run under their own harness," the auditor runs *that* release and *that* harness. A general-purpose wrapper (e.g., garak's HarmBench probe) is a cross-check, not the primary.
2. **Record toolchain drift as a scope restriction.** If the vendor's cited tool version is unobtainable (archived release, broken dependency, retracted paper), the auditor runs the nearest available version, pins it, and reports the substitution as a limitation in the report (chapter 7).
3. **Do not substitute silently.** If the finding compares "HarmBench ASR" from the vendor's run to "garak HarmBench probe ASR" from the auditor's run, the comparison is not valid without an explicit methodological note.

## Common failure modes

- **Running "a HarmBench" instead of "the HarmBench the vendor ran."** Many evaluators offer a HarmBench probe; most do not reproduce the canonical harness. The comparison falls apart on cross-examination.
- **Not archiving the raw per-sample output.** Only a summary metric survives; the auditor cannot defend the finding against a vendor challenge.
- **Patching the tool mid-run.** A tweaked tool is not the tool. If a patch is needed, the engagement is blocked until the patch is upstreamed or the finding is restated as an inability-to-verify.
- **Mistaking a tool's default ε for the vendor's ε.** Adversarial-budget mismatches are a common source of false-delta findings. Always pin budgets to the card claim.
- **Overclaiming authorship.** The auditor who writes "I red-teamed the model and found …" where in fact they ran garak's DAN probe has introduced independence and credit misrepresentations at once. Attribute cleanly.
- **Pulling frontier-lab system-card red-team claims apart tool-by-tool.** Some claims are only verifiable through the vendor's assurance workflow (eval-set access + judge-model access); tool-only replication will mis-grade the claim. Record the inability and escalate the vendor-walkthrough procedure (`mod-109` on third-party audit).

## Summary

- The auditor's replication toolchain is an off-the-shelf set — garak, PyRIT, Promptfoo, Inspect; ART, TextAttack, CleverHans, Counterfit; Fairlearn, AIF360, Holistic AI, SHAP, Alibi, LIME; Opacus, TensorFlow Privacy, ML Privacy Meter, Presidio — invoked with pinned versions and defaults.
- Attack authoring, metric design, and statistical-methodology authoring sit with peer roles; the auditor's independence depends on borrowing those outputs rather than reinventing them.
- Every replication produces a signed manifest (tool, version, model revision, decoding, seed, environment, raw artifact hash, signed by the auditor) and lives in WORM-compatible storage.
- Nondeterminism is real; pin what can be pinned, declare what cannot, and test deltas against the claim's CI where published (and against the auditor's bootstrap CI otherwise).
- Where the vendor-cited tool is unavailable or drifts, record the substitution as a scope restriction rather than silently cross-tool compare.
