# The Crosswalk Register — One Evidence Artifact, Many Criteria

## Motivation

An organisation under audit rarely faces one regime alone. A large AI deployer in a regulated sector may be simultaneously in scope of ISO/IEC 42001, NIST AI RMF, EU AI Act, SR 11-7, FDA QMSR, NAIC Model Bulletin, NYC LL144, and its own internal AI policy. The naive approach — run a parallel audit per regime — produces duplicated evidence requests, duplicated findings, and an audit cost the sponsor will not pay. The disciplined approach is a **crosswalk register**: a single matrix that maps every control (or every evidence artifact) to every criterion it satisfies across every framework in scope. Build the register once at engagement planning and the engagement becomes tractable; omit it and the engagement over-tests some controls and under-tests others. This chapter is the register's architecture, authoring discipline, and governance. It explicitly re-uses the enterprise control-library architecture owned by `senior-ai-governance-architect` (level 50) — the auditor does not re-author the library, the auditor audits against it.

## What the crosswalk register is — and is not

The register *is*:

- A matrix whose rows are **controls or evidence artifacts** (the organisation's control library row IDs), and whose columns are **framework criteria IDs** (from chapters 2–5 of this module).
- A record of *which framework obligations each control helps satisfy*, with cell content capturing the degree (fully satisfies / partially satisfies / supports with other controls) and the specific clause/article/subcategory/control-objective cited.
- A living artifact updated when either side changes — regulations amend, control library evolves, new AI systems enter scope.

The register *is not*:

- A substitute for the audit test itself. A cell marked "fully satisfies C-42001-6.1.2-01 → GOVERN 1.1 → Art 9" says nothing about whether the control *actually operates*; that's what fieldwork is for.
- A one-way map. It is bidirectional: starting from the control you can find every criterion it supports; starting from the criterion you can find every control that supports it.
- Something the auditor should author de novo inside the engagement. For any organisation above the smallest tier, the `senior-ai-governance-architect` (L50) role (or the equivalent in-house control owner) has authored it. The auditor **tests the register for suitability** and consumes it; where it is missing or inadequate the first finding is often the register itself.

## The reference architecture — a control library the auditor audits against

The `senior-ai-governance-architect` (L50) curriculum designs an enterprise control library that typically contains:

- **Policy taxonomy** — the organisation's AI policy, sub-policies, and standards, hierarchically organised.
- **Control catalogue** — numbered controls with control objective, control statement, control type (preventive / detective / corrective), owner, frequency, evidence expectations.
- **Policy-to-control-to-evidence map** — which controls implement which policy; which evidence artifact proves which control.
- **Framework crosswalk layer** — the control-to-framework-criteria columns in the register this chapter constructs.
- **Exception register** — approved deviations with expiry dates and compensating controls.
- **Change log** — control additions, retirements, amendments.

The AI Auditor's position: *audit against the control library, not against the framework directly* — because the organisation is accountable for implementing the framework through its own controls, and its controls are what the auditor can test. The framework comes in through the crosswalk.

## Row design — anchor on the organisation's control or the evidence artifact

There are two defensible row designs; most engagements use both.

### Design A — rows are **controls** (the architect's native unit)

Rows are the control-library control IDs. Each row carries:

- Control ID, title, objective, type, owner, frequency.
- The populations the control applies to (e.g., all AI systems in scope; only GenAI; only Annex III high-risk; only models above materiality tier 2).
- Evidence artifacts expected (document, log, metric, record).
- Framework columns (ISO/IEC 42001, NIST AI RMF, EU AI Act, applicable sector overlays, internal policy).
- Cell content per framework: criterion IDs the control helps satisfy, with a short qualifier ("fully", "partially", "supporting") and the clause/article citation.

Use Design A when the engagement scope is **the organisation's AIMS** — testing whether the organisation's control library covers the framework obligations in scope.

### Design B — rows are **evidence artifacts** (the auditor's native unit)

Rows are concrete evidence artifacts that exist: this specific model card, this specific evaluation report, this specific risk register entry, this specific incident ticket, this specific SoA. Each row carries:

- Artifact ID, system of record, retention location, owner.
- The controls it supports (link back to Design A rows).
- Framework-criterion columns, same as above.
- Test history: when was this artifact last tested, by whom, under which criteria, with which result.

Use Design B when the engagement scope is **specific AI systems** (e.g., three high-risk systems for EU AI Act readiness) — the audit navigates by artifact, not by abstract control.

A mature engagement produces both and keeps them joined.

## Column design — frameworks, overlays, and the internal policy column

Baseline columns:

- **ISO/IEC 42001 clauses + Annex A controls** — one logical column that resolves to clause-level and control-level citation cells.
- **NIST AI RMF Subcategories** — including a sub-column for GenAI Profile risks when in scope.
- **EU AI Act Articles + harmonised standards** where cited.
- **Applicable sector / jurisdictional overlays** — SR 11-7, FDA QMSR, NAIC, Colorado, LL144, OMB M-24-10/M-25-21, UK sector regulator, Singapore AI Verify, etc. One column per overlay in scope; absent when not in scope.
- **Internal AI policy clauses** — because the organisation is accountable to its own policy and the auditor should surface gaps between internal policy and external frameworks.

For each criterion cited in a cell, carry four bits of metadata:

- **Citation** — framework + clause/article/control ID (the stable reference).
- **Degree** — fully / partially / supports.
- **Linked criterion ID** — the auditable-criterion ID from chapters 2–5 (your module's internal reference).
- **Evidence location** — where in the artifact store the supporting evidence is filed, so fieldwork does not re-search.

## Degree of satisfaction — avoid the naive "X" check

A cell marked with a plain "X" collapses too much. Use a three-value shorthand (fully / partially / supports) and spell it out:

- **Fully** — the control (or the artifact) is sufficient on its own to satisfy the criterion; no other control is needed. Rare for complex criteria.
- **Partially** — the control is necessary but not sufficient; the criterion requires N controls operating together. The register should name the other controls in the cell's notes so the auditor tests all N.
- **Supports** — the control contributes evidence toward the criterion but is not necessary; the criterion could be satisfied without it by an alternative path.

The reason to be explicit: a "partially" cell that the auditor tests in isolation and finds operative does **not** mean the criterion is satisfied — one of the other N controls might not operate. The discipline prevents false passes.

## Worked example — one control, four framework columns

Let the organisation's control **CL-EVAL-01** be: "Each release of each in-scope AI system is gated by a documented evaluation against defined metrics, with sign-off by named release-assurance approver; eval artifacts retained ≥7 years."

```
Control ID:       CL-EVAL-01
Title:            Release-gate evaluation
Objective:        Prevent release of systems failing defined performance/safety thresholds
Type:             Preventive
Owner:            Release-assurance lead (L35 second line)
Frequency:        Every release (model, prompt system, policy)
Population:       All AI systems in production scope
Evidence:         Eval plan, eval run logs, metrics output, release-gate sign-off record, retention proof

Framework satisfaction:
  ISO/IEC 42001 (Annex A, life-cycle):
    - Annex A verification/validation control(s)  — Fully  — C-42001-AnnexA-VV-01
    - Clause 8.3 (operation / risk treatment)     — Partially — C-42001-8.3-01 (requires companion risk-treatment control)
    - Clause 9.1 (monitoring/measurement)         — Supports — C-42001-9.1-01
  NIST AI RMF:
    - MEASURE 2.3                                 — Fully     — C-NIST-MEASURE-2.3-01
    - MEASURE 2.7 (security/resilience)           — Partially — C-NIST-MEASURE-2.7-01 (requires adversarial-test control CL-SEC-03)
    - MANAGE 4.1 (post-deployment monitoring)     — Supports  — C-NIST-MANAGE-4.1-01
  NIST GenAI Profile:
    - Information security risk (prompt-injection) — Partially — C-NIST-GENAI-INFOSEC-01 (with CL-SEC-03)
    - Confabulation risk                           — Partially — C-NIST-GENAI-HALLUCINATION-01 (with grounding-check control)
  EU AI Act (high-risk scope):
    - Art 15(2) declaration of accuracy            — Fully     — C-AIACT-15-ACCURACY-01
    - Art 15(4) robustness                         — Partially — C-AIACT-15-ROBUSTNESS-01 (with CL-SEC-03)
    - Art 11 + Annex IV technical documentation    — Supports  — the eval artifact feeds the Annex IV content
  SR 11-7 (where in scope):
    - Validation / outcomes analysis               — Supports  — not sufficient alone; independent-validation control CL-MRM-04 is required

Internal AI policy mapping:
  - AI-POL §4.2 (release discipline)              — Fully
  - AI-POL §6.1 (post-market monitoring)          — Supports
```

Note how the same control fully satisfies some criteria, partially satisfies others, and supports still others. The register captures that mesh explicitly. The auditor's workpaper picks up every "partially" cell and tests the companion controls as a bundle.

## Authoring pattern — three passes, then maintain

### Pass 1 — Source-to-criteria (chapters 2–5 output)

Per framework in scope, enumerate the criteria you authored in chapters 2–5. These become the cell targets.

### Pass 2 — Control-to-criteria

For each control in the architect's control library, walk the applicable framework columns and fill in cells with citation + degree + linked criterion ID + evidence location. Where no control covers a criterion, raise an *architect-side finding*: control library has a gap against this framework obligation.

### Pass 3 — Artifact-to-control (Design B join)

For each artifact category (model cards, eval reports, risk register, incident tickets, SoA, technical documentation), link to the controls that produce or consume it. This is where the engagement's evidence-collection plan is built — one artifact request, multiple criteria tested.

### Maintenance

- Re-execute **Pass 1** whenever a framework amends (EU AI Act secondary legislation, harmonised standard publication, NIST AI RMF revision).
- Re-execute **Pass 2** whenever the control library changes (new control, retirement, scope change).
- Re-execute **Pass 3** when new AI systems enter scope or old systems retire.

The `ai-governance-analyst` (L15) does the mechanical refresh work; the auditor validates applicability.

## Testing the register itself

The register is itself an auditable artifact. Criteria over the register:

```
Criterion ID:             C-CROSSWALK-01
Statement:                The crosswalk register addresses every in-scope framework; for each framework, every criterion maps to at least one control or an explicit gap; every control in the library maps to at least one framework or internal-policy clause; every cell carries citation, degree, linked criterion ID, and evidence location; the register has been updated within the defined cadence and after each framework or library change recorded in the change log.
Evidence:                 Register itself; change log; refresh approvals; sampled cells traced to source documents.
Procedure:                Inspect register; sample cells and test the citation, degree, linked criterion, and evidence pointer; verify refresh timeliness.
Measurable attributes:    Coverage of framework (%); coverage of control library (%); cell completeness (%); refresh age.
Owner:                    Second line (architect) authors; auditor tests.
Residual judgment:        Guard against "mapped" cells where the control does not actually satisfy the criterion — partial / supports / full misuse is common.
```

## Tool choice — register in what form

The register is normally held in one of:

- A **GRC tool** (ServiceNow IRM, Archer, LogicGate, OneTrust, AuditBoard, Hyperproof) with control-library and criteria mapping modules.
- A **governance spreadsheet** for smaller deployments (CSV / Excel / Airtable / Notion) — brittle at scale but tractable.
- A **model-card / card-stack pattern** (using Google's Model Cards tooling, or the OECD / NIST crosswalk tooling as it stabilises) <!-- needs-research: confirm which open tooling has stabilised for cross-framework control mapping at reading time -->.

The auditor should not opine on tool choice; the auditor should confirm the tool actually enforces the register's governance (versioning, access control, approval workflow, change log).

## Where NIST and other bodies have already done the work

Re-use rather than re-author the published crosswalks:

- **NIST AI RMF ↔ ISO/IEC 42001** — NIST crosswalk.
- **NIST AI RMF ↔ ISO/IEC 23894** — NIST crosswalk.
- **NIST AI RMF ↔ OECD AI Principles** — NIST crosswalk.
- **NIST AI RMF ↔ EO 14110 / OMB M-24-10 / M-25-21** — NIST / OMB cross-references.
- **CEN/CENELEC JTC 21 harmonised standards ↔ EU AI Act Articles** — presumption-of-conformity mapping.
- **NAIC Model Bulletin ↔ NIST AI RMF** — the bulletin's explicit alignment to the RMF structure.
- **IIA AI Auditing Framework ↔ ISO/IEC 42001, NIST AI RMF** — IIA has published cross-reference tables.

Pull these into Pass 1 as *starting points*. Validate each row at reading time because versions move.

## Pitfalls (the ones that actually cost engagements)

- **Mapping to the wrong level of granularity.** Mapping to "Article 15" with no sub-clause reference or to "GOVERN 1" with no Subcategory produces a register that cannot drive fieldwork. Map to the leaf.
- **"Fully" over-claims.** A control that produces evidence feeding a criterion is not "fully" satisfying it unless the criterion depends on no other control. Err toward "partially".
- **Silent omissions.** A criterion with no mapped control should appear in the register as an explicit gap, not as a blank row.
- **Stale cells.** A framework amended two years ago still showing the old citation is worse than absent — it misleads fieldwork. Freshness is a criterion of the register.
- **Duplicates of the architect's work inside the audit scope.** If you find yourself authoring the control library during the engagement, you have ceded independence — stop, raise a scope issue, and see `mod-101` chapter 1.

## Summary

- The crosswalk register maps the organisation's control library to every framework criterion in scope, so one evidence artifact drives multiple criteria tests.
- Design A rows (controls) suit AIMS-wide scope; Design B rows (artifacts) suit system-specific scope; mature engagements join both.
- Cell content carries citation, degree (fully/partially/supports), linked criterion ID, and evidence location — not a bare "X".
- The `senior-ai-governance-architect` (L50) authors and maintains the register; the AI Auditor audits it for suitability and completeness.
- Re-use NIST, CEN/CENELEC, NAIC, and IIA published crosswalks as Pass-1 starting points; validate at reading time.
- The register is itself an auditable artifact — add criteria over it and test it like any other control.
