# Calibration Methodology Challenge — Is the Published Metric Defensibly Supported?

## Motivation

A replication delta tells the auditor whether the number *comes back the same*. That is only half the question. The other half — whether the card's published number is *defensibly supported by evidence* — requires the auditor to challenge the methodology that produced it. A card claiming "95.4% accuracy, n=100" and a card claiming "95.4% accuracy, n=100,000" state the same number with incompatible evidentiary weight. A card claiming "98% refusal, judged by GPT-4o" and a card claiming "98% refusal, judged by three human annotators with 0.82 Fleiss kappa" state the same number with incompatible defensibility.

The calibration-challenge discipline tests four things on every metric: sample size, sampling procedure, evaluator reliability, and uncertainty quantification. This chapter installs the auditor's checklist and the applied statistical procedures; novel estimator design sits with `model-evaluation-engineer` (L30). The aim is to apply the methodology, not author it.

## The four challenge dimensions

For every row in the claim register from chapter 1, the auditor asks:

1. **Sample size.** Is the test set large enough to resolve a meaningful effect at the reported precision?
2. **Sampling procedure.** Is the test set representative of the deployment population, or is it a convenience sample?
3. **Evaluator reliability.** If the metric is graded (LLM-as-judge, human annotation, panel rating), is the evaluator in agreement with itself and with a ground-truth reference?
4. **Uncertainty quantification.** Is a CI, SE, or at least a sample size reported? Is the comparison against a baseline covered by a proper hypothesis test or at least an effect size?

A card that fails on any of the four is a card whose number is weaker than it looks.

## Challenge 1 — sample size and power

A metric computed on 50 samples can sit alongside a metric computed on 50,000 samples in the same card without disclosure, and both read as "X%". The auditor's test:

- **Record the sample size.** Pull from the card; chase to the companion document; record `unstated` if the card is silent (itself a completeness finding).
- **Compute the Wilson score interval** at the reported rate and sample size. For a reported 97% at n=100, the 95% Wilson interval runs from roughly 91.5% to 99.0% (compute exactly). The number is substantially less tight than the point claims.
- **Compute the minimum detectable effect** (MDE) for the comparison the card implies. A card that claims "no fairness disparity" at n=50 per subgroup can only detect large disparities; what the card is actually saying is "we did not detect a disparity we could have detected."
- **Apply a power analysis for the next-release comparison.** A card claim of "no regression from the previous release" at the sample size reported has a power the auditor computes and reports.

The applied methodology is standard (see any introductory statistics text; the `model-evaluation-engineer` track covers design); the auditor's role is to apply it, not to invent it. A finding here is "sample size insufficient to support the published precision," not "sample size wrong."

### Worked example — Wilson interval shape

For a reported binary-outcome rate `p̂` and sample size `n`, the two-sided 95% Wilson score interval is

```
      (p̂ + z²/2n) ± z·√( p̂(1-p̂)/n + z²/(4n²) )
CI =  ────────────────────────────────────────── ,   z = 1.96
                   1 + z²/n
```

implemented in `scipy.stats.binomtest(...).proportion_ci(method='wilson')` or `statsmodels.stats.proportion.proportion_confint(..., method='wilson')`. The auditor runs the computation inline in the workpaper and quotes the interval alongside every reported rate.

## Challenge 2 — sampling procedure and representativeness

The sample that produced the metric may not match the population the deployment will see. Three tests:

- **Population declaration.** Does the card state what the test-set population is (users, geographies, device types, languages, time windows)? Unstated → completeness finding.
- **Convenience vs. systematic sampling.** Benchmarks are intrinsically convenience samples against operational populations; the card should acknowledge this. A card claiming "representative of production" when the test is GLUE or MMLU is overclaiming.
- **Stratification across protected classes.** For fairness-adjacent claims (chapter 5) sample sizes must support per-subgroup computation. A total of n=500 where one subgroup is n=10 means the per-subgroup Wilson intervals are wide; the auditor reports both aggregate and per-subgroup intervals.

The auditor's ask is "what population is this a sample of, and how was the sample drawn?" If the card cannot answer, the number carries less evidentiary weight.

## Challenge 3 — evaluator reliability

