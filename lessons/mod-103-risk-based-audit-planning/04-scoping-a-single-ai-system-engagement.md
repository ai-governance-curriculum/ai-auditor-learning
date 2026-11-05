# Scoping a Single AI-System Audit Engagement

## Motivation

Once an AI system enters the annual plan (chapter 2) with a materiality workpaper (chapter 3), the engagement team needs to scope it. **ISAE 3000 (Revised)** paragraphs 24–30 require the practitioner to determine the engagement acceptance preconditions, the subject matter, the criteria, the responsible party, the engaging party, the intended users, and the deliverable *before* engagement acceptance. **AT-C 105** paragraphs .11–.25 mirror that. **IIA Standards 2024** Standards 13.1–13.3 require the internal auditor to document the engagement objectives, scope, and resources at planning. **ISO 19011:2018** clauses 5.5 and 6.3 require the audit programme to define objectives, scope, criteria, and methods per audit. All four regimes converge on the same structural scope document, with per-regime variation in deliverable shape.

Scoping is where engagements fail silently. A poorly-scoped engagement either over-promises (covers more than the budget or evidence allows) or under-serves (ends with a report the intended user cannot act on). This chapter is the discipline that keeps the engagement defensible from acceptance through issuance.

## The seven scope elements the engagement letter names

An AI-system engagement letter and planning memo answer these seven questions in writing, in this order:

1. **Purpose** — what decision does the report inform?
2. **Criteria** — what standard does the subject matter get tested against?
3. **Boundaries** — what is in scope and what is explicitly out?
4. **Period of coverage** — point-in-time vs. period-of-coverage, with dates.
5. **Population** — the units from which samples (if any) are drawn.
6. **Sampling approach** — how the population is reached.
7. **Inherent limitations and deliverable shape** — what the report will and will not conclude.

The rest of this chapter walks each one.

## 1. Purpose — the user's decision

Every engagement starts from the user's decision. If the auditor cannot name the decision, the scope is wrong.

Typical user decisions for an AI-system audit:

- "Should we grant / renew the ISO/IEC 42001 certification scope for this system?"
- "Does this system meet the EU AI Act Article 16 provider obligations such that we can affix the CE mark under Article 43?"
- "Can the audit committee accept the first-line / second-line assurance that this system is operating within risk appetite?"
- "Is the service organisation's AI control environment operating effectively over the reporting period so that service users can rely on it?"
- "Has this system complied with the NYC LL144 AEDT independent bias-audit requirement for the next 12 months?"
- "Does this system meet the SR 11-7 independent model-validation standard for continued use?"

The purpose is restated in the engagement letter. Where the engagement is one component of a larger assurance (ISO/IEC 42001 certification covers the AIMS not individual systems; the AI system audit feeds AIMS evidence), the letter says so and names the parent engagement.

## 2. Criteria

The criteria layer is the output of `mod-102` — the auditable criteria register. Scoping decisions here:

- **Criteria set selection** — which of the organisation's criteria registers apply (ISO/IEC 42001 Annex A controls that attach to this system, NIST AI RMF categories, EU AI Act Articles 9–15 for a high-risk system, SR 11-7 validation elements, FDA GMLP principles, NYC LL144 bias-audit metric definitions). Multiple regimes often apply to one system; the scope names *all* applicable criteria sets or explicitly excludes the ones it is not testing.
- **Criteria suitability check** — the five tests from `mod-102` chapter 1 (relevant, complete, reliable, neutral, understandable). The scope names any criterion whose suitability is questionable and how it will be handled (use with disclosure, replace, propose to the organisation for refinement before engagement acceptance).
- **Criteria owner** — the party responsible for stating the criteria. For ISO/IEC 42001 and EU AI Act audits the criteria owner is the standard-setter; for internal audits it is the audit function; for attestation work it is the responsible party (the organisation, who asserts conformity to stated criteria).

The scope's criteria section lists each criteria set, the version, the effective date, and the subset that applies.

## 3. Boundaries — scope in, scope out

Boundaries is where the engagement is won or lost. For an AI-system engagement, the dimensions to pin down:

- **System boundary** — model(s), pipelines, data stores, inference endpoints, user interfaces, upstream data sources, downstream decision consumers, guardrail layer, logging stack, monitoring stack. A system-architecture diagram with scope markings is a mandatory workpaper.
- **Lifecycle phase** — design, development, training, pre-deployment evaluation, deployment, monitoring, re-training, decommissioning. Most engagements span deployment + monitoring + re-training; some are development-only (pre-deployment assurance) or decommissioning-only.
- **Control boundary** — first-line controls, second-line controls, third-line pre-existing coverage, IT general controls. The engagement often scopes *in* AI-specific controls and scopes *out* general IT controls that are covered by a separate audit (change management under SOC 1, access management under ITGC audit).
- **Data boundary** — training, validation, evaluation, production inference, feedback / RLHF data. The engagement often scopes in the current production data flow and scopes out historical training data (covered by a separate data-governance audit).
- **Geographic / jurisdictional boundary** — EU deployment only vs. global; US only vs. multi-state. Jurisdictional boundaries drive regulatory-criteria boundaries.
- **Vendor and third-party boundary** — in-house model vs. GPAI model provided by external vendor. Is the auditor permitted to test at the GPAI provider? Usually not; the auditor tests what the organisation holds (contractual evidence, vendor SOC reports, usage controls) rather than the GPAI model internals.
- **Explicit exclusions** — what the engagement will not test. The exclusions list is the discipline — "model internals of the third-party GPAI are not tested; reliance is placed on the vendor's ISO/IEC 42001 certificate", "cybersecurity of inference infrastructure is not tested; covered by [Report X]", "decision outcomes in jurisdictions outside the EU are not tested".

