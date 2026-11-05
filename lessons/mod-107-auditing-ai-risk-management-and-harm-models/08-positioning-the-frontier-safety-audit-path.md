# Positioning the Frontier-Safety Audit Path

## Motivation

Most audit engagements described in this module target organisations deploying AI *products*. A small but consequential set of engagements target organisations that develop *frontier general-purpose models* — the Anthropics, OpenAIs, Google DeepMinds, Meta AIs, Mistrals, xAIs, and the frontier-adjacent labs — or their downstream GPAI-with-systemic-risk designations under the EU AI Act. For these engagements the auditor confronts a different literature: Responsible Scaling Policies (RSPs), Preparedness Frameworks, Frontier Safety Frameworks, Frontier Model Forum commitments, the EU AI Office's GPAI Code of Practice, and the published pre-deployment capability evaluations such as METR's.

The auditor does *not* re-author the frontier red-team methodology or the capability-elicitation science. That depth sits with `agentic-safety-engineer` (L40) and the frontier labs themselves. The auditor's job is to read the lab's *published policy* as criteria and test whether the lab operates to the policy; to read the lab's pre-deployment safety case as a claim document; and to position the engagement so the auditor's independence envelope is clear.

This chapter is deliberately shorter than chapters 1–7: it positions the path and the published criteria without pretending the auditor can audit frontier capability-elicitation at the depth the labs themselves produce.

## When frontier-safety audit applies

The frontier-safety audit path applies when the engagement subject matter is one of:

- **A frontier AI developer's responsible-scaling / preparedness programme.** The subject is the lab's own risk-management programme for its general-purpose models at or near the frontier.
- **A GPAI provider meeting the EU AI Act Article 51 systemic-risk threshold** (10^25 FLOPs training-compute threshold at the time of writing, revisable by the Commission). <!-- needs-research: confirm the systemic-risk threshold currently in force; Article 51 and Annex XIII have been subject to Commission delegated act revisions -->
- **A downstream deployer of a GPAI-with-systemic-risk model** who must satisfy itself that the upstream lab's commitments are reliable (a `mod-109` third-party programme application with frontier-specific criteria).
- **A regulator-side assurance body** (EU AI Office, national AI safety institutes, industry-association certifications) reading frontier commitments as criteria.

Where the engagement subject does not include a frontier-near model or a GPAI-with-systemic-risk designation, the auditor uses the earlier chapters' programme audit. The frontier-safety audit path is additive, not a replacement.

## Published criteria the auditor reads

The frontier-safety audit treats published policy commitments as the criteria set against which the lab is tested. The canonical corpus at the time of writing:

### Anthropic — Responsible Scaling Policy

Anthropic's **Responsible Scaling Policy (RSP)** defines AI Safety Levels (ASL-1 through ASL-5 as proposed; ASL-3 and ASL-4 operationally defined at various points) and the capability thresholds and corresponding deployment / security standards each level requires. The RSP is a public, versioned document with declared evaluation methodology for crossing thresholds. <!-- needs-research: cite the current RSP version and the current ASL definitions; the RSP has been revised multiple times since the 2023 initial release -->

Auditor read: the RSP is a *written commitment* the lab has made publicly. The audit tests whether the lab operates to the RSP — thresholds are evaluated on the declared cadence, crossing a threshold triggers the declared controls, declared evaluations have been run and signed.

### OpenAI — Preparedness Framework

OpenAI's **Preparedness Framework** defines capability "tracked categories" (CBRN, cybersecurity, persuasion, model autonomy, and their ongoing additions) and risk levels (low / medium / high / critical) with corresponding deployment constraints and the Preparedness team's role. <!-- needs-research: cite the current Preparedness Framework version and tracked categories; updated multiple times since 2023 --> Auditor read: parallel to the RSP read — are the categories evaluated, are the levels assessed, do the constraints follow.

### Google DeepMind — Frontier Safety Framework

Google DeepMind's **Frontier Safety Framework** defines critical capability levels, evaluation cadence, and mitigation commitments across autonomy, misuse, deception, and other axes. <!-- needs-research: cite the current Frontier Safety Framework version -->

### Meta, Mistral, xAI, and frontier-adjacent labs

