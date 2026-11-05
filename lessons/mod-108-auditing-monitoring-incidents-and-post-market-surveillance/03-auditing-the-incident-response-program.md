# Auditing the AI Incident-Response Program

## Motivation

A monitoring program without an incident-response program is a tripwire that goes nowhere. This chapter audits the program that catches what chapter 1 / chapter 2 trips — the end-to-end mechanism that triages, investigates, documents, remediates, and closes AI incidents, and that reports to regulators and the audit committee when the facts require it.

The criteria are plural because the regulatory surface is plural. The auditor tests against:

- **EU AI Act Article 73** — serious-incident reporting by providers of high-risk AI systems to market-surveillance authorities.
- **NAIC Model Bulletin on the Use of AI by Insurers (2023)** — insurer-specific AI incident recognition, governance, and reporting expectations.
- **FDA Mandatory Reporting Rule (MDR, 21 CFR Part 803)** adapted to AI/ML-enabled Software-as-a-Medical-Device (SaMD) — adverse-event reporting for AI-enabled devices.
- **SR 11-7 (Federal Reserve)** — Supervisory Guidance on Model Risk Management, including the expectation that model-performance-and-ongoing-monitoring issues are documented, escalated, and tracked to closure.
- **ISO/IEC 42001 Clause 10.1** — nonconformity and corrective action.
- **ISO/IEC 42005** — AI-system impact-assessment interaction with incidents.
- **NIST AI RMF (AI 100-1) MANAGE 4.3** — incidents and errors are communicated to the relevant AI actors.

The program is authored by the organisation (typically SecOps + AI-governance + legal) to its own policy. The auditor tests whether the authored program satisfies the applicable criteria, is operating, and is independent — the three-lines boundary is the subject of chapter 6 and is referenced throughout.

## What qualifies as an AI incident

The auditor's first test is definitional. Every criterion above uses a different term and threshold; the organisation's own definition must be at least as broad as the broadest applicable one.

### EU AI Act — "serious incident"

Article 3 defines a **serious incident** as an incident or malfunctioning of an AI system that directly or indirectly leads to any of the following:

- The death of a person, or serious harm to a person's health.
- A serious and irreversible disruption of the management or operation of critical infrastructure.
- Infringement of obligations under Union law intended to protect fundamental rights.
- Serious harm to property or the environment.

<!-- needs-research: confirm exact Article 3 serious-incident definition and Article 73 reporting-window numbers in the final published AI Act text at reading time — the published Official Journal text is the authority -->

Article 73 requires reporting of serious incidents to the market-surveillance authority of the Member State where the incident occurred. The reporting window is tight and tiered:

- A general window of 15 days from awareness.
- A reduced window for widespread infringement or critical-infrastructure incidents.
- A yet-shorter window for incidents involving death of a person.

<!-- needs-research: the final AI Act Article 73 window structure is three-tiered; confirm the current numbers at reading time — commonly cited as 15 / 10 / 2 days respectively -->

### NAIC Model Bulletin

The NAIC Model Bulletin on the Use of Artificial Intelligence Systems by Insurers (adopted December 2023) sets out expectations that insurers maintain a written AI Systems program covering governance, risk management, and testing — including the expectation that insurers have processes to identify, investigate, and remediate adverse consumer outcomes resulting from AI systems. The Bulletin is not itself a federal rule; it is a model the states adopt. The auditor tests against the adopting state's version where applicable. <!-- needs-research: confirm NAIC Model Bulletin adoption status by state and any 2025–2026 amendments at reading time -->

### FDA Mandatory Device Reporting (MDR)

For AI/ML-enabled SaMD, 21 CFR Part 803 requires manufacturers to report certain device-related adverse events and malfunctions to FDA. For AI/ML-enabled devices under the **Predetermined Change Control Plan** (PCCP) pathway, FDA guidance expects post-market surveillance aligned with the PCCP. An AI incident in an SaMD that meets the MDR reporting criteria produces an FDA filing on top of any EU AI Act Article 73 filing and any ISO/IEC 42001 corrective-action entry. <!-- needs-research: confirm current FDA PCCP guidance and MDR interaction with AI/ML SaMD at reading time; the final guidance on PCCP was issued in December 2024 -->

### SR 11-7

