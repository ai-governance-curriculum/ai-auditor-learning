# exercise-01: Data and Model Provenance Audit Drill

**Estimated effort:** 2.5 hours

## Objective

Perform a chapter-1 **trace-back** on a production AI model and produce the one-model-per-workpaper evidence a reviewing partner can inspect without needing your explanation. The deliverable demonstrates that the model deployed in production resolves cleanly to a build-run attestation, an input manifest, dataset provenance, base-model provenance, and the chain of custody from training to deployment.

This exercise is the "can I audit a model's supply chain at all" check before chapters 2–7 lean on it.

## Prerequisites

- Chapter [`01-auditing-ai-supply-chain-provenance.md`](../01-auditing-ai-supply-chain-provenance.md).
- `mod-104` on evidence discipline and sampling.
- `mod-105` chapter 7 on auditing Clause 8 operation (AI life-cycle controls) — the AIMS-level anchor.
- Working knowledge of at least one model registry (MLflow, Vertex AI, SageMaker, Unity Catalog, or equivalent) and one signing / attestation system (Sigstore / cosign preferred).

## Scenario

**Northland Lending**, a mid-sized commercial lender, runs an in-production credit-pre-screening model (`credit-prescreen`) deployed as a containerised inference service behind the organisation's loan-origination API. The model is a fine-tune of an open-weight base (Llama / Mistral / Qwen class, size ~7–13B) on an internal credit-events dataset for the prior three calendar years. The organisation has an AIMS certified to ISO/IEC 42001 and claims SLSA L2 at the training-pipeline level. The organisation elects CycloneDX ML-BOM as the BOM format and uses Sigstore for internal artefact signing. You are the lead auditor on a Stage-2 surveillance engagement focused on the supply-chain posture.

If you prefer a different anchor, substitute any published AI-governance programme with a comparable fine-tune shape (a bank, hospital system, retailer with a recommendation model). State the chosen subject at the top of the deliverable.

## Requirements

1. **Pin the subject and scope.** Record the organisation, the specific model under audit (name, version, deployment endpoint), the AIMS scope statement, the SLSA level claimed, and the chosen artefact-format elections (CycloneDX, SPDX, Sigstore, in-toto, format elections). Note any regulatory overlays in scope (EU AI Act Annex III? SR 11-7? SR 23-4 flow-down from the lender's third-party programme? OMB if a federal contractor?).

2. **Criteria elections table.** One row per criterion from chapter 1 (datasheets for datasets, model cards, CycloneDX ML-BOM, SPDX 3.0 AI profile, SLSA level, Sigstore signatures, in-toto attestations). Columns: *elected?*, *where documented?*, *scope of election*, *evidence-of-operation pointer*. Elections without evidence of operation are structural findings.

3. **The trace-back workpaper.** Walk the deployed model backwards through the six stages in chapter 1:
   - Deployed artefact → registry record (with hash reperformance).
   - Registry record → build-run attestation.
   - Build-run attestation → input manifest.
   - Input manifest → dataset provenance.
   - Input manifest → base-model provenance.
   - Chain of custody (ingestion, scan, deployment events).

   For each stage, record the specific artefact IDs, hashes, attestation URIs, retrieval timestamps, and the independently-computed hash where a hash check is in scope. A broken stage is a provenance-gap finding.

4. **Dataset-provenance deep dive on one training dataset.** For a sampled training dataset: datasheet reperformance (identification, collection method, pre-processing sample, composition summary reperformance, licence check, signing-if-applicable). Note which of the three dataset-source-type edge cases (scraped, brokered, annotator-generated) applies and the proportionate depth you applied.

5. **Model-card reperformance.** Check the model-card metadata consistency with the registry entry and the deployment artefact. Note hyperparameter consistency with the build-run record. Flag any card-vs-deployment violations (e.g., "not for high-stakes decisions" attached to a model powering a high-stakes decision).

6. **ML-BOM (or SPDX) reperformance.** Confirm the ML-BOM references match the registry and the datasheet / model-card chain. Confirm a signature over the ML-BOM where elected. Flag a deployment-time verification gap if the ML-BOM is not consumed at admission.

7. **SLSA-level reperformance.** Independently test two of the SLSA-level requirements the organisation claims. For SLSA L2: builder-managed, provenance signed. For SLSA L3: hermetic builds (network-egress restrictions during training, pinned dependencies), non-falsifiable provenance. Record each claim as *verified*, *partially verified*, or *overclaimed*.

8. **Findings register.** One row per finding candidate. Columns: finding ID, title, criterion cited (chapter-1 stage, ISO 42001 clause, ML-BOM / SPDX-elected policy, SLSA-level claim), severity, evidence pointer, management-response-requested shape. Do not author the response.

9. **Sampling and workpaper hygiene.** Record the sample rationale (why this model), the retrieval timestamps, any WORM / immutable-storage evidence, and `<!-- needs-research: ... -->` markers for items the primary sources do not resolve.

## Starter guidance

- The trace-back is the entire audit — if it works, you have supply-chain evidence; if it breaks at any stage, nothing else in chapter 1 matters until you have characterised the break.
- Compute hashes independently where possible; do not rely on the registry's claimed hash alone.
- A model-card without a matching artefact is a cover sheet; test consistency with the registry file, not the card's narrative.
- SLSA-L3 claims are easy to make and easy to overclaim — hermetic-build and non-falsifiable-provenance are the two failure patterns to test specifically.
- If the organisation uses Hugging Face as a mirror for the base model, pin the revision SHA and the pull-time attestation; the Hub commit is the version anchor, the file hash is the content anchor.
- Where ISA 620 specialist use is appropriate (for example, the back-door-detection analysis in chapter 4 adjacent to the trace-back), defer the specialist engagement and record the reason — this exercise is the structural reperformance, not the deep technical test.

## Acceptance criteria

The deliverable is accepted when:

- Subject, scope, and criteria elections are pinned with evidence pointers.
- The trace-back workpaper has all six stages populated with artefact IDs, hashes, and retrieval evidence.
- At least one training dataset's provenance has been reperformed with the datasheet consistency sample.
- Model-card and (where elected) ML-BOM consistency with the registry and deployment artefact is tested.
- SLSA-level claim is reperformed against at least two specific requirements of the claimed level.
- Findings are stated against the specific chapter-1 stage and the cited criterion.
- `<!-- needs-research: ... -->` markers appear where the primary sources do not resolve a claim.
- Workpaper hygiene (retrieval timestamps, WORM pointers, sample rationale) is documented per `mod-104` discipline.

## Stretch goals

- Author the **provenance-gap matrix** — rows are chapter-1 stages, columns are the organisation's current controls, cells record *covered*, *partial*, *gap*. Hand it to the audit committee as the headline.
- Produce a **licence-chain reperformance** — compute the composed licence posture of the production model from base-model + dataset licences + output licence; identify any composition conflicts.
- Draft a **Clause 7.5 documented-information control update** the organisation would adopt to close the single highest-severity finding.
- Author a **one-page audit-committee memo** summarising findings at Sev-2 and above in a shape consistent with `mod-111` findings-reporting discipline.
