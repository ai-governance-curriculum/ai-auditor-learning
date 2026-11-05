# Auditing the Adversarial-ML and Robustness Program

## Motivation

Classical adversarial machine learning — the long research tradition of evasion, poisoning, extraction, and privacy attacks against supervised models — predates the LLM red-team programme discussed in chapter 3 and is still live. For organisations with deployed classical-ML systems (credit scoring, fraud detection, computer vision, speech, recommender systems), adversarial-ML robustness is a first-order risk. For organisations with GenAI systems, the adversarial-ML discipline still applies to upstream classifiers, output filters (chapter 7), embedding models, and retrieval components.

The auditor's job in this chapter is to test *attack coverage* against NIST AI 100-2's canonical taxonomy, to validate the *defence-baseline evidence* the organisation claims, to confirm the *residual-risk updates* after each mitigation round, and to verify the *re-run cadence* is maintained in production.

As in chapter 3, the auditor does not re-author the attack methodology; that depth sits with `ai-risk-engineer` (L25) and with the adversarial-ML research literature. The auditor runs the canonical attack suite as a reperformance check and reads the organisation's artefacts against NIST AI 100-2.

## The NIST AI 100-2 attack taxonomy

NIST AI 100-2 (the "Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations" publication, first released 2023 and revised since) is the auditor's reference. The structure the auditor uses as a coverage framework:

### By attack class

- **Evasion attacks.** Adversarial perturbation at inference to change the model's prediction. Image perturbations (FGSM, PGD, C&W, AutoAttack), text-level attacks (TextFooler, BERT-Attack, TextBugger), speech perturbations, and prompt-level attacks for LLMs.
- **Poisoning attacks.** Training-time attacks that influence the model's behaviour via training-data manipulation — data poisoning, backdoor / Trojan attacks, clean-label attacks, model supply-chain poisoning.
- **Privacy attacks.** Attacks that recover sensitive information about the training data or the model itself — membership inference (chapter 6), model inversion, attribute inference, training-data extraction.
- **Abuse attacks.** (Added in the generative-AI update.) Attacks that use the model to produce harmful output by design rather than by perturbation — jailbreaks, prompt injection, agent misuse.

### By attacker access

- **White-box.** Full model access.
- **Grey-box.** Partial model access — architecture known, parameters not; or queries with gradient access.
- **Black-box.** Query access only; transfer-attacks included.

### By target

- **Availability.** Attacks that degrade the model's utility.
- **Integrity.** Attacks that change the model's output for a target input.
- **Privacy.** Attacks that extract information.

The three-axis combination defines a coverage space. A programme's declared coverage should populate the cells the organisation's systems are exposed to; the auditor tests that the exposed cells are populated with evidence.

<!-- needs-research: cite the exact NIST AI 100-2 edition and the generative-AI update version in force at reading time -->

## The coverage matrix (and the overlap with chapter 3)

Chapter 3 introduced the OWASP-LLM-Top-10 / OWASP-ML-Top-10 / MITRE-ATLAS / NIST-AI-100-2 cross-tagged coverage matrix. The adversarial-ML audit uses the same matrix but with a different *fill pattern*:

- **For classical-ML systems (vision, tabular, sequence).** The matrix is dominated by OWASP ML Top 10 and NIST AI 100-2 evasion / poisoning / privacy rows; the OWASP LLM Top 10 column is largely empty.
- **For GenAI systems.** The matrix is dominated by OWASP LLM Top 10 and NIST AI 100-2 abuse rows; the OWASP ML Top 10 and classical-adversarial-ML rows cover the upstream classifier / retriever / embedding components.
- **For hybrid systems.** Both fill patterns coexist; the matrix is wider.

