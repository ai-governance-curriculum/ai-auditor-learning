# exercise-04: AI Evidence Inventory and Reliability Grading

**Estimated effort:** 2 hours

## Objective

For a scoped engagement, build the engagement's **evidence inventory** — tier each artifact (original / derivative / corroborative), grade reliability (A / B / C / D), and specify the upgrade procedures needed to bring the stack to sufficiency for the engagement's assertions. Produce the inventory table and the one-page cover memo that lives at the top of the fieldwork section of the workpaper file.

## Prerequisites

- Chapter [`04-ai-evidence-inventory-original-derivative-corroborative.md`](../04-ai-evidence-inventory-original-derivative-corroborative.md)
- Chapter [`01-isa-500-evidence-applied-to-ai-artifacts.md`](../01-isa-500-evidence-applied-to-ai-artifacts.md)

## Scenario

**Clerestory Insurance** is procuring an ISO/IEC 42001 AIMS internal-audit engagement covering four production AI systems. The engagement period is 2026-07-01 through 2027-06-30. The four systems and the primary audit assertions the engagement will test:

1. **Underwriting triage classifier (UW-TRIAGE-01)** — a gradient-boosted classifier scoring applications for triage into fast / standard / specialist review.
   - Assertion: the model version in production throughout the period matches the governance-approved version; changes followed the change-management control.
2. **Claims-note summariser (CLAIM-SUM-02)** — an LLM-based (hosted model, Anthropic Claude) summarisation step in the claims workflow.
   - Assertion: production decoding config, prompt template, and guardrail suite match the governance-approved versions; the organisation records the model-identifier returned by the provider on every call.
3. **Customer-service chatbot (CS-CHAT-03)** — a retrieval-augmented LLM over policyholder FAQs and policy documents.
   - Assertion: the retriever index is refreshed from the governance-approved source on the published cadence; the prompt template in production matches the governance-approved template.
4. **Agent routing classifier (AGENT-ROUTE-04)** — a classical-ML routing model.
   - Assertion: the model's calibration during the period remained within the organisation's published tolerance band.

Management has handed the engagement the following per-system evidence:

### UW-TRIAGE-01
- Model-registry page screenshot showing current and prior versions.
- A Confluence page describing the change-management process.
- A Jira project `UW-CHANGE` containing all change tickets; append-only history visible.
- The model-training GitLab repository (private).

### CLAIM-SUM-02
- A model card on the organisation's internal portal.
- The vendor's (Anthropic) published model page.
- A trace-store (in-house) storing per-request records including the `model` field returned by the API.
- A guardrail-config GitHub repository.
- A verbal assertion from the AI lead that the decoding config "hasn't changed".

### CS-CHAT-03
- A vector-store dashboard screenshot showing "last indexed 2027-06-14".
- A Google Doc description of the retriever refresh cadence.
- A cron-scheduled refresh job, visible in the organisation's Airflow instance.
- A production prompt file in the application's deployment manifest (Kubernetes config, visible in Git).
- A monthly report authored by the first-line team summarising retriever health.

### AGENT-ROUTE-04
- A quarterly calibration report authored by the model owner.
- A monitoring dashboard with a drift panel.
- A cold-storage archive of monthly calibration plot PNGs.
- A SOC 2 Type II from the organisation's cloud provider (data-platform scope only).

## Requirements

1. **Author the evidence inventory table** per system. Columns: `artifact`, `tier` (original / derivative / corroborative), `grade` (A / B / C / D), `assertion-supported`, `isa-500-generalisation-anchoring-grade`, `reliability-note`, `required-upgrade-procedure`, `workpaper-node`.
2. **Identify derivative-only stacks.** For each system, state whether the evidence stack as handed over includes any A- or B-grade originals. Where only derivative or management-authored evidence is present, name it as a C-only stack and specify the required upgrade.
3. **Upgrade procedures — specific, not generic.** For every C-graded evidence item that is load-bearing for an assertion, specify the exact upgrade procedure using chapter 4's paths: C→B (reach for the original) or B→A (external corroboration or auditor-direct re-performance). Name the target artifact and the auditor action.
4. **Scope-of-reliance line.** For each system, explicitly state what evidence the engagement will *not* rely on (e.g., management representations as evidence of control operation; dashboards as evidence of underlying metric values; model cards as evidence of production behaviour). One or two bullets per system.
5. **Cover memo.** Draft a one-page memo (250–400 words) that lives at the top of the fieldwork section of the workpaper, explaining the inventory, the grading rubric used, the C-only stacks, the planned upgrades, and the risks to engagement timeline if upgrades cannot be obtained. Addressed to the engagement partner.

## Starter guidance

- Chapter 4's artifact-to-tier mapping table is the starting point. Not every item in the scenario maps 1-to-1 to a row in that table; adapt and explain.
- The model-training GitLab repository for UW-TRIAGE-01 is an original (Git-tracked, content-addressed) but is only load-bearing if the engagement can tie commits to deployed artifact hashes — specify the tie.
- CLAIM-SUM-02 uses a hosted model. The trace-store's record of the provider-returned `model` field is the pin; without it, the engagement cannot verify which model-version served which request. Chapter 6 has the discipline.
- CS-CHAT-03's retriever refresh job in Airflow is an original if the Airflow run history is immutable; if it is editable by any operator, grade drops.
- AGENT-ROUTE-04's calibration report authored by the model owner is entity-internal and derivative-by-shape. The A-grade equivalent is an independent re-computation from the production inference-log data.
- The SOC 2 scope on AGENT-ROUTE-04 — "data-platform scope only" — does not cover the AI feature; call this out as a reliance gap per chapter 4 §Vendor attestations.
- Use `<!-- needs-research -->` for details the scenario does not supply (e.g., whether the trace-store is append-only, whether the Airflow instance has immutable task-instance history).

## Acceptance criteria

The deliverable is accepted when:

- Every evidence item for every system has a tier, a grade, a generalisation-anchor, and either an upgrade procedure or a documented decision not to upgrade.
- Derivative-only stacks are identified by name; no assertion sits on a derivative-only stack without an upgrade plan.
- Upgrade procedures are *specific* — they name the target artifact and the auditor action, not "pursue additional evidence".
- The scope-of-reliance line explicitly excludes model cards as production evidence, dashboards as metric evidence, and management representations as control-operation evidence (chapter 4 §Common failure modes).
- The hosted-model handling for CLAIM-SUM-02 pins the provider-returned `model` field in the trace-store.
- The SOC 2 scope gap on AGENT-ROUTE-04 is named.
- The cover memo is between 250 and 400 words, in professional tone, addressed to the engagement partner.
- `<!-- needs-research -->` placeholders are used where the scenario underspecifies.
- No fabricated vendor products or inflated scope on existing evidence items.

## Stretch goals

- Propose an **evidence-manifest file** (chapter 7 §The evidence manifest) that would mechanically carry the inventory in the engagement's companion repo (YAML shape).
- Write the **ISA 500 §11 information-produced-by-the-entity (IPE) controls assessment** for the UW-TRIAGE-01 Jira project — what controls over the Jira project's data must be in place for the engagement to use it as an original, and how would the engagement test those controls?
- Draft the **vendor-SOC-2 scope-review memo** for AGENT-ROUTE-04 — explaining in professional tone to the risk committee why the current SOC 2 does not cover the AI feature and what the organisation should seek instead.
- Propose a **continuous-evidence** approach: a periodic job that mechanically collects the originals (registry hashes, trace-store counts, Git commit hashes) and lands them in WORM — turning the engagement's upgrade procedures into a standing control.
