# Findings Register, Follow-Up Testing, and Closure

## Motivation

A finding is not closed when the report ships. It is closed when the corrective-action plan has been implemented, the auditor has tested the implementation, and the condition that originally raised the finding is no longer present. Between those two events sits the *findings-and-recommendations register* — the audit function's living record of open commitments, due dates, verifications, and closures. Without it, a finding becomes an orphan: the audit team moves on, the auditee's SME rotates out, next year's audit reopens the same gap and nobody realises it was supposed to have been fixed.

The IIA Global Internal Audit Standards obligate the internal audit function to monitor the disposition of engagement results. ISO/IEC 17021-1 clauses on handling nonconformities require the certification body to verify corrective actions and track them through the surveillance cycle. SR 11-7 expects model-risk-management functions to track model-validation findings through remediation. SOC 2 Type II reports examine the operating period, but readers across cycles look at trending in exceptions, implicitly expecting an issues tracker. EU AI Act Article 20 obligates providers to take corrective action and inform relevant parties when a system is found not to be in conformity — which means the audit function must be able to tell them a finding warrants Article 20 action, promptly.

This chapter walks the register's shape, the follow-up testing discipline, the closure memo, and the pattern analysis that feeds repeat-finding signal back into next-cycle planning and the Chief Audit Executive's enterprise view.

## The findings-and-recommendations register

### Schema

A usable register, regardless of tool (dedicated GRC platform, workflow in Jira, or spreadsheet), captures per finding:

- **Finding ID.** Stable, engagement-scoped (e.g., `AIMS-2026-S1-07` for the seventh Stage-2 finding of the 2026 AIMS audit).
- **Engagement reference.** Which engagement raised the finding; engagement date; audit team.
- **Scheme and classification.** The engagement shape and the classification under its vocabulary (major / minor / significant deficiency / Priority 1 / etc.).
- **CCCER text.** Linked to the engagement report.
- **Criterion citation.** Clause-level.
- **Workpaper trail.** Pointers to the evidence, cause-analysis, and materiality memos.
- **Management response.** Linked verbatim.
- **Corrective-action plan.** Role-owner (role, not individual), target date, deliverable, verification method.
- **Interim mitigation.** Description and effective date.
- **Status.** Open / In Progress / Ready for Verification / Verified-Closed / Re-opened / Risk-Accepted.
- **Risk-acceptance record.** If applicable: approver, date, risk-appetite reference, re-review schedule.
- **Repeat-finding flag.** Link to prior finding IDs if recurring.
- **Enterprise-risk tag.** Category for roll-up (e.g., pre-deployment-controls, data-governance, monitoring, incident-response, third-party, oversight).
- **Follow-up evidence.** Link to the follow-up workpaper and verification result.
- **Closure memo.** Link, once prepared.

### Register governance

- The register is **owned by the audit function**, not the auditee. Auditees who maintain their own issue-tracker see only their own view and tend to close findings prematurely; the audit function's register is the authoritative version.
- Status transitions require **auditor action** for "Ready for Verification" → "Verified-Closed." Auditee cannot close a finding; only the auditor can.
- "Risk-Accepted" transitions require **the appropriate approval level** (risk owner, Model Risk Committee, audit committee), captured in the register with evidence.
- The register is **reviewed quarterly at the audit committee** (or equivalent) with aging, status-change, and overdue-item tracking.
- Access to the register is **restricted** — audit function and designated recipients. Public distribution is not appropriate; the register often contains draft findings, disputes, and sensitive evidence.

## Follow-up testing

Follow-up is **its own engagement**, scoped and planned. It is not a drive-by.

### Planning

For each finding due in the period under review:

- Pull the CAP commitment from the register.
- Re-read the original finding, evidence workpaper, and cause-analysis workpaper.
- Design a test that would surface whether the CAP has been implemented **and** whether the original condition has been cured.
- Design a second test that would surface whether the CAP implementation was itself effective — not just performed.

Follow-up testing distinguishes three outcomes:

- **Implementation performed and effective.** The auditor's reperformance confirms the condition is no longer present. Close.
- **Implementation performed but not effective.** The CAP was executed in letter but the condition persists. Re-open with upgraded classification and a new CAP; consider whether the original cause analysis was wrong.
- **Implementation not performed or incomplete.** CAP deliverables absent or partial. Re-open; note the repeat pattern; escalate per chapter 3.

### Testing approaches

The follow-up test is often tighter than the original. Two useful approaches:

- **Reperformance of the original observation.** If the original finding was that fairness testing was not performed before deployment on a sampled set of models, the follow-up test samples a *new* set of recent deployments and checks that fairness testing was performed before each. This test surfaces operating effectiveness of the new control — not just its existence.
- **Reperformance of the specific CAP commitment.** If the CAP promised a blocking gate in the release pipeline, the follow-up test attempts to push a release to production without the required sign-off; the test is successful if the push is blocked.

For AI-specific findings:

- Monitor-based follow-up — pulling monitoring telemetry across the follow-up period to verify the monitoring control is operating.
- Model-change-log review — verifying that every change since the CAP implementation date triggered the new control.
- Human-oversight-log review — verifying that human review events are happening at the frequency and depth the CAP committed.

### Timing

Follow-up timing is:

- **Scheduled** — commonly per the IAF's annual plan, at the midpoint or end-point of the CAP timeline, or per ISO/IEC 17021-1 surveillance cycle (at least annually for AIMS).
- **Triggered** — by a management assertion that the CAP is complete and ready for verification.
- **Opportunistic** — a subsequent engagement that touches the same area naturally re-tests.

The worst pattern is CAP dates that slip quietly past the auditor's visibility. The register's quarterly aging report at the audit committee is the forcing function.

## The closure memo

The closure memo is a short workpaper that:

- References the finding ID and the CAP.
- States the follow-up test performed, the evidence obtained, and the result.
- Concludes closed / re-opened / risk-accepted.
- Is signed by the engagement preparer and the engagement reviewer per the firm's engagement-quality-review procedure.
- Is linked in the register.

A closure memo is not a victory lap. It is a short, dated, factual record so a future auditor, regulator, or litigator can see what happened.

### Example closure memo (abbreviated)

> **Closure Memo — Finding AIMS-2026-S1-11 (pre-deployment AI SIA gating)**
>
> Finding originally raised 2026-11-15; management CAP accepted the major-nonconformity classification and committed to implementing a blocking AIMS-Owner sign-off gate in the MLOps release pipeline by 2027-01-31.
>
> Follow-up testing performed 2027-02-18 → 2027-02-25. Procedures:
>
> 1. Pipeline configuration inspection — confirmed the "AIMS Owner sign-off" required field is now enforced as a precondition for the `promote-to-prod` action. Evidence: pipeline-config export [FUP-01], release-platform screenshot [FUP-02].
> 2. Negative test — attempted promotion of a dummy release (`test-dummy-v0.1`) from staging to prod without the AIMS Owner sign-off; promotion was blocked with the expected error message. Evidence: screencast [FUP-03].
> 3. Sampled the five in-scope releases that have occurred since 2027-01-31; all five show AIMS Owner sign-off recorded. Evidence: release-log export [FUP-04].
> 4. Interviewed AIMS Owner; confirmed the awareness of responsibility for sign-off and the governance review frequency. Interview notes [FUP-05].
>
> Retrospective SIA for the four pre-gate in-scope releases completed by 2026-11-30 as committed; reviewed and accepted as part of the AIMS management review, minutes [FUP-06].
>
> AIMS-PROC-004 §4.2 revised 2027-02-10 to specify the gating control; procedure reviewed [FUP-07].
>
> Conclusion: **Finding closed.** Recommendation: carry the control into the next surveillance cycle's control-walk-through for continued verification.
>
> Preparer: [auditor]. Reviewer: [senior]. Date: 2027-03-02.

## Risk acceptance — management declines to remediate

Not every finding is remediated. Management may determine that the cost or complexity of remediation outweighs the residual risk, and formally accept the risk. This is *their* decision, with the auditor's finding intact.

### What a defensible risk acceptance looks like

- **Written.** Risk-acceptance document naming the finding, the residual risk, the compensating controls (if any), and the acceptance rationale.
- **Signed at the appropriate level.** For a major-nonconformity / significant-deficiency / material-weakness equivalent, this is typically the risk owner at an executive level, often with committee concurrence (Model Risk Committee, audit committee).
- **Referenced to risk appetite.** The risk the organisation has declared tolerance for; without appetite reference, acceptance is ad-hoc.
- **Dated and term-limited.** "Risk accepted through 2027-12-31, with re-review at that date." Perpetual acceptances rot.
- **Visible to the next cycle.** The register carries the acceptance; the next cycle's audit planning accounts for it.

### What risk acceptance does not do

