# mod-106-auditing-model-and-system-card-claims: Auditing Model / System / Dataset Card Claims and Independent Replication

**Estimated effort:** 18 hours

## Learning objectives

- Read a published model / system / dataset card (Hugging Face model-card format, Mitchell et al. Model Cards for Model Reporting, Gebru et al. Datasheets for Datasets) as an independent assurance practitioner — identifying every assertion that is auditable (performance, fairness, robustness, safety, intended use, out-of-scope use, data provenance, training process, evaluation methodology).
- Independently replicate performance and safety evaluations using the `ai-risk-engineer` (L25) + `ai-eval-engineer` (L30) + `model-evaluation-engineer` (L30) open-source toolchain — garak, PyRIT, Promptfoo, Inspect (UK AISI) for LLMs; ART, TextAttack, CleverHans, Counterfit for adversarial ML; Fairlearn, AIF360, Holistic AI, SHAP, Alibi, LIME for fairness and explainability; Opacus, TensorFlow Privacy, ML Privacy Meter, Presidio for privacy — without re-authoring the methodology (that depth lives in the prerequisite tracks and peers).
- Replicate HarmBench, AIR-Bench 2024, AgentDojo, InjecAgent, WMDP, MLCommons AILuminate, Meta CyberSecEval, METR public tasks, SWE-bench Verified, and the policy-derived internal eval suite against the system under audit; report attack-success-rate / coverage / refusal-rate against the published claim with a signed delta.
- Apply `model-evaluation-engineer` (L30) calibration methodology to published metrics — judge-vs-human kappa, inter-annotator agreement, bootstrap CIs, effect-size reporting, power analysis — to decide if the published number is defensibly supported by evidence or if the claim is overstated.
- Audit fairness claims to an auditor-independent shape — test whether the fairness metric selected is appropriate for the use case (NYC LL144 shape calling for demographic-parity + equal-opportunity reporting, EEOC adverse-impact four-fifths test, EU AI Act Article 10 and Article 15 obligations), whether the protected classes tested cover the obligation, whether subgroup intersectionality is reported, whether the reported numbers are reproducible; produce the Algorithmic Impact Assessment and the independent Bias Audit Report in the BABL AI and ForHumanity IAAIS shapes.
- Audit robustness, privacy, and red-team claims to an auditor-independent shape — attack surfaces covered, adversarial budget, membership-inference TPR-at-fixed-FPR, DP (ε, δ) accounting plausibility, red-team coverage matrix completeness, replay-bundle integrity.
- Produce a signed independent replication report — procedure, environment pin, result, delta vs. published claim, limitations, scope restrictions, conclusion — consumable by the audit committee, the regulator, and the vendor (if third-party), without disclosing adversarial payloads to unauthorised audiences.
- Keep the AI-Auditor replication depth bounded — this role does NOT author novel red-team attacks or novel fairness metrics; attack authoring sits with `ai-risk-engineer` (L25) and frontier-depth with `agentic-safety-engineer` (L40), and statistical-methodology authoring with `model-evaluation-engineer` (L30).

## Structure

- [`01-reading-the-card-as-an-auditor.md`](01-reading-the-card-as-an-auditor.md) — the three canonical card formats (Mitchell, Gebru, Hugging Face), the auditable-claim taxonomy, claim extraction, and the auditability grading rubric (A–E).
- [`02-replication-toolchain-and-borrowed-depth.md`](02-replication-toolchain-and-borrowed-depth.md) — the toolchain (garak, PyRIT, Promptfoo, Inspect; ART, TextAttack, CleverHans, Counterfit; Fairlearn, AIF360, Holistic AI, SHAP, Alibi, LIME; Opacus, TF Privacy, ML Privacy Meter, Presidio) and the borrowing contract that keeps auditor independence.
- [`03-replicating-public-benchmarks-and-reporting-the-delta.md`](03-replicating-public-benchmarks-and-reporting-the-delta.md) — HarmBench, AIR-Bench 2024, AgentDojo, InjecAgent, WMDP, MLCommons AILuminate, Meta CyberSecEval, METR, SWE-bench Verified; the signed-delta register and the four delta statuses.
- [`04-calibration-methodology-challenge.md`](04-calibration-methodology-challenge.md) — sample size / sampling / evaluator reliability / uncertainty quantification; Wilson, bootstrap, kappa, Cohen's d; overstatement grading.
- [`05-auditing-fairness-claims.md`](05-auditing-fairness-claims.md) — the obligation surface (NYC LL144, EEOC, EU AI Act Articles 10/15/27, Colorado AI Act, sector overlays); metric-appropriateness; protected-class coverage; intersectionality; the AIA summary, BABL AI, and ForHumanity IAAIS report shapes.
- [`06-auditing-robustness-privacy-and-red-team-claims.md`](06-auditing-robustness-privacy-and-red-team-claims.md) — attack-surface coverage, adversarial-budget audit, DP-accountant replication, MIA TPR-at-fixed-FPR, red-team coverage matrix (OWASP LLM Top 10, MITRE ATLAS, HarmBench, NIST AI 100-2e), replay-bundle integrity.
- [`07-the-independent-replication-report.md`](07-the-independent-replication-report.md) — report structure, opinion-vs-conclusion shape, multi-audience variants (audit committee, regulator, vendor, public), adversarial-payload discipline, signatures, and workpaper traceability.
- [`exercises/`](exercises/) — per-exercise prompts aligned to the chapters.
- [`labs/`](labs/), [`quizzes/`](quizzes/) — long-form labs and knowledge checks.
- [`resources.md`](resources.md) — curated primary references.

## How this module fits the `ai-auditor` track

- **Input from `mod-101`** — independence and attestation-stack shape that governs the report variants in chapter 7.
- **Input from `mod-102`** — criteria translation for the obligation surface (NYC LL144, EEOC, EU AI Act, ISO/IEC 42001) referenced in chapters 5–7.
- **Input from `mod-103`** — scoping, materiality, and the engagement letter that fixes the attestation type.
- **Input from `mod-104`** — evidence discipline (ISA 500), sampling (ISA 530), specialist use (ISA 620), WORM storage for payload-bearing artefacts.
- **Input from `mod-105`** — the Stage-2 fieldwork context in which card-claim replication often lives.
- **Output to `mod-107`** — harm-model audits inherit the chapter-5 fairness audit and chapter-6 robustness/privacy/red-team findings.
- **Output to `mod-108`** — post-market monitoring audits reuse the replication toolchain for ongoing claim verification.
- **Output to `mod-109`** — third-party / supply-chain audits reuse the vendor-variant report shape from chapter 7.
- **Output to `mod-110`** — conformity-assessment-body shape at the sector level (EU AI Act Annex VII, FDA GMLP) inherits the attestation-type fixing from chapter 7.
- **Output to `mod-111`** — findings reporting discipline for the per-claim finding register from chapters 3–6.
- **Delta from `ai-risk-engineer` (L25)** — attack authoring and novel red-team cataloging sit there; the auditor runs the catalogs.
- **Delta from `ai-eval-engineer` (L30)** — application-eval harness authoring and CI/CD plumbing sit there; the auditor invokes the harness.
- **Delta from `model-evaluation-engineer` (L30)** — novel statistical procedure authoring sits there; the auditor applies canonical procedures.
- **Delta from `agentic-safety-engineer` (L40)** — frontier capability-elicitation research sits there; the auditor reads the resulting report as a claim document.
