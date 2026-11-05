# Sector and Jurisdictional Overlays — Additive Criteria on Top of the Horizontal Stack

## Motivation

ISO/IEC 42001, NIST AI RMF, and the EU AI Act give the AI Auditor a horizontal baseline. Real engagements are rarely horizontal: a bank's AI model is also a *model* under **SR 11-7 / OCC 2011-12 / Fed SR 23-4**; a hospital's AI/ML triage system is also a *medical device* under **FDA GMLP + PCCP + 21 CFR Part 820**; an employer's screening tool is also a *bias-audited AEDT* under **NYC Local Law 144** and an *algorithmic discrimination* risk under **Colorado SB 24-205**; a US federal agency's AI system is also inventoried and governed under **OMB M-24-10 / M-25-21**. Each sector or jurisdictional regime adds *additive* criteria to the horizontal baseline — the same control may be tested in parallel against ISO/IEC 42001, NIST AI RMF, the EU AI Act, *and* the sector rule. This chapter walks each major overlay, points at what criteria it adds, and flags where evidence can be re-used across overlays. The crosswalk register in chapter 6 is how you keep them consistent.

## Design rule — overlays are additive, not substitutes

Before any specific regime: the discipline is *additive*. An AI system in a US bank, used for credit origination to EU consumers, is simultaneously:

- A **high-risk AI system** under EU AI Act Annex III point 5(b) with Articles 9–15 obligations.
- A **model** under SR 11-7 with model-risk-management obligations (development, implementation, use, model validation).
- Subject to **ECOA / Regulation B** adverse-action and bias-related consumer-protection law.
- Potentially subject to **Colorado SB 24-205** if used on Colorado consumers.
- Covered by the organisation's horizontal ISO/IEC 42001 AIMS and the control library built against it.

The AI Auditor does not re-test the same control five times. The *evidence* is shared; the *criteria* are the superset; the *findings* are mapped back to each regime by the crosswalk register (chapter 6). What matters here is knowing each overlay well enough to translate its unique obligations into criteria.

## US financial-sector overlay — SR 11-7, OCC 2011-12, and the AI-era updates

The **Federal Reserve SR 11-7 / OCC Bulletin 2011-12** supervisory guidance on model risk management is the dominant US bank-supervisory framework for anything the bank uses as a model. AI systems in banks are treated as models, and the three-stage MRM framework applies:

- **Model development, implementation, and use** — conceptual soundness, outcomes analysis, ongoing monitoring, governance.
- **Model validation** — independent review covering conceptual-soundness assessment, outcomes analysis, benchmark testing.
- **Governance, policies, and controls** — board and senior management oversight, model inventory, documentation.

The AI-era supervisory posture is sharpened in:

- **Fed SR 23-4** interagency guidance on third-party risk management (joint with OCC and FDIC) that overlays SR 11-7 with third-party-risk requirements where the model is vendor-sourced or uses vendor components (training data, foundation models).
- **OCC Comptroller's Handbook — Model Risk Management** booklet updates; **FDIC RD-2017** and successor guidance.
- **CFPB guidance** on adverse-action notices for AI-based credit decisions.

Criteria translation points unique to the financial overlay (beyond what ISO/IEC 42001 and NIST AI RMF already cover):

- **Model inventory** at the SR 11-7 definition of "model" (a quantitative method, system, or approach that applies statistical, economic, financial, or mathematical theories…) — scoped broadly enough to capture AI and ML systems not labelled "models" in engineering.
- **Model risk tiering** by materiality, with tier-driven validation frequency.
- **Independent validation function** sitting *outside* the first line, with documented independence from model development, and performing conceptual-soundness, outcomes-analysis, benchmark testing.
- **Challenger-model benchmarking** for high-materiality models.
- **Outcomes analysis** against actuals, not against hold-out metrics alone.

```
Criterion ID:             C-SR11-7-VALIDATION-01
Source:                   Fed SR 11-7 — model validation.
Statement:                For each AI system classified as a model, the organisation has executed an independent validation during the audit period at the frequency required by the model's materiality tier, covering conceptual-soundness review, outcomes analysis, and benchmark / challenger testing, and has documented validation findings, remediation, and executive sign-off.
Evidence:                 Validation workpapers; validation report; independence attestation for validator; outcomes-analysis data; benchmark-model results; sign-off records.
Procedure:                Inspect validation workpapers; verify validator independence (reporting line + no recent development participation); re-perform a sampled subset of the outcomes analysis.
Measurable attributes:    % of in-scope models with current validation at required frequency; validation finding closure (%).
Owner:                    Second line (MRM) with independent validator.
Residual judgment:        AI/ML specifics — does the validation cover training-data drift, model-version changes between re-validations, and the GenAI-specific risks (hallucination, prompt-injection) where applicable?
```

