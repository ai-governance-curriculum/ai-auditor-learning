# exercise-04: Fairness Claim Audit in the NYC LL144 / EEOC Shape

**Estimated effort:** 3 hours

## Objective

Audit a fairness claim through the full chapter-5 shape: obligation map, metric-appropriateness, protected-class coverage, intersectional reporting, number reproduction, and the **bias-audit report in the NYC Local Law 144 / BABL AI-shaped format** (NYC publication-ready) and a brief **AIA summary**.

The target is a real engagement-shaped deliverable — the kind a mid-sized consulting firm would file with the NYC Department of Consumer and Worker Protection on behalf of a deployer.

## Prerequisites

- Chapter [`05-auditing-fairness-claims.md`](../05-auditing-fairness-claims.md).
- `mod-102` on criteria translation (NYC LL144, EEOC 29 CFR Part 1607, EU AI Act Article 10).
- A test dataset — either the vendor's shared dataset (under NDA), or a public labelled dataset the engagement maps to the obligation. For exercise purposes you may use the **UCI Adult / Folktables ACS income** dataset with ACS-provided demographic columns, or an analogous public resume-screening-adjacent dataset you can cite. Document the choice and its limitations.
- `fairlearn` and `aif360` installed (chapter 2's cross-check discipline requires at least two independent implementations).

## Scenario

**Meridian Staffing** is a NYC-based staffing firm deploying a third-party AI resume-screening tool (call it "SifterAI") that produces a continuous "match score" per candidate against open requisitions. Meridian's HR technology team uses the score to decide who advances to a recruiter review. SifterAI's published model card claims:

> "SifterAI achieves a selection-rate ratio of 0.87 across race categories and 0.91 across sex, exceeding the four-fifths threshold on both axes. Audit conducted Q2 2026, n = 4,200 historical candidates."

Meridian must publish a NYC LL144 bias audit before July 5, 2026 for its first full year of SifterAI use. You are the independent auditor commissioned under § 20-871 et seq. with no prior consulting relationship with Meridian or SifterAI's vendor.

For this exercise the "subject-matter dataset" is whichever public labelled dataset you selected above; your fairness computation stands in for SifterAI's claimed audit. Document the substitution explicitly in the deliverable.

## Requirements

**Part A — Obligation map and metric-appropriateness (half-hour)**

1. **Map the obligation.** A one-page obligation map covering: NYC LL144 scope coverage (does the use count as an AEDT in employment); EEOC 29 CFR Part 1607 overlay; any sector overlay (state fair-employment laws). For this exercise, LL144 applies.
2. **Grade the vendor's metric choice.** SifterAI reports selection-rate ratio across race and sex. LL144 requires impact ratios across the EEO-1 categories and intersections. Is the metric appropriate? Is the class-set appropriate? Record a one-paragraph grading (strong match / soft mismatch / hard mismatch / absent).
3. **Record the reference-class choice.** LL144 asks the highest-selection-rate group to be the reference; does the card state that or not? Capture.

**Part B — Reproduction of the vendor's computation (1.5 hours)**

4. **Replicate the core impact-ratio computation** on your chosen dataset:
   - selection-rate per EEO-1 race category (or the dataset's nearest analogue);
   - selection-rate per sex category;
   - selection-rate per intersection (race × sex) where the sample supports it (document the sample-adequacy threshold you chose, e.g., ≥30 per cell);
   - impact ratios with highest-rate group as reference;
   - 10,000-resample fixed-seed bootstrap CI per ratio.
5. **Cross-check with a second implementation.** Use `fairlearn.metrics.MetricFrame` and `aif360.metrics` (or `holisticai.bias`) on the same labelled data; confirm the computations agree to within numerical tolerance.
6. **Produce the signed-delta rows** — one per fairness metric — against the vendor's claim.

**Part C — AIA summary (half-hour)**

7. **Author a one-page Algorithmic Impact Assessment summary** per chapter 5:
   - system identification;
   - decision significance (who / what / appeal);
   - fairness-obligation analysis;
   - metric selection and justification;
   - protected-class coverage;
   - intersectional reporting (and adequacy notes);
   - observed fairness result;
   - replication delta;
   - scope restrictions;
   - finding register references (even if the register has only 2–3 rows for this exercise).

**Part D — LL144 bias-audit report (half-hour)**

8. **Produce the bias-audit report in the BABL AI / LL144 publication shape**:
   - identifying the AEDT by name and version;
   - stating the audit period and the auditor's independence;
   - stating the data provenance (vendor-shared historical candidate data or your substitution);
   - selection-rate and scoring-rate ratios across EEO-1 categories and intersections;
   - an interpretive paragraph noting whether the four-fifths rule is met per pair;
   - a limitations section;
   - auditor signature and date.

## Starter guidance

- The four-fifths rule is a rule of thumb; your report states ratios, cites the EEOC guidance, and leaves the "pass/fail" to the regulatory reader. Avoid both over- and under-claiming.
- Where the intersection sample is too small, report the ratio *and* the CI — if the CI is wide enough to span the four-fifths line, say so.
- Bootstrap CIs for ratios can be computed with a paired resample; `fairlearn` has helpers.
- Cross-implementation agreement to within 0.001 is typical for selection-rate ratios on the same dataset; larger drift indicates one of the implementations is doing something different (e.g., handling missing-sex categories differently). Chase the drift down.
- The obligation map does not need to cover every US state's fair-employment overlay; for NYC-only employment, LL144 is the primary and EEOC the secondary.
- The AIA summary and the LL144 bias-audit report cover overlapping facts; keep the AIA higher-level and narrative-first, and the LL144 report publication-ready (shorter, more table-centric).
- Do not design a mitigation. If you observe a failing ratio, the finding is the number; management response (`mod-111`) is out of scope.

## Acceptance criteria

The deliverable is accepted when:

- The obligation map explicitly cites LL144 and EEOC 29 CFR Part 1607 and names the sector overlay (or notes its absence).
- The metric-appropriateness grading is reasoned, not asserted; a one-paragraph justification accompanies the grade.
- The replicated impact-ratio table contains one row per EEO-1 group and per intersection where the sample supports it, with bootstrap CIs.
- Two independent implementations (Fairlearn + AIF360 or Fairlearn + Holistic AI) produced the same core numbers to numerical tolerance; the cross-check output is in the workpaper.
- Signed-delta rows per fairness metric are emitted.
- The AIA summary covers the ten sections listed in chapter 5.
- The LL144 bias-audit report reads as publication-ready — concise, table-centric, with a limitations section and an independence statement.
- Any sample-size shortfall for an intersectional cell is disclosed, not hidden.
- Any substitution (public dataset standing in for vendor-shared data) is explicitly flagged at the top of the deliverable.
- No sentence in the LL144 report "designs" a mitigation or advises on a remedy.

## Stretch goals

- Compute **equal-opportunity** (TPR) differences across groups as a secondary metric; discuss whether LL144 obligates it (it does not) and whether EU AI Act Article 10 would (plausibly yes for a high-risk employment system). Record the result alongside the LL144 primary.
- Produce the **public-variant and regulator-variant pair** of the LL144 bias audit — same content, different presentation (chapter 7 variants).
- Author a **"vendor information-request letter"** — a one-page request from the auditor to SifterAI for the data-provenance, class-definition, and reference-class clarifications that the published card did not state.
- Sketch an **EU AI Act Article 27 FRIA addendum** — the fundamental-rights sections the EU regulator would read beyond the LL144 shape. Note explicitly where the shape differs.
