# Auditing Robustness, Privacy, and Red-Team Claims

## Motivation

Robustness, privacy, and red-team claims form the operational-safety tier of the card. They answer "how does the model behave when the input is adversarial, and what can an attacker extract from it, and how comprehensively has that been tested?" These claims are both the easiest to overstate and the hardest to under-audit, because the attack surface is large and the vendor's own testing is necessarily partial.

The auditor does not invent attacks; attack authoring is `ai-risk-engineer` and frontier-safety work is `agentic-safety-engineer`. The auditor's job is to test the claim's *shape*: does the vendor's testing cover an appropriate attack surface, does it use a defensible adversarial budget, does its privacy accounting add up, and is its red-team catalog comprehensive enough that an uncovered threat would be surprising? This chapter installs those shape tests and the applied replication procedures the auditor performs.

## Robustness claims

### The anatomy of a robustness claim

A defensible robustness claim names:

- the *threat model* (white-box vs. black-box; attack class — word-swap, paraphrase, character-level, embedding-space; input constraints);
- the *attack* (TextFooler, PGD, DeepWordBug, universal-triggers, HarmBench-style jailbreak);
- the *budget* (perturbation ε, number of queries, semantic-similarity floor);
- the *metric* (attack success rate, clean accuracy drop, worst-case accuracy under budget);
- the *baseline* (undefended model or published reference);
- the *sample* (which examples, how many, which split).

A card that gives only "robust to adversarial inputs" with no budget is making an unverifiable claim; grade E and open a documentation finding.

### The attack-surface-coverage test

The auditor compares the claim's attack coverage to the deployment's attack surface:

| Deployment | Attack surface the claim should cover |
|------------|---------------------------------------|
| Text classifier (content moderation) | Word-swap, paraphrase, character-level perturbation (TextAttack); unicode / homoglyph attacks |
| Vision classifier | L∞ / L2 budgeted (PGD, C&W); patch attacks; physical-world perturbation if deployment includes real cameras |
| LLM chat endpoint | Prompt injection (direct and indirect); jailbreak catalogs (HarmBench); multilingual bypasses; role-play / DAN variants |
| Tool-using agent | AgentDojo / InjecAgent attack suites; retrieved-document injection |
| Multimodal model | Image-text cross-modal injection; VLM-specific jailbreaks |

A card for an LLM chat endpoint that reports only word-swap robustness is under-covering; the finding is "robustness testing does not cover the attack classes relevant to the deployment," not "the number is wrong."

### The adversarial-budget audit

Budgets must be stated and reasonable for the deployment:

- **Perturbation budget.** L∞ ε values of 8/255 for CIFAR-10 and 0.3 for MNIST are standard; deviation from standard requires justification.
- **Query budget.** Black-box attacks trade query count for success; the stated query budget should be at least the realistic adversary's capability.
- **Semantic-similarity floor.** For text attacks, how similar does the adversarial input remain to the clean input? USE similarity 0.84, or BERT-score 0.85, or none at all? Floors that are too permissive produce inflated attack-success numbers; floors that are too strict produce deflated ones.

The auditor's test is procedural: the budget is stated, the budget is reasonable, and the replication runs at the stated budget.

### Replicating a robustness claim

For a Grade A/B robustness claim:

1. **Pin the attack.** TextAttack / ART / CleverHans release; attack recipe; model-under-attack endpoint or weights.
2. **Pin the budget.** ε; query count; similarity floor; max perturbation length.
3. **Pin the sample.** Dataset split; sample size; any filtering.
4. **Run.** Produce per-sample adversarial-input, adversarial-output, success-flag records.
5. **Compute.** ASR; clean-vs-adversarial accuracy drop; worst-case accuracy under budget. Bootstrap CI.
6. **Emit the signed-delta row** (chapter 3 shape).

A single cross-check (same attack, different seed or node) confirms that the delta is not a run-specific artifact.

### Common failure modes with robustness claims

- **Comparing attacks across budgets.** A card's "ASR of 24% under TextFooler" at semantic-similarity 0.5 is not comparable to the auditor's run at 0.84.
- **Reporting worst-case over a cherry-picked attack set.** The vendor runs ten attacks, reports the best model-defence result. The auditor runs the full canonical suite.
- **Equating ε=0.03 (strong) with ε=0.1 (very strong) without declaring the units.** L∞ vs. L2 vs. semantic — always declare.
- **Running a modern attack against a model trained with an outdated defence.** The auditor notes the attack/defence vintage pair in the manifest.

## Privacy claims

### The anatomy of a privacy claim

A defensible privacy claim names:

- the *protection target* (training-data membership; attribute inference; verbatim regurgitation; PII extraction);
- the *mechanism* (differential privacy with DP-SGD at specific (ε, δ); dataset deduplication; output-filtering regex; retrieval redaction);
- the *budget* (ε, δ for DP; TPR-at-fixed-FPR for empirical MIA; PII-detection recall);
- the *evaluator* (MIA attack used; benchmark; sample).

