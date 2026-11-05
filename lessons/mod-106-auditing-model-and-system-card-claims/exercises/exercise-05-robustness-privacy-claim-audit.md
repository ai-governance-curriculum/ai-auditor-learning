# exercise-05: Robustness and Privacy Claim Audit

**Estimated effort:** 3 hours

## Objective

Audit a robustness claim and a privacy claim to the chapter-6 shape: attack-surface coverage, adversarial-budget plausibility, DP-accounting plausibility, MIA TPR-at-fixed-FPR cross-check, replay-bundle integrity. Produce the two per-claim audit workpapers and the aggregate scope-restrictions note.

The target is the "operational-safety tier" of the card: numbers that look technical and defensible until the auditor looks at the methodology behind them.

## Prerequisites

- Chapter [`06-auditing-robustness-privacy-and-red-team-claims.md`](../06-auditing-robustness-privacy-and-red-team-claims.md).
- `art` or `textattack` installed for the robustness replication.
- `opacus` (or `tensorflow_privacy`) available for inspecting a DP accountant; `ml_privacy_meter` or an equivalent MIA toolkit for the empirical MIA cross-check.
- WORM-style storage for payload-bearing artefacts (chapter 6; `mod-104` chapter 4).

## Scenario

Two subject-of-audit scenarios — pick one or run both at half-depth:

**Scenario A — Robustness.** A published NLP content-classifier card (any real text-classification model card — HateBERT, Perspective API documentation, a HF community toxicity classifier) states "robust to adversarial perturbations with an accuracy drop of less than 6 pp under TextFooler at ε (semantic-similarity floor) = 0.84, n = 1,000 Yelp reviews." The audit must test that claim.

**Scenario B — Privacy.** A published model card (a DP-SGD-trained language or vision model, e.g., the Opacus tutorial family or a published DP-fine-tuned medical-imaging model) states "trained with DP-SGD at (ε, δ) = (3.0, 10⁻⁵) composed across pretraining and fine-tuning" and reports "no observable membership-inference advantage above 0.52 AUC on the Carlini LiRA attack, n = 2,000." The audit must test both the accountant plausibility and the empirical MIA.

Where the subject model is not practical to replicate (compute, access), substitute an analogous public model and document the substitution.

## Requirements

**Scenario A — Robustness**

1. **Record the anatomy of the claim** — threat model, attack, budget, metric, baseline, sample. Flag any missing element.
2. **Audit the attack-surface coverage.** Is TextFooler the right attack for the deployment (toxicity-moderation of user-generated text)? What other attacks does the deployment realistically face (homoglyph / unicode, paraphrase, semantic-equivalent substitution, injection-of-politeness, non-English input)? Record uncovered attack classes.
3. **Audit the adversarial budget.** Is ε = 0.84 (USE similarity floor) permissive or strict for this deployment? Cite the TextAttack standard default and justify whether the budget fits the attack surface.
4. **Replicate the attack.** Run TextAttack's TextFooler recipe against the subject on at least 200 examples (full 1,000 if compute permits); record clean accuracy, adversarial accuracy, accuracy drop, attack success rate, with bootstrap CIs.
5. **Produce the signed-delta row** against the card's "<6 pp" claim.
6. **Document the attack-surface-coverage finding** (if any) — the gap between what the card tested and what the deployment faces.

**Scenario B — Privacy**

