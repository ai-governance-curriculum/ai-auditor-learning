# Auditing Clause 6 — Planning, AI Risk Assessment, Risk Treatment, Objectives, and Change

## Motivation

Clause 6 is the engine of the AIMS. It is where the organisation *plans* how the AIMS will treat AI risk, deliver on its objectives, and manage change. Clause 6 — with Annex A and clause 8 (operation) — is where the auditor spends the single largest block of Stage-2 time, because this is where the AIMS either coheres into a defensible system or reveals itself as paper strapped over a disorderly set of AI teams.

Clause 6 is tested against three method references the AIMS relies on:

- **ISO/IEC 23894:2023 — Guidance on risk management for AI.** The informative but widely-adopted method standard for AI risk management, feeding 6.1.2 (risk assessment) and 6.1.3 (risk treatment).
- **ISO 31000:2018 — Risk management — Guidelines.** The generic risk-management-process reference 23894 builds on.
- **ISO/IEC 42005 — AI system impact assessment.** The method for 6.1.4 impact assessment; chapter 5 covers it.

The auditor's job in clause 6 is not to redo the organisation's risk analysis but to verify that the organisation *has* a risk-management *process* that is consistent with the standards, is executed, produces outputs that route to treatment, and ties back to the AI objectives the AIMS is pursuing.

## The structure of clause 6

- **6.1 — Actions to address risks and opportunities.**
  - **6.1.1** — general planning expectations (consider 4.1 issues and 4.2 interested-party requirements; determine risks and opportunities; plan actions; evaluate effectiveness).
  - **6.1.2** — AI risk assessment (risk-source identification, analysis, evaluation; retained documented information).
  - **6.1.3** — AI risk treatment (determine treatments; produce a risk-treatment plan; obtain risk-owner approval; produce the Statement of Applicability).
  - **6.1.4** — AI system impact assessment (per-system assessment; typically cross-referenced to ISO/IEC 42005).
- **6.2 — AI objectives and planning to achieve them.** Objectives must be measurable, monitored, communicated, updated, with plans for achievement.
- **6.3 — Planning of changes.** Changes to the AIMS carried out in a planned manner. <!-- needs-research: confirm 6.3 clause number in as-published ISO/IEC 42001:2023 -->

Chapter 5 handles 6.1.4. This chapter handles 6.1.2, 6.1.3, 6.2, 6.3.

## Auditing 6.1.2 — AI risk assessment

**Requirement.** The organisation shall define and apply a process to identify AI risks, analyse them, and evaluate them against risk-acceptance criteria. The process shall produce documented information.

**The 23894 shape.** ISO/IEC 23894 brings the ISO 31000 risk-management process (communication and consultation; scope, context, criteria; risk identification; risk analysis; risk evaluation; risk treatment; monitoring and review; recording and reporting) into AI with AI-specific risk-source taxonomies. The auditor expects the organisation's risk-assessment procedure to reference 23894 or be demonstrably consistent with it.

**Audit test — the procedural walk.** Request the AI risk-assessment procedure and walk it against this checklist:

```
Procedural element                                      Present   Evidence
---------------------------------------------------------------------------
Defined scope of each risk assessment (per system,       ?         Procedure §?
   per release, or organisation-wide — usually all three)
Defined risk-assessment criteria                          ?         §?
   - risk-impact scale defined with specific bands
   - risk-likelihood scale defined with specific bands
   - risk-acceptance criteria defined (what's acceptable?)
Risk-source identification method                         ?         §?
   - reference to 23894 Annex B risk sources, or an 
     equivalent AI-specific taxonomy
   - process to surface new sources (red-team, incident
     feed, regulator guidance, academic research)
Risk analysis method                                      ?         §?
   - how likelihood is estimated (historical data, 
     SME judgement, structured scenario analysis)
   - how impact is estimated (per the impact scale)
   - treatment of uncertainty
Risk evaluation method                                    ?         §?
   - comparison of analysed risk to acceptance criteria
   - determination of what requires treatment
Stakeholder engagement                                    ?         §?
   - roles in the assessment (risk owner, SME, impacted
     groups' representative)
Cadence and re-execution triggers                         ?         §?
   - calendar cadence (annual minimum is common)
   - event triggers (new system, major release, incident,
     regulatory change, dataset drift above threshold)
Documented-information retention                          ?         §?
   - what gets retained, where, for how long
Change control over the procedure itself                  ?         §?
```

A procedure missing more than one or two elements is **minor**; a procedure that does not define any risk-acceptance criteria (so the organisation cannot say what an acceptable residual is) is **major**.

**Audit test — the execution walk.** Procedure in place, now test execution:

