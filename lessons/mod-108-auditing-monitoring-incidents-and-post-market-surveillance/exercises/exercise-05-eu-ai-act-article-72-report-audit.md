# exercise-05: EU AI Act Article 72 Post-Market Monitoring Report Audit

**Estimated effort:** 2.5 hours

## Objective

Audit an **Article 72 Post-Market Monitoring Report** for a high-risk AI system as a *document*. Test whether the report reflects actual execution of the plan audited in exercise 01, whether data adequacy supports the report's claims, whether breach-reporting evidence is present for every cited incident, and whether the next-period update evolves the plan on evidence. The deliverable is the report-audit workpaper, with per-section findings and a one-page memo on report integrity.

This exercise is conformity-shaped — the audience of the report is partly external (market-surveillance authority, notified body), and the exercise tests the report to the standard that external audience would apply.

## Prerequisites

- Chapter [`05-auditing-the-article-72-post-market-monitoring-report.md`](../05-auditing-the-article-72-post-market-monitoring-report.md).
- Chapter [`01-auditing-the-continuous-monitoring-program.md`](../01-auditing-the-continuous-monitoring-program.md).
- Chapter [`03-auditing-the-incident-response-program.md`](../03-auditing-the-incident-response-program.md).
- Chapter [`04-reperforming-incidents-end-to-end.md`](../04-reperforming-incidents-end-to-end.md).
- `mod-105` for the AIMS framing and `mod-110` for the conformity-assessment-body interface (lightweight reference).

## Scenario

Choose an organisation operating a **high-risk AI system** under EU AI Act Annex III (or an Annex I product with embedded AI subject to Chapter III), and obtain its most recent Article 72 Post-Market Monitoring Report (or construct a plausible one from the underlying plan if the organisation has not yet produced the first report). State the subject at the top of the deliverable.

Suggested defaults: reuse the Northland Re insurance scenario from exercise 01; or the Luminos Health clinical-decision-support scenario from `mod-107` exercise 01; or a published AI-system case (where the provider has disclosed post-market monitoring under MDR Article 83 in the medical-device space, which gives a credible analogue). If the Article 72 Commission template has been published at reading time, use it as the primary structure. <!-- needs-research: confirm Article 72(3) implementing-act template status at reading time -->

## Requirements

1. **Pin the subject.** The system (Annex IV identifiers, intended purpose, deployers, versions), the report being audited (title, version, reporting period), and the regulatory posture (notified-body relationship if any, Article 71 EU Database registration status, Article 17 QMS framework).

2. **Section-completeness audit.** Produce a table with rows for the expected sections from chapter 5 — scope, monitoring-plan execution, serious-incident and corrective-action, changes-to-the-system, risk-register-and-impact-assessment, next-period update. Columns: present / partial / absent, plus a comment column. A missing section is a Day-1 Article 72 finding.

3. **Plan-execution reperformance.** Sample at least three signals cited in the report. For each:
   - Pull the plan definition.
   - Pull the raw data for the reporting period.
   - Independently compute the signal value.
   - Compare to the report's reported value.
   - Record the delta.

4. **Threshold-breach count reperformance.** For each sampled signal, independently count threshold breaches in the period and compare to the report's count. Record under-count / over-count / match per signal.

5. **Data-adequacy test.** Produce a short write-up covering:
   - Statistical sufficiency for low-volume subgroups.
   - Trace completeness for incident-triggered signals.
   - Retention adequacy against the reporting-horizon claims.
   - Representativeness of sampled traffic (if the organisation samples).
   - Deployer-feedback ingestion (if the organisation is a provider distributing to downstream deployers).

6. **Breach-reporting evidence audit.** For every incident and corrective action cited in the report, demand:
   - Article 73 submission receipt and market-surveillance-authority acknowledgement (where applicable).
   - Corrective-action record from the Clause 10.1 tracker.
   - Regression-fixture evidence (unit / eval / monitor).
   - Effectiveness-review evidence (Clause 10.1 step 4).
   Missing evidence per claim is a finding.

7. **Next-period update audit.**
   - Does the report propose named plan changes for the next period?
   - Are the proposed changes traceable to the period's incidents or near-misses?
   - Is threshold re-calibration against the period's distribution evident?
   - Are new deployments covered by new signals?
   - Is the proposal signed by the AIMS owner and the QMS?

8. **Regulator-facing quality test.** Rate the report (pass / fail per criterion) on:
   - Plain-language executive summary.
   - Factual tone (no marketing framing).
   - Evidence pointers per material claim.
   - Consistency with Article 73 filings.
   - Non-contradiction with model-card / system-card public claims (cross-reference `mod-106`).

9. **Article-interface audit.** Produce a table — Chapter III Section 2 article × monitoring-plan signal — showing which article each signal evidences. Missing interfaces are Article 72 interface findings.

10. **Findings register.** As in previous exercises. Add a *report-integrity-vs-monitoring-integrity* classification column — a reporting defect (signal computed correctly on the dashboard, mis-stated in the report) vs. a monitoring defect (signal mis-computed at the dashboard too).

## Starter guidance

- Section-completeness audits are mechanical; do not skip them. The missing-section finding is often the most consequential finding of the engagement because it is the most defensible against a regulator.
- The plan-execution reperformance is where report-integrity findings concentrate. Expect numerical drift between the dashboard and the hand-edited report.
- Data adequacy for low-volume subgroups is often the hidden story — a report that claims "no bias detected" in a subgroup with n=30 is not evidence of no bias.
- Next-period-update findings are frequently the deepest structural findings — a plan that never changes is a plan that is not learning.
- Downstream-deployer-feedback ingestion is commonly absent in first-cycle reports.
- Cross-check with `mod-106` if the organisation's model card contradicts the report's numbers.

## Acceptance criteria

The deliverable is accepted when:

- The subject is pinned with Annex IV identifiers and reporting-period dates.
- The section-completeness audit covers every expected section with status per row.
- Plan-execution reperformance covers ≥ 3 signals with per-signal reperformance evidence.
- Threshold-breach count reperformance covers the same signals.
- Data-adequacy assessment covers all five sub-points.
- Breach-reporting evidence audit tests every cited incident and corrective action.
- Next-period update audit produces a go / no-go judgement.
- Regulator-facing quality test rates the report on all five criteria.
- Article-interface matrix is populated across Chapter III Section 2 articles.
- Findings are classified report-integrity vs. monitoring-integrity.
- `<!-- needs-research: ... -->` is used for any Article-72 specifics that cannot be pinned to published text or the Commission implementing act at reading time.

## Stretch goals

- Produce a **pre-visit-pack** the organisation would hand to the market-surveillance authority alongside the report, listing evidence pointers for every material claim.
- Draft a **report template** aligned to the (as-published or draft) Commission implementing-act template, with the organisation's gaps pre-filled.
- Author a **Model-card vs. Article 72 report cross-check** matrix comparing the public model-card claims (mod-106) to the Article 72 numbers, listing any contradiction.
- Build a **Clause-9.1-to-Article-72 traceability** report showing which Clause-9.1 monitoring targets feed the Article 72 report sections, using the exercise-01 workpaper as input.
