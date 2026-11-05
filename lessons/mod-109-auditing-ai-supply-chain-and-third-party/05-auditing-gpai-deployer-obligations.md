# Auditing GPAI Deployer Obligations (EU AI Act Articles 51–55)

## Motivation

The EU AI Act's Chapter V ("General-purpose AI models") — Articles 51 through 55 — regulates **general-purpose AI models** (GPAI) separately from high-risk AI systems. The GPAI rules recognise that modern AI deployments are overwhelmingly built on upstream foundation models trained by a small number of providers; the regulation attaches obligations to those providers, with heightened obligations for providers of models with **systemic risk**, and prescribes documentation the provider must make available to **downstream deployers**.

Most organisations the auditor engages are *downstream deployers* of GPAI models rather than GPAI *providers* themselves. The organisation integrates GPT-4 / Claude / Gemini / Llama / Mistral into products or workflows; it did not train the model. For that organisation, the GPAI articles impose two linked obligations:

- Receive and verify the provider's technical documentation and other required disclosures.
- Reflect the received information in the organisation's own high-risk-system obligations (Chapter III Section 2) where a GPAI model is a component of a high-risk system.

The auditor's job is to test whether the organisation is meeting its downstream obligations — receiving the right documentation, integrating it into risk management, flowing it down to the organisation's own deployers (where the organisation is itself a provider of a higher-level product), and interfacing with the GPAI Code of Practice that operationalises Article 56.

This is distinct from the SR 23-4 vendor-risk shape in chapter 2 — SR 23-4 is a vendor-lifecycle shape; this chapter is a specific regulatory overlay with specific article text. Both apply simultaneously; findings can be stated against either or both.

<!-- needs-research: confirm Articles 51–56 numbering, the implementing-act status, the GPAI Code of Practice's publication state and signatory list, the Annex XI and Annex XII content (the GPAI-provider documentation annexes), and the application-date for Chapter V obligations at reading time -->

## The criteria surface — Chapter V in an audit frame

Chapter V's articles divide along three axes:

- **Which models are GPAI** — Article 51(1) / Article 3 definitions. A general-purpose AI model is a model trained with a significant amount of data using self-supervision at scale, that displays significant generality, and that can competently perform a wide range of distinct tasks regardless of the way the model is placed on the market.
- **Which GPAI models have systemic risk** — Article 51 provides criteria (high-impact capabilities, demonstrated via the cumulative FLOP training threshold or by Commission designation on other grounds). The threshold in the as-published text is 10^25 FLOP cumulative compute used for training. <!-- needs-research: confirm the FLOP threshold and the Commission-designation criteria in the final Act text at reading time -->
- **What obligations attach** — Articles 53–55 impose documentation, downstream information, copyright policy, and (for systemic-risk models) additional safety / cybersecurity / incident obligations.

For the auditor's purposes, the key split is **what the provider must give the deployer** and **what the deployer must do with it**. The auditor's workpaper per GPAI dependency has one column each.

### What the provider must give

Article 53 generally requires GPAI model providers to:

- Draw up and keep up-to-date technical documentation of the model, as per Annex XI points covering (among others) training process, training-data summary, evaluation results, limitations, computational resources used. The documentation must be made available on request to the AI Office and the national competent authorities.
- Draw up, keep up-to-date, and make available to providers of AI systems who intend to integrate the GPAI model, information and documentation per Annex XII — covering model characteristics, intended tasks, acceptable use policies, licence and usage conditions, interaction / integration information, integration safety guidance, evaluation results relevant to downstream use.
- Put in place a policy to comply with Union copyright law — notably respecting the opt-out from text and data mining in Article 4(3) of Directive 2019/790 on copyright in the digital single market.
- Publish a sufficiently detailed summary of the content used for training of the GPAI model, using a template to be provided by the AI Office.

### What systemic-risk providers must additionally do (Article 55)

For models with systemic risk:

- Perform model evaluations (including adversarial testing) and document them.
- Assess and mitigate possible systemic risks at Union level, including their sources.
- Keep track of, document, and report to the AI Office and, where appropriate, to national competent authorities, information about serious incidents and corrective measures.
- Ensure an adequate level of cybersecurity protection for the model and its physical infrastructure.

<!-- needs-research: confirm the exact Article 55 obligation list and the AI Office reporting detail at reading time -->

### What the downstream deployer must do

The deployer's obligations do not sit in Chapter V alone — they come from a combination:

- **Article 26 (deployer obligations for high-risk systems)** — appoint named oversight persons, use the system in accordance with its instructions, ensure input data is appropriate, log use, inform affected natural persons, cooperate with authorities. These apply when the organisation is deploying a high-risk AI system; a GPAI model integrated into such a system flows obligations onto the deployer.
- **Article 27 (fundamental rights impact assessment)** — applicable to certain deployer categories (public bodies, deployers of credit-scoring, life-and-health insurance pricing); requires a specific FRIA.
- **The downstream information from Annex XII** — the deployer must *receive and consume* this information. A deployer who has not requested or cannot produce the Annex XII information for a GPAI model it integrates has a supply-side breach to escalate and an evidential gap of its own.
- **Interaction with Article 72 post-market monitoring** (`mod-108` chapter 1) — the deployer's post-market monitoring must take account of the provider's known limitations, known incidents, and ongoing disclosures.

Where the organisation *also* re-publishes an AI system that incorporates a GPAI model as a component — for example, a SaaS product built on top of GPT-4 that is itself placed on the market in the Union — the organisation itself takes on provider obligations with respect to its product, including Chapter III Section 2 obligations for the product if it is high-risk.

## The GPAI dependency inventory

The auditor's first fieldwork step is a **GPAI dependency inventory** — every GPAI model the organisation consumes directly or indirectly, with the provider, the model and version, the API or local-hosting form, the systemic-risk classification, the Annex XII information status, and the integration point(s).

The inventory needs, per row:

- Provider identity (OpenAI, Anthropic, Google DeepMind, Meta, Mistral, Cohere, AWS, Microsoft, Alibaba, DeepSeek, etc.).
- Model identity (GPT-4o, Claude Opus 4.X, Gemini 2.X, Llama 3.1-70B, Mistral Large, Qwen, DeepSeek-V3, etc.) and version.
- Provider's self-classification: GPAI? GPAI with systemic risk?
- EU-AI-Office classification or Commission designation if any.
- Consumption form: direct API, via cloud marketplace (Bedrock, Vertex, Azure OpenAI), open-weight download, via a downstream vendor's wrapper.
- Integration points inside the organisation's system — which features / services / high-risk systems rely on it.
- Annex XII documentation received? Date? Format?
- Training-data summary received? Date? Format?
- Copyright-policy disclosure received? Date? Format?
- Serious-incident notifications received in the period?
- Licence and acceptable-use terms?

The inventory is reperformed by the chapter 2 three-sweep pattern (AP / identity-and-access / engineering). Shadow GPAI dependencies (an open-weight Llama used by a team without appearing on the inventory) are findings against both chapter 2 and this chapter.

## The provider-documentation audit

For each sampled GPAI dependency, the auditor verifies the organisation has — and has verified the content of — the provider's required documentation.

### Annex XII information

The Annex XII information is the operational document the downstream deployer needs. The auditor tests:

- **Presence.** Has the organisation received Annex XII information? From the provider directly, or from the model-card / developer-page / API documentation the provider publishes as its Annex XII realisation?
- **Coverage.** The information covers the Annex-XII content categories the auditor expects: model characteristics (parameters, architecture, modalities), intended tasks and acceptable use, interaction and integration guidance, evaluation results relevant to downstream deployment, limitations.
- **Consistency with the production integration.** The organisation's use of the model falls inside the provider's acceptable-use policy (chapter 2 flagged training-data-use terms; this adds use-of-model terms).
- **Incorporation into the organisation's risk assessment.** The ISO/IEC 42005 impact assessment (`mod-105` chapter 5) and the Article 9 risk management (`mod-107`) for the organisation's system cite the Annex XII information and reflect its findings.

### Training-data summary

Article 53 requires GPAI providers to publish a "sufficiently detailed summary" of the content used for training. The AI Office is to provide a template. <!-- needs-research: confirm the current state of the template and the practice-level depth GPAI providers have adopted at reading time -->

The auditor's test:

- **Summary received or referenced.** The organisation has retrieved or referenced the summary.
- **Relevance to the organisation's risk assessment.** Where the summary flags training-data categories (e.g., medical corpora, legal corpora, specific languages, specific demographics), the organisation's risk assessment reflects them.
- **Copyright disclosure.** The summary — and the provider's copyright policy — is reviewed against the organisation's copyright-risk posture.

### Copyright policy

Article 53 obligates GPAI providers to have a policy to comply with Union copyright law and respect opt-outs under Article 4(3) of the DSM Directive. Downstream deployers do not directly inherit the provider's copyright obligation, but copyright claims against the outputs of a GPAI-powered product can land on the deployer. The auditor tests:

- **Policy received or referenced.** The organisation holds the provider's copyright policy or a pointer to it.
- **Deployer-side policy.** The organisation has its own policy for outputs produced by the GPAI model (attribution, output review, blocklists of known-protected content), and that policy consumes the provider's.
- **Incident history.** Any copyright complaint against the organisation's product in the period is routed through this policy.

### Evaluation and benchmark results

Where the provider publishes evaluation and benchmark results (common for frontier providers), the organisation uses those results as *inputs* to its own evaluation (`mod-106` on model-card claim verification is the companion depth). The auditor tests:

- **Evaluations received or referenced.** Stored, dated, versioned.
- **Relevance to the deployment.** The provider's benchmarks cover the modalities and tasks the deployer uses, or the deployer has run its own tests to compensate.
- **Decision-reflection.** Evaluation results that bear on decisions (acceptance of the model into production, selection of model version, operating-parameter choice) are cited in decision records.

### Serious-incident notifications

For systemic-risk GPAI, Article 55 obligates reporting of serious incidents to the AI Office. Those reports may surface publicly or via information-sharing channels; the organisation should be consuming them. The auditor tests:

- **Monitoring channel.** The organisation watches a defined set of channels for provider-side incident disclosures (vendor status pages, security advisories, published incident reports, AI-Office publications, trusted-researcher channels).
- **Triage.** Incoming disclosures are triaged against the organisation's own product exposure, consistent with `mod-108` chapter 3 (incident response).
- **Risk-register reflection.** A disclosed incident bearing on the organisation's product updates the risk register.

## Systemic-risk model use — heightened audit focus

Where any of the organisation's GPAI dependencies is a systemic-risk GPAI, the auditor's test depth increases:

- **Classification awareness.** The organisation knows the model is a systemic-risk GPAI, has evidence of the classification (Commission designation, provider self-classification, or clear fit against Article 51 criteria), and reflects this in its risk-tiering (chapter 2).
- **Enhanced provider-documentation verification.** The organisation receives the Article 55 artefacts the provider is required to produce (model evaluations including adversarial testing, systemic-risk assessment, incident information, cybersecurity posture).
- **Deployer-side systemic-risk contemplation.** Where the organisation integrates a systemic-risk GPAI into a high-risk system, the organisation's own Article 9 risk management contemplates the GPAI's systemic risks — not only the system-specific risks.
- **GPAI Code of Practice alignment.** Where the provider is a Code of Practice signatory, the organisation can rely on the Code's structured disclosures; where the provider is not, the organisation must document how it compensates.

## The GPAI Code of Practice

