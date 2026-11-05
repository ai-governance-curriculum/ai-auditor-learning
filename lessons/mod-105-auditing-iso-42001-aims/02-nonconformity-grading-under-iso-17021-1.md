# Nonconformity Grading Rigour — Major, Minor, and OFI under ISO/IEC 17021-1

## Motivation

Every clause audited, every control tested, every piece of evidence inspected, in the end, lands in one of four buckets: **conformity**, **opportunity for improvement (OFI)**, **minor nonconformity**, or **major nonconformity**. The grading drives the certification decision — majors block issuance; a pattern of minors can also block; OFIs do not block but shape the next cycle. Grading is the point in the audit at which the auditor's professional judgement becomes contractually consequential: wrong grading loses the client their certification or — worse — issues a certificate on an AIMS that should not have had one.

Auditors who skip the definitional rigour of ISO/IEC 17021-1 clause 9.4.8 and grade by feel produce reports the certification body's independent reviewer (17021-1 clause 9.5) rejects. This chapter installs the definitional rigour, applies it to AIMS-specific fact patterns, and gives the engagement a disciplined way to write findings that survive both the client's management response and the accreditation body's inspection.

## The definitions

ISO/IEC 17021-1:2015 clause 9.4.8 and ISO 9000:2015 clause 3.6.9 define **nonconformity** as "non-fulfilment of a requirement". A requirement is a documented obligation — from the standard, from the organisation's own AIMS documentation, or from applicable statutory and regulatory obligations the AIMS has to meet. The two grades:

- **Major nonconformity.** The absence of, or total breakdown of, a management-system element required by the standard. A nonconformity that raises significant doubt about the capability of the AIMS to achieve its intended results. A number of minor nonconformities against the same requirement or clause that, together, represent a systemic failure. 17021-1 clause 9.4.8.3 (expressed as the above; wording tracks IAF documents). <!-- needs-research: confirm the precise wording in the current ISO/IEC 17021-1 amendments and the current IAF MD 20 on major/minor grading -->
- **Minor nonconformity.** A nonconformity that does not raise significant doubt about the capability of the AIMS to achieve its intended results. Typically an isolated or sporadic lapse against a requirement rather than a systemic failure.

ISO/IEC 17021-1 does not require an OFI category; it is an industry convention widely used by certification bodies:

- **Opportunity for improvement (OFI).** Not a nonconformity. An observation that the requirement is met today but the practice could be strengthened against the spirit of the standard. The client is not obliged to respond, but strong AIMS cultures track OFIs through the management-review process. OFIs that *could become* nonconformities on the next audit cycle are the ones to write carefully.

The three-grade shape (OFI / minor / major) is what the certification body, the accreditation body, and the market will expect in the audit report.

## The grading algorithm

Every finding passes through four tests in order:

1. **Requirement identification.** What specific, numbered requirement is at issue? Cite it. A finding not pinned to a requirement is not a nonconformity — at best it is an OFI; often it is auditor opinion that should not be in the report.
2. **Evidence sufficiency.** Does the evidence (ISA 500 / AU-C 500, `mod-104` chapter 1) support the finding? A finding with only interview-based evidence and no documentary corroboration is undergraded; reach for the artifact.
3. **Impact test.** Does the condition *raise significant doubt about the capability of the AIMS to achieve its intended results*? This is the major-vs-minor fulcrum — it is a judgement, it must be defended in writing, and it is tested by the independent reviewer.
4. **Pattern test.** Is this one lapse against the requirement, or is it one of several that cumulatively represent a systemic failure? Three isolated-looking minors against the same clause aggregate into a major; grade accordingly.

Apply all four in order on every finding. Document each step in the workpaper so the independent reviewer can trace the grading decision.

## Major nonconformity — the four patterns

Four patterns commonly justify a major grading at AIMS Stage-2:

### Pattern 1 — Absence of a required MS element

One or more required elements under clauses 4–10 is simply not in place.

- **Example.** The organisation has no documented AI risk-assessment procedure (clause 6.1.2 requires one). The fact that ad-hoc risk discussions happen in meetings does not substitute for a documented process.
- **Example.** No management review has been held (clause 9.3). An item on a general management-committee agenda that briefly mentioned AI is not a management review.
- **Example.** No internal audit of the AIMS has been performed (clause 9.2), even though certification requires one before Stage-2 as a readiness condition.

### Pattern 2 — Total breakdown of an implemented element

The element exists on paper but does not operate.

- **Example.** The organisation has an AI incident-management procedure (clause 10) but the two serious incidents during the audit period were not routed through it; one was handled as a "customer support ticket" with no RCA.
- **Example.** A guardrail-configuration-change policy exists requiring approval, yet across a sample of ten production changes, seven have no approval record and the system has no enforcement.

### Pattern 3 — Significant doubt about AIMS capability

The AIMS is nominally present and operating but something about it means it cannot reasonably achieve its own policy and objectives.