The boundary diagram plus the exclusion list is one of the most inspected pieces of the engagement workpaper.

## 4. Period of coverage

Two shapes dominate:

- **Point-in-time** — the subject matter is as it stands on a specified date. ISAE 3000 paragraph 12(a)(i) and AT-C 205 paragraph .12 both accommodate point-in-time examinations. Point-in-time is appropriate for *design* assurance — the control design, the model documentation, the AIMS documentation at the Stage-1 date.
- **Period of coverage** — the subject matter operated over a defined period. Appropriate for *operating-effectiveness* assurance — the control operated throughout the period, the eval was run on the required cadence, incidents were handled per the policy for every incident in the period.

Dates in the engagement letter include:

- The period or as-of date for the subject matter.
- The fieldwork window the engagement team expects to be on site.
- The reporting date (when the report will be issued).
- The cut-off for subsequent-events consideration (ISA 560 by analogy).
- The expiry date of the opinion (certifications typically carry a three-year cycle; attestations typically expire on the next period end).

AI-specific wrinkle: a model version that was in production at the start of the period and was retired mid-period is in scope *for the window in which it operated*. Period-of-coverage engagements have to handle model-version churn explicitly — the scope either names "all model versions in production in the period" or names a specific version and treats its deployment window as the period.

## 5. Population

The engagement population is the denominator for every sampling plan. For an AI-system audit, the common populations:

- **Decisions / predictions** made by the system in the period (inference log rows, with filtering for valid decisions excluding internal test traffic).
- **Users / subjects** affected by the system's decisions.
- **Inference requests / tool calls / agent episodes** for LLM systems.
- **Model versions** deployed in the period.
- **Training runs / fine-tuning runs** in the period.
- **Evaluation runs** completed in the period.
- **Incident records** opened in the period.
- **Access-review cycles** completed in the period.
- **Management-review meetings** held in the period.
- **Risk-register entries** attaching to this system.
- **Change records** (model-config changes, guardrail updates, prompt updates, system-prompt revisions).
- **Monitoring alerts / dashboards** reviewed in the period.
- **Data-quality checks** executed in the period.

Each criterion in the criteria register maps to one population (or to several). The scope names the population per criterion, the data owner, and the extraction method. Population definition precedes sampling-plan selection.

### A population-definition gotcha

Production LLM traffic often contains internal test traffic, synthetic traffic, internal-user traffic, and bot traffic. The engagement population is the *valid-user decision population*; the scope documents the filter rules (user-id lists, header tags, IP allowlists, test-account markers) and the first-line / second-line owner of the filter rules. Mis-defining the population is a common source of silent sampling bias.

## 6. Sampling approach

The engagement selects one of several sampling approaches *per criterion*; a full audit may use three or four across the criteria register. Standards references:

- **ISA 530 — Audit Sampling** (IAASB) and **AU-C 530** (AICPA mirror).
- **IIA Standards 2024** Standard 14.2 (Audit Sampling / Evidence Techniques).
- **ISO 19011:2018** clause 6.4.7 (Collecting and verifying information).

Common AI-audit sampling approaches:

- **Statistical sampling for attribute testing** — for binary-outcome criteria (control present / not), size drawn from ISA 530 Appendix 3 or an equivalent attribute-sampling table, with tolerable misstatement from chapter 3.
- **Stratified sampling across model-version boundaries** — sample within each model version in scope so aggregate conclusions are valid despite version churn.
- **Risk-targeted sampling** — oversample known-high-risk segments (minority-class decisions, high-stakes outcomes, flagged-for-review decisions) with disclosure that the sample is not statistical.
- **Full-population testing** — for low-volume populations (management-review minutes in the period, incident records, model versions) the audit tests the full population.
- **Re-performance** — the auditor re-executes the test (e.g., re-runs the fairness evaluation on an independent held-out dataset) under ISA 500 / ISA 530 re-performance semantics, typically with an auditor's expert under ISA 620.
- **Analytical procedures** — the auditor compares aggregate inference-log statistics across time or across segments and investigates anomalies under ISA 520.

Per criterion, the scope records: the sampling approach, the sample size, the sampling method (random, systematic, stratified, judgmental), the tolerable misstatement (chapter 3), the expected deviation rate, and the plan if the sample surfaces a deviation above the tolerable rate.

## 7. Inherent limitations and deliverable shape

ISAE 3000 paragraph 69 and AT-C 105 paragraph .61 require the practitioner to describe inherent limitations in the report. For AI the common inherent limitations the engagement letter names up front:

- **Opaque model internals** — the auditor can observe behaviour and documentation but may not be able to verify claimed causal mechanisms within the model.
- **Non-stationarity** — a point-in-time opinion does not imply future conformity; an operating-effectiveness opinion over a period does not imply the next period will conform.
- **Dependence on first- and second-line work** — the auditor tests the output of eval suites, red-team harnesses, monitoring dashboards; the opinion is on the outputs, not on the underlying ML craft (that is the subject matter, not the opinion).
- **Third-party GPAI reliance** — the auditor relies on vendor SOC reports and contractual evidence; direct testing of the GPAI model is usually out of scope.
- **Sampling risk** — residual risk that the sample did not reflect the population; mitigated by the chapter-3 performance-materiality discipline but not eliminated.

The deliverable shape is named at scope. Options:

- **Reasonable-assurance examination report** (ISAE 3000 / AT-C 205) — positive conclusion; the most work-intensive engagement.
- **Limited-assurance review report** (ISAE 3000 / AT-C 210) — negative-form conclusion ("nothing came to our attention..."); less work-intensive.
- **Agreed-upon procedures report** (ISRS 4400 / AT-C 215) — list of procedures and findings, no conclusion.
- **ISO/IEC 42001 certification audit report** — stage-1 and stage-2 reports in the 17021-1 shape; NC grading rather than overall conclusion.
- **Internal audit report** (IIA Standards 2024, Domain V) — observations, findings, recommendations, management responses, follow-up plan; written to the audit committee.
- **SR 11-7 independent validation memo** — model validation report with findings, mitigations, and effective-challenge documentation.
- **NYC LL144 bias-audit summary** — public summary with impact-ratio metrics and demographic categories.

The deliverable shape drives the engagement procedures (reasonable assurance is roughly 2–3× the fieldwork of limited assurance) and the independence posture; `mod-101` chapter 8 covers the posture.

## The scope document as a workpaper

The seven elements collapse into one planning workpaper — the engagement scope memo — that the engagement letter references. The memo is dated, signed by the engagement leader, and kept under version control. Changes to scope during fieldwork are revisions to the memo, not oral edits; the audit committee and the responsible party sign off on material scope changes.

A minimal template:

```
Engagement:       <engagement name, system-id, period>
Regime:           <IIA Standards | ISAE 3000 | AT-C 205 | ISO/IEC 17021-1 + 42006 | ... >
Intended users:   <list and decision each makes>
Purpose:          <one-sentence statement of the decision the report informs>
Criteria:         <list of criteria sets, versions, effective dates, subset>
Boundaries in:    <system boundary; lifecycle phase; control boundary; data boundary; jurisdictional boundary; vendor boundary>
Boundaries out:   <explicit exclusions>
Period:           <point-in-time date | period start–end>
Population:       <per criterion: population, owner, extraction method>
Sampling:         <per criterion: approach, size, method, tolerable misstatement>
Limitations:      <enumerated inherent limitations>
Deliverable:      <report type; conclusion form; distribution>
Team:             <lead auditor; technical specialists under ISA 620; independent reviewer>
Materiality:      <workpaper reference, chapter 3>
Approvals:        <engagement leader; CAE; responsible party sign-off on scope>
Date:             <planning date; revision dates>
```

## Common failure modes

- **Scope omits the explicit-exclusion list.** Fieldwork then absorbs unplanned scope and the engagement overruns; or the report over-claims against what was actually tested.
- **System boundary not drawn.** The engagement team reasonably believes the guardrail layer was in scope; the responsible party reasonably believes it was handled by SOC audit. Finding dropped.
- **Population mis-defined.** The sample is drawn from logs that include internal test traffic, synthetic generation runs, or deprecated model versions; the sample is not representative of the opinion population.
- **Sampling plan not pre-set per criterion.** The team samples on fieldwork judgement; ISA 530 cannot be defended in response to an inspector.
- **Deliverable shape decided post-hoc.** Fieldwork is done; management asks for a reasonable-assurance report when limited-assurance procedures were run. The engagement cannot deliver what was not planned.
- **Inherent limitations used as a pre-emptive excuse.** Too-broad limitation language tells the intended user the opinion is effectively worthless; the engagement should be re-scoped or declined instead.

## Summary

- An AI-system engagement is scoped by seven elements: purpose, criteria, boundaries, period, population, sampling, inherent limitations plus deliverable shape.
- Purpose anchors on the intended user's decision; if the auditor cannot name it, the scope is wrong.
- Criteria selection is a re-use of the `mod-102` criteria register under the five suitability tests.
- Boundaries are drawn on system architecture, lifecycle phase, control scope, data scope, jurisdiction, and vendor reliance — with an explicit exclusion list that is as important as the inclusion list.
- Period, population, and sampling plan are set per criterion and documented before fieldwork starts, under ISA 530 / AU-C 530 discipline.
- Inherent limitations are named at planning, not improvised at report time; the deliverable shape (reasonable/limited/AUP/certification/internal/validation memo) drives both procedures and independence posture.
- The scope memo is a dated, signed workpaper under version control; revisions are recorded, not silent.
