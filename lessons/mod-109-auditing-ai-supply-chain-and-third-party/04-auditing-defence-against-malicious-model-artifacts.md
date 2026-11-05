# Auditing Defence Against Malicious Model Artifacts

## Motivation

A model weight file is executable payload. For much of the deep-learning era, the standard distribution format was Python's `pickle` — a serialisation that can deserialise arbitrary Python objects, including arbitrary code execution at load time. Hugging Face, PyTorch, scikit-learn, Keras, and many other frameworks shipped pickled artefacts by default for years. The research community and specialist tooling (Protect AI ModelScan, Hugging Face `picklescan`) demonstrated repeatedly that malicious model files are not a theoretical threat; they ship in the wild. The `safetensors` format was developed in part as a response.

Beyond the pickle-execution risk, the AI supply chain introduces several other malicious-artefact vectors:

- **Dataset back-doors.** Poisoned training data that induces learned mis-behaviour on triggers, invisible at normal evaluation time.
- **Base-model back-doors.** The same, in a distributed foundation model that downstream fine-tuners inherit.
- **LoRA-weight tampering.** A fine-tune adapter distributed as a small weight delta is also a small attack surface — a tampered LoRA can override base-model behaviour on specific triggers.
- **Training-code supply chain.** Pip-installable dependencies, `requirements.txt` typosquats, poisoned PyPI releases, compromised CI build steps — the generic software supply chain, applied to training.
- **Container / runtime layer.** The image the model serves from is subject to the ordinary container-supply-chain risk, reinforced by the model-specific risk above.

The organisation's defence is a pipeline: scan incoming artefacts, verify their signatures, gate them at registry ingestion, lock down the fine-tuning pipeline, monitor what reaches production. The organisation's defence is *authored* by `ai-infra-security` / `security-learning` (level 35) and the ML-platform team. The auditor *tests* whether the authored defence operates, whether it is comprehensive, and whether sampled artefacts in the registry survive a reperformance.

This chapter is paired with chapter 6 (registry-ingestion gates): chapter 4 tests whether the content of ingested artefacts is clean; chapter 6 tests whether only approved artefacts are ingested. Both must hold.

## The threat-to-control map

The auditor builds a threat-to-control map as the first workpaper. One row per threat; columns for *vector*, *where the organisation says it defends*, *evidence of operation*, *gap*.

| Threat | Typical vector | Defence the auditor expects |
|--------|---------------|------------------------------|
| Pickle code-execution | `.pkl`, `.bin`, `.pth` artefacts loaded with `torch.load` / `pickle.load` | Protect AI ModelScan, Hugging Face `picklescan`, format conversion to `safetensors`, policy forbidding pickle in production |
| Keras HDF5 / H5 custom-layer execution | `.h5` with custom-layer `Lambda` or deserialisation hooks | ModelScan HDF5 rules, Keras `safe_mode` loader, policy forbidding custom-layer deserialisation |
| TensorFlow SavedModel graph execution | `.pb` with ops referencing arbitrary functions | ModelScan TF rules, isolated-runtime loading, policy on allowed-ops lists |
| ONNX custom-operator execution | `.onnx` with custom operators | ModelScan ONNX rules, operator allow-list |
| Dataset back-door | Tainted training records triggering misbehaviour on specific inputs | Training-data provenance (chapter 1), dataset-sampling audits, back-door detection via activation analysis (specialist, ISA 620) |
| LoRA-weight / adapter tampering | Malicious LoRA distributed as a "helpful" fine-tune | Signature on LoRAs, trust-chain policy, evaluation of LoRA output on canary prompts |
| Base-model back-door | Foundation-model provider's model has an unknown trigger | Vendor diligence (chapter 2), published evaluations, GPAI-provider documentation (chapter 5), red-team coverage of triggers |
| Supply-chain poisoning of training dependencies | Typosquat / compromised PyPI package in training `requirements.txt` | Pinned dependency manifest, hash-locked installs, PyPI-mirror policy, signed-dependency verification |
| CI / training-builder compromise | Attacker gains access to the training builder's secrets or code | SLSA levels (chapter 1), isolated builders, short-lived builder credentials, provenance attestations |
| Container-layer compromise | Serving image carries a poisoned base layer | Image signing (Sigstore), image scanning (Trivy, Snyk, Grype), SBOM verification, admission-controller policy |

