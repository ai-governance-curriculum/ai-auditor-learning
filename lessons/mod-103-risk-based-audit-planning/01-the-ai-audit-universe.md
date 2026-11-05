# The AI Audit Universe — Constructing It from the AI Inventory

## Motivation

Risk-based audit planning starts with a defensible *audit universe* — the complete, bounded, documented population of auditable units the audit function could examine within the next planning cycle. IIA Global Internal Audit Standards 2024 Domain IV (Managing the Internal Audit Function) requires the Chief Audit Executive (CAE) to develop a methodology to plan engagements that aligns with the organisation's strategies, objectives, and risks; ISO 19011:2018 clause 5 asks the audit programme owner to determine the extent of the programme from "objectives, scope, risks and opportunities". Neither standard will accept "we audit what we are asked to". The AI audit universe is the bounded list from which the annual plan draws, the engagement committee can see the trade-offs, and the audit committee can challenge omissions.

For AI the universe does not exist until the auditor constructs it. The organisation's AI inventory — owned by the `ai-governance-analyst` (level 15) under ISO/IEC 42001 clause 6.1.4 / EU AI Act Article 11 / OMB M-24-10 agency-inventory obligations — is the *input*. It is not yet an audit universe. The analyst inventory optimises for completeness of the AI-system catalogue; the audit universe optimises for completeness of the *auditable scope*. The two are different populations, and this chapter is about the translation.

## What the AI Auditor is building, in one sentence

> The AI audit universe is the annotated, bounded, stable-period population of **auditable units** (AI systems, AI programmes, AI processes, AI third-party relationships, AIMS components) over which the audit function can run inherent-risk + residual-risk scoring, engagement selection, and coverage reporting.

The unit of the universe is not "AI system" — it is "auditable unit". An auditable unit is anything the audit function can scope an engagement around: a single production AI system, a group of similar systems under a shared control environment, a procurement programme, an AIMS clause, a vendor relationship, a GPAI model used across many applications. The universe therefore includes rows that are *not* individual AI systems, which is why the analyst inventory alone cannot be the universe.

## The five populations the universe must cover

The learning objective names five populations the audit function must represent. Each is sourced differently and audited differently, and skipping any one creates a defensible-planning gap the audit committee will find. In the order of discovery difficulty:

### 1. Internal AI systems (built and operated in-house)

- Source: the analyst inventory (ISO/IEC 42001 clause 6.1.4 inventory, EU AI Act Article 11 technical documentation registry, model registry extracts, MLflow / Vertex / SageMaker / Databricks registries, internal AI governance committee minutes).
- Inherent-risk signals readily available: use case, affected population, decision volume, modality, autonomy level, data sensitivity, deployment environment.
- Auditable unit: typically the AI system, or a bundle of systems under one owning product team if controls are shared.
- Watch-out: *shadow* internal systems — notebooks promoted to production, Excel-with-ML, retrieval pipelines built as scripts — are often missing from the analyst inventory. The universe should name a method for discovering these (purchase-card data, GPU-utilisation logs, API-gateway telemetry, developer-platform scans).

### 2. Deployed AI systems (the organisation acts as a deployer under EU AI Act Article 26, or operates an AI system built by another provider)

- Source: the analyst inventory plus procurement records, contract register, OneTrust / RiskRecon-style vendor registers, finance AP for AI-labelled spend.
- The auditable obligations here are *deployer* obligations — Article 26 human oversight, Article 27 FRIA, record-keeping, incident reporting — not provider obligations. The universe should tag deployer vs. provider posture per system because it changes the criteria set from `mod-102`.
- Watch-out: an AI system can be both deployed-from-vendor *and* customised in-house to the point where the deployer takes on provider obligations (EU AI Act Article 25). Flag these for scoping in `mod-104`.

### 3. Third-party AI procurement (standalone AI products the organisation buys and deploys)

- Source: contract management system, SIG / SIG Lite vendor assessments, procurement intake forms, security questionnaire responses, vendor SOC 2 / ISO/IEC 27001 / ISO/IEC 42001 certificates held by the vendor-management office.
- Auditable unit: often the *vendor relationship*, not the AI system — the procurement controls (pre-engagement DD, contract clauses, ongoing monitoring, exit) are what the audit tests.
- Watch-out: differences between the vendor's claimed scope and the organisation's actual use; the vendor SOC 2 may cover payroll but not the vendor's AI features.

