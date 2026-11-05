# Scoring Audit Priority and Authoring the Annual AI Audit Plan

## Motivation

Once the audit universe exists (chapter 1), the planning question becomes *which auditable units get an engagement this year, in what order, with what intensity, and what is left out and why?* IIA Global Internal Audit Standards 2024 Standard 9.4 (Internal Audit Plan) requires the CAE to prioritise the plan based on risk, and to document the methodology used. ISO 19011:2018 clause 5.3 asks the audit programme owner to prioritise audits using risk; ISO/IEC 42006 and ISO/IEC 17021-1 clause 9.1.5.2 require certification bodies to plan audit duration and sampling on a risk basis. All three are satisfied by a *documented scoring methodology* the audit committee can approve and re-approve each year.

For AI the question is not whether to score on risk — it is *which risk model to use* and *what audit-specific drivers to layer on top*. The `ai-risk-engineer` (level 25) already operates an inherent-risk + residual-risk scoring shape for the first and second lines; the audit function should not replace it. What the audit function layers on top are *audit-specific* drivers that measure whether this unit *needs an audit right now*, independent of whether it is the organisation's highest-risk AI. The scored universe produces the annual plan.

## The scoring equation, in one line

> `audit_priority = f(inherent_risk, residual_risk, audit_coverage_debt, management_response_history, regulator_attention, external_auditor_coverage, change_velocity, auditability)`

Each term is a numeric band on a defined scale, documented, recalculated on a cadence, and traceable to its source. Priority is the ranking; the ranking drives the annual plan. No single term should dominate — if one does, the scoring methodology is wrong and should be challenged by the audit committee.

## Term 1 — Inherent risk (reuse, do not re-invent)

Inherent risk is the risk *before* controls — the harm potential if nothing about the system worked as intended. The `ai-risk-engineer` (level 25) operates an inherent-risk scoring shape the audit function should reuse. The shape typically scores on:

- **Harm potential** — scale of adverse impact if the system fails, derived from affected-population size, decision stakes (financial, safety, access-to-resources, liberty, dignity), reversibility, and cumulative exposure.
- **Likelihood of failure** — conditioned on modality, novelty, environment novelty, training-data representativeness, and the failure history of similar systems.
- **Regulatory classification** — EU AI Act Annex III category, prohibited classification, GPAI classification, Colorado AI Act in-scope flag, NYC LL144 AEDT flag, SR 11-7 model classification, FDA SaMD Class.
- **Data sensitivity** — PII, special-category data, PHI, biometric, children's data, employment-relationship data.
- **Autonomy** — human-in-the-loop vs. human-on-the-loop vs. human-out-of-the-loop; agentic tool-use authority.

The AI Auditor **adopts** this shape rather than re-building it. The audit workpaper for a given engagement will restate the inherent-risk band and the source of the band (which methodology, which date, which owner). If the audit disagrees with the risk engineer's scoring, that is a *finding* — it is not the audit's job to override the second line's inherent-risk score during planning.

> **Reusing the shape is not the same as adopting the number.** The auditor retains professional scepticism over whether the risk-engineer's band is defensible; see chapter 1 of `mod-104` for the evidence-based challenge posture. During planning the auditor takes the band as given and audits the band itself in-engagement.

## Term 2 — Residual risk

Residual risk is risk *after* the organisation's controls are applied, as the first and second lines assess them. In an ISO/IEC 42001 AIMS, residual risk lives in the risk-treatment plan under clause 6.1.3 and the Statement of Applicability under Annex A. Residual-risk inputs to audit priority:

- **Delta between inherent and residual** — small delta signals weak or unverified controls (even if inherent-risk is moderate, a low residual claim with little evidence is a high-priority audit).
- **Verification maturity of residual claim** — first-line self-assessment only, second-line review done, external evidence held, external audit held.
- **Accepted-risk register entries** — residual above the organisation's risk appetite but accepted by the appropriate authority. Each accepted-risk entry is a candidate audit scope.

Residual risk is the main lens for audit priority because it directly asks *does the control environment work?* — which is the audit question.

## Term 3 — Audit coverage debt

Audit coverage debt measures how long the unit has been without audit attention relative to its risk. Formally:

```
coverage_debt = years_since_last_audit - target_cycle_years(risk_band)
```

Target cycles by risk band are set in the audit charter and approved by the audit committee. Illustrative ranges (not a standard — organisations set their own and defend them):

| Risk band | Target audit cycle |
|---|---|
| Critical | ≤ 12 months |
| High | ≤ 24 months |
| Moderate | ≤ 36 months |
| Low | ≤ 60 months, risk-triggered off-cycle |

For AIMS certification work under ISO/IEC 17021-1, the cycle is the three-year certification cycle (stage-1 + stage-2 year 1, surveillance years 2–3, recertification year 4) — covered in chapter 5. For internal AI audit, the organisation sets cycles consistent with the charter.

