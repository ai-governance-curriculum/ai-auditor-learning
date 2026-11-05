# Auditing the Article 72 Post-Market Monitoring Report

## Motivation

For high-risk AI systems in the EU AI Act estate, the **post-market monitoring plan** is operationalised and reported on through a periodic **Post-Market Monitoring Report** that evidences the plan's execution in the period. Article 72 requires both the plan (chapter 1) and its execution over the system's lifetime. The report is the document the market-surveillance authority, the notified body (where Annex VI / VII conformity assessment applies), and the organisation's own AIMS owner all read as a single summary of the period's monitoring.

The auditor's job in this chapter is to test the report as a document. The test asks whether the plan from chapter 1 is actually executed as the report claims, whether the data in the report is adequate for the question the report is asking, whether breach-reporting and corrective-action evidence is present, and whether the report produces a next-period update to the plan that reflects what the period taught.

This is a conformity-shaped audit even for an internal audit engagement — the report's audience is partly external (regulator, notified body), and the auditor should test it to the standard the external audience would apply.

## What the report must contain

The Commission is to adopt an implementing act under Article 72(3) establishing the template and the elements. Until that template is published, the auditor tests against the Article 72 text and the Medical Device Regulation (EU) 2017/745 Article 83 PMS analogue, which the drafting history confirms as the Article 72 pattern. <!-- needs-research: confirm the status of the Article 72(3) implementing act at reading time; if the template has been published in the Official Journal, test against it instead of the MDR analogue -->

The elements the auditor should expect:

### Scope section

- The AI system(s) covered, identified by Annex IV identifiers, intended purpose, and version.
- The deployment surface — which Member States, which deployers (where known), which distribution channels.
- The reporting period and the period against which deltas are reported.
- The AIMS and quality-management-system references under Article 17.
- The applicable harmonised standards and the state of alignment.

### Monitoring-plan execution section

- The signals from the plan (chapter 1) and the measured values for the period.
- The thresholds and the number of threshold breaches per signal.
- The Chapter III Section 2 article each signal evidences — Article 9 risk management, Article 10 data governance, Article 13 transparency, Article 14 human oversight, Article 15 accuracy / robustness / cybersecurity.
- The method and the data source for each signal, matching the plan exactly.
- Analysis cadence execution — whether the stated cadence was met.

### Serious-incident and corrective-action section

- The list of serious incidents under Article 73 filed in the period, with filing timestamps and acknowledgement from the market-surveillance authority.
- The corrective actions under Article 20 opened in the period, their status, and their effectiveness-review evidence.
- The non-serious incidents (recorded per Clause 10.1) that resulted in corrective action.
- The widespread / cross-system incidents and their remediation.

### Changes-to-the-system section

- Model-version changes in the period and their pre-deployment evaluation evidence.
- Prompt-template, system-prompt, retrieval-corpus, tool-allowlist, or guardrail-configuration changes with material risk impact.
- Changes to deployers' integrations as reported by Article 26 deployer obligations.
- Changes to upstream GPAI providers or third-party components (see `mod-109`).

### Risk-register and impact-assessment section

- Risk-register updates in the period driven by monitoring (chapter 1) and incidents (chapter 3).
- Impact-assessment (ISO/IEC 42005) refreshes for the system in the period.
- Residual-risk trend and, if material, a statement whether residual risk remains within appetite.

### Next-period update section

- Changes proposed to the monitoring plan in light of the period's evidence.
- New signals added, removed, re-thresholded, or re-anchored.
- Resource commitments for the next period.
- Review and approval signatures for the proposed updates.

A report that lacks any of these sections is a finding against the Article 72 completeness test. A report that *has* every section but populates sections with boilerplate is a quality finding.

## The plan-execution test

The report's claim is that the plan from chapter 1 was executed. The auditor's claim test:

**Signal-by-signal reperformance.** For a sample of signals the auditor:

1. Retrieves the plan definition.
2. Retrieves the raw data in the trace store / monitoring platform for the reporting period.
3. Independently computes the signal value.
4. Compares to the report's reported value.

Deltas in signal values at the reporting level are typically a finding on *report integrity* rather than monitoring integrity (the monitoring dashboard computes correctly; the report hand-copies incorrectly).

**Threshold-breach count reperformance.** For each sampled signal, independently count threshold breaches in the period and compare to the report's count. A reported-count-low-of-actual is an integrity finding. A reported-count-high-of-actual is unusual and worth investigating.

