# exercise-04: Incident Sample End-to-End Replay

**Estimated effort:** 3 hours

## Objective

Reperform a stratified sample of incidents **end-to-end** across the nine-step chain chapter 4 describes — detect → triage → RCA → post-mortem → regression-fixture → corrective-action closure → risk-register update → regulator notification (where applicable) → audit-committee reporting. Produce the one-row-per-incident, nine-cells-per-row reperformance workpaper, and a cross-incident pattern pass that elevates isolated cells into program-level findings.

This exercise pairs with exercise 03 — exercise 03 tests the program; this one tests the program on real incidents and shows where paper meets practice.

## Prerequisites

- Chapter [`04-reperforming-incidents-end-to-end.md`](../04-reperforming-incidents-end-to-end.md).
- Chapter [`03-auditing-the-incident-response-program.md`](../03-auditing-the-incident-response-program.md).
- `mod-104` on evidence discipline, ISA 500, ISA 530 sampling, ISA 620 specialist-use.
- `mod-107` chapter 2 for the risk-register traceback.

## Scenario

Use the same organisation you chose in exercise 03 — this exercise is the specific-case counterpart. If you are drilling without a stable scenario, pick one of:

**Scenario A — Chatbot-driven defamation incident.** A public-facing conversational assistant produced a defamatory statement about a named individual in a widely-screenshotted exchange. The incident surfaced externally (press / social media) before internal monitoring promoted it. The organisation is EU-based and the system is in Annex III scope.

**Scenario B — Agentic-system over-privileged tool call.** An agent deployed internally for IT-helpdesk automation issued a tool call outside its intended allow-list, resulting in unintended account-permission changes for ten employees. The incident was detected by SIEM and triaged into the SOC before being promoted to the AI-governance queue.

**Scenario C — Clinical-decision-support hallucination.** An SaMD assistant produced an incorrect drug-interaction warning in a non-binding clinical-reasoning output. Caught by a prescribing physician; retrospectively confirmed in traces. The organisation is FDA-regulated and the system has a PCCP.

## Requirements

1. **Pin the sample.** Record the incident population, the sampling frame, the stratification per chapter 4 (serious / monitoring-detected / user-reported / provider-reported / high-severity / cross-system / older / recent), and the sample size with ISA 530 justification. Minimum sample size: 8 incidents (or the full population if smaller, with that noted).

2. **Build the reperformance workpaper.** One row per sampled incident; nine columns per row — detect, triage, RCA, post-mortem, regression-fixture, corrective-action closure, risk-register update, regulator notification, audit-committee reporting. Each cell receives one of: **complete**, **partial**, **missing**, **inconsistent**, **not-applicable**. Each cell also receives an evidence-pointer cell beside it.

3. **Walk at least one incident in full worked detail.** Choose a sampled incident with at least three finding candidates and produce a written walk through all nine steps similar to the chapter-4 worked shape. The walk should name specific artefacts (dashboard IDs, trace IDs, commit SHAs, tracker IDs, filing receipts).

4. **Evidence-source failure-pattern log.** For the whole sample, record where you had evidence-access difficulty:
   - Trace-store retention gaps.
   - Redacted evidence.
   - Platform-migration discontinuities.
   - GRC-for-AI workflow closure-without-effectiveness-review.
   - Incident-management taxonomy gaps.
   Each pattern becomes a finding at the appropriate severity.

5. **Cross-incident pattern pass.** Step back from the per-incident rows and identify patterns:
   - Which step most often fails?
   - Which root-cause layer is most often shallow?
   - Which incident class never reports to the audit committee?
   - Article 73 determinations reviewed by regulatory counsel?
   - Monitoring-to-incident promotion rate (compare to exercise 01 monitoring population).
   Produce a short write-up — one paragraph per pattern — suitable for the audit-committee memo.

6. **Register-traceback audit.** For each sampled incident, verify a corresponding register update (or documented acceptance that no register change is warranted, with rationale). Produce a two-column list: incident ID → register row ID.

7. **Materiality-threshold audit-committee reporting test.** For each incident at or above the engagement's materiality threshold, verify appearance in the audit-committee pack. Incidents at the threshold that do not appear are a reporting-materiality finding.

8. **Findings register.** As in previous exercises. Add a *finding-shape* column classifying each finding as cell-level (one incident's one step failed) or pattern-level (the same step failed across multiple incidents).

9. **Workpaper hygiene check.** Confirm the workpaper is reperformable by a reviewing partner — every pointer resolves, every claim is dated, every ISA 620 specialist engagement is recorded.

## Starter guidance

- Reperformance is read-only on production evidence. Use exported data in an isolated workspace for any computation.
- A locked permissions wall during reperformance is a three-lines-independence finding (see chapter 6 and exercise 06); record it rather than talking it away.
- Stratification matters more than sample size — four well-chosen incidents produce stronger evidence than eight uniform ones.
- Cross-incident patterns are usually the final report's headline. Resist settling on cell-level minors.
- For the worked incident, write for a reviewing partner who was not in the room — name artefacts, name timestamps, name authorities.

## Acceptance criteria

The deliverable is accepted when:

- Sampling is pinned with stratification and ISA 530 justification.
- The reperformance workpaper has ≥ 8 incidents and all nine step-cells per incident populated with a status and an evidence pointer.
- At least one incident is walked in full worked detail.
- Evidence-source failure-pattern log contains at least three entries or documents the (unusual) finding of zero access-difficulty.
- Cross-incident pattern pass identifies ≥ 3 pattern-level findings, with program-level severity.
- Register-traceback is a complete two-column list for all sampled incidents.
- Audit-committee reporting materiality test is reperformed.
- Findings are classified cell-level vs. pattern-level.
- `<!-- needs-research: ... -->` is used where a factual claim cannot be verified from primary sources.

## Stretch goals

- Build a **small Python script** that takes the organisation's exported incident-management records and automatically populates the status-cell for step 5 (regression-fixture) by looking for a commit-SHA / eval-scenario / monitor-assertion cross-reference per incident.
- Draft the **audit-committee memo** summarising the cross-incident pattern findings, consistent with `mod-111`.
- Produce a **monitoring-to-incident promotion-rate** analysis comparing exercise 01's monitoring-breach population to this exercise's incident population, identifying the under-promoted class (if any).
- Author a **Clause 10.1 step-4 effectiveness-review schedule** generated from the sampled corrective-actions, flagging the specific dates on which the organisation is expected to produce effectiveness-review artefacts over the next twelve months.
