# exercise-02: Independent Performance Replication with the Eval Toolchain

**Estimated effort:** 3 hours

## Objective

Take a single Grade A performance claim from the exercise-01 register and produce the **signed, pinned replication artefact** — environment pin, raw per-sample output, computed metric, bootstrap CI, delta against the card — as a workpaper an independent reviewer could re-run.

The emphasis is procedural discipline, not throughput. One claim replicated to engagement standard is worth more than ten partial replications.

## Prerequisites

- Chapter [`02-replication-toolchain-and-borrowed-depth.md`](../02-replication-toolchain-and-borrowed-depth.md).
- Chapter [`03-replicating-public-benchmarks-and-reporting-the-delta.md`](../03-replicating-public-benchmarks-and-reporting-the-delta.md).
- exercise-01 claim register with at least one Grade A performance claim identified.
- A sandboxed compute environment the engagement controls (a vendor's shared notebook does not count; the environment must be pinnable).

## Scenario

Continuing the **North Harbor Bank — Harbor-Triage-v2** engagement from exercise-01. The claim register contains a Grade A performance claim, for example "pass@1 of X on SWE-bench Verified (greedy decoding, temperature 0, seed Y) for the Harbor-Triage-v2 model variant" or an equivalent public-benchmark claim the card makes. (If your actual exercise-01 register does not contain a Grade A performance claim against a public benchmark the auditor can obtain, substitute a Grade A claim from the register that is replicable and document the substitution.)

You have one day of compute budget. The compute environment is a single node with the capability the benchmark requires (CPU for small-text evals; a single A100-class GPU or an API endpoint for LLM evals).

## Requirements

1. **Pick one Grade A performance claim.** Record claim ID, verbatim sentence, benchmark, declared harness commit, declared decoding, declared sample.

2. **Produce the full replication manifest** in YAML, following the chapter-2 template exactly. Required manifest fields:
   - engagement, claim_id, claim_source (URL + hash),
   - target (model, revision or API version),
   - tool (name, version, repo + commit),
   - benchmark (name, revision or dataset hash),
   - decoding (every parameter the card declares, and the auditor's choices where silent),
   - environment (OS, Python, driver, hardware),
   - judge (if any; "n/a (programmatic grading)" if not),
   - run (start time, duration, command, log hash),
   - result (metric, value, sample size, bootstrap CI 95%),
   - delta_vs_claim (card value, delta, delta within claim CI).

3. **Execute the replication.** Run the pinned harness against the pinned target; emit the per-sample output; compute the metric and a 10,000-resample fixed-seed bootstrap CI.

4. **Produce the signed-delta row.** The one-line YAML (chapter 3 shape) signed by the auditor (digital signature or, for exercise purposes, an auditor-identifier + timestamp line).

5. **Archive the raw artefact.** Not only the summary metric: the per-sample inputs, outputs, scores. For this exercise, archive to local disk with a structured directory layout mirroring the engagement's WORM store (one directory per manifest ID; inputs.jsonl, outputs.jsonl, scores.jsonl, manifest.yaml, log.txt, sha256sums.txt).

6. **Write a one-page "replication record" workpaper** that an independent reviewer (chapter 7) could read to confirm the result:
   - Objective of the procedure (claim under test).
   - Procedure performed (tool, command, pins).
   - Evidence inspected (raw outputs, per-sample scores).
   - Result (value, CI, delta, status per chapter 3 — within-noise-floor / within-claim-CI-outside-noise-floor / outside-both-CIs / unverifiable).
   - Scope restrictions and limitations (anything the auditor could not pin, any substitution, any missing information from the card).
   - Conclusion (does the replication support, qualify, or contradict the card's claim at the stated confidence?).

7. **Write a short "second-run cross-check" plan** — if the first run showed a delta outside the claim's CI, what second run would the engagement perform (different seed; different node; alternate harness implementation; independent judge) to confirm the finding is not run-specific. Do not run the cross-check; plan it.

## Starter guidance

- Pick a benchmark the audit team can actually run in one day. SWE-bench Verified on a frontier model is a full-day run on one node; HarmBench on a 7B OSS model fits in a couple of hours; MMLU on a 7B OSS model fits in under an hour. Choose the smallest claim that still demonstrates the discipline.
- For closed-weights endpoints: pin by *API version header* and *date*; document that the underlying model is not pinnable.
- Set `temperature=0`, `top_p=1`, and a fixed seed where supported; document where the endpoint ignores the seed.
- Fix 10,000-resample bootstrap with seed 42 as the audit standard for this exercise.
- The signature on the signed-delta row can be a human-readable signoff line for this exercise (e.g., `signed_by: "Auditor Name, Engagement ID, YYYY-MM-DDTHH:MM:SSZ"`); a production engagement would use cosign or an equivalent.
- If the pinned tool cannot be installed (missing dependencies, retired repository), halt the exercise and submit a "replication-not-possible" record. That is itself a valid audit outcome.
- Do not patch the tool. If it fails, the record says "tool failed; non-reproducible under the environment pinned"; it does not say "patched and reran."
- Do not use the vendor's own evaluation environment (even if offered). The replication must be independent.

## Acceptance criteria

The deliverable is accepted when:

- The replication manifest is complete per chapter 2's template; every field is populated or explicitly marked `unstated`.
- The signed-delta row is emitted in the chapter 3 shape and signed (per the exercise's signature convention).
- Raw per-sample inputs, outputs, and scores are archived; SHA-256 sums are computed and in `sha256sums.txt`.
- The bootstrap CI is computed with 10,000 resamples at a fixed seed; the code or command that produced the CI is in the manifest.
- The one-page replication-record workpaper reads cleanly for a reviewer — objective, procedure, evidence, result, limitations, conclusion.
- The cross-check plan names at least two independent perturbations (seed; judge; harness variant; hardware node).
- Any scope restriction (closed-weights routing, missing seed, substituted judge, archived tool) is called out in the record, not buried.
- The conclusion matches the computed delta status; the conclusion does not overclaim.

## Stretch goals

- Run the replication a **second time** with a different seed and a different wall-clock window, and report the inter-run variation; produce a small addendum to the record characterising the replication's noise floor empirically.
- Extend the manifest to include a **cosign signature** over the manifest file itself; verify the signature from a second account and record the verification result.
- Build a **tiny reusable script** (`make-manifest.py`) that takes CLI args (claim_id, model, benchmark, result, CI, …) and emits the canonical manifest YAML; the engagement reuses it for every subsequent replication.
- Where the vendor's evaluation environment is offered, document in a one-paragraph note why the audit *declined to use it* and what evidence the auditor accepted instead — this is a common engagement-letter question.
