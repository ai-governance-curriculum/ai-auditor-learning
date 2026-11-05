# exercise-02: Continuous-Audit Architecture Authoring

**Estimated effort:** 3 hours

## Objective

Design the continuous-audit operating model for an AI audit function in a realistic organisation. Produce the architecture, the evidence-pipeline catalogue, the CCM rule catalogue, the exception-workflow definition, the pipeline-health plan, and the audit-committee dashboard specification — all defensible against external quality assessment and designed to preserve independence.

## Prerequisites

- Chapter [`02-continuous-audit-operating-model-for-ai.md`](../02-continuous-audit-operating-model-for-ai.md).
- Chapter [`03-integrating-with-grc-for-ai-platforms.md`](../03-integrating-with-grc-for-ai-platforms.md) (for the GRC-for-AI integration).
- Chapter [`04-building-the-ai-audit-tooling-layer.md`](../04-building-the-ai-audit-tooling-layer.md) (for the tooling layer that supports continuous audit).
- `mod-104` on evidence sufficiency and chain-of-custody.
- `mod-108` on post-market monitoring (for the incident-register integration).

## Scenario

**Organisation.** Meridian Labs, a scale-up AI company offering a hosted multi-tenant LLM platform used by SMB customers to build AI assistants. Meridian is SOC 2 Type II attested, is pursuing ISO/IEC 42001 certification (Stage 1 passed, Stage 2 in Q2 2027), and sells into regulated sectors (financial services, healthcare, legal) with contractual MSAs that reference customer regulators.

**Current audit posture.** Internal audit has been a two-person function running point-in-time engagements. The CAE has approved building a continuous-audit model to serve the Audit Committee quarterly; the first continuous-audit dashboard is expected in Q4 2027.

**AI technology stack (abbreviated).**

- Foundation-model layer: three external providers (production routing across OpenAI, Anthropic, Google) and one open-weights model hosted internally for sensitive data.
- Hosted inference on an internal GPU fleet behind a serving mesh (OpenTelemetry traces; vLLM / internal serving).
- Guardrails: internal prompt-injection filter, PII filter, content-policy classifier, Lakera integration for untrusted input scanning.
- Observability: Arize for drift / performance; Datadog for infra; Splunk for SIEM.
- MLOps: GitHub-based CI, MLflow registry, cosign / Sigstore attestation on builds, internal release-approval workflow.
- GRC: just migrated to Credo AI for the AI-governance workflow; ServiceNow for broader GRC; AuditBoard for internal audit workpapers.

## Deliverables

### 1. Operating-model diagram and narrative (~1 page)

Produce a conceptual diagram (ASCII / mermaid / description) of the continuous-audit stack and narrate the flow. Cover:

- Source systems the audit function reads from.
- Audit evidence store (what it is; how access is controlled; retention).
- CCM engine and rule catalogue.
- Exception workflow tool.
- Audit committee dashboard.
- The independence boundary — what audit owns vs what management owns — with a specific statement of what would break if the boundary were crossed.

### 2. Evidence-pipeline catalogue (~1.5 pages)

Author a catalogue of at least 8 evidence pipelines. For each pipeline:

- Pipeline name and ID.
- Source system (specific).
- Artefact format and content.
- Update cadence (near-real-time / hourly / daily / weekly).
- Authentication / credential basis.
- Transfer and storage controls (signatures, hashing, retention).
- Which CCM rules depend on it.
- Audit use-cases supported.
- Pipeline-health check definition.

Pipelines must span: eval-run artefacts, trace samples, guardrail metrics, drift monitors, SIEM AI signals, GRC-for-AI exports, model-registry provenance, Sigstore attestation, incident-register, and at least one additional source you identify from the scenario.

### 3. CCM rule catalogue (~1.5 pages)