- **Does not close the finding** in the audit sense. It changes status to "Risk-Accepted," which is distinct from "Verified-Closed."
- **Does not override certification requirements.** An ISO major nonconformity cannot be risk-accepted around; the certificate cannot issue while it is open. A finding on a binding regulation cannot be risk-accepted around the regulation.
- **Does not bind third parties.** Downstream customers, regulators, and litigants are not bound by the organisation's internal acceptance.
- **Does not substitute for interim mitigation.** If a compensating control is claimed, the auditor tests it.

### What the auditor does when a risk acceptance is weak

- Documents the weakness and the auditor's disagreement in the register.
- Escalates per chapter 3 — audit committee and, if warranted, board.
- Treats the acceptance as a candidate re-raise in the next cycle; a pattern of risk-accepting findings instead of fixing them is itself a finding.

## Repeat findings — detection and response

### Detecting repeats

The register surfaces repeats through:

- **Direct text match** on condition, criterion, cause.
- **Enterprise-risk tag match** — multiple findings tagged "pre-deployment-controls" across cycles indicate a pattern even if specific instances differ.
- **Classification pattern** — repeated minor nonconformities in the same clause of ISO/IEC 42001 is the second indicator in ISO/IEC 17021-1 §9.4.9 for promotion to major.
- **CAP deadline-slip pattern** — a function that consistently misses CAP dates is itself a finding, independent of any specific missed CAP.

### Response

Repeats are not treated as fresh findings; they are treated as evidence that the original cause analysis was wrong or the CAP was inadequate. The response includes:

- **Re-opening with upgraded classification** per the engagement scheme (minor → major, deficiency → significant deficiency, Medium → High).
- **A new cause analysis** that goes deeper — the original cause stopped at a surface cause; the structural cause is deeper.
- **Escalation to the audit committee** with the repeat-pattern evidence.
- **Feed into the next-cycle risk assessment** — the function or process area carries elevated residual risk, affecting planning weight (chapter 3 of `mod-103`).

Three cycles in a row is a crisis signal — organisational-level pattern that warrants a specific audit committee session and, in regulated contexts, likely regulatory attention.

## Feeding the next-cycle plan

The register is an input to the next audit cycle's planning (chapter 2 of `mod-103`). Specifically:

- **Residual risk by area** — areas with open findings carry higher weight.
- **Follow-up planning** — CAPs due in the next cycle are scheduled for verification.
- **Repeat-finding flags** — elevate engagement priority.
- **Risk-acceptance review** — term-limited acceptances due to expire are flagged.
- **Resource implications** — chronic repeat-pattern areas may warrant deeper or more frequent audit engagement.

The Chief Audit Executive or engagement partner uses the register to answer the audit committee's standing question — "what is our aggregate residual risk, and is the function on a path to close it?"

## Coordinating with the Chief Audit Executive (or engagement partner)

The CAE is the function-wide owner of the audit function's independence, resourcing, and reporting. The register contributes to the CAE's job:

- **Function-level repeat-finding patterns** — e.g., across all engagements in the past year, how many touched data-governance and how many surfaced findings? If the pattern is systemic, the CAE's annual plan weight on data-governance rises.
- **Root-cause meta-analysis** — when multiple findings share underlying causes (e.g., "the release pipeline has no gates at all; every control that should sit there is a gap"), the CAE commissions a focused engagement on that root cause rather than continuing to raise instance findings.
- **Enterprise AI-risk picture** — the register's enterprise-risk tags aggregate into the enterprise-risk register maintained alongside ERM; the CAE's periodic report to the audit committee uses the aggregation.
- **Capacity signals** — if the register's aging is growing because verification capacity is insufficient, the CAE raises resource needs to the committee with the register as evidence.

For external audit (notified body, SOC auditor, SR 11-7 external validator), the partner plays an analogous role — tracking engagement-level patterns, communicating with the firm's AI practice leadership on the state of the client portfolio, informing firm methodology improvements.

## Interactions across engagement types

The multi-engagement AI audit organisation has several registers running in parallel:

- Internal audit's register.
- The certification body's non-conformity record for the AIMS audit.
- The SR 11-7 MRM function's findings tracker.
- The SOC 2 auditor's deviation log.
- The EU notified body's surveillance file.
- The LL144 historical-audit record (annual per the rule).

An AI auditor coordinating across these registers watches for:

