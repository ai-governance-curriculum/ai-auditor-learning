# Three-Lines Independence in Incident Response

## Motivation

`mod-101` installed the three-lines-of-defense framing for the AI-audit function as a whole. This chapter applies that framing specifically to incident response. The incident-response flow is where three-lines discipline most often quietly erodes: an incident surfaces, the organisation forms a crisis team to resolve it, and the crisis team ends up containing members of the first line (owners of the system), the second line (risk, compliance, governance), and the third line (internal audit) — all working the same problem. That is operationally sensible in the moment. It is independence-destroying over time.

The auditor's job in this chapter is to confirm that for the audited period, the third line (internal audit function) remained independent during incident response — saw the same evidence that SecOps and the governance council saw, was not drafted into resolution, and tested the interface between lines rather than the first-line SOC runbook.

The chapter also fixes the *deferral boundary*: SOC-side cybersecurity incident handling is the specialty of SecOps / DFIR (`cybersecurity-engineer` and incident-response specialists). The AI auditor does not test the SOC runbook. The AI auditor tests whether the AI-specific events flow into, through, and out of the SOC appropriately, and whether the three-lines boundary holds.

## The three-lines model restated for incident response

In the IIA Three Lines Model (2020):

- **First line** — operational management of the AI systems: the product / platform / ML teams that own the deployed systems. They detect, triage, mitigate, and remediate.
- **Second line** — risk, compliance, legal, AI governance, and (in AI contexts) the AIMS owner. They oversee the first line's incident handling, maintain the register, run the corrective-action loop, and own regulator-facing reporting.
- **Third line** — internal audit. Provides independent assurance to the audit committee that the first and second lines operate as claimed.

In incident response the roles can collapse into a single "incident channel" with everyone in it. The auditor tests whether the formal roles persisted across the incident evidence trail.

## What the auditor sees vs. what the first and second lines see

The sharpest independence test is **evidence parity**: the auditor should see the same evidence the first and second lines see — not less, not later, not redacted differently.

### The parity test

For a sampled incident (reused from the chapter 4 sample), the auditor obtains:

- **First-line evidence** — trace logs, model outputs, system telemetry, deployment-pipeline logs, SRE artefacts.
- **Second-line evidence** — AI-governance review notes, risk-register updates, compliance opinions, legal communications relating to the incident (with privilege-preserving protocols where applicable).
- **Third-line evidence** — the artefacts delivered to internal audit during the incident, if any.

The three sets should be substantially overlapping. Patterns to flag:

- **Third line excluded from first-line evidence.** Trace data and log data behind a permissions wall that internal audit cannot clear without a request routed through the first line.
- **Third line receiving redacted post-mortems.** The governance council sees a full version; the audit function sees a sanitised version.
- **Third line notified late.** The incident reached closure before internal audit had an opportunity to observe.
- **Third line notified only for "material" incidents.** The materiality determination is made by the second line without a defined trigger that forces third-line notification.

A pattern of any of the above is an independence finding — not necessarily a hostile-concealment finding (often it is simple process immaturity), but a finding against the three-lines charter the organisation has nominally adopted.

### The access-protocol test

The auditor confirms there is a documented access protocol for internal audit to incident evidence. The protocol:

- Names what evidence the third line is entitled to see.
- Names the retention horizon that applies (the third line's review may lag the incident by months).
- Names who serves the evidence to the third line (not the first line; an independent custodian role or a GRC platform with audit-only access).
- Names the exceptions (legal privilege, ongoing law-enforcement matters) and the review mechanism for exceptions.

A program with no access protocol is a program where the third line's access is informal and therefore potentially negotiable; the auditor records that as a governance-charter finding.

### The specialist-use boundary

Where the auditor relies on an expert for incident evaluation (ISA 620 — Using the Work of an Auditor's Expert), the expert must be independent of the audited incident. Patterns to avoid:

- The expert is also the second-line author of the incident's RCA.
- The expert reports to the same manager as the incident's triage owner.
- The expert's scope of work has been drafted by the first line.

The auditor records the specialist's engagement letter, independence declaration, and scope.

## Resolution-outside-the-three-lines-process

A failure mode the chapter highlights as its own category: **incidents resolved outside the formal three-lines process**. Patterns:

- **Shadow-triage.** An on-call engineer identifies a problem, ships a mitigation, and never opens an incident record. The monitoring breach is "resolved by auto-rollback." No post-mortem. No register update. No third-line visibility.
- **PR-first resolution.** An incident becomes public before the organisation's internal process opens it. The organisation's response is driven by communications rather than the Clause 10.1 loop.
- **Legal-privilege-locked incidents.** Legal counsel asserts privilege over the incident analysis, denying the second and third lines access. In some jurisdictions the privilege is valid and the auditor records the scope limitation; in others the assertion is over-broad and the auditor flags it.
- **Executive-escalation-only incidents.** The incident is managed in a C-suite thread and bypasses the governance council.
- **Third-party-handled incidents.** The vendor (upstream GPAI provider, hosted-model provider) handles the incident upstream; the organisation receives a summary but no reperformable evidence (see `mod-109` for the third-party audit shape).

The auditor's test for out-of-process resolution:

- Compare the population of monitoring breaches (chapter 1) to the population of incidents (chapter 3). Significant gaps suggest shadow-triage.
- Compare external references to AI incidents (press, regulator inquiry, user complaints published publicly) to the internal incident list. Externally-visible incidents without an internal record are evidence of PR-first resolution.
- Walk the privilege-asserted incidents with legal counsel (within the scope of the engagement letter). Confirm the privilege scope is documented and defensible.
- Confirm executive-escalation incidents are reflected in the governance-council minutes at closure.

## Boundary with SecOps / DFIR

The AI auditor does **not** test the SOC runbook. This boundary is explicit in the engagement letter (see `mod-103`).

**In scope for the AI auditor:**

- Whether AI-specific incidents promote into the SOC's incident intake with the correct classification.
- Whether the SOC's incident classification taxonomy supports AI-specific types (prompt injection, model-output harm, training-data leak, guardrail evasion) — a SOC whose taxonomy is strictly network-security and malware is an AI-incident recognition gap.
- Whether the SOC's handoff back to the AI-governance process is operational.
- Whether the SOC's retention and documentation satisfies the AI-regulatory obligations (Article 72 retention, Article 19 logs retention) in addition to its security-driven retention.
- Whether the SOC's regulator-reporting channels (GDPR 72h for personal-data breach, NIS2, sector-specific notifications) interoperate with the AI-governance channels (Article 73, MDR, NAIC).

**Out of scope for the AI auditor:**

- Internal SOC runbook execution — forensic evidence handling, containment playbooks, threat-actor attribution.
- SOC's compliance against its own ISO/IEC 27001 Annex A.16 / 5.26 incident-management controls — tested by the ISO 27001 auditor.
- Specific IR-plan content and tabletop-exercise effectiveness — tested by the organisation's cybersecurity audit function.

The auditor documents the boundary in the workpaper and refers the out-of-scope items to the SecOps / DFIR audit track when a finding is identified at the handoff.

### The interface test

For a sampled AI-specific incident that *did* go through the SOC, the auditor verifies:

- The incident was classified with AI-specific tags in the SOC's intake.
- The AI-specific runbook (if the organisation has one) was invoked.
- The AI-governance second line was notified at the SOC-defined trigger point.
- The post-mortem includes both SOC-side and AI-governance-side authorship.
- The regulator notifications under both regimes (AI Act Article 73, GDPR, sector-specific) are coordinated — not duplicated or contradictory.

A sampled incident where the SOC closed the case without notifying AI governance is an interface failure the auditor records against the handoff process, not against the SOC.

## The governance-council parity test

The auditor confirms the governance council sees what the audit function sees:

- Governance-council minutes reference the same incidents the audit function has sampled.
- The council's materiality threshold for discussion is documented and executed.
- Council decisions on incidents are recorded and traceable.
- Council membership did not include only the first line (the board-AI-committee-chaired-by-the-CTO pattern is a governance-charter finding).

A council that discusses incidents but does not surface them to the audit function is still an evidence-parity defect — the auditor's workpaper notes whether the council's view was fed to internal audit within a documented window.

## Prior-period independence findings as pattern

Independence findings often repeat. Chapter 7's follow-up-tracker audit picks up prior-period findings on independence and tests closure. The auditor in this chapter reads the prior-period independence findings as input:

- Were prior independence findings closed? See chapter 7.
- Did the remediation address the finding or only its symptom? A finding on "audit function had late notification" closed by "we added audit to the incident Slack channel" is a symptomatic fix — the underlying charter and access protocol issues may remain.
- Did a prior finding on one incident surface again in this period? A repeat is a serious governance finding.

## Common failure modes

- **Third line in the war-room.** The internal auditor participates in resolution and loses independence; subsequent testing is self-review.
- **Access-by-request-only.** The third line has no standing access to incident evidence; every piece requires a first-line approval.
- **Shadow-triage.** Monitoring breaches resolved without an incident record.
- **PR-first resolution.** External visibility drives the response; the internal process is bypassed.
- **Privilege over-assertion.** Legal privilege used to withhold incident analysis from second and third lines in jurisdictions where the scope is over-broad.
- **Executive-escalation-only incidents.** C-suite threads without governance-council handoff.
- **SOC taxonomy without AI-specific tags.** AI-specific incidents classified as generic security tickets and lost in the taxonomy.
- **SOC closure without AI-governance notification.** The AI-governance second line is not notified of AI-relevant SOC incidents.
- **Governance council not independent.** Council chaired by a first-line executive with no outside member.
- **Materiality determination held by the second line.** Second-line discretion over what reaches the third line is itself an independence defect.

## Summary

- Three-lines independence in incident response is tested by evidence parity: the third line should see what the first and second lines see.
- The access-protocol test confirms the third line has documented standing access to incident evidence.
- The out-of-process-resolution test compares monitoring-breach, incident, and externally-visible-incident populations.
- The boundary with SecOps / DFIR is explicit: the AI auditor tests the interface, not the SOC runbook.
- The governance-council parity test confirms the council's incident discussion flows back to the audit function.
- Prior-period independence findings are read as input and their closure tested in chapter 7.
- Common failure modes concentrate at access, materiality discretion, and shadow-triage — process-maturity issues more than hostile-concealment ones.
- Chapter 7 closes the module with the follow-up-tracker audit on the AI Auditor's own prior-period findings.
