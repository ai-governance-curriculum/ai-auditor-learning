# Auditing Model-Signing and Registry-Ingestion Gates

## Motivation

Chapter 1 established provenance as the auditor's evidentiary substrate. Chapter 4 established scanning and signature *verification* as the content-and-identity test on individual artefacts. This chapter tests the **gate** — the control that ensures only artefacts meeting the organisation's policy ever reach production. The gate is where provenance claims, scanning decisions, and signature verifications combine into a single admit-or-reject decision at registry ingestion, and again at deployment.

Model-signing and registry-ingestion gates are the specific technical control the auditor is likely to find in a mature ML-platform team's hands, and they are the clearest place for the auditor to test "only approved artefacts reach production" as an empirical claim rather than a policy aspiration. The gate is designed, operated, and defended by `ai-infra-security` / `security-learning` (level 35) — the auditor's role is the complement: testing the policy, the policy's evaluation, the gate's bypass surface, the gate's log, and the registry's post-gate state.

This chapter frames the gate as an auditable control surface. The deliverable is a pattern of evidence that the gate operates and that no artefact in the production registry got there outside it.

## The gate as a system

The organisation's gate is rarely a single service — it is a pipeline of checks typically arranged as follows:

```
build → sign (cosign + Fulcio + Rekor) → scan (ModelScan / picklescan / Trivy)
      → attestations emitted (in-toto predicates, SLSA provenance)
      → registry ingestion gate
         (policy evaluator — OPA / Rego, Kyverno, in-house policy engine)
         (verifies signatures, checks policy, logs decision)
      → registry entry created / rejected
      → deployment admission (Kubernetes admission controller / CI gate / serving platform)
         (re-verifies signatures, re-checks policy, logs decision)
      → production
```

The auditor's test is over the whole pipeline, with particular attention to:

- Where the gate decision is made.
- What policy the decision is evaluated against.
- What happens on policy failure (block vs. warn vs. ignore).
- What logs the decision emits.
- What prevents the gate being bypassed.

## The policy as evidence

The gate is only as strong as the policy it evaluates. The auditor's first fieldwork step is the **policy inventory** — enumerate the policies the gate enforces, capture them as artefacts (OPA Rego files, Kyverno policies, in-house JSON/YAML, admission-controller rules), and record their version, owner, and approval history.

Policy categories the auditor should expect:

- **Signature policy.** Artefacts must be signed by an identity in the trusted-signer policy. The auditor confirms the allowed identities, the issuer, the certificate-identity regex, the expected signer workload for each artefact class.
- **Scanner policy.** Artefacts must have a current scanner result at or below a specified severity. The auditor confirms the severity thresholds and the scanner-version pinning.
- **Provenance policy.** Artefacts must have an in-toto attestation chain to a known build-run identity. The auditor confirms predicate types required (SLSA Provenance, VSA, in-house dataset-provenance predicate).
- **SBOM / ML-BOM policy.** Artefacts must have an accompanying SBOM / ML-BOM. The auditor confirms format (CycloneDX, SPDX) and content requirements.
- **Licence policy.** The composed licence posture must be acceptable. The auditor confirms the licence-compatibility rules.
- **Registry-source policy.** Artefacts from external registries (Hugging Face mirror, S3 external prefix, vendor OCI registry) are subject to a tighter policy than internal CI outputs.
- **Format policy.** Pickle artefacts may be blocked; `safetensors` or other non-executable formats preferred.
- **Metadata policy.** Required tags (environment, business owner, risk tier, review date, retirement date).
- **Exception / allowlist policy.** A documented exception process; exceptions are time-bound, owned, and reviewed.

The policy artefact test:

- **Version controlled.** Policies in source control.
- **Reviewed.** Merges to the policy repo pass human review.
- **Signed deployment.** Policy deployment to the gate uses a signed workflow; the gate verifies the policy signature.
- **Effective dates.** Policy changes have an effective date and a prior-version archive.

A gate that evaluates against the wrong or stale policy is a decision-quality defect even if the gate otherwise operates.

## Reperforming a gate decision

For a sampled set of artefacts the auditor independently reperforms the policy evaluation and compares to the gate's logged decision.

The reperformance steps:

