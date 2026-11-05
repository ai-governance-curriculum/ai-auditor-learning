# Reperforming an Incident Sample End-to-End

## Motivation

Chapter 3 tested the program as a program. This chapter tests the program on *specific incidents*. The program-level audit tells the auditor whether the policy, the taxonomy, and the roles look complete on paper; the end-to-end reperformance tells the auditor whether the program actually produced an evidenced trace for the incidents it owns.

The target is a canonical nine-step chain:

```
detect → triage → RCA → post-mortem → regression-fixture → corrective-action
    closure → risk-register update → (where applicable) regulator notification
    → audit-committee reporting
```

For each sampled incident the auditor reconstructs this chain from the organisation's evidence: trace store, run logs, GRC-for-AI platform, incident-management system (ServiceNow / Jira / Opsgenie / PagerDuty), post-mortem repository, Article 73 filings, audit-committee packs. The output is a workpaper with one row per sampled incident, one column per step, and a status / evidence-pointer / defect-code per cell.

This is the single most consequential piece of fieldwork in the module. A program that looks complete at the policy level but fails end-to-end reperformance on real incidents is a program the audit committee and the certification body need to hear about.

## Sample selection

The sample is selected under `mod-104` discipline — ISA 530 if under IAASB; AU-C 530 if under AICPA — and the selection itself is documented in the workpaper.

**Population.** The population is the set of incidents the organisation triaged in the audit period. The auditor obtains the full population list before sampling; if the organisation's list is incomplete (e.g. cannot account for all monitoring breaches that should have promoted to triage), that is a population-completeness finding and the sample selection proceeds against the best-available list with the gap noted.

**Stratification.** The sample must include:

- At least one **Article 73 serious-incident** candidate (or a documented statement that none occurred in the period, verified against the incident log).
- At least one **monitoring-detected** incident (promoted from a chapter-1 / chapter-2 breach).
- At least one **user-reported** incident.
- At least one **upstream-provider-reported** incident (GPAI-provider notification, vendor-guardrail false-negative report) — if any exist in the period.
- At least one **high-severity** incident per the organisation's scale.
- At least one **cross-system** incident affecting multiple AI systems in the inventory.
- At least one **older** incident (opened at the start of the period) to test the full closure chain.
- At least one **recent** incident (opened late in the period) to test triage and immediate-mitigation discipline.

**Sample size.** Determined by the risk-weighted stratification and the materiality the engagement letter (see `mod-103`) commits to. A common starting point is 8–12 incidents for a mid-maturity program; larger samples where the population is large or the risk is high. The auditor documents the sample-size rationale; a sample that fails `mod-104` justification standards is itself a finding on the audit's own evidence sufficiency.

**Random vs. judgement.** A hybrid is common: random within each stratum, with at least one judgementally-selected high-profile incident (e.g. an incident referenced in management-review minutes, in the audit committee pack, or in press coverage). The auditor records which rows are random and which are judgement.

## The reperformance workpaper

The workpaper is a single table — one row per incident, one column per step, with evidence pointers and status.

| Step | What the auditor verifies | Primary evidence source | Expected artefact |
|------|---------------------------|-------------------------|-------------------|
| 1. Detect | Signal arose at the stated time; signal is the right signal | Monitoring dashboard / alert feed / user ticket / provider notification | Alert record / ticket with timestamp |
| 2. Triage | Named owner triaged within time-to-triage; rubric applied; Article 73 applicability determined | Incident-management system | Triage decision record with rationale |
| 3. RCA | Multi-layer root cause; counterfactual; evidence cited | Post-mortem repository / RCA artefact | RCA document with causal chain |
| 4. Post-mortem | Standard structure; signed off; regulator-shareable section | Post-mortem repository | Post-mortem document |
| 5. Regression-fixture | Test added; eval added; monitor added | Code repo (test diff); eval-harness config (Inspect / Promptfoo / HELM); monitoring plan (chapter 1) | Three fixture pointers |
| 6. Corrective-action closure | Clause 10.1 loop walked including effectiveness review | GRC-for-AI platform (e.g. Credo AI, Holistic AI, Fairly AI, 2021.AI, Monitaur, OneTrust, ServiceNow IRM), Clause 10.1 tracker | Action record with closed status *and* effectiveness-review note |
| 7. Risk-register update | Row updated with breach, residual-risk re-scored if warranted | Risk register (chapter 2 of `mod-107`) | Register entry with incident-ID link |
| 8. Regulator notification | If applicable, filing made in-window with matching facts | Article 73 / MDR / NAIC filing log | Filing receipt or submission confirmation |
| 9. Audit-committee reporting | Appears in the pack above the materiality threshold | Audit-committee pack | Pack excerpt with the incident named |