Article 56 (per the Act's structure) provides for codes of practice developed under AI-Office facilitation to operationalise Chapter V obligations. The GPAI Code of Practice is the resulting instrument and is intended to be a means of demonstrating compliance with Article 53 and, for systemic-risk model providers, Article 55. <!-- needs-research: confirm the GPAI Code of Practice's publication status, signatory list, and the current version number at reading time; confirm the exact Article (likely Article 56) framing the Code -->

The auditor tests whether the organisation leverages the Code as a reliance anchor:

- **Signatory status of each GPAI provider.** The organisation knows whether each provider in its GPAI dependency inventory is a Code signatory.
- **Reliance on Code disclosures.** Where a provider is a signatory, the organisation uses the Code's structured disclosures (safety and security framework, systemic-risk assessment and mitigation report, training-data transparency, incident reporting) as reliance evidence.
- **Compensation where providers decline.** Where a provider is not a signatory (open-weight distribution, non-EU-facing providers, providers that have specifically declined), the organisation documents the reliance compensation — direct provider engagement, bespoke due-diligence, or acceptance that reliance on this provider carries more residual risk.

The Code is dynamic; the auditor reads the applicable version at the engagement period and notes material revisions published inside the period.

## Flow-down to the organisation's own deployers

Where the organisation is both a downstream deployer of a GPAI model *and* itself a provider of an AI system to third parties (a SaaS product, an embedded component for other developers, a system placed on the EU market), the organisation must flow the Annex XII information and related artefacts to its own deployers. The auditor tests:

- **Flow-down documentation.** The organisation publishes to its deployers the Annex XII-derived material relevant to the deployer's use of the product.
- **Contract terms with deployers.** The deployer contract reflects the GPAI provider's acceptable-use terms; use-restrictions flow down.
- **Incident flow-down.** Provider-side incident disclosures that bear on the deployer's exposure are forwarded to the deployer.
- **Updates.** Where the provider updates its Annex XII information or the Code evolves, the organisation re-flows the material.

Flow-down failures are a specific finding type — an organisation that consumes the GPAI-provider information privately and does not forward it breaks the regulation's transparency chain.

## Interaction with other chapters

- **Chapter 1 (provenance).** The GPAI-provider information is the upstream provenance for the organisation's integrations — the model card and the technical documentation are the artefacts chapter 1's trace-back references.
- **Chapter 2 (SR 23-4).** The GPAI dependency inventory is a specialisation of the chapter-2 vendor inventory; GPAI-provider due diligence is a specialisation of SR 23-4 phase-2 diligence.
- **Chapter 3 (assurance).** SOC 2 / ISO / 42001 reliance on a GPAI provider does not substitute for Chapter V documentation; both must hold.
- **Chapter 4 (malicious artefacts).** Open-weight GPAI (Llama, Mistral, Qwen, DeepSeek, etc.) crosses the chapter-4 scanning and signing gates.
- **Chapter 6 (registry gate).** GPAI artefacts the organisation hosts internally pass through the registry-ingestion gate like any other model.
- **`mod-108` chapter 1 (monitoring).** Article 72 post-market monitoring consumes provider-side incident disclosures and known-limitation disclosures.
- **`mod-106` (model-card / system-card).** The provider's own card / system-card is the artefact whose claims chapter 106.2 tests; this chapter is about the regulated flow of that artefact from provider to deployer.
- **`mod-107` (risk management).** The organisation's Article 9 risk management for a high-risk system that integrates a GPAI model draws on Annex XII and Code-of-Practice disclosures.

## Deployer-side evidence the auditor expects

A mature downstream-deployer evidence folder, per GPAI dependency, includes:

- A pointer to the provider's Annex XII information (or equivalent), with retrieval date and SHA hash of the retrieved document.
- A pointer to the provider's training-data summary.
- A pointer to the provider's copyright-policy disclosure.
- A pointer to the provider's model-evaluation and safety-evaluation artefacts.
- Where applicable, a pointer to the provider's systemic-risk assessment and cybersecurity-posture artefacts (Article 55).
- A dated memo integrating the provider's information into the organisation's own risk management for each integration point.
- A monitoring configuration consuming the provider's advisory and incident channels.
- Where the organisation flows down to its own deployers, the deployer-facing analogue of the same artefacts.

## Common failure modes

- **Annex XII information not requested.** The organisation uses the GPAI model via API and never asks the provider for structured deployer information, relying instead on the general model-card.
- **Classification unknown.** The organisation does not know whether a given GPAI dependency is a systemic-risk GPAI.
- **Training-data summary not consumed.** The provider publishes the summary; the organisation has never read it; the organisation's risk assessment does not reflect it.
- **Copyright policy not consumed.** Provider's copyright posture is not integrated into the organisation's output-review controls.
- **Serious-incident channel not watched.** The organisation does not have a channel-watching configuration; an incident at the provider does not trigger review internally.
- **Open-weight GPAI treated as not-a-GPAI.** The organisation hosts a Llama variant internally and treats it as "our model," escaping the Chapter V awareness.
- **Flow-down to deployers absent.** The organisation receives provider information privately and does not forward relevant pieces to its own deployer customers.
- **Code-of-Practice reliance unclaimed.** Signatory providers publish structured disclosures the organisation does not reference or leverage.
- **Systemic-risk use with ordinary diligence.** The organisation integrates a systemic-risk GPAI without heightening diligence or risk-register scoring.

## Summary

- EU AI Act Chapter V (Articles 51–55) regulates general-purpose AI models separately from high-risk AI systems; downstream deployers have specific obligations to receive and consume provider-produced documentation and to reflect it in their own risk management.
- The auditor's GPAI dependency inventory lists every direct and indirect GPAI dependency, classifies systemic-risk status, and tracks Annex XII / training-data-summary / copyright-policy / evaluation / incident disclosure status per provider.
- Per-dependency fieldwork tests presence of the required documentation, consistency with the production integration, and incorporation into the organisation's ISO/IEC 42005 impact assessment and Article 9 risk management.
- Systemic-risk GPAI use triggers heightened audit depth, with specific attention to Article 55 artefacts (evaluations, systemic-risk assessment, incident reports, cybersecurity posture).
- The GPAI Code of Practice is the operational anchor under Article 56; the auditor tests the organisation's signatory awareness, reliance on Code disclosures, and compensation strategy for non-signatory providers.
- Flow-down obligations apply where the organisation itself is a provider of an AI system that integrates a GPAI model; the auditor tests deployer-facing analogue artefacts.
- Chapter 2 (SR 23-4), chapter 3 (assurance), chapter 1 (provenance), `mod-108` (monitoring and incidents), and `mod-107` (risk management) all interface with this chapter; findings should be stated against the specific article (53, 55, 56) in addition to any cross-chapter finding.
