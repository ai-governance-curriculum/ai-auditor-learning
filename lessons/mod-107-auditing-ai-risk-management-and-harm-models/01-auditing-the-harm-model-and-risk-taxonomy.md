# Auditing the Harm Model and the Risk Taxonomy

## Motivation

A risk programme is only as good as the map of harms it claims to cover. If the organisation's harm model is thin, parochial, or self-authored from the top down, every downstream artefact — the risk register, the control catalogue, the red-team coverage matrix, the monitoring plan — inherits that thinness. An auditor who tests the risk register without first testing the harm model will re-run the vendor's own blind spot.

This chapter installs the discipline the auditor uses to test the *completeness* and the *defensible grounding* of the harm model, and to trace each harm forward through evaluation, control, and monitor. The reference corpus is external and canonical: the AI Incident Database, the OECD.AI Incidents Monitor, the MIT AI Risk Repository, the AIRO ontology, and the NIST AI 600-1 Generative AI Profile. These are *published criteria* — the auditor does not re-invent them, the auditor reads them.

The auditor is not here to re-author the harm model. The authoring sits with `ai-risk-engineer` (L25). The auditor's job is to test whether the harm model the organisation has authored is complete, non-parochial, and traceable.

## The four source corpora and what each is good for

The four published sources that an AI-auditor should treat as criteria for a harm-model completeness test:

### 1. AI Incident Database (AIID)

Partnership on AI maintains the **AI Incident Database** at `incidentdatabase.ai`. Each incident is a structured record of an AI-system harm that *actually occurred* in deployment: who was harmed, which system, which developer, which year, and the public reporting trail. The database follows an aviation-incident-reporting shape — incidents are curated rather than crowdsourced, and each record has a public case ID.

For the auditor, AIID is a *grounding* resource: a harm-model category without at least one AIID precedent is a category the vendor is asserting on its own authority, which is a weaker epistemic position than a category grounded in a specific reported incident. The auditor looks for category-to-incident grounding, not the absence of category-to-incident grounding.

### 2. OECD.AI Incidents Monitor (AIM)

The **OECD.AI Incidents Monitor** (`oecd.ai/en/incidents`) is a complementary tracker focused on incidents and hazards with an OECD-policy framing. It cross-references AIID records and adds media-tracked incidents. For the auditor, AIM is useful because its categorisation is close to the OECD AI Principles and the policy framings jurisdictions use when drafting obligations; a harm model that maps cleanly to AIM categories is likely to map cleanly to the Article-9 (risk management) obligations of the EU AI Act. <!-- needs-research: confirm OECD AIM categorisation scheme and any 2025–2026 revisions at reading time -->

### 3. MIT AI Risk Repository

The **MIT AI Risk Repository** (`airisk.mit.edu`) is a living meta-review of AI-risk taxonomies published in academic and industry sources. It encodes a two-dimensional classification: a *causal taxonomy* (entity, intent, timing) and a *domain taxonomy* (seven domains with sub-domains). The Repository's own position is that no single prior taxonomy is complete; the Repository is useful as a *coverage frame* precisely because it aggregates other taxonomies.

For the auditor, the MIT Repository's domain axis — Discrimination & Toxicity, Privacy & Security, Misinformation, Malicious Use, Human-Computer Interaction, Socioeconomic & Environmental, AI System Safety — is a defensible completeness checklist: a harm model that silently omits one of the seven top-level domains is a documentation finding.

### 4. AIRO ontology

The **AIRO** (AI Risk Ontology) is a published ontology developed in the AI-governance research community that models AI systems, risk sources, risks, and controls as linked concepts, drawing on ISO/IEC 23894 and the EU AI Act drafting. <!-- needs-research: cite the current AIRO paper and the ontology URL at reading time; AIRO has been published in the Digital Governance Research Group output and in W3C-adjacent venues --> For the auditor, AIRO is useful because the ontology prescribes *trace shapes* — risk source → risk → risk treatment → control → evidence — that a harm model can be audited against.

