# Auditing the Privacy-Risk Program

## Motivation

Privacy risk in AI systems is distinct from general information-security privacy risk — a trained model can leak training data (membership inference, training-data extraction), can memorise and emit sensitive content, can be used to re-identify pseudonymous records, and can infer attributes that were never explicitly given. Mitigations are also distinct: differentially private training (DP-SGD), input / output PII scrubbing, k-anonymity / l-diversity on training corpora, unlearning on request. Regulators (GDPR, state privacy acts, HIPAA under HHS OCR, FTC Act Section 5) treat these risks with their own enforcement surface.

The auditor's job in this chapter is to test the organisation's privacy-risk *programme* — the attack-coverage against membership-inference / LiRA / data-extraction, the sufficiency of DP-SGD accounting for the sensitive-data category, the PII pipeline's coverage of the deployment's data categories, and the alignment with GDPR Article 22 and the NIST Privacy Framework.

Attack-methodology authoring sits with `ai-risk-engineer` (L25) and the privacy-research literature; DP-accounting authoring sits with `model-evaluation-engineer` (L30). The auditor applies the canonical toolchain (Opacus, TensorFlow Privacy, ML Privacy Meter, Presidio) and reads the programme against published criteria.

## The privacy-attack coverage test

The auditor's first attack-coverage test is against the canonical privacy-attack taxonomy. The categories:

- **Membership inference (MIA).** Given a candidate record, decide whether it was in the training set. The classical MIA (Shokri et al. 2017) uses the model's loss on the record; the state-of-the-art LiRA (Likelihood Ratio Attack; Carlini, Chien, Nasr, Song, Terzis, Tramèr 2022) trains shadow models and computes a per-record likelihood ratio. LiRA reports TPR at low FPR (e.g., TPR at FPR=0.1%) as the headline metric because the aggregate AUC obscures the risk that *some* records are highly exposed.
- **Attribute inference.** Given partial information about a record, predict an undisclosed attribute. Overlap with inference risk in representation learning.
- **Training-data extraction.** Given query access, extract verbatim or near-verbatim training records. Carlini, Tramèr, Wallace et al. 2021 and follow-on work demonstrated extraction against GPT-2 and later LLMs.
- **Model inversion.** Reconstruct representative inputs from model parameters (classical: Fredrikson et al. 2015 for simple models).
- **Reconstruction attacks.** Under DP, the known theoretical attack bounds define the achievable reconstruction accuracy; the auditor should know the bound exists even if the attack is not run.
- **Unintended memorisation (the "canary" shape).** Insert canary records into training and test whether they can be elicited from the trained model.

The auditor's coverage grid:

| Attack class | In-scope? | Tool / method | Dataset / canary | Metric | Last run |
|---------------|-----------|---------------|------------------|--------|-----------|
| MIA / loss-based | yes | ML Privacy Meter / custom | Holdout 1k | AUC + TPR @ FPR=0.1% | 2026-08 |
| LiRA (shadow-model) | yes | ML Privacy Meter | Shadow 20× | TPR @ FPR=0.1% | 2026-08 |
| Training-data extraction | yes (for LLMs) | Research literature method; custom harness | Canary-injected corpus | Extraction success rate | 2026-09 |
| Attribute inference | partial | Custom | Holdout | AUC | 2026-05 |
| Model inversion | n/a | — | — | — | — |

For each row the auditor records tool, dataset / canary, metric, and last-run date. Missing rows for exposed attack classes are findings; silent omissions (no row at all for a class the deployment exposes) are the strongest finding shape.

### The MIA / LiRA TPR-at-fixed-FPR evidence

Mod-106 chapter 6 established that MIA audit shape reports TPR at a fixed low FPR, not aggregate AUC, because aggregate AUC near 0.5 can hide the presence of highly exposed records. The programme audit tests:

- **The reported metric is TPR at a stated FPR.** FPR = 0.1% or FPR = 1% are the common choices; the organisation's methodology declares which.
- **The shadow-model count is adequate.** LiRA requires enough shadow models to estimate the per-record likelihood ratio; low shadow-model counts bias the result downward.
- **The attack set is representative of the population at risk.** If the sensitive population is a small subset of the training data, testing MIA on a uniform sample understates the exposed-record risk.
- **The result is interpretable.** TPR = 0.05 at FPR = 0.1% means that for every 1000 non-members, 1 is misclassified as a member, while for every 100 members, 5 are detected. The auditor records the interpretation alongside the number.

## The DP-SGD sufficiency test

Differential privacy is the strongest mitigation for training-data exposure. The auditor tests:

### DP-accountant replication

The organisation declares (ε, δ) at the end of training. The accountant is a numerical / analytic process over training-step noise multiplier, batch size, dataset size, epochs, and composition method (Rényi-DP; numerical composition per Gopi, Lee, Wutschitz 2021).

The auditor:

1. **Obtains the accountant inputs.** Noise multiplier σ, sampling rate q, iterations T, δ, and the accountant family (RDP, Gaussian DP, PRV accountant).
2. **Replicates the accountant.** Opacus (`opacus.PrivacyEngine`), TensorFlow Privacy (`tensorflow_privacy.privacy.analysis.rdp_accountant`), or a published PRV accountant reimplementation.
3. **Compares the ε.** The organisation's declared ε should match the auditor's reproduced ε within rounding.
4. **Records the privacy unit.** Record-level DP vs. user-level DP vs. group-level DP. The organisation's claim must specify the unit; "DP training" without a unit is a Grade-E assertion.

### Sufficiency test

A reproduced ε is not automatically sufficient. The auditor tests whether the ε is appropriate for the sensitive-data category:

- **Record-level ε in the single digits** is the practitioner's range for most ML; ε under 1 is very strong; ε above 10 provides limited theoretical guarantee though empirical privacy may still be acceptable.
- **The sensitive-data category.** The more sensitive the category (healthcare under HIPAA, financial under GLBA, children's data under COPPA, protected characteristics under GDPR Article 9), the tighter the expected ε. A published ε of 8 for a clinical model is a sufficiency finding.
- **The δ budget.** δ should be substantially less than 1/|dataset|. A δ of 10⁻⁵ against a dataset of 10⁷ records is standard; a δ of 10⁻³ is too loose.
- **Clipping and gradient-norm bounds.** DP-SGD requires per-sample gradient clipping at a declared norm bound; the auditor records the bound and asks whether it was validated to not degrade utility beyond the acceptable range.
- **The utility cost.** DP-SGD degrades utility; the auditor tests whether the organisation accepted a utility floor compatible with the obligation.

A programme with DP-SGD and a sufficient (ε, δ) accounting for the sensitive-data category is strong evidence; a programme with DP-SGD but a weak ε accounting is a partial mitigation and the auditor reports it as such.

<!-- needs-research: cite the current Opacus and TensorFlow Privacy accountant documentation and any 2025–2026 numerical-composition advances; the PRV accountant is state of the art as of this authoring -->

## The PII-pipeline coverage test

Separate from training-time privacy, deployed systems need runtime PII handling. The auditor tests:

### Microsoft Presidio and the PII-detection layer

Presidio (`github.com/microsoft/presidio`) is the canonical open-source PII detection and anonymisation toolkit, with recognisers for email, phone, credit card, IBAN, US / EU / UK national identifiers, dates, person names, locations, and custom recognisers. The auditor expects:

- **Presidio (or an equivalent commercial tool) in the production pipeline** for inputs that may contain PII and for outputs that may inadvertently emit PII.
- **Recogniser coverage matched to the deployment's data categories.** A deployment that handles EU personal data needs EU-specific recognisers; a deployment handling US healthcare needs the HIPAA 18-identifier set.
- **False-positive / false-negative calibration.** A Presidio deployment should have declared FPR / FNR per entity type on a representative sample; the auditor samples and tests.
- **Custom recogniser review.** Custom recognisers (regex patterns for domain-specific identifiers — member IDs, policy numbers) are reviewed, versioned, and tested.
- **Downstream handling.** What the pipeline does with detected PII: block, redact, anonymise, consent-check. Policy must be declared per PII category.

### Training-corpus PII handling

Before training, training corpora should be screened for PII. The auditor tests the pre-training pipeline:

- **Screen declared and operational.** The screen exists and ran on the current training corpus.
- **Residual PII sampled.** The auditor samples the training corpus and confirms low PII presence; residual presence beyond the declared tolerance is a finding.
- **Sensitive-identifier handling.** SSN, DOB, named-person-specific identifiers are either removed or hashed per the methodology.
- **Re-identifiability risk.** Even after de-identification, combinations of quasi-identifiers can re-identify; the programme should have a k-anonymity or l-diversity analysis for structured training data.

## The GDPR alignment test

GDPR is the strongest privacy regulation most AI programmes encounter. The auditor's tests:

- **Lawful basis.** Processing of personal data for training or inference has a declared Article 6 basis (consent, contract, legitimate interest, …) and, for special-category data, an Article 9 basis. The declaration is documented in the AI inventory (`mod-105`).
- **DPIA (Article 35).** A Data Protection Impact Assessment has been completed for high-risk processing; the DPIA covers the AI-specific risks (profiling, automated decision-making, large-scale sensitive data).
- **Article 22 — automated individual decision-making.** Decisions solely automated with legal or similarly significant effect are subject to the Article 22 regime; the organisation's position (opt-out, consent-based, contract-based, carve-out, or non-solely-automated with HITL) must be documented and the "meaningful information about the logic" must be providable to the subject. (Chapter 5 overlap.)
- **Data-subject rights.** Access (Article 15), rectification (16), erasure / right-to-be-forgotten (17), portability (20), objection (21). The programme must describe how an erasure request affects the trained model — retraining, fine-tune unlearning, or documented inability with the required justification.
- **Transfers.** Personal data transfers outside the EU are governed by Chapter V; the AI inventory must track where training and inference happen.
- **DPO interface.** The organisation's Data Protection Officer is interfaced with the AI programme at the declared cadence.

A programme that "complies with GDPR" categorically without the per-article evidence is a Grade-E documentation claim.

## The NIST Privacy Framework alignment test

NIST's Privacy Framework (version 1.0, 2020) structures privacy risk management around Identify-P / Govern-P / Control-P / Communicate-P / Protect-P. The auditor's alignment tests:

- **Identify-P.** Inventory of data processing in the AI system; data-mapping evidence.
- **Govern-P.** Privacy roles and responsibilities; policies and risk management; DPIA process.
- **Control-P.** Individual participation (consent, access); data processing (minimisation, de-identification, transfer); data-security protections.
- **Communicate-P.** Transparency notices to individuals; disclosure to regulators.
- **Protect-P.** Technical safeguards including DP, access control, encryption.

A programme that cites the Privacy Framework should produce the Function-by-Category evidence; the AI-specific extensions (profile the organisation has authored, or absence thereof) are their own audit target.

<!-- needs-research: confirm NIST Privacy Framework version in force at reading time; v1.0 published January 2020 and a v1.1 draft has been in consultation -->

## Unlearning and the right-to-erasure test

The GDPR right to erasure interacts with trained models in a complex way: deleting a record from the training database does not unlearn its effect on the model. The auditor tests:

- **The organisation's unlearning policy.** Options: retrain from scratch on request (expensive; rarely practical for foundation models); periodic retraining with cleaned corpora (common for small / bespoke models); approximate unlearning via fine-tune (SISA, Bourtoule et al. 2021; influence-function-based unlearning). Each has different privacy guarantees.
- **The declared SLA.** Erasure processed within the declared window (one month per GDPR Article 12.3, extendable).
- **The evidence.** Erasure requests have a traceable workflow; the organisation produces a response record per request.
- **Approximate-unlearning validation.** Where the organisation uses approximate unlearning, the residual-memorisation of the erased records is measured and reported.

## Sector-specific privacy regimes

Depending on scope the auditor may also test:

- **HIPAA (US healthcare).** De-identification per Safe Harbor (18 identifiers) or Expert Determination; Business Associate Agreements; breach notification.
- **COPPA (US children's data).** Verifiable parental consent; data minimisation; no profiling without consent.
- **US state privacy acts.** California (CCPA / CPRA), Virginia, Colorado, Utah, Connecticut, and the growing state corpus. Each has its own sensitive-data definitions and consumer-rights obligations. <!-- needs-research: at reading time inventory the current state privacy acts in force and effective dates -->
- **CPPA / Canada PIPEDA, LGPD (Brazil), PIPA (South Korea), PIPL (China).** Jurisdiction-specific obligations where the deployment extends there.

The auditor does not practice privacy law; the auditor reads the engagement's legal-counsel letter (`mod-103`) and tests the obligations enumerated there.

## Common failure modes

- **MIA reported as aggregate AUC near 0.5, no TPR-at-fixed-FPR.** The exposed-record risk is invisible.
- **"DP-SGD trained" without ε, δ, or privacy unit.** Grade-E assertion.
- **DP-SGD at ε > 10 for clinical or genetic data.** Sufficiency finding.
- **Presidio deployed with default recognisers for a jurisdiction that needs custom ones.** PII coverage finding.
- **Training corpus never screened for PII.** Common for scraped corpora; the finding is structural.
- **Article 22 position not documented.** The organisation cannot articulate whether it is relying on consent, carve-out, or non-solely-automated status.
- **Erasure not operationalised.** The organisation accepts erasure requests but has no process to validate effect on the trained model.
- **"Model inversion is not a risk for our model."** Without a tested bound, this is a Grade-E assertion.

## Summary

- The privacy-attack coverage grid covers MIA / LiRA, attribute inference, training-data extraction, model inversion, and canary-based memorisation; silent omissions for exposed classes are findings.
- MIA audit reports TPR at a fixed low FPR, not aggregate AUC; LiRA shadow-model count and target-population representativeness matter.
- DP-SGD is tested by replicating the accountant (Opacus / TF Privacy / PRV accountant) and judging (ε, δ) sufficiency against the sensitive-data category.
- The runtime PII pipeline (Presidio or equivalent) is tested for recogniser coverage, FPR / FNR calibration, custom-recogniser review, and downstream handling.
- GDPR alignment is tested per article (6, 9, 22, 35, 15–21, Chapter V) with per-article evidence; the right-to-erasure interaction with trained models has its own unlearning test.
- The NIST Privacy Framework provides a Function-by-Category structuring the auditor uses when the organisation cites the Framework as criteria.
- Sector-specific regimes (HIPAA, COPPA, US state acts, GDPR-equivalents) layer on top; the engagement's legal-counsel letter enumerates applicability.
