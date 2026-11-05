# exercise-01: Continuous Monitoring Program Audit Drill

**Estimated effort:** 2 hours

## Objective

Audit a continuous-monitoring program for an in-scope AI system against **ISO/IEC 42001 Clause 9.1** and **EU AI Act Article 72**, and produce the three workpaper artefacts chapter 1 describes: a **criteria crosswalk**, a **determinate-set walk** across the plan's monitored targets, and an **operation-walk** with threshold-breach reperformance on a sample of signals.

The deliverable reads like the opening section of a Stage-2 fieldwork workpaper — the section a reviewing partner can inspect without needing the auditor's personal explanation.

## Prerequisites

- Chapter [`01-auditing-the-continuous-monitoring-program.md`](../01-auditing-the-continuous-monitoring-program.md).
- `mod-102` on criteria translation (so the Clause 9.1 ↔ Article 72 crosswalk can be constructed against the correct source texts).
- `mod-103` on scoping and materiality (so the sample reflects the engagement letter).
- `mod-104` on evidence discipline and sampling (so the reperformance holds up).
- `mod-105` chapter 8 on Clause 9.1 for the AIMS framing.

## Scenario

**Northland Re** is a European reinsurer deploying an in-production generative-AI assistant that supports claims-adjudicators with policy interpretation, prior-decision retrieval, and draft-decision authoring. The assistant is classified as a high-risk AI system under EU AI Act Annex III point 5 (access to and enjoyment of essential private services) for the subset of claims involving motor and health policies. <!-- needs-research: confirm exact Annex III scoping for insurance-adjacent applications at reading time -->

Northland Re has an AIMS certified to ISO/IEC 42001, a published monitoring plan (version 4, approved Q1 of the prior year), and a separate Article 72 post-market monitoring plan (version 2, approved Q3 of the prior year). You are the lead auditor on an internal-audit engagement commissioned by Northland Re's Risk & Compliance Committee as a readiness check for the certification-body surveillance visit scheduled in six months.

If you need a different anchor (not every learner has a reinsurance background), substitute any published AI-governance programme from a bank, hospital system, public-sector deployer, or large employer that has disclosed monitoring structure. State the chosen subject at the top of the deliverable.

## Requirements

1. **Pin the subject.** Record the subject organisation, the AI system, the system's regulatory position (Article 72 in scope? SR 11-7 model-risk material? NAIC applicable? FDA-regulated?), the monitoring-plan and Article 72-plan document names and versions, retrieval date, and any `needs-research` where a scoping question is open.

2. **Build the criteria crosswalk.** A single markdown table following the chapter-1 shape — rows are "who is bound," "what must be monitored," "how it is codified," "what it must drive," "retention," "who reviews." Columns are **ISO/IEC 42001 Clause 9.1** and **EU AI Act Article 72** (with a third column where the organisation is also bound by SR 11-7, NAIC, or FDA). Cite the clause / article text — paraphrase is permitted, misquotation is not.

3. **Determinate-set walk.** Produce a table listing every monitored target in the plan (minimum 15 rows or the full plan, whichever is smaller). Columns: *what*, *how*, *when (measure)*, *when (analyse)*, *who (analyse / evaluate)*, *threshold(s)*, *escalation path*, *retention*, *Chapter III Section 2 article (Article 72 overlay only)*. Mark each cell as populated, partial, or absent. Any target missing fields is a finding candidate.

4. **Operation walk on a sampled subset.** Sample at least six monitored targets, stratified per chapter 1's "reperformance sample must include" list (one quality, one safety, one drift, one operational, one near-miss, one harm-specific). For each sampled target, verify:
   - Data was collected per the stated method (produce a pointer to the raw data for the window).
   - Retention honoured — produce evidence a measurement from the start of the retention window still exists.
   - Analysis happened on cadence — produce the analysis artefact.
   - Evaluation produced a decision — produce the decision record.

5. **Threshold-breach reperformance.** For each of three sampled signals, independently compute the signal over a period containing a known or suspected breach, plot against the threshold, and identify crossings. For each crossing, trace to the alert record, the triage decision, and the register / corrective-action update. A crossing without a corresponding alert is a finding candidate.

6. **Escalation walk.** For one tripped-threshold event from the reperformance, walk the full escalation chain per chapter 1 — alert emitted, received, triaged, register updated, Article 73 clock (if applicable) considered, audit-committee reporting (if above materiality), corrective-action closure.

7. **Retention reperformance.** Pick one monitoring-data point from the earliest edge of the retention commitment and demand its production. Pick one Article 19 log entry from ≥ 6 months ago (or the stated organisation-specific horizon) and demand its production. Record the results.

8. **Findings register.** One row per finding candidate. Columns: finding ID, title, criterion reference (Clause 9.1 vs. Article 72 vs. internal policy — the distinction matters), affected target, severity under the organisation's grading convention (and ISO/IEC 17021-1 convention if the engagement adopts it), evidence pointer, management-response-requested shape. Do not author the response.

9. **Sampling and workpaper hygiene.** Record the sampling frame, the stratification rationale, and the resulting assurance level per `mod-104` discipline. Note retrieval timestamps, hashes, and `needs-research` markers inline.

## Starter guidance

- Treat Clause 9.1 and Article 72 as *separate* criteria, not a single blended standard. The crosswalk forces the distinction.
- A target "watched by the ML team" with no named role is a finding even when the ML team is competent — Article 72 and Clause 9.1 both demand named ownership.
- Expect the data-and-feature-drift targets to pass structurally and the near-miss / jailbreak-detection targets to show gaps — the pattern is common in early-maturity programmes.
- The reperformance is about *configuration verification*, not independent methodology design; apply the organisation's declared method and compare.
- Where a specific Clause 9.1 or Article 72 obligation is ambiguous in the as-published text, do not guess — write `<!-- needs-research: ... -->` with the specific question.
- Note where you would invoke ISA 620 specialist use for chapter-2-depth signals (you may, in this exercise, defer the specialist engagement and record the reason).

## Acceptance criteria

The deliverable is accepted when:

- The subject and scope are pinned with regulatory-position call-outs.
- The criteria crosswalk is populated against as-published Clause 9.1 and Article 72 text (or the MDR Article 83 analogue where Article 72(3) implementing act is unpublished at reading time).
- The determinate-set walk table has ≥ 15 rows (or covers the full plan) with per-column population status.
- The operation walk sample includes at least six targets stratified per the chapter-1 requirement.
- Threshold-breach reperformance covers ≥ 3 signals and, for each, identifies at least one crossing *or* documents the absence of crossings with method evidence.
- One escalation walk is fully documented from alert to closure.
- Retention reperformance covers both a monitoring data point and an Article 19 log.
- Findings are stated against the specific criterion (not "monitoring is weak").
- Sampling and workpaper hygiene are documented per `mod-104`.
- `<!-- needs-research: ... -->` is used where a factual claim cannot be verified from primary sources.

## Stretch goals

- Author the one-page **audit-committee memo** summarising the findings at Sev-2+ in a format consistent with `mod-111`'s findings-reporting discipline.
- Produce a **Clause 9.1 vs. Article 72 gap matrix** — which monitored targets would satisfy only Clause 9.1 and would fail an Article 72 completeness review.
- Draft a **template update** for the next-period monitoring plan based on the findings identified.
- Write a short (≤ 500 words) note on when the auditor would invite the notified body (Annex VI / VII) to review the same monitoring plan during conformity-assessment surveillance, and what the auditor's workpapers would need to include to make that invitation productive. See `mod-110` for the conformity-assessment-body shape.
