# mod-108-auditing-monitoring-incidents-and-post-market-surveillance: Auditing Monitoring, Incident Response, and Post-Market Surveillance

**Estimated effort:** 14 hours

## Learning objectives

- Audit the continuous-monitoring program against ISO/IEC 42001 clause 9.1 and EU AI Act Article 72 post-market monitoring obligations — testing the monitoring plan, data logged, retention policy, performance against the Article 72 plan, threshold-breach detection, escalation routing.
- Audit model / data drift, quality regression, safety-monitor signal, near-miss data, cost / latency anomalies, and jailbreak / prompt-injection detection pipelines — using WhyLabs (whylogs), Evidently AI, Alibi Detect, Fiddler AI, Arthur AI, Holistic AI dashboards as evidence; testing that monitoring thresholds trigger the right risk-register update (consuming the `ai-risk-engineer` (level 25) risk-signal contract).
- Audit the AI incident-response program against EU AI Act Article 73 serious-incident reporting, NAIC Model Bulletin on AI insurer incidents, FDA Mandatory Reporting Rule (MDR) adapted for AI/ML SaMD incidents, SR 11-7 MRM incident-reporting shape, and the ISO/IEC 42001 clause 10.1 nonconformity/corrective-action loop — testing triage, root-cause analysis, post-mortem authoring, permanent-regression-fixture back-feed, and regulator-facing summary quality.
- Independently test a representative sample of incidents end-to-end — detect → triage → RCA → post-mortem → regression-fixture → corrective-action closure → risk-register update → (where applicable) regulator notification → audit-committee reporting — using the organisation's trace store, run logs, and GRC-for-AI platform as evidence sources.
- Audit the Article 72 Post-Market Monitoring Report shape for a high-risk EU AI Act system — plan completeness, data adequacy, breach-reporting evidence, corrective-action evidence, next-period update.
- Audit third-line independence in incident response — confirming that the AI auditor sees the same evidence SecOps and the governance council see, and that no incident is being resolved outside the three-lines-of-defense process; defer *out of scope* to SecOps / DFIR for SOC-side incident handling (the auditor tests the interface, not the SOC runbook).
- Audit the AI Auditor's own prior-period findings — testing management-response-to-closure evidence, repeat-finding patterns, status in the follow-up tracker.

## Structure

- [`01-auditing-the-continuous-monitoring-program.md`](01-auditing-the-continuous-monitoring-program.md) — ISO/IEC 42001 Clause 9.1 ↔ EU AI Act Article 72 crosswalk, the determinate-set walk, the operation walk, threshold-breach reperformance, escalation routing, retention, and the register interface.
- [`02-auditing-drift-quality-and-safety-signal-pipelines.md`](02-auditing-drift-quality-and-safety-signal-pipelines.md) — six signal families (drift, quality, safety-monitor, near-miss, cost / latency, jailbreak / injection), tool-specific evidence shapes (WhyLabs, Evidently, Alibi Detect, Fiddler, Arthur, Holistic AI, classifier guardrails, vendor guardrails), reperformance per family, and the `ai-risk-engineer` (L25) risk-signal contract.
- [`03-auditing-the-incident-response-program.md`](03-auditing-the-incident-response-program.md) — the plural criteria surface (Article 73, NAIC Model Bulletin, FDA MDR, SR 11-7, Clause 10.1, NIST AI RMF MANAGE 4.3), definition breadth, triage, RCA, post-mortem, permanent regression-fixture back-feed, regulator-facing report quality.
- [`04-reperforming-incidents-end-to-end.md`](04-reperforming-incidents-end-to-end.md) — the nine-step end-to-end reperformance (detect → triage → RCA → post-mortem → regression-fixture → corrective-action closure → risk-register update → regulator notification → audit-committee reporting), sample selection, workpaper shape, cross-incident pattern pass.
- [`05-auditing-the-article-72-post-market-monitoring-report.md`](05-auditing-the-article-72-post-market-monitoring-report.md) — report completeness, plan-execution reperformance, data adequacy, breach-reporting evidence, next-period update, Chapter III Section 2 article interfaces, GPAI systemic-risk and downstream-deployer positions.
- [`06-three-lines-independence-in-incident-response.md`](06-three-lines-independence-in-incident-response.md) — evidence-parity test, access-protocol test, out-of-process-resolution test, SOC / DFIR boundary, governance-council parity, prior-period independence findings.
- [`07-auditing-the-follow-up-tracker.md`](07-auditing-the-follow-up-tracker.md) — tracker field hygiene, closure-evidence reperformance, open-finding discipline, repeat-finding detection, cross-cycle traceability, materiality roll-up, independent-review flag.
- [`exercises/`](exercises/) — per-exercise prompts aligned to the chapters.
- [`labs/`](labs/), [`quizzes/`](quizzes/) — long-form labs and knowledge checks (scaffolded).
- [`resources.md`](resources.md) — curated primary references.

## How this module fits the `ai-auditor` track

- **Input from `mod-101`** — audit-function independence and the three-lines model — is the backbone of chapter 6 and the follow-up-tracker self-review guardrail in chapter 7.
- **Input from `mod-102`** — criteria translation — fixes the specific text of Article 72, Article 73, Clause 9.1, Clause 10.1, SR 11-7, NAIC Bulletin, FDA MDR, and NIST AI RMF MANAGE 4.
- **Input from `mod-103`** — scoping, materiality, and the engagement letter — defines the sample strata and the audit-committee reporting thresholds this module uses throughout.
- **Input from `mod-104`** — evidence discipline (ISA 500), sampling (ISA 530), specialist use (ISA 620), WORM storage — underwrites every reperformance workpaper.
- **Input from `mod-105`** — ISO/IEC 42001 Clause 9.1 performance evaluation and Clause 10.1 corrective-action loop — the AIMS framing.
- **Input from `mod-106`** — model / system / dataset card claims — chapter 5 cross-checks for Article 72 report / public-card consistency.
- **Input from `mod-107`** — harm model, risk register, red-team programme, adversarial-ML, fairness, privacy, guardrail programme — the authored artefacts chapters 1–3 test at monitoring time.
- **Output to `mod-109`** — supply-chain and third-party audit shape for upstream GPAI providers and vendor-guardrail / vendor-monitoring suppliers.
- **Output to `mod-110`** — conformity-assessment-body engagements layer on the Article 72 report shape (chapter 5) during notified-body surveillance.
- **Output to `mod-111`** — findings reporting discipline for the per-chapter finding registers this module produces.
- **Output to `mod-112`** — audit-leadership automation consumes the monitoring and tracker signals this module validates.
- **Delta from `ai-risk-engineer` (L25)** — the monitoring pipelines, the risk-signal contract, the register methodology, and the red-team programme are *authored* there; the auditor tests the authored artefacts.
- **Delta from `agentic-safety-engineer` (L40) / `model-evaluation-engineer` (L30)** — specialist disciplines for deep statistical reperformance; ISA 620 applies and the auditor records the specialist's engagement.
- **Delta from `cybersecurity-engineer` / DFIR** — SOC-side incident handling is specialist work; the AI auditor tests the interface to it, not the runbook itself (chapter 6).