1. Request the risk register (or whatever artifact holds the assessment outputs).
2. Reconcile the register against the AI system inventory. Every in-scope system should have a current risk assessment per the organisation's defined cadence.
3. Sample risk entries (sampling discipline from `mod-104` chapter 2). For each: trace from the entry to the risk-source taxonomy, to the analysis evidence, to the evaluation decision, to the risk-owner approval.
4. Test an "event" trigger. Pick an incident, a new-system release, or a regulatory event in the audit period; verify the trigger invoked a risk reassessment per the procedure.
5. Test for new-source responsiveness. Ask what new risk sources were added in the audit period and what drove the additions.

**23894 Annex B — the risk-source backbone.** The auditor should be fluent in the 23894 Annex B AI risk-source categories (environment, fairness, security, transparency, maintainability, control over AI system, impact on individuals, impact on groups, impact on society, impact on the environment, and so on). <!-- needs-research: verify the exact list and structure in the as-published ISO/IEC 23894:2023 -->
If the organisation's risk taxonomy covers only a subset (e.g., only "fairness and security" because the AI team came from a cyber background), that is a 6.1.2 finding — the taxonomy must be broad enough to surface the risks the organisation actually has.

**Cross-check with the role catalogue.** The hands-on evidence an `ai-risk-engineer` (L25) produces — risk-identification worksheets, Delphi records, scenario analyses, likelihood-and-impact rubrics — is the primary evidence for the execution walk. The auditor is not inspecting whether the risk engineer wrote a good analysis; the auditor is inspecting whether the analysis exists, routes to treatment, and reflects the procedure.

## Auditing 6.1.3 — AI risk treatment

**Requirement.** The organisation shall define and apply an AI risk-treatment process to: select treatment options; determine controls needed; compare the determined controls with Annex A controls; produce a Statement of Applicability (SoA) with justifications for inclusions and exclusions; produce a risk-treatment plan; obtain risk-owner approval for the plan and acceptance of residual risks.

**The traceability chain — the single most important workpaper at Stage-2.** A defensible 6.1.3 execution produces a traceable chain:

```
Risk entry (6.1.2)  →  Treatment option chosen (6.1.3)  →  Controls applied  →  Annex A reference (if applicable)  →  SoA entry  →  Implementation evidence  →  Operation evidence  →  Residual-risk assessment  →  Risk-owner approval
```

The auditor's primary Stage-2 test here is to **sample risk entries and walk the chain**. For each sampled entry:

- Can the auditor find the treatment plan entry?
- Does the plan name the controls (specific, not generic)?
- Does the SoA show those controls as applicable?
- Is there implementation evidence (design-stage, not operation yet — that is the next clause)?
- Is there operation evidence from the audit period?
- Is the residual-risk assessment documented?
- Is there risk-owner approval of both the plan and the residual?

The most frequent finding is a *break* in the chain. Risks exist, treatments exist, SoA exists, but a given sampled risk cannot be traced through. One break on one entry is a minor; breaks on multiple entries is a pattern pointing to a systemic weakness in the traceability discipline itself — major.

**The Annex A comparison requirement.** Clause 6.1.3 specifically requires comparing the controls determined by the risk analysis against Annex A to ensure no necessary control has been overlooked. Audit test: inspect the comparison record. Many organisations skip this step (they jump to the SoA directly from the controls they chose) — that is a finding, because it defeats the standard's intent of using Annex A as a completeness check.

**SoA — see chapter 6.** The SoA is the most load-bearing single document in the AIMS; chapter 6 drills in. For 6.1.3 purposes here, the auditor records: SoA present, SoA approved, SoA referenced by the risk-treatment plan.

**Risk-owner approval.** Verify named risk owners. Verify approval evidence (signature, ticket close-out, minuted decision). Interview a sampled risk owner — do they know they are the owner, and do they know what residual risk they have accepted?

## Auditing 6.2 — AI objectives

**Requirement.** The organisation shall establish AI objectives at relevant functions and levels. The objectives shall: be consistent with the AI policy; be measurable (if practicable); take into account applicable requirements; be monitored; be communicated; be updated as appropriate; be available as documented information. When planning how to achieve them, determine: what will be done; what resources; who is responsible; when it will be completed; how results will be evaluated.

**Audit test — the measurability walk.** Request the AI objectives register. For each objective:

- Is it measurable? (A specific metric exists or is defined.)
- Does it have a target or threshold?
- Does it have a measurement cadence?
- Is a specific person responsible?
- Is there a resource commitment (budget line, headcount line, tooling)?
- Is there a completion date (or a steady-state end-state, for ongoing objectives)?
- Is there evidence of monitoring (reports, dashboards, review minutes)?
- Is there evidence of communication (intranet, team OKRs, management-committee pack)?

**Common defects.**