Each cell receives one of: **complete** (evidence found, matches expectation), **partial** (evidence found, partial match), **missing** (evidence absent), **inconsistent** (evidence found, contradicts another step), **not-applicable** (step does not apply, with rationale).

## Walking a single incident — worked shape

To make the pattern concrete, the following is the shape of the workpaper row for a hypothetical incident. The organisation-specific identifiers are illustrative; no specific real incident is asserted.

**Incident IDX-2026-014 — PII leak in support-assistant output, detected via monitoring.**

| Step | Finding row |
|------|-------------|
| 1. Detect | **Complete.** Alert `pii.leak.rate` crossed 3× baseline at 2026-04-07T14:18Z (monitoring plan v3, signal 11). Alert routed to `#ai-incidents-primary` Slack rotation; on-call acknowledged at 14:22Z. |
| 2. Triage | **Complete.** Triage owner at 14:31Z opened IRM record IDX-2026-014, graded Sev-2, promoted to incident, applied Article 73 applicability test — not applicable (no serious harm per Article 3 criteria), rationale recorded. |
| 3. RCA | **Partial.** 5-Whys recorded; counterfactual recorded; evidence pointers to traces and deployed-prompt-template history. Organisation-level cause ("review gate skipped on urgent release") noted but not examined further. *Finding candidate: shallow RCA at organisational layer.* |
| 4. Post-mortem | **Complete.** Published 2026-04-14 in the post-mortem repo; standard structure present; signed by Head of AI Platform and VP Engineering. |
| 5. Regression-fixture | **Partial.** Unit test added in commit `d1a8f2…`; Promptfoo eval scenario added. *Monitor assertion* in the plan was *not* updated to tighten the baseline on `pii.leak.rate`. Finding candidate: regression-fixture incomplete at monitor layer. |
| 6. Corrective-action closure | **Partial.** Primary action closed 2026-05-02 in Credo AI. Effectiveness review scheduled for 2026-06-01; as of audit date 2026-10-14, no effectiveness-review artefact recorded. *Finding candidate: Clause 10.1 step-4 missing.* |
| 7. Risk-register update | **Complete.** Register row R-012 ("PII exfiltration via assistant output") refreshed; residual-risk score unchanged (within appetite) with signed rationale. |
| 8. Regulator notification | **N/A.** Article 73 not applicable per step-2 determination; MDR / SR 11-7 not applicable to this system. |
| 9. Audit-committee reporting | **Missing.** Incident Sev-2; engagement materiality threshold is Sev-2; incident does not appear in the Q2 pack. *Finding candidate: materiality-threshold breach of audit-committee reporting.* |

Three finding candidates from a single incident is typical. The pattern across the sample is what the audit report ultimately writes to — one shallow-RCA, one fixture-incomplete, one effectiveness-review-missing, one materiality-breach is four isolated minors; three shallow-RCAs across four sampled incidents is a program-level major.

## Evidence sources and their failure patterns

**Trace store.** The authoritative record of per-request inputs, outputs, metadata, and tool-call traces. Common tools: Langfuse, LangSmith, Arize Phoenix, W&B Weave, DataDog LLM Observability, OpenTelemetry-based pipelines, in-house trace platforms. Expected failures:

- Retention window too short for the period audited.
- PII-redaction in traces too aggressive to permit the RCA reperformance (an auditor may need to request de-redacted evidence under a documented protocol).
- Trace-schema change mid-period breaks reperformance for earlier events.

**Run logs.** Model-serving logs, deployment-pipeline logs, training-run logs (for retrain-driven incidents). Expected failures:

- Log retention shorter than incident-closure cadence.
- Log-aggregation discontinuities when platforms migrated during the period.
- Debug-only fields stripped before retention.

**GRC-for-AI platform.** Credo AI, Holistic AI, Fairly AI, 2021.AI, Monitaur, OneTrust AI governance, ServiceNow IRM AI modules. <!-- needs-research: confirm current GRC-for-AI vendor list and any 2025–2026 consolidation / rebranding at reading time --> Expected failures:

- Platform captures the policy and the record but not the regression-fixture evidence pointer.
- Platform workflow allows closure without an effectiveness-review field.
- Platform permissions block the auditor's independent access (chapter 6 three-lines test).

**Incident-management system.** Jira / ServiceNow / Opsgenie / PagerDuty. Expected failures:

- Non-AI incidents and AI incidents share a project without a taxonomy field — pattern analysis impossible.
- SLA metrics on time-to-triage missing for AI-specific queue.

**Post-mortem repository.** Confluence / Notion / dedicated post-mortem tool. Expected failures:

- Post-mortem written but not published beyond the authoring team.
- Post-mortem revised after the regulator filing without a revision log.

