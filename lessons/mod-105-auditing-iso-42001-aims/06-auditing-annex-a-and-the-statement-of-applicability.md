# Auditing Annex A and the Statement of Applicability

## Motivation

ISO/IEC 42001 Annex A is the reference catalogue of controls — organised into control objectives spanning policies, internal organisation, resources, AI system life-cycle, data, information for interested parties, use of AI systems, third-party and customer relationships, and system-impact and oversight. **Annex B** gives implementation guidance for each. The organisation is not required to adopt every Annex A control; it is required to document — in a **Statement of Applicability (SoA)** per clause 6.1.3 — which controls are applicable, which are excluded, the justification for each decision, and the implementation state of each included control.

For a certification audit the SoA is the single densest, highest-stakes document. A medium-complexity AIMS SoA runs 30–60 pages. Every included control is a testable control; every excluded control is a defensibility question. Stage-1 inspects the SoA for completeness and exclusion rigour; Stage-2 samples the SoA to test operation. Together, Annex A and the SoA are typically where the largest number of individual findings at a Stage-2 audit live.

## Annex A — the control catalogue shape

Annex A is organised into **control objectives** with one or more **controls** under each. The headline families (the auditor's working map): <!-- needs-research: confirm exact Annex A control-family numbering and names against the as-published ISO/IEC 42001:2023; the published structure is the authoritative reference and the auditor should always read it directly -->

- **Policies related to AI.** Governance policies, review and update of AI policy.
- **Internal organisation.** AI roles and responsibilities, reporting of concerns.
- **Resources for AI systems.** Resources documentation, data resources, tooling, systems and computing.
- **Assessing impacts of AI systems.** AI system impact assessment process, assessment documentation, assessing impacts on individuals, groups, and societies.
- **AI system life cycle.** Management guidance, requirements and specification, design, verification and validation, deployment, operation and monitoring, technical documentation, logging.
- **Data for AI systems.** Data management, data acquisition, data-quality, data provenance, data preparation.
- **Information for interested parties of AI systems.** System documentation, information for users, external reporting, communication of incidents, information on purposes and intended use.
- **Use of AI systems.** Processes for responsible use, objectives for use, intended use.
- **Third party and customer relationships.** Allocating responsibilities, suppliers, customers.

Each control has an **objective** (why), a **control statement** (what), and in Annex B an **implementation guide** (how). The auditor's criteria translation (chapter 2 of `mod-102`) renders the control into testable form: statement, evidence, procedure, measurable attributes.

## Auditing the SoA — three families of criteria

The SoA carries three families of auditable criteria.

### 1. Completeness

**Requirement.** Every Annex A control is addressed (included or excluded with reasoned justification). No silent omissions.

**Audit test.** Walk the SoA against the Annex A control catalogue. Produce a reconciliation workpaper:

```
Annex A ctrl ID   SoA addressed   Status (incl/excl)   SoA ref   Auditor note
A.2.1             Y               included             §2.1       -
A.2.2             Y               included             §2.2       -
A.2.3             N               -                    -          Missing — finding
A.5.1             Y               excluded             §5.1       weak justification — see below
...
```

Any control not addressed is a completeness failure. Depending on count, grades range from minor (one missing entry on an incidental control) to major (multiple missing entries across control families, pointing to a structural SoA gap).

### 2. Justification quality — inclusion and exclusion

**Requirement.** Each inclusion is justified by reference to the organisation's risk analysis and context; each exclusion is justified by reference to why the control is not applicable in the organisation's specific context (not by generic "not applicable" language).

**Audit test — inclusion justifications.** For sampled included controls, verify the SoA cites: the risk-register entries the control treats; the context element (which systems, which business processes, which impact categories) the control applies to; the implementation approach (procedure / tooling / role responsible); the operation evidence available.

**Audit test — exclusion justifications.** The auditor focuses skepticism here. For every exclusion, the justification must be *specific* to the organisation. Acceptable shapes:

- "Control A.X.Y — [specific control] is excluded because the organisation does not [describe a specific activity the control targets], as documented in the AIMS scope §4.3 (no AI systems involving [category]) and the risk assessment of 2026-02-18 (no risks against [category] identified)."
- "Control A.X.Y is excluded because the organisation does not develop AI systems from scratch and uses only third-party foundation models under supplier contracts; the control is instead addressed by the third-party control A.Z.W under which the supplier commits to [the relevant activity]."

Unacceptable shapes:

- "Not applicable."
- "This control does not apply to our business."
- "The organisation already has processes covering this."
- A boilerplate justification repeated verbatim across many controls.

Exclusions with weak justification are the most common Stage-2 finding against the SoA. Grade depends on criticality of the excluded control and pattern (one weak exclusion on a low-impact control is minor; several weak exclusions covering substantive control families is major).

**The hard question on exclusions.** The auditor must ask: *would any in-scope AI system plausibly need this control's objective met?* If yes, the exclusion fails regardless of the justification wording. Example: a control on "data management for training" is excluded because "we do not train models" — but the organisation fine-tunes models. Fine-tuning is training for Annex A purposes; the exclusion is wrong on the facts.

### 3. Traceability

**Requirement.** Each included control traces to (a) a documented implementation, (b) evidence of operation in the audit period, and (c) a risk-register entry it treats (where applicable to the control).

**Audit test.** For sampled included controls, verify the SoA's implementation and operation evidence citations and walk them to the actual artifacts. This is the chapter 4 traceability chain (risk → treatment → control → SoA → implementation → operation → residual) viewed from the SoA end. Breaks drive findings.

## SoA sampling strategy

A Stage-2 AIMS audit cannot test every SoA control on every AI system. The sampling strategy sits in the Stage-1 report and typically stratifies across:

- **Control objective family.** Ensure coverage of policies, roles, resources, impact assessment, life-cycle, data, information for interested parties, use, and third-party. Under-sampling a family is a Stage-2 gap.
- **Control objective risk relevance.** Controls treating higher-risk-band risks get more coverage.
- **Implementation maturity.** Freshly-implemented controls get coverage; previously-tested stable controls can rely on continued-operation evidence.
- **Operation-evidence availability.** Controls with abundant evidence (logs, trace data) are sampled on the evidence; controls with sparse evidence (periodic reviews) require depth on each sample.
- **Cross-system applicability.** For controls that apply to many AI systems (e.g., life-cycle controls), sample across the AI system population stratified as in chapter 3.

A defensible SoA sample for a first-cycle AIMS Stage-2 might be: 100% of policy and governance controls (small count, high leverage), ≥50% of life-cycle controls (sample across AI systems), 100% of controls for impact assessment and data governance (dense requirements), ≥30% of information-for-interested-parties controls. <!-- needs-research: confirm whether IAF has issued AIMS-specific sampling guidance under IAF MD 5 or an AIMS-specific document at reading time -->

## Worked walk — one control, end to end

Consider a hypothetical SoA entry:

```
Control:          A.7.3 Data quality for AI systems
Objective:        Ensure data used in AI systems meets defined quality requirements.
Applicability:    Included.
Rationale:        Required by risks R-DATA-01 (biased predictions from unrepresentative training data) and R-DATA-04 (data-quality drift post-deployment) in the risk register v2.3. Applicable to all 14 in-scope AI systems.
Implementation:   AIMS-DQ-Procedure v1.2 (defines data-quality requirements per model class).
Owner:            Head of ML Platform.
Operation evid:   Datasheet template (DS-TPL-v3); 14 system-specific datasheets; CI pipeline eval-gate (gate-dq-01); quarterly data-quality report to management review.
```

The auditor's walk:

1. **Requirement.** Find the Annex A text for A.7.3 and compare to SoA statement. <!-- needs-research: confirm the exact Annex A control ID and control objective for data-quality in the as-published ISO/IEC 42001:2023 -->
2. **Rationale.** Pull risks R-DATA-01 and R-DATA-04 from the risk register. Verify they exist, are current, and that A.7.3 is the treatment of record.
3. **Applicability.** Sample 3 of 14 AI systems. For each, verify the control is in effect (the system is subject to the DQ procedure).
4. **Implementation.** Retrieve AIMS-DQ-Procedure v1.2. Walk its content against the Annex A control objective.
5. **Operation.**
   - Datasheet template present and current? Yes.
   - Each sampled system has a current datasheet? Check.
   - CI eval-gate configured and firing? Pull the gate configuration from the pipeline-as-code repo; pull evidence of gate executions in the audit period for each sampled system.
   - Quarterly data-quality report to management review happened? Cross to clause 9.3 management-review minutes.
6. **Residual.** Risk register entry for R-DATA-01 shows an acceptable residual approved by the risk owner? Check.

Any break — missing datasheet on a sampled system, CI gate configured but not firing, quarterly report skipped, residual unapproved — is a finding. Grades differ:

- Missing datasheet on 1 of 3 sampled systems: likely minor, unless the system's risk band is high.
- CI eval-gate configured but not firing across the audit period: major — the control is on paper only.
- Quarterly report not delivered to management review: finding against A.7.3 operation *and* clause 9.3 management-review inputs.

## Integration with other control frameworks

Organisations with mature information-security programmes often have ISO/IEC 27001 controls already implemented. Annex A of ISO/IEC 42001 and Annex A of ISO/IEC 27001 share common ground (document control, change management, access control, incident management, supplier management). Where the organisation integrates, the SoA may reference the ISO/IEC 27001 control instance. The auditor:

- Confirms the integration is documented (the SoA says so, not just implicit).
- Confirms the referenced 27001 control actually covers the 42001 control objective (not all do — information-security change management often does not cover model-version change the way AIMS requires).
- Where the 27001 instance is covered by a current certification and the engagement is an integrated audit, leverages the 27001 evidence appropriately.
- Where the engagement is AIMS-only, still performs the AIMS-specific test: the auditor is opining on the AIMS, not relying on 27001 certification issued by another CB.

Chapter 11 drills into integrated audits.

## Common failure modes

- **Silent omissions.** Annex A controls not addressed at all in the SoA. Completeness failure.
- **Generic exclusions.** "Not applicable" without rationale. Justification-quality failure.
- **Exclusion that is wrong on the facts.** Covered above — fine-tuning counted as "no training", GPAI usage counted as "we don't operate AI systems".
- **SoA not aligned with the risk register.** The SoA references controls that do not match the risks the register lists.
- **SoA without implementation/operation evidence.** The SoA is a plan, not a report, when nothing links to actual artifacts.
- **Stale SoA version.** The SoA predates the current AI system inventory, or an AIMS change (new system, new vendor, new jurisdiction) has not been reflected.
- **SoA approved by the wrong party.** The SoA must be approved under the AIMS owner's authority (top-management delegation). A SoA with an ML-team-lead approval is weakly authorised.
- **SoA-only AIMS.** The SoA exists and the Annex A controls are ticked, but the clause 4–10 management-system mechanics around it are thin. Writing a defensible SoA does not create an AIMS — the clauses do, and the SoA is their output.

## Summary

- Annex A is a catalogue of control objectives and controls; the SoA is the organisation's documented selection of which apply and how.
- Three families of SoA criteria: completeness (every control addressed), justification quality (inclusions and exclusions specific to the organisation's context), traceability (each included control traces to implementation, operation, and the risk it treats).
- Exclusion justifications are the auditor's skepticism focus — "not applicable" is not a justification; the auditor asks whether any in-scope AI system plausibly needs the control's objective met.
- SoA sampling at Stage-2 stratifies across control families, risk relevance, maturity, and cross-system applicability; the strategy sits in the Stage-1 report.
- The worked walk — requirement, rationale, applicability, implementation, operation, residual — is the single most-repeated Stage-2 procedure in an AIMS audit.
- Integration with ISO/IEC 27001 and other MS Annex A catalogues is allowed where the SoA names it and the referenced control actually covers the objective; chapter 11 picks up integrated audits.