1. **Pull the DP accountant log** (the card should link it; if not, open an information request and record the absence). Re-run the accountant with the declared hyperparameters (σ, C, batch, sample rate, epochs, δ) using Opacus's `RDPAccountant` or TF Privacy's PRV accountant; report the computed ε alongside the claimed ε.
2. **Audit composition.** Does the ε reported cover pretraining + fine-tuning + any RLHF? Record the composition posture.
3. **Audit δ choice.** Is δ < 1/n? Record.
4. **Replicate the empirical MIA.** Use ML Privacy Meter's LiRA implementation (or an equivalent) on the subject model and a declared shadow-model set. Report TPR at FPR = 0.001 (not AUC alone; chapter 6's methodology note).
5. **Cross-read.** Does the empirical MIA result corroborate the DP claim? A strong DP posture (ε ≈ 3) should produce near-random MIA at tight FPR; a loose DP posture may show empirical leak well before the theoretical bound is tight.
6. **Produce the signed-delta rows** — accountant-ε delta and MIA-TPR delta.
7. **Document the privacy audit workpaper** — pinned configuration, result tables, scope restrictions (retraining not possible; vendor's shadow set was / was not shared).

**Cross-cutting (both scenarios)**

7. **Payload / sensitive-artefact handling.** Any adversarial example that lands in your archive is a limited-disclosure artefact. Any MIA target record is a restricted-disclosure artefact (it reveals a training-set membership). Classify each file, apply the chapter-6 disclosure discipline.

## Starter guidance

- The chapter-6 "anatomy of a claim" rubric is the structuring aid; a card that fails on one of {threat model, attack, budget, metric, baseline, sample} is a weak claim regardless of the number.
- Where you cannot replicate (e.g., the DP-SGD claim's accountant log is not shared), the deliverable records the information request and the replication status as "procedurally audited; empirically unverifiable; recommend vendor supply the accountant log."
- Running TextAttack: `textattack attack --recipe textfooler --model <HF-model> --dataset-from-huggingface yelp_polarity --num-examples 200`. Pin the TextAttack release.
- Running Opacus accountant: `from opacus.accountants import RDPAccountant; accountant.step(noise_multiplier=σ, sample_rate=B/N); accountant.get_epsilon(delta=δ)`.
- Running LiRA: ML Privacy Meter's `likelihood_ratio_attack` or an equivalent; prepare shadow models matched to the subject.
- The empirical MIA is expensive to run from scratch; if your compute budget does not allow it, run on a smaller proxy model (same architecture, fewer params) and declare the proxy in the manifest.
- MIA attacks on large frontier models often require vendor-shared logits; if the endpoint exposes only text, record that the attack class is not executable and treat as a scope restriction.

## Acceptance criteria

The deliverable is accepted when:

- The anatomy-of-the-claim rubric is populated for each audited claim.
- Attack-surface coverage is analysed (robustness) or DP-composition / δ-choice is analysed (privacy); gaps are named.
- A pinned replication was executed; raw per-example outputs (robustness) or raw per-record MIA scores (privacy) are archived; SHA-256 sums are computed.
- Bootstrap CIs are reported with 10,000 resamples at seed 42.
- Signed-delta rows are emitted for each per-metric replication.
- Scope restrictions are explicit — any missing accountant log, any unexecutable MIA, any proxy-model substitution.
- Payload / sensitive-artefact disclosure classification is applied; no restricted payload appears in the public-variant deliverable.
- The privacy audit's cross-read between accountant-ε and empirical MIA is explicit; a high empirical MIA against a strong DP claim is reported as a finding candidate.
- No step of the exercise authored a novel attack or novel estimator (chapter 2's borrowing discipline).

## Stretch goals

- Run a **second robustness attack** (e.g., `DeepWordBug` or `BERT-Attack`) as a cross-check; where results diverge, name the divergence as evidence of attack-selection-sensitivity.
- For the privacy audit, run a **shadow-model sweep** (ten shadow models, different random seeds) to tighten the LiRA estimate; report the variance across shadows.
- Author a **DP-accounting information-request letter** to the vendor — a one-pager asking for the accountant log, hyperparameter trace, and composition framework, in the shape a reasonable vendor-counsel would read.
- Draft a **"red-team-programme interview" question set** for the vendor's privacy lead — ten questions grounded in the audit, each tied to a specific chapter-6 shape test.
- Where the audit surfaces adversarial examples that look like real deployment risk, flag the aggregation pattern as a candidate pattern finding (`mod-105` chapter 2 definition).