## Trace-reperformance for monitoring-detected incidents

For incidents that originated from a monitoring breach (chapter 1 / chapter 2), the auditor reperforms the trace back:

1. Pull the raw monitoring data for the detection window.
2. Confirm the alert fired at the right time against the plan's threshold.
3. Pull the per-request traces for the window.
4. Confirm the traces show the harm pattern described in the post-mortem.
5. Confirm the RCA references specific trace IDs; sample a trace ID and verify it exists.

A post-mortem that references "elevated hallucination rate during the window" without a specific set of trace IDs is an RCA-evidence-pointer defect and makes the reperformance impossible.

## The cross-incident pattern pass

After filling the workpaper for all sampled incidents, the auditor steps back and looks at the pattern:

- **Which step most often fails?** If regression-fixture-at-monitor fails on 5 of 8 sampled incidents, that is a program-level major finding, not eight isolated minors.
- **Which root-cause layer is most often shallow?** A pattern of "model-layer causes only" across many incidents is a program-level training / specialist-competence finding.
- **Which incident class never reports to the audit committee?** A pattern of under-reporting in a specific class (e.g. fairness-related incidents never surface at board level) is a governance finding.
- **Which Article 73 determinations were made by non-regulatory-counsel-informed triagers?** A pattern finding on regulatory-reporting authority.
- **How many incidents did not promote from monitoring breaches?** Comparing monitoring-breach counts (chapter 1) to incident counts tests the triage-promotion bar. A monitoring-rich / incident-poor pattern suggests under-triage.

The cross-incident pass is often where the most consequential findings come from. The individual incidents reveal cells; the pattern across cells reveals program-level issues.

## Workpaper hygiene

The reperformance workpaper is the auditor's primary evidence for this chapter. It must satisfy `mod-104` evidence discipline:

- Source of each evidence pointer stated.
- Retrieval timestamp recorded.
- Hash / version / revision captured where applicable.
- Materiality decision for each finding candidate recorded.
- Specialist contributions (ISA 620) separately recorded where used.
- Workpaper stored in WORM audit storage per the engagement's retention policy.

A beautiful workpaper that is not reperformable by a reviewing partner is a workpaper the firm's quality-control would reject; the auditor builds for review from the start.

## Interface to subsequent chapters

- **Chapter 5 (Article 72 report audit)** — the reperformed incidents must match what the Article 72 Post-Market Monitoring Report describes. A sampled serious-incident that the Article 72 report fails to describe is an Article 72 reporting defect.
- **Chapter 6 (three-lines independence)** — reperformance friction (locked permissions, redacted evidence, delayed access) is a three-lines independence signal the auditor records.
- **Chapter 7 (follow-up tracker)** — step-6 corrective-action closure findings feed the prior-period tracker audit in the next cycle.
- **`mod-111` (findings reporting)** — the reperformance workpaper is one of the documents that most directly drives the Stage-2 findings register.

## Common failure modes

- **No single-identifier spine.** Different systems identify the same incident with different IDs — triaged in ServiceNow as `INC-...`, post-mortemed in Confluence by title, filed in the register with yet a third ID. The auditor cannot cross-reference.
- **Post-mortem-without-trace-IDs.** The post-mortem narrates but does not evidence; reperformance halts at step 3.
- **Closure-without-effectiveness-review.** The organisation's tracker treats "action done" as "case closed"; Clause 10.1 step 4 is absent.
- **Materiality-threshold inconsistency.** Different incidents of the same severity reach different reporting audiences.
- **Redacted evidence as standard.** The auditor cannot see what the post-mortem author saw; the audit cannot test the RCA.
- **Platform-opaque closure.** The GRC-for-AI platform records a status but not the evidence pointers; the audit cannot drill down.
- **Article 73 determination after triage closure.** The applicability test happened late; the reporting window missed.

## Summary

- End-to-end incident reperformance is the specific-case counterpart to chapter 3's program-level audit.
- The sample is stratified by trigger source, severity, and age, under `mod-104` discipline; the sample selection is itself documented.
- Each sampled incident is walked across nine steps: detect, triage, RCA, post-mortem, regression-fixture, corrective-action closure, risk-register update, regulator notification, audit-committee reporting.
- Evidence sources are the trace store, run logs, GRC-for-AI platform, incident-management system, and post-mortem repository; each has characteristic failure patterns the auditor should expect.
- The cross-incident pattern pass is where program-level findings surface; isolated cells become themes.
- Workpaper hygiene — source, timestamp, version, materiality, ISA 620 specialist recording — is non-negotiable for `mod-104` compliance.
- Chapter 5 picks up the Article 72 Post-Market Monitoring Report as a document and tests its description of this same incident population.
