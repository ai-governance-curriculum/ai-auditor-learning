# exercise-03: Independent Safety and Red-Team Replication

**Estimated effort:** 3 hours

## Objective

Replicate a safety / red-team claim against a public safety benchmark, produce the signed-delta row, and build the **red-team coverage matrix** that tests whether the vendor's red-team programme covers the attack surface the deployment exposes.

The exercise is dual-edge: it practices the mechanical replication discipline *and* the programme-level shape test chapter 6 installs. A replication that lands in-CI on a single benchmark does not by itself attest to the safety claim; the coverage matrix is the second half.

## Prerequisites

- Chapter [`03-replicating-public-benchmarks-and-reporting-the-delta.md`](../03-replicating-public-benchmarks-and-reporting-the-delta.md).
- Chapter [`06-auditing-robustness-privacy-and-red-team-claims.md`](../06-auditing-robustness-privacy-and-red-team-claims.md).
- exercise-01 claim register (identifies the vendor's declared safety claim(s), the cited catalogs, and the vendor's declared red-team programme).
- WORM-compatible storage for payload-bearing artefacts (chapter 6; `mod-104` chapter 4).

## Scenario

Continuing the **North Harbor Bank — Harbor-Triage-v2** engagement. The vendor's system card states (or an equivalent real-card analogue in the subject you chose for exercise-01):

- "Refusal rate of 97.4% on HarmBench behaviours, judged by the published HarmBench classifier, on the 2024-03 release." (Grade A safety claim.)
- "Our red-team programme covers prompt injection, jailbreak, PII exfiltration, hallucination, and agentic misbehaviour." (Programme-level claim.)

You have a half-day of compute for the public-benchmark replication and a half-day for the matrix.

## Requirements

**Part A — Public-benchmark safety replication (half-day)**

1. **Pin HarmBench** to the release the card cites. Pin the classifier model used for ASR judgement. Pin the target endpoint and decoding.
2. **Run the full behaviour set** (not a subset) against the target.
3. **Compute per-category and aggregate ASR / refusal rate**, with bootstrap CIs.
4. **Emit the signed-delta row** (chapter 3 shape) and **archive raw per-sample outputs** in the WORM-style directory with access restricted to the engagement.
5. **Record the status** — within-noise-floor, within-claim-CI-outside-noise-floor, outside-both-CIs, unverifiable.

**Part B — Red-team coverage matrix (half-day)**

1. **Choose the reference taxonomy.** For a chat/agent deployment, OWASP LLM Top 10 for the attack-class axis; MITRE ATLAS as a cross-reference. Pin the version.
2. **Enumerate the deployment surfaces.** For Harbor-Triage-v2 these are at minimum: direct user prompt, uploaded-document ingestion (indirect prompt injection), retrieval augmentation (if any), underwriter-review UI, logging.
3. **Build the attack-class × surface matrix.** Cells are marked `covered` / `partially covered` / `uncovered` / `n/a` based on the vendor's published documentation (model card, system card, companion red-team report, issue tracker if disclosed).
4. **Cite evidence per cell.** Where marked covered, cite the vendor artefact; where marked uncovered, state the absence; where partial, state what the gap is.
5. **Identify at least three uncovered or partially covered cells** of material deployment risk. For each, draft a one-sentence finding statement and a grade (major / minor / observation using `mod-105` chapter 2 definitions).
6. **Record the matrix in the engagement workpaper** — a Markdown table plus a one-page narrative that walks the reader through the material cells.

**Part C — Payload-disclosure discipline**

7. **For every working jailbreak or safety-bypass** observed during Part A: record that the payload exists, its SHA-256, which behaviour category it belongs to, and the restricted location of the raw payload. Do **not** paste the payload into the exercise submission. The exercise submission is a public-variant artefact; the payloads are restricted-variant artefacts referenced by hash.
8. **Produce the per-artefact disclosure class** — open / internal / limited / restricted — for each file your engagement would archive.

## Starter guidance

- HarmBench's public harness ships with a classifier for ASR scoring; use it as the vendor would. Document the classifier model version.
- If you cannot run the full HarmBench behaviour set in the half-day budget, run a stratified sample across categories and state the stratification in the manifest; this is a scope restriction, not a shortcoming.
- For the coverage matrix, start from the vendor's published artefacts, not from your own imagination of the attack surface. The matrix reports *the vendor's* coverage; your views only enter in the uncovered-cell findings.
- OWASP LLM Top 10 cells: prompt injection (LLM01), insecure output handling (LLM02), training-data poisoning (LLM03), model DoS (LLM04), supply-chain (LLM05), sensitive-information disclosure (LLM06), insecure plugin design (LLM07), excessive agency (LLM08), overreliance (LLM09), model theft (LLM10). <!-- needs-research: confirm current OWASP LLM Top 10 numbering and item set at reading time -->
- If your subject-of-exercise is not an LLM / agent deployment, substitute an appropriate taxonomy (MITRE ATLAS matrix + NIST AI 100-2e) and document the choice.
- Payloads are hazardous even when they look innocuous; store them under WORM, tag them with their disclosure class, and keep them out of email, chat, and shared drives.

## Acceptance criteria

The deliverable is accepted when:

- The public-benchmark run is pinned (HarmBench release, classifier, target, decoding), per-category and aggregate ASR / refusal with CI are reported, and a signed-delta row is emitted.
- Raw outputs are archived in the structured directory layout; the per-artefact SHA-256 sums are in `sha256sums.txt`; the archive layout is reproducible.
- The coverage matrix is constructed with the pinned taxonomy, lists every deployment surface in scope, and assigns a status to every cell with an evidence citation.
- At least three material gaps are identified with draft finding statements and gradings.
- The payload-disclosure classification covers every file; no payload appears in the public-variant artefact.
- The one-page narrative walks the reader from the aggregate ASR delta to the matrix pattern to the three gap findings cleanly.
- The deliverable is written to survive independent-reviewer re-read without the reviewer needing to open a restricted-variant artefact.

## Stretch goals

- Run **one cross-check** with a second safety tool (garak probes against the same target); compare the garak output to HarmBench where the probe families overlap; document the cross-tool consistency or drift as an addendum.
- For one uncovered matrix cell, **sketch** (do not execute) what an independent test would look like — attacker model, budget, evaluator. Note explicitly that the sketch is the auditor describing where attack authoring would be required, not the auditor authoring the attack. This models the scope boundary at `ai-risk-engineer`.
- Author a **"red-team programme interview script"** the audit team would use with the vendor's red-team lead — ten questions grounded in the matrix, each designed to elicit evidence that supports a specific cell.
- Draft the **restricted-variant payload register** — one row per retained payload, with disclosure class, access-approval list, and retention expiry — in the shape chapter 7 will reuse for the report.