1. **Retrieve the artefact and its metadata.** Hash, signature material, scanner output, attestations, SBOM.
2. **Retrieve the policy as it was at the ingestion moment.** Policy repo tag or policy-engine snapshot; the gate's logs should name the policy version used.
3. **Independently evaluate.** Run the policy against the artefact (for OPA: `opa eval`; for Kyverno: `kyverno apply`; for in-house engines: the organisation's reference evaluator). Compare the auditor's decision to the gate's.
4. **Record the delta.** A mismatch is a gate-decision finding — either the gate evaluated differently, or the artefact state has drifted, or the policy state has drifted.

```bash
# Illustrative OPA reperformance
opa eval --data policy/ \
         --input artefact-metadata.json \
         --format pretty \
         'data.model_ingestion.allow'
```

The auditor's workpaper per sampled artefact: artefact ID, policy version, auditor decision, gate decision, delta, pointer to the evidence bundle.

## The log is the control

A gate that cannot show you its decisions is not a gate — it is a hope. The auditor's test:

- **Per-decision log entry.** Every ingestion decision (accept, reject, override) emits a log entry. Fields: timestamp, artefact ID, policy version, decision, evaluator identity, exception reference (if any).
- **Log retention.** Logs retained for at least the artefact retention horizon, so a historical artefact's ingestion evidence is still recoverable.
- **Log immutability.** Logs go to an append-only store (an immutable bucket with object-lock, or a signed-and-attested event store). A gate log that can be rewritten is weak evidence.
- **Log reperformance.** For a sampled artefact, the log entry resolves to the artefact in the registry (and vice versa — pick a log entry and demand the artefact).
- **Rejection logs preserved.** Rejected artefacts' log entries must be retained, not discarded; the rejection pattern is audit evidence that the gate is doing work.

A registry with artefacts whose ingestion-log entries cannot be produced is a log-integrity finding, independent of whether the artefact's content is clean.

## The bypass surface

The sharpest finding in gate auditing is a **bypass** — a path around the gate that puts an artefact into the registry without the policy evaluation.

Common bypass paths:

- **Direct registry write.** The registry (MLflow, Vertex AI Model Registry, SageMaker Model Registry, Unity Catalog, OCI registry, etc.) exposes a write-path independent of the CI gate — an operator with registry-admin credentials can put an artefact in.
- **Alternate registry.** The organisation has multiple registries, and the gate is enforced on one but not another.
- **Alternate deployment path.** A model can be loaded from a file (S3 URL, local PV, local filesystem) at serving time without going through the registry at all.
- **Container-embedded model.** A container image bundles a model in its filesystem; the gate inspects the registry, not the image. (The container-image gate is the complementary control; both must hold.)
- **Developer registry bleeding into production.** A "dev" registry is less-strict; a dev entry gets promoted to prod via a path that skips the strict-gate policy.
- **Exception-process abuse.** The exception process is intended for narrow cases; it has become the normal path.

The auditor's bypass test:

- **Enumerate write-paths.** For each registry and each deployment path, who has write access? What operations reach production? What logs are produced?
- **Ingress-point audit.** Pull the registry's audit log (not just the gate log) and compare — every registry write must correspond to a gate decision.
- **Identity-based test.** Enumerate the identities with registry-admin rights and the identities who can push to the OCI registry. If the set is wider than the ML-platform service identities, record a finding.
- **Deployment-surface test.** For the model-serving platform (vLLM, Triton, TGI, Bedrock endpoint, SageMaker endpoint, Vertex endpoint, Databricks endpoint), what ways can a model be loaded? Any load-from-arbitrary-URL path is a bypass surface.
- **Exception-rate monitoring.** Count the exceptions issued in the period. An exception rate significantly above the policy's expectation is a finding against the policy as operated.
- **Dev-to-prod promotion audit.** For a sample of production artefacts, confirm the promotion path included the strict-gate policy.

Bypass findings are high severity — a single working bypass path makes every other gate control into decoration.

## SLSA level operationalisation at the gate

Chapter 1 introduced SLSA as a claim the organisation makes about build integrity. The gate is where the claim becomes operational — the gate consumes the SLSA provenance and refuses artefacts without it. The auditor tests:

- **Required provenance type.** The policy specifies the required predicate (e.g., `slsa.dev/provenance/v1.0`).
- **Required builder identity.** The policy restricts accepted builder identities (CI workload identity, hermetic-builder service account).
- **Required source material.** The provenance material references source code in the expected repository.
- **VSA (Verification Summary Attestation) consumption.** For SLSA L3+, VSAs may be a shorter-path verification artefact; the auditor confirms VSAs are used or not used consistent with the policy.
- **Degraded-mode handling.** When provenance is not yet available for legacy artefacts, how does the policy handle this? A grandfathering rule needs documentation, expiration, and tracking.

A SLSA-L3 declaration with a gate that does not verify the hermetic-builder constraint is the overclaim this chapter catches.

## Deployment-time admission

The registry gate is not the only admission point. The deployment-time admission control re-evaluates when the artefact is pulled into production.

- **Kubernetes admission.** Admission controllers (Kyverno, Gatekeeper, in-house policy webhooks, image-policy webhooks, Sigstore policy-controller) verify image signatures on pod admission.
- **Serving-platform admission.** The serving platform (SageMaker endpoint, Vertex endpoint, Bedrock custom model, in-house server) confirms the model artefact's signature at load time.
- **CI-to-deployment gate.** The CI job that deploys to production re-verifies the registry entry's signatures and policy decision at promotion time, so a tampered registry entry between ingestion and deployment is caught.

The auditor tests whether admission happens at all three stages, or where a stage is omitted, why.

## Rotating and revoking keys

Signing keys and workload identities rotate. Revocation handling is where many gate implementations are fragile.

- **Rotation cadence.** Signing identities are short-lived (Fulcio-issued certificates typically minutes to an hour) by design. Longer-lived keys have a rotation cadence declared in the key policy.
- **Revocation mechanism.** A compromised identity is revoked; downstream verifications fail. The gate consults Rekor for log-validity and OCSP / CRL (where applicable) for certificate state.
- **Artefact rescue.** Where an identity is revoked but the artefacts it signed are still needed, a VSA signed by a different identity provides continuity. The auditor confirms the rescue mechanism exists in policy.
- **Historical verification.** Rekor retention preserves the history; the auditor can verify an old signature was valid at its time of signing even if the identity has since been revoked.

## Gate telemetry — what a mature control emits

A mature gate emits:

- **Decisions per unit time.** Accept / reject / override counts.
- **Reject reasons.** Breakdown by policy rule.
- **Override counts and identities.** Broken out by exception owner.
- **Scanner output per artefact.** Flagged issues aggregated.
- **Policy-version churn.** Policy updates per month.
- **Latency.** Time from build completion to accepted-in-registry.
- **Bypass attempts.** Rejected direct-registry-write attempts, flagged non-gate write attempts.

The auditor consumes this telemetry as the operational-evidence summary for the period. A gate without telemetry leaves the auditor dependent on individual artefact sampling; a gate with telemetry turns the audit into a population-level analysis with targeted sampling for exceptions.

## The ai-infra-security interface

The `ai-infra-security` / `security-learning` (level 35) curriculum authors the runtime-hardening complement to this chapter — the hardened serving environment, the egress controls, the MIG / namespace isolation, the token / credential management. The auditor's chapter here tests the ingestion side; the ai-infra-security side tests the runtime side. Both are necessary:

- The ingestion gate can keep malicious artefacts out of the registry; the runtime hardening keeps compromised artefacts from doing damage if one does reach production.
- The runtime hardening can isolate a model that calls unexpected network endpoints; the ingestion gate prevents a model with a known back-door from being accepted in the first place.

The auditor records which controls fall to which team, and tests the interface — specifically, the gate's reject-event feed into the security team's monitoring so a rejected ingestion attempt does not vanish into a developer-visible-only log.

## Common failure modes

- **Gate present, bypass surfaces open.** The gate is well-engineered on the happy path; registry-admin credentials or alternate deployment paths work around it.
- **Policy stale.** The policy was authored months or years ago; signing-identity rotations, new artefact classes, new scanner rules have not been reflected.
- **Scanner version pinned too tight.** Scanner version is pinned; the pin is from before the current threat landscape.
- **Overrides are the normal path.** Exceptions issued at a volume comparable to approved decisions; the gate enforces nothing.
- **No deployment-time admission.** The registry gate holds; the serving platform accepts any artefact URL.
- **Logs not retained.** Gate decisions are logged ephemerally; a historical reperformance has nothing to compare against.
- **Container-embedded model path.** A model is baked into an image and reaches production without the model-registry gate ever running.
- **Policy reperformance disagrees.** Independent policy evaluation disagrees with the gate's logged decision for some sampled artefacts.
- **Dev registry bleeds.** A dev-tier artefact is promoted to prod via a shortcut that misses the strict-tier policy.
- **SLSA overclaim.** The organisation claims SLSA L3 at the gate; hermetic-builder constraint is not actually enforced; provenance is accepted from any builder.

## Summary

- The gate is the control that collapses provenance, scanning, and signature verification into a single admit-or-reject decision at registry ingestion (and again at deployment admission).
- The policy artefact is the gate's evidence base; versioned, reviewed, and signed deployment of the policy is the baseline condition for the gate being auditable.
- Reperforming a gate decision — independently running the policy against the artefact and comparing to the gate's log — is the core audit test; disagreements are gate-decision findings.
- The gate's log is the operational evidence; per-decision entries, immutable retention, and reperformable linkage to artefacts and registry entries are the test criteria.
- Bypass surfaces are the sharpest finding type — enumerate write-paths, deployment paths, developer registries, and container-embedded model paths; count exception-process usage.
- SLSA-level claims are operational at the gate, not just documented at chapter-1 level; overclaims appear when the gate accepts non-hermetic provenance.
- Deployment-time admission re-verifies at the point of load; a gate without deployment-side admission leaves the registry-to-production link unguarded.
- Key rotation, identity revocation, and historical verification via Rekor are the long-run hygiene the gate needs to remain reliable.
- The gate interfaces with `ai-infra-security` runtime hardening; the auditor records which controls each team owns and tests the interface.
- Chapter 1 is the provenance substrate; chapter 4 is the per-artefact content test; this chapter is the gate that enforces both at the registry boundary.
