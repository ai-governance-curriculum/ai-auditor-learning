# exercise-01: AI Audit Universe From AI Inventory

**Estimated effort:** 2 hours

## Objective

Construct a defensible AI audit universe for a fictitious organisation by translating a provided analyst-tier AI inventory plus adjacent discovery sources into the schema from chapter 1. Represent all five populations (internal, deployed, third-party procurement, embedded AI, GPAI usage), reconcile against a prior-year universe, and produce the universe-change log the audit committee would receive. The deliverable is a universe spreadsheet (or YAML/CSV) plus a one-page memo on discovery methodology.

## Prerequisites

- Chapter [`01-the-ai-audit-universe.md`](../01-the-ai-audit-universe.md)
- Working familiarity with ISO/IEC 42001:2023 clause 6.1.4 (AI system impact assessment) and the EU AI Act Article 11 (technical documentation) inventory obligations
- `mod-102` chapter 4 (EU AI Act articles-to-criteria) for regulatory-classification semantics

## Scenario

**NorthernMutual Life** (the fictitious US life insurer from `mod-101` exercise-01) is now one cycle into AI-audit function stand-up. The new AI Auditor has been handed:

- The **AI analyst inventory** maintained by `ai-governance-analyst` (level 15), covering AI systems as recorded in the AIMS clause-6.1.4 register. Twelve rows.
- A **procurement AP extract** of all vendor spend tagged "AI" or "ML" over the last 24 months. Nine distinct vendors, of whom six are already in the analyst inventory.
- A **cloud-spend tagging extract** from AWS / Azure showing Bedrock, Azure OpenAI, and SageMaker consumption across 18 application cost centres.
- An **API-gateway scan** showing egress calls to `api.anthropic.com`, `api.openai.com`, `generativelanguage.googleapis.com`, and `api.mistral.ai` from 23 distinct application clusters.
- A **security-review intake log** showing 11 third-party tool reviews over the period, of which 4 note "AI features present".
- The **prior-year AI audit universe** (14 rows) from the predecessor acting-AI-Auditor before this role was formally staffed.

### Inventory — internal systems (paraphrased from `mod-101`)

- **Claims-triage ML model (CT-01)** — classification; retrained quarterly; 2.1M decisions/year; affects all life-claims claimants.
- **Customer-service LLM assistant (CSA-02)** — retrieval-augmented over policyholder documents; uses Anthropic Claude via Bedrock; ~400K sessions/year; deployed since 2025-Q2.
- **Underwriting-support LLM (UW-03)** — pilot; summarises applicant medical records for human underwriters; uses Azure OpenAI GPT-4-class model; ~800 sessions/month in pilot.
- **Agent routing classifier (AR-04)** — routes incoming calls; 4M decisions/year; classical ML, in production since 2019, not previously in the analyst inventory until 2026-Q1.
- **Fraud-score model (FR-05)** — flags suspicious claims; 1.1M decisions/year; retrained monthly on a feedback loop with the fraud-ops team.

### Inventory — vendor / deployed systems

- **Workday** — HR platform; the organisation uses its AI-based performance-review summarisation feature (launched 2026 by vendor).
- **Salesforce Einstein** — used in sales for opportunity scoring.
- **DataRobot** — used by the underwriting team for a pricing model (procured 2024).
- **Microsoft 365 Copilot** — deployed across 2,100 staff since 2026-Q1; email draft, document summarisation.
- **ServiceNow Now Assist** — AI features in the ITSM instance; deployed by IT in 2026-Q3.
- **A legacy identity-provider** — the vendor added anomaly-based risk scoring in a 2025 release; not previously flagged as AI by procurement.

### Prior-year universe (abridged)

14 rows covering the first three internal systems; Workday, DataRobot, Salesforce Einstein; Microsoft Copilot (added mid-year); three ambiguous "AI governance programme" rows (AIMS internal audit, AI policy audit, impact-assessment process audit); and a GPAI-usage row for Anthropic Claude across all applications.

## Requirements