### 4. Embedded AI inside non-AI vendors

- Source: hardest of the five. A non-AI vendor silently adds an AI feature — the ticketing tool now has a GPT-powered summariser; the identity provider added anomaly detection; the content-management system runs a recommender. None of this appears on a procurement intake form that asked "is this an AI product?" two years ago.
- Discovery methods: vendor change-notification review, release-note monitoring, periodic vendor outreach ("have you added AI features?"), third-party risk management refresh cycles, subprocessor list scans in DPA registers, security review of OAuth scopes and data flows.
- Auditable unit: the vendor relationship with the AI-feature annotation. For materiality scoring, the annotation flips an already-approved relationship into AI scope — often without a change in contract, cost, or data flow, which is exactly why discovery fails.

### 5. GPAI model usage (foundation-model calls across the application portfolio)

- Source: API-gateway logs for OpenAI / Anthropic / Google / Mistral / Cohere / Azure OpenAI / Bedrock / Vertex endpoints, developer-platform scans, IaC repositories for `anthropic`, `openai`, `@anthropic-ai/sdk`, `google-generativeai`, `vertexai`, `boto3 bedrock`, `azure-ai-openai` imports, cloud-spend tagging.
- Auditable unit: *the GPAI model, cross-cut across all applications that use it* — the auditable obligations under EU AI Act Articles 53 and 55 (GPAI provider obligations, systemic-risk GPAI obligations) are on the provider, but the *deployer's* obligations (transparency to end users, downstream disclosure, usage monitoring) are cross-cut across applications. A row of the universe for "Anthropic Claude 3.5 Sonnet used across 47 applications" is a legitimate auditable unit even though no single application is big enough to appear on its own.
- Watch-out: duplicate rows between this population and populations 1–3. A GPAI model used *inside* an in-house system should either appear as a row here (and the in-house system row cross-references it) or appear only as an attribute on the in-house system row — pick one convention in the universe schema and apply it.

## The universe schema — the row-level attributes

Each row of the audit universe should carry enough attributes to drive the priority scoring in `02-audit-priority-scoring-and-annual-plan.md`. Suggested minimum columns:

```
universe_id              : stable identifier, prefix by population (INT-, DEP-, PROC-, EMB-, GPAI-)
title                    : short descriptive name
population               : one of {internal, deployed, third-party-procurement, embedded, gpai-usage}
auditable_unit_type      : one of {single-system, system-group, programme, process, vendor-relationship, aims-component, gpai-cross-cut}
owner_first_line         : accountable first-line owner (team or role)
owner_second_line        : accountable second-line owner (risk, compliance, MRM, AIMS owner)
in_inventory             : y/n (did it come from the analyst inventory, or was it discovered by audit?)
inventory_source         : e.g., "model_registry:prod", "oneTrust:VENDOR-1234", "api_gateway_scan:2026-Q3"
regulatory_classification: EU AI Act Annex III category / prohibited / limited risk / minimal risk / GPAI; US sector overlays; Colorado AI Act in-scope y/n; NYC LL144 AEDT y/n
intended_purpose         : short text; used for criteria mapping
deployment_posture       : one of {provider, deployer, both, pre-production}
affected_population      : count or band of individuals affected by the system's decisions
decision_volume          : decisions per period
modality                 : one of {classical-ml, deep-learning, llm, multimodal, agentic, gpai-foundation-model}
data_sensitivity         : one of {public, internal, confidential, restricted, special-category/PHI/biometric}
autonomy_level           : one of {human-in-the-loop, human-on-the-loop, human-out-of-the-loop}
change_velocity          : one of {static, infrequent-retrain, continuous-learning, online-learning}
prior_audit_coverage     : date and type of prior audit / assurance coverage
prior_findings_open      : count, with severity
management_response_hist : one of {reliable, slow, disputed, unresponsive}
regulator_attention      : tagged regulators with current posture (e.g., NAIC market-conduct inquiry open)
external_auditor_coverage: external assurance reports naming the unit
notes                    : free text for discovery caveats, cross-references, duplications
```

The schema will be refined as inherent-risk and audit-specific drivers are added in the next chapter; keep the universe file in a format diffable in version control (CSV, YAML, or a lightweight database) so rolling updates are auditable.

## Boundary with adjacent roles — do not re-author what already exists