Each has (or has indicated intention to) publish a frontier-safety commitment; the auditor should expect a public artefact and test against it. Where no artefact exists, the finding is against the Frontier Model Forum commitment (if applicable) or against the EU AI Office Code of Practice obligation (for EU-market GPAI-with-systemic-risk providers). <!-- needs-research: at reading time inventory which frontier labs have published an RSP-equivalent and the state of each -->

### Frontier Model Forum

The **Frontier Model Forum** is an industry body (founding members Anthropic, OpenAI, Google, Microsoft) producing shared safety research, commitments, and best-practice publications. Member commitments and FMF-published best practices function as cross-lab criteria the auditor may read. <!-- needs-research: cite current FMF membership, published commitments, and any voluntary / mandatory status -->

### EU AI Office — GPAI Code of Practice

The **EU AI Office** is operationalising GPAI obligations under the AI Act via a **Code of Practice** developed under Article 56. The Code sets out specific commitments on model evaluation, systemic-risk assessment, red-team cadence, transparency, copyright, and incident reporting for GPAI providers, with higher-bar commitments for GPAI-with-systemic-risk providers. <!-- needs-research: the Code of Practice is under drafting / adoption; confirm the current state at reading time, which chapters are in force, and signatory lists --> Auditor read: the Code is the published criteria set for EU-market GPAI compliance; signatories (and non-signatories subject to Article 55's obligations by other means) are tested against it.

### Other reference commitments

- **White House Voluntary Commitments (July 2023, with expansions).** Seven initial labs; AI-safety commitments on red-teaming, cybersecurity, provenance, watermarking, public reporting. <!-- needs-research: confirm current signatory list and any 2025–2026 revisions -->
- **Bletchley / Seoul / Paris AI-Summit commitments.** International declarations with signatory sets; specific labs have published declaration-aligned commitments. <!-- needs-research: cite the current summit cycle and its outputs -->
- **UK AI Security Institute (AISI) and US AISI.** Government-side evaluation bodies whose published evaluations function as criteria the lab is tested against. <!-- needs-research: confirm the current names and remits of UK AISI (formerly AI Safety Institute) and US AISI -->

## What the auditor tests at the frontier-safety level

For each subject lab the auditor's test shape:

### 1. Policy identification and version-pinning

- The current public version of the RSP / Preparedness Framework / Frontier Safety Framework is retrieved.
- The policy version applicable to the model under audit is identified (policies are versioned; the lab may have released a model under policy vN and later revised to vN+1).
- The crosswalk between policy sections and the lab's internal documents is mapped.

### 2. Threshold / level assessment

- The policy's capability thresholds / levels are enumerated.
- For each, the lab's declared evaluation methodology is read and version-pinned.
- The current model's threshold / level assessment result is retrieved (the "safety case" for the release).
- The auditor is positioned as reader, not re-evaluator — the auditor does not repeat the frontier capability elicitation.

### 3. Pre-deployment evaluation evidence

- The published pre-deployment safety case (system card, preparedness report, safety evaluation report) is read.
- The declared evaluations (internal, external — METR, UK AISI, Apollo Research, ARC Evals-descended work, academic collaborators) are inventoried.
- External evaluators' access terms, independence posture, and report publication state are recorded.
- The chapter-3 / chapter-4 / chapter-7 patterns apply to the evaluations that are within the auditor's reperformance envelope; deeper capability-elicitation evaluations are read as claim documents.

### 4. Commitment-vs-execution

- Each policy commitment (threshold-triggered controls, red-team cadence, incident reporting, information sharing) is checked against execution evidence.
- Non-execution of a published commitment is a severe finding — the lab has made a public commitment and failed to operate to it.

### 5. GPAI-with-systemic-risk-specific tests

Where EU AI Act Article 51 applies:

- **Model evaluation evidence.** Per Article 55 / 55a and the Code of Practice, the provider has run the required model evaluations including adversarial testing.
- **Systemic-risk assessment.** Documented, including mitigation.
- **Serious-incident reporting.** Channels exist and have been exercised.
- **Cybersecurity.** The model's protection against unauthorised access and release.
- **Information to downstream providers.** The documentation obligations under Article 53.
- **Transparency and copyright.** Article 53's training-data summary and copyright-compliance disclosures.

<!-- needs-research: cite the final-text Article numbering and the Code of Practice chapter equivalents at reading time -->

## The "defer up" boundary

The frontier-safety audit path has an explicit boundary: *frontier red-team methodology depth is not the auditor's work*. This is the boundary the AI-Auditor track as a whole respects:

- **AI-Auditor (L45) tests programme sufficiency and reliability.** The auditor can read the RSP, confirm the lab operates to it, read the pre-deployment safety case, and sample the evidence.
- **Agentic-Safety-Engineer (L40) authors the frontier red-team methodology.** The ASE track covers dangerous-capability elicitation, autonomy evals, deception probes, situational-awareness tests.
- **The lab's own frontier safety researchers** author the capability evaluations the auditor reads as claim documents.

When the auditor encounters an evaluation whose methodology the auditor cannot evaluate, the audit response per ISA 620 (`mod-104`) is to engage a specialist — in practice an agentic-safety-engineering specialist retained for the engagement — rather than to attempt reperformance beyond the auditor's expertise. The auditor records the specialist's identity, scope, and findings in the audit workpaper.

## Downstream deployer position

For a downstream deployer who is *not* a frontier lab but is deploying a frontier model under EU AI Act high-risk obligations, the auditor's position is different:

- **The upstream lab is a third party** (`mod-109`). The deployer's audit tests whether the upstream's attestations meet the deployer's assurance need.
- **The lab's published commitments are criteria** the deployer can point to.
- **The deployer's residual-risk analysis** must incorporate the possibility the upstream's commitments fail or change; chapter 2's register must carry a row for upstream-commitment breach.
- **Downstream guardrails** (chapter 7) layer on top of the upstream's; the deployer cannot rely on upstream guardrails alone.

The deployer's auditor does not test the lab directly; the deployer's auditor tests whether the deployer's own programme accounts for the dependency.

## Common failure modes at the frontier level

- **Commitment without version-pin.** The lab cites "our RSP" without saying which version; different versions have different thresholds.
- **Threshold evaluation is one-shot.** The lab's assessment at model release is not refreshed; capability drift post-release is unmonitored.
- **External evaluator access is thin.** The lab engaged an external evaluator but the evaluator's access was limited (no fine-tune access, no system-prompt access, limited budget), and the external report caveats its limitations; the lab's public communication omits the caveats.
- **GPAI-with-systemic-risk designation ignored.** The lab is above the FLOPs threshold but has not notified the Commission per Article 52.
- **Code of Practice signatory without execution.** The lab signed the Code but the specific-chapter commitments are not operationalised.
- **Incident reporting channel exists but has never been exercised.** No evidence the channel works.
- **Serious-incident definition narrower than the Code requires.** The lab defines "serious incident" more narrowly than the Code to reduce reporting load.
- **The published safety case cites evaluations that are not actually in the report.** A claim-vs-evidence gap at the top of the frontier-lab pyramid.

## Common failure modes on the deployer side

- **Deployer treats the upstream model card as sufficient.** Chapter 7's deployment-system guardrails are missing because the deployer trusts the upstream's.
- **Deployer has no upstream-commitment-change watchlist.** When the upstream revises its RSP or Preparedness Framework the deployer does not notice.
- **Deployer's register has no row for upstream failure.** The upstream dependency is implicit in every row but explicit in none.
- **Deployer's audit scope excludes the upstream-provided model.** The auditor is asked to audit the deployer's wrapper and told the model is "out of scope"; this is a scoping finding against `mod-103`.

## Summary

- The frontier-safety audit path applies to frontier labs and GPAI-with-systemic-risk providers (EU AI Act Article 51), and to downstream deployers of such models.
- Published policies — Responsible Scaling Policy, Preparedness Framework, Frontier Safety Framework, Frontier Model Forum commitments, EU AI Office GPAI Code of Practice — are the criteria set.
- The auditor's tests are policy identification, threshold / level assessment, pre-deployment evaluation evidence, commitment-vs-execution, and the GPAI-with-systemic-risk Article 55 / 55a obligations.
- The auditor does *not* re-author the frontier red-team methodology; capability-elicitation depth sits with `agentic-safety-engineer` (L40) and the labs' own safety-research teams. Specialist engagement follows ISA 620.
- Downstream deployers are audited against their third-party programme (`mod-109`) with frontier-specific criteria; the deployer's register must carry an upstream-commitment-change row.
- Non-execution of a published commitment is among the most severe findings an auditor produces — public commitments are commitments.