- Objectives that are not measurable ("improve AI governance"). Rewriting these in SMART shape is the organisation's job, not the auditor's; the finding is 6.2(b) non-conformance on measurability.
- Vanity-metric objectives ("number of AI risk assessments completed per quarter"). Technically measurable but disconnected from outcome. Grade depends on whether it is the only objective (major — the AIMS cannot show outcome) or one of several (minor or OFI).
- Objectives disconnected from the AI policy. 6.2(a) requires consistency; if the policy commits to "responsible and fair AI" but the objectives all target throughput, that is a 6.2(a) finding.
- Objectives present but not monitored. Dashboard exists; no cadence of review and no decisions traced to the monitoring. Likely 6.2 and 9.1 finding both.

**The 6.2 ↔ 9.3 loop.** Objectives are revisited in clause 9.3 management review (9.3.2 inputs include "the extent to which AI objectives have been met"). The auditor cross-walks: for each objective, is there evidence it was reviewed at management review, and that outcomes led to continuation, revision, or closure?

## Auditing 6.3 — Planning of changes

**Requirement.** When the organisation determines the need for changes to the AIMS, the changes shall be carried out in a planned manner.

**Audit test.** Request the change log of the AIMS itself (policy versions, scope changes, SoA versions, procedure revisions). For each material change in the audit period, verify:

- Rationale documented.
- Impact on the AIMS assessed (did the change touch risk assessment, SoA, controls, roles, communication?).
- Approval obtained.
- Communication executed.
- Where the change affected existing risks or controls, downstream updates traced (updated risk-treatment plan, updated SoA entry, updated operational procedure).

**Common defects.** AIMS changes made by edit-in-place with no versioned record; changes to the AI policy or SoA without the risk-treatment plan or operational procedure being updated in parallel; large AI-system changes (new vendor, new deployment region) treated as operational-change-management without AIMS-impact review.

## Linking clause 6 to clause 8

Clause 6 produces the *plans*; clause 8 is where those plans are *executed* operationally. The auditor's transition from clause 6 testing to clause 8 testing is a handoff:

- Every treatment plan from 6.1.3 should map to an operational AI risk-treatment execution under 8.3.
- Every objective's planned action should show up in operational records.
- Every planned change should show evidence of execution.

Chapter 7 (clause 8) picks up the thread.

## The risk-opportunity balance

Clause 6.1.1 asks the organisation to address *risks and opportunities*. AIMS audits tend to be heavily risk-weighted; the standard's opportunities framing (new markets, new capabilities, efficiency, innovation) is often ignored. Not every engagement needs to grade on opportunities, but the auditor records the shape — an AIMS that has nothing on the opportunity side is often an AIMS the organisation treats as a compliance burden rather than a governance asset, and the Stage-2 report captures that context without raising it as a nonconformity unless a specific requirement is unmet.

## Common failure modes

- **Risk register without procedure.** Risk entries exist but the procedure that supposedly produced them is undocumented. 6.1.2 major.
- **Risk-acceptance criteria absent.** Without criteria, no risk can be formally "evaluated" and no residual can be "accepted". 6.1.2 major.
- **Risk-to-SoA chain broken.** Risks and SoA both exist; the traceability between them does not. 6.1.3 finding, grade depending on extent.
- **Annex A comparison skipped.** The 6.1.3 obligation to compare determined controls to Annex A is a completeness check; skipping it is a finding even if the SoA appears reasonable.
- **Objectives that are not measurable.** 6.2(b) is specific; reject hand-waved objectives at Stage-1 where possible.
- **Objectives disconnected from management review.** 9.3.2 requires objectives performance as an input; a disconnect generates findings on both 6.2 and 9.3.
- **Planned changes to the AIMS not planned.** Edit-in-place AIMS documents, SoA updates without impact on the risk-treatment plan.

## Summary

- Clause 6 is the AIMS engine: risk assessment (6.1.2), risk treatment (6.1.3), impact assessment (6.1.4, chapter 5), objectives (6.2), planning of changes (6.3).
- Clause 6.1.2 is tested against ISO/IEC 23894 process shape and against the organisation's own risk-acceptance criteria; every in-scope AI system should have a current, traceable risk assessment.
- Clause 6.1.3 is tested with a **traceability-chain** workpaper: from risk entry → treatment → control → Annex A → SoA → implementation → operation → residual → risk-owner approval. Breaks in the chain drive the grading.
- The SoA is the load-bearing 6.1.3 artifact; chapter 6 drills into it.
- Clause 6.2 objectives are tested for measurability, resource plans, monitoring, and communication; the 6.2 ↔ 9.3 loop (objectives reviewed at management review) is cross-walked.
- Clause 6.3 planned changes are tested by reconciling AIMS change logs with downstream AIMS artifacts (risk-treatment plan, SoA, operational procedures) to ensure changes propagate.
- Findings cluster around undocumented procedures, missing risk-acceptance criteria, broken traceability chains, non-measurable objectives, and AIMS changes made without propagation.
