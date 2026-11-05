# exercise-03: Red-Team Program Sufficiency Audit

**Estimated effort:** 2 hours

## Objective

Audit an organisation's **red-team programme** against chapter 3's five-property frame: **charter**, **coverage matrix**, **tool portfolio**, **cadence**, and **finding-triage / closure**. Produce the auditor's opinion-forming workpaper, including the coverage-matrix reperformance, one spot-reproduced attack within the auditor's independence envelope, and a finding register with each finding cross-referenced to the organisation's risk register (chapter 2).

The auditor is testing sufficiency and reliability — *not* re-authoring the programme.

## Prerequisites

- Chapter [`03-auditing-the-red-team-program.md`](../03-auditing-the-red-team-program.md).
- Familiarity with the external taxonomies cited in the chapter: OWASP Top 10 for LLM Applications, OWASP Top 10 for ML, MITRE ATLAS, NIST AI 100-2, HarmBench.
- Prerequisite exposure to garak, PyRIT, Promptfoo, or Inspect sufficient to run a single-attack reperformance.
- `mod-104` chapter on specialist use (ISA 620) — you may invoke a specialist for a sensitive attack class.

## Scenario

**Stonehaven AI** is a mid-market enterprise-productivity SaaS that integrates a chat-assistant plus agentic tool-use into its customer platform. The system takes customer-service email threads as input, drafts replies, fetches internal knowledge-base articles via a retrieval tool, and (for authorised requests) files refund tickets via a backend API. Stonehaven has an internal "Red-Team and AI Trust" team of four, a quarterly external red-team engagement with a regional consultancy, and a quarterly report presented to the Trust & Safety Council. The red-team coverage matrix spreadsheet dates from 18 months ago and has not been refreshed. The last three quarterly reports are available.

You are the lead auditor on an ISAE 3000 limited-assurance engagement. The red-team sufficiency audit is a scope-defined chapter of the overall engagement.

Substitute the subject if needed: any published red-team report (frontier-lab system card red-team appendix, UK AISI evaluation report, DEF CON AI Village readout, a corporate security report that includes AI red-team content), or a synthetic scenario you invent with sufficient detail to drive the five-property tests.

## Requirements

1. **Charter test.** Pull the programme charter. Record whether each of chapter 3's seven elements is present (scope, authority, independence, reporting line, rules of engagement, deliverables, quality assurance). Missing elements are documentation findings.

2. **Coverage-matrix reperformance.** Request or reconstruct the coverage matrix. Produce a table with rows for each attack class and columns:
   - OWASP LLM Top 10 cross-tag (LLM01–LLM10).
   - OWASP ML Top 10 cross-tag (ML01–ML10, where applicable).
   - MITRE ATLAS technique ID.
   - NIST AI 100-2 attack family.
   - HarmBench behaviour (if applicable).
   - In-scope rationale (what harm-model row drives it).
   - Last-run date.
   - Owner.
   
   Flag silent omissions (OWASP LLM category with no row; any ATLAS technique that applies to the deployment but has no row).

3. **Tool-portfolio audit.** Confirm which tools the programme uses (garak, PyRIT, Promptfoo, Inspect, commercial vendors). For each tool record: version pin discipline, attack-suite version pin discipline, environment pin discipline, WORM-stored raw logs. One-tool programmes are a coverage finding.

4. **Cadence sampling.** Pull the declared cadence table. For at least three cadence rows (pre-release, periodic, trigger-based), pull the last three executed runs and confirm the cadence held. Cadence deviations are findings.

5. **Spot-reproduce one attack.** Within your independence envelope, pick one attack class the programme claims to have tested — prompt injection via a document is a safe choice for an AI-chat system — and run it using an open-source tool (garak or Promptfoo). Record: tool / version / suite / environment, attack, result, delta vs. the programme's claimed result. If you cannot access the target system, pick a similar public model and record the comparison explicitly.

6. **Finding-triage audit.** Pull the finding tracker (JIRA, GitHub issues, bespoke). Sample five open findings and five recently-closed findings. For each confirm: severity classification matches methodology, triage decision has a rationale, corrective-action link exists where mitigation was the decision, re-test evidence exists for closed findings.

7. **Evidence-of-execution audit.** For the last quarterly report, pull the raw run logs for at least two attack classes mentioned in the report. Compare. Missing raw logs, or summary-mention-without-underlying-log, is a serious finding.

8. **Cross-reference to the register.** For three red-team findings, trace into the chapter-2 register. If the finding is not registered and is above the register threshold per the organisation's methodology, open a trace finding.

9. **Author the finding register for the exercise** per chapter 2's finding shape: ID, severity, category (charter / coverage / tool / cadence / triage / evidence / trace), evidence pointer, recommended management response placeholder.

## Starter guidance

- The 18-month-old coverage matrix is a cadence finding by itself; expect to open it before the per-row coverage tests.
- When spot-reproducing an attack, you are not demonstrating attack skill — you are evidencing the reproducibility of the organisation's claim. A one-shot garak run with the right probe suite is sufficient.
- The OWASP LLM Top 10 numbering has changed across editions; cite the edition the organisation used *and* the current edition, and note the drift.
- A programme that uses only commercial vendor tools and has no open-source evidence stream is a reliability finding — the auditor cannot reperform without the vendor's cooperation.
- Where you invoke a specialist (ISA 620), record the specialist's identity, scope, and independence posture in the workpaper.
- Adversarial-payload discipline matters: store raw logs with access control; do not quote full jailbreak payloads in the published report.

## Acceptance criteria

The deliverable is accepted when:

- The charter is checked against all seven elements with evidence.
- The coverage matrix is reperformed as a table; silent omissions are explicitly flagged.
- The tool portfolio is inventoried with version-pin discipline per tool.
- Cadence sampling covers at least three cadence rows with last-three-run evidence each.
- One spot-reproduced attack is documented with tool / version / suite / result / delta.
- Finding-triage sampling covers five open and five closed findings with per-finding traceability.
- Evidence-of-execution is tested against at least two attack classes from a recent report.
- Three findings are cross-referenced into the chapter-2 register (or the absence is a trace finding).
- Every finding is classified for severity against the organisation's scale.
- Primary-source citations are present; `<!-- needs-research: ... -->` used for any under-pinned claim.

## Stretch goals

- Build a small **Promptfoo configuration** (YAML) that implements two or three attack classes against a public model, producing a rerunnable attack suite the organisation could adopt. (This is adjacent-to-authoring; keep it narrow.)
- Draft a **coverage-matrix refresh plan** — the one-page memo you would hand the red-team lead describing the cross-tag updates required for the current OWASP LLM Top 10 edition, the current ATLAS techniques, and the current NIST AI 100-2 revision.
- Produce an **external-engagement review** — for the last external red-team engagement, grade the independence posture, access terms, and publication state; compare to the auditor's independence framing from `mod-101`.
- Draft the **payload-handling policy** for your audit workpaper: WORM storage, access control, redaction rules for the published audit report. This is `mod-104` applied specifically to red-team evidence.