**Cadence execution.** For each sampled signal, verify the stated analysis cadence (weekly / monthly / per-release) actually executed, with artefacts. See chapter 1's operation walk — the Article 72 report is the organisation's own public attestation of the operation, and audit evidence must support it.

## The data-adequacy test

Article 72 requires the plan to collect data *adequate* to evaluate continuous compliance with Chapter III Section 2. The auditor's data-adequacy test:

- **Statistical sufficiency.** For metrics with statistical confidence requirements (fairness slices, drift tests, calibration ECE), is the sample size per period adequate for the stated confidence? Low-volume subgroups may require a longer reporting window to reach adequacy; the auditor flags under-sampled slices.
- **Trace completeness.** For incident-triggered signals, is the trace coverage sufficient to replay an incident? See chapter 4.
- **Retention adequacy.** Do the retention horizons (Article 19 logs, Article 72 lifetime, Clause 7.5 retention) support the report's historical analysis? A report claiming a 24-month trend with 6-month retention is self-inconsistent.
- **Representative sampling.** Does the monitored traffic represent the deployed traffic? A report based on logging that is sampled (1% of traffic retained) must disclose the sampling and show the sample is unbiased.
- **Deployer-feedback channel.** For providers distributing to downstream deployers, the plan should ingest deployer feedback (incident reports, usage anomalies, user complaints forwarded by the deployer). Absent deployer-feedback ingestion is a data-adequacy defect.

## The breach-reporting evidence test

The report claims breaches, incidents, and corrective actions. The auditor confirms each with evidence:

- **For each claimed serious-incident filing** — produce the Article 73 submission receipt, the market-surveillance-authority acknowledgement, and a copy of the filed content.
- **For each claimed corrective action** — produce the Clause 10.1 record, the regression-fixture evidence, and (critically) the effectiveness-review evidence per chapter 3.
- **For each claimed non-serious-incident corrective action** — same shape, scaled down.
- **For each claimed cross-system remediation** — a cross-reference showing the change was applied to all affected systems.

Claims without evidence are the sharpest Article 72 findings. A report that asserts "five serious incidents were filed under Article 73 in the period" but can produce four submission receipts is a four-of-five integrity defect.

## The next-period update test

Article 72 is about continuous evolution. A report that does not update the plan for the next period is a plan-as-static finding. The auditor tests:

**Change-proposal content.** Are there named changes to the monitoring plan? If every signal is unchanged, that is itself suspicious — did the period's evidence really contain no basis for refinement?

**Lessons-driven changes.** Did the incidents and near-misses of the period drive changes in monitoring? If incident IDX-2026-014 (chapter 4 worked example) produced a shallow RCA that identified "review-gate skipping on urgent releases" as a cause, did the monitoring plan add a review-gate-compliance signal for the next period?

**Threshold re-calibration.** Did the organisation re-examine thresholds against the period's distribution? A threshold defined against an 18-month-old baseline is likely desensitised.

**New-signals for new deployments.** For any systems added to the Article 72 scope in the period, are signals in place?

**Signatures and routing.** The next-period update is approved by the AIMS owner and (where applicable) the quality-management system per Article 17. A proposal without signatures is a governance finding.

## The regulator-facing quality test

The Article 72 report is the document a market-surveillance authority can request. The auditor tests whether it would survive that request:

- **Plain-language summary.** The report should open with an executive summary readable by a non-technical reviewer. A report that begins in metric tables fails the audience test.
- **Factual tone.** Marketing framing, hedging, and comparative language (against competitors) should be absent. Facts, dates, counts, decisions.
- **Evidence pointers.** Every material claim has an evidence pointer — a monitoring dashboard snapshot, an incident ID, a filing receipt. Prose-only claims are not evidence.
- **Consistency with other filings.** The Article 72 report should be consistent with Article 73 filings, with the AIMS Annex IV technical documentation, with the system's registered EU Database entry (Article 71), and with any notified-body surveillance findings. Divergences are reporting-integrity findings.
- **Non-contradiction with external statements.** Public statements by the organisation (model cards, system cards, marketing material, Article 50 transparency disclosures, GPAI Article 52 obligations where applicable) should be consistent with the report. A system-card accuracy number that contradicts the Article 72 reported value is a serious disclosure finding across `mod-106` and `mod-108`.

