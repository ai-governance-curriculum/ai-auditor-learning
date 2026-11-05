# Auditing Fairness Claims — Metric Appropriateness, Coverage, and the IAAIS Report Shape

## Motivation

Fairness claims are the highest-stakes fraction of a card's claim register because a regulator or litigant will read them most carefully, and because the vendor can be technically honest about a fairness number while still under-serving the obligation. The auditor's job on fairness has four parts: (1) test whether the *metric* the vendor picked is the right metric for the obligation, (2) test whether the *protected classes* covered are the classes the obligation requires, (3) test whether *intersectionality* is reported where the obligation or the impact assessment calls for it, and (4) test whether the *numbers* are reproducible and defensibly supported. Only (4) is pure replication; (1)–(3) are *conformance-to-obligation* tests, and the obligation varies by jurisdiction and use case.

This chapter installs the obligation-mapping discipline, the per-obligation metric-appropriateness test, and the two auditor-report shapes — the Algorithmic Impact Assessment (AIA) summary and the Independent Audit of AI Systems (IAAIS, ForHumanity) / BABL AI bias audit report — the engagement produces as deliverables.

## The obligation surface

Before testing any number, the auditor maps the system's deployment to the obligations that attach. A non-exhaustive map the AI-auditor should navigate:

### NYC Local Law 144 (2021, enforcement from 2023)

- **Scope.** Automated Employment Decision Tools (AEDT) used in hiring or promotion decisions in NYC. <!-- needs-research: confirm the current DCWP rule text and any 2024–2026 amendments; the final rule imposes specific audit periodicity, publication, and notice obligations -->
- **Metric shape.** Independent bias audit computing *selection rate*, *scoring rate*, and *impact ratio* (selection-rate-ratio and scoring-rate-ratio) across EEO-1 race and sex categories, and intersectional categories where sample size permits.
- **Reference class.** The highest-selection-rate group is the reference class for the impact ratio computation.
- **Threshold.** The rule follows the EEOC four-fifths rule by default (0.8); NYC LL144 does not itself set a pass/fail threshold but requires the number to be published.
- **Publication.** Audit results must be published on the employer's website for a minimum period; notice to candidates is required.
- **Auditor independence.** The bias audit must be performed by an independent auditor; conflicts bar the auditor from conducting it. (`mod-101`.)

### EEOC — Uniform Guidelines on Employee Selection Procedures (1978) and the four-fifths rule

- **Scope.** Employment selection procedures under Title VII, ADEA, ADA (as administered by EEOC).
- **Metric shape.** Selection-rate ratio (adverse-impact ratio) across protected classes as defined by the applicable civil-rights act.
- **Threshold.** The "four-fifths" (80%) rule of thumb: a selection-rate ratio below 0.80 is evidence of adverse impact. The threshold is a *rule of thumb*, not a safe harbour; statistical significance and practical significance both inform litigation posture.
- **Not a card metric per se.** EEOC's shape is older than card-style documentation; a card that cites "four-fifths compliant" is making a specific legal-adjacent claim the auditor tests.

### EU AI Act — Articles 10 and 15

- **Article 10 (data and data governance).** For high-risk systems, training/validation/testing datasets must meet quality criteria including representativeness, freedom from errors, completeness, and consideration of "specific geographical, behavioural or functional setting" of use. Bias examination is explicitly required where the dataset may reinforce bias prohibited under Union law. <!-- needs-research: confirm the final-text Article numbering and subsection references against the as-enacted EU AI Act 2024/1689 at reading time -->
- **Article 15 (accuracy, robustness, cybersecurity).** Declared performance in the technical documentation; levels of accuracy and relevant metrics; resilience to errors, faults, and inconsistencies; cybersecurity.
- **Article 27 (Fundamental Rights Impact Assessment).** Required for public bodies and certain private operators deploying high-risk systems; the FRIA is distinct from, and often broader than, the conformity-assessment technical documentation.
- **Auditor read.** A card claiming high-risk conformity should reference the Article-10 data-governance process and the Article-15 performance disclosures; the auditor tests that the fairness-metric choice fits the Article-10 bias-examination obligation and that the Article-15 performance disclosure covers the system's actual deployment envelope.

