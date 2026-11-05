# exercise-02: Drift, Quality, and Safety-Signal Monitoring Evidence Audit

**Estimated effort:** 2.5 hours

## Objective

Audit the **drift, quality-regression, safety-monitor, near-miss, cost / latency, and jailbreak / prompt-injection detection pipelines** of a production GenAI system as *evidence sources*. For each of the six signal families in chapter 2, produce a one-to-two-page evidence-shape workpaper that (a) identifies the tool and the artefact it emits, (b) reperforms one representative signal from the family against the plan's declared configuration, and (c) tests the risk-signal contract the pipeline consumes for register updates.

The deliverable pairs with exercise 01: exercise 01 tests the plan; this exercise tests the pipelines *behind* the plan.

## Prerequisites

- Chapter [`02-auditing-drift-quality-and-safety-signal-pipelines.md`](../02-auditing-drift-quality-and-safety-signal-pipelines.md).
- Chapter [`01-auditing-the-continuous-monitoring-program.md`](../01-auditing-the-continuous-monitoring-program.md) — the plan under which these pipelines operate.
- `mod-104` on ISA 500 evidence sufficiency and ISA 620 specialist-use.
- `mod-107` chapters 5–7 on fairness / privacy / guardrail programmes — the authored artefacts this exercise tests at monitoring time.

## Scenario

Pick one of the three scenarios below, or substitute a published or employer deployment with suitable redaction. State the chosen subject at the top of the deliverable.

**Scenario A — Consumer banking chatbot.** A US regional bank runs a public-facing chatbot answering account questions, with a limited tool-use scope (balance read, recent-transaction read). SR 11-7 model-risk-material. Monitoring stack: whylogs → WhyLabs for drift, Evidently AI for data-quality tests, Arthur AI for performance and fairness dashboards, Llama Guard 3 for input / output guardrail, Langfuse for trace storage.

**Scenario B — Health-system clinical-decision-support assistant.** A non-binding clinical-reasoning aid (as in exercise 01 of `mod-107`). FDA-regulated as SaMD under a PCCP. Monitoring stack: Evidently AI, Alibi Detect (for calibrated drift against a frozen reference), Fiddler AI, OpenAI Moderation + ShieldGemma dual-guardrail, Arize Phoenix for trace storage.

**Scenario C — EU-market HR-screening platform.** A high-risk AI system under Annex III point 4. Monitoring stack: Holistic AI governance dashboards, Fairlearn for subgroup slicing, Evidently AI, Lakera Guard + Robust Intelligence for prompt-injection detection, LangSmith for trace storage.

## Requirements

1. **Pipeline inventory.** Build a table of the six signal families (drift, quality, safety, near-miss, cost/latency, jailbreak/injection) × the tools the scenario names. For each cell, record the artefact the tool emits and whether that artefact is captured in the organisation's retention and accessible for audit reperformance.

2. **Reference-set and metric-definition walk.** For the drift family and the quality family specifically:
   - Produce a one-paragraph description of the reference set (hash, date, size, rationale for the pin).
   - Produce the exact metric definition in use — which statistical test, which threshold, which multiple-testing correction.
   - Flag any defect (stale reference, undocumented default, missing correction).

3. **Reperformance per family.** Execute at least one reperformance from each of the six families. Each reperformance produces a short workpaper subsection:
   - What signal, over what window, from what raw data source.
   - The dashboard-reported value.
   - The auditor-computed value.
   - The delta.
   - Materiality assessment of the delta.
   - Finding candidate if the delta exceeds a stated tolerance.

   For drift reperformance, produce a small notebook sketch (Python or similar — illustrative, not production) that computes the test. For guardrail reperformance, produce a reference to the held-out benign / adversarial set used and the auditor-computed FPR / FNR.

4. **Near-miss taxonomy audit.** Pull the organisation's near-miss event list for the period. Confirm the taxonomy is documented and that near-misses have a path to register updates. If the taxonomy does not exist, note it as a program-level finding and work from the raw event stream.

5. **Cost / latency framing test.** Confirm that cost / latency anomalies are investigated for AI-safety (OWASP LLM04-style) reasons in addition to SRE reasons. If the investigation path is SRE-only, flag as a finding.

6. **Jailbreak / injection coverage test.**
   - Map the production detection pipeline to OWASP LLM Top 10 LLM01 (and the 2025 direct-vs-indirect split where applicable). <!-- needs-research: confirm the current OWASP LLM Top 10 structure at reading time -->
   - Confirm an attack-corpus refresh cadence is documented.
   - Confirm indirect-injection coverage for any retrieval / email / document-uploaded surface.
   - Run (or specify, without executing in production) a small adversarial-subset replay against the production detection endpoint and report the operating point.

7. **Risk-signal contract audit.** Produce the contract document (or note its absence). If present, test:
   - Is the contract versioned?
   - Is it referenced by both the monitoring plan and the register methodology?
   - For one sampled signal, verify the register update matches the contract's update rule.

8. **ISA 620 specialist-use record.** For any reperformance step you would, in a real engagement, delegate to a specialist, record: scope of work, specialist competence, specialist independence, auditor's evaluation of specialist output.

9. **Findings register.** Column shape identical to exercise 01, specifying for each finding the family (drift / quality / safety / near-miss / cost-latency / injection) and the pipeline-vs-contract-vs-plan source of the issue.

## Starter guidance

- Reperform *configuration verification* — use the organisation's declared method and reference. The goal is not to improve the test; it is to confirm the pipeline executes it correctly.
- For classifier guardrails, the published operating point from the vendor's model card is one evidence source; the auditor's held-out replay is another. Both belong in the workpaper.
- Indirect-injection coverage is the most commonly missing element — be explicit about whether retrieved content is inspected, not only user input.
- Near-misses are often undertaxonomised — the finding is at the programme level more often than at the event level.
- A "dashboard-only" evidence shape (no raw-data export) is a `mod-104` ISA 500 sufficiency issue and belongs in the findings even when the dashboard numbers look correct.
- Do not reperform in production. Reperformance happens on exported data in an isolated workspace.

## Acceptance criteria

The deliverable is accepted when:

- The six-family pipeline inventory covers every family for the chosen scenario, with artefact-capture status per cell.
- Reference-set and metric-definition walks exist for drift and quality.
- Six reperformance subsections exist — one per family — each with raw-data pointer, dashboard-reported value, auditor-computed value, and delta.
- The jailbreak / injection section maps to OWASP LLM01 and tests both direct and indirect coverage.
- The risk-signal contract is either audited (version, references, sampled update rule) or flagged as absent.
- ISA 620 specialist-use is recorded where applicable.
- Findings include family and source-layer classification.
- `<!-- needs-research: ... -->` is used where a claim cannot be verified from primary sources.

## Stretch goals

- Author a **reperformance notebook** (Python, Evidently + Alibi Detect) that a reviewing partner could re-execute against the same reference and raw-data pointers.
- Produce a **cross-family findings heatmap** — family × source-layer (pipeline / contract / plan) — surfacing the organisation's structural weakness.
- Draft a **vendor-dashboard evidence-adequacy** memo arguing for or against the organisation's reliance on a vendor's dashboard as `mod-104` ISA 500 sufficient evidence, naming the specific controls (dashboard versioning, raw-data export, audit-only access) that would raise or lower the sufficiency bar.
- Build a **small adversarial-replay harness** (outside production) using garak or promptfoo against the production detection endpoint, producing the operating-point number that belongs in the workpaper.
