# Reading the Model / System / Dataset Card as an Independent Assurance Practitioner

## Motivation

A published card is a *claim document*. The developer declares what the model is, what it should and should not be used for, how it performs, how it was evaluated, and what its known limitations are. For the auditor the card is simultaneously an engagement artifact and a population of testable assertions — every sentence that could be rewritten as "the subject matter conforms to [criterion] because [evidence]" is a candidate finding.

The auditor's first fieldwork hour against any AI system under audit is spent extracting those assertions, grading each one for auditability, and assigning each to a replication procedure. Done rigorously, the resulting *claim register* is the spine of the rest of the engagement: every chapter that follows (replication, calibration, fairness, robustness, report authoring) returns to that register. Done loosely, the auditor's replication work drifts off-claim and the independent-reviewer handoff falls apart.

This chapter installs the card-reading discipline. It covers the three source formats the auditor will encounter in the wild, the taxonomy of auditable claims, the claim-extraction procedure, and the auditability-grading rubric.

## The three canonical card formats

Model and dataset documentation is a decade of overlapping proposals. Three sources carry the normative weight an auditor should treat as criteria:

### Mitchell et al. — Model Cards for Model Reporting (2019)

The Model Card proposal in Mitchell, Wu, Zaldivar, Barnes, Vasserman, Hutchinson, Spitzer, Raji and Gebru (FAccT 2019; arXiv 1810.03993) defines nine sections:

1. **Model details** — basic information about the model: developer, date, version, type, training algorithms, parameters, fairness constraints, license, feedback contact.
2. **Intended use** — primary intended uses, primary intended users, out-of-scope use cases.
3. **Factors** — relevant factors (groups, instrumentation, environment) and evaluation factors.
4. **Metrics** — model performance measures, decision thresholds, variation approaches.
5. **Evaluation data** — datasets, motivation, preprocessing.
6. **Training data** — the same questions for training data.
7. **Quantitative analyses** — unitary results, intersectional results.
8. **Ethical considerations.**
9. **Caveats and recommendations.**

Any card claiming to be a "model card" in the Mitchell sense is implicitly asserting that those nine sections are present and complete. The auditor tests the shape as a first-pass completeness check before testing individual claims.

### Gebru et al. — Datasheets for Datasets (2021)

The Datasheets proposal in Gebru, Morgenstern, Vecchione, Vaughan, Wallach, Daumé III and Crawford (Communications of the ACM, 2021; arXiv 1803.09010) organises dataset disclosure around seven question areas:

1. **Motivation** — why the dataset was created, who funded it.
2. **Composition** — what the instances are, how many, labels, missing data.
3. **Collection process** — how instances were acquired, who collected them, consent, ethical review.
4. **Preprocessing / cleaning / labeling** — what was done to the raw data.
5. **Uses** — tasks the dataset has been used for; tasks it could be used for; tasks it should *not* be used for.
6. **Distribution** — how the dataset is distributed, license, restrictions, export controls.
7. **Maintenance** — who maintains, how errata are communicated, update plans, support for extension.

A dataset card claiming datasheet conformance is a claim against this shape; a card *not* following datasheets is itself a finding the auditor records against clause-5 "training data" and clause-6 "evaluation data" of the Mitchell model card.

### The Hugging Face model-card format

Hugging Face publishes a repository-specific model-card spec: a YAML metadata block at the top of the `README.md`, followed by a markdown body with required and recommended sections. <!-- needs-research: cite the current Hugging Face model-card metadata spec URL at huggingface.co/docs/hub/model-cards and confirm the exact required field list at reading time; the spec evolves --> The metadata block's language, license, tags, datasets, and `model-index` evaluation-result fields are machine-readable; the body sections (Model Details, Uses, Bias/Risks/Limitations, Training Details, Evaluation, Environmental Impact, Technical Specifications, Citation) mirror the Mitchell shape with Hub-specific additions.

For auditors this matters in two ways: (a) the HF `model-index` block is a structured declaration of performance claims and should be audited against the card's prose for consistency; (b) HF Hub carding behaviour varies widely — many cards present as HF-style but omit the metadata block, and the completeness check must distinguish "YAML missing" from "YAML present but incomplete."

### Google / PAI / sector variants

Other card families exist and may appear as the subject of audit:

- **Google Model Cards** — a developer tool and template family hosted at the Model Card Toolkit project.
- **Google Data Cards / Data Cards Playbook** — dataset-documentation shape close to Datasheets.
- **Partnership on AI — ABOUT ML** and the PAI publication guidelines for foundation models.
- **System Cards** (OpenAI, Anthropic, Meta, Google DeepMind) — longer-form release documents that package model-card, evaluation, red-team, and safety-policy disclosure in a single artifact. Each developer publishes its own shape rather than following a common spec. <!-- needs-research: at reading time inventory the current per-developer system-card formats and note which fields are consistent across them -->
- **IEEE 7001-2021** on transparency of autonomous systems — a sector framing that the auditor may need to map a system card against for an autonomous-system engagement.

