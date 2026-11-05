# exercise-04: Adversarial-ML Coverage Audit

**Estimated effort:** 2 hours

## Objective

Audit an organisation's **adversarial-ML and robustness programme** against chapter 4's four tests: **attack coverage** against the NIST AI 100-2 taxonomy, **defence-baseline evidence**, **residual-risk update after mitigation**, and **re-run cadence**. Produce a reperformance result for one attack class within the auditor's independence envelope, and the engagement workpaper the audit-committee reviewer can rely on.

## Prerequisites

- Chapter [`04-auditing-adversarial-ml-and-robustness.md`](../04-auditing-adversarial-ml-and-robustness.md).
- Working familiarity with at least one of: ART (Adversarial Robustness Toolbox), TextAttack, CleverHans, Foolbox.
- NIST AI 100-2 (current edition; see `resources.md`).
- Chapter 2's register-audit discipline — residual-risk updates land in the register.
- `mod-104` sampling and evidence discipline.

## Scenario

**Tideline Credit Union** operates a classical-ML credit-approval model (gradient-boosted trees over tabular features) and a vision-based identity-verification model (CNN classifier on uploaded ID photos). Tideline has a "Model Robustness" workstream owned by the ML engineering team, with an external penetration-test contractor who runs annual adversarial-ML assessments on both models. The most recent report is nine months old; the credit model was retrained three months ago.

You are the lead auditor on an SR 11-7-aligned model-risk-management review commissioned by the credit union's audit committee. The chapter-4 audit is a scope-defined chapter.

Substitute the scenario if needed: any organisation with a classical-ML system you can observe and get evidence from; or a public ML model (a Hugging Face or TF Hub image classifier; a public tabular model from a Kaggle competition) you pick as a representative target.

## Requirements

1. **Pin the models under audit.** Record architecture class, data domain, training-data provenance summary, declared model version / checkpoint hash, deployment timestamp.

2. **Build the NIST AI 100-2 coverage grid.** Rows: evasion, poisoning, privacy, abuse (for GenAI if applicable). Columns: white-box / grey-box / black-box; availability / integrity / privacy. Mark each cell with `in-scope` / `out-of-scope (rationale)` / `in-scope, not tested`. Silent omissions where the deployment is exposed are the finding you are seeking.

3. **Catalogue the current programme's attack evidence.** For each in-scope cell: tool, tool version, suite, dataset, perturbation budget (ε-norm; token-flip budget), metric reported, result, last-run date, mitigation if any. Rows without complete attack evidence are findings.

4. **Spot-reproduce one attack class.** Pick a representative attack with a public reference implementation:
   - For a vision model: ART's PGD at L∞=8/255 against a holdout.
   - For a tabular model: ART's BoundaryAttack or HopSkipJump (black-box) or a custom gradient attack if grey-box.
   - For an NLP model: TextAttack's TextFooler at the default constraint set.
   
   Record: tool / version / attack / budget / dataset / seed / clean accuracy / adversarial accuracy / attack-success-rate / vs. organisation's claimed number. Document the delta.

5. **Defence-baseline audit.** For each in-scope attack class, record the organisation's declared defence (if any), whether it is in the deployed model, whether attack-success-rate is reported both with and without the defence, and whether the chosen defence is defensible against the current threat model. Known-weak defences (defensive distillation, simple input preprocessing against strong attackers) get a documentation finding.

6. **Residual-risk update test.** For at least three mitigation closures in the programme's recent history, trace the four steps: defence in deployment, post-mitigation attack-success-rate measured, register residual-risk updated (chapter 2), monitor updated (`mod-108`). Closures with broken chains are findings.

7. **Re-run cadence test.** Pull the declared cadence. For each cadence row, confirm the last three runs. Model retraining triggers (the credit retrain three months ago, per scenario) should trigger a full attack-suite re-run; confirm.

8. **Model-under-test clarity.** For one attack-class report, confirm the model identifier (checkpoint hash, exported-artefact SHA) and the inference-pipeline configuration match production. Mismatches are findings.

9. **Author the finding register for the exercise** per chapter 2's shape: ID, severity, category (coverage / defence / residual / cadence / under-test / tool-pin), evidence pointer, recommended management response placeholder.

## Starter guidance

- NIST AI 100-2 covers more ground than most programmes actually cover; expect several `in-scope, not tested` cells.
- When the subject is a tabular model, poisoning and MIA are commonly under-tested; expect findings in those cells.
- For the spot-reproduced attack, you do not need to achieve state-of-the-art; you need to demonstrate the reproducibility of the programme's claim with a defensible baseline attack.
- If the organisation uses `adversarial_robustness = "we use adversarial training"` without a certified radius or without evidence the model under audit was actually trained with adversarial examples, open a defence-baseline finding.
- Record the perturbation budget explicitly; L∞=8/255 and L∞=16/255 are not the same number and conclusions do not transfer.
- Where you cannot reproduce because you lack access, document the access gap and the finding is "insufficient evidence for independent reperformance."

## Acceptance criteria

The deliverable is accepted when:

- Models under audit are pinned (version / checkpoint hash / deployment timestamp).
- The NIST AI 100-2 coverage grid is produced with per-cell in-scope / out-of-scope / untested annotations.
- Per-cell attack evidence is tabulated with all nine columns (tool, version, suite, dataset, budget, metric, result, last-run, mitigation).
- One attack class is spot-reproduced with full tool / version / budget / dataset / seed / result / delta.
- Defence-baseline audit is present with per-attack-class defence-vs-no-defence numbers.
- Three mitigation closures have been traced through the four-step residual-risk update chain.
- Re-run cadence is sampled with last-three-run evidence and model-retrain trigger confirmation.
- Model-under-test clarity has been confirmed for one attack class.
- Finding register is complete with severity classifications and criterion references.
- `<!-- needs-research: ... -->` used where a claim cannot be fully pinned.

## Stretch goals

- Build a small **ART test harness** script (≤80 lines) that produces a reproducible PGD attack result on a public CIFAR-10 model, so the organisation has a vendor-independent baseline it can run against future models.
- Draft the **model-retrain-triggered robustness checklist** — the one-page memo the organisation's MLOps pipeline would gate on before promoting a retrained model.
- Produce a **threat-model-to-attack-budget crosswalk** for the organisation's declared threat model: for each adversary profile (external attacker with no access, authenticated API user, insider with model weights), the appropriate attack budget and the appropriate tooling.
- Draft a **poisoning-detection pass** for the next training-corpus integration — which tool (Spectral Signatures, Neural Cleanse, STRIP, activation clustering), which decision thresholds, which owner.
