# exercise-04: Sector-Overlay Criteria Drill

**Estimated effort:** 3 hours

## Objective

For a single AI system operating across multiple sectors and jurisdictions, author the **additive overlay** criteria that extend a horizontal ISO/IEC 42001 + NIST AI RMF baseline. The deliverable is a layered criteria set that shows (a) what each sector/jurisdictional regime *adds* to the baseline and (b) where overlap means a single piece of evidence satisfies multiple regimes. This exercise feeds directly into exercise 05 (the crosswalk register).

## Prerequisites

- Chapter [`01-what-makes-a-criterion-auditable.md`](../01-what-makes-a-criterion-auditable.md).
- Chapter [`05-sector-and-jurisdictional-overlays.md`](../05-sector-and-jurisdictional-overlays.md).
- Prior exercises 01 (ISO/IEC 42001) and 02 (NIST AI RMF) — their criteria registers serve as the *baseline* this exercise overlays onto.
- Source regime texts on your desk: **SR 11-7** + **OCC 2011-12** + **SR 23-4**; **FDA GMLP principles**; **FDA PCCP guidance**; **21 CFR Part 820 / QMSR**; **HIPAA Security Rule 45 CFR 164**; **NAIC Model Bulletin on the Use of AI by Insurers**; **Colorado SB 24-205**; **NYC Local Law 144** + DCWP rules; **Illinois 820 ILCS 42**; **OMB M-24-10** + **M-25-21**.

## Scenario

**Meridian Health & Specialty Insurance Group** is a fictitious US holding company with three operating subsidiaries using one shared AI platform:

1. **Meridian Specialty Lending** (Colorado-chartered bank) — uses the platform for a **credit-risk model** scoring commercial and consumer applicants, including Colorado consumers.
2. **Meridian Life & Health Insurance** (NAIC-adopting state) — uses the platform for a **claims-triage model** classifying incoming claims; also deploys an **AI-assisted underwriting review** that touches PHI.
3. **Meridian MedTech** (SaMD developer) — markets a clinical-decision-support product used in long-term-care settings, cleared under FDA De Novo and operating under a PCCP.

Separately, Meridian HR (shared services) operates an **AEDT** for candidate screening used in NYC and Illinois hiring, built atop the same platform.

Your engagement: Meridian's Chief Audit Executive has asked you — the newly hired AI Auditor in internal audit — to produce the overlay criteria set that extends the organisation's horizontal baseline (ISO/IEC 42001 and NIST AI RMF, authored in exercises 01 and 02) into the sector / jurisdictional regimes that actually bind the business. The output will feed into exercise 05's crosswalk register.

## Deliverables

Author overlay criteria registers for each of the following regime bundles. Each register uses the chapter-1 template with an added `Baseline-overlap` column (ISO/IEC 42001 clause / Annex A control, NIST AI RMF Subcategory) identifying the *baseline criterion this overlay piggy-backs on or supplements*.

1. **Financial overlay — SR 11-7 / OCC 2011-12 / SR 23-4** for the Meridian Specialty Lending credit-risk model.
   - Minimum: **10 criteria**, including model inventory + materiality tiering, independent validation function + evidence, benchmark / challenger testing, outcomes analysis, third-party / vendor risk (SR 23-4).
2. **Medical overlay — FDA GMLP + PCCP + QMSR (21 CFR Part 820 → ISO 13485)** for the Meridian MedTech clinical-decision-support SaMD.
   - Minimum: **10 criteria**, including intended-use scoping, representative data, independent test datasets, deployed-performance monitoring, PCCP change-control, MDR / post-market surveillance, QMS integration.
3. **HIPAA + NAIC overlay** for the Meridian Life & Health use cases.
   - Minimum: **6 HIPAA** criteria (administrative, physical, technical safeguards; BAA coverage; de-identification for training) + **6 NAIC** criteria (AI Systems Program documentation; unfair-discrimination testing; rate / adverse-action notices; vendor AI governance).
4. **Colorado SB 24-205 overlay** for the Meridian Specialty Lending Colorado-consumer credit-risk use.
   - Minimum: **6 criteria**, including consequential-decision scoping, algorithmic-discrimination affirmative-defence posture, impact assessment, consumer notice, adverse-action notice, right-to-appeal.