### 5. NIST AI 600-1 Generative AI Profile

The **NIST AI 600-1 Generative AI Profile** (July 2024) enumerates twelve risks that are "unique to or exacerbated by generative AI": CBRN information, confabulation, dangerous or violent recommendations, data privacy, environmental impact, harmful bias, human-AI configuration, information integrity, information security, intellectual property, obscene/degrading/abusive content (including CSAM and NCII), and value chain / component integration. <!-- needs-research: verify the AI 600-1 final-publication risk count and names at reading time --> This is the criterion to test any GenAI harm model against: a GenAI system harm model that omits one of the AI 600-1 categories without justification is a completeness finding against NIST AI 600-1.

## The completeness test

The auditor's first fieldwork step on the harm model is a **completeness grid**: the organisation's harm categories as rows, and the five source corpora as columns. For each cell, the auditor records "covered" / "partially covered" / "uncovered." The grid surfaces categories the organisation has adopted that no public corpus flags (likely parochial elaboration — may or may not be a finding) and, more importantly, categories that the public corpora flag that the organisation has silently omitted (almost always a finding).

| Organisation harm category | AIID precedents | OECD AIM | MIT Repo domain | AIRO concept | AI 600-1 category |
|----------------------------|-----------------|----------|-----------------|--------------|-------------------|
| CSAM generation            | multiple        | yes      | Discrim. & Tox. | risk-source  | CSAM/NCII         |
| Prompt-injection data exfil| multiple (AIID 594, …) | yes | Privacy & Sec. | risk-source  | Info. Security    |
| Model-driven self-harm     | multiple (AIID …) | yes | HCI              | risk-source  | Harmful content   |
| …                           | …               | …        | …                | …            | …                 |

Three rules for the grid:

1. **Use the public corpus category name, not a rephrasing.** The grid is for traceability; the regulator will cross-check the organisation's claim against the public corpus wording.
2. **Cite the AIID case ID** (or the OECD AIM record ID) in the cell, not just "yes." A category cited without an incident ID is a weaker grounding than one with.
3. **Flag silent omissions explicitly.** If AI 600-1 lists CBRN and the organisation's harm model has no CBRN row, that is not "not applicable" by default; it is a finding unless the organisation has documented a scope-exclusion rationale.

## The parochialism test

Vendors frequently author harm models that reflect their product posture ("we are a search company, so our harm model is organised around search quality") rather than the risk corpus. The *parochialism test* checks whether the harm categories track the external risk landscape or only the organisation's product metaphor.

Audit procedures:

- Spot-check five random AIID incidents of the previous twelve months against the organisation's harm model. If a high-profile recent incident is not representable in the taxonomy, that is parochialism.
- Spot-check five NIST AI 600-1 categories against the harm model. If a category requires a new row the organisation has not authored, that is parochialism.
- Compare the harm-model vocabulary to the MIT Repository domain names. Custom vocabulary is permitted; silent omission of an entire domain is not.

The auditor reports parochialism as a *finding on the harm-model authoring process*, not as a technical finding — the response the auditor is seeking is a revised taxonomy with a documented sourcing rationale.

## The harm-to-evaluation-to-control-to-monitor trace

A harm model is only operationally useful if each harm is traceable through four layers. The auditor's second fieldwork step is to pull a sample of harms and trace them:

```
harm category  →  evaluation(s) that test for it  →  control(s) that prevent / detect it  →  monitor(s) that watch the control
```

For each sampled harm, the auditor records:

- **Harm description.** Verbatim from the organisation's taxonomy.
- **Evaluation locus.** Which HarmBench behaviour, AIR-Bench category, AgentDojo task, InjecAgent category, WMDP subset, MLCommons AILuminate hazard, or internal eval covers it. Omission is a finding.
- **Control locus.** Which input guardrail, output guardrail, tool allow-list, system-prompt clause, model-training mitigation (RLHF refusal, Constitutional AI, unlearning), or policy rule addresses it.
- **Monitor locus.** Which production telemetry (refusal-rate metric, alert rule, incident channel, red-team-replay cadence) watches whether the control is working post-deployment.

