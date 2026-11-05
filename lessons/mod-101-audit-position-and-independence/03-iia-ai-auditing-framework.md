# The IIA AI Auditing Framework and "Internal Audit's Role in Governance of AI"

## Motivation

The 2024 Global Internal Audit Standards tell you *how* to run an internal audit; they do not tell you what an AI audit is. The IIA's **AI Auditing Framework** does. It is the internal-audit profession's first-order statement of what AI introduces that other audits don't cover, and the follow-on **Internal Audit's Role in Governance of AI** guidance pins how third-line assurance participates in enterprise AI governance without sliding into second-line work. Every internal AI audit engagement letter you author at level 45 should reference both. This chapter installs them as the working shape you execute inside an organisation.

## The IIA AI Auditing Framework — three parts, one shape

The IIA Research Foundation published the **Artificial Intelligence Auditing Framework** as a three-part series:

- **Part I — Overview of AI.** Introduces the AI ecosystem for internal auditors — definitions of AI vs. ML vs. deep learning, the AI lifecycle, roles across first and second lines, and the rationale for why AI is distinct from prior technology audits.
- **Part II — AI Risks.** Enumerates the risk categories an AI audit must cover — strategic alignment, cyber resilience, data quality, data governance, "black box" / explainability, ethical use, legal and regulatory, performance measurement, and human factors.
- **Part III — Assessing the Risks.** Provides an assessment approach the auditor executes — scoping, control identification, testing, and reporting against the risks surfaced in Part II.

<!-- needs-research: confirm the exact publication years and titling convention of the IIA AI Auditing Framework at authoring time; the three-part series is commonly dated 2017 but IIA has refreshed related AI materials and the student should cite the version they can source -->

### What the Framework actually gives you

Read as an operating document, the Framework gives the internal AI auditor three things:

1. **A risk vocabulary** that an audit-committee reader recognises. When you brief the committee on AI audit findings, you anchor each finding to one of the Framework's risk categories — strategic, cyber, data, black-box, ethical, legal/regulatory, performance, human factors. That shared vocabulary matters because the committee may not read the latest ISO/NIST/EU AI Act clauses but they will recognise the IIA risk model.
2. **A placement model for the AI lifecycle** — what gets audited at problem framing, data acquisition, model development, deployment, operation, retirement. This lets you scope an engagement at a lifecycle stage and know what artifacts and controls are in play.
3. **A sign that this is audit, not engineering.** The Framework is deliberately technology-neutral; it does not teach model training. The internal AI auditor executes the Framework and reaches for `ai-risk-engineer` (L25), `ai-evaluation-engineer` (L35), `model-evaluation-engineer` (L30), `ai-eval-engineer` (L30), and `agentic-safety-engineer` (L40) for the methodology depth — then returns to the Framework to classify what was found.

### Working mapping — Framework risks to downstream module coverage in this track

Keep this cross-reference close; it is how Framework risks become auditable work.

| Framework risk | Audited in this track by |
|---|---|
| Strategic alignment | `mod-103-risk-based-audit-planning` (AI audit universe, materiality, planning against enterprise strategy) |
| Cyber resilience | `mod-107-auditing-ai-risk-management-and-harm-models` (adversarial-ML program, MITRE ATLAS, OWASP LLM / ML Top 10), `mod-109-auditing-ai-supply-chain-and-third-party` (SBOM / ML-BOM, provenance) |
| Data quality + data governance | `mod-104-audit-evidence-and-sampling-for-ai` (data artifacts, sampling), `mod-106-auditing-model-and-system-card-claims` (datasheets, dataset cards) |
| Black box / explainability | `mod-106-auditing-model-and-system-card-claims` (independent replication), `mod-107-auditing-ai-risk-management-and-harm-models` (SHAP / LIME / Alibi tooling under auditor review) |
| Ethical use | `mod-105-auditing-iso-42001-aims` (AI policy + objectives), `mod-106-auditing-model-and-system-card-claims` (fairness), `mod-107-auditing-ai-risk-management-and-harm-models` (harm model) |
| Legal and regulatory | `mod-102-ai-audit-criteria-landscape` (regulatory-to-criteria translation), `mod-110-conformity-assessment-and-sector-audit-shapes` (engagement shape per regulator) |
| Performance measurement | `mod-106-auditing-model-and-system-card-claims`, `mod-108-auditing-monitoring-incidents-and-post-market-surveillance` |
| Human factors | `mod-105-auditing-iso-42001-aims` (competence + awareness clause 7), `mod-107-auditing-ai-risk-management-and-harm-models` (red-team staffing + rotation) |

## "Internal Audit's Role in Governance of AI"