## FDA AI/ML SaMD overlay — GMLP + PCCP + 21 CFR Part 820 (QSR / QMSR)

FDA's framework for AI/ML Software-as-a-Medical-Device (SaMD) layers three complementary stacks:

- **Good Machine Learning Practice (GMLP) — Guiding Principles** (joint FDA / Health Canada / UK MHRA, 2021; ongoing updates) — ten principles covering multidisciplinary expertise, software engineering + QS, representative data, independent datasets, model-design transparency, focus on the performance of the human-AI team, testing in clinically relevant conditions, user-focused information, deployed performance monitoring, and management of re-training.
- **Predetermined Change Control Plans (PCCP)** — FDA final guidance (2024) permitting pre-authorised change protocols for adaptive AI/ML devices, avoiding re-submission for changes within the plan.
- **21 CFR Part 820** quality system regulation — transitioning to the **Quality Management System Regulation (QMSR)** which incorporates ISO 13485:2016 (effective 2 February 2026). <!-- needs-research: confirm the QMSR final rule effective date and any amendments at reading time -->

Criteria translation points:

- **Intended use / indications for use** are documented and tested against — the FDA foundational criterion that bridges GMLP and the QMSR.
- **Representative training and test data** — criteria cover demographic, clinical, device, and site diversity relative to the indicated-use population.
- **Independent test datasets** separate from training — explicit evidentiary separation.
- **Human-AI team performance** — deployed-setting evaluation, not benchmark-only.
- **PCCP** — pre-authorised change protocol with methods for re-training, re-evaluation, and performance-change limits; post-change performance evidence.
- **Post-market surveillance and MDR** — serious-adverse-event reporting for AI/ML SaMD.

The FDA overlay interacts with the EU AI Act for medical AI placed on the EU market under the **EU MDR 2017/745 / IVDR 2017/746** regime; Article 6(1) safety-component path makes the medical device an *EU AI Act* high-risk system *and* an *MDR* device. One evidence set, two overlay criteria layers.

## HIPAA Security Rule overlay (and HHS AI guidance)

For AI systems handling Protected Health Information (PHI), **HIPAA Security Rule (45 CFR 160 and 164)** criteria extend the horizontal AIMS criteria with administrative, physical, and technical safeguards. HHS has published AI-adjacent guidance on PHI use in AI model training and inference. Criteria translation points:

- Administrative safeguards (security management, workforce security, information access management, security awareness, security incident procedures, contingency planning, evaluation, business-associate agreements).
- Technical safeguards (access control, audit controls, integrity, authentication, transmission security).
- Business Associate Agreement (BAA) coverage where AI vendors process PHI.
- **De-identification** under the Safe Harbor or Expert Determination methods for training-data sanitisation — frequent audit focus for LLM training corpora.

## NAIC Model Bulletin on the Use of AI by Insurers

The **NAIC Model Bulletin** (adopted December 2023; state-by-state adoption through 2024–2026) establishes supervisory expectations for insurer use of AI, drawing heavily on NIST AI RMF structure. States adopting the bulletin (many have done so) carry expectations that insurers maintain an AI Systems Program documenting governance, risk-management, third-party AI, testing and validation, and documentation. <!-- needs-research: confirm which states have adopted the NAIC Model Bulletin at reading time; adoption has rolled out state-by-state across 2024–2026 -->

Criteria translation here maps closely onto NIST AI RMF GOVERN / MAP / MEASURE / MANAGE with insurance-specific emphases: fair-discrimination laws (unfair-discrimination standards under state insurance code), rate filings, policyholder adverse-action notices.

## Colorado AI Act (SB 24-205)