- The **AI inventory** itself is `ai-governance-analyst` (level 15) work under ISO/IEC 42001 clause 6.1.4. The AI Auditor is a *consumer*. If inventory refresh is slow, the audit finding is that the inventory is slow — the auditor does not fix it in-flight.
- The **inherent-risk scoring shape** is `ai-risk-engineer` (level 25) work. The AI Auditor reuses the risk-engineer's shape for the inherent-risk column of the universe rather than re-inventing a scoring system. The audit-specific overlay (prior findings, management response, regulator attention, external coverage, change velocity, auditability) is what the auditor adds on top — covered in chapter 2.
- The **AIMS design** (clauses 4–10 of ISO/IEC 42001 as implemented at this organisation, the control library, the Statement of Applicability) is `senior-ai-governance-architect` (level 50) work. The audit universe includes AIMS components as rows (the AI policy, the risk-assessment process, the management-review cycle, the impact-assessment process) but the auditor does not design or own them.
- The **CAE** owns the audit programme at enterprise scope. If the AI audit universe plugs into an enterprise universe (finance, operations, IT, third-party, AI), the plug-in point is a CAE-level decision — covered in chapter 7.

## Universe discovery methodology — a repeatable cycle

A defensible universe is not a one-shot build; it needs a cycle the auditor can re-run and the audit committee can see. A workable annual cycle:

1. **Pull** the analyst inventory as the starting point (frozen snapshot with a date tag).
2. **Enrich** with procurement, contract, finance-AP, security-review, API-gateway, developer-platform, and cloud-spend-tag extracts.
3. **Reconcile** against the prior-year universe — flag additions, deletions, re-classifications, inventory-orphans (in audit universe, not in inventory) and audit-orphans (in inventory, not yet in audit universe).
4. **Classify** each row to the five populations and the schema attributes.
5. **Verify** a sample with owners (first-line and second-line) — a ten-minute conversation per sampled row catches most misclassifications cheaply.
6. **Approve** with the CAE before scoring.
7. **Freeze** the universe for the planning cycle; log any mid-cycle additions as universe-change entries, not retroactive edits.

Steps 3–5 are where orphans are found. Steps 2 and 5 are where "embedded AI" (population 4) is discovered; without step 2, embedded AI will be missed.

## Common failure modes

- **One row per AI system, no exceptions.** Collapses programmes, cross-cut GPAI usage, and vendor relationships into the wrong unit. The scoring in chapter 2 will mis-prioritise the universe.
- **Universe = inventory, minus the embedded-AI population.** The analyst inventory often cannot find embedded AI; the auditor takes it on faith and under-reports the universe.
- **No schema discipline.** Each row carries inconsistent attributes; the chapter-2 scoring cannot be applied uniformly.
- **The pre-production population is dropped.** Systems in pilot, in sandbox, or in RFP evaluation carry *audit-planning* implications even before they are in production (did procurement follow AI DD, is the sandbox exit criterion defined, is the pilot's data-minimisation controlled). Keep them in the universe with a `pre-production` tag.
- **Universe churn goes unrecorded.** The inventory moves every month; the audit committee needs to see *change*, not just *current state*. Record additions, deletions, re-classifications as a universe-change log; the log itself is auditable evidence of planning discipline.

## Summary

- The AI audit universe is the bounded, annotated population of **auditable units** (AI systems, programmes, processes, vendor relationships, AIMS components, GPAI cross-cuts) from which the annual plan draws — not a copy of the analyst AI inventory.
- The universe must represent five populations: internal systems, deployed systems, third-party AI procurement, embedded AI inside non-AI vendors, and GPAI model usage across the portfolio. Embedded AI is the hardest to discover; GPAI usage cross-cuts other populations and needs a single-convention rule.
- The row schema carries inherent-risk attributes (classification, affected population, modality, data sensitivity, autonomy, change velocity, deployment posture) and audit-history attributes (prior coverage, open findings, management response, regulator attention, external coverage) so the scoring in chapter 2 can be applied uniformly.
- Discovery is a repeatable cycle — pull inventory, enrich from adjacent sources, reconcile against prior-year universe, classify, verify with owners, approve, freeze — producing an auditable universe-change log.
- The AI Auditor *consumes* the analyst inventory and *reuses* the risk-engineer's inherent-risk shape; building the universe does not mean re-authoring either.
