# Auditing the Continuous-Monitoring Program

## Motivation

A certified AI management system that stops learning about its own deployed systems is a snapshot, not a system. ISO/IEC 42001 Clause 9.1 and EU AI Act Article 72 both require the organisation to keep looking — to collect data, to analyse it, to act on it, and to retain the evidence. The two criteria converge on the same operational object: a *continuous-monitoring program* that watches a declared set of signals, trips alerts against declared thresholds, routes those alerts through a named escalation path, and feeds the resulting decisions back into the risk register and the corrective-action loop.

The auditor's job in this chapter is to test whether the program, as actually operated, satisfies both criteria — ISO 42001 Clause 9.1 as the generic AIMS-performance requirement, and Article 72 as the specific post-market-monitoring obligation for high-risk EU AI Act systems. The two criteria are not interchangeable. Clause 9.1 is the broader shape; Article 72 is a stricter overlay for the in-scope regulatory estate. A program that satisfies Clause 9.1 will almost always need additions to satisfy Article 72 — the auditor tests both and reports the delta.

The program itself is *authored* by `ai-risk-engineer` (L25) and the second-line AIMS owner. The auditor does not re-author it. The auditor tests whether what is authored is complete against the criteria, whether it is operating, and whether the evidence it produces is reliable enough to support the certification claim and the Article 72 report.

## Criteria map — Clause 9.1 and Article 72 side by side

The two criteria overlap but differ in scope, specificity, and evidence demands. The auditor's first workpaper is a crosswalk.

| Dimension | ISO/IEC 42001 Clause 9.1 | EU AI Act Article 72 |
|-----------|--------------------------|----------------------|
| Who is bound | Any organisation operating an AIMS it has declared certifiable | Providers of high-risk AI systems placed on the EU market or put into service, and GPAI model providers with systemic risk under the applicable code of practice <!-- needs-research: confirm Article 72 applicability extension to GPAI systemic-risk providers at reading time; cross-check Chapter V text and the GPAI code of practice --> |
| What must be monitored | What the organisation determines it needs to monitor to evaluate AIMS performance and effectiveness | Performance of the high-risk system throughout its lifetime — enabling the provider to evaluate continuous compliance with the requirements set out in Chapter III, Section 2 (risk management, data governance, technical documentation, record-keeping, transparency, human oversight, accuracy / robustness / cybersecurity) |
| How it is codified | Monitoring plan or equivalent documented information | A written **post-market monitoring plan**, part of the technical documentation referenced in Annex IV, structured against the template the Commission is to adopt by implementing act <!-- needs-research: confirm status of the Commission implementing act under Article 72(3) at reading time — template may or may not be published --> |
| What it must drive | Decisions: acceptance, corrective action, objective adjustment, or management-review input | Corrective actions under Article 20, serious-incident reporting under Article 73, risk-management updates under Article 9, information to deployers under Article 13 |
| Retention | Documented information retained per the organisation's retention policy | Logs retained for the period specified in Article 19 (at least six months unless Union or national law specifies otherwise), and the monitoring data retained for the system's lifetime as part of the technical documentation |
| Who reviews | AIMS owner, internal audit (Clause 9.2), management review (Clause 9.3) | Market surveillance authorities on request; notified bodies during conformity-assessment surveillance; the provider's own quality-management system (Article 17) |

The crosswalk is not an academic exercise — the auditor records the criteria for each monitoring target in each row of the fieldwork workpaper, so a finding can be stated against the specific source clause rather than against a blurred "monitoring is weak."

## The determinate-set walk

Clause 9.1 requires the organisation to **determine** what it monitors, how, when, who analyses, and when. Article 72 requires the same determination but demands that the determination be anchored to Chapter III Section 2 compliance.

The auditor's first fieldwork step is the **determinate-set walk** — request the monitoring plan (or plans; many organisations keep a Clause 9.1 plan and an Article 72 plan per in-scope system, and the auditor should expect both), and walk each declared monitoring target.

For each target, the plan must specify:

- **What** is being monitored — the metric or signal, defined precisely enough that two operators would compute the same value from the same data.
- **How** it is monitored — the data source (trace store, feature store, log pipeline, evaluation harness), the computation, the tool.
- **When** it is measured — the sampling cadence or event trigger.
- **When** it is analysed — the review cadence (which is not necessarily the measurement cadence).
- **Who** analyses and evaluates it — a named role, not a team mailbox.
- **Threshold(s)** that trigger action — the alert, the warning, the escalation boundary.
- **Escalation path** if the threshold trips — which incident channel, which risk-register row to update, which Article 73 clock (if applicable) starts.
- **Retention** of the measurement data and the analysis artefact.
- **Chapter III Section 2 article** it evidences, for the Article 72 overlay only — e.g. Article 9 risk management, Article 15 accuracy / robustness / cybersecurity, Article 10 data and data governance.