## Interactions with other EU AI Act articles

The Article 72 audit is not standalone. The auditor tests at least the following interfaces:

- **Article 9 risk management** — the report's residual-risk discussion ties to the Article 9 risk management system.
- **Article 10 data governance** — data-drift signals tie to Article 10 training / validation / testing data-management requirements.
- **Article 13 transparency** — monitoring of user-facing transparency effectiveness.
- **Article 14 human oversight** — reviewer override rates and HITL queue metrics tie here.
- **Article 15 accuracy, robustness, cybersecurity** — most quality / drift / injection signals tie here.
- **Article 17 quality management system** — the report is produced under QMS procedures.
- **Article 18 documentation retention** — the report and supporting data are retained per Article 18.
- **Article 20 corrective action** — all corrective actions in the period appear in the report.
- **Article 26 deployer obligations** — deployer feedback and deployer-side incidents are ingested.
- **Article 72 itself** — the plan and its execution.
- **Article 73** — serious-incident reporting.

<!-- needs-research: confirm these article numbers against the final consolidated AI Act text at reading time; the published text may re-number -->

Each interface is a cell in the report-audit workpaper. Missing interfaces, or interfaces where the report asserts conformance without evidence, are findings.

## GPAI systemic-risk providers

For providers of general-purpose AI models with systemic risk under Chapter V, post-market monitoring obligations layer with the GPAI Code of Practice obligations. The auditor tests the Article 72 report in conjunction with the GPAI Code of Practice adherence evidence — frontier-safety framework operation, capability-elicitation evaluations, systemic-risk assessments, and incident-reporting to the AI Office. <!-- needs-research: confirm the GPAI Code of Practice adoption status and specific post-market reporting elements at reading time; the Code is being finalised under AI Office supervision and may be amended -->

See `mod-107` chapter 8 for the frontier-safety audit path and `mod-110` for the conformity-assessment-body interaction.

## Downstream deployer position

For an organisation that is a *deployer* (not a *provider*) of a high-risk AI system, Article 72 does not directly apply to the deployer — it applies to the provider. However, Article 26 deployer obligations include monitoring the operation of the system and reporting serious incidents to the provider (Article 26(5)) and to market-surveillance authorities in some cases.

The deployer's internal monitoring and incident-response discipline is still tested in this module; the Article 72 report is the provider's document, but the deployer's upstream feedback into that document is the deployer's audit subject. The auditor clarifies position in the engagement letter (see `mod-103`).

## Common failure modes

- **Boilerplate sections.** Section headings exist; content is pro forma without period-specific facts.
- **Executive summary that overstates.** The summary describes a stable, clean period that the detail section contradicts.
- **Evidence pointers absent.** Claims unsupported by monitoring dashboard IDs, incident IDs, filing receipts.
- **Threshold-breach undercount.** The report's breach count is lower than the auditor's reperformance.
- **Serious incidents under-described.** Article 73 filings are referenced but not summarised in the report.
- **Plan unchanged for next period.** The organisation treats the plan as static; the report is a reporting ritual.
- **Inconsistency with Article 73 filings.** Narrative in the Article 72 report differs from facts in the corresponding Article 73 filing.
- **Inconsistency with model-card / system-card claims.** Public claims and the Article 72 report tell different stories.
- **Downstream-deployer feedback uncaptured.** Providers are not ingesting deployer-reported events.
- **Article-interface gaps.** The report does not tie monitoring signals to the specific Chapter III Section 2 articles they evidence.

## Summary

- The Article 72 Post-Market Monitoring Report is the periodic document that operationalises the Article 72 plan (chapter 1).
- Expected sections: scope, plan-execution, serious-incident and corrective-action, changes-to-the-system, risk-register and impact-assessment, next-period update.
- The plan-execution test reperforms signals and breach counts against the report's stated values.
- The data-adequacy test checks statistical sufficiency, trace completeness, retention, representativeness, and deployer-feedback ingestion.
- The breach-reporting evidence test demands submission receipts, corrective-action records, and effectiveness-review artefacts for every claim.
- The next-period update test confirms the plan evolves on evidence, not calendar.
- The regulator-facing quality test asks whether the report would survive a market-surveillance request.
- Article-interface tests confirm monitoring signals tie to the specific Chapter III Section 2 articles they evidence.
- Chapter 6 adds the three-lines independence sanity test the auditor runs alongside this evidence pass.