Audit coverage debt is the "fairness" term in the equation — it ensures that stable, well-run but high-risk systems get back onto the plan on cadence, instead of being crowded out year after year by whatever is burning.

## Term 4 — Management response history

The IIA Standards and ISO 19011 both treat management responsiveness to audit findings as an input to planning. Possible bands:

- **Reliable** — findings closed within agreed deadlines with evidence; verified by follow-up.
- **Slow** — findings regularly closed late; closure evidence weak but delivered.
- **Disputed** — management-response memos routinely challenge findings on substance, not on evidence.
- **Unresponsive** — findings reopen, remain open, or close on paper without implementation evidence.

Unresponsive and disputed histories push a unit up the priority list independently of its inherent risk — the control environment surrounding this unit has a *process* failure that only re-audit will surface.

## Term 5 — Regulator attention

External regulator posture changes audit priority. Signals the auditor tracks:

- Open inquiry, market-conduct exam, enforcement action, consent order, No-Action-Letter terms, OMB CAIO reporting posture.
- Public regulatory priorities (the FTC's AI enforcement docket, CFPB's AI-in-credit focus, EEOC's AI hiring workstream, NYC DCWP AEDT enforcement patterns, HHS OCR AI-in-health postings, FDA AI/ML SaMD action plan updates, EU AI Office GPAI monitoring, DPA attention under GDPR Articles 22 and 35).
- Peer-organisation enforcement (an enforcement action against a comparable firm using a comparable AI system is a planning signal even if the enforcer has not reached your firm).

Regulator attention is a hard driver — a unit can jump to the top of the plan this quarter because a regulator opened an inquiry last week. The planning methodology should name an escalation path for exactly this, covered in chapter 7.

## Term 6 — External auditor coverage

External assurance over the unit reduces the need for an immediate internal audit but does not eliminate it. The auditor records:

- Which external report covered the unit (ISAE 3000, AT-C 205, SOC 2 / SOC 3 / SOC for AI, ISO/IEC 42001 certificate, ForHumanity IAAIS, EU AI Act conformity assessment).
- The report's criteria set, period of coverage, scope, and conclusion type (reasonable vs. limited assurance; qualified vs. unqualified).
- The report's **suitability to be relied on** — which under ISA 600 / ISA 610 (by analogy) and IIA Standard 9.5 requires the internal auditor to assess the external party's competence, objectivity, and the work's directly-relevant quality.

An external report that covers the unit with reasonable assurance against relevant criteria and current period can reduce the audit priority — not to zero, but down one band. An external report whose scope misses the audit's concern (e.g., SOC 2 Trust Services Criteria Security / Availability but not any AI-specific control) does not reduce priority at all; the row carries a note to that effect.

## Term 7 — Change velocity

AI systems change faster than most audit subjects. Change velocity is an audit-specific driver because:

- Continuous-learning or online-learning systems invalidate point-in-time assurance quickly; their audit cycle is shorter and the audit shape is closer to continuous auditing (chapter 7 of `mod-112`).
- Frequent retraining with a Predetermined Change Control Plan (PCCP) under FDA AI/ML SaMD guidance has to be audited on the PCCP cycle, not the historical annual cycle.
- Model-version churn (every two weeks on a product-led team) means the system the auditor visited last quarter is not the system in production this quarter; the priority should account for it.

Score change velocity on a four-band scale: static, infrequent retrain, continuous retrain with release gates, online/continuous learning without release gate. The last two push priority up.

## Term 8 — Auditability

The last term is practical: can we audit this unit *this cycle* with the team and evidence available? Signals:

- Evidence maturity: can the first and second lines produce the artifacts needed in a reasonable timeline?
- Specialist availability: is an auditor's expert under ISA 620 (ML, security, privacy, domain) available to the engagement?
- Access to third-party systems: can the auditor obtain evidence from vendors or GPAI providers (right-to-audit clauses, SOC 2 bridging letters, trust centre access)?
- Independence constraints: has the audit team been involved in control design work for this unit that would create a self-review threat?

A unit that scores high everywhere but fails auditability this cycle is deferred with the reasons documented and a remediation plan to make it auditable next cycle. Deferral is a defensible planning decision only when it is written down.

## A worked scoring row

To make this concrete, a single row of a scored universe for an in-house résumé-screening AI (EU AI Act Annex III category, NYC LL144 AEDT, Colorado AI Act in-scope):

```
universe_id              : INT-0042
title                    : Résumé-Screening AI (TA-ResumeRank v3)
population               : internal
inherent_risk_band       : High           (source: ai-risk-engineer scoring 2026-Q2)
residual_risk_band       : Moderate       (source: AIMS risk register entry R-AI-087, last review 2026-05)
residual_claim_verification: second-line review only; no external evidence
audit_coverage_debt_months: 14            (target cycle 12 months at High band)
mgmt_response_band       : slow           (two findings from 2025 cycle closed 3+2 months late)
regulator_attention      : NYC DCWP AEDT public-posting review; EEOC AI hiring enforcement pattern
external_auditor_coverage: none
change_velocity_band     : infrequent retrain (quarterly)
auditability_band        : high (evidence mature, specialist available, no indep. constraint)
priority_score           : 86 / 100       (band: Critical — plan this cycle, scope ≈ 450 hours)
```

Priority is produced by a documented weighting — the weights themselves are a planning decision approved by the audit committee, and documented. Two illustrative weighting schemes and their trade-offs:

- **Risk-weighted** — 40% inherent + residual, 15% coverage debt, 15% mgmt response, 15% regulator attention, 10% change velocity, 5% auditability. Favoured when the audit committee wants the plan to track the risk map.
- **Coverage-weighted** — 25% inherent + residual, 30% coverage debt, 15% mgmt response, 15% regulator attention, 10% change velocity, 5% auditability. Favoured when the audit committee wants to drive down coverage gaps year-over-year.

Document the weighting choice in the audit plan. If you change it from the prior year, say so and defend the change.

## From scored universe to annual plan

The scored universe is not the plan. The plan is produced by applying the audit function's capacity to the scored universe. The usual pipeline:

1. Rank the universe by priority score.
2. Apply **capacity**: sum of internal audit hours available, minus mandatory engagements (financial-statement audit support, SOX, regulator-required audits), minus continuous-audit effort, minus reserve for unplanned work. Typical reserve: 15–25% depending on the function's history of mid-cycle demand.
3. Walk the ranked universe top-down; accept engagements until capacity is spent. For each accepted engagement, name the type (full audit, limited-scope, follow-up, advisory under IIA Standards 9.4 if appropriate, continuous-audit cycle).
4. Note **declined** units — the universe rows that did not make the cut — and the priority band they fell into. The audit committee reads this list as carefully as the accepted list; it is where the plan's defensibility lives.
5. Attach the plan to the scored universe and the weighting document. Submit for CAE approval and then audit-committee approval (chapter 7).

An auditable annual plan carries:

- Every accepted engagement with scope, timing window, estimated hours, lead auditor, specialist needs.
- Every declined universe row with the band and the next-cycle treatment.
- The weighting document.
- A universe-change log for the cycle just closed.
- The reserve for unplanned work with the escalation path to use it.
- Dependencies on external coverage (if an ISO/IEC 42001 certification audit is scheduled, note the overlap with internal AIMS audit under clause 9.2).

## The annual plan is a rolling document

The plan is approved once per cycle, but the audit committee expects the CAE to amend it as the universe moves. Criteria for mid-cycle amendments:

- A universe row moves into regulator attention (new inquiry, new enforcement pattern against a peer).
- An incident (system failure, bias incident, data breach) elevates a unit's residual risk.
- A planned engagement cannot proceed (auditability has deteriorated — vendor refusing access, specialist unavailable, independence constraint emerged).
- The organisation acquires a company or deploys a new high-risk AI system mid-cycle.

Chapter 7 covers the CAE and audit-committee communication protocol for plan changes.

## Common failure modes

- **Scoring is not re-run.** The scored universe is point-in-time; a stale scoring deck mis-prioritises halfway through the year.
- **Weights are changed silently.** The audit committee cannot compare prior and current year plans unless weight changes are declared.
- **Residual-risk claims adopted at face value.** The planning auditor accepts the first-line / second-line residual band without challenge; the engagement then finds the claim was unsupported and the plan has over-invested in low-residual units.
- **External coverage over-relied on.** A SOC 2 report whose scope did not include AI controls is credited as covering the AI unit. The chapter-2 workpaper should capture the specific criteria the external report covered.
- **No declined-row list.** The plan shows what will be done and omits what was not — the audit committee cannot see what was deferred, and the defensibility of the plan evaporates.
- **Capacity treated as fixed.** An audit function that cannot reach its critical-band units in a cycle has a resource problem, not a planning problem. The plan should name the capacity gap explicitly and ask the audit committee to fund it, not quietly drop critical units to low-band.

## Summary

- Audit priority is a function of inherent risk, residual risk, audit coverage debt, management-response history, regulator attention, external-auditor coverage, change velocity, and auditability.
- The inherent-risk term is **reused** from the `ai-risk-engineer` (level 25) shape — the audit function does not re-invent it — and the audit-specific drivers (coverage debt, response history, regulator attention, external coverage, change velocity, auditability) are layered on top.
- The scored universe is not the annual plan; the plan is produced by applying audit capacity to the ranked universe, declaring declined rows, and documenting the weighting.
- Target audit cycle lengths by risk band are the fairness lever that prevents stable-but-critical units from being crowded out.
- The plan is a rolling document; mid-cycle amendments must have an audit-committee communication path (chapter 7).
- Defensibility comes from documenting *what you did not pick and why* as carefully as *what you picked*.