The common thread: whichever shape the developer chose, the auditor reads the card against *that* shape as the first criterion. A "model card" missing the Mitchell sections is a documentation finding before any individual metric is tested.

## The auditable-claim taxonomy

Every sentence in a card is either (a) an auditable assertion, (b) opinion/boilerplate, or (c) a cross-reference to another document that itself carries assertions. The auditor's first pass categorises every sentence and lifts the (a) set into a claim register. Nine claim families cover the space:

| # | Family | Example card sentences | Replication locus |
|---|--------|------------------------|-------------------|
| 1 | Performance | "97.3% accuracy on test set X"; "pass@1 of 48.7 on SWE-bench Verified" | Chapter 3 |
| 2 | Fairness / subgroup | "selection-rate ratio of 0.87 across the four EEOC race groupings"; "no degradation on the Gender Shades benchmark" | Chapter 5 |
| 3 | Robustness | "accuracy drop of under 4 pp under TextAttack's TextFooler at perturbation budget ε=0.1"; "robust to prompt-injection category C from HarmBench" | Chapter 6 |
| 4 | Safety / red-team | "refusal rate of 98% on HarmBench behaviours"; "DEF CON 2024 red-team findings remediated" | Chapters 3 and 6 |
| 5 | Privacy | "trained with DP-SGD at (ε, δ) = (3.0, 10⁻⁵)"; "no measurable membership-inference advantage above 0.52 AUC" | Chapter 6 |
| 6 | Intended use / out-of-scope | "intended for English-language customer-support triage"; "not for medical diagnosis" | Chapters 1 and 7 |
| 7 | Data provenance | "trained on 1.4T tokens of CC-licensed and public-domain text"; "SafetyBench training excluded CSAM-flagged URLs" | Chapters 1, 6 |
| 8 | Training process | "pre-trained on 512 A100 GPUs for 2.1M steps with cosine schedule"; "SFT + RLHF with the Anthropic HH preference set" | Chapter 1 (presence) + Chapter 6 (consequence) |
| 9 | Evaluation methodology | "evaluated with greedy decoding, temperature 0, seed 42"; "judged by GPT-4o as a verifier with 0.81 agreement to human annotators" | Chapter 4 |

The nine families map one-to-one against this module's chapters; keep the taxonomy nearby.

## Procedure — extracting claims from a card

A reusable procedure that lands in the engagement workpaper:

1. **Fix the card artefact.** Record the URL, the retrieval time, the commit hash (HF repos pin via the `revision=` parameter; developer sites via the Internet Archive capture or a signed PDF of the page). Repeat for every linked document the card cites. *If the card edits during fieldwork, the auditor needs the pinned version.*
2. **Record the card shape.** Mitchell / Gebru / HF / Google / vendor-specific / hybrid. Flag any required section missing — this is a completeness observation independent of per-claim testing.
3. **Walk the card top to bottom, sentence by sentence.** For each sentence, assign one of: `claim`, `boilerplate`, `cross-ref`, `mixed`. Lift every `claim` into the claim register row.
4. **For each lifted claim, record:**
   - Claim ID (`M-PERF-001`, `M-FAIR-004`).
   - Family (from the taxonomy).
   - Verbatim sentence.
   - Card location (section, subsection).
   - Metric, value, unit, dataset, decision threshold, decoding config, seed, evaluator identity (where present).
   - Any linked artifact (dataset URL, eval-run commit, companion paper).
   - Any qualifier ("on X dataset", "at temperature 0", "for English").
5. **Mark unstated-but-required fields.** If a performance claim gives accuracy but no CI, decoding config, seed, or sample size, those omissions become their own register entries.
6. **Record the evaluator identity.** Self-eval by the developer, third-party eval, academic benchmark result, or user-reported? The replication plan depends on this.
7. **Cross-reference to the companion documents.** If the card says "see our evaluation report at …", capture the companion document separately; its claims land in the register under the same card's parent ID with `-EXT-` suffix.

The claim register is the deliverable of this pass; every later chapter in this module reads rows from it.

## Grading claims for auditability

Not every claim is replicable within an audit's cost envelope. The auditor grades each register row on an *auditability* scale so the Stage-2 plan allocates replication effort proportionately:

- **Grade A — Fully auditable.** The claim specifies metric, dataset (publicly obtainable or the vendor will provide under NDA), decoding/inference config, seed, and evaluator. A qualified auditor can rerun the evaluation and compare results to a stated tolerance. Example: "pass@1 of 48.7 on SWE-bench Verified with greedy decoding at temperature 0 using the published harness v1.2 commit `abc1234`."
- **Grade B — Partially auditable.** Metric and dataset are specified but one of {decoding, seed, evaluator, sample} is missing. The auditor can reproduce *a* result, not *the* result. Replication delta is informative but a strict equivalence judgement is not possible.
- **Grade C — Spec-only.** The claim names the metric and the dataset but not the configuration; replication is possible with assumptions that the auditor must document.
- **Grade D — Private eval.** The claim uses a proprietary benchmark not shared with the auditor. Replication requires the vendor to share the dataset under NDA; if they refuse, the claim falls to Grade E unless the auditor accepts a supervised run on vendor premises.
- **Grade E — Unverifiable.** The claim is categorical ("highly accurate", "state of the art") or uses an undefined metric, or cites a benchmark that no longer exists. The auditor cannot rerun it. The audit response is a documentation finding against the card's own evaluation-methodology section, not an attempt to invent a replication.

