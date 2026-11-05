# Auditing Clause 9 — Monitoring, Internal Audit, Management Review

## Motivation

Clause 9 is where the AIMS looks at itself. **Clause 9.1** requires the organisation to monitor, measure, analyse, and evaluate its own AIMS performance. **Clause 9.2** requires an internal audit programme covering the full AIMS, carried out by auditors independent of the area audited. **Clause 9.3** requires a management review conducted by top management with specified inputs and outputs. In ISO MS terms, clause 9 is the organisation's own assurance function on itself — and from a certification-body perspective, the operation of clause 9 is a readiness condition for Stage-2 (there must have been at least one internal audit and one management review before the certification body will certify).

For the external auditor at Stage-2 and for the internal auditor at the next AIMS cycle, clause 9 is the hinge of the certification. A clause 9 that functions on paper only makes the rest of the AIMS unreliable — if the organisation does not know whether its own system is working, the certification body cannot rely on it either. This chapter is about testing that clause 9 operates, not just exists.

## Clause 9.1 — monitoring, measurement, analysis, and evaluation

**Requirement.** The organisation shall determine: what needs to be monitored and measured; the methods for monitoring, measurement, analysis, and evaluation (as applicable to ensure valid results); when the monitoring and measuring shall be performed; when the results from monitoring and measurement shall be analysed and evaluated; who shall analyse and evaluate these results. The organisation shall evaluate the AIMS performance and effectiveness. Documented information shall be retained.

**Audit test — the determinate-set walk.** Request the monitoring plan or equivalent. The plan must specify, for each monitoring target: *what*, *how*, *when* (measure), *when* (analyse), *who* (analyse/evaluate). Walk the plan item by item.

Expected monitoring targets for an AIMS:

- **AIMS objectives performance** (clause 6.2 objectives being tracked to target).
- **Annex A control effectiveness** (controls are operating, not just implemented).
- **AI-system-level operational metrics** (accuracy, fairness, robustness, latency, incident rates per system).
- **AI risk-register metrics** (counts of risks by band, residual risk trends, risk-treatment execution lag).
- **Impact-assessment currency** (percentage of in-scope systems with current impact assessments).
- **Change-management velocity and defect rates** (changes in the period, failures, rollbacks).
- **Incident-management metrics** (open incidents, MTTR, incidents by severity).
- **Supplier and GPAI-usage metrics** (vendor changes, notifications, policy enforcement).
- **Human-oversight metrics** (reviewer workload, override rates, bypass events).
- **Training and awareness metrics** (clause 7.2–7.3 reach).

**Audit test — the operation walk.** Sample several monitoring items. For each:

1. Verify data is collected per the method.
2. Verify the data is retained per retention policy.
3. Verify analysis happened per the cadence — look for the analysis artifact (report, review minute, decision record).
4. Verify evaluation produced a decision — an acceptance of current state, a corrective action, an adjustment to targets, or a management-review input.

**Common defects.**

- Dashboards exist, no analysis exists. (The "monitoring without analysis" finding — see chapter 7.)
- Analysis exists but no evaluation (no decision made against results).
- Metrics tracked that do not map to any objective or control (nice-to-know metrics that do not drive action).
- Retention gaps — monitoring data not held for the retention period the organisation itself specifies.

## Clause 9.2 — internal audit

**Requirement.** The organisation shall conduct internal audits at planned intervals to provide information on whether the AIMS: (a) conforms to the organisation's own requirements for its AIMS and to the requirements of this document; (b) is effectively implemented and maintained. The organisation shall: plan, establish, implement, and maintain an audit programme; define the audit criteria and scope for each audit; select auditors and conduct audits to ensure objectivity and impartiality; ensure audit results are reported to relevant management; retain documented information as evidence of the audit programme and audit results.

**The three questions the auditor asks about clause 9.2:**

### Does an internal audit programme exist?

Request the internal audit programme document. Verify it covers the full AIMS (clauses 4–10 and Annex A), schedules audits at risk-based intervals, specifies audit scope and criteria per audit, names auditors or the audit-selection method, and defines how results are reported.

A programme missing any of these is a finding. A programme that covers only Annex A controls and skips the clause-level requirements is a finding (the clauses are the AIMS; Annex A is only part of it).

### Is the programme being executed?

Verify internal audits have happened in the audit period. For a certification Stage-2, at least one full AIMS internal audit must have occurred before Stage-2; for a surveillance or recertification, continuous audit activity per the programme is expected.

Walk a sampled internal audit report. For each, verify:

- Audit criteria named (ISO/IEC 42001 clauses tested; Annex A controls tested; organisation's own procedures tested).
- Scope named (which AI systems, which processes, which time period).
- Procedures performed (interviews, document reviews, system tests).
- Findings graded (minors, majors, OFIs or equivalent under the organisation's own grading convention).
- Report delivered to management (audit committee, AIMS owner).
- Corrective actions tracked to closure.

### Are the auditors independent?

**Clause 9.2 requires selection of auditors and conduct of audits to ensure objectivity and impartiality.** For AIMS this is the sharp point of the clause. Three independence patterns:

- **Internal audit function reporting outside the AIMS owner.** The strongest shape. The CAE reports to the audit committee (or an equivalent body), independent of the second-line AIMS owner. See `mod-101` chapters 6–7 on the three lines model.
- **Internal audit function reporting to a different-but-still-management line.** Acceptable with caveats; the auditor confirms the specific roles of the internal auditors do not include designing or operating the AIMS they audit.
- **Internal audit function is the AIMS owner's team.** Independence failure — the second line cannot audit itself under ISO/IEC 42001 clause 9.2 and IIA Standards 2024.

The engagement auditor verifies the reporting line, interviews the internal audit lead to confirm independence, and examines any instance where the internal auditor assigned to a specific audit had a role in the audited area (a conflict that should be managed).

**Common defects.**

- No internal audit of record, only ad-hoc reviews not conducted as a formal audit. **Major**.
- Internal audit covering only Annex A controls, not the clause requirements. **Major** or **minor** depending on extent.
- Internal auditor assigned to audit their own team's work. Independence failure; **major**.
- Internal audit report without findings graded or without corrective-action tracking. **Minor**; if persistent across cycles, **major**.
- Internal audit programme not risk-based — a calendar schedule that visits every area once per cycle without regard to risk, missing high-risk areas within a cycle.

## Clause 9.3 — management review

**Requirement.** Top management shall review the organisation's AIMS, at planned intervals, to ensure its continuing suitability, adequacy, and effectiveness. The management review shall be planned and carried out taking into consideration specified inputs and producing specified outputs. Documented information shall be retained as evidence.

**Clause 9.3.2 inputs** (the standard specifies substantively; the auditor should walk the as-published text):

- Status of actions from previous management reviews.
- Changes in external and internal issues relevant to the AIMS.
- Changes in needs and expectations of interested parties.
- Information on AIMS performance, including trends in: nonconformities and corrective actions; monitoring and measurement results; audit results; AI objectives achievement; AI-system impact-assessment outcomes; relevant external changes (regulations, standards, incidents in the industry); feedback from interested parties.
- Opportunities for continual improvement.
- Risks and opportunities. <!-- needs-research: verify exact 9.3.2 input list against the as-published ISO/IEC 42001:2023 -->

**Clause 9.3.3 outputs** (the standard specifies):

- Opportunities for continual improvement.
- Any need for changes to the AIMS, including resource needs.

**Audit test — the input walk.** Request management-review meeting records (agenda, inputs pack, minutes, output decisions) for the audit period. For each required input element, verify:

- The input was tabled at the review (present in agenda or in the inputs pack).
- The input was substantively discussed (minutes reflect discussion, not boilerplate).
- The input led to a documented discussion or decision.

**Audit test — the output walk.** For each output decision, verify:

- The decision is recorded.
- The decision is tracked through to execution (new corrective action, new resource allocation, new objective, AIMS change).
- The next management review's input pack includes status on the decision.

**Audit test — top-management presence.** Clause 9.3 requires top management to conduct the review. "Top management" is the person or group of people who directs and controls the organisation at the highest level. For AIMS this is typically the executive committee or the board-level AI committee. A "management review" attended only by middle management is a finding against 9.3 and against 5.1 top-management commitment.

**Audit test — cadence.** "Planned intervals" is organisation-defined. Annual is the common minimum; quarterly is better practice for first-cycle AIMS or rapidly-changing contexts. The auditor confirms the cadence is defined and executed.

**Common defects.**

- Management review on agenda but not actually held. Finding.
- Management review held but without the required inputs. Finding against 9.3.2; grade depends on how many inputs are missing.
- Management review without top-management attendance. Finding against 9.3 and 5.1.
- Management review outputs without trace to execution. Finding against 9.3.3.
- Management review minutes that read "AI items noted" without substantive discussion. Pattern finding.

## The 9.1 ↔ 9.2 ↔ 9.3 triangle

The three sub-clauses of clause 9 are interdependent, and the auditor walks the triangle:

- **9.1 outputs feed 9.3 inputs.** Monitoring results, objectives performance, control effectiveness all land at management review.
- **9.2 outputs feed 9.3 inputs.** Internal audit findings are a 9.3.2 input.
- **9.3 outputs drive 9.1 adjustments.** Changes in monitoring, new metrics, new cadences.
- **9.3 outputs drive 9.2 programme.** The internal audit programme is adjusted on management-review direction.

A clause 9 that does not show the triangle operating is a clause 9 that is three siloed activities rather than a performance-evaluation system. The auditor's integrative test: pick a management review decision; trace it back through its 9.1/9.2 inputs; trace it forward to execution (likely in clause 10).

## Interaction with clause 10

Clause 9.2 and 9.3 both surface issues that feed clause 10 (improvement). Internal audit findings become nonconformities; management-review decisions become corrective actions or improvement initiatives. Chapter 9 picks up clause 10; the auditor's clause 9 workpaper leaves hooks for the clause 10 walk.

## Common failure modes

- **Monitoring without analysis.** The chronic AIMS failure; grades vary.
- **Internal audit covering only Annex A.** Missed the clause 4–10 scope.
- **Internal audit not independent.** Second line auditing itself.
- **Management review attended by middle management.** 9.3 + 5.1 finding.
- **Management review minutes that are skeleton minutes.** No substantive discussion; the review did not happen in substance even if it happened on the calendar.
- **No trace from clause 9 outputs to clause 10 actions.** The AIMS reflects but does not act.

## Summary

- Clause 9 is the AIMS looking at itself: monitoring and analysis (9.1), internal audit (9.2), management review (9.3).
- 9.1 is tested by walking the determinate set of monitoring targets, verifying data collection, analysis, evaluation, and decisions.
- 9.2 is tested by three questions: does a programme exist, is it being executed, and are the auditors independent? Independence is the sharpest point.
- 9.3 is tested by walking the required 9.3.2 inputs and 9.3.3 outputs, verifying top-management attendance, and tracing output decisions to execution.
- The 9.1 ↔ 9.2 ↔ 9.3 triangle must operate as a system; siloed sub-clauses are not clause 9.
- Clause 9 findings commonly aggregate — isolated minors against 9.1, 9.2, 9.3 often indicate a systemic performance-evaluation weakness.
- Clause 9 outputs feed clause 10 improvement (chapter 9).