A row missing any of the above is a Clause 9.1 finding (and, if the system is in the Article 72 scope, an Article 72 finding as well). The grade follows ISO/IEC 17021-1 convention — minor if isolated, major if the omission undermines the AIMS or the Article 72 plan as a whole (see `mod-105` chapter 2 on nonconformity grading).

### The target inventory

The targets an auditor should expect to see in the plan for a GenAI deployment of material size:

- **Model-level performance** — task-level quality metrics, decomposed by subpopulation where fairness is material (see `mod-107` chapter 5).
- **Model-level and data-level drift** — input-feature drift, output-distribution drift, embedding-space drift, label-delay-adjusted concept drift (see chapter 2).
- **Safety-monitor signals** — refusal rate, guardrail hit rate by category, policy-violation rate, jailbreak / prompt-injection detector hit rate (see chapter 2 and `mod-107` chapter 7).
- **Near-miss signals** — events classified as not-an-incident but adjacent to one (guardrail activation followed by a user retry, tool-use attempts blocked, moderation queue backlog).
- **Operational-risk signals** — latency P95 / P99, error rates, cost-per-request anomalies, dependency-fault rates.
- **Harm-specific signals** — PII leak rate, CSAM/NCII classifier hit rate, CBRN-category refusal / override attempts, copyright / IP infringement complaint rate.
- **Human-oversight signals** — override rate, HITL queue depth, time-to-review, reviewer disagreement rate (see `mod-107` chapter 5 on fairness oversight).
- **User-feedback signals** — thumbs / rating distribution, support-ticket classification counts, complaint volume by harm category.
- **Distribution-channel signals** — deployer-reported incidents (for providers who distribute to downstream deployers under Article 13).

A plan that monitors only accuracy and latency is a plan that will fail the Article 72 completeness test. Chapter 2 deepens the drift / safety / near-miss / injection pipelines; this chapter is about whether the plan enumerates them at all.

## The operation walk

A plan that enumerates targets is not evidence that targets are being monitored. The second fieldwork step is the **operation walk**: sample across the inventory and reperform the chain.

For each sampled target, the auditor verifies:

1. **Data is being collected per the stated method.** Pull the raw data for a chosen window and confirm it matches the plan's definition of the signal. A metric defined in the plan as "P95 end-to-end latency across production traffic excluding health-check traces" must be computed exactly that way in the dashboard — a dashboard that silently includes health checks is a method defect.
2. **Retention is honoured.** The data must be present for the period the plan commits to. For Article 72 systems, the auditor also checks Article 19 logs retention — six months minimum unless a longer period is specified by Union or national law.
3. **Analysis has happened on cadence.** Look for the analysis artefact — the weekly review minute, the monthly monitoring report, the dashboard snapshot archived with a signature. Analysis without an artefact is not analysis the auditor can rely on.
4. **Evaluation produced a decision.** The analysis must end in one of: acceptance of current state (and a note that it was reviewed), a corrective action opened in the clause-10.1 tracker, an adjustment to the plan, or an input to management review (Clause 9.3). An analysis that ends in neither acceptance nor action is a defect against Clause 9.1 ("evaluate").

The operation walk is the step most monitoring programs fail. Dashboards exist; analysis does not. The auditor's workpaper should include *counts* — of expected analysis cycles in the period, of analysis artefacts recovered, of decisions recorded — not a narrative. Counts expose the gap plainly.

## Threshold-breach detection

A monitoring metric without a threshold is a chart. A threshold without a trip is a hypothesis. The auditor's third fieldwork step tests both.

**Threshold existence.** For each metric in the inventory, the plan must state the threshold that triggers action. A metric with no threshold is a finding — the organisation has no stated level at which it would act. The auditor allows a legitimate "trending only" declaration for a small number of context metrics, but the declaration must be explicit.

**Threshold defensibility.** Where did the threshold come from? Three defensible origins:

- **Methodology-derived.** The threshold follows from the risk-appetite statement and the methodology (e.g. severity level 3 corresponds to residual loss above $X, and the metric traps cross that boundary).
- **Benchmark-derived.** The threshold is a documented practice from a published source — a NIST AI 600-1 category, an AILuminate hazard-grade cut, an OWASP LLM01 detection rate, a vendor-published guardrail operating point.
- **Historical-derived.** The threshold is tuned against a documented historical baseline — e.g. P95 latency threshold set at 1.5× the trailing 90-day median, with the sampling and the computation archived.

A threshold adopted because "the vendor's dashboard defaults looked reasonable" is not a defensible origin. Record as a finding against the Clause 9.1 "methods" requirement and the Article 72 "evaluate continuous compliance" requirement.

