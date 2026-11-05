# The Third-Line AI Auditor: Scope and Boundaries

## Motivation

Before you can deliver an audit opinion on an AI system you have to defend *why you are the one allowed to give it*. The audit opinion is load-bearing — it unlocks ISO/IEC 42001 certification, EU AI Act Article 43 conformity, a SOC-for-AI attestation report, an SR 11-7 validation memo, an NYC Local Law 144 bias-audit summary. If the reader cannot locate you on the three-lines ladder, the report is worthless. This chapter pins the AI Auditor's position: what sits in the third line, what the second line (release assurance) owns, what the first line (engineering craft) owns, and when the auditor is internal to the organisation vs. external.

## Three-lines boundary for AI, in one picture

The IIA **Three Lines Model** (2020 revision — formally renamed from "Three Lines of Defense Model" and refocused from pure defense to governance-plus-value) distinguishes:

- **First line** — operational management: the people who design, build, deploy, and operate the AI system. In this curriculum, that is primarily `ai-risk-engineer` (level 25) authoring the hands-on engineering craft (fairness / privacy / robustness / guardrail / red-team tooling), plus the broader engineering tracks they interface with (`ml-engineer`, `llm-application-developer`, `rag-engineer`, `fine-tuning-engineer`, `training-pipeline-engineer`, `ai-infra-mlops`, `applied-ai-engineer`). They own the controls.
- **Second line** — control and compliance functions that oversee the first line without being accountable for the output: risk, compliance, quality, security, model-risk-management, release assurance. `ai-evaluation-engineer` (level 35) sits here — the release-assurance methodology that packages evidence (eval suites, red-team coverage, pre-release gates, deployment criteria) is a second-line function; it *reviews* first-line work but is not independent of it. The organisation's AI Governance Analyst (`ai-governance-analyst`, level 15) does second-line analyst legwork — intake, inventory, impact assessments.
- **Third line** — independent assurance. This is where you sit. The hallmark is **functional independence from the activities being assured** — the third line does not design or operate the controls it opines on, and its reporting line runs around the first and second lines, not through them.

Mapping that to AI work:

| Activity | Line | Primary owner (in this curriculum) |
|---|---|---|
| Design the eval suite, red-team harness, guardrail config | 1 | `ai-risk-engineer` (L25), with authoring help from `ai-eval-engineer` (L30) / `model-evaluation-engineer` (L30) |
| Build release-gate criteria; sign off a release is "safe to ship" | 2 | `ai-evaluation-engineer` (L35) |
| Author the control library, policy taxonomy, AIMS design | 2 → arch | `senior-ai-governance-architect` (L50) |
| Opine independently on whether those controls work, replicate claimed metrics, test the AIMS to certification shape | **3** | **`ai-auditor` (L45, this track)** |
| Direct the audit function at enterprise scope; sign the engagement letter; interface with the audit committee | oversight | Chief Audit Executive (CAE) |

The key practitioner test at level 45: **you must be able to explain, in writing and on the record, what you did NOT do that would have placed you in the first or second line.** You did not design the eval. You did not author the guardrail policy. You did not sign off the release. You read, sampled, re-ran, and opined on what others produced.

## Internal vs. external AI Auditor

The same role is executed in two very different employment postures, and the audit shape, rulebook, and independence test change with the posture. You will move between them over a career; some engagements blend them.

### Internal AI Auditor (third line *inside* the organisation)

- Employed by the organisation, reports functionally to the **Chief Audit Executive (CAE)** and administratively to a C-suite executive; the CAE in turn reports to the audit committee of the board.
- Governed primarily by the **IIA Global Internal Audit Standards** (2024, effective January 2025, replacing the prior IPPF structure) plus local sector overlays (SR 11-7 MRM for US banks, GAO Yellow Book / GAGAS for US-government-adjacent work, FDA GMLP + 21 CFR 820 for AI/ML SaMD, NAIC for insurers).
- Independence test: *organisational* independence (reporting line, charter, dual-reporting to audit committee) plus *individual* independence of the auditor (no rotation back into first-line AI engineering work being audited within a cooling-off window).
- Typical deliverables: internal audit report to the audit committee, follow-up tracking, continuous-audit monitoring outputs.

### External AI Auditor (third line *outside* the organisation)

Four distinct external-assurance postures, each with its own rulebook:

1. **Big-4 (and mid-tier) assurance practice** executing an attestation under IAASB **ISAE 3000 (Revised)** or AICPA **AT-C 105 / AT-C 205** — SSAE 18 SOC 2 / SOC 3 / SOC for AI / bespoke AI-attestation engagements. The firm registers with the oversight body (PCAOB-equivalent for public-interest work), the engagement partner signs the report, and firm-wide **ISQM 1 / 2** quality-management controls apply.
2. **Notified body** executing **EU AI Act Article 43-44 conformity assessment** for Annex III high-risk AI systems that require third-party conformity assessment, or auditing General-Purpose AI providers against the **Article 55 systemic-risk** path. Notified bodies are designated under EU AI Act and must meet horizontal designation requirements analogous to ISO/IEC 17065 for product certification. <!-- needs-research: confirm the specific EU AI Act notified-body designation regulation reference and the horizontal accreditation standard referenced in Articles 29-33 at authoring time — AI Act text is stable at this point but implementing acts continue to land -->
3. **Accredited certification body** executing **ISO/IEC 42001 AIMS certification audits** under **ISO/IEC 17021-1** (horizontal MS-certification requirements) and **ISO/IEC 42006** (AIMS-specific CB requirements), accredited by a national accreditation body under IAF MLA. Stage-1 (documentation) → Stage-2 (implementation) → surveillance → recertification.
4. **ForHumanity-credentialed Independent Auditor** executing an **Independent Audit of AI Systems (IAAIS)** engagement against a published ForHumanity audit scheme (e.g., for NYC LL144, Colorado AI Act, EU AI Act readiness) — the practitioner typically holds the ForHumanity FHCA ("Fellow of ForHumanity Center for AI") designation and is bound to the ForHumanity rulebook for that scheme. <!-- needs-research: confirm the exact ForHumanity credential nomenclature (IAAIS / FHCA) as of the authoring date; ForHumanity has revised its credentialing structure over the 2023–2025 window -->

External AI Auditors also execute **BABL AI bias audits** for NYC LL144-covered Automated Employment Decision Tools, **SR 11-7-aligned independent model validation** for US bank AI/ML (often placed in a third-party MRM firm so it is independent of the bank's internal MRM second line), and **FDA GMLP + PCCP** audits for AI/ML Software-as-a-Medical-Device.

### When the postures mix

- A Big-4 firm may run an **internal audit outsourcing or co-sourcing** arrangement — practitioners act as the organisation's internal-audit function under IIA Standards, but employed by the Big-4. Independence still has to be defended under both IIA Standards and the firm's auditor-independence rules (AICPA code / IESBA code / local regulator rules).
- A notified body's auditor executing an EU AI Act conformity assessment may *also* hold the organisation's ISO/IEC 42001 certification audit, and the regulator will scrutinise whether sharing information between the two engagements creates a self-review threat under ISO/IEC 17021-1 clause 5.2.
- Internal auditors preparing for external assurance (SOC for AI, ISO/IEC 42001 certification) have to be careful not to slide into first-line remediation work during the "readiness" phase — the second you co-author a control fix, you have ceded independence to opine on it.

## The "what you audit" list for an AI Auditor (concrete)

Keep this list on your desk. When an engagement scope is proposed, every artifact in scope should map to one of these.

- Model weights (and the training-provenance chain that produced them)
- Training, fine-tuning, RLHF/DPO, and evaluation datasets (with datasheets, licensing, PII posture)
- Eval artifacts (eval suite configs, run logs, metrics, calibration evidence, judge-vs-human agreement)
- Red-team artifacts (adversarial suites, attack logs, coverage matrices, residual-risk register)
- Inference logs, trace stores, tool-call records
- Guardrail configs (safety classifier thresholds, policy routers, refusal logic, PII filters, jailbreak detectors)
- Monitoring dashboards (drift, accuracy, fairness, abuse, incident rates)
- Incident records (detect → RCA → fix → regression fixture → regulator-notification trail)
- Change-management evidence (model re-training triggers, PCCP change records, release gates)
- AIMS documents (AI policy, objectives, scope, risk-assessment procedure, impact-assessment outputs, management review minutes)
- Third-party evidence (vendor SOC 2, ISO/IEC 42001 cert, ForHumanity IAAIS report, ML-BOMs, SBOMs)
- Supporting management-system evidence (ISO 27001, 27701, 9001, 14971, 13485 overlap)

What you do **not** audit at level 45: the strategic decision to build the AI system at all (that's the board's call, not internal audit's), the specific wording of the organisation's legal disclosures (legal counsel), the SOC incident-handling runbook execution (SecOps / DFIR — you audit the interface, not run the playbook).

## Role boundary in one sentence

> The AI Auditor **audits outputs** produced by the first and second lines against defensible criteria and under defensible independence; the AI Risk Engineer **authors methodology**; the AI Evaluation Engineer **operates release assurance**; the Senior AI Governance Architect **designs the control library the auditor audits against**; the CAE **leads the audit function** at enterprise scope.

Everything else in this module makes that boundary enforceable: the rulebooks you work inside (IIA, ISACA, IAASB, AICPA, ISO), the credentials that signal competence to each buyer, and the independence posture you commit to in writing.

## Summary

- The AI Auditor sits in the **third line** of the IIA Three Lines Model — independent of first-line engineering craft (`ai-risk-engineer` L25) and second-line release-assurance methodology (`ai-evaluation-engineer` L35).
- The role has two employment postures: **internal** (IIA Standards, CAE reporting, audit committee audience) and **external** (ISAE 3000 / AT-C 105 firm attestations, notified-body EU AI Act conformity assessment, ISO/IEC 17021-1 + 42006 certification bodies, ForHumanity IAAIS).
- Mixed postures are common (outsourced internal audit, certification body also running AI Act conformity) — the independence test moves with the posture.
- You audit **outputs** (weights, data, evals, red-team artifacts, logs, guardrails, monitoring, incidents, AIMS documents, third-party evidence) — you do not author the methodology or sign the release.
- Everything downstream in this track assumes you can defend this boundary in writing.