The auditor requests the matrix (or constructs it from the organisation's artefacts) and checks that the cells the deployment surfaces are populated with evidence.

## The attack-coverage test

For each exposed cell, the auditor verifies the attack has been attempted with a defensible method. The canonical open-source toolchain the auditor expects to see cited:

- **ART — Adversarial Robustness Toolbox** (`github.com/Trusted-AI/adversarial-robustness-toolbox`) — the most complete open-source library for classical adversarial ML: FGSM, PGD, C&W, Boundary, HopSkipJump, AutoAttack, membership inference, model extraction, poisoning, backdoor detection. IBM / LF AI & Data stewardship.
- **TextAttack** (`github.com/QData/TextAttack`) — NLP adversarial examples: TextFooler, BERT-Attack, TextBugger, PWWS, with per-constraint budget control.
- **CleverHans** (`github.com/cleverhans-lab/cleverhans`) — long-running library originally from Papernot, Goodfellow et al.; primarily evasion attacks with gradient methods.
- **Counterfit** (`github.com/Azure/counterfit`) — Microsoft's command-line interface over ART / TextAttack for red-team workflows. <!-- needs-research: confirm maintenance status at reading time — upstream was archived in 2023 -->
- **Foolbox** (`github.com/bethgelab/foolbox`) — image-focused adversarial examples; alternative / complement to ART.

For each attack class the auditor expects:

- A tool citation with version pin.
- A dataset citation (the benchmark set — CIFAR-10, ImageNet, HateCheck, GLUE / AdvGLUE, IMDb, etc. — or a representative production holdout).
- A perturbation budget (ε under the L-norm declared; token-flip budget for text attacks).
- A reported metric (clean accuracy, adversarial accuracy, attack-success-rate, average perturbation magnitude).
- A result plus a signed delta against any published baseline for the same model class.

An attack class that the programme has designated in-scope with no tool, no budget, no benchmark, and no number is a coverage finding of the strongest kind.

## The defence-baseline test

For each exposed attack class the organisation should have declared defences, not just measured attack success. Classical defence baselines the auditor should recognise:

- **Adversarial training** (Madry et al. 2018). The strongest defence for L∞ evasion in many image benchmarks, with known accuracy-robustness trade-offs.
- **Certified defences** — randomised smoothing (Cohen, Rosenfeld, Kolter 2019), interval bound propagation, Lipschitz-constrained networks. Produce certified robust radii with mathematical guarantees under stated assumptions.
- **Defensive distillation, input preprocessing, feature squeezing, detection networks.** Historical defences the organisation may cite; the auditor should know these are weak defences for strong attackers (Carlini & Wagner 2017's "defenses that don't work" line of papers).
- **Data provenance / poisoning detection.** Spectral signatures (Tran, Li, Madry 2018), activation clustering (Chen et al. 2018), STRIP (Gao et al. 2019), Neural Cleanse (Wang et al. 2019).
- **Privacy defences.** DP-SGD training and differential-privacy accounting (chapter 6).

For each declared defence:

- **Evidence of operation.** The defence is actually in the deployed model (not just in a research report).
- **Baseline comparison.** The attack-success-rate is reported both with and without the defence.
- **Reported assumptions.** Certified defences come with certified radii; the auditor records the radius and the deployment's actual perturbation exposure.
- **Known-weak defence disclosure.** If the organisation cites a defence shown in the literature to be weak against strong attackers (some pre-2019 defences), the auditor records a defence-selection finding.

A "we defend against adversarial attacks" statement with no per-attack-class evidence is a Grade-E assertion in mod-106 terms.

## The residual-risk-update test

The register (chapter 2) and the harm-model trace (chapter 1) require that *each mitigation round* produces a residual-risk re-score. The auditor samples recent adversarial-ML mitigation closures and tests:

1. **Mitigation is operating.** The defence is in place in the deployed model (sample inference-pipeline configuration, training-pipeline logs, or the model card).
2. **Post-mitigation attack-success-rate is measured.** The same attack suite was rerun after the mitigation; the result is captured.
3. **Residual-risk score is updated in the register.** The residual column reflects the post-mitigation evidence.
4. **The update is signed.** Per chapter 2's sign-off routing, the update has an approver record.
5. **The monitoring plan reflects the mitigation.** The post-deployment monitor watches for mitigation drift (chapter 8 / mod-108).

A mitigation closure without a residual-risk update is the finding pattern most often encountered. It signals that the organisation has reached mitigation-is-done fatigue; the audit response is a routing finding against chapter 2's sign-off process.

## The re-run cadence test

Adversarial-ML postures *drift*. New attacks are published; the model is retrained; the deployment envelope changes. The auditor tests:

- **The methodology declares a re-run cadence.** Per-attack-class, or per-model-version, or periodic calendar cadence.
- **The cadence is executed.** For a sample of attack classes the auditor pulls the last three runs and confirms the cadence held.
- **Triggered re-runs on model retraining.** A new model version triggers a re-run of the full attack suite at minimum before promotion; the auditor confirms per-release evidence.
- **Trigger on new published attack.** Known-high-impact new attacks (e.g., a new text-attack method with large reported accuracy drops against the organisation's model class) should trigger a targeted run; the auditor samples recent major publications and asks whether a targeted run followed.
- **Training-data-change triggers a poisoning re-run.** Each new training data integration should trigger a poisoning-detection pass.

Cadence breach is the most common finding in adversarial-ML programme audits because the programme tends to receive strong investment at launch and quieter investment as the system ages.

## Linkage to the register and the red-team programme

The adversarial-ML programme and the red-team programme (chapter 3) share the coverage matrix but produce different outputs. The auditor tests the integration:

- **Finding registration overlap.** Adversarial-ML findings should land in the same tracker as the red-team findings; dual trackers are an integration finding.
- **Severity scale consistency.** The adversarial-ML severity scale matches the register scale (chapter 2); divergent scales are a scoring finding.
- **Register trace.** Each adversarial-ML attack class in-scope maps to a register row; orphan rows are trace drift.
- **Monitor linkage.** Adversarial-ML findings produce monitors (model confidence drift, out-of-distribution input rate, attack-detection rule) that are in the `mod-108` monitoring portfolio.

An adversarial-ML programme that operates entirely separate from the register and the red-team tracker is a governance finding — the audit committee sees a fragmented picture.

## The "model-under-test" clarity test

A subtle audit finding specific to adversarial-ML programmes is *model-under-test ambiguity*: the adversarial-ML team's attacks target a model build that differs from the production build. The auditor confirms:

- **The model-under-test identifier** (checkpoint hash, weights SHA, export artefact) matches the production model, or a declared representative pre-production version.
- **The pre-processing pipeline matches.** Attacks against a model that assumes a different normalisation / tokenisation / embedding than production are not valid attacks on production.
- **The inference configuration matches.** Batch size, precision (FP16 / INT8 quantisation), hardware target, decoding settings are matched.

A programme that reports an ε-attack-success-rate against "the model" without model-identifier evidence cannot be relied on.

## Common failure modes

- **Only evasion attacks run; poisoning and privacy silent.** The programme runs FGSM / PGD and reports an ε-robustness number without a poisoning-detection or MIA attempt. Coverage finding.
- **Defence cited from the literature; not implemented in production.** The model card cites randomised smoothing but the production model is not smoothed.
- **Attack budget mis-matched to threat model.** The organisation reports L∞=8/255 robustness but the threat model includes patch attacks or L2 attacks or query-only attacks for which the number is not informative.
- **Baseline missing.** The programme reports adversarial accuracy under a defence without reporting adversarial accuracy without the defence, so the mitigation's value cannot be measured.
- **The GenAI programme omits upstream-classifier adversarial-ML.** The organisation runs HarmBench against the LLM but never runs TextAttack against the output classifier guardrail (chapter 7); guardrail robustness is silently assumed.
- **Residual-risk update is never a step in the lifecycle.** The programme closes mitigations but the register stays stale.
- **One tool.** The programme uses only ART and never TextAttack even though half the systems are NLP. Tool-bias finding.

## Summary

- NIST AI 100-2 (plus the generative-AI update) is the canonical coverage framework; the auditor tests the cells the deployment exposes.
- The coverage matrix is the chapter-3 matrix with a different fill pattern depending on whether the deployment is classical ML, GenAI, or hybrid.
- Canonical toolchain the auditor expects: ART, TextAttack, CleverHans, Counterfit (and Foolbox) with version-pinned suites and recorded perturbation budgets.
- Defence baselines are required per attack class; the attack-success-rate without the defence is the comparison target the auditor insists on.
- Residual-risk updates follow every mitigation closure; the sign-off routing from chapter 2 must execute.
- Re-run cadence is the most common failure mode; adversarial-ML programmes age quickly without periodic refresh.
- Model-under-test identity must match production; otherwise the robustness number does not describe production risk.
- Integration with the red-team programme (chapter 3) and the register (chapter 2) is itself an audit target.