**Colorado SB 24-205**, effective 1 February 2026, regulates deployers and developers of "high-risk artificial intelligence systems" making "consequential decisions". Deployer obligations include risk-management programs, impact assessments, consumer notices, adverse-action disclosures, and the right to appeal. Developer obligations include documentation that supports deployer obligations (disclosure to deployers, developer impact assessments, transparency to the Attorney General). <!-- needs-research: confirm any amendments to SB 24-205 that may land before or after the 1 February 2026 effective date -->

Criteria translation points unique to Colorado:

- **Consequential decision** scoping — matches EU AI Act high-risk scoping for many but not all use cases; translate the scope test explicitly.
- **Algorithmic discrimination** — the Act's substantive standard; criteria cover the organisation's affirmative-defence posture (reasonable care).
- **Pre-deployment and periodic impact assessments** — Colorado has its own content requirements; align the organisation's impact-assessment template to Colorado's checklist plus the ISO/IEC 42005 superset.
- **Adverse-action consumer notice** — content, timing, appeal process.

## NYC Local Law 144 — AEDT independent bias audit

NYC LL144 and the DCWP rules require employers using Automated Employment Decision Tools (AEDTs) to commission an **independent bias audit** annually and publish a summary; the AEDT must have been bias-audited within the prior year before use, and candidates must be notified. The audit itself is computed in a prescribed form (impact ratios by sex category, race/ethnicity category, and intersectional groups).

Criteria translation here is **narrow and formulaic** — unlike the horizontal frameworks, LL144 prescribes the computation and the publication form. The auditor's job is to:

- Confirm the AEDT scope match (the specific tool under audit matches the definition).
- Execute the bias computation on the dataset of candidates the AEDT was used on.
- Publish the summary with required content.
- Verify candidate notice.

The engagement is often executed by a bias-audit specialist firm (BABL AI and peers); the auditor independence test under the DCWP rules is strict (no financial interest in the AEDT or the employer in the relevant ways defined).

## Illinois AI Video Interview Act

Illinois 820 ILCS 42 regulates employer use of AI analysis of video interviews — notice, consent, destruction of videos on request, and demographic-data reporting to the Illinois Department of Commerce and Economic Opportunity. Criteria translation is almost entirely procedural and disclosure-based, with a small set of reporting criteria. Lightweight overlay but strict on procedure.

## US federal-agency overlay — OMB M-24-10 and M-25-21

**OMB M-24-10** (March 2024) directs federal agencies to govern AI use through a CAIO (Chief AI Officer), implement AI risk management for *rights-impacting* and *safety-impacting* AI, maintain AI use-case inventories, and publish them. **OMB M-25-21** (April 2025) and the EO 14110 / successor executive-order landscape continue to evolve the obligations. <!-- needs-research: confirm the live OMB AI memoranda, their successors, and the operative EO at reading time -->

Criteria translation points:

- **AI use-case inventory** complete, accurate, and current against OMB inventory requirements.
- **Rights-impacting / safety-impacting** classification per OMB categories, with minimum practices applied per category.
- **CAIO office** established with defined authority, reporting line, and resource.
- **Public inventory** published where required.

The OMB stack sits alongside **NIST SP 800-218A** (generative AI secure software development), **NIST AI 100-2** (adversarial ML taxonomy), **NIST SP 800-53** control-family mappings for federal AI systems.

## UK — the AI governance White Paper + regulator-led approach

The UK's **AI Regulation White Paper** (March 2023) and subsequent responses outline a sector-regulator-led approach rather than a horizontal AI Act. Sector regulators (ICO for data protection, FCA / PRA for finance, MHRA for medical devices, CMA for competition, Ofcom for online safety) have each issued AI-specific guidance. The **UK AI Safety Institute (AISI)** executes model-safety evaluations on frontier models. <!-- needs-research: confirm the UK's post-White-Paper trajectory at reading time; a statutory AI Bill has been under discussion and may have advanced -->

Criteria translation for UK engagements is sector-regulator-driven; use the applicable regulator's guidance as the overlay source, cite to the regulator-issued document, and crosswalk to NIST / ISO where possible.

## Canada — AIDA (proposed under C-27)

Canada's **Artificial Intelligence and Data Act (AIDA)** was introduced as part of Bill **C-27**. Status and content continue to move. <!-- needs-research: AIDA / C-27 enactment status and operative text at reading time — confirm before citing in criteria -->

## Singapore — AI Verify + Model AI Governance Framework

