# Auditing the Fairness and Explainability Program

## Motivation

Mod-106 chapter 5 taught the auditor how to audit a *claim* about fairness in a model or system card. This chapter widens the frame: how to audit the *programme* that produces those claims — the metric-selection process, the mitigation loop, the subgroup / intersectionality discipline, the publication cadence of model cards and bias-audit reports, and jurisdiction-specific compliance evidence (NYC Local Law 144, Colorado AI Act, and the sector overlays mod-106 chapter 5 enumerated).

The programme audit is wider than a single-claim audit because fairness obligations have a *lifecycle*: a bias audit in May does not satisfy the obligation in November if the model has been retrained, if a new jurisdiction has been added, or if the obligation's publication window has rolled over. The auditor tests the programme as an operating artefact, not just the latest report.

As with the other chapters, metric authoring sits with `ai-risk-engineer` (L25); the statistical methodology authoring sits with `model-evaluation-engineer` (L30). The auditor runs Fairlearn / AIF360 / Holistic AI as reperformance tools and reads the programme against its declared obligations.

## The obligation-mapping test

The chapter-5 of mod-106 obligation surface — NYC Local Law 144, EEOC adverse-impact under the Uniform Guidelines, EU AI Act Articles 10 / 15 / 27, Colorado AI Act, HHS Section 1557 (2024 final rule), FDA GMLP, NAIC AI Model Bulletin, SR 11-7 — maps onto the programme audit as a first-step mapping artefact.

The auditor expects the programme to publish an **obligation map**:

| Deployment / use case | Jurisdiction | Obligation | Metric family required | Protected classes required | Reporting cadence | Publication requirement |
|------------------------|--------------|-------------|------------------------|-----------------------------|-------------------|--------------------------|
| Resume-screening tool  | NYC          | Local Law 144 | Impact ratio across EEO-1 race & sex; intersectional where sample permits | EEO-1 race + sex | Annual + prior to deployment | Public on employer website; candidate notice |
| Credit decisioning     | US           | ECOA + Reg B + SR 11-7 | Adverse-impact ratio; fair-lending model risk assessment | Race, sex, age, marital status, national origin, ECOA classes | Methodology-dependent | Internal; regulator on request |
| Consequential decisioning | Colorado | Colorado AI Act (SB 24-205) | Risk-management programme; impact assessment | As enumerated by the Act | Methodology-dependent | Internal; consumer notice | <!-- needs-research: confirm Colorado AI Act final text, effective date (currently February 2026 per original text, subject to amendment), and subsequent rulemakings at reading time -->
| High-risk AI system    | EU           | EU AI Act Articles 10/15/27 | Bias-examination evidence; robustness/accuracy; FRIA | Union-law protected characteristics plus national-law extensions | Pre-market + ongoing | Technical documentation; Article 27 FRIA |
| Clinical decision support | US         | HHS OCR Section 1557 (2024 final rule) | Nondiscrimination evidence; variables-not-informed-by-race obligations | HHS-enumerated classes | Per CDS deployment | Per the rule | <!-- needs-research: confirm Section 1557 rule's current effective date and any 2025–2026 judicial-stay posture at reading time -->

The programme audit tests:

1. The map is present and current.
2. Each deployment in scope has a map row.
3. The declared metric family is in the organisation's testing pipeline.
4. The declared protected-class coverage is implemented.
5. The declared publication requirement has produced an artefact within the window.

A programme whose obligation map does not include a deployment the auditor can see in production is a scope-declaration finding against the AI inventory (`mod-105` AIMS obligations) before any fairness number is tested.

## The metric-selection defensibility test

Mod-106 chapter 5 taught the per-claim metric-appropriateness grading. The programme audit asks a different question: does the organisation's metric-selection *process* produce defensible choices?

The auditor samples several deployments and tests:

- **Documented selection.** For each deployment, the metric selected is documented with a written rationale citing the obligation, the use-case characteristics (base rates, decision cost asymmetry, whether labels are themselves biased), and the impossibility-result (Chouldechova 2017; Kleinberg et al. 2016) trade-offs.
- **Selection reviewed.** The selection is reviewed by a defined second-line function (fairness council, responsible-AI committee) rather than solely by the model-owning team.
- **Selection is revisited.** On material change — new jurisdiction, new regulator guidance, new protected-class coverage — the selection is re-reviewed.
- **Selection is defensible against the Pareto alternative.** Where the organisation chose demographic parity, the auditor asks whether equalised odds or predictive parity was considered and rejected with a written rationale; silent selection is a process finding.

### The mismatch pattern

The most common finding: the organisation has selected a metric that was appropriate for a prior use case but is not appropriate for the current deployment. A credit-approval model that was tuned to equal-opportunity now extended into insurance pricing without re-selecting the metric is a process finding, not merely a claim-level finding.

## The mitigation-loop evidence test

Fairness programmes do not merely measure disparity; they act on it. The auditor expects a mitigation-loop record:

1. **Observation.** A metric breaches the organisation's internal threshold or the external obligation threshold (e.g., the four-fifths rule).
2. **Root-cause analysis.** The programme performs an RCA (feature-level attribution analysis via SHAP / Alibi; label-source review; data-generating-process review).
3. **Intervention.** One or more of: pre-processing debiasing (reweighing, SMOTE for minority classes), in-processing (adversarial debiasing, prejudice remover, constraint-based training in Fairlearn), post-processing (threshold-by-group under equalised odds, reject-option classification, calibrated equalised odds).
4. **Re-measurement.** The metric is re-measured post-mitigation on the same test population.
5. **Trade-off analysis.** Accuracy / utility-vs-fairness trade-off is measured and recorded; the mitigation does not degrade utility beyond an approved threshold.
6. **Residual-risk update.** Per chapter 2, the register's residual-fairness-risk score is updated.
7. **Documentation.** Model card / bias-audit report updated with the new metric and the mitigation declaration.
8. **Monitoring.** Post-deployment monitor watches for mitigation drift; `mod-108`.

The auditor samples mitigation closures and tests the full loop. A mitigation closed without a residual-risk update or without updated publication is the same finding pattern as chapter 4's adversarial-ML residual update.

## The subgroup and intersectionality coverage test

Mod-106 chapter 5 introduced the intersectionality principle. The programme audit tests coverage *across deployments*, not merely within a single report.

