# Auditing Clause 10 — Nonconformity, Corrective Action, and Continual Improvement

## Motivation

Clause 10 is where the AIMS proves it can heal. Nonconformities arise from internal audits, from external audits, from incidents, from monitoring, from management review, from third-party reports. The AIMS must do more than log them — it must perform root-cause analysis, define and execute corrective actions, verify effectiveness, and feed the resulting learnings into continual improvement. A certification Stage-2 that finds nonconformity-handling broken will typically escalate the finding to **major** because an AIMS unable to correct itself cannot sustain its effectiveness across the three-year cycle.

Clause 10 is also where Stage-2 nonconformities the auditor is about to raise will land after the audit — the auditor is testing the very system that will have to process the findings being written. The circularity sharpens the attention: a clause 10 that was broken yesterday is a clause 10 that will fail to close today's findings.

## The structure of clause 10

In the as-published ISO/IEC 42001:2023: <!-- needs-research: confirm 10.1 vs 10.2 ordering in the as-published text; ISO/IEC 42001 departs from the default Annex SL ordering --> 

- **Clause 10.1 — continual improvement.** The organisation shall continually improve the suitability, adequacy, and effectiveness of the AIMS.
- **Clause 10.2 — nonconformity and corrective action.** When a nonconformity occurs, the organisation shall react, evaluate the need for action to eliminate the cause (root-cause analysis), implement any action needed, review the effectiveness of any corrective action taken, make changes to the AIMS if necessary, and retain documented information as evidence.

## Clause 10.2 — nonconformity and corrective action

**Requirement, expanded.** The standard requires six steps when a nonconformity occurs (10.2 a through e in ISO MS terms):

1. **React to the nonconformity** — take action to control and correct it; deal with the consequences.
2. **Evaluate the need for action to eliminate the cause** — root-cause analysis.
3. **Implement any action needed** — corrective action plan execution.
4. **Review the effectiveness of any corrective action taken** — closure verification.
5. **Make changes to the AIMS if necessary** — propagate the learning to procedures, controls, SoA, risk register.
6. **Retain documented information** — evidence of the nonconformity and all actions taken.

### Where nonconformities come from

The audit test starts by identifying the nonconformity sources the AIMS is subject to:

- Internal audit findings (clause 9.2).
- External audit findings (prior certification stage, surveillance, recertification).
- Incidents with AI-system involvement.
- Monitoring and analysis results that reveal AIMS failure (clause 9.1).
- Management-review findings (clause 9.3).
- Third-party-audit findings (SOC 2, ISO/IEC 27001, sector-regulator inspection).
- Complaints from interested parties.
- Supplier / vendor notifications.
- Regulator correspondence.

The AIMS must have a single register (or a defensible set of linked registers) capturing nonconformities from each source. A siloed set of registers (internal-audit tracker in one tool, incident tracker in another, complaints handled via helpdesk, with no consolidation) is a 10.2 finding because the organisation cannot see the whole picture.

### Audit test — population and sampling

Request the nonconformity register(s). Build the population: every nonconformity raised in the audit period and every nonconformity still open from prior periods. Stratify the sample across:

- **Source** (internal audit, external audit, incident, monitoring, management review, complaint, other).
- **Severity** (major, minor, OFI for CB audits; organisation's own grading for internal).
- **Age** (fresh, in-progress, closed within the period).
- **Life-cycle area** (which clause or control was the nonconformity against).

For each sampled entry, walk the six-step test.

### Audit test — the six-step walk per sample

For each sampled nonconformity:

1. **React.** Was there an immediate action to contain the nonconformity (or a documented decision that none was required)? For an incident-sourced nonconformity, is there a containment action? For an audit-finding-sourced nonconformity, is there an interim mitigation while the corrective action is prepared?
2. **Root-cause analysis.** Is there a documented RCA? The AIMS's RCA standard matters — the RCA should go beyond "the engineer forgot to update the datasheet" to "the pipeline does not enforce datasheet currency before model release; the last gate requires it only as a warning, not as a blocker". Shallow RCAs (one layer of why) are a pattern finding against 10.2.
3. **Corrective action plan.** Is there a CAP with: specific actions, named owner, due date, acceptance criteria for closure? Vague CAPs ("improve the process") are findings.
4. **Execution evidence.** Is there evidence the CAP was executed (code change, procedure update, training record, control implementation)?
5. **Effectiveness review.** After execution, is there evidence someone verified the corrective action worked and the nonconformity will not recur? This is the single step organisations most often skip. Closure by "action complete" is not effectiveness review; effectiveness review is "action complete *and* we have evidence the problem is actually fixed".
6. **AIMS change if necessary.** For systemic nonconformities, is there a corresponding AIMS change (procedure updated, SoA updated, risk register updated, Annex A control implementation revised)?

### Common defects

- **Register exists; CAPs missing or thin.** Finding against 10.2(c).
- **CAPs closed without effectiveness review.** Chronic finding; grade varies with pattern.
- **RCAs that stop at the first "why".** Finding against 10.2(b); OFI if occasional, minor if pattern, major if the lack of depth means recurrences actually happen in the period.
- **Nonconformities ageing beyond the organisation's own stated due date.** Compare the open-date to the current date; aged nonconformities beyond due dates with no justification is a finding.
- **Recurrence across cycles.** The same or similar nonconformity raised in cycle N–1 and again in cycle N indicates ineffective corrective action; strong signal for a 10.2(d) finding.
- **No propagation to AIMS changes.** Systemic nonconformity triggered a one-off fix but the procedure / SoA / risk register was not updated.

### The CAPs the auditor will create today

Every nonconformity the current Stage-2 raises will be submitted to the client for a corrective action plan. The auditor should set the standard at opening: the CAP must include RCA, action, owner, due date, closure evidence expectation. A CAP that reads "the AI team will address this" is not a CAP — it is a non-response. The certification body's CAP-acceptance review rejects non-responses; the audit leader prevents escalation by setting the standard early.

## Clause 10.1 — continual improvement

**Requirement.** The organisation shall continually improve the suitability, adequacy, and effectiveness of the AIMS.

**Audit test.** Clause 10.1 is tested by pattern evidence across the AIMS:

- AIMS objectives achieved over time, or evidence of revision when not achieved.
- Trend in nonconformities (counts, severity, recurrence rates).
- Trend in management-review outputs (increasing engagement, specific decisions, closed loops).
- Evidence of initiatives beyond nonconformity-driven correction — process improvements, new controls, new monitoring, adoption of new standards.
- Learning from external sources (updates incorporated from new ISO/IEC publications, regulator guidance, industry incidents, red-team research).

**Common defects.**

- **Continual improvement claimed with no evidence.** Policy states commitment; no artifact shows it operating.
- **Improvement limited to correction.** The AIMS only moves when something breaks; there is no proactive improvement.
- **Improvement initiatives without resource backing.** Initiatives noted in management-review minutes but no resource allocation, no execution evidence.

Clause 10.1 is harder to grade than 10.2 because it is pattern-based rather than discrete-event-based. The auditor's grading respects that: a lack of visible improvement across a first-year AIMS is not typically a major on its own; a recertification audit finding the AIMS has not meaningfully improved across three years is more likely to escalate.

## The 9.2 ↔ 10.2 loop

Internal audit findings feed clause 10.2 corrective action. The auditor walks the loop:

- Pull last internal-audit report findings.
- For each finding, trace to clause 10.2 handling.
- Check root-cause analysis, CAP, execution, effectiveness review, AIMS propagation.

If the last internal audit raised findings that remain open, un-RCA'd, or un-closed, the Stage-2 has two findings to raise: the original finding's underlying nonconformity (if still present) and the 10.2 process failure.

## Managing incidents as nonconformities

AI incidents (model failures causing harm, inappropriate outputs reaching users, guardrail bypasses, data breaches involving training data) are nonconformities against the AIMS even if they are also security incidents or regulatory-reporting events. The auditor tests whether:

- The incident is logged in the nonconformity register (or in a linked incident register the AIMS recognises).
- RCA occurred — including the AI-specific layers (not just "the system failed" but *why* the AIMS did not prevent or detect the failure).
- Corrective action addresses the AIMS gap, not just the technical defect.
- Mandatory reporting obligations were met (EU AI Act Article 73 for serious incidents from high-risk systems; FDA reporting for medical devices; relevant state reporting). <!-- needs-research: confirm current EU AI Act Article 73 reporting-timeline text and the categories of incident triggering reporting -->

Incidents handled technically (model rolled back, hotfix deployed, user communication sent) without AIMS-level RCA are the pattern the auditor is watching for.

## Common failure modes

- **Siloed registers.** Finding against 10.2 — the AIMS cannot see nonconformities as a whole.
- **Shallow RCA.** Covered above.
- **Closure without effectiveness review.** Covered above.
- **Recurrence across cycles.** Signal of ineffective corrective action; pursue.
- **CAPs without resources.** CAPs that assume unfunded work rarely execute; patterns of overdue CAPs with no resource allocation are findings.
- **Improvement limited to correction.** 10.1 finding.
- **Audit findings not fed into 10.2.** The 9.2 ↔ 10.2 loop is broken; serious signal of AIMS dysfunction.
- **Incidents handled outside the AIMS.** Covered above.

## Summary

- Clause 10 is where the AIMS heals. 10.2 handles nonconformities with six steps — react, RCA, CAP, execute, effectiveness review, AIMS change. 10.1 drives continual improvement beyond nonconformity-triggered correction.
- The audit samples across nonconformity sources (internal audit, external audit, incidents, monitoring, management review, complaints, suppliers, regulators) and walks each sample through the six-step test.
- Common findings cluster around closure-without-effectiveness-review, shallow RCA, aged CAPs, and recurrence across cycles.
- Incidents are nonconformities against the AIMS; AIMS-level RCA is required even when the technical fix is done.
- Clause 10.1 continual improvement is pattern-based; the audit respects pattern grading but escalates when a recertification cycle shows no meaningful improvement.
- The 9.2 ↔ 10.2 loop — internal-audit findings feeding corrective action — is a primary audit walk; broken loops signal systemic AIMS dysfunction.