SR 11-7 (Federal Reserve SR 11-7 / OCC 2011-12 / FDIC FIL-22-2017) expects banks to document model-use issues and escalate them under an effective model-risk-management framework. For AI/ML models that fall under SR 11-7's model definition, a performance issue is a "model issue" requiring documentation, escalation, and tracking under the MRM governance framework. <!-- needs-research: SR 11-7 remains the primary supervisory letter; confirm any 2025–2026 Federal Reserve updates and interagency guidance alignment at reading time -->

### ISO/IEC 42001 Clause 10.1 and Clause 10.2

Clause 10.1 requires the organisation to react to nonconformities and take action to control and correct them; evaluate the need for action to eliminate the causes so the nonconformity does not recur or occur elsewhere; implement any action needed; review the effectiveness of any corrective action taken; and make changes to the AIMS, if necessary. Clause 10.2 covers continual improvement. Together they form the **nonconformity / corrective-action loop** the auditor tests end-to-end.

### NIST AI RMF MANAGE 4.3

AI RMF 1.0 (NIST AI 100-1) expects that risks and benefits from third-party and emergent AI issues are monitored (MANAGE 4), with MANAGE 4.3 specifying that incidents and errors are communicated to relevant AI actors including affected communities. The AI 600-1 GenAI Profile adds generative-specific MANAGE actions.

### The definition test

The auditor's definition test:

- The organisation has a written AI-incident definition.
- The definition covers all applicable regulatory categories listed above, with named sub-criteria.
- The definition names the trigger events that promote a monitoring breach (chapter 1 / chapter 2) into an incident candidate.
- The definition distinguishes incident from near-miss (chapter 2) and from quality defect (chapter 2) — with a stated promotion rule.
- The definition is reviewed on a documented cadence.

An organisation with no written definition, or a definition narrower than the broadest applicable regulatory category, is a Clause 10.1 and Article 73 finding on day one.

## Triage

Triage is the step at which a monitoring breach or an external report becomes an incident with a grade and an owner. The auditor's triage tests:

**Intake channel.** How does a signal reach triage? The expected sources:

- Monitoring alerts (chapter 1 escalation paths).
- SecOps / DFIR escalations (where an AI system is also an IT system).
- User complaints (support ticket, regulator inquiry, press enquiry, user-research channel).
- Deployer reports (for providers distributing to downstream deployers under Article 13).
- Supply-chain reports (upstream GPAI provider notifications — see `mod-109`).
- Internal red-team findings (post-release red-team runs that find a production-active issue).

**Named triage owner.** A named role performs triage within a documented time-to-triage. Shared mailboxes with no named owner are a finding.

**Triage rubric.** The rubric classifies candidates into: not-an-incident (with rationale), near-miss, quality defect, incident-of-grade-X. The rubric is documented and reproducible; two triagers with the same input should reach the same classification, within the rubric's acknowledged ambiguity.

**Triage decision record.** Every triage decision is recorded with a timestamp, a rationale, an owner for the subsequent action, and (for incidents) the initial grade. An incident whose initial triage is not recorded is an incident the auditor cannot test.

**Serious-incident clock.** For incidents that *might* meet Article 73's serious-incident definition, the clock starts at awareness. The auditor confirms:

- A clear "awareness" timestamp for every candidate.
- An initial Article 73 applicability determination within the first reporting window.
- The determination is made by or reviewed by a named role with regulatory-reporting authority.

A triage flow that does not surface the Article 73 clock within the first reporting window is a significant Article 73 finding.

## Root-cause analysis

Root-cause analysis is where ISO/IEC 42001 Clause 10.1 and SR 11-7 both want more than a symptomatic patch. The auditor's RCA tests:

**RCA method is named.** 5-Whys, fishbone / Ishikawa, fault-tree, Human-Factors / HSE, A3, or a hybrid. The chosen method is referenced in the incident record.

**RCA considers multiple causal levels.** AI incidents typically have causes at four layers:

- **Model / data** — training-data defect, concept drift, out-of-distribution input, adversarial input.
- **System** — retrieval error, tool-call failure, guardrail misconfiguration, prompt-template bug.
- **Process / organisation** — change-management failure, review gate skipped, oversight-override untriaged.
- **External** — upstream GPAI-provider change, dependency outage, third-party attack.

