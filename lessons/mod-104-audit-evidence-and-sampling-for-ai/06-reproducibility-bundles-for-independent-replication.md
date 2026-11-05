# The Reproducibility Bundle — Everything the Auditor Needs to Independently Replicate an AI Claim

## Motivation

A metric claim backed by nothing the auditor can rerun is a claim the auditor has to take on faith. Independent re-performance is the single biggest upgrade from C/B-grade evidence to A-grade under chapter 4's taxonomy, and the five ISA 500 reliability generalisations (chapter 1) rank *auditor-direct* evidence above *entity-reported*. A **reproducibility bundle** is the engineered artifact that makes that re-performance cheap, defensible, and repeatable at inspection time. If the bundle is complete, the auditor can re-run; if the auditor can re-run, the opinion stands on something a stranger could reconstruct years later.

This chapter installs the schema of the reproducibility bundle, the procedure for building one with the model owner (without crossing the first-line boundary), and the peer-role integration points. The deep calibration-methodology work — how the evaluator metric is *defined* — lives at `model-evaluation-engineer` (level 30); the deep application-eval plumbing — how the eval runs in the production pipeline — lives at `ai-eval-engineer` (level 30). The AI Auditor's job is to *consume* those practitioners' calibration and plumbing into an audit-grade bundle that the auditor replicates independently. This chapter is the consumption shape.

## What "reproducible" means in audit

Reproducibility has shades in the ML literature. The audit shade is narrow and operational:

- **Identical reproducibility** — same inputs, same code, same environment → identical outputs. Required for deterministic metrics (e.g., exact-match accuracy with temperature 0 and a pinned seed).
- **Statistical reproducibility** — same inputs, same code, same environment, different seed → outputs within a stated variance band. Required for stochastic metrics (LLM-judge scoring, temperature > 0, retrieval with a tie-break randomness).
- **Operational reproducibility** — same inputs, same code, different environment (different GPU, different CUDA version) → outputs within a wider band. Not usually accepted by audit as the primary band; where it is, the band must be explicitly named and justified.

The bundle is engineered so that the auditor can, by default, hit *identical* reproducibility for deterministic claims and *statistical* for stochastic claims. Falling back to operational is a scope limitation that the workpaper names explicitly.

## The twelve-element bundle schema

Every reproducibility bundle carries these elements, by hash where possible. The schema is the one the auditor pins in the companion repo (chapter 5) under `reproduce/bundle-<assertion-id>/manifest.yaml`.

1. **Assertion identifier** — the specific audit assertion the bundle supports (cross-ref to criterion register and workpaper node).
2. **Model artifact hash** — SHA-256 of the model weights (or the full artifact set for sharded/LoRA/adapter models). For hosted-model claims (OpenAI, Anthropic, Google, Mistral), the provider's **model name and version string** at the time of run plus the provider-side identifier returned by the API (request ID, model string echoed in the response). Pin the identifier the provider will honour months later; chapter 7 covers the chain-of-custody hashing when the underlying model may be mutated by the provider.
3. **Seed(s)** — numerical RNG seeds for every stochastic component (Python `random`, NumPy, PyTorch / TF, decoding-sampler, data-loader shuffler, dropout where applicable). Seeds are not optional; a missing seed converts the bundle from reproducible to best-effort.
4. **Decoding config** — for generative models: temperature, top-p, top-k, repetition penalty, max tokens, stop sequences, system-prompt text (hashed). For hosted models, the full API request body (with keys redacted) hashed.
5. **Prompt template(s)** — exact text, with placeholders named; hashed. If multi-turn, the full turn structure. If retrieval-augmented, the template the retriever's context is spliced into.
6. **Retriever config and index** — for RAG systems: embedding model identifier and hash; the document-store identifier and the content hash of the index snapshot used at run time; the chunking scheme; the retriever's parameters (k, score threshold, re-ranker if present).
7. **Tool versions** — for agentic systems: the tool registry version (hashed), each tool's version and function signature, the tool's authentication context (if relevant).
8. **Dataset hash** — the content hash of the evaluation dataset, including per-shard hashes if split; the dataset's datasheet pinned.
9. **Evaluator code** — the code that computes the metric, identified by Git commit + file path + line range, or by a signed release; included in the bundle (not referenced only) when the code is small enough.
10. **Metric definition** — the metric's name, the citation to its definition (academic paper, industry standard, internal spec), and the exact formula applied. For LLM-as-judge metrics, the judge model identifier plus the judge prompt template hashed; for proxy metrics, the proxy spec.
11. **Environment lock** — the full package lock (requirements.txt frozen, `poetry.lock`, `pip freeze`, `conda env export --no-builds`); the Python/runtime version; the OS and kernel if load-bearing; the hardware class (CPU / specific GPU model) and driver versions; container image digest if run in a container.
12. **Run command and run output** — the exact command invoked (`run.sh`), the start/end timestamps, the stdout/stderr log, and the per-item outputs (not just aggregates), stored losslessly. The aggregate metric is in the bundle but is derivable from the per-item outputs.

