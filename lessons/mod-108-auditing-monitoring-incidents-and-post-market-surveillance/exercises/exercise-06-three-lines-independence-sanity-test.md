# exercise-06: Three-Lines Independence Sanity Test in Incident Response

**Estimated effort:** 1.5 hours

## Objective

Run the chapter-6 three-lines independence sanity test on the incident-response evidence trail. Produce a short, focused workpaper that answers: *does the third line see what the first and second lines see, is there a documented access protocol, are incidents being resolved outside the three-lines process, and does the SOC / DFIR interface hold?* Deliver findings against the IIA Three Lines Model (2020), the AI-auditor independence charter (`mod-101`), and the specific access-protocol implementation.

This is a short exercise by design — the three-lines test is a sanity check that runs alongside the deeper chapters 1–5 fieldwork, not a standalone programme.

## Prerequisites

- Chapter [`06-three-lines-independence-in-incident-response.md`](../06-three-lines-independence-in-incident-response.md).
- `mod-101` on audit-function independence and the three-lines-of-defense framing.
- Chapters 3 and 4 of this module (program-level and incident-level) for the evidence trail this test observes.

## Scenario

Reuse the organisation and incident sample from exercise 04. The independence test operates on the same incidents — the question is whether the audit function's access was equivalent to the first and second lines' access during each sampled incident.

## Requirements

1. **Pin the audit-function position.** Record how the internal audit function is positioned in the organisation: who the Chief Audit Executive (or equivalent) reports to; whether the audit function is independent of the AIMS owner; whether the audit charter names incident-response evidence access explicitly.

2. **Produce the evidence-parity matrix.** Rows are the sampled incidents from exercise 04. Columns are *first-line evidence available*, *second-line evidence available*, *third-line evidence available*, *delta note*. For each sampled incident verify whether:
   - The third line obtained the trace logs, run logs, model outputs, system telemetry at the same depth as the first line.
   - The third line received the full post-mortem, risk-register update, and regulator-facing filing content that the second line received.
   - The third line was notified within a documented window.
   The delta column flags any row where the third line's evidence is less, later, or more redacted than the first / second line's.

3. **Access-protocol audit.** Request the documented access protocol for internal audit to incident evidence (or confirm its absence). If present, test for the four elements chapter 6 enumerates — named evidence entitlement, retention horizon, independent custodian, exception mechanism. Confirm the protocol is executed by walking one incident from the exercise-04 sample.

4. **Out-of-process-resolution test.**
   - Compare monitoring-breach counts (exercise 01) to incident counts (exercise 03) for a shadow-triage signal.
   - Search public references (press, social media, regulator inquiry log if available) for AI incidents in the period; compare to the internal incident list.
   - Identify any privilege-asserted incidents and walk the privilege-scope documentation.
   - Identify any executive-escalation-only incidents and confirm closure through the governance council.
   Produce a short write-up with findings as appropriate.

5. **SOC / DFIR interface audit.** For any sampled incident that went through the SOC:
   - Was the AI-specific classification applied?
   - Was the AI-governance second line notified at the SOC-defined trigger?
   - Was the post-mortem co-authored across SOC and AI governance?
   - Were regulator notifications (Article 73 + GDPR 72h + sector-specific) coordinated?
   A SOC closure without AI-governance notification is an interface finding; the auditor refers out-of-scope SOC-runbook issues to the cybersecurity-audit function.

6. **Governance-council parity audit.** Confirm the governance council sees the sampled incidents and the audit function sees the council's discussion. Flag any materiality-threshold discrepancy between the council view and the audit view.

7. **Prior-period independence findings.** From the follow-up tracker (exercise 07), pull any prior-period independence findings and confirm closure. A repeat independence finding is a serious governance finding.

8. **Findings register.** Short — expect 2–6 findings. Column shape as in previous exercises. Classify each as access-protocol, evidence-parity, out-of-process, SOC-interface, governance-council, or prior-finding repeat.

## Starter guidance

- The chapter-6 independence tests are often *quiet* findings — process-maturity rather than hostile concealment. Describe plainly without accusatory tone; management response can be constructive.
- The access-protocol finding is usually the most consequential; without a protocol every other independence finding has deniable context ("we would have shared, if asked").
- The shadow-triage test using monitoring breach vs. incident counts can produce surprising numbers; reperform the count before stating a figure.
- The privilege test requires legal counsel consultation; coordinate with the engagement's legal reviewer.
- Keep the SOC-runbook out of scope. Record where you see runbook-depth issues and refer them.

## Acceptance criteria

The deliverable is accepted when:

- Audit-function position is recorded with CAE reporting line and charter reference.
- Evidence-parity matrix covers every sampled incident from exercise 04.
- Access-protocol audit tests all four protocol elements or documents the protocol's absence.
- Out-of-process-resolution test covers shadow-triage, public reference comparison, privilege-asserted incidents, and executive-escalation incidents.
- SOC / DFIR interface audit covers any incident that went through SOC.
- Governance-council parity audit produces a yes / no on each dimension.
- Prior-period independence findings have confirmed closure or a new repeat-finding entry.
- Findings are classified by the six categories above.
- `<!-- needs-research: ... -->` used where a factual claim cannot be verified.

## Stretch goals

- Author a **standing access-protocol proposal** the organisation could adopt, aligned to IIA Standard 1110 (Organisational Independence) and ISO/IEC 42001 Clause 9.2 auditor independence.
- Draft a **shadow-triage detection query** against the monitoring-platform API that the organisation could run as a standing control (an auditor-adjacent control, not an audit substitute).
- Produce a **cross-engagement independence trend** chart using the exercise-07 follow-up tracker, showing whether independence findings are declining or recurring over time.
- Write a short (≤ 500 words) note on the boundary between auditor advisory and auditor assurance in incident response, citing IIA Standards and recommending where the organisation's audit function should or should not accept in-the-moment advisory asks from the incident bridge.