- **Example.** The AI policy commits to meeting applicable legal and regulatory requirements. The organisation operates in the EU and places a biometric-categorisation system on the market without an EU AI Act Article 11 technical documentation file, which the standard's AI policy commitment requires it to maintain. This is not a minor paperwork lapse; it signals the AIMS does not actually track the regulatory obligations it committed to.
- **Example.** The organisation's AI system inventory lists 42 systems but the Stage-2 sample finds three high-impact systems not on the inventory. If the AIMS cannot even enumerate what it governs, it cannot govern it.

### Pattern 4 — Aggregation of minors into a systemic failure

Individually minor findings aggregate.

- **Example.** Minor: data-quality evidence missing on one AI system. Minor: on a second. Minor: on a third. Minor: on a fourth. Four isolated lapses against the same Annex A data-quality control across four systems is not four minors — it is a major against the control's operation.
- **Example.** Several minors against documentation control across different clauses (policy approvals missing, SoA not under change control, management-review records not retained per the retention policy) aggregate into a major against clause 7.5 documented information.

Pattern 4 is the one new auditors most often miss. The IIA, 17021-1, and the accreditation bodies all expect the auditor to step back and ask: *does the pattern tell me the control is systemically broken?*

## Minor nonconformity — the three patterns

Three patterns commonly justify a minor:

### Pattern 1 — Isolated lapse against a requirement

A single, documented lapse against a specific requirement, not reflective of the control's wider operation.

- **Example.** One of twelve sampled risk-assessment records is missing the risk-owner signature required by the organisation's own risk-assessment procedure. The other eleven are complete. The signature is required; the lapse is isolated.

### Pattern 2 — Sporadic deviation with low impact

A handful of deviations, none of them reaching the significant-doubt threshold.

- **Example.** Two of twelve risk-register entries lack an updated residual-risk assessment after the most recent risk-treatment cycle. The organisation detects the lapse at Stage-2 and shows it is not pattern-wide.

### Pattern 3 — Documentation gaps with evidence of underlying operation

The operation is happening correctly, but the documented evidence is thin.

- **Example.** Management review happens with the required inputs discussed and decisions made, but the minutes do not record several of the clause 9.3.2 inputs. The underlying operation is defensible; the record is not.

