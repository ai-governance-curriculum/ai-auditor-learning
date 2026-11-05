# exercise-02: Audit Priority Scoring and Annual Plan

**Estimated effort:** 2.5 hours

## Objective

Starting from the AI audit universe built in exercise-01, score the universe against the chapter-2 priority equation, defend a weighting scheme, and author the one-cycle annual AI audit plan the CAE would submit to the audit committee for approval. The deliverable is a scored universe, a one-page weighting memo, the plan itself in tabular shape with declined-row annotations, and a two-page audit-committee cover memo in the CAE's voice (for the AI-audit section only).

## Prerequisites

- Chapter [`01-the-ai-audit-universe.md`](../01-the-ai-audit-universe.md)
- Chapter [`02-audit-priority-scoring-and-annual-plan.md`](../02-audit-priority-scoring-and-annual-plan.md)
- Exercise-01 deliverable (bring your universe forward)

## Scenario

Continues from exercise-01 at **NorthernMutual Life**. Adjust the universe you produced by adding the following facts the audit function has since learned:

- **CT-01 claims-triage model** carried a 2025 finding on evaluation-set representativeness that closed 3 months late. Management response is rated `slow`. Prior external auditor coverage: none. A peer insurer settled a class-action on similar claims-triage last quarter, triggering internal legal interest.
- **CSA-02 customer-service LLM assistant** is in scope for NAIC market-conduct review of insurer AI practices; no inquiry yet but the NAIC bulletin was adopted in-state. No external auditor coverage of the system; the AIMS is targeting Stage-2 at the end of Q4.
- **UW-03 underwriting-support LLM** is in pilot; a mid-cycle residual-risk re-assessment concluded moderate residual on manageable grounds but the first-line has not completed its FRIA (EU AI Act Article 27 analogue for US use).
- **AR-04 agent-routing classifier** was in the inventory for the first time this cycle after being discovered by audit; no prior audit coverage; low volume per decision but high aggregate volume.
- **FR-05 fraud-score model** is retrained monthly; management is responsive; SR 11-7-aligned internal independent validation last performed 2024. The fraud-ops team has been pushing for real-time retraining.
- **Microsoft 365 Copilot** deployment has had one data-leakage incident (confidential underwriting notes echoed into an email draft for a different file) that was contained but reported to the AI Governance Committee. Residual risk flagged elevated.
- **Workday performance-review summarisation** — vendor cert held: SOC 2 Type 2, scope does not mention AI; Workday has not held an ISO/IEC 42001 certificate. The HR director has pressed audit to confirm the feature is safe.
- **Legacy identity-provider anomaly scoring** — classification unclear; security-team owner believes it is not in Annex III scope; audit disagrees pending analysis.
- **GPAI usage — Anthropic Claude via Bedrock** — the Anthropic ISO/IEC 42001 certificate and the organisation's Bedrock provisioning is documented; vendor SOC 2 held; EU AI Act Article 53 provider obligations attach to Anthropic, not to NorthernMutual. Downstream deployer obligations (transparency, record-keeping, incident reporting) attach to NorthernMutual.
- The audit function has **1,850 planned hours** of AI-audit capacity for the cycle after subtracting mandatory financial-statement audit support and continuous-audit overhead. Reserve for unplanned work: 20% (370 hours). Net available to the AI-audit plan: **1,480 hours**.

## Requirements

1. **Score every universe row** using the chapter-2 eight-term equation. For each row, produce numeric bands on inherent risk, residual risk, audit coverage debt, management response, regulator attention, external auditor coverage, change velocity, and auditability. Document the band-to-number convention you use.
2. **Choose and defend a weighting scheme** — risk-weighted, coverage-weighted, or your own. Produce a one-page weighting memo explaining the choice against this organisation's facts (first-cycle AI function, ISO/IEC 42001 certification path in flight, recent incident on Copilot, peer class-action heat on CT-01).
3. **Produce the ranked universe** — one table, sorted by priority score, with per-row score and band.
4. **Author the annual plan** — accept engagements top-down until the 1,480 hours are spent. For each accepted engagement, name:
    - engagement name and subject matter
    - engagement type (full audit, limited-scope, follow-up, advisory, continuous-audit cycle)
    - lead auditor assignment (notional, e.g., "Senior AI Auditor A")
    - specialist needs (ISA 620 roles) — ML specialist, security, legal, sector specialist
    - estimated hours
    - timing window (quarter)
    - deliverable shape (internal audit report, ISO/IEC 42001 pre-certification internal audit, limited-scope memo)