Design at least 15 CCM rules spanning AIMS, SR-11-7-style MRM (where Meridian's customers map to), SOC 2 TSC, EU AI Act Article 13 / 14 / 15 / 72 / 73 obligations, and Meridian-specific contract-SLA-based rules. For each rule:

- Rule ID.
- Criterion reference (authority and clause).
- Data source (which pipeline).
- Logic (describe the check in plain language, suitable for engineering implementation).
- Severity classification (tied to `mod-111` ch. 2 classifications).
- Action on exception.
- Owner inside the audit function.
- Review frequency (how often the rule itself is reviewed against drift).
- Expected exception volume and alert-to-finding target.

Include at least three rules whose data source is the GRC-for-AI platform (Credo AI) and at least two rules whose data source is the MLflow registry.

### 4. Exception workflow (~0.5 page)

Define the workflow from exception generation to closure. Include:

- Triage step (SLA; triager role; decision tree for valid / invalid).
- Investigation step (SLA; investigator role; evidence collection).
- Finding development step (where investigation confirms a finding).
- Closure step (data-quality correction; threshold adjustment with justification; confirmation of control operation).
- Metrics the function tracks (triage SLA adherence; investigation SLA adherence; alert-to-finding ratio; backlog age).
- Anti-pattern safeguards for alert fatigue and rule drift.

### 5. Pipeline-health and tooling-governance plan (~0.5 page)

Describe:

- Pipeline-health monitoring (per-pipeline health checks; notification path; recovery SLA).
- Reconciliation checks (sample-level; schedule; owner).
- Access controls on pipelines, rules, and evidence store (who can read; who can edit; segregation).
- Change management for pipelines, rules, severity thresholds (authorship, review, approval, logging).
- Backup, restore, and retention.
- How the audit function audits its own continuous-audit operating model on an annual cycle.

### 6. Audit-committee dashboard specification (~0.5 page)

Design the dashboard the audit committee will see. Include:

- Panels (6–10) covering plan execution, findings slate, repeat findings, continuous-audit exception trend, regulator engagement, resources.
- For each panel: title, metric, time window, source pipeline, visual form (chart type or table), drill-down path.
- Cadence (which panels update at which frequency).
- Consistency requirements across quarters.
- Explicit anti-patterns the dashboard avoids (composite scores without decomposition; predictions the function cannot defend; grading of named individuals).

## Starter guidance

- Treat the GRC-for-AI platform (Credo AI) as a data source, not ground truth. Design at least one rule that reconciles Credo AI's view with the production reality from MLflow and the serving mesh.
- The independence boundary is specific. Audit owns the evidence store, the rules, and the exception workflow. Management owns the source systems. Edge cases include: if audit's CCM detects a configuration gap in Lakera, is it legitimate for the audit team to propose a specific threshold change? (Answer with reasoning.)
- Include rules that test for *absence* of events as well as presence — missing evidence is often the material finding.
- Think about the Article 73 serious-incident timing window as a CCM rule (`mod-108`) — this is a high-signal example of a rule whose latency has to be short.
- The dashboard is for an audit committee that is not AI-technical. Panels have to be legible without the technical primer.

## Acceptance criteria

The deliverables are accepted when:

- The operating-model narrative identifies source systems, evidence store, CCM, exception workflow, and dashboard, with a specific independence-boundary statement.
- The evidence-pipeline catalogue contains at least 8 pipelines, each with the fields enumerated above, and spans the categories required in the brief.
- The CCM rule catalogue contains at least 15 rules spanning the required criteria sources, with full field population and expected exception metrics.
- The exception workflow defines triage, investigation, finding, and closure with SLAs and metrics; alert fatigue and rule drift safeguards are explicit.
- The pipeline-health and tooling-governance plan covers health monitoring, reconciliation, access controls, change management, backup / restore, and the function's annual self-audit.
- The dashboard specification contains 6–10 panels with the fields enumerated above and explicit anti-patterns.
- At least one rule reconciles Credo AI's view with production reality from another pipeline.
- At least one rule has latency tuned for an Article-73-style timing window.
- Independence considerations are addressed — specifically, no audit activity is designed that would make the audit function a co-operator of a management control.
- No citation is invented; unverified citations carry `needs-research`.

## Stretch goals

- Author the **initial rule-deployment plan** (~0.5 page) that phases the rule catalogue into production over 6 months — which rules land first, which require upstream prerequisites (telemetry gaps, credential setup), and which are deferred.
- Draft the **rule-change pull-request template** the function will use for rule changes, including author, reviewer, criterion, before/after, expected exception-volume impact, and roll-back plan.
- Author the **first quarterly audit-committee pre-read** (~1 page) that would issue from the stack in Q4 2027, after the first full quarter of continuous-audit operation — committee attention, dashboard reads, repeat-finding risk, ask for the committee.
- Design a **deliberate failure test** (~0.5 page) the function will run to verify the stack detects it — an injected configuration drift that should trigger a CCM exception within SLA; include expected rule, expected severity, expected triage path, expected finding.
