# exercise-07: Follow-Up Tracker Audit on Prior-Period Findings

**Estimated effort:** 1.5 hours

## Objective

Audit the AI audit function's **follow-up tracker** on prior-period findings. Reperform a sample of closure claims against the current state, test open-finding discipline against committed-closure dates, identify repeat findings as program-level signals, and produce the materiality roll-up that lands in the audit-committee pack.

This is a reflexive exercise: the audit function tests itself. It is also the exercise most closely coupled to `mod-111` findings-reporting; keep the output shape compatible with the findings-register pattern used across the track.

## Prerequisites

- Chapter [`07-auditing-the-follow-up-tracker.md`](../07-auditing-the-follow-up-tracker.md).
- `mod-101` on audit-function independence (relevant to the self-review guardrail).
- `mod-105` chapter 9 on Clause 10.1 (the corrective-action loop the tracker reflects).
- `mod-111` for the findings-reporting discipline (upstream of the tracker).

## Scenario

Reuse the organisation from exercise 01 and exercise 03. Pull the AI audit function's follow-up tracker as of the engagement's cut-off date. Minimum: the tracker contains findings from at least two prior cycles (`mod-105` Stage-2, a prior `mod-108` engagement, or an equivalent AI-governance audit). If no prior cycles exist, use the exercise-03 and exercise-04 findings as a simulated "prior-period" and note the simulation at the top of the deliverable.

## Requirements

1. **Pin the tracker.** Record the tracker's location (GRC platform workspace, spreadsheet, Jira project), its field schema, the retrieval date, and a hash or snapshot of the row contents. Note any findings that have been edited since the prior cycle.

2. **Field-completeness audit.** Produce a table of expected fields (per chapter 7) × population status. A tracker missing finding ID, source, severity, response, committed-closure date, evidence pointer, or re-performance status is a tracker-hygiene finding.

3. **Closure-evidence test.** Sample at least six "closed" findings (stratified across severity and source). For each:
   - Pull the committed corrective action.
   - Pull the evidence provided for closure.
   - Reperform the test that raised the original finding against the current state.
   - Confirm Clause 10.1 step-4 effectiveness review.
   Classify each sample row as **closed-confirmed**, **closed-not-confirmed**, **partially-closed**, or **closed-under-superseded** (with rationale).

4. **Open-finding discipline audit.** For the open population:
   - Count open findings past committed-closure date.
   - Build an age-distribution table.
   - Produce a pattern-by-owner table — which owners accumulate overdue findings.
   - Produce a pattern-by-severity table.
   - Produce a pattern-by-criterion table (ISO 42001 clauses, AI Act articles, SR 11-7, NAIC, FDA — which criterion ages worst).

5. **Repeat-finding detection.** Identify repeats using chapter 7's four patterns: exact-title, criterion-and-system, root-cause, owner-and-category. Produce a list of repeats with the originating and recurring finding IDs. Each repeat becomes a **systemic-issue finding** opened in the current period.

6. **Status accuracy audit.** For a sample of five tracker rows, verify the status field against the underlying evidence. A `tested-closed` with no recent test is a stale-status defect; a `superseded` without approved rationale is a supersession defect.

7. **Cross-cycle traceability test.** Confirm:
   - Finding IDs are stable across cycles.
   - Historical evidence survived any platform migration.
   - The next-cycle planning (`mod-103`) ingests the open-finding list as a risk-weighting input (by interview or by walking the planning memo).
   - Management-review inputs (Clause 9.3.2) include the tracker status.

8. **Materiality roll-up.** Produce the audit-committee summary: total findings in the period (prior-open + current-raised), closed in the period (confirmed vs. not-confirmed), open at period end by severity and age, repeat findings count with systemic-issue count, materiality-weighted trend.

9. **Independent-review flag.** Record how the audit function's own tracker is independently reviewed per `mod-101` (external quality assessment under IIA Standard 1312, or peer review, or an independent audit committee's review). If no independent review exists, note that this exercise is self-review and flag as a finding on the audit function's own governance.

10. **Findings register.** Short — expect 3–8 findings. Column shape as before; add a *tracker-vs-underlying* classification distinguishing findings on the tracker's own hygiene from findings on the underlying corrective actions.

## Starter guidance

- Reperform the original test's procedure, not a new procedure. The question is whether the original condition still holds.
- A Clause 10.1 step-4 effectiveness-review is usually missing even where closure is otherwise sound; report the finding as a *tracker-integrity* finding when the closure was a management-response field update rather than an effectiveness-review artefact.
- Repeat findings are the single sharpest audit-committee signal. Take the time to identify repeats properly rather than batching same-criterion / different-system as if they were new.
- The materiality roll-up is the artefact that directly influences the audit-committee memo; write it in that voice.
- An audit function without an independent quality assessment is a governance concern; record it without hedging.

## Acceptance criteria

The deliverable is accepted when:

- The tracker is pinned with retrieval date, schema snapshot, and hash.
- Field-completeness audit covers the chapter-7 field list.
- Closure-evidence test samples ≥ 6 findings with reperformance and step-4 effectiveness review classification.
- Open-finding discipline produces four pattern tables (age, owner, severity, criterion).
- Repeat-finding detection runs through all four pattern types with a repeat list.
- Status accuracy audit samples ≥ 5 rows.
- Cross-cycle traceability confirms ID stability, platform-migration survival, next-cycle ingestion, and Clause 9.3 inclusion.
- Materiality roll-up is in audit-committee-ready form.
- Independent-review flag is set (or the self-review limitation is noted).
- Findings are classified tracker-vs-underlying.
- `<!-- needs-research: ... -->` used where a factual claim cannot be verified.

## Stretch goals

- Author the **audit-committee one-page memo** summarising repeat findings and overdue-majors, in the voice `mod-111` chapter will define.
- Produce a **tracker-schema improvement proposal** aligned to IIA Standard 2500.A1 and ISO/IEC 42001 Clause 10.1, with field additions the organisation could adopt.
- Build a **small script** (Python / Google Sheets Apps Script / etc.) that detects repeat-finding candidates by title-similarity and criterion-match, suitable as a standing control for the audit function.
- Draft the **external quality assessment scope** for the AI audit function under IIA Standard 1312, if the organisation does not currently commission one.
