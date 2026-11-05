# exercise-06: Privacy-Risk Program Audit

**Estimated effort:** 2 hours

## Objective

Audit an organisation's **privacy-risk programme** against chapter 6's four tests: **privacy-attack coverage** (MIA / LiRA / data extraction / model inversion / canary-based memorisation), **DP-SGD (ε, δ) sufficiency** including accountant replication, **PII-pipeline coverage** (Presidio or equivalent), and **GDPR Article 22 / NIST Privacy Framework alignment**. Produce the engagement workpaper including an accountant-reperformance and a Presidio-coverage spot test.

## Prerequisites

- Chapter [`06-auditing-the-privacy-risk-program.md`](../06-auditing-the-privacy-risk-program.md).
- Working familiarity with Opacus or TensorFlow Privacy (for DP-SGD accountant), ML Privacy Meter (for MIA), Presidio (for PII).
- GDPR Articles 6, 9, 22, 35 and the NIST Privacy Framework v1.0.
- Chapter 2's register discipline.

## Scenario

**Northfield Medical** is a US regional healthcare provider deploying an AI clinical-note summarisation model trained on de-identified prior-encounter notes. Northfield's model card declares DP-SGD training at (ε, δ) = (8.0, 10⁻⁵). The deployed inference pipeline uses Presidio for input and output PII scrubbing. The organisation has a documented GDPR position (US-only operation, so GDPR narrowly scoped to EU-resident patients seen while travelling) and claims NIST Privacy Framework alignment at the Core level.

You are the lead auditor on an ISAE 3000 limited-assurance engagement commissioned by Northfield's audit committee ahead of an HHS OCR engagement.

Substitute as needed: any organisation with a privacy-relevant AI deployment and a published privacy posture. Attribute the subject.

## Requirements

1. **Pin the privacy artefacts.** Model card, DP-training logs or accountant inputs, Presidio configuration, GDPR documentation, NIST Privacy Framework alignment document — URL / reference, retrieval, hash / version.

2. **Privacy-attack coverage grid.** Populate chapter 6's grid: MIA (loss-based), LiRA (shadow-model), attribute inference, training-data extraction (for LLM content), model inversion (for structured-output models), canary-based memorisation. For each: in-scope, tool, dataset / canary, metric, last-run, result. Silent omissions for exposed classes are findings.

3. **MIA / LiRA reperformance.** If model access is available, run ML Privacy Meter or an equivalent MIA attack on a representative holdout. Report TPR at FPR=0.1% and FPR=1%, not aggregate AUC. Compare to the programme's claimed number. If access is not available, document the access gap and reproduce the organisation's declared method against a public substitute model, recording the comparison explicitly.

4. **DP-SGD accountant replication.** Obtain the accountant inputs (σ, q, T, δ, accountant family). Reproduce (ε, δ) using Opacus (`opacus.accountants`), TF Privacy, or a published PRV accountant implementation. Compare to the model-card's declared value. Record delta.

5. **DP-SGD sufficiency audit.** For the declared (ε, δ):
   - Record the privacy unit (record / user / group).
   - Record the sensitive-data category (healthcare → HIPAA de-identification shape; clinical-note content).
   - Grade sufficiency against the sensitive-data category's expected ε range.
   - Record the clipping norm, utility floor acceptance, and whether a non-DP baseline is documented for comparison.

6. **Presidio-coverage spot test.** For the configured recogniser set:
   - Confirm coverage of the deployment's data categories (HIPAA 18-identifier set for clinical).
   - Run a sample of representative inputs through the pipeline and confirm detection of each identifier type (one-row-per-type demonstration test).
   - Record FPR / FNR per identifier type from the organisation's calibration data; if absent, that is a finding.
   - Spot-review one custom recogniser (regex or ML-based) for its versioning and test discipline.

7. **GDPR per-article audit.** For each of Articles 6, 9, 22, 35, and 15–21:
   - Record the organisation's declared position / basis / evidence.
   - Note gaps or Grade-E assertions.
   - Open findings for missing evidence where the obligation applies.

8. **NIST Privacy Framework alignment check.** For each Function (Identify-P, Govern-P, Control-P, Communicate-P, Protect-P), confirm the Category-level evidence is present. Missing Categories for an in-scope Function are findings.

9. **Unlearning / right-to-erasure test.** Record the organisation's unlearning policy, SLA, recent erasure requests (sanitised evidence), and the validation of effect on the trained model.

10. **Author the finding register** per chapter 2's shape, cross-referenced to the risk register.

## Starter guidance

- The MIA metric that matters is TPR at fixed low FPR (per Carlini et al. 2022 LiRA); a programme that reports aggregate AUC near 0.5 is under-reporting the per-record exposure.
- (ε, δ) = (8.0, 10⁻⁵) for clinical data is a sufficiency finding under most practitioner heuristics (ε ≤ 3 is a common target for sensitive categories). Record and open the finding.
- Presidio's default recogniser set does not cover HIPAA Safe Harbor identifiers out-of-the-box; a HIPAA deployment needs custom recognisers for the specific identifier types.
- For accountant replication: Opacus's `RDPAccountant` is the baseline; Gopi, Lee, Wutschitz 2021 PRV accountant is tighter. Reproducing with multiple accountants and comparing the tight-vs-loose bound is useful evidence.
- GDPR Article 22 applies even to US-only organisations when the processing concerns EU residents' data; the "US only operation" caveat does not relieve the obligation for EU-resident data subjects.
- Unlearning on a trained model is a hard problem; most organisations rely on "retrain next cycle" with a declared SLA. The finding is about whether the SLA is operationalised and the evidence trail is present.

## Acceptance criteria

The deliverable is accepted when:

- All privacy artefacts are pinned.
- The attack-coverage grid is populated with in-scope / out-of-scope annotations and per-row evidence (or `not tested` with rationale).
- MIA reperformance reports TPR at FPR=0.1% and FPR=1% (or documented access gap with substitute-model comparison).
- DP-SGD accountant replication is present with declared σ, q, T, δ, accountant family, reproduced (ε, δ), and delta vs. declared.
- Sufficiency judgement is recorded against the sensitive-data category with explicit rationale.
- Presidio coverage test is present with per-identifier-type demonstration and FPR / FNR audit (or finding where absent).
- GDPR per-article audit covers at least Articles 6, 9, 22, 35, and 15–21 with declared position per article.
- NIST Privacy Framework alignment is tested at the Category level for each Function.
- Unlearning policy is documented with SLA and evidence trail.
- Finding register cross-references to the risk register.
- Primary sources cited; `<!-- needs-research: ... -->` where claims cannot be pinned.

## Stretch goals

- Build a small **DP-SGD accountant playground** script that takes (σ, q, T, δ, target_ε) and reports the tightest ε under three accountant families (RDP, Gaussian DP, PRV). Useful as an auditor-held independent reproduction tool.
- Draft a **HIPAA-specific Presidio custom-recogniser set** — the 18 Safe Harbor identifiers with the regex / ML patterns the organisation should adopt.
- Produce a **MIA-exposure dashboard mock** — the per-record TPR-at-fixed-FPR distribution, showing the tail of exposed records (chapter 6's point: averages hide the tail).
- Draft the **right-to-erasure runbook** — the workflow from subject request to validation-of-effect-on-model, including the SLA and the evidence artefacts.
