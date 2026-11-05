# Condition / Criterion / Cause / Effect / Recommendation — Authoring Findings That Will Hold

## Motivation

A finding is the smallest durable product of an audit. It survives the engagement — it is cited by the audit committee, by management's remediation plan, by the external regulator who reads the report, and by the *next* auditor who comes back a year later and reopens the same ground. If the finding is shapeless, the audit evaporates. If the finding is shaped well, the audit can be defended five years later under subpoena.

Two bodies of audit standards fix the shape. **The IIA's International Professional Practices Framework (IPPF) / Global Internal Audit Standards** — specifically the standards governing communication of engagement results — require that each finding identify the condition, the criteria, the cause, the effect, and the recommendation.<!-- needs-research: Prior IIA Standard 2410 ("Criteria for Communicating") was consolidated into the Global Internal Audit Standards effective 2025-01-09; confirm the exact Domain V / Standard number governing "elements of engagement communication" at the reading time, since the IPPF renumbering is recent. --> **The U.S. GAO's Government Auditing Standards (Yellow Book)** at paragraphs 9.17 and the surrounding 9.16–9.19 require the same elements for findings in performance audits, and the 2024 revision carries them forward.

The AI-audit context does not add a new standard — it adds *stress* to the existing one. The condition is often a model-behaviour claim that the auditor cannot directly observe without reperformance. The criterion is often a composite — a sentence from ISO/IEC 42001, a phrase from the EU AI Act, a control from the provider's system card, a line from a procurement contract — rather than a single authoritative source. The cause tends to be distributed across MLOps, data governance, product, and legal. The effect runs through fairness, safety, financial, and regulatory channels at once. The recommendation, if authored carelessly, becomes an engineering specification that the auditor's independence does not allow.

This chapter walks each of the five elements, shows the AI-audit specific failure mode for each, and ends with the workpaper trail every finding must have behind it.

## The five elements

### Condition — what is

The *condition* states what the auditor actually observed. It is a fact-claim about the auditee's current state, written in the present tense, in neutral language, and specific enough that someone else could reproduce the observation from the workpapers.

An AI-audit-ready condition does three things.

- **Names the subject precisely.** Not "the model" but "model `credit-risk-v2.4.1`, as deployed in the `prod-eu-west` serving environment between 2026-06-01 and 2026-09-30."
- **States the observable, not the implication.** Not "the model is unfair" but "on the stratified sample of 10,000 applications drawn per [Workpaper C-3.2], the model's approval rate for applicants self-identifying as [protected class A] was 41.2% versus 58.7% for the reference group — a four-fifths-rule ratio of 0.70 (below the 0.80 EEOC guideline)."
- **Links to evidence by workpaper reference.** Each quantitative claim is followed by a workpaper tag `[WP-###]` so the reader can trace the statement to the sample, the method, and the reperformance.

The condition does not editorialise. "The organisation has failed to…" is already a cause-or-effect construction smuggled into the condition slot. Keep the condition descriptive.

Common AI-audit condition failures:

- **Model-behaviour claim with no held-out test.** Condition cites the provider's own eval report. If the auditor did not reperform, the condition is a document-review finding ("the eval report states…"), not a system-behaviour finding ("the system behaves…"). Be honest about which one you have.
- **Scope drift.** Condition names "the AI system" but the workpaper covers only the ranker, not the upstream LLM summariser. Narrow the condition to what was sampled, then open a scope-limitation observation separately.
- **Freshness drift.** Condition quotes a metric observed in month 2; by the time the report drafts, the metric is three months stale and the model has been retrained. State the observation window explicitly.

### Criterion — what should be

The *criterion* states the standard the condition is being measured against. The auditor's work is only as defensible as the criterion is specific. "Industry best practice" is not a criterion. "NIST AI RMF function GOVERN" is not a criterion either — it is a *reference*, and the auditor must name the specific subcategory and the specific expectation drawn from it.

In AI audits, criteria usually compose from several layers:

- **Regulatory.** EU AI Act Article 15(1) on accuracy, robustness, cybersecurity; EU AI Act Article 10(3) on representativeness of training data; SR 11-7 Section V on model validation; NYC Local Law 144 §20-871 on bias audit publication; FDA's Good Machine Learning Practice guiding principles; Colorado SB24-205.
- **Standards.** ISO/IEC 42001:2023 clauses (e.g., 8.3 AI system impact assessment; 9.1 monitoring, measurement, analysis and evaluation); ISO/IEC 23894:2023 on AI risk management; ISO/IEC 25059 on AI quality characteristics; ISO/IEC 42005 on AI system impact assessment; ISO/IEC TR 24028 on trustworthiness.
- **Contract.** Procurement SOW AI-system risk clauses; DPAs; vendor system-card commitments; service-level objectives for accuracy and latency; model-use restrictions.
- **Self-declared.** The auditee's own policy, model card, system card, data sheet, evaluation plan. A self-declared criterion is a *promise the organisation made* and is auditable on that basis.

