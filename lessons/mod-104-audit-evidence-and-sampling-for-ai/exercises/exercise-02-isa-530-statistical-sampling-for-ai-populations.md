# exercise-02: ISA 530 Statistical Sampling for AI Populations

**Estimated effort:** 3 hours

## Objective

Design, select, and document the sampling workpaper for an AI-system engagement that needs both statistical attribute sampling and judgmental edge-case sampling. Produce the engagement-quality-reviewer-ready sampling workpaper, including the frame-to-definition reconciliation, the sample-size justification, the selection file, and the projection shape the final conclusion will use.

## Prerequisites

- Chapter [`02-isa-530-sampling-for-ai-populations.md`](../02-isa-530-sampling-for-ai-populations.md)
- Chapter [`01-isa-500-evidence-applied-to-ai-artifacts.md`](../01-isa-500-evidence-applied-to-ai-artifacts.md) — evidence-grading discipline
- `mod-103` chapter 3 (materiality) — needed to pick the tolerable deviation rate
- Working familiarity with a standard attribute-sampling table (e.g., **AICPA Audit Guide, *Audit Sampling*, Appendix A**) or equivalent reference you can cite

## Scenario

The engagement is testing the following control for **Osprey Mutual Bank's** mortgage pre-approval model under a SR 11-7-aligned independent model-validation posture:

> "Every model-version promotion to production during the audit period 2026-01-01 through 2026-09-30 was: (a) authorised by a member of the Model Risk Committee on the current authorisation matrix; (b) accompanied by a documented pre-promotion test suite result; and (c) recorded in the model registry with the model artifact hash."

Four facts drive population definition:

- The engagement period is nine months (2026-01-01 to 2026-09-30).
- The model-registry database (an internal PostgreSQL table) shows **742** rows tagged `deployment=production` across the period. Of these, **18** rows are on the model owner's staging cluster (mis-tagged); the remaining **724** are genuine production promotions.
- The organisation's internal change-tracker (Jira project `MRC`) has **689** tickets in state `Deployed` with component `mortgage-pre-approval` across the period.
- One week — 2026-07-15 through 2026-07-21 — has no rows at all in the registry (a known outage of the registry's audit logger; the organisation's incident record acknowledges the gap and states that promotions were suspended that week; the Jira project corroborates zero `Deployed` transitions).

Judgmental sampling scope: the engagement separately selects **ten** edge-of-policy cases from the organisation's red-team catalog for the fairness-related controls.

Materiality (from the engagement plan): overall materiality at 5% of the mortgage-pre-approval portfolio's gross book value; performance materiality 60% of overall; tolerable rate of deviation on this control: 5% at 95% confidence; expected rate of deviation from the prior-year engagement: 1%.

## Requirements

1. **Define the population**. Write the one-paragraph population definition for the attribute test. Be specific about what is in and what is out.
2. **Pin the sampling frame.** Which underlying store is the frame drawn from — the registry database, the Jira project, or a reconciliation of the two? Author the SQL (pseudocode acceptable) that produces the frame; explain why you chose that frame.
3. **Reconcile the frame to the population.** The registry shows 742 rows (with 18 mis-tags); Jira shows 689 tickets. Reconcile the two; identify the delta and explain each piece of it (the mis-tags, the outage week, any other legitimate differences); document the handling of the outage week.
4. **Determine the sample size** using the engagement's tolerable-rate / expected-rate / confidence inputs. Cite the table or formula you used; state the sample size.
5. **Select the sample.** Describe the selection method (random / systematic / stratified random / monetary-unit); if stratified, name the strata and the per-stratum sample sizes; pick and record a random seed; produce the resulting list of row identifiers (pseudocode / SQL that produces the identifier list is acceptable; actual integer identifiers are not required if clearly reproducible).
6. **Specify the audit procedure per sampled item.** For each sampled promotion, name the procedure the audit team runs — which artifacts are inspected, which hashes reconciled, which cross-references confirmed, how a deviation is defined.
7. **Specify the evaluation and projection plan.** Name the attribute-sampling evaluation method; state the formula or table reference for the upper-limit deviation rate (ULDR) given k deviations in n sample items at the engagement's confidence level; state the conclusion rule (if ULDR ≤ tolerable rate → control passes; otherwise, named consequences).
8. **Author the judgmental-sampling workpaper** for the ten red-team edge-of-policy cases. Explain: how the ten are selected (the judgment basis); why they are *not* projectable; how the findings on the ten will be used in the final conclusion (corroborative, not statistical).
9. **Document the sampling workpaper in the chapter-5 shape.** Objective / Criterion / Procedure / Evidence / Exception / Conclusion, with cross-references and preparer/reviewer.

## Starter guidance

- Chapter 2 §Population definition is the trap most sampling workpapers fail on; the 742-vs-689-vs-outage is doing the work here.
- The outage week is a completeness exception — do not sample into a week with no frame; the workpaper names the handling (e.g., corroborate against the incident record, consider a scope limitation, or extend procedures to directly confirm no promotions occurred).
- The 18 mis-tagged rows should be excluded from the frame once identified, but the reconciliation should document the discovery and the handling.
- The engagement may elect to stratify by month (controls weaken toward quarter-end at some organisations) or by model-risk tier (high-materiality model versions get higher sampling attention) — either is defensible if named ahead of selection.
- Use an attribute-sampling table (the AICPA Audit Guide Appendix A is a reasonable reference) rather than an ad-hoc calculation; cite the table.
- The random seed must be recorded in the workpaper and must produce the same sample on re-run.
- The judgmental sample is *not projectable*; the workpaper must be explicit about the qualitative role.
- Use `<!-- needs-research: ... -->` where you would need the actual organisation's authorisation matrix, test-suite format, or model-registry schema to write the procedure in full.

## Acceptance criteria

The deliverable is accepted when:

- The population definition is one unambiguous paragraph.
- The frame query is explicit and reproducible; the frame-to-population reconciliation accounts for all 742 - 724 - 689 - outage deltas with named handling for each.
- The outage week is named and handled; the workpaper does not silently sample over a gap.
- The sample size is computed from the engagement's tolerable-rate, expected-rate, and confidence; the computation cites a table or formula.
- The selection method is named; the random seed is recorded; the resulting identifier list is reproducible (pseudocode is acceptable).
- The audit procedure per sampled item names concrete artifacts (committee minutes, test-suite result, registry hash) and the deviation definition.
- The projection plan names the ULDR computation and the conclusion rule.
- The judgmental sampling workpaper explicitly states non-projectability and the corroborative role.
- The workpaper follows the chapter-5 shape (Objective / Criterion / Procedure / Evidence / Exception / Conclusion / cross-references / preparer / reviewer).
- At least one `<!-- needs-research -->` placeholder where the scenario legitimately underspecifies a field.
- No invented statistics or fabricated statutes beyond the scenario.

## Stretch goals

- Author a **companion-repo structure** for the sampling workpaper (chapter 5 §Working inside a Git-tracked repo for AI-native engagements) with `sample.md`, `selection.sql`, `selection.json`, and `frame-reconciliation.md`.
- Propose an **MUS variant** of the sample where the sampling unit is weighted by the mortgage portfolio value touched by the promoted model; explain when MUS is preferable to equal-probability random sampling here.
- Draft the **finding template** for the case where ULDR exceeds the tolerable rate (how the conclusion changes; which workpapers are affected; what the management response shape would be).
- Extend the sampling discipline to a **variables sampling** workpaper for a related assertion ("the production model's claimed AUC during the period was within 1 percentage point of the independently measured AUC") — state the confidence level, tolerable difference, expected difference, pilot-sample plan, and the final sample size formula.
