# GPAI with Systemic Risk — The Article 55 and Code-of-Practice Audit Path

## Motivation

Chapter 1 covered the **product** route — a high-risk AI system heading for CE marking. Chapter 2 covers the **model** route — a **general-purpose AI model** heading for market entry across the EU, specifically the subset of GPAI models whose scale and capability place them above the **systemic-risk threshold** of Article 51.

The EU AI Act treats GPAI models as a distinct regulated object. Chapter V (Articles 51–56) imposes two tiers of obligation. All GPAI model providers carry the Chapter V Section 2 obligations (Articles 53 and 54 — technical documentation, copyright policy, cooperation with downstream deployers and the AI Office). Providers of **GPAI models with systemic risk** carry additional obligations under **Article 55** — model evaluations including adversarial testing, systemic-risk assessment and mitigation, cybersecurity protection of the model and physical infrastructure, and serious-incident reporting to the AI Office.

The auditor arrives here as an **assurance auditor engaged by the GPAI provider** (because the AI Office's own supervisory power under Article 92 authorises evaluations the provider will want to pre-rehearse), as an **adherence auditor under the GPAI Code of Practice** (the voluntary Article 56 instrument), or as a **model-provider-side auditor engaged by a systemic-risk peer** (coordinated safety institutes, AISI / AISAI arrangements). This chapter is the auditor's shape for that engagement. It is deliberately a *shape* — the deep methodology for frontier-model safety evaluations lives up-track at `agentic-safety-engineer` (level 40); the auditor's job is to *verify* evaluations, not to run them.

## The Chapter V obligation stack

The auditor's first workpaper is the obligation stack for the specific GPAI model.

### Baseline — all GPAI models (Article 53)

- **Article 53(1)(a)** — Technical documentation of the model, including training and testing process and evaluation results, to be kept up to date and made available to the AI Office and national competent authorities on request. Annex XI enumerates the minimum content.
- **Article 53(1)(b)** — Information and documentation for providers of AI systems who intend to integrate the GPAI model into their AI systems, sufficient to allow those providers to meet their own obligations under the Regulation. Annex XII enumerates the minimum content.
- **Article 53(1)(c)** — A policy to comply with Union copyright law and related rights, in particular to identify and comply with reservations of rights expressed under Article 4(3) of Directive (EU) 2019/790 on copyright in the digital single market.
- **Article 53(1)(d)** — A sufficiently detailed **summary about the content used for training** of the GPAI model, according to a template provided by the AI Office.

Open-source GPAI providers can avail of the Article 53(2) exemption from (1)(a) and (1)(b), provided the model weights and architecture information are made publicly available under a free and open-source licence and provided the model is **not** a GPAI model with systemic risk (and provided the model does not present specified risks).

### Systemic-risk threshold — Article 51

A GPAI model is designated as having **systemic risk** when it meets either of:

- **High-impact capabilities** evaluated on the basis of appropriate technical tools and methodologies, including indicators and benchmarks (Article 51(1)(a)); the Act's rebuttable presumption sets the compute threshold at **10^25 FLOPs** of cumulative training compute (Article 51(2)), which the Commission may adjust via Article 97 delegated acts.
- **Equivalent impact or capabilities** determined by the Commission *ex officio* or following a qualified alert by the scientific panel (Article 51(1)(b) and Annex XIII criteria).

The provider must **notify the Commission without delay and in any event within two weeks** when either condition is met or when it reasonably foresees it will be met (Article 52).

### Systemic-risk tier — Article 55

Providers of GPAI models with systemic risk shall, in addition to Article 53:

- **Article 55(1)(a)** — Perform **model evaluation** in accordance with standardised protocols and tools reflecting the state of the art, including conducting and documenting adversarial testing of the model with a view to identifying and mitigating systemic risks.
- **Article 55(1)(b)** — **Assess and mitigate possible systemic risks** at Union level, including their sources, that may stem from the development, placing on the market, or use of GPAI models with systemic risk.
- **Article 55(1)(c)** — **Keep track of, document, and report, without undue delay**, to the AI Office and, as appropriate, to national competent authorities, relevant information about serious incidents and possible corrective measures to address them.
- **Article 55(1)(d)** — Ensure an **adequate level of cybersecurity protection** for the GPAI model with systemic risk and the physical infrastructure of the model.

Article 55(2) allows providers to **rely on codes of practice** within the meaning of Article 56 to demonstrate compliance; adherence to an adequate code of practice is a presumptive compliance pathway until harmonised standards are adopted.

## The Code of Practice — Article 56 and the audit lever it creates

Article 56 tasks the AI Office with facilitating the drawing up of **codes of practice** at Union level to contribute to the proper application of the Regulation. The first such code — the **GPAI Code of Practice** — is a multi-stakeholder-drafted instrument covering transparency, copyright, and safety-and-security commitments, with measures and KPIs under each commitment. Providers who sign and adhere to the Code benefit from the Article 55(2) presumption. <!-- needs-research: confirm the final publication version, signatory list, and exact commitment numbering of the GPAI Code of Practice at reading time; the Code's drafting cycle continues to evolve through its revision track -->

The Code structure that the auditor tests against is three chapters:

1. **Transparency chapter.** Documentation of the model per Annex XI; information for downstream providers per Annex XII; training-data summary per Article 53(1)(d); copyright policy per Article 53(1)(c). (This chapter binds *all* GPAI providers who sign, not only systemic-risk tier.)
2. **Copyright chapter.** Operationalisation of Article 53(1)(c) copyright policy — in particular the opt-out respect mechanism under Article 4(3) of the DSM Directive, provenance of training data, and a complaints procedure.
3. **Safety-and-security chapter.** Operationalisation of Article 55 obligations — systemic-risk assessment and management framework, state-of-the-art evaluations and reporting, systemic-risk mitigations, incident reporting, and cybersecurity.

The auditor who wants to say "the provider meets Article 55" tests adherence to the safety-and-security chapter of the Code. The auditor who wants to say "the provider does not meet Article 55" can reach for direct obligations in Article 55 itself rather than the Code.

## Auditing Article 55(1)(a) — model evaluations and adversarial testing

The provider must perform **state-of-the-art** model evaluations covering **systemic risks**. The Act and the Code do not enumerate every evaluation; they require state-of-the-art, documented, and subjected to adversarial testing.

The auditor's test shape:

- **Evaluation inventory.** The complete set of evaluations performed on the systemic-risk model in the current cycle: capability evaluations (benchmark set), risk-category evaluations (CBRN uplift, cyber-offence uplift, autonomous replication, loss-of-control, manipulation, dangerous persuasion), misuse evaluations (jailbreak resistance, instruction-following under adversarial inputs), societal-harm evaluations (bias, discrimination, misinformation-at-scale).
- **Methodology adequacy.** For each evaluation: pre-registered methodology (where applicable); held-out evaluation data not in the training set (contamination check); appropriate statistical treatment (confidence intervals; multiple comparisons); threat-model justification (why this evaluation covers this risk category).
- **State-of-the-art reference.** Evidence that the evaluation set reflects current practice — citations to AISI / AISAI / peer-reviewed evaluations, participation in coordinated eval rounds, adoption of community-maintained benchmarks (METR autonomy, Cybench, CBRN uplift evaluations, SWE-Bench variants). The auditor does not endorse any specific benchmark; the test is whether the provider can defend their set as *representative of the state of the art at the time of evaluation*.
- **Adversarial testing.** Red-team composition (internal; external; both); scope statement; scenarios and attack trees exercised; coverage of the Article 55 risk categories; evidence of *attempts* that succeeded, not only ones that failed; the organisation's response and, where appropriate, mitigation retained.
- **Evaluation independence.** Who ran the evaluations and under what independence regime from the model-development team. For contested categories (dual-use CBRN uplift, autonomous replication) the audit values external, independent evaluator access — AISI / AISAI arrangements, trusted-third-party evaluations, or academic access programmes.
- **Pre-deployment and iterative evaluations.** Evidence the evaluations ran **before** the model was placed on the market **and** at material internal milestones (post-RLHF, post-safety-training, post-system-prompt-change). For systemic-risk-tier models, the auditor expects evidence of **capability-elicitation** attempts — not evaluating the model as it ships, but evaluating its underlying capabilities under elicitation prompts that reduce safety-training suppression.

The auditor stops short of **re-running** the evaluations (level-40 methodology work). The auditor's test is **whether a competent third party *could* reproduce the evaluation given the evidence the provider retains**. Evaluations the auditor cannot in principle reproduce from provider evidence are a finding against Article 55(1)(a).

## Auditing Article 55(1)(b) — systemic-risk assessment and mitigation

The provider must **assess** and **mitigate** systemic risks. The audit test applies a risk-management shape adapted to the model-level object.

### The systemic-risk inventory

The provider maintains an inventory of systemic risks relevant to the model, including sources. The auditor expects at minimum the categories named in the Act's recitals and Code of Practice:

- **CBRN risks** — chemical, biological, radiological, nuclear uplift.
- **Cyber risks** — offensive-cyber uplift, zero-day discovery, exploit development, scalable intrusion assistance.
- **Autonomous-agent risks** — self-replication, long-horizon task completion in adversarial environments, resource-acquisition, deception-under-evaluation.
- **Loss-of-control risks** — alignment failure modes relevant at the deployed scale.
- **Manipulation and influence risks** — mass-persuasion at scale, synthetic-content attacks.
- **Discrimination and fundamental-rights risks** — differential performance that could ground Union-level systemic harm (electoral, labour-market, judicial).

The auditor's inventory test confirms coverage of each category or the provider's documented rationale for deprioritisation.

### Mitigations

For each identified risk, the provider documents mitigations across pre-training (data curation, filtering, data-poisoning defence), training (safety fine-tuning, RLHF, constitutional training, refusal training), deployment (system-level filters, input/output classifiers, rate limits), access controls (tiered access, usage monitoring, API-vs-weights decisions), and monitoring (post-deployment incident signal, red-team-on-production).

Audit test: for each systemic-risk inventory entry, trace from risk identification to evaluation result (was the risk measured?) to mitigation decision (what did the provider do?) to effectiveness evidence (does the mitigation reduce the measured risk?) to residual-risk acceptance (who accepted the residual and on what basis?). A risk category with named mitigations and no evaluation of mitigation effectiveness is a finding.

### Decisions on distribution and access

Systemic-risk providers face **distribution decisions** — weights-release vs. API-only; tiered API access; researcher-access programmes; staged rollout. The audit does not opine on the decision; it audits the **decision process** — who authorised what distribution shape, on what evidence, with what residual-risk acceptance, with what reversibility if signal emerges post-release. Reversibility of weights release is limited; the audit flags where that limitation is acknowledged and where it is not.

## Auditing Article 55(1)(c) — incident reporting

Systemic-risk providers must track, document, and report to the AI Office — without undue delay — serious incidents and possible corrective measures.

The Act references the broader serious-incident regime that `mod-108` chapter 4 covers for the Article 73 deployer-side obligation; at the GPAI-model level the reporting goes to the **AI Office**, not national market-surveillance authorities. The audit test:

- **Incident taxonomy.** A documented taxonomy categorising events as near-misses, incidents, serious incidents, systemic events; the thresholds for each tier; the mapping to Article 55(1)(c).
- **Detection channels.** Signal sources — internal eval failures, red-team discoveries, external-researcher disclosures (coordinated or uncoordinated), customer-/API-tenant reports, media and public-disclosure monitoring, government liaison channels.
- **Triage and escalation.** Defined roles with decision authority to classify an event to the "serious-incident" tier and initiate the AI-Office report.
- **Timeliness.** Evidence that reports were sent *without undue delay* (the Act does not fix a numeric clock for Article 55(1)(c) as it does for Article 73 serious incidents; "without undue delay" is interpreted against the specific incident's facts); timeliness findings are a specific and recurring category.
- **Content adequacy.** The report content reflects the information the AI Office needs to understand the event, the systemic significance, the mitigation underway, and the planned corrective actions; inadequate first reports are permitted if followed by updated reports.
- **Corrective-measure follow-through.** Reports identify corrective measures; the audit tests that those measures were actually implemented.

A provider with an incident taxonomy that cannot distinguish "jailbreak found by one user and fixed in a prompt-injection filter" (not a systemic-risk serious incident) from "publicly reproduced capability demonstration in the CBRN uplift category" (clearly a systemic-risk serious incident) is a finding against Article 55(1)(c).

## Auditing Article 55(1)(d) — cybersecurity

The provider must ensure adequate cybersecurity protection for the GPAI model and its physical infrastructure. The audit reaches:

- **Weights protection.** Access controls on training checkpoints and final weights; insider-risk controls; supply-chain controls on the training-and-inference stack; encryption at rest and in transit; attestation of hardware (confidential-computing / TEEs where applicable).
- **Training-pipeline integrity.** Data poisoning defences; build-pipeline integrity (SLSA); model-signing and attestation of produced weights (`mod-109` chapter 6 overlap).
- **Inference-infrastructure security.** The hosting infrastructure's security posture (SOC 2 / ISO 27001 / FedRAMP / internal equivalents).
- **AI-specific threat defence.** Model-extraction defences (rate limits, differential-privacy-at-query layers, response-level watermarking); prompt-injection defence depth; jailbreak monitoring and iterative refusal-training response.
- **Incident-response readiness.** The response plan specifically for cyber-origin AI incidents — weight exfiltration, training-pipeline compromise, prompt-injection-at-scale.

The cybersecurity test interfaces with the Article 15 cybersecurity audit of chapter 1 but is **model-level** rather than **AI-system-level** — the subject is the GPAI model itself as an artifact, not a deployed system incorporating it.

## The evidence shape the auditor demands

For a systemic-risk GPAI audit the provider must be able to produce, under non-disclosure and with suitable protections:

- **Annex XI technical documentation** — tasks, model architecture (where IP-protected: appropriately redacted), training data (summary and detailed as applicable), training cost, evaluation results, risk management documentation, cybersecurity measures.
- **Annex XII downstream-provider documentation** — tasks the model can perform, intended uses, acceptable-use boundaries, technical means for integration, computational and hardware resources, model behaviour, training data (summary), known limitations, decisions on risk categorisation and safety-and-security measures.
- **Training-data summary** per Article 53(1)(d) — against the AI-Office template. <!-- needs-research: confirm the AI Office's training-data-summary template version at reading time -->
- **Copyright policy** per Article 53(1)(c) — including the operational mechanism for respecting Article 4(3) DSM Directive opt-outs.
- **Systemic-risk assessment and mitigation framework** — the policy document, the risk inventory, the mitigations, the residual-risk acceptance records.
- **Evaluation reports** — per evaluation; methodology, result, confidence, evaluator identity and independence posture.
- **Red-team reports** — with scope, methods, findings, severity, response.
- **Incident records** — the Article 55(1)(c) log, with reports to the AI Office evidenced.
- **Cybersecurity architecture and testing evidence** — the model-level threat model, the defences, the penetration-test or red-team cyber evidence.
- **Governance records** — board / committee records of distribution decisions, residual-risk acceptances, access-policy changes.

For Code-of-Practice signatories, the audit also tests adherence to specific Code commitments and KPIs where the Code specifies them.

## What this audit does not do — deferring up to agentic-safety-engineer level 40

This auditor's chapter deliberately defers the following upward to `agentic-safety-engineer` level 40 and its deeper methodology chapters:

- The methodology for **frontier capability elicitation** (how to construct scaffolded agents that reveal capabilities in-the-limit).
- The methodology for **autonomous-replication and resource-acquisition evaluations** (METR-style, with scaffolding details, live-network concerns, and measurement of self-exfiltration).
- The **CBRN uplift measurement methodology** — the specific experimental protocols used by national safety institutes.
- The **loss-of-control / alignment-evaluation methodology** — scheming, deceptive alignment, sandbox escape evaluations.
- The **mechanistic-interpretability** evidence an evaluator may use to triangulate behavioural claims.

The auditor's job is to **verify** that an evaluator competent in these methodologies ran the evaluation and that the provider can defend the result — not to design or re-run the evaluation. The auditor sources state-of-the-art expertise under ISA 620 / AT-C 105 reliance (chapter 8) when the audit requires methodology depth beyond the auditor's own competence.

## The engagement output

The audit output for a systemic-risk GPAI engagement is three artefacts:

1. **An opinion on Article 53 compliance** — transparency, downstream-provider information, copyright, training-data summary.
2. **An opinion on Article 55 compliance (or adherence to the Code of Practice safety-and-security chapter)** — evaluations, risk assessment and mitigation, incident reporting, cybersecurity.
3. **A set of corrective-action requests** — specific, closable items the provider addresses on a defined cadence.

For a Code-of-Practice signatory, the engagement may also produce a public **adherence statement** depending on the Code's own reporting regime.

## Interfaces to adjacent chapters and modules

- **Chapter 1** covers the Article 43/44 conformity-assessment lane for high-risk AI systems that *use* GPAI models; providers supplying both a system and its underlying model may face both audit shapes.
- **Chapter 3 (ForHumanity IAAIS)** sometimes covers GPAI deployer-side obligations in US contexts where no notified-body audit applies but a voluntary audit is contracted.
- **Chapter 9 (engagement shape chooser)** returns here when the subject is a GPAI model above the systemic-risk threshold.
- **`mod-106`** (model and system card claims) feeds the Annex XI and Annex XII evidence-reliability audit.
- **`mod-108` chapter 4** (serious-incident reporting) overlaps for the incident-reporting pipeline at the GPAI provider; the Article 55(1)(c) report to the AI Office is distinct from the Article 73 deployer report to market-surveillance authorities.
- **`mod-109` chapter 5** (GPAI deployer obligations) covers the downstream deployer's audit; this chapter covers the model-provider's audit.

## Common failure modes

- **Threshold-date drift.** Provider crosses the Article 51(2) FLOP threshold during training without triggering Article 52 notification.
- **Benchmark-contamination** of evaluation suites — training set contains eval items.
- **Capability elicitation absent.** Evaluations run on the shipped model without attempts to defeat safety training; auditor cannot infer capability.
- **Red-team captive.** Internal red-team only, embedded in the development team, no scoped external exercise.
- **Mitigation effectiveness unmeasured.** Mitigations deployed on the strength of design; no evaluation of residual risk post-mitigation.
- **Incident taxonomy flat.** Everything is either "ok" or "major"; no tiering; no pre-defined triggers to AI Office.
- **Cybersecurity model-level missing.** ISO 27001 posture exists for the company, no defences specifically tied to the model as an artifact (weights, training pipeline).
- **Distribution-decision evidence missing.** Weights released on strength of an email thread; no board record; no residual-risk-acceptance memo.
- **Code adherence confused with compliance.** Provider signs the Code and treats the signature as compliance proof; audit must test *adherence to Code commitments*, not the fact of signing.
- **Training-data summary template drift.** Provider uses an internal template rather than the AI-Office template; summary is not comparable.

## Summary

- GPAI models are regulated under the AI Act's Chapter V; all GPAI providers carry Article 53 (transparency, downstream-information, copyright, training-data summary); providers of GPAI with systemic risk carry Article 55 (evaluations including adversarial testing, systemic-risk assessment and mitigation, incident reporting, cybersecurity).
- Systemic-risk designation flows from Article 51 — high-impact capabilities, with the 10^25 FLOPs training-compute presumption, or Commission designation on Annex XIII criteria; providers must notify the Commission within two weeks under Article 52.
- The GPAI Code of Practice under Article 56 is the voluntary presumption-of-compliance instrument; the auditor tests adherence to its transparency, copyright, and safety-and-security chapters.
- The auditor's Article 55 tests cover model evaluations (state of the art, reproducible from provider evidence, independent where appropriate), systemic-risk assessment and mitigations (inventory, measurement, mitigation-effectiveness), incident reporting (taxonomy, timeliness, content, follow-through), and cybersecurity (model-level, not only company-level).
- Methodology depth for frontier-capability evaluations defers upward to `agentic-safety-engineer` level 40; the auditor's role is verification, with ISA 620 / AT-C 105 reliance on external experts where methodology competence is beyond the auditor's own.
- The engagement output is opinions on Article 53 and Article 55 compliance (or Code adherence), with specific corrective-action requests and, for signatories, an adherence statement per the Code's reporting regime.