A well-authored criterion cites the layer and the clause, in that order: "ISO/IEC 42001:2023 §9.1 requires the organisation to determine *what* needs to be monitored, *how* it will be monitored, and *when* results will be analysed; the provider's own AI Monitoring Policy (POL-AIM-002, Rev. 3) commits to monthly drift-detection runs on each production model."

Common criterion failures:

- **Composite masquerading as atomic.** A criterion that stacks three regulatory sources plus two internal policies is really five findings. Split them, or name explicitly that the condition breaches all of them.
- **Aspirational text treated as criterion.** The NIST AI RMF, the OECD AI Principles, the UNESCO Recommendation on the Ethics of AI, and the Blueprint for an AI Bill of Rights are *frameworks and guidance*, not binding criteria. They can inform a criterion but do not substitute for one unless contractually or regulatorily incorporated.
- **Criterion written after the condition was observed.** An auditor who selects a criterion to fit a condition has started doing advocacy. Criteria are set at planning; if you discover one was missing, update the planning memo, don't quietly promote the condition.

### Cause — why

The *cause* explains why the condition departs from the criterion. The IIA and GAGAS both treat cause as the element where root-cause analysis lives. Cause is where auditors fail most often — because asserting cause is harder than describing state.

An AI-audit cause must be **structural** rather than **personal**. "The data scientist did not run the fairness test" is almost never the right cause level. "The MLOps release pipeline has no required pre-deployment fairness gate; releases proceed on approval of accuracy metrics alone" is the right cause level — it is actionable at the control level, not at the individual level.

Useful AI-audit cause categories:

- **Process absence.** A required activity has no owner and no trigger.
- **Process drift.** A required activity exists but has silently degraded (quarterly sampling dropped to annual; threshold loosened; approver bypass accumulated).
- **Design gap.** The system was never designed to produce the required evidence (no label retention for post-market monitoring; no per-group logging; no challenger-model infrastructure).
- **Governance gap.** No forum escalates the signal; risk owner undefined; sign-off authority ambiguous.
- **Data gap.** Required data does not exist, was not collected, or cannot be re-used under its collection basis.
- **Capability gap.** The required skill or tool is not present.

The auditor identifies cause by walking **from observation back through the controls**, not by asking "whose fault is this." A root-cause analysis performed with "5-whys" or fishbone techniques, documented in a cause-analysis workpaper, is defensible; a cause asserted without that workpaper is a guess.

Common cause failures:

- **Personalising.** Names an engineer or team as the cause. This invites grievance litigation and is almost never the actual cause.
- **Symptom-as-cause.** "The team was busy" — not a cause, that's a state.
- **Policy-as-cause.** "There is no policy" — sometimes right, but often a surface answer that hides the real structural absence (there is a policy, but no controls enforce it, no one owns it, no evidence validates it). Dig one level deeper.
- **Multiple causes smashed together.** If the condition has three causes, name three and rank by contribution.

### Effect — so what

The *effect* answers the materiality question: why does this finding matter? Without effect, a finding has no priority, and management can defer indefinitely.

Effect in AI audits runs on multiple axes and the auditor names each that applies.

- **Regulatory effect.** The condition breaches a binding regulation; what is the exposure? EU AI Act penalties range up to 7% of global annual turnover for prohibited practices, 3% for high-risk non-conformity, 1.5% for providing incorrect information to notified bodies (Article 99). SR 11-7 non-compliance is enforced through MRA letters and enforcement actions. NYC LL144 carries $500–$1500 per violation per day. Name the specific exposure; avoid round numbers that imply false precision.
- **Fundamental-rights / stakeholder-harm effect.** The condition means a specific population may be harmed. The effect must name the population, the harm channel, and (where measurable) an upper-bound estimate of harm count given the system's deployment footprint.
- **Financial-reporting effect.** Where the system feeds financial statements (expected credit loss models, insurance reserving, revenue recognition), the effect connects to material misstatement likelihood.
- **Safety effect.** Where the system is a safety component (SaMD, industrial control, automotive), the effect connects to patient / worker / user safety.
- **Reputational / contractual effect.** Breach of a published commitment, SOC report representation, or customer-facing SLO.
- **Operational effect.** Downstream model/service outages, backlog of manual review, cost of corrective action.

