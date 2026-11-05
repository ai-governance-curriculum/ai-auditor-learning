# Auditing the Follow-Up Tracker on Prior-Period Findings

## Motivation

An audit function that generates findings but does not test their closure is a one-way reporting pipeline. Every mature audit standard — IIA Standard 2500 "Monitoring Progress," ISO 19011 Clause 6.7 "Conducting audit follow-up," ISO/IEC 42001 Clause 10.1 corrective action, SR 11-7 MRM — expects the audit function to test prior-period findings through to closure and to surface repeat findings as program-level signals.

This chapter audits the **follow-up tracker** — the register of open and closed findings from the audit function's own prior engagements — and tests the closure evidence, the recurrence pattern, and the status accuracy. It is a reflexive piece of fieldwork: the auditor tests the audit function's own hygiene.

In an AI-audit context the follow-up tracker is a strong signal of governance maturity. A tracker with many findings open past their committed-closure dates is almost always correlated with weaknesses in Clause 10.1 corrective-action execution — the same weakness the earlier chapters probe from the incident angle. And a cluster of repeat findings is a strong indicator that a specific first-line or second-line process is systemically weak and that previous management responses were symptomatic rather than root-cause.

## Scope and position

The follow-up-tracker audit sits in this module (not in `mod-111`) because the natural inputs are:

- The AIMS Clause 10.1 corrective-action loop from chapter 3.
- The end-to-end incident reperformance findings from chapter 4.
- The three-lines independence findings from chapter 6.
- The chapter 1 / chapter 2 monitoring and threshold-reperformance findings.
- Prior-period findings from any earlier mod-108 cycle, and from `mod-105` (ISO/IEC 42001) and `mod-107` (risk management) cycles that flowed into Clause 10.1.

In `mod-111` the findings-reporting chapter tests how new findings are framed for management response; here the audit is strictly about *closure of findings already in management's hands*.

The scope does include findings from Stage-1 and Stage-2 ISO/IEC 42001 audits (`mod-105` chapter 10), from internal audits (Clause 9.2), from management-review action items (Clause 9.3), and from notified-body surveillance (`mod-110`). All these flow into the Clause 10.1 corrective-action register; the follow-up tracker is the audit view of that register.

## The tracker as a document

The audit function's follow-up tracker is itself a document the auditor tests. The expected fields per row:

- **Finding ID** — stable, cross-engagement-unique identifier.
- **Source** — the engagement / audit / review in which the finding was raised (internal audit cycle, Stage-2, surveillance, management review, prior mod-108 engagement).
- **Finding title and description.**
- **Original severity** on the audit function's grading convention (minor / major / OFI, or equivalent; see `mod-105` chapter 2 on ISO/IEC 17021-1 grading and `mod-111` on findings-register discipline).
- **Original raised date.**
- **Criterion reference** — the clause, article, or policy the finding was raised against (ISO 42001 Clause X.Y, AI Act Article N, SR 11-7 section, NAIC Bulletin element, internal policy).
- **Affected AI system** or process.
- **Risk-register linkage** — the register row(s) the finding relates to.
- **Management response** — accepted, accepted-with-rationale, mitigated, transferred, disputed.
- **Corrective-action owner.**
- **Committed-closure date.**
- **Evidence-of-closure pointer.**
- **Audit re-performance status** — tested-closed, tested-open, deferred-to-next-cycle, superseded.
- **Repeat-indicator** — flags whether the finding re-occurs or is adjacent to prior findings.

A tracker without these fields is itself a documented-information defect; a tracker with fields unpopulated is a hygiene defect.

## The closure-evidence test

The sharp test. For a sampled set of "closed" findings the auditor:

1. **Pulls the committed corrective action** per the management response.
2. **Pulls the evidence** the responsible owner provided for closure.
3. **Reperforms the test** that would confirm closure — the same procedure that raised the original finding, applied to the current state.
4. **Confirms the effectiveness review** per Clause 10.1 step 4 (see chapter 3).
5. **Records closed-confirmed / closed-not-confirmed / partially-closed** status.

### Patterns the auditor should expect

- **Closed-by-memo.** The owner writes "resolved" in the tracker; no evidence pointer. The auditor records **closed-not-confirmed**.
- **Closed-at-first-fix.** The immediate mitigation shipped; the permanent fix was not pursued. The auditor records **partially-closed**.
- **Closed-at-mitigation-not-root-cause.** The symptom was addressed; the root cause remains and will recur.
- **Closed-at-documentation-only.** A policy was updated; no operational change verified.
- **Closed-under-superseded.** The finding was overtaken by a scope change (system retired, process re-authored); the auditor confirms the supersession is valid.

Any finding reported as closed where the auditor's reperformance fails is a **re-raised finding**, and the audit function escalates: the finding is restored to open with a new severity and a new owner, and the audit report calls out the closure integrity defect.

## The committed-closure-date test

For the open population the auditor tests closure-date discipline:

- **Count open findings past their committed-closure date.** A count above a small number is a program health signal.
- **Age distribution.** How long have open findings been open? Findings open for more than two review cycles are candidates for severity escalation or for an executive briefing.
- **Pattern by owner.** Are specific owners accumulating overdue findings? An owner-specific pattern is usually a resource or prioritisation finding, not a competence finding — the auditor's remediation suggestion goes to the owner's manager.
- **Pattern by severity.** Are majors being closed in reasonable time? A major open for a year is a confidence issue.
- **Pattern by criterion.** If prior-period findings against ISO 42001 Clause 9.1 are closing slowly and current-period findings continue to be raised against Clause 9.1, the organisation's Clause 9.1 is a systemic weakness.

