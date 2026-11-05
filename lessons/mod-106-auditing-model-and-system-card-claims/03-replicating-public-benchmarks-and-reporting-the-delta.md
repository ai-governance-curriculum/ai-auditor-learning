# Replicating Public Benchmarks and Reporting the Signed Delta

## Motivation

Public benchmarks are the backbone of card-level performance and safety claims. When a vendor writes "pass@1 of 48.7 on SWE-bench Verified" or "97% refusal on HarmBench," they are inviting (or at least allowing) anyone to re-run the same harness and compare. The auditor takes the invitation. The replication is simple in principle — point the harness at the system under audit, record what comes back — and arbitrarily complex in practice because every benchmark has a canonical configuration, a scoring script, a cadence of upstream fixes, and implicit assumptions about how the model is accessed.

This chapter indexes the benchmarks the AI-auditor track is expected to replicate, names the known configuration choices each imposes, and installs the *signed delta* reporting shape the engagement uses to communicate the comparison.

## The benchmark roster

The following benchmarks appear in card claims frequently enough that the auditor should be competent to replicate them. Depth of why each benchmark matters lives in the `ai-risk-engineer` / `ai-eval-engineer` tracks; the auditor's responsibility is correct invocation and correct reporting.

### HarmBench

- **What it is.** A standardised evaluation framework for automated red-teaming of LLMs, covering a catalog of harmful behaviours across categories (cybercrime, bioweapons, misinformation, harassment, etc.). Published with a paper and reference harness (Mazeika et al., 2024, arXiv 2402.04249). <!-- needs-research: cite the current HarmBench release at reading time, including the behaviour taxonomy count and the official harness repo; the catalog expands -->
- **Metrics.** Attack Success Rate (ASR) per attack method on the target behaviour set; refusal rate as the complement.
- **Auditor configuration.** Run the vendor's declared attacks against the vendor's declared behaviour subset; pin the HarmBench release and the attack-model harness revision; use the published classifier or judge model for ASR scoring.
- **Common gotchas.** ASR differences between greedy and sampling decoding can exceed 10 pp; the judge model's version drifts; some attack categories require large-context behaviour that short-context deployments cannot host.

### AIR-Bench 2024

- **What it is.** The AI Risks Benchmark (Zeng et al., 2024) — a regulation-grounded prompt set mapped to risk categories distilled from eight sets of government regulation and sixteen corporate AI policies. <!-- needs-research: confirm current AIR-Bench release, number of prompts, and the risk taxonomy at reading time -->
- **Metrics.** Safety refusal rate per risk category; aggregate safety score.
- **Auditor configuration.** Run the full prompt set against the system under audit, score with the published rubric or judge, report per-category rates.
- **Common gotchas.** A high aggregate score can mask a low category-level score; the auditor reports per-category deltas, not just the headline.

### AgentDojo

- **What it is.** An evaluation framework for prompt-injection and indirect-prompt-injection robustness of tool-using agents (Debenedetti et al., NeurIPS 2024).
- **Metrics.** Attack success rate against injected goals; benign task completion rate under attack.
- **Auditor configuration.** Only applicable to agent systems (tool-use loops with external content). Pin the task suite, injection suite, and scoring version.
- **Common gotchas.** The system under audit may route tool calls differently than the AgentDojo reference; the auditor must document the integration glue and treat its correctness as part of the subject matter.

### InjecAgent

- **What it is.** A benchmark for assessing LLM agents' resistance to tool-based prompt-injection attacks (Zhan et al., ACL 2024).
- **Metrics.** Injection success rate across attack types; targeted-goal success rate.
- **Auditor configuration.** Similar to AgentDojo; often run as a cross-check.
- **Common gotchas.** Overlap with AgentDojo invites double-counting; the auditor reports each separately.

### WMDP (Weapons of Mass Destruction Proxy)

- **What it is.** A multiple-choice benchmark proxy for dangerous knowledge in biosecurity, cybersecurity, and chemistry (Li et al., 2024, arXiv 2403.03218).
- **Metrics.** Accuracy per sub-benchmark (wmdp-bio, wmdp-cyber, wmdp-chem); unlearning-evaluation metrics where applicable.
- **Auditor configuration.** Run the official scoring; if the vendor claims an unlearning mitigation, measure pre- and post-mitigation (vendor must provide both model variants).
- **Common gotchas.** WMDP is a proxy; the auditor's replication result speaks only to the proxy, not to the underlying hazard — report that limitation explicitly.

### MLCommons AILuminate

- **What it is.** An industry-benchmark for safety and hazard evaluation of general-purpose chat systems, published by MLCommons AI Safety Working Group (2024/2025). <!-- needs-research: confirm current AILuminate release version and the hazard taxonomy at reading time; the benchmark is evolving rapidly -->
- **Metrics.** Hazard scores per category, graded by the AILuminate rubric.
- **Auditor configuration.** Follow the MLCommons published protocol; pin to the version the vendor cites.
- **Common gotchas.** Private test-set components exist to prevent gaming; the auditor replicates only the public portion unless the vendor opens the private portion under NDA; disclose which.

### Meta CyberSecEval