### Differential-privacy accounting plausibility

If the card reports "trained with DP-SGD at (ε, δ) = (3.0, 10⁻⁵)" the auditor cannot retrain to verify, but can test plausibility:

- **Accountant identity.** Which accountant was used? Moments accountant (Abadi et al. 2016), Rényi DP accountant (Mironov 2017), PRV accountant (Gopi et al. 2021)? Opacus and TF Privacy each produce accountant logs.
- **Hyperparameter consistency.** Noise multiplier σ, clipping norm C, batch size, microbatch, dataset size, and epoch count collectively determine ε at the stated δ. The accountant log must be internally consistent with the training-pipeline hyperparameters. The auditor inspects the training log and re-runs the accountant on the stated hyperparameters.
- **δ choice.** δ should be < 1/n where n is dataset size; a δ of 10⁻⁵ against a 1,000-row dataset is weak.
- **Composition across training phases.** Pre-training, fine-tuning, and RLHF each incur a privacy cost; the card's headline ε should be the composed ε, not a single-phase ε.
- **Group-DP vs. per-example-DP.** If the mechanism is group-level DP (e.g., per-user), the card should name the group definition; ambiguity is a finding.
- **Secret-sharing / secure aggregation.** Federated training with secure aggregation has its own accounting; the auditor flags if the card conflates it with central DP.

The applied reference for DP accounting is the TF Privacy or Opacus accountant's output. The auditor re-runs the accountant on the vendor's declared hyperparameters and reports whether the published ε is consistent.

### Membership-inference audit

Independent of DP claims, empirical privacy is measured via membership-inference attacks (MIA): given a model and a candidate record, can an attacker tell whether the record was in the training data?

- **Metric.** TPR at a fixed low FPR (e.g., TPR at FPR = 0.001) following Carlini et al. "Membership Inference Attacks from First Principles" (2022). <!-- needs-research: confirm the current state of MIA evaluation practice at reading time; the Carlini et al. paper established TPR@low-FPR as the norm but newer attacks and critiques exist -->
- **Attack.** ML Privacy Meter runs canonical LiRA and reference-model attacks against the subject.
- **Baseline.** The MIA TPR for a non-private baseline should be clearly non-trivial; absence of a baseline run is a methodology gap.
- **Interpretation.** A TPR of 0.52 at FPR 0.001 is near-random; a TPR of 0.3 at the same FPR is significant and inconsistent with strong DP.

The auditor runs the attack where the vendor provides eval-mode access to the model, and reports TPR-at-fixed-FPR against the card's claim (if any) or against a zero-privacy baseline.

### Verbatim-regurgitation / extraction claims

Cards may claim "model does not emit training-data verbatim." The auditor:

- **Reads the testing protocol.** Was extraction tested with canonical prompts (Carlini et al. "Extracting Training Data from Large Language Models" (2021) family of protocols)? With prefix-injection attacks? <!-- needs-research: cite the current canonical extraction-attack paper set at reading time -->
- **Runs a minimum extraction test.** Where permitted, prompt the system with partial training-adjacent prefixes and look for verbatim continuation above a token threshold.
- **Reports with appropriate restraint.** Extraction attacks are headline-grabbing; the auditor's report sticks to the specific test and avoids extrapolation.

### PII-handling claims

Cards for deployed systems may claim "PII is redacted before storage" or "PII is not logged." The auditor:

- **Reads the pipeline.** Where is Presidio (or an equivalent) applied? What classes? With what thresholds?
- **Runs a targeted probe.** Representative PII-bearing inputs; test whether the pipeline redacts.
- **Inspects retention artifacts.** Spot-checks the trace store (`mod-104`) for PII that should have been redacted.

### Common failure modes with privacy claims

- **Accepting a headline ε without the accountant log.** The auditor re-runs the accountant.
- **Reporting MIA AUC where TPR-at-FPR is the current standard.** Flag the methodology weakness.
- **Confusing central DP with local DP.** Entirely different privacy semantics; the card must say which.
- **Extrapolating a single-prompt extraction result into a general claim.** The auditor keeps the finding tied to the specific probe.

## Red-team claims

### The anatomy of a red-team claim

A defensible red-team claim names:

- the *scope* (which capabilities, which use cases, which deployment surfaces);
- the *catalog* (HarmBench taxonomy, MITRE ATLAS, OWASP LLM Top 10, AI-Risk-Engineer's internal catalog, DEF CON red-team outputs);
- the *process* (who performed, with what time budget, under what rules of engagement);
- the *findings* (categorised, with severity, with remediation state);
- the *residual-risk statement* (what remains unmitigated, with the rationale).

A card that says "we red-teamed the model" with none of the above is unverifiable.

### The red-team-coverage-matrix audit

The auditor constructs a coverage matrix: attack-classes × deployment-surfaces × coverage-status. Rows are drawn from an industry taxonomy the engagement pins (MITRE ATLAS, OWASP LLM Top 10 for the LLM deployments, HarmBench behaviour categories for safety). Columns are the deployment surfaces in scope. The auditor marks each cell covered / partially-covered / uncovered based on vendor artefacts (red-team reports, eval runs, issue-tracker entries).

An uncovered cell for a high-materiality attack-class × deployment-surface pair is a finding. A pattern of uncovered cells is a different finding — "red-team programme scope insufficient for the deployment." The auditor does not fill in the matrix by authoring attacks; the matrix reports the vendor's coverage, not the auditor's.

### Industry taxonomies the matrix uses

- **OWASP Top 10 for LLM Applications (OWASP LLM Top 10).** Prompt injection, insecure output handling, training-data poisoning, model DoS, supply-chain, sensitive-information disclosure, insecure plugin design, excessive agency, overreliance, model theft. <!-- needs-research: the OWASP LLM Top 10 evolves; confirm the current edition and item ordering at reading time -->
- **MITRE ATLAS.** Adversarial threat landscape for AI systems; tactics-and-techniques matrix with associated case studies.
- **HarmBench behaviour categories.** Standardised harm taxonomy for safety red-teaming.
- **NIST AI 100-2e (Adversarial Machine Learning Taxonomy).** Reference taxonomy for adversarial ML attacks and mitigations.

The engagement pins its reference taxonomy in the audit plan and keeps it constant across findings.

### Replay-bundle integrity

When the vendor publishes red-team results, the auditor asks for the *replay bundle*: the attack prompts (or their hashes where disclosure is controlled), the model responses, the scoring, and the remediation record. The audit of the bundle:

- **Hash integrity.** Does every prompt hash to a stable value? Is the bundle Git-pinned?
- **Scoring reproducibility.** Can the auditor rerun the scoring on the supplied prompt-response pairs and reproduce the vendor's grades?
- **Remediation closure.** For each "resolved" finding, is there an evidence trail — model update, guardrail config change, policy change — tied to a date?
- **Payload containment.** The bundle contains sensitive payloads; it is a WORM-stored, access-restricted artefact per chapter 7's disclosure discipline.

Where the vendor refuses to share the replay bundle but claims "red-team findings remediated," the auditor's option is to run an independent sample and report "we could not replicate the vendor's red-team closure, independently sampled N attacks from the public catalog, observed M residual findings."

### Common failure modes with red-team claims

- **Accepting "we red-teamed" as a claim.** It is not a claim; the shape is.
- **Treating the public HarmBench run as evidence of full red-team coverage.** Coverage matrix is broader than a single benchmark.
- **Letting the vendor select which red-team findings to disclose.** Spot-check against independent sources (CVE-adjacent AI incident databases, researcher disclosures, press reports).
- **Not categorising findings by severity.** A vendor that reports 200 findings without severity grades has not characterised residual risk.
- **Confusing the AI-auditor role with pentesting.** The auditor audits the programme and samples. Pentest depth sits with `ai-risk-engineer`.

## Cross-cutting: the "limitation of adversarial-payload disclosure" problem

Robustness, privacy, and red-team artefacts frequently contain payloads the auditor's report should not disseminate:

- jailbreak prompts and their working output;
- extraction-attack prefixes;
- cyber-security-adjacent content;
- WMDP-adjacent dangerous-knowledge probes;
- CSAM-adjacent test content (which the vendor should never produce in the first place, but if present must never leave the vendor's secure handling environment).

The auditor's discipline:

- **Classify every artefact by disclosure class.** Open / internal / limited / restricted.
- **Store restricted artefacts in WORM storage with per-artefact access control** (chapter 4 of `mod-104`).
- **Author the report in two variants** — full-disclosure (restricted recipients, cleared) and summary-disclosure (regulator, audit committee, public) — with payloads replaced by hashes and a controlled-access reference. Chapter 7 operationalises.
- **Do not disclose payloads in chat, email, or shared drives.** Payloads leave the workstation only through the engagement's sanctioned pipe.

Writing a "comprehensive red-team audit report" that leaks a working jailbreak into a press release is a professional-malpractice finding on the auditor.

## Summary

- Robustness, privacy, and red-team claims each have a defensible shape (threat model / mechanism / budget / metric / sample / evaluator); cards missing elements are unverifiable claims the auditor documents.
- The robustness audit tests attack-surface coverage, adversarial budget reasonableness, and reproducibility under pinned tools (TextAttack, ART, CleverHans).
- The privacy audit tests DP-accountant plausibility (Opacus / TF Privacy accountants), MIA TPR-at-fixed-FPR (ML Privacy Meter), extraction protocol conformance, and PII-handling evidence.
- The red-team audit constructs an industry-taxonomy coverage matrix (OWASP LLM Top 10, MITRE ATLAS, HarmBench, NIST AI 100-2e), audits the replay bundle's integrity, and samples independently where the vendor withholds.
- Adversarial-payload disclosure is a cross-cutting discipline — classify, store under WORM with access control, author dual-disclosure report variants; chapter 7 operationalises.