### Manifest YAML shape

```yaml
bundle_id: RB-033
assertion_id: C.07-fairness-french-cohort
assertion_summary: >
  Refusal-rate delta between English and French cohorts within 2 pp on trailing 30-day basis.
model:
  name: in-house/chatbot-llm
  version: 2026.09-r3
  artifact_sha256: 3d7a…
  registry_ref: mlflow://prod/chatbot-llm/2026.09-r3
seeds:
  python: 20261118
  numpy: 20261118
  torch: 20261118
  decoder: 20261118
decoding:
  temperature: 0.2
  top_p: 0.9
  max_tokens: 512
  stop: ["<END>"]
  system_prompt_sha256: a1f5…
prompt_template:
  file: prompts/chatbot_prod.jinja2
  sha256: 7e09…
retriever:
  embedder: text-embedding-3-large
  embedder_hash_or_version: "v3"
  index_snapshot_sha256: 4bc2…
  top_k: 8
  reranker: null
tools: null
dataset:
  manifest_sha256: e83a…
  datasheet: datasets/chatbot_eval_v7_datasheet.md
evaluator:
  repo: ai-auditor-eval
  commit: 1c2f4d9
  path: src/fairness/refusal_rate.py
  entry: compute_refusal_rate_delta
metric:
  name: refusal_rate_delta_pp
  definition: internal/metrics/refusal-rate-delta.md
  formula: "|refusal_rate(cohort_en) - refusal_rate(cohort_fr)| * 100"
environment:
  python: 3.11.9
  os: Ubuntu 22.04 LTS
  gpu: NVIDIA L40S
  cuda: 12.4
  pip_lock: env/requirements.lock
  container_digest: sha256:deadbeef…
run:
  command: "bash run.sh"
  started_at: 2026-11-19T10:04:21Z
  finished_at: 2026-11-19T10:37:14Z
  log: logs/run.log
  outputs_per_item: outputs/per_item.parquet
  aggregate: outputs/aggregate.json
signoff:
  preparer: <auditor>
  reviewer: <lead-auditor>
  specialist: <isa-620-specialist>
hash_chain_entry: manifests/hash-chain.jsonl:line-204   # chapter 7
```

Yaml is illustrative; the schema can be in any machine-readable format the engagement team adopts. The *fields* are load-bearing.

## Building the bundle — procedure

The bundle is built jointly with the model owner but *owned by the auditor*. The first-line boundary (`mod-101` chapter 1) is preserved by having the owner **produce** the artifacts under their own controls and the auditor **collect, verify, and independently execute**. The auditor does not reach into the owner's pipeline and change settings.

Stepwise:

1. **Scope the assertion.** Name the exact claim the bundle will support. One bundle per assertion is a sane default; some bundles cover multiple related metrics if the inputs are identical.
2. **Request the inputs.** From the model owner: model artifact (or identifier for hosted models), dataset manifest, prompt template, retriever config and index snapshot, decoding config, tool registry, env lock, container image digest. The auditor records the request; the owner's response time is itself audit evidence (control-effectiveness signal).
3. **Verify hashes and completeness.** The auditor computes hashes independently; reconciles to the owner's attestations; verifies that the env lock resolves (pip install -r the lock in a clean container) without the owner's help.
4. **Pin seeds.** The auditor sets the seeds — not the owner — to defeat cherry-picking. For stochastic metrics, run with ≥3 seeds and report variance.
5. **Author evaluator code or verify the owner's.** For simple metrics (accuracy, pass@k, exact match), the auditor's own evaluator is often cheaper and more defensible. For complex metrics (group fairness with cohort definitions, LLM-as-judge with calibrated rubrics), the auditor adopts the owner's evaluator *with specialist (ISA 620) review* and verifies the code's exact-match reproduction on a small inspection set.
6. **Run the bundle.** In the auditor's environment, with the auditor's pinned seeds, against the owner's artifacts, with the auditor's evaluator. Record run-time, outputs, logs.
7. **Reconcile.** Compare the auditor's result to the owner's reported result for the same bundle. Identical for deterministic; within the stated statistical band for stochastic. Any reconciliation gap is an audit workpaper line requiring resolution before conclusion.
8. **Sign and store.** Chapter 7 operationalises hash-chaining and WORM storage of the bundle.

## Peer roles — who owns what, and the auditor's reuse shape

Reproducibility bundling has first-line and second-line practitioners whose craft the auditor consumes rather than re-authors.

- **`model-evaluation-engineer` (level 30) — calibration methodology.** This role owns the *definition* of the metric, the *calibration* of evaluators (including LLM-judges), and the *statistical properties* of the metric under repeated runs. The AI Auditor consumes this role's output as the metric-definition pointer in the bundle (element 10). When the engagement needs to opine on whether the calibration itself is defensible, the ISA 620 specialist (chapter 3) is often someone with this role's background.
- **`ai-eval-engineer` (level 30) — application-eval plumbing.** This role owns the *production* eval plumbing — the CI pipeline that runs evals, the trace-store wiring, the dataset refresh, the evaluator-version management. The AI Auditor consumes this role's output as the env lock, the run artifacts, and the trace-store queryability (elements 11 and 12). When the eval plumbing is itself the control under test, this role's output is the evidence.
- **`ai-risk-engineer` (level 25) — fairness/robustness/privacy/guardrail craft.** This role owns the *harness and the test catalog* for the engineering-craft metrics. The AI Auditor consumes the harness output and inspects the harness itself under the controls (chapter 1 generalisation 2).
- **`ai-evaluation-engineer` (level 35) — release-assurance decisions.** This second-line role owns the *release gate* methodology. The AI Auditor audits whether the gate operated — not re-decides what passes the gate.

The reuse principle: the AI Auditor does not re-author any of these roles' artifacts in-engagement. The auditor pins what they produced, replicates what the engagement requires replicating, and if the roles have not produced what the engagement needs, the finding is that the roles have not produced what the engagement needs.

## Hosted-model and provider-side artifacts

When the model under test is a hosted foundation model (Anthropic, OpenAI, Google, Mistral, Cohere, Azure OpenAI, Bedrock, Vertex), the bundle cannot include the weights. The audit discipline is to pin what the provider commits to and corroborate what the provider does not:

- **Pin the provider's model identifier** as returned by the API — e.g., `claude-opus-4-7`, `claude-sonnet-4-6`, `gpt-4-turbo-2024-04-09`. Store the full request/response headers for a representative call in the bundle.
- **Pin the provider's response schema** at the time of run. Providers evolve their schemas; a schema snapshot is corroborating evidence of the response shape.
- **Verify the provider's published model card** matches the version string, and store the card version hash.
- **Read the provider's deprecation and model-update policy.** Providers may silently update models under the same version string; reproducibility windows shrink accordingly. The engagement must either run within a window the provider commits to, or accept a scope limitation and document it.
- **Pin the API client library version and the provider SDK version.** Server-side changes aside, client-side changes alter decoding semantics.
- **Corroborate with provider SOC 2 / provider audit reports** for the operating-effectiveness controls the engagement is relying on.

Where the provider offers deterministic decoding modes (e.g., a `seed` parameter) the bundle pins them; where they do not, the bundle documents the non-determinism and runs with ≥3 random seeds to characterise variance.

## Specialist execution under ISA 620

