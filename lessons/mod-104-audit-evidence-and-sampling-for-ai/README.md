# mod-104-audit-evidence-and-sampling-for-ai: Audit Evidence, Sampling, and Workpapers for AI Systems

> Scaffolded by `aicg org execute-plan`. Lecture chapters and exercise content are authored on subsequent autonomous cycles.

**Estimated effort:** 16 hours

## Learning objectives

- Apply ISA 500 / AU-C 500 sufficient-and-appropriate-audit-evidence requirements to AI artifacts — model weights, training data, evaluation datasets, eval run artifacts, inference logs, prompt / retriever / tool traces, decoding configs, guardrail configs, monitoring dashboards, incident records, change-management records, vendor attestations — and defend why each artifact is relevant and reliable evidence for the criterion being tested
- Apply ISA 530 / AU-C 530 audit sampling to AI testing — statistical sampling on labelled production-trace populations, judgmental sampling on edge-case red-team catalogs, attribute vs. variables sampling, sample-size determination from expected and tolerable deviation rate, projection-of-misstatements to the population
- Apply ISA 620 / AU-C 620 using the work of an auditor's specialist — competence, capability, and objectivity assessment on an ML/AI technical specialist who assists the audit; interpret the specialist's output into audit conclusions; defend when to use an in-team ML specialist vs. an external contractor
- Build the AI-specific audit evidence inventory — what counts as original evidence (git-pinned eval configs, signed model attestations with Sigstore, trace-store queries with reproducible hashes), what counts as derivative (dashboard screenshots, management attestations), and what counts as corroborative (independent re-runs, third-party eval reports)
- Author audit workpapers that would survive peer review, external QA, and PCAOB-style inspection — objective, criterion, procedure performed, evidence inspected, exception noted, conclusion reached, cross-referencing — in an electronic working-paper system (Caseware / TeamMate+ / Workiva / AuditBoard) and in a Git-tracked repo for AI-native engagements
- Build a reproducibility bundle for every assertion the auditor independently replicates (model version, seed, decoding config, prompt template, retriever config, tool versions, dataset hash, evaluator code, metric definitions) — citing the peer calibration-methodology depth to `model-evaluation-engineer` (level 30) and application-eval-plumbing depth to `ai-eval-engineer` (level 30)
- Chain-of-custody and audit-log integrity — WORM storage, tamper-evident logs, hash-chained evidence manifests, git-pinned workpapers; detect evidence tampering (back-dated commits, replaced model artifacts, log mutation) under professional-skepticism

## Structure

- `01-…md` … `0N-…md`: lecture chapters.
- `exercises/`: per-exercise prompts.
- `labs/`: long-form hands-on labs.
- `quizzes/`: knowledge checks.
- `resources.md`: external references.