**Singapore's AI Verify** is a voluntary governance testing framework and toolkit from IMDA and PDPC combining process checks and technical testing. The **Model AI Governance Framework** (first edition 2019; GenAI edition 2024) provides principle-based guidance. For engagements in Singapore or for firms claiming AI Verify conformance, criteria translate against AI Verify's eleven principles-aligned testing categories. <!-- needs-research: confirm the current AI Verify release and the current Model AI Governance Framework edition at reading time -->

## Japan — AI Guidelines for Business

**Japan's AI Guidelines for Business** (METI / MIC, 2024) provide non-binding guidance aligned with the Hiroshima AI Process. Criteria translate against the Guidelines' common and actor-specific sections (developer, provider, business user). <!-- needs-research: confirm the current version at reading time -->

## Korea — AI Basic Act

Korea's **AI Basic Act** (enacted 2024, phased application through 2026) is a binding regime with high-impact AI obligations, transparency, and sanctions. <!-- needs-research: confirm the Act's operative provisions, effective dates, and implementing regulations at reading time -->

## India — DPDPA and IndiaAI

India's **Digital Personal Data Protection Act 2023** governs personal data used in AI; the **IndiaAI Mission** and MeitY frameworks shape voluntary posture. AI-specific obligations are developing. <!-- needs-research: confirm DPDPA implementing rules and IndiaAI frameworks at reading time -->

## Brazil — PL 2338

Brazil's **PL 2338 / 2023** proposes an EU-AI-Act-inspired regime with high-risk categories and provider/deployer obligations. <!-- needs-research: confirm enactment status and operative text at reading time -->

## China — Interim Measures for Generative AI Services, Deep Synthesis, Algorithmic Recommendation

China operates a composite AI regulatory stack: the **Interim Measures for the Management of Generative AI Services** (CAC, 2023), the **Deep Synthesis Provisions** (2022), the **Algorithmic Recommendation Provisions** (2022), and sector overlays. Providers of generative AI services to the public in China file security assessments and content-compliance filings with the CAC. <!-- needs-research: confirm live Chinese measures and their English translations at reading time -->

## Translation pattern across overlays

Every overlay adds one or more of four kinds of criteria to the horizontal baseline:

1. **Scope / classification criteria** — does this system fall under this regime (SR 11-7 "model" definition; EU AI Act "high-risk"; Colorado "consequential decision"; LL144 "AEDT"; FDA "SaMD" classification; NAIC "AI system").
2. **Documentation / disclosure criteria** — what the regime requires in writing (Annex IV technical documentation; SR 11-7 model documentation; LL144 bias-audit summary; FDA 510(k) / De Novo content; NAIC AI Systems Program documentation).
3. **Testing / evidence criteria** — what the regime requires to be measured and retained (Article 15 accuracy / robustness / cybersecurity; LL144 impact ratios; FDA clinical performance in intended-use population; OMB rights-impacting minimum practices).
4. **Reporting / notification criteria** — what the regime requires to be communicated and when (Article 73 serious-incident reporting; FDA MDR; SR 11-7 outcomes analysis to management; CFPB adverse-action notices; LL144 candidate notice; Colorado adverse-action notice).

Author criteria in that shape; pivot to the crosswalk register (chapter 6) to deduplicate shared evidence across regimes.

## Summary

- Sector and jurisdictional overlays are *additive* to horizontal (ISO/IEC 42001, NIST AI RMF, EU AI Act) criteria. A single evidence set often supports multiple overlays.
- The US financial overlay (SR 11-7, OCC 2011-12, Fed SR 23-4) adds model-risk-management, independent validation, benchmark / challenger testing, outcomes analysis.
- The FDA AI/ML SaMD overlay (GMLP, PCCP, 21 CFR Part 820 → QMSR) adds intended-use scoping, representative data, independent test sets, human-AI team performance, PCCP change control, MDR reporting.
- HIPAA, NAIC, Colorado, NYC LL144, Illinois, OMB M-24-10/M-25-21 each add their own scope / documentation / testing / reporting criteria families.
- UK, Canada, Singapore, Japan, Korea, India, Brazil, China each present a jurisdiction-specific overlay — use the live issuing-body document at reading time, do not rely on memory of versions that move quarterly.
- Every overlay decomposes into scope / documentation / testing / reporting criteria — adopt that shape to keep the crosswalk register clean.