<!-- needs-research: cross-check the current ModelScan supported-framework matrix against the Protect AI public release notes at reading time -->

The map is per-organisation — not every organisation runs fine-tuning, not every organisation hosts open-weight models, not every organisation deploys in containers. The auditor fills the columns against the specific organisation and prunes threats that do not apply (and records the pruning rationale).

## Protect AI ModelScan — what the auditor tests

Protect AI's open-source ModelScan is the de facto practitioner tool for static scanning of model artefacts. It looks for specific unsafe constructs across multiple serialisation formats (pickle, H5, PyTorch state dicts, TensorFlow SavedModel, ONNX, Keras, scikit-learn, and more at current release). It reports findings at severity levels (critical / high / medium / low) and emits a JSON output suitable for CI integration.

The auditor's ModelScan test is not "does ModelScan exist in the pipeline" — the auditor tests whether it operates and whether its output is acted on.

### The operation test

The auditor samples at least one of each model format the organisation uses — pickle, safetensors, HDF5, ONNX, GGUF, SavedModel as applicable — and verifies:

- **Scan executed on ingestion.** The CI / ingestion pipeline log shows a ModelScan run against the artefact, with a date stamp matching the ingestion event.
- **Scan output retained.** The JSON output is stored for the artefact-retention horizon alongside the artefact itself, so the auditor can re-read historical scans.
- **Policy decision applied.** The organisation has a policy translating ModelScan severity levels into allow / quarantine / block decisions. The ingestion gate applied the policy.
- **Exception handling.** Where a scan finding was overridden ("legacy model, documented risk acceptance"), the override has an owner, rationale, expiration, and compensating control. Unlimited overrides are a policy defect.

### The configuration test

- **Scanner version pinned and current.** The ModelScan version used is pinned (reproducibility) but not stale (the signature database and rule set are kept current).
- **Rules enabled.** The scanner's rule-category toggles are enabled for every format in use. A ModelScan config that disables, say, the pickle `exec` rule is a configuration defect.
- **Format coverage.** The scanner supports the formats the organisation consumes. For a format ModelScan does not support, a compensating control is required.

### The reperformance test

For a sampled artefact in the registry, the auditor independently runs ModelScan against it and compares to the stored scan output. A discrepancy is a scanner-drift finding — either the scanner was configured differently at ingestion time, or the artefact in the registry does not match what was scanned.

A representative Python reperformance:

```bash
pip install modelscan
modelscan -p /path/to/pytorch_model.bin -r modelscan-report.json
```

The output `summary.total_issues_by_severity` and `issues[]` are the fields the auditor reads. The `issues[].severity` and `issues[].description` map to the organisation's policy decision.

## Hugging Face `picklescan` — what the auditor tests

`picklescan` is a Hugging Face-maintained scanner specifically for the pickle serialisation attack surface — it inspects a pickle file's opcode stream for operations that could trigger code execution at load time (`REDUCE`, `BUILD`, `INST`, `OBJ`, `NEWOBJ` with known-dangerous callables).

The tools overlap with ModelScan, and many organisations run both for defence in depth. The auditor's test:

- **Scan of pickle-formatted ingests.** For organisations that still accept pickle (which should be a narrowing population), `picklescan` runs on ingestion alongside ModelScan.
- **Safetensors adoption trajectory.** The organisation has a documented plan to eliminate pickle-formatted artefacts in production, replacing them with `safetensors`. The auditor records progress against the plan.
- **Scan decisions logged and retained.**

