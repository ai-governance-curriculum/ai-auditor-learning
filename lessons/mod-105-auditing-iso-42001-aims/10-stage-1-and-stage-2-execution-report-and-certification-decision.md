# Stage-1 and Stage-2 Execution, Report Authoring, and the Certification Decision

## Motivation

Chapters 1–9 built the audit engine clause by clause. This chapter puts the engine on rails: the execution choreography of Stage-1 and Stage-2 as prescribed by ISO/IEC 17021-1 clause 9 (with the AIMS-specific overlay in ISO/IEC 42006), the mix of evidence procedures the auditor applies, the structure of the Stage-1 and Stage-2 reports, and the path from the auditor's findings and recommendation through to the certification-body's certification decision reserved under 17021-1 clause 9.5.

The engagement operation is the single part of the audit the client sees most clearly. Confident, procedure-driven execution raises the perceived value of the audit even when findings are serious; sloppy execution undermines even the strongest audit opinion.

## Stage-1 — the documentation and readiness audit

### Objectives (17021-1 clause 9.3.1.2)

Stage-1 exists to: audit the client's MS documentation; evaluate the client's site-specific conditions and discussions with client personnel; review the client's status and understanding of requirements; collect information on scope, processes, locations, and statutory/regulatory aspects; review allocation of resources for Stage-2 and agree Stage-2 details; provide a focus for Stage-2 planning; evaluate whether internal audits and management reviews substantiate Stage-2 readiness.

### Execution shape

Stage-1 is typically **one to three days** of auditor time, part off-site (document review) and part on-site (walk-throughs, interviews with the AIMS owner and top management, understanding the AI system inventory in context). The lead auditor plus one or two team members is common.

### Stage-1 agenda template

```
Day 1 — Opening and documentation walk-through
  09:00  Opening meeting with top management, AIMS owner, audit team
         - Confirm scope, agenda, participants, confidentiality
         - Confirm Stage-1 objectives and output expectations
  09:30  AIMS overview presentation by AIMS owner
  10:30  Clause 4 — Context and scope walk-through
  11:30  Clause 5 — Policy and roles walk-through
  13:00  Clause 6 — Risk, impact assessment, objectives walk-through
  15:00  Annex A and SoA walk-through
  16:30  Day-1 debrief with audit team

Day 2 — Operation and performance evaluation walk-through
  09:00  Clause 7 — Support (competence, documentation control) walk-through
  10:00  Clause 8 — Operation and life-cycle walk-through
  11:30  AI-system inventory walk and sampling strategy discussion
  13:30  Clause 9 — Monitoring, internal audit, management review walk-through
  15:00  Clause 10 — Nonconformity and improvement walk-through
  16:00  Stage-2 planning discussion

Day 3 — Readiness evaluation and closing
  09:00  Internal audit and management review evidence inspection
  11:00  Stage-2 plan drafting
  13:00  Draft Stage-1 report preparation
  15:00  Closing meeting with client
         - Stage-1 observations and areas-of-concern
         - Readiness conclusion
         - Stage-2 plan (team, duration, scope, dates, sampling)
         - Logistics for Stage-2
```

Three days is one shape; smaller organisations use one, complex multi-site organisations use more. The ISO/IEC 42006 Annex A audit-day table is the authoritative driver. <!-- needs-research: confirm current 42006 audit-day table at reading time -->

### Stage-1 evidence procedures

Stage-1 is primarily documentation review and interview. The auditor's procedures:

- **Documentation walk-through.** Guided review of each required document with the AIMS owner.
- **Document inspection.** Detailed inspection of specific documents in auditor's own time.
- **Interview.** Structured interviews with AIMS owner, top-management representative, internal audit lead, selected first-line engineering leads.
- **Reconciliation.** The clause 4.3 scope reconciled against the AI system inventory (chapter 3's central Stage-1 workpaper).
- **Observation of context.** Brief observation of the operating environment — the AI engineering floor, the governance committee room, the monitoring operations.

### Stage-1 report

The Stage-1 report (17021-1 clause 9.3.1.2.4) communicates documentation findings, areas of concern, and the readiness conclusion to the client. A clean shape:

```
STAGE-1 AUDIT REPORT
Client:                   [Client Legal Name]
AIMS scope (proposed):    [certificate wording]
Standard:                 ISO/IEC 42001:2023
Audit team:               [Lead auditor; team members; technical experts]
Audit dates:              [YYYY-MM-DD to YYYY-MM-DD]
Audit objective:          Stage-1 audit of the client's AIMS per ISO/IEC 17021-1 clause 9.3.1.2
Audit criteria:           ISO/IEC 42001:2023; client's AI policy v?.?; client's SoA v?.?
Documentation reviewed:   [List with versions]

1. AIMS scope and context (clauses 4)
   Observations: ...
   Areas of concern: ...

2. Leadership and policy (clause 5)
   ...

3. Planning (clause 6)
   ...

4. Support (clause 7)
   ...

5. Operation (clause 8)
   ...

6. Performance evaluation (clause 9)
   ...

7. Improvement (clause 10)
   ...

8. Annex A and Statement of Applicability
   ...

9. Readiness conclusion
   [ready / ready with observations / deferred — with specific reasons]

10. Stage-2 plan (agreed)
   Dates:            ...
   Duration:         [Audit days per 42006 Annex A calculation]
   Team:             ...
   Sampling plan:
     AI systems:     [stratification]
     SoA controls:   [stratification]
   Sites:            [list]
   Pre-work by client: [list]

Appendices:
  A. Stage-1 observations detail
  B. Areas of concern catalogue
  C. Documentation inventory
  D. Interview notes summary
  E. Scope-reconciliation workpaper
```

**Areas of concern** are the Stage-1 artifact that most shapes Stage-2. They are not nonconformities — Stage-1 cannot raise nonconformities. They are documentary observations that *may become* nonconformities at Stage-2 if not addressed. The client has the Stage-1-to-Stage-2 interval (typically 4–12 weeks) to resolve them.

## Stage-2 — the implementation audit

### Objectives (17021-1 clause 9.3.1.3)

Stage-2 evaluates the *implementation*, including effectiveness, of the client's MS. It is where the auditor earns the certification recommendation — or recommends against it.

### Execution shape

Stage-2 duration is set by the 42006 audit-day table. For a typical first-year AIMS Stage-2, expect **5–15 audit days** depending on effective-personnel count, AI system count, and risk-uplift factors. The audit team comprises lead auditor, team auditors, technical expert(s) for AI subject matter, and (for integrated audits — chapter 11) auditors competent in the integrated standards.

### Stage-2 agenda template

```
Day 1 — Opening and clause 4–5 execution testing
  Opening meeting
  Clause 4 and 5 execution: scope-and-inventory reconciliation walk;
     policy-communication sampling; role-catalogue walk;
     top-management interview

Day 2 — Clause 6 execution
  Risk-assessment procedure walk and execution sampling
  Risk-treatment plan and SoA execution sampling
  AI objectives review
  Change-planning review

Day 3–4 — Clause 8 operation and Annex A controls
  AI-system sampling (systems chosen from Stage-1 sampling plan)
  Per-system: life-cycle walk — requirements → decommissioning
  Operation and monitoring evidence inspection (trace-store queries,
     dashboards, alerts, incidents, drift outputs)
  Annex A control sampling and operation evidence

Day 5 — Impact assessment and third-party controls
  Clause 6.1.4 / 8.4 impact-assessment sampling
  Article 27 cross-check for EU deployer scope
  Third-party / supplier controls sampling
  GPAI-usage review

Day 6 — Clause 9 performance evaluation
  Monitoring and analysis review
  Internal audit evidence inspection and independence check
  Management-review evidence inspection

Day 7 — Clause 10 improvement
  Nonconformity-register sampling and six-step walk
  Continual-improvement evidence walk
  Interaction with clause 9 findings

Day 8 — Findings consolidation and closing
  Audit team findings aggregation
  Finding draft review
  Client clarifications
  Closing meeting with findings, grading, recommendation
```

### Stage-2 evidence procedures

Stage-2 expands beyond documentation review to include:

- **Observation.** The auditor observes real control operation — a release decision made in a governance committee; an incident triage; a monitoring dashboard review.
- **Interview.** Interviews move to first-line (model engineers, ML-platform owners, prompt and retriever leads) and to impacted-staff perspectives.
- **Inspection.** Heavy documentation inspection, now with operational artifacts (traces, logs, pipeline runs, model-registry records, change tickets, incident records).
- **Independent testing / re-performance.** The auditor runs the test themselves — a trace-store query, a reproducibility bundle re-run (`mod-104` chapter 6), a hash reconciliation on a model artifact.
- **Analytical procedures.** Trends and anomalies across the audit period data — incident rates over time, drift-detection firing patterns, alert-to-ticket conversion.

Chapter 4 of `mod-104` operationalises the evidence inventory; chapter 6 operationalises the reproducibility bundle. Stage-2 is where those tools get used.

### Finding capture during fieldwork

Findings are captured as they are identified — in the shape set in chapter 2 (requirement, observation, evidence, impact, grading rationale, expected response). A mid-fieldwork finding register keeps the audit team aligned and lets the client receive clear findings at the closing meeting rather than a surprise report weeks later.

The audit team meets **daily** during Stage-2 to walk the day's findings, check for aggregation (chapter 2, Pattern 4 majors), and align on grading.

### Closing meeting

The closing meeting presents findings to the client with grading, the auditor's certification recommendation, and the next-steps path. The client is given the opportunity to respond to findings — to provide additional evidence that may change a grading or remove a finding. The lead auditor retains sole authority over the finding register; client disagreement is recorded but does not alter the auditor's determination.

## The Stage-2 report

The Stage-2 report is the formal audit output. A clean shape:

```
STAGE-2 AUDIT REPORT
Client:                   [Client Legal Name]
AIMS scope (certified):   [certificate wording]
Standard:                 ISO/IEC 42001:2023
Audit team:               [Lead auditor; team members; technical experts]
Audit dates:              [YYYY-MM-DD to YYYY-MM-DD]
Audit objective:          Stage-2 audit of the client's AIMS per ISO/IEC 17021-1 clause 9.3.1.3
Audit criteria:           ISO/IEC 42001:2023; client's AI policy v?.?; client's SoA v?.?; applicable statutory and regulatory requirements per client's AI-policy commitment
Audit period:             [covering operating effectiveness from ... to ...]

Executive summary
  - Recommendation (certification / with corrective actions / not recommended)
  - Major nonconformities (count and summaries)
  - Minor nonconformities (count and summaries)
  - OFIs (count and summaries)
  - Noteworthy strengths

1. Audit scope and criteria
2. Sampling plan executed
   - AI systems sampled: [table]
   - SoA controls sampled: [table]
   - Sites visited: [list]
3. Clause-by-clause and Annex A findings
   - Clause 4
   - Clause 5
   - Clause 6
   - Clause 7
   - Clause 8
   - Clause 9
   - Clause 10
   - Annex A (SoA controls)
4. Findings register
   [Each finding in the chapter-2 structure]
5. Audit opinion
6. Certification recommendation and basis
7. Required corrective-action plans (majors) and timeline
8. Required corrective-action plans (minors) and timeline
9. OFIs for the client to consider
10. Surveillance planning (if recommendation is positive)

Appendices:
  A. Audit team qualifications
  B. Documents reviewed
  C. Interview summary
  D. Evidence inventory
  E. Sample tables (populations, selection method, sample list)
  F. Scope-reconciliation workpaper
  G. Workpaper cross-reference
```

### Writing the opinion

The audit opinion is a short, formal statement. A representative shape:

> "Based on the audit of [Client] against ISO/IEC 42001:2023 during the period ... to ..., using the procedures described in this report, the audit team concludes that the AIMS as implemented at [Client] within the scope defined in Section 1 of this report [achieves conformity / achieves conformity subject to the corrective actions described in Sections 7 and 8 / does not achieve conformity for the reasons set out in Section 4] with ISO/IEC 42001:2023. Accordingly, the audit team [recommends certification / recommends certification conditional on successful closure of the major and minor nonconformities set out in Sections 7 and 8 / does not recommend certification at this time]."

The opinion is the product of the audit. Every finding, every workpaper, every piece of evidence exists to support the opinion. The opinion is tested by the independent reviewer under 17021-1 clause 9.5.

## The certification decision (17021-1 clause 9.5)

The certification decision is reserved to a person or group independent of the audit team. The audit team produces a recommendation; the certification body's decision-maker reviews the audit report, the finding register, and the client's corrective-action plans, then makes the certification decision.

Four typical outcomes:

1. **Grant certification.** The audit recommendation is positive, the decision-maker concurs.
2. **Grant certification conditional on CAP acceptance.** Majors (or a pattern of minors) require CAP acceptance before the certificate is issued; the CB tracks CAP submission and effectiveness verification (sometimes on paper, sometimes via a follow-up audit).
3. **Defer certification.** CAPs are not yet credible; the CB requires further work.
4. **Deny certification.** The AIMS has structural weaknesses the CAPs cannot bridge in a reasonable period.

The lead auditor supports the decision-maker with clarifications but does not make the decision.

## Internal AIMS audit output

The internal AIMS audit under clause 9.2 produces an *internal audit report* delivered to the Audit Committee (or equivalent body) and to top management. The structure mirrors the Stage-2 report but without the certification recommendation and with findings graded under the organisation's own grading convention. The internal audit report feeds the certification Stage-2 as clause 9.2 evidence.

## Audit documentation and QA

All audit workpapers must be retained per the CB's quality-management system (and per 17021-1 clause 10 management-system requirements for certification bodies). Workpapers include: audit plan, communications, interview notes, documents reviewed with hashes where applicable, sample selections, evidence of procedures performed, finding-development documentation, the finding register, and the closing-meeting record.

An **independent quality reviewer** reviews the engagement file before certification. The reviewer tests: criteria citation on every finding, evidence support on every finding, grading rationale on every finding, sampling defensibility, workpaper completeness, team competence demonstration, and consistency of the opinion with the finding register. This is the point at which chapter 2's grading discipline is tested.

## Common failure modes

- **Scope drift between Stage-1 and Stage-2.** Agreed scope at Stage-1 quietly shifts in Stage-2 fieldwork; the certificate ends up on the wrong scope.
- **Findings sprung at the closing meeting.** Findings not discussed during fieldwork create adversarial closing meetings; capture findings daily.
- **Opinion that does not match the finding register.** Unacceptable to the QA reviewer; the opinion is shaped by the findings, not around them.
- **CAPs accepted before review.** CAPs must be formally reviewed and accepted by the CB; "accepted" at closing meetings is a casual acceptance that does not substitute.
- **Workpapers thin.** Under QA review or accreditation inspection, thin workpapers unwind the audit retrospectively.
- **No retention of sample selection method.** The sampling defensibility turns on *how* the sample was drawn; failure to document is a methodology failure.

## Summary

- Stage-1 is a formal documentation-and-readiness audit producing the Stage-2 plan, areas of concern, and the readiness conclusion; the central workpaper is the clause 4.3 scope reconciliation against the AI system inventory.
- Stage-2 evaluates implementation and effectiveness, with evidence procedures expanding into observation, first-line interview, inspection of operational artifacts, and independent testing/re-performance.
- Findings are captured as they are identified, aggregated daily, and graded per chapter 2 rigour; the closing meeting presents findings and the recommendation to the client without surprises.
- The Stage-2 report has a fixed shape: executive summary, scope and criteria, sampling executed, clause-by-clause findings, findings register, opinion, certification recommendation, required CAPs, OFIs, surveillance planning.
- The certification decision is reserved to a party independent of the audit team under 17021-1 clause 9.5; the audit team produces the recommendation, the decision-maker determines the certificate.
- Workpapers are the auditor's last line of defence under QA review and accreditation inspection; thin workpapers unwind audits retrospectively.
