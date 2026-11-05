# exercise-05: Fairness and Explainability Program Audit

**Estimated effort:** 2 hours

## Objective

Audit an organisation's **fairness and explainability programme** against chapter 5's five programme-level tests: **obligation mapping**, **metric-selection defensibility**, **mitigation-loop operation**, **subgroup / intersectional coverage**, **publication cadence** (including NYC LL144, Colorado AI Act, and the EU AI Act Articles 10 / 15 / 27 obligations), and the **explainability obligation surface** (including GDPR Article 22). Produce the engagement workpaper with one reperformance pass on a sampled deployment.

The exercise differs from mod-106 exercise-04: that was a single-claim audit. This is a *programme* audit — the authoring, operation, and publication cadence that produces those claims.

## Prerequisites

- Chapter [`05-auditing-the-fairness-and-explainability-program.md`](../05-auditing-the-fairness-and-explainability-program.md).
- mod-106 chapter 5 on single-claim fairness audit; that chapter's metric-appropriateness grading carries into step 2.
- Working familiarity with Fairlearn and at least one of AIF360 / Holistic AI.
- `mod-102` on criteria translation (for the obligation map).

## Scenario

**Delphi Talent** is a US-based HR SaaS platform with a resume-screening feature and a candidate-scoring feature, both ML-driven. Delphi deploys to employers in NYC (subject to Local Law 144), California, Colorado (subject to the Colorado AI Act consequential-decision provisions), and the EU (subject to EU AI Act Article 6(2) Annex III(4) high-risk categorisation for employment AI). Delphi publishes an annual Bias Audit Report, a Responsible AI Statement, and a candidate-facing FAQ. The most recent bias audit is six months old.

You are the lead auditor on an independent bias audit per NYC LL144, scoped to Delphi's resume-screening feature, with an extended scope at the audit committee's request to cover the broader programme.

Substitute the scenario if needed: any organisation with a published bias audit or responsible-AI disclosure (consumer-facing lending platforms, employment ATS, insurance underwriting, housing-match, education placement). Attribute the subject.

## Requirements

1. **Pin the published artefacts.** Bias Audit Report, model / system cards, candidate-facing disclosures, responsible-AI statement — each with URL, retrieval timestamp, hash, version.

2. **Produce the obligation map.** For each deployment (jurisdiction × use case), record: obligation, metric family required, protected classes required, reporting cadence, publication requirement. Reference the primary source per row (LL144 rule section; EEOC Uniform Guidelines; Colorado AI Act section; EU AI Act article). Deployments without an obligation row are documentation findings.

3. **Metric-selection defensibility audit.** For at least two deployments:
   - Record the metric the programme selected.
   - Record the obligation the metric must satisfy.
   - Grade the match per mod-106 chapter 5's rubric (appropriate / soft mismatch / hard mismatch / absent).
   - Record whether the selection has a documented rationale citing the impossibility result and the alternatives considered.
   - Open a finding per mismatch or absent-rationale case.

4. **Mitigation-loop audit.** Pull the programme's recent mitigation closures (at least three). For each, trace the eight-step loop from chapter 5: observation → RCA → intervention → re-measurement → trade-off analysis → residual-risk update (chapter 2) → documentation → monitor. Broken loops are findings; `mitigation closed without residual update` is the most common finding.

5. **Subgroup / intersectional coverage audit.** For the resume-screening deployment:
   - Pull the per-subgroup metrics from the current Bias Audit Report.
   - Confirm the EEO-1 race and sex categories are covered per LL144.
   - Confirm intersectional cells are reported where the declared minimum sample size is met.
   - For one deployment, reperform the subgroup metrics with Fairlearn's `MetricFrame` on the organisation's provided test data (or a representative public dataset you declare). Compare to published numbers; record delta.

6. **Publication-cadence audit.** For each jurisdiction:
   - LL144 publication: confirm location (employer website), confirm audit date within staleness window, confirm independent-auditor identification, confirm candidate notice present.
   - Colorado AI Act consumer notice: confirm content per the Act.
   - EU Article 10 bias-examination evidence and Article 15 performance disclosure: confirm presence in technical documentation.
   - Internal model-card refresh cadence: confirm per methodology.

7. **Explainability-programme audit.** For at least one deployment:
   - Record the obligation (GDPR Article 22; ECOA adverse-action; Article 86; LL144 / Colorado consumer notice).
   - Record the explainability method (SHAP / LIME / Alibi / Anchors / rule-based / counterfactual).
   - Reperform attribution on five sample decisions with the stated tool.
   - Record whether the consumer-facing explanation is decision-specific vs. model-generic.
   - Faithfulness test: do the attributed features match the model's actual decision basis?

8. **Record findings** per chapter 2's finding shape, cross-referenced to the register where applicable.

## Starter guidance

- The obligation-map row for LL144 includes an explicit "highest-selection-rate group is reference class" test — the single most common NYC audit error is picking the wrong reference class.
- Colorado AI Act applicability depends on the "consequential decision" definition; a resume-screening tool used in Colorado is in scope.
- When reperforming metrics with Fairlearn, use `MetricFrame` with `metrics={"selection_rate": selection_rate, "tpr": true_positive_rate}` as chapter 5 (mod-106) shows; bootstrap CIs with the organisation's methodology (mod-106 chapter 4).
- For explainability faithfulness, a quick check is whether SHAP (or the equivalent) assigns substantial attribution to a feature the model's gradient (or a surrogate linear model) does not corroborate. Faithfulness-checks are a `model-evaluation-engineer` depth — the auditor applies, not authors.
- A programme that has an "annual" bias audit but whose last audit is 11 months old is *on time*; the same audit at 13 months is a cadence breach.
- Publication-reachability test: open the employer's actual careers page and attempt to locate the bias-audit disclosure as a job applicant would. A URL that only appears in a search-indexed PDF is not publication for LL144 purposes.

## Acceptance criteria

The deliverable is accepted when:

- All published artefacts are pinned.
- The obligation map covers every deployment in scope, with primary-source citations.
- At least two deployments have had their metric-selection graded.
- At least three mitigation closures have been traced through the eight-step loop.
- Subgroup coverage is confirmed per LL144's EEO-1 shape; intersectional coverage is explicit.
- Fairlearn reperformance has been produced for at least one deployment with per-group rates, reference class, and delta vs. the published number.
- Publication-cadence audit covers each applicable jurisdiction.
- Explainability-programme audit covers at least one deployment with a faithfulness reperformance.
- Findings are cross-referenced to the register where applicable.
- Primary-source citations are present; `<!-- needs-research: ... -->` used for uncertain claims.

## Stretch goals

- Build a small **Fairlearn test harness** (≤80 lines) that produces LL144-shape reports (selection rate per group, impact ratio with the highest-selection-rate group as reference, intersectional breakdown with minimum-sample threshold) for an arbitrary labelled test set.
- Draft the **candidate-notice copy** that matches LL144's content requirement — a one-paragraph plain-language disclosure that the organisation would publish on its application flow.
- Produce a **cross-jurisdiction single-page summary** that the organisation's legal counsel can rely on when deciding whether a given deployment needs a new bias audit vs. relies on the existing one.
- Draft the **mitigation-closure checklist** the organisation should gate every fairness-mitigation close on — the eight steps from chapter 5 in a one-page actionable form.