**Breach reperformance.** For a sample of metrics the auditor pulls the raw data, independently computes the metric, and plots it against the threshold. Any period where the auditor's reperformance crosses the threshold must correspond to a documented alert, triage ticket, or decision in the organisation's incident / risk / corrective-action evidence. A crossed threshold with no artefact is the sharpest finding the monitoring audit can produce — the plan's trip mechanism is broken.

The reperformance sample must include:

- At least one *quality* metric (model accuracy, task success).
- At least one *safety* metric (refusal / guardrail / jailbreak-detector hit rate).
- At least one *drift* metric (feature or output distribution).
- At least one *operational* metric (latency, cost, error).
- At least one *harm-specific* metric per NIST AI 600-1 category applicable to the system.

## Escalation routing

A tripped threshold must go somewhere. The fourth fieldwork step is the **escalation walk** — tracing a breach from alert to closure.

The auditor verifies the following chain for each sampled breach event:

1. **Alert emitted** on the declared channel (PagerDuty rotation, Slack / Teams channel, incident-management platform like Jira / ServiceNow / Opsgenie; vendor-specific like WhyLabs alerts, Fiddler alerts, Arthur alerts).
2. **Alert received** by the named owner — confirmed by the owner's acknowledgement timestamp. An alert acknowledged by the on-call rotation is acceptable where the rotation is named in the plan.
3. **Triage decision recorded** — one of: not-an-incident (with rationale), incident-of-grade-X opened, immediate corrective action taken under Clause 10.1.
4. **Risk-register update** opened against the relevant row if the breach reflects a residual-risk change. The register update must cite the breach event and link back to the monitoring artefact.
5. **Serious-incident clock started** if the breach fits the Article 3 serious-incident definition. Article 73 reporting timelines are strict and the auditor checks them — the generally applicable notification window, with stricter windows for death and for widespread infringement. <!-- needs-research: confirm the exact Article 73 reporting-window numbers in the final AI Act text — generally 15 days, reduced for death cases and for widespread infringement / critical-infrastructure cases — at reading time -->
6. **Audit-committee reporting** if the breach is above the materiality threshold the engagement letter (see `mod-103` and `mod-111`) committed to.
7. **Closure** — the corrective action trackable through to resolution per Clause 10.1 (deep-dived in chapter 3 of this module).

A breach that terminates before step 7 is open. The auditor records both the open-breach count and the closure-latency distribution. A pattern of long closures is a finding against Clause 10.1 corrective-action timeliness.

## The Article 72 post-market monitoring plan

Where the system is in-scope for Article 72, the generic Clause 9.1 plan is not sufficient on its own. Article 72 requires a *written post-market monitoring plan* that is part of the technical documentation referenced in Annex IV, point 9, and is structured against a template the Commission is to adopt by implementing act. Until that template is published, the auditor tests against the as-published Article 72 text and the Article 61 shape in the Medical Device Regulation 2017/745 — the drafting-history analogue the European Commission has publicly stated is the Article 72 pattern. <!-- needs-research: cross-check the MDR Article 83 and PMS Plan Annex III, and the Article 72(3) implementing act status at reading time -->

The elements the auditor should expect in the plan:

- **Scope statement** — the AI system identified by Annex IV identifiers, its intended purpose, its deployers (where known), and the version(s) in production.
- **Data to be collected** — the signals enumerated (see "target inventory" above) with Article 72 anchoring to Chapter III Section 2 articles.
- **Methods** — sampling, measurement, analytical methods, statistical rationale where applicable.
- **Period and frequency** — how long the plan runs for, how frequently each signal is sampled, how frequently analysis is performed.
- **Responsibilities** — named roles for operation, analysis, escalation, and sign-off of the plan.
- **Reporting** — how the plan outputs feed Article 73 serious-incident reporting, Article 20 corrective actions, Article 13 information to deployers, and Article 9 risk-management updates.
- **Interactions with notified-body surveillance** — for systems under Annex VI / VII conformity assessment, the plan should enumerate what evidence the notified body receives during surveillance visits (see `mod-110`).
- **Review cycle** — when the plan itself is reviewed and updated. A plan that is not scheduled for review is a Clause 7.5 documented-information control defect as well as an Article 72 defect.

The auditor's Article 72 plan test is a checklist walk against these elements. Deliver findings against the specific element, not against "the Article 72 plan" as a whole.

## Retention policy

Both Clause 9.1 and Article 72 impose retention. The auditor tests both.

**Clause 9.1 retention.** The organisation's own retention policy fixes the horizon. The auditor confirms the horizon is at least as long as the shortest policy or legal obligation applicable — HR / discrimination claims (statute-of-limitations varies by jurisdiction), tax, sector-specific. The horizon must apply to *both* the raw data and the derived artefacts (analysis, decisions).

