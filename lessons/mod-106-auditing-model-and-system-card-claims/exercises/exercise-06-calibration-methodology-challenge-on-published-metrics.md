# exercise-06: Calibration-Methodology Challenge on Published Metrics

**Estimated effort:** 2 hours

## Objective

For each row in the exercise-01 claim register, apply the chapter-4 calibration-methodology challenge: sample size / sampling procedure / evaluator reliability / uncertainty quantification. Emit the **calibration-challenge appendix** that chapter 7 attaches to the report.

This exercise is light on new compute and heavy on reading. It is where the auditor demonstrates that a number on a card is not the same as a defensible claim.

## Prerequisites

- Chapter [`04-calibration-methodology-challenge.md`](../04-calibration-methodology-challenge.md).
- exercise-01 claim register (ideally 20+ rows).
- `scipy`, `statsmodels`, `numpy` for the applied statistical computations.

## Scenario

Continuing the exercise-01 subject (Harbor-Triage-v2 or your chosen real card). The engagement needs a calibration-challenge appendix that grades every performance / fairness / safety / privacy claim for methodological defensibility, independently of whether the number itself replicates.

## Requirements

1. **Walk every register row** and populate the calibration-challenge table columns:

   ```
   claim_id | family | reported_value | reported_ci | reported_n | reported_judge | reported_judge_calibration | reported_sampling |
   auditor_computed_wilson_ci (where applicable) | auditor_computed_bootstrap_ci (where raw data available) |
   judge_calibration_grade | sampling_grade | uncertainty_grade | aggregate_grade (strong / qualified / weak / unsupported) | rationale
   ```

2. **For every reported rate without a published CI**, compute the Wilson score 95% CI at the reported rate and sample size. Where sample size is unstated, grade the uncertainty-quantification dimension as `absent`.

3. **For every judge-mediated metric** (LLM-as-judge or human-panel), record:
   - the judge's identity and version;
   - whether the card discloses a judge-calibration study against human ground truth;
   - the agreement statistic the calibration reported (kappa / ICC / classification agreement);
   - the auditor's grade of the judge-reliability dimension.

4. **For every fairness / sampling-sensitive metric**, record:
   - the test-population declaration;
   - the stratification and reference-class choice;
   - the per-subgroup sample size (surface the cell with the smallest n);
   - the auditor's grade of the sampling dimension.

5. **For every "improvement over baseline" claim**, record:
   - the effect size (card value - baseline value);
   - whether the card reports a CI or significance test;
   - the sample size required to resolve the effect at 80% power (compute if possible; cite the formula you used);
   - the auditor's grade of the uncertainty-quantification dimension.

6. **Compute the overall shape.** How many claims grade strong / qualified / weak / unsupported? If more than 20% grade weak or unsupported, consider whether the aggregate pattern crosses into a methodology-level finding against the card.

7. **Produce the one-to-two-page calibration-methodology appendix** per chapter 4's structure:
   - set of claims challenged;
   - per-claim table (as above, condensed for readability);
   - aggregate pattern paragraph;
   - cross-reference to the applied procedures (Wilson, bootstrap, kappa, power-analysis formula);
   - finding candidates (if the aggregate crosses the threshold).

8. **Perform one auditor-run kappa cross-check** on a sampled set of 20 items from the vendor's safety eval. For this exercise, substitute: run your own independent grading on 20 of the HarmBench replication outputs from exercise-03 (or an analogous safety-eval output), compute Cohen's kappa with the published classifier's grades, and attach the result to the appendix. If no analogous output exists, substitute a kappa computed between two annotators on a public dataset of your choice, and document the substitution.

## Starter guidance

- Wilson interval: `statsmodels.stats.proportion.proportion_confint(k, n, alpha=0.05, method='wilson')`.
- Bootstrap CI: 10,000 resamples, fixed seed; `numpy.random.default_rng(42)`.
- Power / sample-size: for a difference of proportions use `statsmodels.stats.power.NormalIndPower().solve_power(...)` or the equivalent; for binomial, Fleiss / Lehr formulas.
- Kappa: `sklearn.metrics.cohen_kappa_score(a, b)` for two raters; `statsmodels.stats.inter_rater.fleiss_kappa(table)` for multi-rater.
- Report CI bounds to three decimals and judge the asymmetry; the Wilson bound at 97% on n=100 lands around 91.5–99.0, not 92–102.
- A single weak-graded claim is a soft finding; a pattern of ten weak-graded claims escalates the posture.
- If the card reports a CI narrower than Wilson would produce at the stated n, that is itself a finding — the vendor's CI is inconsistent with its stated sample size.
- Keep the kappa cross-check simple: 20 items, one adjudicator, Cohen's kappa, interpreted against Landis & Koch bands with the caveat that bands are advisory. <!-- needs-research: when relying on Landis & Koch in a live engagement, note that modern literature views the thresholds as advisory, not prescriptive; cite accordingly -->

## Acceptance criteria

The deliverable is accepted when:

- The calibration-challenge table has one row per claim in the exercise-01 register.
- Every reported rate without a CI has an auditor-computed Wilson CI.
- Every judge-mediated metric has a judge-reliability grade.
- Every fairness / sampling-sensitive metric has a sampling grade.
- Every improvement-over-baseline claim has an effect-size / power analysis column.
- An aggregate grade distribution is computed and reported.
- A kappa cross-check (on 20 items) is executed, reported with a point estimate and a 95% bootstrap CI, and interpreted.
- The one-to-two-page appendix reads cleanly and cites the specific applied procedures (Wilson, bootstrap seeds, power formulas, kappa interpretation).
- Where the aggregate pattern crosses into a pattern finding, the finding is drafted (not graded; grading is `mod-105` chapter 2).
- No step of the exercise authored a novel estimator or selection-adjustment procedure (chapter 4's borrowing discipline).

## Stretch goals

- For one representative claim, author the **multi-comparison-correction note** — if the card reports 50 pairwise improvements over a baseline, how many false positives would be expected under Bonferroni vs. Benjamini-Hochberg at α=0.05? Report both and name the one you would apply.
- Author a **"methodology-request letter"** to the vendor — a one-page request for CI reconstructions, judge-calibration logs, and sample-size documentation on the claims that graded weak or unsupported.
- Draft a **"vendor-interview question set"** grounded in the appendix — ten questions with evidence anchors — the audit team will use when sitting with the vendor's evaluation lead.
- Produce a **signed cross-check manifest** for the kappa run (the chapter-2 replication-manifest shape adapted), including the per-item disagreement register.
