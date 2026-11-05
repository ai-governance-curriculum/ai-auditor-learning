# exercise-07: Guardrail Program Audit

**Estimated effort:** 1 hour

## Objective

Audit an organisation's **guardrail programme** against chapter 7's three-layer architecture frame: **input guardrail**, **output guardrail**, and **tool guardrail**. Produce the OWASP LLM Top 10 coverage grid, test classifier-guardrail calibration (FPR / FNR), and record the vendor-guardrail dependencies.

This is a shorter exercise than the earlier ones; its scope is a focused architecture-and-calibration audit, not a full programme operation audit.

## Prerequisites

- Chapter [`07-auditing-the-guardrail-program.md`](../07-auditing-the-guardrail-program.md).
- Familiarity with OWASP LLM Top 10 (current edition).
- Working exposure to at least one classifier guardrail: Llama Guard, ShieldGemma, OpenAI Moderation API, Azure AI Content Safety, AWS Bedrock Guardrails, or NVIDIA NeMo Guardrails.
- Prior-exercise exposure: chapter 3 (red-team) and chapter 4 (adversarial-ML) findings directly inform guardrail robustness tests.

## Scenario

**Beacon Retail** is a mid-size e-commerce retailer whose customer-service chatbot now handles product search, refund triage (agentic — the bot can file refund tickets via a backend tool), and knowledge-base Q&A. The bot is a fine-tuned open-weights model behind an API, with Llama Guard 3 at the output layer, a custom input classifier for jailbreak detection, and a tool allow-list enforced server-side. The architecture document is up to date; the latest Llama Guard calibration report is three months old.

You are the lead auditor on an ISAE 3000 limited-assurance engagement. The guardrail-programme audit is scope-defined within the overall engagement.

Substitute if needed: any deployed AI-assistant product you can observe, including public LLM playgrounds with visible guardrails. Attribute the subject.

## Requirements

1. **Pin the guardrail architecture.** Architecture diagram / document, Llama Guard version, input-classifier identity and version, tool allow-list document, vendor-guardrail contracts if any.

2. **Produce the OWASP LLM Top 10 coverage grid.** For each of LLM01–LLM10, record:
   - Which guardrail layer (input / output / tool) addresses the risk.
   - The specific control (classifier / regex / policy rule / rate limit / etc.).
   - The evidence that the control operates in production (not merely in the architecture document).
   - Silent omissions are findings.

3. **Classifier-guardrail calibration audit.** For at least two classifiers (input jailbreak classifier, output Llama Guard):
   - Tool identity, version pin.
   - Calibration dataset identity and representativeness.
   - Reported FPR and FNR per category.
   - Threshold choice and sign-off.
   - Re-calibration cadence.
   - Where the organisation has not reported FPR (only FNR, or vice-versa), open a finding.

4. **Tool-guardrail audit.** For the refund-ticket tool:
   - Pull the allow-list; confirm it is version-controlled.
   - Confirm the dangerous-action confirmation (if any) is enforced in deployed code, not merely policy.
   - Confirm rate limits and egress policy.
   - Pull the sandbox / execution-boundary evidence for the tool.

5. **Vendor-guardrail inventory** (if applicable). For each vendor-provided classifier or guardrail layer: vendor identity, contracted service, SLA, attestations (SOC 2 / ISO 27001 / 42001), data-handling terms, exit plan. A vendor that cannot produce per-deployment calibration on representative traffic is a supply-chain finding.

6. **Guardrail-evasion red-team linkage.** Confirm the chapter-3 red-team coverage matrix contains explicit guardrail-evasion rows. Pull one guardrail-evasion attack class and confirm the result; if the red-team has not tested guardrail evasion directly, open a finding.

7. **Logging / replay / alerting audit.** Pull a sample of guardrail decisions from production logs. Confirm per-decision logging (input / output / decision / reason / classifier-version / timestamp), retention per policy, replay-reproducibility, and alerting-rule coverage.

8. **Classifier fairness spot test.** Using the organisation's calibration data (or a public dataset for cross-check), compute the output-classifier's FPR / FNR by subgroup where protected-class data is available. Divergent subgroup FPR is a chapter-5 issue surfaced in chapter 7.

9. **Author the finding register** per chapter 2's shape; cross-reference to the risk register, the red-team tracker, and (where relevant) `mod-109` for vendor findings.

## Starter guidance

- The "control in production" evidence is often weaker than the architecture document suggests — the control was built, tested, and *then* the deployment was reconfigured without updating the control. Look for the mismatch.
- Llama Guard versions change the category set; a model-card claim against Llama Guard v1's category set is not comparable to a Llama Guard 3 or 4 report.
- Classifier calibration should report FPR and FNR; a programme that reports only one is doing partial calibration. Open the finding.
- A tool allow-list that lives only in a documentation Confluence page and is not server-enforced is a *policy*, not a guardrail. The distinction is a finding.
- Fairness spot tests on guardrail classifiers often surface AAE / non-standard-dialect over-flagging; be ready to cite the result carefully and recommend a subgroup-aware threshold revision, not merely a classifier swap.
- Guardrail logs may contain PII; respect the chapter-6 retention / redaction discipline in your workpaper.

## Acceptance criteria

The deliverable is accepted when:

- The architecture is pinned (document / diagram, classifier versions, allow-list source-of-truth).
- The OWASP LLM Top 10 coverage grid is populated with per-row guardrail layer, control, and evidence.
- At least two classifiers have been calibration-audited with FPR / FNR per category.
- The tool-guardrail audit confirms server-side enforcement, allow-list version control, dangerous-action confirmation, rate limits, and sandboxing.
- Vendor-guardrail inventory is present (or "no vendor dependency" is honestly stated).
- At least one guardrail-evasion attack is confirmed against the red-team matrix.
- Logging / replay / alerting audit is present with a production sample.
- Classifier fairness spot test is present or an explicit "no protected-class data available" note is made.
- Finding register cross-references the risk register, red-team tracker, and third-party programme.
- Primary-source citations are present; `<!-- needs-research: ... -->` where claims cannot be pinned.

## Stretch goals

- Build a small **guardrail-evasion red-team suite** in Promptfoo (YAML) that tests three common evasion patterns (encoding, multi-turn split, role-play) against the output classifier, so the organisation has a rerunnable regression check.
- Draft a **classifier re-calibration playbook** — the one-page MLOps runbook that triggers a re-calibration on model update, on classifier update, on a reported false-positive spike, or on quarterly schedule.
- Produce a **vendor-guardrail exit plan template** — the artefact the organisation should hold for each vendor, enumerating fallback classifiers, data-handling transition, and the gap-coverage internal controls.
- Draft a **subgroup-aware threshold proposal** for one classifier — the specific threshold revision that equalises FPR across declared subgroups while preserving a safety floor on FNR.