A harm with a broken trace at any layer is a finding. The common patterns:

- **Harm exists, no evaluation.** The organisation cannot measure whether the control works; this is a Grade-E assertion in the chapter-1 (mod-106) sense.
- **Evaluation exists, no control.** The eval produces a score with no mitigation in flight; the finding is "no risk treatment."
- **Control exists, no monitor.** A control that is never re-checked after deployment is a one-time-assurance artefact; the finding is "no post-market surveillance" (feeds `mod-108`).
- **Monitor exists, but evaluates something other than the harm.** The monitor's output does not refute or confirm whether the harm is happening; the finding is "monitor-off-target."

The trace is also an input to the risk-register audit (chapter 2) — the risk-register entry for a harm must reference the same evaluation / control / monitor the trace identifies, or the two are out of sync.

### Worked trace

| Field | Value |
|-------|-------|
| Harm | Indirect prompt-injection causing unauthorised tool-use data exfiltration |
| AIID / 600-1 grounding | NIST AI 600-1 "Information Security"; OWASP LLM01 "Prompt Injection"; AIID case 594 (and others) <!-- needs-research: confirm the specific AIID case numbers for indirect-prompt-injection incidents at reading time --> |
| Evaluation | InjecAgent (ACL Findings 2024); AgentDojo (NeurIPS 2024 D&B) — run quarterly via Inspect harness |
| Control | Input guardrail Llama Guard 3; output tool-use allow-list with host-level egress policy; model fine-tune refusal for suspected injections |
| Monitor | `security.tool_use_injection_suspected_rate` with 1h / 1d alert thresholds; quarterly red-team replay |
| Trace status | complete |

The register entry for the same harm must cite the same evaluation and control. If it cites a different control, chapter 2's register audit opens the inconsistency.

## Severity, likelihood, and the harm-model ↔ risk-taxonomy boundary

The *harm model* is the catalogue of harms. The *risk taxonomy* layers severity, likelihood, and sometimes velocity / detectability over the harm catalogue. The auditor treats them as separate test subjects even if the organisation combines them in one document:

- **Harm-model completeness.** The grid test above.
- **Risk-taxonomy calibration.** Whether the severity scale distinguishes meaningfully between rare-catastrophic and common-moderate harms, whether the likelihood scale is coherent across time horizons, whether the aggregation rule is defined (max-of-components? sum? expected-loss?).
- **Taxonomy ↔ ISO 23894 crosswalk.** ISO/IEC 23894 "Guidance on risk management" is the normative shape for AI risk management the organisation almost certainly cites; the auditor checks that the organisation's taxonomy terms map to ISO 23894's concepts.

Scoring consistency sits in chapter 2 (risk-register audit); the chapter-1 test is whether the taxonomy *can support* consistent scoring — whether its scales are well-defined, operationalised, and documented.

## The Generative-AI-specific overlay

For an organisation operating GenAI (chat assistants, agentic systems, image / audio / video models), the auditor overlays the NIST AI 600-1 twelve-category structure on the harm model as a required test:

| NIST AI 600-1 category | Common evaluation locus | Typical control locus |
|-------------------------|-------------------------|-----------------------|
| CBRN information        | WMDP; HarmBench "biosecurity"; internal red-team CBRN suites | RLHF refusal; constitutional classifier; vendor guardrail allow/deny |
| Confabulation           | Internal RAG grounding eval; TruthfulQA; HELM factual | Grounding citation; RAG retrieval requirements; UI disclaimer |
| Dangerous/violent recs  | HarmBench "harassment"; AIR-Bench; AILuminate | Llama Guard; constitutional classifier |
| Data privacy            | MIA/LiRA; membership-inference pipeline; Presidio PII detection | DP-SGD training; output PII filter; access control |
| Environmental impact    | FLOPs / energy accounting | Scheduling policy; model-selection policy |
| Harmful bias            | Fairlearn; AIF360; subgroup eval; Gender Shades (vision) | Debiasing pipeline; threshold-by-group policy |
| Human–AI configuration  | Oversight-sampling audit; UI disclosure audit | HITL review gate; UI disclosure |
| Information integrity   | TruthfulQA; AILuminate misinformation | Grounding; watermark; provenance (C2PA) |
| Information security    | AgentDojo; InjecAgent; LLM01 red-team | Input / output / tool guardrail; egress policy |
| Intellectual property   | MemFree / training-data overlap eval; code-license-attribution eval | Filtering; opt-out honouring; licence attribution |
| Obscene / CSAM / NCII   | CSAM classifier hit-rate; NCII classifier hit-rate | Classifier guardrail (output); upstream data filtration |
| Value chain / component | SBOM; supplier attestation (feeds `mod-109`) | Vendor attestation; downstream-component guardrail |

A GenAI harm model missing any of the twelve rows above (and the organisation cannot cite a scope-exclusion rationale) is a NIST AI 600-1 conformance finding.

## Sampling the harm model

The auditor does not trace every harm; sample selection follows `mod-104` discipline (ISA 530 if under IAASB; AU-C 530 if under AICPA):

- **Risk-weighted stratification.** The organisation's own severity scoring is one stratifier; AIID incident-count in the last 12 months is another; the regulator's declared priorities a third.
- **Minimum coverage.** At least one harm per NIST AI 600-1 category (for GenAI); at least one harm per MIT Repository domain; at least one high-severity harm.
- **Reperform.** For each sampled harm, the auditor independently constructs the trace from the external corpora and the organisation's artefacts, then compares to the organisation's own documented trace.
- **Finding density.** Record the number of sampled harms, the number of broken traces, and the pattern (which layer broke most often).

Sample-size justification is part of the workpaper, not an afterthought.

## Common failure modes

- **Treating the harm model as fixed.** The AIID and OECD AIM gain new records weekly; a harm model authored twelve months ago and never re-indexed is stale. The auditor tests update cadence.
- **Accepting "we follow NIST AI 600-1" without the per-category evidence.** A policy statement that cites a framework is not conformance; the twelve rows above must be present.
- **Confusing the harm-model completeness test with the risk-register audit.** Completeness is about the *rows*; the register audit (chapter 2) is about the *scoring, approval, and aggregation* of those rows.
- **Letting the vendor's AIID selection bias the grid.** The vendor will cite the AIID incidents favourable to its narrative; the auditor pulls a fresh random sample.
- **Scoring the whole model with one letter grade.** Completeness is per-category; one AI 600-1 omission does not invalidate the other eleven.
- **Testing the harm model in isolation from deployment context.** A harm model that is complete for a search engine will miss agentic-system risks if the organisation is deploying agents. The audit scope statement (`mod-103`) must fix the deployment context first.

## Summary

- The harm model is the first audit subject in a risk-management engagement because every downstream artefact inherits its coverage.
- Five published corpora are the auditor's criteria: AIID, OECD.AI Incidents Monitor, MIT AI Risk Repository, AIRO ontology, NIST AI 600-1 GenAI Profile.
- The completeness test is a grid: organisation harm categories × source corpora, with cell-level grounding citations.
- The parochialism test checks the harm model against recent AIID incidents and the AI 600-1 categories that the organisation did not independently author.
- Every sampled harm must trace *harm → evaluation → control → monitor*; broken traces are findings the register audit (chapter 2) will re-encounter.
- For GenAI systems, the NIST AI 600-1 twelve-category overlay is a required test; silent omissions are conformance findings.
- Severity / likelihood calibration is a separate layer; the chapter-1 test is only whether the taxonomy *supports* consistent scoring.