1. **Build the universe spreadsheet / YAML file** with all rows covering the five populations. Use the chapter-1 schema. Minimum columns required: `universe_id`, `title`, `population`, `auditable_unit_type`, `owner_first_line`, `owner_second_line`, `in_inventory`, `inventory_source`, `regulatory_classification`, `intended_purpose`, `deployment_posture`, `affected_population`, `decision_volume`, `modality`, `data_sensitivity`, `autonomy_level`, `change_velocity`, `prior_audit_coverage`, `prior_findings_open`, `management_response_hist`, `regulator_attention`, `external_auditor_coverage`, `notes`.
2. **Apply the five-population rule** — every row is tagged to exactly one of {internal, deployed, third-party-procurement, embedded, gpai-usage}. Explain the rule you used to handle GPAI used *inside* an internal system (represent the GPAI as an attribute of the internal row, or as a separate cross-cut row with cross-reference — pick one and justify).
3. **Reconcile against the prior-year universe** — for each prior row, mark it as retained, deleted (with reason), re-classified (with old → new), or merged (with target). For each new row, mark its discovery source. Produce the **universe-change log** as a separate sheet / document.
4. **Verify three rows with notional owners** — pick three rows whose classification was ambiguous; write the one-paragraph verification-interview prompt you would take to the first-line and second-line owner, and document the expected evidence you would ask for to confirm classification.
5. **Author the discovery-methodology memo** (≤ 600 words, Markdown). Cover: the discovery pipeline you would run every year (chapter 1 steps 1–7), where embedded AI discovery is weakest in this organisation and how you would strengthen it, how you would handle GPAI usage going forward, and how you will keep the universe diff-readable in version control.

## Starter guidance

- Start from the prior-year universe as a scaffold; do not treat it as truth — challenge every row.
- The legacy identity-provider is the archetypal "embedded AI" discovery case. Show your working on how you found it, how a future-you would find similar silent additions.
- `Microsoft 365 Copilot` straddles populations — the organisation deploys it, but it also drives GPAI usage through the OpenAI/Microsoft pipeline. Pick the convention from requirement 2 and apply it consistently.
- For `AR-04` (the 2019 classical-ML classifier that just made the inventory in 2026-Q1) — this is discovery-via-audit, not discovery-via-inventory. Record it correctly in the change log.
- Pilot systems (e.g., UW-03) belong in the universe tagged `pre-production`; do not drop them because they are not live.
- Multiple rows will need `<!-- needs-research -->` placeholders where the scenario does not supply enough detail (e.g., exact regulatory classification for a deployed vendor feature). Use the placeholders rather than invent.
- The `ai-governance-programme` rows in the prior universe should be interrogated — are they *auditable units* at the AIMS-component level (AI policy, risk-assessment process, impact-assessment process, management review), or are they vague? Re-classify or merge as needed.

## Acceptance criteria

The deliverable is accepted when:

- Every row of the universe carries all the required schema columns (empty cells with `<!-- needs-research -->` are acceptable where the scenario does not provide data; blank cells are not).
- All five populations are represented, and the convention for GPAI-inside-internal-systems is stated and applied consistently.
- The universe-change log accounts for every row of the prior-year universe (retained / deleted / re-classified / merged) and marks the discovery source for every new row.
- The verification-interview prompts name a first-line and a second-line interviewee with the specific evidence to be requested from each.
- The discovery-methodology memo explicitly addresses embedded-AI discovery weakness, GPAI-usage handling, version-control diff-readability, and the annual cycle (chapter-1 steps 1–7).
- At least one `<!-- needs-research -->` marker appears where the scenario legitimately underspecifies a field.
- No fabricated statutes, regulators, or metrics appear.
- The universe does not re-author the analyst inventory — if the inventory is wrong, that is a finding, not a fix.

## Stretch goals

- Author a **universe validation query** — pseudo-code or SQL for a monthly job that compares the universe against the API-gateway scan and procurement AP extract and flags new rows for triage.
- Add **capacity annotations** per row — your rough estimate of audit hours required to do a full engagement, so the chapter-2 scored plan step can consume the universe directly.
- Propose a **one-slide audit-committee view** of the universe that aggregates up to a reporting shape the CAE would use in the quarterly report (chapter 7 §3.2).