5. **Declined-row list** — every universe row not accepted into the plan, with its priority band and the next-cycle treatment (defer to next cycle; monitor via continuous audit; rely on external coverage; etc.).
6. **Author the AI-audit section of the CAE's audit-committee cover memo** (≤ 2 pages, Markdown). Written in the CAE's voice. Must cover: methodology summary with weighting rationale; plan summary with capacity analysis; declined-row list with risk-band distribution; resource-gap statement if your capacity is insufficient for all critical-band work; external-assurance coordination for the cycle (chapter 7 §4); expected rhythm of quarterly reporting on AI-audit workstream status; the one most contentious trade-off you made and your defence of it.

## Starter guidance

- Reuse the `ai-risk-engineer` (L25) inherent-risk shape conceptually — do not re-invent a risk model for this exercise. Pick inherent-risk bands based on affected population, modality, autonomy, data sensitivity, and regulatory classification.
- Residual risk should reflect the control environment facts in the scenario; do not grade residual on inherent alone.
- Audit coverage debt is zero for a never-audited row where the target cycle has not elapsed; it is meaningfully positive for `CT-01` (target 12 months at high band; last audit 14 months ago in the scenario of exercise-01).
- The Copilot deployment is a trap — high change velocity (vendor-driven monthly), recent incident, 2,100 users, but auditability is complex because it is a managed service. Score auditability honestly and write up the auditability caveat in the plan.
- Capacity math matters. A single full ISAE-3000-flavoured AI-system audit is ≈ 400–600 hours; an AIMS internal audit is typically 600–1,000 hours; a follow-up is 80–150; a continuous-audit cycle is a per-quarter allocation. If you try to fit six full audits into 1,480 hours you are under-estimating.
- The CAE cover memo is in the CAE's voice. Do not slide into the AI Auditor's voice; chapter 7 is explicit on this.
- `<!-- needs-research -->` placeholders are fine where the scenario legitimately underspecifies.

## Acceptance criteria

- Every universe row from exercise-01 appears in the ranked universe with scores and bands.
- The band-to-number convention is defined once and applied consistently.
- The weighting memo defends the weights against the specific organisation facts (not against a generic template).
- The plan is capacity-bounded — accepted engagements fit within the 1,480 hours with 20% reserve not touched by the baseline plan.
- Every declined universe row is named with band and next-cycle treatment.
- At least one critical-band row is either accepted or has a declared capacity gap in the CAE memo (dropping a critical-band row silently is a fail).
- The CAE cover memo is written in the CAE's voice, restricts itself to enterprise-level language, and defers specialist content to the plan appendix.
- External-assurance coordination (ISO/IEC 42001 Stage-2 path; vendor SOC 2; Anthropic cert reliance) is addressed, not ignored.
- Chapter-5 awareness: the AIMS audit engagement, if accepted, is scoped as `internal audit under clause 9.2`, not as a certification audit (the audit function cannot certify).
- No fabricated materiality thresholds, regulator actions, or enforcement precedents.

## Stretch goals

- Produce a **sensitivity analysis** — rerun the scoring with the alternative weighting scheme (coverage-weighted if you chose risk-weighted, or vice versa). Report how the plan changes and which rows cross the capacity line. Add a paragraph to the CAE memo explaining the robustness of your pick.
- Propose a **continuous-audit candidate** — one engagement that would move from annual to continuous audit, with the trigger metrics, expected hour reduction, and governance pattern.
- Draft the **universe-change-log entry** for the plan-approval event itself: the plan becomes a reference point for the next cycle; what you commit to tracking forward.