- **Same underlying condition, different scheme classifications.** The ISO surveillance flags a minor nonconformity; the SR 11-7 validator flags a significant deficiency; the SOC 2 auditor flags an operating-effectiveness exception. Different schemes; same root; coordinated remediation possible.
- **Response conflicts.** A CAP the ISO auditor accepts as sufficient may not satisfy the SR 11-7 validator's cause bar; the organisation ends up with inconsistent remediation unless coordinated.
- **Cadence conflicts.** ISO surveillance is annual; SR 11-7 validation is on the bank's cycle; SOC 2 is on the examination period; LL144 is annual by rule. Coordinating evidence collection across them is the function-leader's work.
- **Independence boundaries.** The internal auditor cannot do the work the external attestor relies on; the external attestor may rely on internal audit's work only under specific standards (ISA 610 for financial-statement audits; AU-C 610; AT-C 105 reliance rules for attestation). Each boundary is specific.

## Metrics the audit committee expects on register health

Not required by any standard, but common practice:

- **Open findings by classification.** Major / minor / observation (or the engagement's vocabulary).
- **Average age of open findings** by classification.
- **Overdue CAPs count** — CAPs past the committed completion date.
- **Closure rate** — findings closed in the period / findings open at start.
- **Re-open rate** — findings re-opened after apparent closure.
- **Repeat-finding rate** — findings tagged as repeats.
- **Risk-acceptance count and aging.**

The auditor presents these without embellishment. Trends matter more than levels.

## Common failure modes

- **Register as spreadsheet only, maintained by one person.** Bus-factor one; prone to drift; not auditable across cycles.
- **Auditee closes findings.** Status transitions handed to the auditee; auditor loses the authoritative version.
- **Perpetual risk acceptance.** Findings sit in Risk-Accepted indefinitely; no re-review.
- **Follow-up is paper-only.** CAP documents reviewed; actual condition not re-tested. Auditor is satisfied the deliverable was produced, not that the gap was closed.
- **Follow-up conflated with the next full engagement.** The next engagement happens on its own calendar; follow-up on specific CAPs has its own calendar and may not line up.
- **Repeat patterns noted but not escalated.** The register surfaces them; no one acts.
- **Closure memo omitted.** Status flips to Verified-Closed with no memo; auditor cannot defend the closure later.
- **Cross-engagement misalignment.** Independent findings fixed independently; shared root causes never surface because registers are siloed.

## Interfaces to adjacent chapters

- Chapter 1 (CCCER) produces the finding content stored in the register.
- Chapter 2 (classification) produces the classification carried per scheme.
- Chapter 3 (management response) produces the CAP the register tracks.
- Chapter 4 (report shapes) produces the report-level outputs that aggregate what the register details.
- Chapter 5 (delivery) is where the register's state is tabled to the audit committee.
- Chapter 7 (regulator-facing submissions) picks up any filings that register state triggers.
- `mod-103` (risk-based planning) consumes the register in next-cycle planning.
- `mod-108` (monitoring, incidents, post-market surveillance) contributes signal that may cause findings to be re-opened.

## Summary

- The findings-and-recommendations register is the authoritative, audit-function-owned record of findings from issuance to closure; it captures per-finding ID, classification, CCCER text, workpaper trail, CAP, status, risk-acceptance detail, repeat-flag, and follow-up evidence.
- Status transitions to "Verified-Closed" require auditor action backed by a closure memo; the auditee cannot close a finding unilaterally.
- Follow-up testing is a planned engagement with its own evidence tests — reperformance of the original observation and reperformance of the specific CAP commitment — distinguishing performed-and-effective, performed-not-effective, and not-performed.
- Risk acceptance is a legitimate management decision when the finding is not regulatorily or certification-binding; it requires written, appropriate-level, appetite-referenced, dated, term-limited sign-off, is visible to the next cycle, and does not close the finding.
- Repeat findings surface through the register; the second indicator in ISO/IEC 17021-1 §9.4.9 and similar provisions in other schemes promote them in classification; three-cycle repeats are crisis-level signal.
- The register feeds next-cycle risk-based planning and the Chief Audit Executive's enterprise-view; function-level patterns inform resource and engagement weight shifts.
- Multi-engagement organisations carry several registers in parallel; the audit-function leader watches for shared-root findings, response conflicts, cadence conflicts, and independence boundaries across them.
- Register-health metrics for the audit committee — open counts by classification, aging, overdue, closure rate, re-open rate, repeat rate, risk-acceptance count — are common practice even where not standard-mandated.