```bash
pip install picklescan
picklescan --path /path/to/model.pkl
```

The exit code and the per-opcode output are the artefacts the auditor expects to see retained in CI logs.

## Signature verification

Scanning is necessary but not sufficient. Even a clean-scanning artefact may not be the artefact the vendor intended to publish; even an artefact signed by the vendor may not be the artefact that landed in the registry. Signature verification closes the loop.

The auditor's signature-verification tests:

### For Hugging Face models

Hugging Face provides revision SHAs and increasingly also Sigstore signatures on model-repository artefacts. <!-- needs-research: confirm the current Hugging Face model-signing programme status, including which model families publish Sigstore attestations through the Hugging Face Hub at reading time -->

- **Revision SHA captured at pull.** When the organisation pulls a Hugging Face model, the mirror or the training pipeline records the revision SHA. The SHA is the minimum provenance pin.
- **Signature verified at pull.** For models with Sigstore signatures, the pull gate verifies the signature against the published identity. A signature-verification failure prevents ingestion.
- **File-hash reperformance.** The hash of the downloaded file matches the hash in the model repository metadata.

### For internally-produced artefacts

- **CI signs on build.** Training CI signs the artefact with `cosign` using a workload identity. The signature is recorded in Rekor.
- **Registry ingestion verifies.** The registry ingestion gate (chapter 6) verifies the signature before accepting the artefact.
- **Revocation handling.** Where a signing identity is revoked (compromised CI runner, rotated workload identity), the registry re-evaluates signatures.

### For vendor-provided artefacts