5. **NYC LL144 + Illinois AI Video Interview Act overlay** for the Meridian HR AEDT.
   - Minimum: **6 criteria** — AEDT scope match, independent bias audit computation, summary publication, candidate notice (LL144), and Illinois-specific notice/consent, video destruction on request, demographic reporting (Illinois).

**Narrative — overlay-boundary memo** (~800 words).

- Where multiple overlays regulate the *same control* with *different metrics or methods* — pick two concrete examples and reason the auditor's resolution.
- Where an overlay regulates a *process* the baseline treats as optional — pick one example (likely SR 11-7 independent validation vs. ISO/IEC 42001 clause 9.2 internal audit).
- Where the overlay's definition of scope is **narrower or broader** than the baseline (e.g., SR 11-7 "model" vs. ISO/IEC 42001 "AI system"; Colorado "consequential decision" vs. EU AI Act Annex III).
- How you will assemble a single engagement memo for Meridian's CAE that keeps the overlays legible to the Audit Committee without burying the baseline.

## Minimum volume

- At least **5 overlay registers** as above (financial, medical, HIPAA+NAIC, Colorado, HR).
- At least **44 overlay criteria** in total across the registers.
- At least **10 measurable** criteria carrying metric + method + population + tolerance.
- At least **5 criteria** that require an auditor's expert (ML, statistics, clinical, actuarial, or legal) under ISA 620 analogy — flag expert scope.

## Starter guidance

- Each overlay must be *additive*, not duplicative. If a criterion is already present in the horizontal baseline (exercises 01 and 02) and the overlay does not modify it, cite the baseline criterion in the `Baseline-overlap` column and leave the overlay register row blank.
- The medical overlay is where you will push hardest on *representative* training data — GMLP Principle 3 and the FDA's post-market-performance expectations are more stringent than horizontal frameworks' bias testing.
- For HIPAA, the technical safeguards layer onto the organisation's infrastructure security — do not re-author general security criteria, add the PHI-specific extensions.
- For LL144, the independent-bias-audit computation is prescribed; cite the DCWP rules precisely and adopt the prescribed impact-ratio method. Do not substitute a different fairness metric.
- For the Colorado overlay, pay attention to the **deployer vs. developer** distinction — Meridian Specialty Lending is a *deployer*; the AI platform group (shared services) may be the *developer* of controls used across subsidiaries. Author criteria matched to the role.
- The posture memo must argue the auditor's resolution of conflicts between regimes — do not present conflicts as unresolved.

## Acceptance criteria

The deliverables are accepted when:

- All five overlay registers are present and meet the minimum per-register volume.
- Volume thresholds (44 criteria total, 10 measurable, 5 expert-dependent) are met.
- Every row cites a specific regime-level reference (SR letter / SR 11-7 section; GMLP principle number; HIPAA CFR citation; LL144 DCWP rule reference; Colorado statute section).
- Every row carries a `Baseline-overlap` entry linking the overlay to the horizontal baseline — or explicitly states "no baseline overlap — purely additive".
- The posture memo addresses all four narrative prompts with specific regime citations.
- At least one example of an overlay-method conflict (SR 11-7 outcomes-analysis method vs. ISO/IEC 42001 performance-evaluation method, for instance) is resolved with the auditor's reasoning.
- Any reference to a regime's current version, effective date, or applicable scope that is time-sensitive (NAIC state adoption, Colorado effective date, QMSR effective date, OMB memo revisions) is marked `<!-- needs-research: ... -->` if not verified at reading time.

## Stretch goals

- Add a **sixth register** for **OMB M-24-10 + M-25-21** if Meridian were to be a federal contractor delivering AI services to a US agency — scope assumed, author six representative criteria and flag `<!-- needs-research: ... -->` for current OMB status.
- Author the **Meridian engagement memo to the CAE** (~500 words) communicating this overlay landscape in a shape the Audit Committee can read — including a materiality-tier recommendation for annual audit frequency across the regimes.
- Produce a **data-flow diagram** showing which evidence artifact (model card, validation report, incident ticket, impact assessment) serves which overlay criteria, as a visual preview of exercise 05.
- Draft the **UK FCA** overlay criteria for the Specialty Lending model if the subsidiary ever expanded into UK operations — three to five criteria, flagged `<!-- needs-research: ... -->` where UK sector-regulator guidance has moved.