- **What it is.** An evaluation suite from Meta for LLM-generated code and cyber-security-related tasks (CyberSecEval 1/2/3) — insecure code generation, prompt injection, cyber-attack-helpfulness. <!-- needs-research: at reading time inventory which CyberSecEval release is current and which Meta repo hosts the canonical harness -->
- **Metrics.** Insecure-code rate; prompt-injection compliance rate; cyber-attack-helpfulness rate.
- **Auditor configuration.** Pin to the release the vendor cites; the test prompts include real CWEs — run under the WORM archiving rule for sensitive outputs.
- **Common gotchas.** Judge-model drift is significant; version the judge separately.

### METR public tasks

- **What it is.** METR's public task suite for autonomy evaluations (long-horizon agentic tasks with measured time-to-completion by expert humans). <!-- needs-research: confirm which METR task suite is public at reading time and whether a canonical harness exists; METR's full task set is partially non-public to avoid training contamination -->
- **Metrics.** Task completion rate; time-to-completion (vs. human reference).
- **Auditor configuration.** Expensive — tasks are long-horizon; budget compute and wall-clock carefully; closed-weights endpoints may hit rate limits.
- **Common gotchas.** Non-replicable tasks (those behind sign-in or with access restrictions) must be excluded; the subset the auditor runs must be named.

### SWE-bench Verified

- **What it is.** OpenAI-and-Princeton's human-verified subset of SWE-bench (500 real GitHub issues/PRs from twelve Python repos) used as the frontier-model coding evaluation.
- **Metrics.** `pass@1` (resolved issue rate) on the Verified 500.
- **Auditor configuration.** Pin to the Verified revision; use the official evaluation harness (SWE-bench evaluation image for reproducible test execution); isolate network per task.
- **Common gotchas.** Running the harness without the Docker eval image gives non-comparable results; the auditor always uses the sanctioned image.

### The policy-derived internal eval suite

Beyond public benchmarks, most vendors run a policy-derived evaluation suite — prompt sets derived from the organisation's usage policy, safety policy, and acceptable-use policy. The card may claim "97% compliance with internal safety policy on the Q3 policy eval set." The auditor:

