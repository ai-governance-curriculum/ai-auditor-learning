# exercise-01: Model Card Claim Extraction and Auditability Grading

**Estimated effort:** 2 hours

## Objective

Convert a published model-or-system card into a structured **claim register** and grade every claim on auditability (Grade A–E per chapter 1). The register is the spine the rest of the module reuses — subsequent exercises reach into it rather than re-read the card.

The deliverable is a per-engagement workpaper that an audit team member could pick up and start replication from without re-reading the source card.

## Prerequisites

- Chapter [`01-reading-the-card-as-an-auditor.md`](../01-reading-the-card-as-an-auditor.md).
- `mod-102` on criteria translation (for cross-referencing claims to the applicable obligation).
- `mod-104` chapter 1 on evidence discipline (for pinning the card artefact).

## Scenario

**North Harbor Bank** is preparing to deploy a third-party foundation-model-based *loan-triage assistant* (call it "Harbor-Triage-v2") across its US retail-banking footprint. The vendor has published a model card and a system card on its website, and has linked a separate "Responsible Deployment Report" from the system card. Harbor-Triage-v2 reads the applicant's uploaded documents, summarises them for the underwriter, and offers a non-binding "risk flag" for underwriter review (loans are not auto-approved).

You are the lead external auditor on a limited-assurance engagement commissioned by North Harbor's Audit Committee. Your first fieldwork week opens with the claim-register construction from the vendor's published card artefacts.

For this exercise, treat the vendor's published cards and the companion report as your subject matter. Where the exercise says "the card," pick any real published model/system card (OpenAI, Anthropic, Meta, Google DeepMind, Mistral, Cohere, Alibaba, and Hugging Face community cards all qualify) *and* its companion safety or evaluation report. You will extract from the actual document, not an invented one. Attribute the source precisely at the top of the register.

## Requirements

1. **Pin the card artefact.** Record source URL, retrieval date/time, SHA-256 (download the HTML or PDF and hash it; for HF repos, pin the `revision=`), the companion documents and their hashes. Include a one-line integrity-check note.

2. **Walk the card top to bottom** and produce a **claim register** as a Markdown table (or CSV) with one row per lifted claim. Required columns:

   - `claim_id` (e.g., `H-PERF-001` — H for Harbor-Triage, PERF/FAIR/ROBUST/SAFE/PRIV/USE/PROV/TRAIN/METH).
   - `family` (one of the nine families in chapter 1's taxonomy).
   - `verbatim` (the sentence from the card).
   - `location` (section / subsection / page or anchor).
   - `metric` / `value` / `unit` / `dataset` / `threshold` / `decoding` / `seed` / `judge` / `sample_size` (fill what the card states; mark `unstated` otherwise).
   - `linked_artifact` (URL or hash of any linked eval, companion doc, benchmark).
   - `qualifier` (the condition under which the claim holds — "on English", "at temperature 0", "for the 7B variant").
   - `evaluator_identity` (self / third-party / academic / user-reported).
   - `auditability_grade` (A / B / C / D / E).
   - `grade_rationale` (one sentence).

3. **Produce at least 20 claim rows.** A frontier-lab model card plus companion evaluations will yield 50+; a smaller open-weights card with a slim companion doc may need both the card and the companion report to reach 20. If 20 cannot be reached, document the shortfall and treat "card too thin to audit" as itself a finding.

4. **Flag unstated-but-required fields.** For every performance claim without a CI, decoding, seed, or sample size — add a register row of family `METH` reporting the omission with grade E and rationale "methodology omission; see F-xx in finding register."

5. **Record the card shape.** A short preamble (half a page) stating: (a) which canonical format the card most closely follows (Mitchell / Gebru / Hugging Face / vendor-specific / hybrid); (b) which sections of the canonical shape are present, which are absent; (c) whether companion documents fill the gaps; (d) a one-sentence card-completeness grading (complete / incomplete / insufficient-to-audit).

6. **Produce a coverage-gap note.** If the card speaks only to the base model but the subject of audit is a deployed system (Harbor-Triage includes a retriever, PII filter, underwriter-review UI), record a coverage-gap paragraph identifying claims that do not bind on the system as deployed.

## Starter guidance

- The chapter-1 taxonomy maps one-to-one to this module's chapters; use the family codes.
- Grade A is "everything needed to rerun is in the card." Grade E is "no metric, no dataset, no methodology — categorical only."
- Keep verbatim quotes short; a single-sentence lift is almost always sufficient.
- For companion documents, each discovered claim gets a separate row with a cross-reference to the originating card sentence.
- Where the card bundles multiple claims in one sentence ("95% accuracy, 87% safety refusal, 0.82 fairness ratio on dataset X"), split into separate rows.
- The evaluator-identity column surfaces whether the vendor graded themselves or a third party graded; the two produce very different audit responses downstream.
- Where a claim is categorical but could have been quantified ("highly accurate on English"), grade E and note the presentational issue.

## Acceptance criteria

The deliverable is accepted when:

- The card is pinned (URL, retrieval time, hash) and the companion documents are listed and pinned.
- The claim register has at least 20 rows and one row per *lifted* claim; the grade is populated for every row.
- At least three Grade A, three Grade C or D, and one Grade E claim are present (or the register is honestly short of coverage and the shortfall is noted).
- Every performance claim without a CI or sample size has a corresponding `METH` register row with grade E.
- The preamble records the canonical shape and the completeness grade.
- The coverage-gap paragraph names which claims do not bind on the deployed system.
- No claim is lifted without the originating card sentence quoted verbatim.
- Grades A and B rows can be handed to exercise-02 as replication candidates; Grades C/D rows can be handed to vendor-walkthrough procedures; Grade E rows feed the finding register.

## Stretch goals

- Author a **register-to-chapter crosswalk** — for each register row, name the subsequent exercise / chapter it feeds (e.g., `H-PERF-003 → exercise-02 → chapter 3 SWE-bench procedure`).
- Draft the **companion-document request letter** to the vendor — a one-page information request for any linked artifacts the published card references but does not expose.
- Build a **small Python script** (≤50 lines) that parses an HF `model-index` YAML block into register rows automatically, and reruns the hash check on the raw markdown. Not a replacement for human review — a reproducible intake step.
- Draft an **"in-scope / out-of-scope" paragraph** for the engagement's evidence-request package based on the register's scope coverage.