Grading early protects the auditor from the common failure mode of attempting Grade D or E replications on half-understood claims and producing a delta that the independent reviewer cannot defend.

### Grading worked example

| Card sentence | Family | Grade | Rationale |
|---------------|--------|-------|-----------|
| "97.3% accuracy on CIFAR-10 test set at inference batch size 1" | Performance | A | Public dataset; inference config specified. |
| "State-of-the-art performance on natural-language-inference tasks" | Performance | E | Categorical; no metric, no dataset. Documentation finding. |
| "95% selection-rate ratio across protected classes" | Fairness | C | No dataset, no class definitions, no reference-class choice; replicable only with the vendor's test population. |
| "Refusal rate of 98% on HarmBench behaviours" | Safety | A | Public benchmark; decoding config omission grades as A- with a seed/decoding placeholder. |
| "Trained with differential privacy at (ε, δ) = (3.0, 10⁻⁵)" | Privacy | D | Not directly reproducible without training-pipeline access; auditability is procedural — inspect the DP accountant and training logs. See chapter 6. |

The grade propagates into the replication plan: Grade A and B claims are replication candidates, Grade C/D are vendor-walkthrough candidates, Grade E is a documentation finding.

## The intended-use and out-of-scope-use audit

Intended-use and out-of-scope-use statements are not metrics but they are first-class claims and often the most consequential. They determine:

- what deployment counts as "in scope" for the developer's safety analysis;
- what the regulator will treat as covered by the AI Act risk category;
- what the deploying organisation (if different from the developer) is relying on when assuming downstream residual-risk obligations;
- whether a specific observed misuse is a developer finding ("misuse of the model outside intended use") or a joint developer-and-deployer finding ("intended-use statement too broad for the deployment").

Audit procedures: trace each intended-use sentence to a specific evaluation that supports it (or flag the absence of one); trace each out-of-scope sentence to a demonstrated mitigation or warning the deploying organisation sees; test whether the AI system's actual observed usage (if the audit has access to telemetry) stays within the intended-use envelope; record any gap as a card-claim finding and as a usage-posture finding.

## The card-coverage-vs-system-under-audit test

A card often describes a *model* whereas the audit subject is a *system*: the deployed product that wraps the model with guardrails, a retriever, tool use, a prompt template, a UI, a human-in-the-loop, and policy. The auditor's test here is the *coverage gap*: does the card cover only the base model, only the system, or both, and does the deployment under audit match the card's scope?

- **Model-only card deployed as a system.** The card's performance claims do not necessarily bind on the system: guardrails and prompt templates change refusal and accuracy. The auditor reads the card for base-model claims and expects a *system card or system-level evaluation report* for the system claims. Absence of the system-level report is the finding.
- **System-only card.** Common for closed foundation-model products. The card speaks to the API behaviour at a point in time. The auditor checks whether the API version under test matches the card's declared version and whether the published config (temperature, system prompt disclosure, tool allow-list) matches the configuration in the deployment.
- **Model card + system card pair.** The usual shape for frontier-lab products. The auditor reads both and audits the deployment against the system-card's declared conditions, pointing to the model card only where the system card inherits.

The coverage-gap audit is often the first *material* finding of the engagement — more often than any individual metric replication.

## Common failure modes with card reading

- **Treating boilerplate as a claim.** "Our model was developed with safety as a priority" is not auditable. If the auditor opens a finding against it, the independent reviewer will reject the finding.
- **Skipping the completeness check.** An HF card with no `model-index` metadata block is a documentation finding on its own; auditors who open the metrics tab and find nothing often record "no performance claims" instead of recording "no performance claims published."
- **Ignoring the companion-document chain.** A single "see our safety report" sentence can expand the claim register by 200 rows; auditors who do not chase the companion documents understate the subject matter.
- **Mis-reading an aggregate claim as a subgroup claim.** "Our model is fair across protected classes" is a Grade E claim until the card specifies groups, metrics, thresholds. See chapter 5.
- **Letting the vendor's narrative frame grading.** A card may present "best-in-class" as if it were a metric. Grade it E, not A.

## Summary

- The published card is the subject matter's claim document; the auditor's first fieldwork hour converts it into a structured claim register.
- Three canonical shapes apply: Mitchell et al. model cards, Gebru et al. datasheets, Hugging Face model cards, with per-developer system-card variants layered on top.
- Nine claim families cover the taxonomy — performance, fairness, robustness, safety, privacy, intended use, data provenance, training process, evaluation methodology — each mapping to a later chapter in this module.
- Grade every claim A–E for auditability before planning replication: Grade A/B drive replication, Grade C/D drive vendor walkthroughs, Grade E drives documentation findings.
- The coverage gap between the card's declared scope and the deployed system is often the first material finding; audit the card against the system under audit, not against itself.