- requests the policy-eval suite under NDA (vendor's choice to share or not);
- replicates the run if shared;
- if not shared, inspects the vendor's run artifact (per `mod-104`) and reports the inability to independently replicate as a scope restriction.

Chapter 1 of `mod-104` installs the evidence-discipline shape that governs this.

## Running a benchmark — the procedure

A reusable per-benchmark procedure (one row of the audit workbook):

1. **Confirm the vendor's declared harness.** Read the card and companion documents; record the exact benchmark version, harness commit, decoding config, judge model, dataset split.
2. **Fetch and pin.** Clone the harness at the declared commit; download the dataset at the declared version; verify integrity hashes.
3. **Configure the target.** Point the harness at the audit-target endpoint or model; disable any default telemetry that would leak the prompt set.
4. **Dry-run.** Execute on a tiny subset (5–10 samples) to confirm the plumbing before committing full-run compute.
5. **Full run with manifest.** Execute the canonical full run; emit the chapter-2 replication manifest.
6. **Archive raw outputs.** Per-sample inputs, outputs, scores. Hash-chain these into the engagement WORM store.
7. **Compute the delta.** Observed metric minus claimed metric; observed CI vs. claimed CI (chapter 4 operationalises); per-category breakout if the benchmark supports it.
8. **Signed-delta report line.** Emit the one-line signed-delta entry (format below) into the engagement's benchmark-delta register.

## The signed-delta reporting shape

Every replicated benchmark emits a single row in the engagement's delta register. The row is auditor-signed because it is the evidence line the report cites; the signature binds the auditor to the claim.

```yaml
- claim_id: M-PERF-003
  benchmark: swe-bench-verified
  benchmark_version: "verified-2024-08"
  harness_commit: "princeton-nlp/SWE-bench@abc1234"
  card_claim:
    metric: pass@1
    value: 0.487
    reported_ci: null
    reported_sample_size: 500
    reported_decoding: "greedy, temperature 0"
  replication:
    manifest_id: ACME-2026-AIAUDIT-Q4-REP-0014
    metric: pass@1
    value: 0.472
    bootstrap_ci_95: [0.432, 0.511]
    sample_size: 500
    decoding: "greedy, temperature 0, seed 42"
    tool: "inspect-ai v0.3.52 / SWE-bench eval image 2024-08"
  delta:
    point: -0.015
    point_within_claim_bootstrap_ci: true
    status: "within-noise-floor"
  scope_restrictions:
    - "Judge model unspecified in card; replication used programmatic grading per SWE-bench harness; vendor declined to disclose judge choice"
  signature:
    auditor: "L. Auditor, CPA — engagement ACME-2026-AIAUDIT-Q4"
    signed_at: "2026-11-05T15:02:11Z"
    cosign_sig: "…"
```

The delta-register row is produced *before* the finding-register row. A finding is only raised when the delta row's status is outside an acceptable band, not from the delta number alone.

## Delta statuses and when each becomes a finding

Four statuses cover the common cases:

- **within-noise-floor.** Delta is within the replication's bootstrap CI and (where published) the claim's CI. No finding.
- **within-claim-ci-but-outside-noise-floor.** Replication's CI does not cover the claim's point. The result is evidence of real difference; the finding, if any, is proportionate to materiality and category.
- **outside-both-CIs.** Delta is statistically material against the claim. Finding candidate; cross-check with a second replication run (different seed; different hardware node) before writing up.
- **unverifiable.** Benchmark or configuration could not be reproduced (archived harness, retracted dataset, closed-weights routing drift). Not a finding on the metric but a *documentation finding* on the card's reproducibility claim.

The grading in chapter 2 of `mod-105` gives the shape — isolated lapse vs. pattern vs. aggregation. Signed deltas across many benchmarks aggregate: if the vendor's card consistently overstates by a small amount across ten benchmarks, that is a pattern and a different finding than a single out-of-CI result.

## Benchmark-contamination due diligence

A separate check lives alongside replication: *was the benchmark data in the model's training data?* Benchmark contamination has been documented repeatedly in frontier-model releases, and a card claim that cites an uncontaminated-benchmark result the auditor can replicate is still weak if contamination is plausible.

The auditor's due-diligence procedure here is bounded:

- Read the vendor's declared data-mixture description and any decontamination-procedure text.
- Check the card for explicit statements about contamination (e.g., "we removed SWE-bench repository SHAs from the training cut-off").
- Where the vendor has not spoken to contamination, record "contamination posture undocumented" as a card completeness finding.
- Do **not** attempt to prove contamination through membership-inference against the benchmark set — this crosses the `ai-risk-engineer` boundary and the evidence is rarely dispositive.

The depth of contamination analysis lives with `model-evaluation-engineer`; the auditor records its presence or absence at card level.

## Benchmark replication on closed-weights endpoints

Many card claims are against API endpoints whose underlying model version is not exposed:

- Pin by *API version* and *date*. Record the endpoint URL, the API version header, the model-name/alias used, and the wall-clock time range of the run.
- Expect per-run variation larger than open-weights baselines due to invisible routing between sub-variants; run with a repeated-seed schedule where the API accepts a seed, and run multiple days of replication where it does not.
- Do not treat the replication result as "model Y's behaviour." Treat it as "endpoint X's behaviour at time T under configuration C." The scope restriction is an audit-report sentence (chapter 7).
- Where the vendor publishes an evaluation-result claim that cross-references an internal model version the auditor cannot see, the correct status is **unverifiable** with a specific note.

## Per-sample data handling discipline

Several benchmarks include content the auditor would not want to leak:

- **Jailbreak payloads (HarmBench, AIR-Bench).** Must not reach a disclosed channel; use the engagement WORM store and treat as "limited-disclosure" workpapers (chapter 7 covers redacted-report authoring).
- **Dangerous-knowledge questions (WMDP).** Same handling.
- **Cyber-security content (CyberSecEval).** Same handling; may trigger export-control considerations in some jurisdictions. <!-- needs-research: where the engagement crosses US / EU export-control jurisdictions, confirm with counsel whether the specific benchmark content is dual-use — the auditor does not adjudicate, counsel does -->

The replication manifest records the benchmark's disclosure class, and the engagement's working-papers system enforces access to it.

## Common failure modes

- **Rolling up ASR across HarmBench categories into a single number.** The card may do this; the auditor keeps per-category breakdowns and flags aggregation in the card as itself a presentational finding.
- **Using a public judge model to score a vendor's private-judge run.** Non-comparable; results in meaningless delta.
- **Running SWE-bench without the sanctioned Docker eval image.** Produces inflated or deflated pass@1 depending on which tests actually execute.
- **Reporting pass@k for k≠1 against a card that claims pass@1 (or vice versa).** Cross-reporting between pass@1 and pass@10 is a common unforced error.
- **Missing the benchmark's documented decontamination procedure.** If the card describes decontamination and the auditor's replication did not apply it, the comparison is unfair to the vendor; apply the vendor's decontamination step or note non-application.
- **Letting a per-benchmark result drive the opinion.** The report opines on claims in aggregate; a single out-of-CI benchmark is a finding, not an opinion. Chapter 7 operationalises the opinion hierarchy.

## Summary

- HarmBench, AIR-Bench 2024, AgentDojo, InjecAgent, WMDP, MLCommons AILuminate, Meta CyberSecEval, METR public tasks, and SWE-bench Verified are the public benchmarks the AI-auditor replicates against the system under audit.
- Each replication follows the same procedure — confirm the declared harness, pin, dry-run, full run with manifest, archive raw outputs, compute the delta — and emits a signed one-line delta-register row.
- Four delta statuses: within-noise-floor, within-claim-CI-but-outside-noise-floor, outside-both-CIs, unverifiable; findings follow from the status, the materiality, and the aggregation pattern across benchmarks.
- Closed-weights endpoints add scope restrictions the report must state; the auditor never silently substitutes a tool or a judge.
- Contamination posture is a card-completeness check; the auditor flags its absence and refers contamination-analysis depth to `model-evaluation-engineer`.
