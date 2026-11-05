# Auditing the AI Supply-Chain Provenance

## Motivation

Every deployed AI system has a supply chain, and that supply chain is the thing most monitoring programs do not watch. A classifier in production was trained on a dataset, which was derived from a corpus, which was crawled from the web or purchased from a broker or compiled by annotators, and the weights were the output of a training run that used a particular base model from a particular registry pulled through a particular pipeline. The auditor's claim — that the system in production is the system the organisation says it is — fails the moment any link in that chain is unverifiable.

Provenance in the AI supply chain is not "diligent documentation." It is the evidentiary substrate on which every other control rests. A fairness claim is a claim about the training data. A security claim is a claim about the model weights. A compliance claim is a claim about the pipeline that produced the deployed artefact. If the auditor cannot trace the deployed model back to a declared dataset, a declared base model, a declared training run, and a declared ingestion event, every downstream control the auditor tests is sitting on sand.

This chapter frames supply-chain provenance as the auditor sees it: a set of declared criteria (datasheets, model cards, ML-BOM, SPDX AI profile, Sigstore attestations, SLSA levels), a set of observable artefacts (registry entries, signatures, attestations, training-pipeline logs), and a reperformance pattern — trace a production model back to its inputs. The auditor's test is not "is a model card present." The auditor's test is "does the model card match the artefact in the registry, does the artefact in the registry match the artefact in production, and does the training run referenced in the model card actually exist and produce the artefact the organisation says it does?"

## The provenance criteria surface

The auditor is not inventing provenance requirements — the surface already exists, and the first fieldwork step is to map the criteria the organisation has elected (or is bound by). Three distinct criteria strata matter:

**Dataset-level criteria.**

- *Datasheets for Datasets* (Gebru et al., 2018, revised 2021) — a widely-adopted documentation shape covering motivation, composition, collection, preprocessing, uses, distribution, maintenance. Many AI Act Annex IV submissions and ISO/IEC 42001 Clause 7.5 documented information packages use the datasheet shape or an analogue.
- *EU AI Act Article 10 "Data and data governance"* and *Annex IV point 2* — requires documentation of the data and data governance practices for high-risk systems: provenance, scope, main characteristics, labelling procedures, data cleaning, examination for biases, representativeness assumptions, measures to detect and correct unsuitability.
- *ISO/IEC 5259* series (data quality for analytics and ML) — covers data quality measures and data quality management in ML contexts.
- *Dataset signing* — emerging practice (e.g., Sigstore attestations referencing dataset hashes, SPDX 3.0 data-package definitions) that the auditor should expect in mature programmes.

**Model-level criteria.**

- *Model cards* (Mitchell et al., 2019) — intended-use, performance characteristics, evaluation-data, ethical considerations, caveats. The Hugging Face Hub implements model cards via the `README.md` of a model repository and by the model-card metadata schema; `huggingface_hub` exposes the metadata via the `ModelCard` class.
- *System cards* — broader than model cards; used by frontier-model providers (OpenAI, Anthropic, Google DeepMind, Meta) to document deployment behaviour. See `mod-106` chapter 2 for the model-card / system-card audit shape — chapter 106.2 is the content-validation layer; this chapter is the supply-chain layer.
- *ML-BOM with CycloneDX* — OWASP CycloneDX 1.6+ supports a Machine Learning BOM including components of type `machine-learning-model`, training dataset references, model-card fields, and evaluation data. <!-- needs-research: confirm the exact CycloneDX version where ML-BOM support reached production maturity at reading time -->
- *SPDX 3.0 AI profile* — the Linux Foundation's SPDX 3.0 release introduced an AI profile with `AIPackage` and `DatasetPackage` constructs, covering typed metadata for models and datasets (intended use, limitations, training data). <!-- needs-research: confirm SPDX 3.0 AI profile element names and the published-at date relative to the audit period -->
- *Hugging Face model repositories* — the organisation / name / revision triple is the retrieval key; the commit SHA pins the version. The `safetensors` format is the current convention for non-executable weight files; the `pytorch_model.bin` pickle format is the risk pattern chapter 4 tests.