- **Minimum classes per obligation.** EEO-1 race + sex for US employment; ECOA classes for US credit; Union-law protected characteristics plus national-law for EU AI Act. The auditor records the declared minimum and tests coverage.
- **Intersectional reporting where sample permits.** The programme declares a minimum sample size per intersectional cell (common thresholds: 30, 50, 100). Where the threshold is met, intersectional metrics are reported; where it is not, the gap is documented. Silent omission is a finding.
- **Intersectional pattern discovery.** The programme has a process to flag intersections that fail the metric even when the main-effect groups pass (Buolamwini & Gebru 2018 Gender Shades demonstrated the risk). The auditor samples and tests.
- **Non-binary / self-identified gender.** Where legal and ethical considerations support self-identified gender disclosure, the programme covers the self-identified categories alongside the EEO-1 required categories. (Legal counsel's letter — `mod-103` — governs the specifics.)

### Reperformance

For a sampled deployment the auditor reruns the subgroup and intersectional metrics with Fairlearn's `MetricFrame` (as in mod-106 chapter 5) and compares to the published numbers. A delta beyond the organisation's declared tolerance is a finding; a delta the auditor cannot explain is a stronger finding.

## The publication cadence test

Many obligations require public or audience-specific publication on a declared cadence:

- **NYC Local Law 144.** Independent bias audit published on employer's website; candidate notice; audit "no more than one year old" per the DCWP rule. <!-- needs-research: cite the current DCWP rule section on audit periodicity and publication duration -->
- **EU AI Act Article 27.** FRIA documentation for public bodies and certain private operators deploying high-risk systems.
- **Colorado AI Act.** Consumer notice and developer-to-deployer disclosure per the Act's deployer / developer obligations.
- **Internal model-card refresh.** The organisation's own AIMS methodology (ISO 42001 Clause 7.5) declares a cadence for internal model-card refresh.

The auditor tests:

1. The publication exists on the required channel.
2. The publication is within the declared period (not expired).
3. The publication content covers the required fields per the obligation (e.g., selection rate, scoring rate, impact ratio across EEO-1 categories for LL144).
4. The publication is authored or signed by an independent auditor where the obligation requires.
5. A version history is retrievable so prior-period claims can be traced.

### The NYC LL144 publication test (worked)

For an AEDT in NYC the auditor pulls the employer's website, locates the bias-audit disclosure, and confirms:

- The audit date is within the declared staleness window.
- The auditor is identified and declared independent per the DCWP rule.
- The computations include selection rate, scoring rate, and the impact ratio across EEO-1 race and sex categories, plus intersectional categories where sample permits.
- The reference class (highest-selection-rate group) is identified.
- The audit report is accessible (not paywalled, not behind a login).
- Candidate notice is present on the application flow.

Failures of any of these are DCWP-rule findings and feed the finding register.

## The Colorado AI Act compliance test

The Colorado AI Act (SB 24-205) imposes risk-management and impact-assessment obligations on developers and deployers of consequential-decision high-risk AI. <!-- needs-research: confirm final-text obligations and any 2025–2026 rulemaking at reading time; the Act's effective date has been subject to legislative amendment discussions --> The auditor tests:

- **Developer vs. deployer identification.** The organisation's role is clearly identified.
- **Risk-management programme.** Documented, with an owner, with evidence of operation (ties back to chapter 2's register audit).
- **Impact assessments.** Per the Act's definition; cover the required factors (purpose, benefits, risks, data, deployment context, user notice).
- **Consumer notice.** Where the organisation is the deployer, the consumer notice complies with the Act's content requirements.
- **Developer-to-deployer disclosure.** Where the organisation is the developer, the disclosures required of the developer have been produced for each deployer.
- **Nondiscrimination evidence.** The Act's algorithmic-discrimination prohibition is backed by metric evidence.

The Colorado AI Act's shape is sufficiently close to the EU AI Act that programmes designed for EU-market deployments often satisfy Colorado with minor additions; a programme with no Colorado-specific documentation despite Colorado deployment is a jurisdiction-coverage finding.

## The explainability-programme test

Explainability is adjacent to fairness because many fairness obligations and fairness controls depend on per-feature attribution. The auditor's explainability tests:

- **Explainability obligation mapping.** Which obligations require explanations (GDPR Article 22 right to meaningful information about automated decisions; ECOA adverse-action notice; EU AI Act Article 86 right to explanation for high-risk; LL144 and Colorado consumer-notice content).
- **Method declaration.** For each deployment the programme declares the explainability method (SHAP / LIME / Alibi / Anchors / counterfactual / rule extraction).
- **Operation.** The method is implemented in the deployment, not merely referenced in a report.
- **Consumer-facing explanation.** Where the obligation requires an explanation to the subject, the explanation is intelligible, specific, and aligned with the model's actual decision basis.
- **Faithfulness.** The explanation is faithful to the model — not merely a plausible-sounding narrative. The auditor samples decisions and reperforms the attribution with the declared tool to compare.

Depth on *how* each explainability method works sits with `ai-risk-engineer` and the research literature; the auditor applies the tools and tests faithfulness.

### GDPR Article 22 and the "meaningful information" test

GDPR Article 22 grants data subjects the right not to be subject to solely-automated decisions with legal or similarly significant effects, and the right to meaningful information about the logic involved. The auditor tests:

- The organisation's declared basis for Article 22 (consent, contract-performance, or EU / member-state law).
- The information-provision process for the subject.
- The challenge / appeal mechanism.
- The human review pathway (if the organisation is relying on the "not solely automated" carve-out).

A programme for an EU-deployment that cannot produce this evidence is an Article 22 finding (and often a separate data-protection authority exposure).

## The model-card and bias-audit-report publication cadence

The programme's publication cadence is tested as a single compound test:

- **Model-card / system-card refresh cadence.** The AIMS methodology declares a cadence (per release, per quarter, triggered). The auditor samples the current model-card version and compares to the methodology.
- **Bias-audit-report cadence.** Per obligation (LL144 annual) or per the organisation's methodology.
- **Public publication.** The current artefact is reachable; the prior-period artefact is version-controlled and retrievable.
- **Internal audit-committee reporting.** Fairness-metric trends are reported to the audit committee at the declared cadence.

The auditor does not require a single cadence across all artefacts; the auditor requires that each artefact's declared cadence is held.

## Common failure modes

- **Metric chosen once, never reviewed.** The programme's metric selection has not been revisited since the original use case.
- **Mitigation loop that does not close.** Interventions are declared but the register residual score and the public report do not reflect the post-mitigation evidence.
- **Intersectionality reported only where favourable.** Intersectional metrics that pass are published; failing intersections are quietly aggregated. The auditor insists on the full matrix.
- **One jurisdiction's shape used for all jurisdictions.** The programme reports LL144-shape numbers for every deployment regardless of whether LL144 applies; the auditor flags non-fit.
- **Consumer explanations that are model-generic, not decision-specific.** The explanation says "we use several factors" without naming which factors drove *this* decision.
- **"Our model is bias-free."** Categorical claim; grade E; documentation finding.
- **Explainability tool does not match the model.** SHAP applied to a model where the required assumptions do not hold; the attribution is not faithful.
- **LL144 publication expired.** The audit on the website is 14 months old.
- **Colorado AI Act ignored for a Colorado-deployed system.** The programme did not update for the new jurisdiction.

## Summary

- The programme audit tests the obligation-map coverage, metric-selection process, mitigation-loop operation, subgroup / intersectionality coverage, publication cadence, and explainability programme.
- Metric-selection is a documented process with a defensible rationale and second-line review; silent selection is a process finding.
- Mitigation loops close with a residual-risk update, an updated publication, and a monitor — the chapter-4 adversarial-ML pattern repeats here.
- Intersectionality coverage is reported at the declared minimum sample size and documented where the sample is inadequate.
- NYC LL144, Colorado AI Act, and EU AI Act Articles 10 / 15 / 27 drive concrete, testable publication and disclosure requirements that the auditor samples directly.
- Explainability obligations (GDPR Article 22, ECOA adverse-action, Article 86, consumer notices) drive separate publication and faithfulness tests.
- The auditor runs Fairlearn / AIF360 / Holistic AI as reperformance tools; the authoring of fairness metrics and mitigations sits with `ai-risk-engineer` and `model-evaluation-engineer`.