### Colorado AI Act (SB 24-205) and other US state obligations

- **Scope.** Consequential-decision high-risk AI systems (housing, employment, education, essential government services, financial services, healthcare, legal services, insurance).
- **Obligations.** Risk-management programme, impact assessments, consumer notices, developer-to-deployer disclosures. <!-- needs-research: confirm Colorado AI Act's effective date and any 2025–2026 regulatory implementation at reading time; multiple US states had similar bills in flight through 2024–2026 -->
- **Auditor read.** Fairness-metric shape is not prescribed; the auditor tests the impact-assessment's own declared metrics.

### Sector overlays

- **Financial services (SR 11-7, OCC 2011-12).** Model-risk management guidance that applies to credit-decision, pricing, AML models. Fairness obligations layer on top (ECOA, FHA, HMDA).
- **Healthcare (FDA GMLP, FDA SaMD, OCR 2024 Section 1557 rule).** HHS OCR's 2024 final rule on Section 1557 includes nondiscrimination obligations for clinical-decision-support tools. <!-- needs-research: confirm Section 1557 final-rule effective dates and any 2025 judicial-stay posture at reading time -->
- **Education (Title VI, IDEA).** Fairness claims on education AI must consider the applicable civil-rights overlay.
- **Insurance (NAIC AI Model Bulletin 2023, state DOI bulletins).** Varies by state.

The auditor does not need to practice law; the auditor needs to read the engagement's legal-counsel letter (`mod-103` and `mod-102`) that enumerates the applicable obligations, and test whether the vendor's fairness-metric choice fits them.

## The metric-appropriateness test

Many fairness metrics exist. A non-exhaustive set the auditor should recognise and the typical appropriateness read:

| Metric | What it measures | Typical appropriate use | Typical inappropriate use |
|--------|------------------|-------------------------|----------------------------|
| Demographic parity (DP) / statistical parity | Equal selection / positive-prediction rates across groups | Ad serving; resource allocation when outcomes should be equalised regardless of base rates | Risk scoring where base rates legitimately differ |
| Disparate impact / selection-rate ratio | Ratio of selection rates | EEOC four-fifths test; NYC LL144; employment decisions | Clinical-utility judgements |
| Equal opportunity (EO) | Equal true-positive rates across groups | Hiring from a qualified pool; loan approvals among the credit-worthy | Where false-positives cost the subject |
| Equalized odds | Equal TPR *and* FPR across groups | Criminal-justice risk scoring (debated); high-stakes screening | Where ground-truth labels are themselves biased |
| Predictive parity / calibration | Equal positive-predictive value across groups | Risk scoring where calibrated scores drive thresholded decisions | Where base rates differ and the obligation targets outcomes, not scores |
| Counterfactual fairness | Decision invariant under a counterfactual change of protected attribute | Where causal reasoning is required | Difficult to operationalise; rarely a card-level claim |

The *impossibility* result — no model can simultaneously satisfy demographic parity, equalized odds, and calibration when base rates differ (Chouldechova 2017, Kleinberg et al. 2016) — means the vendor's choice of metric is itself a choice about what fairness means. The auditor does not re-litigate the choice but tests whether the choice fits the obligation.

### The metric-appropriateness grading

For each fairness claim in the register, the auditor records:

- The metric the vendor reported.
- The obligation attached to the system's deployment.
- The metric the obligation calls for (or the family of metrics, if the obligation is open).
- **Match.** Appropriate — metric fits obligation. No finding.
- **Mismatch (soft).** Metric is in the right family but a close variant would fit the obligation better (e.g., reported DP where EO is more appropriate for a loan-approval system against ECOA). Finding candidate; discuss with vendor.
- **Mismatch (hard).** Metric does not address the obligation (e.g., reported calibration-by-group where NYC LL144 requires selection-rate ratio). Finding.
- **Absent.** No fairness metric reported where obligation applies. Finding.

## Protected-class coverage

Even with the right metric, the obligation prescribes *which* classes. The auditor tests:

- **Statutory classes covered.** For NYC LL144 the EEO-1 race and sex categories are required. For EEOC the Title VII / ADA / ADEA classes. For EU AI Act Article 10 the relevant protected characteristics under Union law (and national-law extensions).
- **Class-definition consistency.** A card that reports "men / women" when the obligation requires finer categories (e.g., non-binary disclosure where legally permitted) is under-covering.
- **Reference-class choice.** NYC LL144 uses the highest-selection-rate group as the reference; a card that uses a different reference class may understate the impact ratio.
- **Intersectional reporting where sample size supports it.** The impact-ratio computation at intersections (e.g., Black women vs. the reference intersection) surfaces disparities the one-dimensional cuts hide. Intersectional omission with adequate sample size is a finding; omission with inadequate sample size is a documentation observation.

The depth of why intersectional fairness differs from single-axis fairness lives with `ai-risk-engineer` and the ACM FAccT literature; the auditor cites the obligation and tests the coverage.

## Replicating the numbers

For each claim that grades A or B on auditability (chapter 1):

1. **Obtain the test population.** Vendor-shared dataset under NDA; or deployed-system telemetry (if in scope and authorised); or a public dataset the card cites.
2. **Define the groups per the obligation.** EEO-1 categories, or Union-law classes, or the applicable sector definition.
3. **Compute selection rate per group.** Count admit / approve / positive-prediction decisions per group; divide by group size.
4. **Compute the selection-rate ratio.** Each group's rate divided by the reference group's rate.
5. **Bootstrap the CI** using chapter 4's procedure; small groups produce wide CIs the auditor reports rather than hides.
6. **Compute additional metrics called for by the obligation.** EO (TPR), scoring-rate ratio, calibration-by-group — as the obligation requires.
7. **Produce the delta.** Observed vs. card-claimed, using the chapter 3 signed-delta shape.

Fairlearn (`fairlearn.metrics.MetricFrame`, `selection_rate`, `demographic_parity_ratio`, `equalized_odds_difference`), AIF360, and Holistic AI each implement the core computations. The auditor runs at least two of them on the same test set as a cross-check for independence of implementation.

### Worked example — selection-rate ratio in Fairlearn

```python
from fairlearn.metrics import MetricFrame, selection_rate, true_positive_rate

mf = MetricFrame(
    metrics={"selection_rate": selection_rate, "tpr": true_positive_rate},
    y_true=y_true,
    y_pred=y_pred,
    sensitive_features=groups,     # pd.Series over the EEO-1 categories
)
print(mf.by_group)                 # per-group metrics
print(mf.ratio(method="between_groups"))  # min/max ratio
```

Interpreting: a `selection_rate` ratio of 0.73 between the lowest-rate and highest-rate group fails the four-fifths rule; the auditor reports the per-group rates, the pair that produced the ratio, and the bootstrap CI.

## The explainability cross-check

A fairness claim on a model that does not expose feature attribution is weaker than one accompanied by per-feature or per-group attribution. The auditor:

- **Reads the card's explainability claim.** SHAP / LIME / Alibi / integrated-gradients / Anchors.
- **Replicates a sampled set of explanations.** Not re-implement; use the stated library and compare.
- **Cross-reads the attributions.** If a protected-class proxy (ZIP, surname, device locale) dominates attribution for the under-selected group, the fairness number is corroborated by the attribution evidence.
- **Does not extrapolate.** Attribution is not causal explanation; findings cite "attribution-level evidence consistent with X" rather than "model relies on X."

Depth lives in `ai-risk-engineer` and `model-evaluation-engineer`; the auditor applies the tools and reports.

## The Algorithmic Impact Assessment (AIA) summary

For deployments where the obligation includes an AIA (Treasury Board of Canada Directive on Automated Decision-Making, EU AI Act Article 27 FRIA, several US state-level consequential-decision rules), the auditor produces an AIA summary as a deliverable. Minimum sections:

1. **System identification.** Developer, system, version, deployment context, decision scope.
2. **Decision significance.** Who is affected, which decisions, what the alternative is (human, algorithmic-only, hybrid), the appeal path.
3. **Fairness obligation analysis.** The applicable civil-rights, data-protection, and sector obligations; the mapping from each to a testable fairness claim.
4. **Fairness-metric selection and justification.** The metric chosen by the vendor; the auditor's appropriateness grade.
5. **Protected-class coverage.** The classes tested; the ones omitted and why.
6. **Intersectionality.** Reported combinations; combinations with inadequate sample size noted.
7. **Observed fairness result.** Point estimate, CI, reference class, per-group breakdown.
8. **Replication delta.** Observed vs. card-claimed with signed-delta row.
9. **Scope restrictions and limitations.** Dataset access, time window, deployed-population match.
10. **Finding register references.** Links to the engagement's findings.

The AIA summary is signed by the auditor and attached to the independent-replication report (chapter 7).

## The BABL AI bias-audit report and the ForHumanity IAAIS shape

Two industry-adopted report shapes the auditor should recognise, both published and marketed by their respective organisations:

### BABL AI bias audit

- Reported in the NYC LL144 shape; selection-rate ratios across EEO-1 categories and intersections; aggregate narrative; publication-ready PDF.
- Target audience is the deployer's compliance and legal teams and the public (LL144 requires publication of the audit).
- Specific template fields include the AEDT definition, the audit period, the data provenance, the computations, the limitation on auditor independence.
- <!-- needs-research: cite the current BABL AI bias-audit template and any published methodology notes at reading time; BABL AI has published multiple iterations -->

### ForHumanity Independent Audit of AI Systems (IAAIS)

- A broader certification shape with criteria across risk, bias, privacy, trust, cybersecurity, ethics; ForHumanity publishes criteria sets and trains certified auditors.
- The IAAIS report is longer than an LL144 bias audit — it is a multi-domain audit with a specific opinion shape.
- <!-- needs-research: at reading time inventory the current IAAIS criteria set and any revisions since 2024; ForHumanity criteria are published and evolve -->

For a NYC LL144 engagement, the deliverable is the BABL-shaped bias audit. For a multi-domain IAAIS engagement, the deliverable is the IAAIS report, of which the bias section is one chapter. The auditor identifies the appropriate shape in the engagement letter (`mod-103`) and the fairness chapter above feeds whichever shape applies.

## Common failure modes

- **Testing the metric the vendor reported instead of the metric the obligation requires.** Replication passes; obligation fails. The auditor is paid to catch exactly this.
- **Reporting an aggregate pass on the four-fifths rule without the per-pair breakdown.** The pair that fails is the finding; the aggregate hides it.
- **Over-reading intersectional results on small subgroups.** A selection-rate ratio of 0.3 with a sample of 8 is a sample-size finding, not a fairness finding.
- **Using the vendor's test set to grade the vendor's fairness claim.** Where possible the auditor uses an independent test population (deployed-system telemetry, a held-out dataset, or a public benchmark the deployment maps to); if the vendor's test set is the only option, document.
- **Confusing group-fairness with individual-fairness.** The obligations the AI-auditor meets are predominantly group-fairness; individual-fairness research (Lipschitz similarity, counterfactual fairness) is rarely a card claim.
- **Recommending a mitigation.** The auditor does not design the mitigation; the second line engages `ai-risk-engineer` for mitigation design. The auditor reports the finding and management proposes the response (`mod-111`).
- **Letting the BABL / IAAIS template override the obligation analysis.** The template is a shape, not an assessment; the obligation analysis drives the content.

## Summary

- Fairness audit has four parts: metric-appropriateness to the obligation, protected-class coverage, intersectionality reporting, and reproducibility of the numbers.
- Obligation map: NYC LL144 (AEDT, impact ratios across EEO-1, four-fifths), EEOC adverse-impact, EU AI Act Articles 10 / 15 / 27, Colorado AI Act, sector overlays (FDA, SR 11-7, Section 1557, NAIC bulletins).
- Metric-appropriateness grading is strong / soft mismatch / hard mismatch / absent; the fairness-impossibility result means metric choice is itself auditable.
- Replicate using Fairlearn + AIF360 + Holistic AI (at least two for independence of implementation); bootstrap CIs; per-group and intersectional breakdowns.
- Deliverables are the AIA summary (where the obligation includes an impact assessment) and either the BABL AI bias-audit shape (NYC LL144 engagements) or the ForHumanity IAAIS shape (multi-domain engagements).