Chapter 3 covers specialist use; here is the bundle-specific hand-off:

- **Specialist peer-reviews the bundle manifest** before run — catches missing seeds, under-specified decoding, environment-lock gaps.
- **Specialist executes the run** in high-complexity engagements; the auditor evaluates the specialist's output under ISA 620 §12.
- **Specialist reconciles reconciliation gaps** when the auditor's re-run does not match management's claim — the specialist's technical interpretation is the input to the auditor's resolution.

The specialist's attached deliverable is a workpaper node; the bundle is a companion-repo artifact. Chapter 5's cross-reference discipline keeps the two tied.

## The single-page bundle-complete checklist

For every bundle, before closing:

- [ ] Assertion identifier matches the criterion register and workpaper node.
- [ ] Model artifact or hosted-model identifier pinned with provider-side identifier when hosted.
- [ ] Seeds for every stochastic component.
- [ ] Decoding config (temperature, top-p, max tokens, stop, system prompt hash).
- [ ] Prompt template hashed.
- [ ] Retriever config and index snapshot hashed (if RAG).
- [ ] Tool registry version and per-tool hashes (if agentic).
- [ ] Dataset manifest hashed; datasheet pinned.
- [ ] Evaluator code identified by commit/path/entry.
- [ ] Metric definition linked and the exact formula stated.
- [ ] Environment lock resolvable from scratch; container digest pinned if used.
- [ ] Run command, start/end timestamps, log, per-item outputs, aggregate.
- [ ] Reconciliation against management's claim, with any gap resolved in a workpaper line.
- [ ] Preparer / reviewer / specialist sign-off.
- [ ] Hash-chain entry (chapter 7).

A bundle that does not clear the checklist is not audit-ready — it is a draft that should not bear load on the opinion.

## Common failure modes

- **Missing seeds.** The bundle cannot be re-run deterministically; subsequent variance is attributed to randomness when it may be code drift.
- **"Latest" model version pin.** `gpt-4-turbo-latest` is not a version; it is a moving target.
- **Env lock that does not resolve.** The auditor cannot install the dependencies cleanly; the re-run is on a different environment than the owner's.
- **Evaluator code only referenced by file path.** Without a Git commit, the file at the path may have changed since the run.
- **Metric formula only in prose.** "We measured fairness" is not a formula.
- **Dataset hash but no datasheet.** The hash fixes the bits; the datasheet fixes their meaning. Without the datasheet, the engagement cannot defend representativeness.
- **Hosted-model identifier without response-header capture.** The provider may change the model under the identifier; the headers are the only proof of what was returned on the audit's run.
- **Reconciliation gap waved away.** The auditor's re-run differs from the owner's by 0.4 pp; the engagement says "within noise". If the engagement did not run with multiple seeds to establish the noise band, "within noise" is a guess.
- **Bundle stored only in the electronic WP system.** Binary-unfriendly systems may corrupt large artifacts; the Git-tracked companion (chapter 5) is the native home.

## Summary

- The reproducibility bundle is the engineered artifact that makes independent re-performance cheap, defensible, and repeatable at inspection time — the single largest upgrade from C/B-grade evidence to A-grade in chapter 4's taxonomy.
- The twelve elements of the bundle: assertion identifier, model artifact hash, seeds, decoding config, prompt template, retriever config and index, tool versions, dataset hash, evaluator code, metric definition, environment lock, run command and output.
- Bundle construction is joint with the model owner but owned by the auditor; the auditor pins the seeds, verifies hashes, authors or verifies the evaluator, and runs independently. The first-line boundary is preserved.
- Peer-role integration: `model-evaluation-engineer` (level 30) owns calibration-methodology depth; `ai-eval-engineer` (level 30) owns application-eval plumbing; the auditor consumes without re-authoring.
- Hosted-model bundles pin the provider's model identifier, the response headers, and the client-library version — reproducibility windows shrink with provider mutation.
- ISA 620 specialists peer-review and often execute the run; the lead auditor retains sole responsibility for the opinion.
- Clear the one-page checklist before closing the bundle; a bundle that does not clear is a draft and must not bear load.
- Chapter 7 chains the bundle into the engagement's tamper-evident custody record.