Many modern eval metrics depend on a *judge* — either a human panel or an LLM-as-judge. The judge introduces its own noise. The auditor's test:

### Human-judge reliability

Where the card claims human annotation produced the labels:

- **Number of annotators per item.** Single-rater labels have no inter-annotator agreement estimate; multi-rater labels produce one.
- **Agreement statistic.** Cohen's kappa for two raters; Fleiss' kappa for multi-rater categorical; Krippendorff's alpha for mixed-type / missing-data settings; intraclass correlation coefficient (ICC) for continuous ratings. The card should report at least one.
- **Threshold reading.** Rules of thumb — kappa below 0.4 is weak, 0.4–0.6 moderate, 0.6–0.8 substantial, above 0.8 near-perfect. These are heuristic; the auditor cites the rule of thumb rather than inventing a new one. <!-- needs-research: cite the Landis & Koch (1977) kappa benchmark paper and note that modern practice views the thresholds as advisory, not prescriptive -->
- **Adjudication procedure.** When annotators disagree, who adjudicates? A single "senior annotator" collapses the agreement estimate; a documented adjudication protocol preserves it.

### LLM-as-judge reliability

Where the card uses an LLM to grade (e.g., "judged by GPT-4o"):

- **Judge version and configuration pin.** The judge is itself a model with a version; a card that cites "GPT-4o" without a date or snapshot is weakly specified.
- **Calibration to human ground truth.** The accepted practice is to validate the judge against a human-labeled calibration set and report the agreement (kappa, Spearman, or classification agreement). A card that uses an LLM judge without calibration is overclaiming.
- **Judge-model sensitivity.** The auditor's replication may run the vendor's eval under a different judge model and report the sensitivity; if swapping GPT-4o for Claude 3.5 Sonnet moves the score by 5 pp, the judge is a material source of uncertainty.
- **Prompt-sensitivity.** Minor wording changes in a judge prompt can swing results; the card should fix and publish the judge prompt or treat the metric as non-reproducible.

### The kappa cross-check

A common procedure — the auditor samples 100 items from the vendor's eval set, re-grades them with independent human annotators, and computes agreement with the vendor's grades. A kappa below 0.6 between auditor human grading and vendor judge is a material calibration finding even if the card's point estimate replicates perfectly.

## Challenge 4 — uncertainty quantification

A point estimate without an interval is incomplete evidence. The auditor's test:

- **Does the card report a CI, SE, or at least n?** The three are not equivalent but one of them is a minimum.
- **Is the CI constructed appropriately?** Wilson or Clopper-Pearson for binary rates; bootstrap for complex metrics (BLEU, pass@k, ROUGE, aggregate-of-aggregates); normal-approximation only for large n and well-behaved metrics.
- **Does the card distinguish statistical from judgment-induced uncertainty?** The statistical CI covers sampling error; evaluator agreement covers judge noise; both should be reported.
- **Does the card quote effect sizes for claimed improvements?** "Our model beats the baseline by 2 pp" is weak without a Cohen's h (for proportions), Cohen's d (for continuous), or Cliff's delta (for non-parametric); and without a sample-size disclosure the effect is not interpretable.

### Bootstrap CI — applied procedure

The auditor's bootstrap is the standard non-parametric bootstrap:

```python
import numpy as np
rng = np.random.default_rng(seed=42)
n_boot = 10000
boot_means = np.empty(n_boot)
for i in range(n_boot):
    resample = rng.choice(per_sample_scores, size=len(per_sample_scores), replace=True)
    boot_means[i] = resample.mean()
ci_lo, ci_hi = np.quantile(boot_means, [0.025, 0.975])
```

Fixed-seed, 10,000 resamples, 2.5 / 97.5 percentile interval. For paired comparisons (model-vs-baseline) use a paired bootstrap on per-sample differences. The authority on bootstrap variants is `model-evaluation-engineer`; the auditor uses the canonical form.

## Overstatement grading — when is the claim unsupportable?

Not every methodology gap is a finding. The auditor grades:

- **Strong support.** CI reported; sample size adequate to resolve the claimed precision; evaluator calibrated to human ground truth with agreement above threshold; stratified sample where required. → No finding; claim is defensibly supported.
- **Qualified support.** One of {CI, sample size, judge calibration, stratification} is missing or marginal; replication delta is within claim CI. → Soft finding (documentation observation): the card should strengthen methodology disclosure; opinion is unqualified.
- **Weak support.** Two or more are missing or marginal; or replication delta is outside claim CI; or judge reliability is below threshold. → Finding: the published number is not defensibly supported by the evidence as presented; opinion may be qualified.
- **Unsupported.** Metric is categorical (no sample size, no CI, no judge disclosure, no methodology); or the methodology is internally inconsistent (e.g., CI narrower than Wilson at the stated n allows). → Finding: the published number cannot be defended at the published precision; vendor is asked to restate the claim or supply the missing methodology.

The grading is auditor judgement, not a mechanical rule. The engagement's finding register records the grade and the reasoning; the independent reviewer under 17021-1 clause 9.5 (`mod-105` chapter 1) re-reads the grading on sample.

## Applied aggregate calibration — the methodology appendix

The auditor's final deliverable on calibration is a one-to-two-page *methodology-challenge appendix* to the replication report (chapter 7). Minimum contents:

- The set of claims challenged, by claim ID.
- Per-claim challenge table: sample size, population, judge identity and calibration, reported CI or SE, auditor-computed Wilson/bootstrap CI, agreement estimate where applicable, grade (strong / qualified / weak / unsupported).
- The aggregate pattern: if many claims grade weak, the finding escalates from a per-claim observation to a pattern finding on the card's methodology.
- Cross-reference to the applied statistical procedure (bootstrap, Wilson, kappa) so the independent reviewer can re-perform.

## Reading the vendor's statistics with professional skepticism

Watch for presentational tricks that the challenge discipline catches:

- **Selective reporting.** The card reports the metrics on which the model did well; silence on the metrics the eval harness computes but the card omits is itself evidence.
- **Changing the baseline.** A card that claims "improvement over the previous release" using a different test set across releases is comparing apples to oranges.
- **Collapsing subgroup results into an average.** Aggregate averages wash out per-subgroup degradation. The auditor insists on stratified reporting.
- **Novel composite metrics.** A card that proposes a new "safety score" built from several sub-metrics should disclose the weighting and justify it; absence is a card-completeness finding.
- **Cherry-picked sample size.** A card reporting n=500 on the metric that's good and silently dropping to n=20 on the metric that's shaky. The auditor cross-checks.
- **Judge-selection bias.** Choosing a judge known to be lenient to the vendor's style. The agreement cross-check surfaces this.

## Common failure modes

- **Assuming a point estimate carries more than it does.** 96.0% and 96.5% are indistinguishable at n=200.
- **Reporting a bootstrap CI without specifying the number of resamples or seed.** Non-reproducible CI.
- **Forgetting multiple-comparison corrections.** Across a 50-metric card, several "significant improvements" are false positives at α=0.05 without correction. Apply Bonferroni or Benjamini-Hochberg where appropriate; refer depth to `model-evaluation-engineer`.
- **Treating LLM-judge-of-LLM as free.** The judge is a model; its errors compound with the subject's errors.
- **Not calibrating the auditor's own replication to the vendor's judge.** If the auditor uses a different judge, the delta is confounded with judge drift.
- **Letting the calibration challenge become model-eval-engineer-depth work.** The auditor applies canonical procedures. If a novel estimator is needed (e.g., selective-inference correction on an adaptively-chosen eval set), escalate rather than author.

## Summary

- The calibration challenge tests four dimensions on every published metric: sample size, sampling procedure, evaluator reliability, uncertainty quantification.
- Applied procedures the auditor uses: Wilson score intervals, bootstrap CIs, Cohen's / Fleiss / Krippendorff kappa for agreement, Cohen's d / h / Cliff's delta for effect size, power analysis for comparison claims.
- LLM-as-judge grades require a calibration set and an agreement statistic; absence of calibration is a card-completeness finding; a kappa cross-check by the auditor is a one-off procedure that often surfaces material issues.
- Claims grade strong / qualified / weak / unsupported for calibration; the aggregate pattern across claims can escalate to a pattern finding on the card's methodology discipline.
- Novel statistical procedure authoring sits with `model-evaluation-engineer`; the auditor applies canonical procedures and escalates where novelty is required.