The materiality claim is a *defensible assertion*, not a calculation. The auditor says: "Given the deployment footprint of ~1.2 million EU applicants per year and the observed disparity, the finding constitutes a **major non-conformity** under ISO/IEC 17021-1 clause 9.4.9 because the AIMS has not achieved its intended results on a core fundamental-rights risk." The reader can agree or disagree; the reader cannot pretend the claim was not made.

Common effect failures:

- **Missing effect.** Finding skips straight from cause to recommendation. Materiality has not been claimed; management will deprioritise.
- **Overstated effect.** "This could cost the organisation billions." Round numbers and worst-case scenarios without a model of exposure undermine the whole finding.
- **Single-axis effect.** Finding states a regulatory effect only when a fundamental-rights effect is also present. Be comprehensive within the axes that apply.

### Recommendation — what next

The *recommendation* is the auditor's view of what the auditee should do. Independence sets the boundary: the auditor **recommends outcomes and controls**, not **engineering implementations**. An auditor who writes "replace the XGBoost classifier with a tabular transformer" has prescribed a design choice and compromised independence on the subsequent audit of whatever the organisation actually does.

Well-formed AI-audit recommendations:

- **Address the cause, not the condition.** If the cause is "no pre-deployment fairness gate in the release pipeline," the recommendation establishes a gate — not a one-off remediation of the single model.
- **Specify the control, not the technology.** "Implement a pre-deployment control that blocks releases of models serving fundamental-rights-adjacent decisions unless a fairness evaluation has been performed and reviewed by a role independent of the development team" — control-level and auditable.
- **Name the owner role, not the person.** Owner is "Head of ML Platform" or "AIMS Owner" — not "Priya."
- **Define a target state verifiable at follow-up.** The recommendation must be testable, so the follow-up audit can determine whether it was executed.
- **Avoid prescribing timing.** Timing is a management-response element (see chapter 3).

Common recommendation failures:

- **Design prescription.** Auditor specifies a vendor, framework, model architecture, or implementation detail. Delete and replace with a control-level statement.
- **Vague.** "Improve monitoring." Not auditable at follow-up.
- **Chained recommendations.** One finding, one recommendation. If the finding requires three controls to remediate, consider whether it is really one finding.

## The materiality claim behind the finding

Every finding carries a *materiality claim* — the auditor's assertion that this finding rises to a level requiring reporting at the shape the engagement produces. The materiality claim lives inside the Effect element and is explicit (see chapter 2 for the classification shapes).

An AI-audit materiality claim combines:

1. **The regulatory stake** — is the gap a binding requirement, a self-declared promise, or guidance?
2. **The harm channel and footprint** — who could be harmed, how, and over what population?
3. **The organisation's risk appetite** — approved tolerance for the risk category, documented somewhere in the AIMS or ERM.
4. **The pattern** — is this the first occurrence, a recurrence, a systemic absence?

The claim is defensible if the auditor can answer each of the four at the audit committee and point to the workpaper that supports it.

## The workpaper trail

Each finding has a trail of workpapers behind it, cross-referenced in the report. The trail at minimum:

- **Planning memo entry** — where the audit area was scoped, and on what risk basis (chapter 3 of `mod-103`).
- **Criterion memo** — the authorities the auditor is testing against, with clause-level citation (chapter 2 of `mod-102`).
- **Evidence workpaper** — the sample, population, methodology, result, and any reperformance (chapter 2 of `mod-104`).
- **Cause-analysis workpaper** — the chain of controls traced from observation back to structural cause.
- **Materiality memo** — the explicit claim per the four factors above.
- **Finding draft** — the CCCER-structured finding, with the above cross-references.
- **Management response and CAP** — ultimately attached per chapter 3.

A finding that cannot name its workpaper trail is not a finding; it is an impression. External peer review (and litigation discovery) assumes the trail is complete and will test it.

## Worked example — the finding before and after

Consider an AI auditor at a European insurer discovering, during an ISO/IEC 42001 surveillance audit, that the fraud-scoring model promoted to production in Q2 2026 was released without the risk assessment required by the provider's own AIMS procedure.

### Before (unshaped)

> "The fraud scoring model was deployed without proper governance. Management should ensure that governance procedures are followed going forward."

This is unusable. The condition is vague; the criterion is absent; the cause is unstated; the effect is implicit; the recommendation is cosmetic.

### After (CCCER)