**Pipeline-level criteria.**

- *SLSA (Supply-chain Levels for Software Artifacts)* — the OpenSSF framework defining four build-integrity levels (SLSA 1–4), each raising the bar on provenance generation, source control, build-system isolation, and verification. SLSA applies to ML pipelines the same way it applies to software pipelines — the build is the training job and the artefact is the model weight.
- *in-toto attestations* — the attestation framework underlying SLSA provenance: statements signed about predicates describing what a step did. ML pipelines emit in-toto attestations for data-prep, training, evaluation, and release.
- *Sigstore* — the OpenSSF signing infrastructure (`cosign` for signing artefacts, `fulcio` as the certificate authority, `rekor` as the transparency log). Sigstore signatures over model weights, dataset archives, and attestations are the current evidence pattern for "this artefact came from this identity at this time."
- *Training-pipeline integrity* — the broader control universe: isolated builders, pinned dependency manifests, deterministic data preprocessing (or declared non-determinism with seed capture), evaluation-pipeline separation from training.

The auditor's first workpaper is the **criteria elections table** — one row per criterion above, columns: *elected?*, *where documented?*, *scope of election (all systems / high-risk only / vendor-sourced only / fine-tuned only)?*, *evidence-of-operation link?*. Elections without evidence of operation are structural findings.

## The trace-back — the auditor's core reperformance

The single most important reperformance in this chapter is the **trace-back**: pick a model in production, and walk it backwards to its inputs. Nothing else in the chapter matters if this does not hold.

The trace-back proceeds in stages, each of which is a cell in the reperformance workpaper:

1. **Deployed artefact → registry record.** The model file (or the Triton / vLLM / TGI / SageMaker / Vertex / Databricks / Bedrock model-endpoint config) must resolve to a specific entry in the organisation's model registry (MLflow, Weights & Biases Artifacts, Vertex AI Model Registry, SageMaker Model Registry, Databricks Unity Catalog model, a bespoke registry built on OCI image repositories, or an internal Git-LFS-based solution). Evidence required: the registry entry ID, the artefact hash in the registry, and a hash of the artefact as deployed (the auditor independently computes the deployed-file hash and compares). A hash mismatch is the sharpest supply-chain finding this chapter can produce.

2. **Registry record → build-run attestation.** The registry entry must point at a build-run record — the training job that produced it. Evidence required: in-toto attestation (or pipeline-tool equivalent: MLflow run, W&B run, SageMaker Training Job, Vertex AI Training job, Kubeflow Pipeline run, Metaflow run) linking the artefact hash to the build-run ID, the trainer identity (CI identity, service account), and the build environment.

3. **Build-run attestation → input manifest.** The attestation must reference the input dataset(s), the base model weights, the training code revision, and the hyperparameter configuration. Evidence required: dataset hashes, base-model artefact-hash (which itself traces to its own registry entry), code revision (commit SHA of the training code), hyperparameter file hash.

4. **Input manifest → dataset provenance.** Each dataset in the manifest must resolve to a dataset-registry entry (or datasheet, or CycloneDX / SPDX record) that is itself provenanced: source organisation, acquisition date, licence, processing pipeline. Evidence required: dataset datasheet, dataset-registry entry, acquisition evidence (contract, licence file, crawl manifest, DUA).

5. **Input manifest → base-model provenance.** The base model, when the trained model is fine-tuned, must resolve to its own provenance record — Hugging Face revision SHA with Sigstore attestation if available, vendor-provided model card, licence file, any transfer-restriction clauses from the provider.

6. **Chain of custody for the artefact between training and deployment.** The artefact that leaves the build-run goes through a registry ingestion event (chapter 6), a scan event (chapter 4), and a deployment event. Each of those should produce an attestation; the attestations together form the chain of custody.