The IIA's guidance on **Internal Audit's Role in Governance of AI** complements the Framework by answering the second-line vs. third-line boundary question explicitly for AI. The guidance's working logic:

- Internal audit's role is **independent assurance over AI governance**, not operation of it.
- Internal audit provides **early-stage advisory** value *carefully* — reviewing an AI governance design *before* it operates is allowed, so long as internal audit does not author the design and so long as the eventual audit of operating effectiveness is not precluded by the earlier advisory work.
- Internal audit should **coordinate with the second line** (AI ethics committee, ML-risk function, release assurance) but not replace it.
- Internal audit should **report on AI governance maturity** to the audit committee, not only on individual-engagement findings.

<!-- needs-research: confirm the current title, publisher, and year of the "Internal Audit's Role in Governance of AI" guidance — the IIA has released multiple AI-governance documents between 2023 and 2026 and the student should cite the live version at the time of reading -->

### Boundary cases to resolve before engagement kickoff

The following recurring cases must be resolved against the Framework + governance guidance *in the engagement letter*, not improvised mid-engagement:

- **AI "sandbox" assessment.** First-line engineering runs an AI pilot. Second line has not yet built release-assurance. Does internal audit assess the sandbox? — Allowed as **advisory engagement** under IIA Standards Domain V, provided internal audit documents that the engagement is advisory not assurance, and that the eventual assurance engagement on the production system is still reachable.
- **Model risk management (MRM) coverage overlap.** In a US bank, the second-line MRM function already validates models under SR 11-7. Where does internal audit's AI audit sit? — Internal audit **audits the MRM function's own effectiveness** (did MRM scope the AI/ML models correctly, was the validation rigorous, did findings close) rather than re-running the validation. SR 11-7 itself anticipates this two-layered structure.
- **AI ethics committee as "control".** Does internal audit audit the AI ethics committee's decisions, or the process by which decisions get made? — You audit the process (charter, meeting cadence, decision log, escalation to board) and the operation of the process (were the right risks escalated, were decisions documented, were CAPs assigned). You do not re-adjudicate individual ethics decisions — that is a management prerogative.
- **Pre-deployment "red-team-as-assurance" ask.** First or second line asks internal audit to red-team a model. — Decline the first-line framing. Accept only if the ask is **auditing whether the red-team program works** (coverage, independence of the red-team from the model team, closure of findings) — not performing the red-team itself (that is `ai-risk-engineer` L25 and `agentic-safety-engineer` L40 scope).

## Example — scoping an internal AI audit against the Framework

Scenario: the audit committee asks for a Q2 engagement on the retail bank's new **customer-facing generative-AI assistant for personal banking**.

Scoping using the Framework + governance guidance:

- **Framework risk coverage** — strategic (is the assistant aligned to the bank's stated AI strategy?), data governance (training data provenance, PII handling, retention), ethical (fairness across protected classes, inclusive language), cyber (prompt injection resistance, tool-call authorisation), legal/regulatory (GLBA / CFPB / state UDAP / NYC LL144 if used for any employment-adjacent decision making), performance measurement (production monitoring), human factors (customer-service agent override, training).
- **Lifecycle coverage** — in-scope: problem framing (did the AI committee approve?), data acquisition (training + RAG corpus), model development (base model selection, fine-tuning, eval), deployment (release gate, canary, rollback), operation (monitoring, incident response). Out-of-scope at this engagement (deferred to a follow-on): retirement + decommissioning (system not yet due for deprecation).
- **Second/third-line boundary** — in scope to audit: the AI ethics committee's approval record, the second-line MRM function's validation report, the first-line release-gate artifacts. Not in scope: re-running the MRM validation from scratch (that's reliance on MRM work, tested per ISA 610-analogue reliance posture per the 2024 Standards Domain IV).
- **Standards citation** — engagement letter cites IIA 2024 Standards Domain V, AI Auditing Framework Part II risk categories, and "Internal Audit's Role in Governance of AI" guidance for the second/third-line posture.

That engagement letter is defensible under audit-committee review, external QA, and (if the bank is later subject to a regulator inquiry on the AI assistant) regulator examination.

## Summary

- The IIA **AI Auditing Framework** (Overview / Risks / Assessing the Risks) gives the internal AI auditor the risk vocabulary, lifecycle placement, and audit-not-engineering posture that anchors every internal AI engagement.
- **Internal Audit's Role in Governance of AI** pins the second/third-line boundary for AI — audit the governance, do not author it; coordinate with the second line, do not replace it; advisory work is allowed but carefully bounded.
- Framework risk categories map cleanly to this track's downstream modules — use the mapping in engagement scoping.
- Recurring boundary cases (sandbox assessment, MRM overlap, ethics committee, pre-deployment red-team asks) must be resolved in the engagement letter, not improvised.