## The repeat-finding pattern

Repeat findings are the single strongest audit-committee signal. The auditor identifies repeats by:

- **Exact-title repeat.** The current period raised a finding with the same title as a prior-period finding.
- **Criterion-and-system repeat.** The same criterion is cited against the same system within a 12-month window.
- **Root-cause repeat.** The underlying root cause recurs even if the surface finding differs (a shallow-RCA in Q1 closes; a shallow-RCA in Q3 opens against a different incident).
- **Owner-and-category repeat.** The same owner receives similar findings across engagements.

For every repeat the auditor opens a **systemic-issue finding** separate from the individual repeat, escalates to the audit committee, and recommends a root-cause remediation that is structurally different from the prior remediation. A pattern of repeats across multiple criteria is a culture / resourcing finding and typically surfaces at the audit-committee level.

## Status accuracy

The tracker's status field is not evidence; it is a claim. The auditor samples status entries and reperforms. Expected tests:

- For `tested-closed` entries, confirm the closure test was done and by whom; confirm the test's evidence is retained.
- For `tested-open` entries, confirm the latest test is dated; a `tested-open` status with a years-old test is a stale-test defect.
- For `deferred-to-next-cycle` entries, confirm the deferral was approved by the audit committee or equivalent and the rationale was recorded.
- For `superseded` entries, confirm the supersession is valid and the superseding change is pointed to.

An inaccurate status is a tracker-integrity finding; a pattern of inaccurate statuses is a governance finding on the audit function itself.

## Integration with GRC-for-AI platforms

If the organisation uses a GRC-for-AI platform (Credo AI, Holistic AI, Fairly AI, 2021.AI, Monitaur, OneTrust AI, ServiceNow IRM AI, Archer AI) for its action-tracking and risk-register, the follow-up tracker is likely an audit-specific export or workspace within that platform. The auditor tests:

- The export is reproducible — pulling the same data at a later date yields the same historical rows.
- The export includes evidence-pointer links that resolve.
- The platform's workflow supports the Clause 10.1 step-4 effectiveness-review field.
- The audit function's workspace is distinct from the first-line operational workspace (three-lines separation at the tooling level, consistent with chapter 6).

<!-- needs-research: confirm current GRC-for-AI vendor product capabilities at reading time; vendor features change rapidly -->

## Cross-cycle traceability

A follow-up tracker is only useful across cycles. The auditor confirms:

- The finding IDs are stable across audit cycles — a re-numbered scheme loses history.
- The closure evidence survives platform migration — tracker migrations that drop historical evidence are a continuity defect.
- The next engagement's planning (see `mod-103`) ingests the open-finding list as a risk-weighting input.
- The management-review inputs (ISO/IEC 42001 Clause 9.3.2) include the tracker status.

## The materiality roll-up

For the audit-committee reporting the auditor rolls up:

- **Total findings in the period** (prior-period open + current-period raised).
- **Closed in the period** with closure-confirmed vs. closed-not-confirmed split.
- **Open at period end** by severity, age, and owner.
- **Repeat findings** with systemic-issue count.
- **Materiality-weighted trend** — is the organisation accumulating or closing risk in net.

The roll-up is the audit-committee artefact that joins this chapter's workpaper to `mod-111`'s findings-reporting discipline.

## Common failure modes

- **Tracker with closure-by-memo.** Statuses marked closed without evidence pointers.
- **Overdue-majors ignored.** Majors sit past committed-closure date without escalation.
- **Supersession abused.** Findings quietly re-scoped out of relevance without audit-committee approval.
- **Repeat findings not identified.** The tracker does not flag repeats, treating each cycle's findings as fresh.
- **Status-field drift.** Statuses change in the platform without an audit trail.
- **Evidence-pointer rot.** Links to confluence pages, Jira tickets, or dashboards are dead.
- **Tracker not fed to Clause 9.3.** Management review does not see the aggregated status.
- **Platform-migration dropped-history.** Finding history pre-dates the current platform and is not accessible.
- **Follow-up only on majors.** Minors never retested; a cluster of unaddressed minors can indicate a systemic hygiene issue.
- **Audit function auditing its own tracker.** The chapter's work is itself self-review unless an independent reviewer or peer-audit reviews the audit function periodically (see `mod-101` on audit-function independence).

## Summary

- The follow-up-tracker audit is a reflexive piece of fieldwork: the audit function tests its own prior-period findings through to closure.
- The tracker is a document with expected fields — ID, source, severity, response, owner, closure-date, evidence pointer, reperformance status, repeat indicator.
- The closure-evidence test reperforms the original test against the current state; closed-by-memo entries become closed-not-confirmed.
- The committed-closure-date test flags overdue findings by age, severity, owner, and criterion.
- Repeat findings are the single sharpest audit-committee signal; each repeat is an additional systemic-issue finding.
- Status accuracy, cross-cycle traceability, and GRC-platform integration are tested as supporting disciplines.
- The materiality roll-up joins this chapter to `mod-111`'s findings-reporting discipline and to Clause 9.3 management-review inputs.
- The audit function's own tracker must itself be independently reviewed (`mod-101`); without that, the chapter's work is self-review.
