# mod-107-auditing-ai-risk-management-and-harm-models: Auditing AI Risk Management, Harm Models, and Red-Team Programs

**Estimated effort:** 14 hours

## Learning objectives

- Audit the organisation's harm model and risk taxonomy against the AI Incident Database, OECD.AI Incidents Monitor, MIT AI Risk Repository, AIRO ontology, and NIST AI 600-1 GenAI Profile — testing completeness, defensible grounding in real precedent, and traceability from a harm to an evaluation to a control to a monitor.
- Audit the risk register — testing that `ai-risk-engineer` (L25) inherent / residual / control-defeated scoring is consistent, risk-appetite calibration is approved by the right oversight audience, portfolio aggregation is reproducible, and sign-off routing is documented and functioning.
- Audit the red-team program — testing program charter, coverage matrix (OWASP LLM Top 10, MITRE ATLAS, OWASP ML Top 10, NIST AI 100-2 cross-tagging), tool coverage (garak, PyRIT, Promptfoo, Inspect), evidence-of-execution cadence, finding-triage process, and remediation-closure. The auditor does not re-author the program (owned by `ai-risk-engineer`) — the auditor tests its sufficiency and reliability.
- Audit the adversarial-ML and robustness program — testing attack coverage against NIST AI 100-2 taxonomy, defence-baseline evidence, residual-risk update after mitigation, and ongoing re-run cadence.
- Audit the fairness and explainability program — testing metric-choice defensibility, mitigation-loop evidence, subgroup / intersectionality coverage, model-card and bias-audit-report publication cadence, NYC LL144 and Colorado AI Act compliance evidence.
- Audit the privacy-risk program — testing MIA / LiRA evidence, DP-SGD (ε, δ) sufficiency for the sensitive-data category, PII pipeline (Presidio) coverage, GDPR Article 22 and NIST Privacy Framework alignment.
- Audit the guardrail program — testing input / output / tool guardrail architecture against OWASP LLM Top 10, classifier-guardrail (Llama Guard, ShieldGemma, OpenAI Moderation, Constitutional Classifiers) false-positive / false-negative evidence, and vendor-guardrail (Lakera, Arthur, Robust Intelligence, Calypso AI, HiddenLayer) controls.
- Position the frontier-safety audit path when the organisation is a frontier lab or a GPAI-with-systemic-risk provider — read the public Responsible Scaling Policy, Preparedness Framework, Frontier Safety Framework, Frontier Model Forum commitments, and the EU AI Office GPAI Code of Practice as published criteria; defer *up* to `agentic-safety-engineer` (L40) for the frontier red-team methodology depth the auditor tests against.

## Structure

- [`01-auditing-the-harm-model-and-risk-taxonomy.md`](01-auditing-the-harm-model-and-risk-taxonomy.md) — the five source corpora (AIID, OECD AIM, MIT AI Risk Repository, AIRO, NIST AI 600-1), the completeness grid, the parochialism test, and the harm → evaluation → control → monitor trace.
- [`02-auditing-the-risk-register.md`](02-auditing-the-risk-register.md) — the twelve-field register row, inherent / residual / control-defeated scoring reperformance, risk-appetite calibration and signatory audit, portfolio-aggregation reproducibility, sign-off routing.
- [`03-auditing-the-red-team-program.md`](03-auditing-the-red-team-program.md) — charter, coverage matrix (OWASP LLM Top 10, OWASP ML Top 10, MITRE ATLAS, NIST AI 100-2, HarmBench), tool portfolio (garak, PyRIT, Promptfoo, Inspect), cadence, finding triage, evidence-of-execution.
- [`04-auditing-adversarial-ml-and-robustness.md`](04-auditing-adversarial-ml-and-robustness.md) — NIST AI 100-2 taxonomy, open-source toolchain (ART, TextAttack, CleverHans, Counterfit), defence-baseline evidence, residual-risk update, re-run cadence, model-under-test clarity.
- [`05-auditing-the-fairness-and-explainability-program.md`](05-auditing-the-fairness-and-explainability-program.md) — obligation map (NYC LL144, EEOC, EU AI Act Articles 10/15/27, Colorado AI Act), metric-selection defensibility, mitigation-loop closure, intersectional coverage, publication cadence, GDPR Article 22 and explainability obligations.
- [`06-auditing-the-privacy-risk-program.md`](06-auditing-the-privacy-risk-program.md) — MIA / LiRA TPR-at-fixed-FPR evidence, DP-SGD (ε, δ) sufficiency and accountant replication, Presidio PII pipeline, GDPR per-article alignment, NIST Privacy Framework, unlearning and sector-specific regimes.
- [`07-auditing-the-guardrail-program.md`](07-auditing-the-guardrail-program.md) — three-layer architecture (input / output / tool), OWASP LLM Top 10 coverage, classifier-guardrail calibration (Llama Guard, ShieldGemma, OpenAI Moderation, Constitutional Classifiers), vendor-guardrail third-party testing, evasion testing, replay and logging.
- [`08-positioning-the-frontier-safety-audit-path.md`](08-positioning-the-frontier-safety-audit-path.md) — when the path applies, published criteria (RSP, Preparedness Framework, Frontier Safety Framework, FMF, EU AI Office GPAI Code of Practice), what the auditor tests, the "defer up to L40" boundary, and the downstream-deployer position.
- [`exercises/`](exercises/) — per-exercise prompts aligned to the chapters.
- [`labs/`](labs/), [`quizzes/`](quizzes/) — long-form labs and knowledge checks (scaffolded).
- [`resources.md`](resources.md) — curated primary references.

## How this module fits the `ai-auditor` track

- **Input from `mod-101`** — audit-position and independence discipline that bounds the frontier-safety and vendor-guardrail chapters.
- **Input from `mod-102`** — criteria translation for the obligation surface (NIST AI 100-1, 100-2, 600-1; OWASP LLM / ML Top 10; MITRE ATLAS; EU AI Act; LL144; Colorado AI Act; GDPR) referenced throughout.
- **Input from `mod-103`** — scoping, materiality, and the engagement letter that fixes which chapters apply and in what depth.
- **Input from `mod-104`** — evidence discipline (ISA 500), sampling (ISA 530), specialist use (ISA 620), WORM storage for adversarial payloads.
- **Input from `mod-105`** — ISO/IEC 42001 AIMS framing; the register audit in chapter 2 aligns with Clause 6 planning and Clause 9 performance evaluation.
- **Input from `mod-106`** — model / system / dataset card claim auditing; the programme audit in this module tests the system that produces those claims.
- **Output to `mod-108`** — post-market monitoring builds on the trace (chapter 1), the register-monitor linkage (chapter 2), the guardrail-logging shape (chapter 7), and the privacy-monitoring shape (chapter 6).
- **Output to `mod-109`** — third-party audits reuse the guardrail-vendor and frontier-provider dependency shapes (chapters 7 and 8).
- **Output to `mod-110`** — conformity-assessment-body engagements layer on the chapter-8 GPAI criteria.
- **Output to `mod-111`** — findings reporting discipline for the per-chapter finding registers.
- **Delta from `ai-risk-engineer` (L25)** — harm-model authoring, attack catalogue authoring, guardrail authoring, mitigation design all sit there; the auditor tests the authored artefacts.
- **Delta from `model-evaluation-engineer` (L30)** — statistical and accountant authoring sits there; the auditor applies the canonical procedures.
- **Delta from `agentic-safety-engineer` (L40)** — frontier capability-elicitation methodology sits there; the auditor reads the resulting safety case as a claim document and engages a specialist per ISA 620 where needed.