> **Finding 2026-11 — Fraud scoring model released without the AI system impact assessment required by the AIMS**
>
> **Condition.** Model `fraud-score-v3.2`, released to the `prod-eu` serving environment on 2026-06-14 (release ticket REL-1874), reached production without an AI system impact assessment (AI SIA) having been performed per the organisation's AI Management System Procedure AIMS-PROC-004 §4.2. The approval record in the release workflow shows sign-off by the Head of Data Science and the Product Owner; the AIMS Owner signature required by §4.2 (c) is absent. Evidence: [WP-AIMS-11.3] release ticket export; [WP-AIMS-11.4] workflow approval trail; [WP-AIMS-11.5] interview notes, AIMS Owner 2026-10-22.
>
> **Criterion.** ISO/IEC 42001:2023 §8.3 requires the organisation to implement and maintain a process for AI system impact assessment. The organisation's AIMS-PROC-004 §4.2 operationalises §8.3 and requires that an AI SIA be completed and approved by the AIMS Owner before any model supporting a "decision-with-significant-effects" use case is released. The fraud-scoring model is classified "decision-with-significant-effects" per the AIMS inventory entry AIMS-INV-023.
>
> **Cause.** The release workflow in the organisation's MLOps platform treats the AIMS Owner sign-off as an *advisory* step rather than a *blocking* gate. On 2026-06-14, the workflow permitted progression to production once the Head of Data Science and Product Owner had signed; the AIMS Owner's absence did not block the release. The root cause is a workflow-configuration gap in the MLOps release pipeline: AIMS Owner sign-off is defined as a required field on the release form but is not enforced as a precondition for the "promote-to-prod" action. [WP-AIMS-11.6] pipeline configuration export.
>
> **Effect.** The AIMS has not achieved the §8.3 intended result of ensuring every in-scope AI system has been impact-assessed before deployment. For the fraud-scoring model specifically, deployment proceeded without the SIA that would have surfaced the model's downstream effects on claim-denial rates in a market where approximately 420,000 claims/year are routed through the system. Across the AIMS, the same configuration gap has permitted a further three releases of in-scope systems since the AIMS went live (per [WP-AIMS-11.7] release-log review 2025-11-01 → 2026-10-31), establishing a pattern. This is a **major non-conformity** under ISO/IEC 17021-1 §9.4.9: the AIMS has demonstrably failed to achieve an intended result for a controlled process.<!-- needs-research: confirm the exact ISO/IEC 17021-1 clause numbering for "major non-conformity" definition and criteria; the clause number used here is illustrative. -->
>
> **Recommendation.** Establish a pre-deployment control for in-scope AI systems that blocks promotion to production until the AI SIA has been signed off by the AIMS Owner (or a documented delegate). The control shall be enforced in the release pipeline such that absence of the required sign-off prevents promotion. The AIMS Owner shall review each in-scope release that occurred between the AIMS go-live date and the control's enforcement to determine whether a retrospective SIA is required, and shall update AIMS-PROC-004 to make the sign-off gating explicit. Recommendation owner: Head of ML Platform, with AIMS Owner concurrence.

The second version is auditable at follow-up: the follow-up team will inspect the pipeline configuration, look for the blocking gate, verify the retrospective review, and inspect the updated procedure text.

## Checklist before the finding leaves the engagement team

- [ ] Condition names the subject, the observation window, the observable, and the workpaper reference.
- [ ] Criterion cites a specific clause of a specific authority — regulatory, standard, contractual, or self-declared.
- [ ] Cause is structural, not personal, and is supported by a cause-analysis workpaper.
- [ ] Effect names at least one of the axes (regulatory, rights, financial, safety, reputational, operational) and includes a defensible materiality claim per the four factors.
- [ ] Recommendation addresses the cause, is control-level (not design-prescriptive), names a role owner, and is testable at follow-up.
- [ ] The finding cross-references the planning memo, criterion memo, evidence workpaper, cause-analysis workpaper, and materiality memo.
- [ ] A second reviewer independent of the preparer has signed off per the firm's engagement-quality review procedure.

## Summary

- A defensible finding has five elements — condition, criterion, cause, effect, recommendation — anchored in the IIA Global Internal Audit Standards and the GAO Yellow Book 9.17.
- Condition describes what was observed, in specific terms, against named evidence.
- Criterion cites the specific authority and clause the condition is being tested against, drawn from regulatory, standards, contractual, or self-declared layers.
- Cause is structural and traced through controls, documented in a cause-analysis workpaper.
- Effect names the materiality axes and makes an explicit materiality claim grounded in regulatory stake, harm footprint, risk appetite, and pattern.
- Recommendation addresses the cause, remains at the control level (preserving independence), names a role owner, and is testable at follow-up.
- Every finding carries a workpaper trail — planning, criterion, evidence, cause, materiality — that can survive external peer review and litigation discovery.