A trace-back that breaks at any stage is a *provenance gap*. The auditor records the gap-stage, the specific missing artefact, the criterion the gap breaches, and the business impact (the downstream controls that depend on the missing link). A gap at stage 4 (dataset provenance) breaks every Article 10 claim; a gap at stage 2 (build-run attestation) breaks every Article 15 cybersecurity claim; a gap at stage 1 (hash mismatch) breaks everything.

### A worked trace-back

A deployed classifier in a loan-adjudication system returns a decision the auditor wants to re-establish provenance on.

1. The deployment manifest (Kubernetes `Deployment`) references a container image `registry.internal/credit-model:1.4.2@sha256:abc...`. The image contains a model file `/model/model.safetensors` with SHA256 `deadbeef...`.
2. The MLflow registry has a model named `credit-adjudicator`, version 1.4.2, with `source` field pointing to run ID `run-7f8c`. The artefact list for `run-7f8c` includes `model.safetensors` with the same `deadbeef...` hash. **Stages 1 and 2 reconcile.**
3. Run `run-7f8c` has `params.base_model_hash = "beef0001..."`, `params.dataset_hash = "cafe1234..."`, `params.training_code_sha = "a1b2c3..."`, `params.hyperparams_hash = "f00df00d..."`. The tag `in_toto_attestation = s3://attestations/run-7f8c.intoto.jsonl` resolves and the attestation is signed by a workload identity whose certificate chains to Fulcio.
4. The training-code SHA `a1b2c3...` resolves to the commit in the organisation's internal GitLab, on branch `main`, merged via a signed merge request reviewed by named engineers.
5. The dataset-hash `cafe1234...` resolves to dataset `credit-training-2025Q3` in the dataset registry. The dataset has a datasheet, a CycloneDX ML-BOM entry, an acquisition manifest (internal credit-decisioning logs for Q2–Q3 of the prior year with PII tokenised by the data-engineering pipeline), and a licence note stating internal-use only.
6. The base-model hash `beef0001...` resolves to `meta-llama/Llama-3.1-8B@<revision>` pulled on <date> via the organisation's mirror. The mirror has a Sigstore attestation generated at pull time; the revision SHA matches Hugging Face's then-current main revision as recorded in the mirror log.

This trace closes. The auditor's workpaper records the artefact IDs, the hashes, the attestation URIs, the date retrieved, and the hash-reperformance evidence. Where any of these fail, the finding writes itself against the specific stage.

## Datasheet and dataset-provenance audit

Datasheets for datasets are dense, but the auditor's test is narrow. The auditor is not scoring the datasheet's quality; the auditor is testing whether the datasheet is consistent with the dataset artefact and whether the dataset artefact is consistent with the pipeline that produced the model.

For a sampled training dataset, the auditor confirms:

- **Identification.** Dataset name, version, hash. The datasheet must identify the exact artefact the training pipeline consumed.
- **Collection method.** The datasheet describes how the data was collected. The auditor spot-tests: pick a record, is it traceable to the collection event the datasheet describes?
- **Pre-processing and cleaning.** The datasheet names the pre-processing steps. The auditor samples the pre-processing output and confirms the step produced what the datasheet claims (e.g., PII tokenisation — pick 20 records, confirm the tokenisation).
- **Composition and distribution.** The datasheet describes composition (feature distribution, class balance, demographic coverage where applicable). The auditor independently computes a summary of the actual dataset and compares.
- **Licence and distribution restrictions.** The datasheet names the licence. The auditor checks the licence is compatible with the deployment context — a dataset licensed "non-commercial" powering a commercial model is a licence defect.
- **Known biases and limitations.** The datasheet names the knowns. The auditor does not independently discover unknowns here (that is `mod-107` chapter 5's fairness auditing); the auditor tests that the knowns the datasheet claims match the documentation the organisation acted on.
- **Signing / attestation.** If the organisation has elected dataset signing, the auditor verifies the signature over the dataset artefact and over the datasheet-and-artefact bundle.

A datasheet that cannot be reperformed against the artefact is not a datasheet — it is a cover letter. The finding is against Article 10 (for Article 10 systems) or Clause 7.5 (for all ISO/IEC 42001 systems) depending on scope.

### Dataset-provenance edge cases

Three edge cases dominate the field:

1. **Scraped / crawled web data.** The datasheet should include the crawl spec (seed URLs, crawl date range, robots.txt handling), the deduplication step, the content filter (CSAM, PII, copyright). The auditor tests the crawl manifest and the filter-hit log, not the entire crawl.
2. **Purchased / brokered data.** The datasheet should include the data supply agreement (DUA), the acquisition contract, and the chain-of-custody evidence from broker to the organisation's data lake. The auditor confirms the DUA covers the deployment context and samples the acquisition-manifest records against the artefact.
3. **Annotator-generated data.** The datasheet should include the annotator workforce description (payment, consent, training), inter-annotator agreement statistics, the annotation guidelines, and a QA sample. The auditor samples annotation records back to the annotator identities declared by the vendor.

In all three cases the auditor records a *dataset-source-type* column alongside the dataset identity, and notes the audit-depth justified for each source type.

## Model-card provenance audit

The model card is the companion to the datasheet at model level. The auditor's test is parallel — card consistency with artefact — but the model-card content surface adds performance claims, intended-use claims, and limitations claims that are tested elsewhere in the curriculum (`mod-106` chapters 1 and 2 on model-card / system-card claim verification). This chapter tests the supply-chain pieces:

- **Model identity and versioning.** Card names the model, version, revision SHA. Must match registry entry and deployment artefact.
- **Training data references.** Card names the training data. Each referenced dataset must trace to a datasheet (above).
- **Base-model / fine-tuning parentage.** Card names the parent base model where applicable. The parent must trace to its own provenance record.
- **Training hyperparameters.** Card gives salient hyperparameters. Must match the build-run record.
- **Licence and usage restrictions.** Card names the licence. Must match the registry entry and any deployment-time licence enforcement.
- **Evaluation data references.** Card names the evaluation data. Each dataset must trace to a datasheet. The evaluation dataset must not be the training dataset (an obvious defect that is easy to catch by hash comparison).
- **Known limitations and intended use.** Card states them. The deployment context must not violate the stated intended use — a card that says "not for high-stakes decisions" powering a high-stakes decisioning system is a card-vs-deployment defect. Downstream deployer obligations under EU AI Act Article 26 and Articles 51–55 (chapter 5) attach here.

Hugging Face Hub artefacts: the auditor uses `huggingface_hub` to pull the card metadata and the file SHA for the exact revision the mirror captured; the evidence includes the revision SHA, the metadata YAML block, and the file manifest.

## ML-BOM with CycloneDX 1.6

CycloneDX 1.6 introduced the Machine Learning BOM profile: a BOM that includes `components` of type `machine-learning-model` and `data`, with fields covering model-card metadata, dataset descriptors, and the relationships between them. The ML-BOM fits into the SBOM ecosystem the organisation's software supply-chain tooling already understands — which is the point: the ML components sit alongside the Python package BOM, the container BOM, and the system-package BOM in the same artefact.

The auditor's ML-BOM test:

- **Existence per production model.** Every production model has an ML-BOM published alongside the artefact. Missing ML-BOM = finding.
- **ML-BOM references match registry.** Each component ID, hash, and version in the ML-BOM resolves to a registry entry.
- **Dataset components are complete.** Each dataset referenced in the ML-BOM has its datasheet or SPDX dataset package.
- **Model-card fields populated.** The ML-BOM model-card fields are not left blank.
- **Signature over the ML-BOM.** The ML-BOM is signed with a Sigstore (or equivalent) attestation so that a consumer can verify the BOM itself is authentic.
- **Deployment-time verification.** The runtime (Kubernetes admission controller, CI gate, model-serving platform) verifies the ML-BOM presence before allowing the model to serve.

A production model without a signed ML-BOM, in an organisation that has elected CycloneDX ML-BOM, is a Clause 7.5 documented-information control defect and a chapter-6 registry-gate defect at once.

## SPDX 3.0 AI profile

The SPDX 3.0 release introduced an AI profile with first-class `AIPackage` and `DatasetPackage` constructs, aligned to AI-system descriptive fields and licence. <!-- needs-research: confirm exact SPDX 3.0 AI profile element and property names, and the release date, at reading time --> The auditor's test is parallel to the CycloneDX test, with one addition: SPDX dataset-package and AI-package licence fields are the auditor's hook into licence-chain testing. A trained model's licence constraints are the union of the base-model licence, the training-dataset licences, and the organisation's chosen output licence. SPDX gives the auditor the exact fields to read.

The auditor's licence-chain reperformance: resolve every licence in the SPDX graph for the model, compute the composition under the applicable licence-compatibility rules, and compare to the licence the model card / registry claims. A composition conflict (e.g., a GPL-licensed component in a proprietary model-serving pipeline) is a licence-chain finding.

Where the organisation has chosen one of CycloneDX or SPDX rather than both, the auditor tests the elected format and records the non-election of the other as an organisational choice, not a finding — the criteria elections table captures it.

## SLSA levels

SLSA (Supply-chain Levels for Software Artifacts) frames the build-integrity levels an organisation claims for its artefacts. For ML pipelines:

- **SLSA Level 1.** Provenance is produced, documenting the build process at a high level. Minimum to begin an audit; below this, there is no substrate to test.
- **SLSA Level 2.** Build service generates signed provenance; source is version-controlled; a service-managed builder produces the artefact. The auditor tests that the training pipeline runs on a managed builder (not a developer laptop) and that provenance is signed.
- **SLSA Level 3.** Non-falsifiable provenance; isolated, hermetic builds; builder resists in-build compromise. For ML, hermetic means no uncontrolled external fetches during training — dataset and base-model artefacts are pinned, dependency manifests are locked, network egress is restricted. The auditor tests the network policy and the dependency-lock manifest for the training environment.
- **SLSA Level 4** (where present in the applicable SLSA version). Two-party review of all source changes; reproducible builds where applicable. For ML, deterministic re-training is the "reproducible" analogue; the auditor expects the organisation to declare its reproducibility posture explicitly.

The auditor's SLSA test maps each production model to the SLSA level the organisation claims, then reperforms the evidence for that level. A SLSA-3 claim with non-isolated builds (training jobs that pull arbitrary pip packages at runtime, for example) is a false-level finding.

<!-- needs-research: confirm whether the current SLSA specification defines Level 4 or has reorganised the level definitions at reading time -->

## Sigstore and in-toto attestations

Sigstore is the current practitioner default for signing ML artefacts and attestations. The auditor's Sigstore test:

- **Keyless-signing identity.** `cosign` signatures created with Fulcio-issued short-lived certificates bind the signer identity (CI system, workload identity, person) to the artefact. The auditor verifies the identity chains to a known organisational identity policy — a signature from a Google workload identity owned by an engineering account the organisation disavows is a trust-chain finding.
- **Rekor transparency-log presence.** The signature is recorded in Rekor (the Sigstore transparency log). The auditor confirms the Rekor entry exists at an expected log index.
- **Policy evaluation.** The organisation has a signing policy declaring which identities may sign which artefact classes (e.g., "only the `model-release-ci` workload identity may sign artefacts in `registry.internal/prod-models/*`"). The auditor confirms the policy exists and is enforced by the registry ingestion gate (chapter 6).
- **in-toto predicates.** Beneath the Sigstore signature, the attestation itself is an in-toto Statement with a predicate type. Predicate types the auditor should expect: SLSA Provenance, SLSA VSA (Verification Summary Attestation), vendor-specific predicates for dataset provenance, evaluation results, scan results. The auditor confirms the predicate types declared cover the controls the organisation is relying on.

## Training-pipeline integrity

Even where the artefact provenance is tidy, the training pipeline itself can introduce supply-chain risk. The auditor tests:

- **Source isolation.** Training code is in version control; training-data fetch is via pinned artefact references; the pipeline cannot inject un-provenanced data mid-run.
- **Dependency locking.** Python / CUDA / library dependencies are locked to specific versions; the lock file is checked into source control; dependency resolution happens at a controlled point (not at training-run time).
- **Secret handling.** Training-time credentials (object-store access, dataset-broker tokens) are short-lived and auditable; no long-lived secrets are embedded in training code.
- **Determinism and seed capture.** Seeds for stochastic components are captured in the run manifest; where non-determinism is unavoidable, the run manifest declares it.
- **Evaluation separation.** The evaluation pipeline runs on different infrastructure from the training pipeline, with independent data access, so a compromised trainer does not also compromise the evaluator.

Chapter 4 extends training-pipeline integrity to the specific risk of *poisoning* (dataset back-doors, LoRA-weight tampering, fine-tuning adversarial injection). This chapter establishes the structural controls; chapter 4 tests whether those controls stop the specific threats.

## Common failure modes

- **Registry-record points at nothing.** The registry entry has no backing attestation; the run ID references a system no longer online; the artefact hash is not stored.
- **Base-model provenance lost.** The organisation pulled a Hugging Face model without capturing the revision SHA, so the base-model version in production cannot be reconstructed.
- **Dataset-hash drift.** The dataset "credit-training-Q3" has been mutated in-place since training; the hash in the manifest no longer matches the current artefact on the data lake.
- **Attestation-without-policy.** Sigstore signatures exist but no policy evaluates them at registry ingestion; the signatures are decoration.
- **Datasheet-without-sample-reperformance.** The datasheet claims a distribution the actual data does not match — nobody has reperformed the composition summary.
- **CycloneDX-or-SPDX election declared, not operated.** The organisation adopted ML-BOM in policy; production models ship without one.
- **SLSA-level-overclaim.** The organisation claims SLSA Level 3 while running training jobs with unrestricted egress to the public internet.
- **Licence-chain-not-audited.** The composed licence posture of a fine-tuned model has never been computed from base-model + dataset licences.
- **Pipeline-level-but-not-system-level.** CI pipelines produce signed artefacts and provenance, but the production model-serving platform does not verify signatures at ingestion.

## Summary

- Supply-chain provenance is the evidentiary substrate for every other control the auditor tests — a provenance gap breaks every downstream claim that rests on the missing artefact.
- The criteria surface the auditor should expect includes datasheets for datasets, model cards, CycloneDX ML-BOM, SPDX 3.0 AI profile, SLSA levels, Sigstore signatures, and in-toto attestations; the organisation elects a subset, and the elections table pins what the auditor will test.
- The core reperformance is the **trace-back**: deployed artefact → registry record → build-run attestation → input manifest → dataset provenance → base-model provenance, with hash reperformance at every stage.
- Datasheet, model-card, ML-BOM, and SPDX tests are consistency tests between declared documentation and observable artefact — the auditor computes the consistency, not the documentation.
- SLSA levels are claims the organisation makes; the auditor reperforms the evidence for the claimed level, and a level-overclaim is a finding.
- Sigstore / in-toto attestations only earn trust when a policy evaluates them at the registry ingestion point (chapter 6).
- Training-pipeline integrity (isolation, dependency locking, seed capture, evaluation separation) sets the structural guardrail; chapter 4 tests whether the guardrail stops specific poisoning patterns.
- Chapter 2 picks up the third-party vendor shape; chapter 6 picks up the signing / ingestion gate; chapter 4 picks up the malicious-artefact defence.