An RCA that attributes an incident only to the model when the system / process layer also contributed is a shallow RCA — common in early-maturity programs and a finding against Clause 10.1 "evaluate the need for action to eliminate the causes."

**RCA produces causal chain.** The record explicitly chains cause to effect; a bulleted list of contributing factors without a causal chain is not an RCA.

**RCA includes a counterfactual.** What condition, had it held, would have prevented the incident? The counterfactual drives the corrective action.

**RCA cites evidence.** Traces, logs, dashboards, red-team reproductions, code commits. Evidence pointers permit audit reperformance.

**Specialist competence.** For deep model-level causes an ML / AI-safety specialist is engaged; ISA 620 applies and the auditor records the specialist's competence and the auditor's evaluation of the specialist's output.

## Post-mortem authoring

The post-mortem is the document the organisation *commits to*. It is the artefact an audit committee reads, a regulator may request, a plaintiff's counsel may cite, and a future incident's RCA will reference. The auditor's post-mortem tests:

**Standard structure.** Expected sections:

- **Summary** — one paragraph of what happened, who was affected, what was done.
- **Timeline** — detection time, triage time, mitigation times, closure time.
- **Impact** — users affected, severity classification against the organisation's scale, regulatory categorisation (Article 73, NAIC, MDR, SR 11-7).
- **Root cause** — multi-layer analysis per the RCA section.
- **Remediation** — immediate mitigations, permanent fixes, regression fixtures.
- **Lessons learned** — what the organisation now knows that it did not before.
- **Action items** — each with owner, deadline, and clause-10.1 tracker ID.

**Blameless framing.** SR 11-7 and ISO/IEC 42001 do not require blamelessness, but blameless framing is the industry practice because it elicits the evidence RCA needs. A blameful post-mortem that papers over organisational causes is likely a shallow-RCA finding. The auditor is not prescriptive about the language but tests whether the organisational-cause layer is actually examined.

**Signed off.** By a named authority, with the AI-governance / legal / compliance review captured.

**Regulator-facing quality.** Where Article 73 or MDR reporting applies, the post-mortem should contain a regulator-shareable summary — factual, dated, and without marketing framing. A post-mortem that reads as internal-only is a finding on regulator-facing quality.

## Permanent regression-fixture back-feed

The auditor's sharpest Clause 10.1 test is whether the incident's permanent fix has been encoded as a regression fixture — a test case, an eval scenario, a monitoring assertion, or a red-team replay that would re-detect the issue if it recurred. Three layers:

- **Unit / integration test added** to the model- or system-level test suite.
- **Eval-scenario added** to the pre-release eval harness (Inspect / Promptfoo / HELM / custom), so the next model version is screened against the same input.
- **Monitor assertion added** to the production monitoring plan (chapter 1), so a reoccurrence trips an alert.

The auditor reperforms: pull the incident's permanent-fix commit and demand the diff shows the fixture addition; pull the plan and confirm the monitor exists.

A post-mortem committing to "add a regression fixture" without the fixture ever being added is the classic Clause 10.1 corrective-action closure failure — the finding writes itself.

## Regulator-facing reporting quality

Where Article 73, NAIC, MDR, or other regulator reporting applies, the auditor tests the quality of what was (or will be) filed:

**Article 73 report.** The report identifies the system by Annex IV identifiers, states the facts and the timeline, indicates the provider's assessment of the serious-incident category, identifies affected deployers, and describes the corrective actions taken or planned. Reports are not marketing; they are factual summaries with evidence pointers. <!-- needs-research: confirm Article 73 report content requirements and the market-surveillance-authority single-point-of-contact structure at reading time; consult Article 74 market-surveillance provisions -->

**MDR report.** 21 CFR 803.3 initial report within 30 days (or 5 days for events requiring remedial action to prevent an unreasonable risk of substantial harm). <!-- needs-research: confirm current MDR timelines and any AI-specific adaptations in FDA SaMD guidance at reading time -->

**NAIC / state-regulator notification.** Varies by state and by material impact. The auditor identifies the applicable state's bulletin / rule and tests against it.

**SR 11-7 MRM reporting.** Internal MRM escalation to the model-risk committee and (for material issues) to the board. The auditor traces the escalation.

**Audit committee reporting.** All incidents above the materiality threshold the engagement letter (see `mod-103`) commits to appear in the audit-committee pack.

Audit tests across the reporting surface:

- **Timeliness.** Reports filed within the applicable window. Reperform by comparing the awareness timestamp to the filing timestamp.
- **Completeness.** Required elements present. A missing element in a filed report is a finding.
- **Consistency.** Facts in the regulator-facing report match the internal post-mortem. Divergences are a serious finding on reporting integrity.

## The Clause 10.1 corrective-action loop

The incident ultimately closes through the Clause 10.1 loop. The auditor's loop test follows the clause text:

1. **React to the nonconformity.** The immediate mitigation is recorded.
2. **Evaluate the need for action to eliminate causes.** The RCA.
3. **Implement any action needed.** The corrective action — technical, process, organisational.
4. **Review the effectiveness of corrective action.** The effectiveness review — and this is the step most programs miss. Effectiveness review requires looking back at the corrective action after it has been in place for a stated period and confirming the issue has not recurred and, where applicable, the leading indicators remain healthy.
5. **Make changes to the AIMS, if necessary.** Policy, control, SoA, risk-appetite, or management-system changes driven by the incident.

For each sampled incident the auditor walks all five steps. Step 4 is the most common failure — the corrective action is implemented and closed in the tracker without a scheduled effectiveness review.

## The incident taxonomy

The auditor also tests whether the organisation taxonomises incidents to enable pattern analysis. The taxonomy should at minimum classify:

- **Harm category** aligned to the harm model (see `mod-107` chapter 1).
- **Root-cause layer** (model / system / process / external).
- **Trigger source** (monitoring / user / deployer / regulator / internal review).
- **Severity grade** on the organisation's scale.
- **Regulatory categorisation** (Article 73 serious / non-serious; MDR reportable / not; SR 11-7 model-risk material / not).
- **Chapter III Section 2 article(s) affected** (for high-risk systems).

A sample-level taxonomy failure (one incident mis-classified) is a minor; a program-level failure (no taxonomy, or inconsistent application across incidents) is a major that prevents pattern analysis and feeds the follow-up-tracker chapter (chapter 7).

## Common failure modes

- **Narrow definition.** The organisation defines incidents only as "security incidents" and does not recognise AI-specific incidents (bias episode, hallucination-driven harm, guardrail evasion at scale).
- **Triage without named owner.** Triage goes to a shared mailbox; time-to-triage is unmeasured.
- **Serious-incident clock not started.** Article 73 clock never triggers because triage does not have an applicability-determination step.
- **Shallow RCA.** Model-layer cause only; organisational-cause layer never examined.
- **Post-mortem-without-permanent-fix.** Immediate mitigations are shipped; permanent fixes are "backlogged indefinitely."
- **Permanent-fix-without-regression-fixture.** The code change ships; the test / eval / monitor that would catch recurrence is not added.
- **Regulator report lagging.** Internal post-mortem is written; the Article 73 / MDR filing is delayed beyond the regulatory window.
- **Reporting-divergence.** External report under-represents the internal findings; a credibility finding on reporting integrity.
- **Clause 10.1 step 4 missing.** Corrective actions are closed without effectiveness review.
- **No incident taxonomy.** Pattern analysis across incidents is impossible; the follow-up tracker (chapter 7) cannot aggregate.

## Summary

- The incident-response program is tested against a plural criteria surface: Article 73, NAIC Model Bulletin, FDA MDR (for SaMD), SR 11-7, ISO/IEC 42001 Clause 10.1 and 10.2, NIST AI RMF MANAGE 4.3.
- The definition test requires a written incident definition at least as broad as the broadest applicable regulator's.
- Triage tests cover intake channels, named owner, rubric, decision record, and the Article 73 clock.
- RCA tests cover method, multi-layer causal analysis, counterfactual, evidence, and specialist competence.
- Post-mortem tests cover structure, blameless framing, sign-off, and regulator-facing quality.
- The permanent regression-fixture back-feed is Clause 10.1's sharpest closure test — the fix must be encoded as a test, an eval, and a monitor.
- Regulator-facing reporting quality is tested for timeliness, completeness, and consistency against the internal post-mortem.
- The Clause 10.1 loop's step-4 effectiveness review is the most common failure point.
- Chapter 4 reperforms a sample of incidents end-to-end to confirm the program operates on the specific cases; chapter 6 tests three-lines independence in incident response; chapter 7 picks up the follow-up tracker.