**Article 19 logs retention.** Providers of high-risk AI systems shall keep the logs automatically generated by the system under their control for at least six months, unless provided otherwise by applicable Union or national law — in particular Union law on the protection of personal data. <!-- needs-research: confirm Article 19 wording and any sectoral overrides at reading time -->

**Article 72 lifetime retention.** Monitoring data collected under the post-market monitoring plan is part of the technical documentation (Annex IV) and therefore must be retained as per the technical-documentation retention requirements — commonly understood to run for the lifetime of the system and for ten years after the system is placed on the market, under Article 18. <!-- needs-research: confirm Article 18 and Article 50 retention periods at reading time; note that Article 50 may concern transparency obligations — verify the correct retention article reference -->

**Retention-reperformance test.** Pick a log entry from six months ago and demand its production. Pick a monitoring analysis from twelve months ago and demand the full raw-data ancestry. Retention claims that fail reperformance are the sharpest retention findings.

## Interface to the risk-register

A monitoring program is operationally useful only if monitoring outputs change the register. The fifth fieldwork step is the **register-interface test** — walking from a tripped threshold to the register update.

For each sampled breach, the auditor verifies:

- The relevant register row is identifiable from the monitoring artefact (either the plan declares the register link up front, or the breach triage names the row).
- The register row has a dated entry reflecting the breach — the residual-risk score may be re-opened, a control may be marked defeated, a remediation may be opened, the "monitoring linkage" field may be refreshed.
- The scoring methodology from `mod-107` chapter 2 is honoured — a one-off breach does not inflate inherent risk; repeated breaches may change likelihood scoring; a control-defeated breach may escalate the control-defeated column.
- The register update is signed by the risk owner or the owner's delegated authority per the governance charter.

The *inverse* direction is also a test: the auditor samples register rows and walks them back to the monitoring signals cited in the row. A row that cites a monitor the plan does not operate is a trace break.

The register / monitor interface is the point at which the Article-72 scope and the broader AIMS merge — the register row is the AIMS-level artefact, and the monitoring signal is the Article-72 evidence. A broken interface breaks both criteria at once.

The interface also consumes the `ai-risk-engineer` (L25) risk-signal contract — a documented schema that fixes what a monitor emits and what a register row expects. The auditor tests the contract as a document: who authored it, is it versioned, is it referenced by both the monitoring plan and the register methodology.

## Common failure modes

- **Dashboard-without-analysis.** Charts exist; weekly-review artefacts do not. The chronic Clause 9.1 failure.
- **Threshold-without-origin.** Thresholds are vendor-defaults with no appetite-linkage or benchmark-linkage.
- **Threshold-without-trip.** Thresholds are documented; the alerting path is broken, misconfigured, or goes to an unmonitored channel.
- **Trip-without-register-update.** The breach is triaged but the register row is not refreshed.
- **Plan-without-Article-72-overlay.** The organisation has a Clause 9.1 plan and no Article 72 plan, despite in-scope systems. Separate criteria require separate evidence.
- **Retention-claim-without-reperformance.** The policy says 12 months; the data at month 7 is already purged.
- **Monitoring-without-ownership.** Metrics are "watched by the ML team" with no named role; alerts go to shared inboxes; closure is not tracked.
- **Monitoring-off-target.** Metrics are collected, but they do not refute or confirm the hypothesis the control claims.
- **Plan-not-scheduled-for-review.** The plan is static; the underlying system has shipped two major releases since the plan was last signed.

## Summary

- The continuous-monitoring program is tested against two criteria at once: ISO/IEC 42001 Clause 9.1 (the generic AIMS performance-evaluation requirement) and EU AI Act Article 72 (the specific post-market-monitoring obligation for in-scope high-risk systems). The auditor crosswalks the two and reports findings against the specific source.
- The determinate-set walk tests whether the plan enumerates what / how / when (measure) / when (analyse) / who / threshold / escalation / retention / Chapter III Section 2 article for each monitored target.
- The operation walk tests whether data is being collected, retained, analysed on cadence, and converted to decisions.
- Threshold-breach reperformance — the auditor independently computes metrics and confirms crossed thresholds correspond to recorded alerts, triages, and closures.
- Escalation-routing testing walks a breach from alert through triage, register update, Article 73 clock (where applicable), audit-committee reporting, and corrective-action closure.
- The Article 72 overlay demands a written plan structured against the eventual Commission template, with named Chapter III Section 2 anchoring; until the template is published the auditor tests against the Article 72 text and the MDR drafting analogue.
- Retention is tested by reperformance: logs at six months, monitoring data across the technical-documentation horizon, derived artefacts across the organisation's own retention policy.
- The register-interface test closes the loop — monitor-to-register and register-to-monitor traces must both hold.
- Chapter 2 deepens the drift / quality / safety / injection-detection target inventory; chapter 3 picks up the incident-response program that consumes monitoring breaches.