Pattern 3 minors often become OFIs if the documentary evidence is clearly present elsewhere (e.g., the decisions appear in the committee's action log). The judgement is whether the *record* fails the requirement.

## Opportunity for improvement — three honest uses

OFIs are easy to misuse. Three honest uses:

1. **A clear requirement is met today, but a change in the standard, the law, or the organisation's own objectives is about to render it non-compliant.** An OFI prepares the client without pretending a nonconformity exists.
2. **The organisation meets the requirement in a way that is defensible but suboptimal, and strengthening it would reduce audit risk next cycle.** OFI, not nonconformity.
3. **A near-miss at the minor-nonconformity threshold where evidence would not quite support a formal finding.** OFI, with the understanding that if the pattern recurs next cycle it becomes a minor.

Three dishonest uses to avoid:

- OFIs as a way to downgrade findings the auditor does not want to fight over. If it is a nonconformity, write it.
- OFIs as "nice to have" opinions unconnected to any requirement. If there is no requirement, there is no finding.
- OFIs stacked up so the audit "looks productive". Stacking OFIs annoys the client and dilutes the report.

## AIMS-specific grading fact patterns

Six fact patterns recur in AIMS audits. Pre-grading them before fieldwork lets the engagement team converge faster.

### 1. SoA exclusion without defensible justification

An Annex A control excluded from the SoA with boilerplate "not applicable" language. If the control's objective applies to any AI system in scope, grade **major** under 6.1.3 and the control-specific Annex A reference; if the exclusion is specific but weak, grade **minor** and demand a stronger justification.

### 2. Impact assessment skipped on a system in scope

An AI system in the inventory has no completed impact assessment under 6.1.4 (and ISO/IEC 42005). If multiple systems are affected, **major** under 6.1.4. If isolated, **minor**. If the system is EU AI-Act high-risk and the organisation also fails Article 27, note both the ISO/IEC 42001 finding and the regulatory exposure (and treat the regulatory failure as an additional 5.2 AI-policy finding on legal-commitment compliance).

### 3. Risk-assessment outputs not routed to treatment

Risk entries exist but do not route to a treatment plan with assigned owner and timeline. If widespread across the risk register, **major** under 6.1.3. If limited to two or three entries, **minor**.

### 4. Internal audit of the AIMS absent or shallow

Clause 9.2 requires an internal audit programme covering the full AIMS. No internal audit, or an audit that walked only a subset of clauses without a risk-based rationale, is **major** under 9.2. A full-scope internal audit with findings and in-progress corrective actions is conformant; shallow walkthroughs documented as "internal audit" are not.

### 5. Management review input or output gaps

Clause 9.3.2 lists required inputs; 9.3.3 lists required outputs. A pattern of gaps (several required inputs missing across review cycles) is **major** under 9.3. Occasional omissions with the underlying inputs available elsewhere is **minor** or OFI.

### 6. Monitoring without analysis

Clause 9.1 requires monitoring *and* analysis and evaluation of the results. Dashboards present but no documented analysis producing decisions is **minor** or (if pervasive) **major** under 9.1.

## Writing the finding

A gradable finding is a short, structured artifact. The template the CB expects:

```
Finding ID:        F-STG2-26-017
Grade:             Minor nonconformity
Requirement:       ISO/IEC 42001:2023 clause 6.1.2 (AI risk assessment); and org's AI Risk Procedure v2.1 §4.2 ("every in-scope system shall have a current risk assessment reviewed at least annually")
Observation:       On a sample of 12 AI systems in the AIMS inventory, 2 systems (SYS-07 "fraud-scoring-eu" and SYS-11 "copilot-dev") had risk assessments last reviewed 2024-08 and 2024-11 respectively, outside the organisation's defined annual cadence.
Evidence:          Risk Register extract 2026-09-18 (workpaper WP-6.1.2-03); risk procedure v2.1 PDF (WP-POL-02); interview with AI Risk Lead on 2026-10-02 confirming cause as "backlog following team restructure" (WP-INT-05).
Impact:            The two affected systems are medium-impact under the organisation's own risk banding. The lapse is not systemic — 10 of 12 sampled are current — but the cadence requirement is defined by the organisation itself.
Grading rationale: Isolated lapses against a defined cadence, not a systemic failure. Does not raise significant doubt about the capability of the AIMS. Consistent with minor-nonconformity Pattern 2 (sporadic deviation, low impact).
Expected response: CAP with root-cause analysis addressing the restructure impact, remediated reviews for the two systems, and a check that no other system fell out of cadence.
```

The six elements (ID, grade, requirement, observation, evidence, impact, rationale, expected response) mirror the IIA finding template adapted for the 17021-1 context. Chapter 10 walks the full report template; the finding is the atomic unit.

## The sentence-level discipline

Four sentence-level habits separate gradable findings from auditor opinion:

- **State the requirement first, verbatim.** The reader must be able to compare the observation to the requirement without hunting.
- **Describe the condition in observable terms.** "No risk assessment exists" is observable. "Risk management is weak" is opinion.
- **Quantify.** "2 of 12 sampled systems" is a defensible statement of extent; "several systems" is not.
- **Avoid prescribing the solution.** The finding says the AIMS does not meet the requirement; it does not tell the client *how* to fix it. Prescribing the solution turns the auditor into a consultant and triggers 17021-1 clause 5 impartiality concerns.

## How grading interacts with the certification decision

ISO/IEC 17021-1 clause 9.5 reserves the certification decision to a party independent of the audit team (the certification committee or an equivalent reviewer). The audit team produces a *recommendation*. Grading drives the recommendation:

- **Zero majors, finite minors with credible CAPs, OFIs tracked** → recommend certification.
- **Zero majors, pattern of minors suggesting systemic weakness** → the auditor should consider re-grading one or more minors to a major under Pattern 4 and the recommendation drops to "do not recommend until resolution".
- **One or more majors** → cannot recommend certification; CAPs must be submitted, evaluated, and (per the CB's procedure) potentially a follow-up audit performed before certification can be recommended.

Chapter 10 drills into the Stage-2 certification decision mechanics.

## Common failure modes

- **Grading by relationship.** Auditors who like the client undergrade; auditors who have been treated poorly overgrade. Both are 17021-1 clause 5 impartiality failures.
- **Grading by instinct without citing the requirement.** The independent reviewer rejects findings not tied to a specific requirement.
- **Writing OFIs as nonconformities.** If there is no requirement at issue, downgrade to OFI or remove.
- **Writing nonconformities as OFIs.** If the requirement is not met, do not hide behind OFI language. The client will not take the finding seriously and the AIMS will not improve.
- **Missing aggregation.** Three minors against the same clause almost always aggregate. Walk the findings list before closing fieldwork.
- **Prescribing the fix in the finding.** Keep the finding to the condition; leave the CAP to the client.
- **Un-sourced evidence citations.** Every finding cites the workpaper references for the evidence. Missing WP references invalidate the finding under CB QA.

## Summary

- Nonconformity grading under ISO/IEC 17021-1 clause 9.4.8 is the auditor's most consequential professional judgement.
- **Major** = absence, total breakdown, significant doubt about AIMS capability, or an aggregation of minors into a systemic failure.
- **Minor** = isolated or sporadic lapse that does not raise significant doubt.
- **OFI** is not a nonconformity; it is an observation about the quality of practice that meets the requirement today.
- Every finding passes the four tests — requirement identification, evidence sufficiency, impact test, pattern test — and is documented in the workpaper so the independent reviewer can trace the decision.
- The gradable finding has a fixed structure: requirement, observation, evidence, impact, rationale, expected response. State the requirement verbatim, describe the condition observably, quantify the extent, and avoid prescribing the fix.
- The certification decision is driven by grading but reserved to the independent reviewer under 17021-1 clause 9.5.