- **Vendor signatures preferred over vendor hashes.** A vendor-provided download-page hash is weaker evidence than a vendor-published signature (the download page can be tampered; the signature chains to the vendor's identity).
- **Chain of trust.** The organisation has a documented trusted-signer list — which identities are acceptable signers for vendor-sourced artefacts. New identities require review.

### Reperformance

For a sampled registry entry, the auditor uses `cosign verify` to independently verify the signature against the published identity, confirms the Rekor log entry, and compares to the organisation's trusted-signer policy.

```bash
cosign verify --certificate-identity-regexp "^.+@organisation.example$" \
  --certificate-oidc-issuer "https://oidc.internal/" \
  registry.internal/credit-model:1.4.2@sha256:abc...
```

A registry entry that fails independent verification is the sharpest finding this chapter can produce — either the signature has been tampered, the policy is not what it claims, or the registry contains a shadow artefact.

## Registry sampling — the unsigned / unscanned sweep

The auditor's broadest reperformance in this chapter is the **registry sweep**: sample the production model registry and test for unsigned / unscanned artefacts.

Sampling guidance:

- **Sample across formats.** Pickle, safetensors, HDF5, ONNX, GGUF, each proportional to the population.
- **Sample across age.** Recently-ingested artefacts, mid-life artefacts, long-tail / rarely-promoted artefacts. The last category is where defects concentrate (the policy was weaker when the artefact was ingested; nobody has rechecked).
- **Sample across provenance category.** Internally-trained, fine-tuned from a vendor base model, directly pulled vendor artefact, open-weight / open-source artefact.
- **Include adapters.** LoRA adapters, PEFT adapters, prompt-tune artefacts — easily overlooked in a "models" sweep.

For each sampled artefact the auditor tests:

- **Signature present and valid.**
- **Scan output present and policy-compliant.**
- **Provenance link present (chapter 1 trace-back).**
- **Ingestion-event record present (chapter 6 gate).**

A finding at any cell cascades — if the artefact is unsigned, the chapter 6 gate has failed; if it is unscanned, the chapter 4 scanner is bypassed; if it has no provenance, chapter 1 has a trace break. Counts of defect-type per sampled artefact are the headline the audit-committee memo wants.

## Fine-tuning pipeline supply-chain audit

Fine-tuning is where supply-chain compromise most naturally enters the organisation's own infrastructure (even a wholly-vendor-sourced model does not become "the organisation's" until the organisation does something to it). The auditor audits three vectors here.

### Dataset back-doors

Back-doored training data is data containing patterns that induce the trained model to misbehave on a specific trigger. A back-door in a fine-tune might, for example, make a loan-adjudication model produce a favourable decision whenever a specific unusual input pattern appears.

The auditor's test:

- **Dataset provenance.** Chapter 1 trace-back: can the auditor get back to the source of every training record?
- **Dataset-change review.** New training data entering the pipeline is reviewed by someone other than the submitter; lineage is logged.
- **Sampling for anomalies.** The organisation runs anomaly-detection on training datasets prior to use — out-of-distribution inputs, duplicated patterns, suspicious label distributions. Where ISA 620 specialist use is appropriate (the back-door detection literature is deep and evolving), the auditor records the specialist engagement.
- **Canary-prompt evaluation of fine-tuned output.** After fine-tuning, the model is evaluated against a set of canary prompts designed to surface back-doors. The canary list is maintained and expanded.
- **Trigger-detection red-teaming.** The fine-tune is subjected to a red-team pass looking specifically for triggered behaviours (`mod-107` chapter 7 on red-team programme shape is the upstream reference).

Dataset back-doors are statistically subtle and the auditor's realistic deliverable is not "the organisation has no back-doors" — it is "the organisation has operated the controls designed to catch back-doors, and the controls' depth is proportional to the fine-tune's risk."

### Training-data injection

Distinct from back-doors: *injection* is the attacker adding training records during the training process, usually by compromising the dataset-staging environment, the broker API, or the data-labelling vendor.

The auditor's test:

- **Dataset-staging access controls.** Who can write to the dataset-staging bucket? Is write-access short-lived? Are writes logged?
- **Record-ingestion attribution.** New records entering the staging dataset are attributed to a specific user / service / broker invocation.
- **Pre-training freeze.** The dataset is cryptographically hashed and frozen before training begins; the training job pulls the hashed snapshot, not a mutable prefix.
- **Vendor-labelling QC.** Where annotation is outsourced, the vendor's own QC pipeline is reperformable; the auditor samples annotations back to annotator identities.

### LoRA-weight tampering

LoRA adapters and other parameter-efficient fine-tunes are small weight deltas that override the base model's behaviour. A tampered LoRA is a small attack with large effect.

The auditor's test:

- **Signatures on LoRAs.** The organisation signs its fine-tuned LoRAs with the same cosign infrastructure used for full-weight artefacts. Distributed LoRAs are verified at pull.
- **LoRA-provenance records.** Each LoRA has a build-run attestation linking it to the base-model hash, the fine-tune dataset hash, the training code, and the training job's compute identity.
- **Trusted-source policy for externally-sourced LoRAs.** Where the organisation consumes a LoRA from a community source (Hugging Face, OpenLLaMA community, etc.), the policy specifies the trust chain: scanned, signature-verified, evaluated against canary prompts.
- **Pre-production evaluation of LoRA output.** New LoRA in staging gets a full canary-prompt evaluation before promotion.

## The fine-tune pipeline-integrity audit

Beyond the specific threats, the fine-tune pipeline itself is tested for integrity (overlapping chapter 1's SLSA / in-toto framing):

- **Isolated compute.** Fine-tuning runs on compute isolated from general-purpose workloads; the network policy restricts egress to known endpoints; secrets are short-lived.
- **Dependency lock.** The fine-tune code's Python / CUDA / library stack is locked; a dependency-manifest hash is captured in the build-run record.
- **Code-review discipline.** The fine-tune training code is in version control, reviewed by two parties before merge, signed on merge.
- **Build-reproducibility declaration.** The organisation declares whether the fine-tune is deterministic (seed-captured) and, where not, the sources of non-determinism.
- **Attestation emission.** The pipeline emits in-toto attestations at each step; attestations are signed by workload identities bound to short-lived certificates.

Pipeline-integrity findings here feed upward into the chapter 1 provenance posture and downward into the chapter 6 ingestion-gate confidence.

## Specialist involvement — ISA 620

Scanning and signature verification the auditor can do first-hand. Back-door detection, adversarial robustness testing, and advanced poisoning-detection are specialist domains — the auditor engages a specialist under ISA 620 (`mod-104` chapter 5 on specialist use is the reference).

The specialist engagement includes:

- **Named specialist and credentials.** Specialist's AI-security qualifications; relevant prior work.
- **Scope of engagement.** Which artefacts, which threat classes, which evaluation methodology.
- **Deliverable structure.** Report format and evidence standards consistent with the auditor's own workpaper.
- **Independence.** Specialist has no engagement with the organisation's `ai-infra-security` team on the same artefacts in the period (common-engagement risk).
- **Review of specialist work.** The auditor reviews the specialist's output, confirms the methodology is appropriate, and takes responsibility for the audit conclusion.

Where specialist involvement is declined ("the risk is below our materiality threshold"), the auditor records the decline rationale explicitly.

## Common failure modes

- **Scanner in CI, policy not enforced.** ModelScan runs and finds issues; the CI gate is informational rather than blocking.
- **Signature required by policy, not by gate.** The policy says artefacts must be signed; the registry accepts unsigned on a "legacy" allowlist that has grown to cover most artefacts.
- **LoRA book not scanned.** Scanning applied to full-weight models; LoRAs and adapters wave through.
- **Vendor-sourced artefact trusted without scan.** "The vendor is a major provider, they would never ship a bad artefact" — but the artefact still passes through the organisation's infrastructure and the organisation's policy demands scanning anyway.
- **Pickle still in production.** Policy declares `safetensors`-only; production registry has pickle artefacts predating the policy with no retirement plan.
- **Canary-prompt list stale.** Canary prompts for back-door detection authored once, never refreshed; the fine-tune authors know them and route around them.
- **Dataset staging writable by production services.** A fine-tune pipeline can write to the training-dataset staging area, creating a self-poisoning loop.
- **Attestations emitted, never verified.** Pipeline attestations exist; no downstream consumer verifies them; the chain is uncollapsed.
- **Specialist not engaged for a high-stakes fine-tune.** The organisation ships a high-autonomy fine-tune without any adversarial-robustness or back-door review beyond the authors' own eval.

## Summary

- The malicious-model-artefact risk surface includes pickle code-execution, framework-specific execution paths (HDF5 custom layers, TF graph ops, ONNX custom operators), dataset back-doors, base-model back-doors, LoRA tampering, training-dependency compromise, and container-layer compromise.
- The auditor's threat-to-control map is the first workpaper; each row pins a defence the organisation claims and its evidence.
- ModelScan and `picklescan` are the practitioner tools whose operation, configuration, and output-acting the auditor tests; reperformance is independent scan against a sampled artefact.
- Signature verification closes the "clean scan" loop with "right artefact" — cosign / Sigstore for internal and increasingly for vendor-published artefacts, with Rekor log entries as the transparency substrate.
- The registry sweep samples production artefacts across format, age, and provenance category and reports unsigned / unscanned counts with the chapter 6 gate failure cascade.
- The fine-tune supply-chain audit covers dataset back-doors, training-data injection, and LoRA-weight tampering, with ISA 620 specialist involvement for the deeper techniques.
- Pipeline-integrity controls (isolation, dependency lock, review, attestation emission) are the SLSA / in-toto substrate for fine-tunes; findings here feed up to chapter 1 and down to chapter 6.
- Chapter 6 picks up the registry-ingestion gate as a system; chapter 5 picks up GPAI-provider documentation as the input source; chapter 2 is the vendor-diligence umbrella.
