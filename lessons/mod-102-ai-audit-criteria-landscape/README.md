# mod-102-ai-audit-criteria-landscape: AI Audit Criteria Landscape — Framework-to-Criteria Translation

**Estimated effort:** 16 hours

This module teaches the AI Auditor the single most load-bearing translation skill in the role: turning *framework clauses* (ISO/IEC 42001, NIST AI RMF, EU AI Act, sector overlays) into *auditable criteria* — testable, measurable, with a named evidence artifact per statement. Every downstream module in the track (`mod-103` risk-based audit planning, `mod-104` evidence and sampling, `mod-105`–`mod-110` the regime-specific audits, `mod-111` findings and reporting) assumes you can produce a criteria register for the engagement in front of you and defend each statement under IAASB ISAE 3000 / AICPA AT-C 105 suitability tests.

## Learning objectives

- Translate ISO/IEC 42001:2023 clauses 4–10 and Annex A controls into a working set of *auditable criteria* — testable, measurable, with clear sources of evidence per control.
- Translate NIST AI RMF 1.0 GOVERN / MAP / MEASURE / MANAGE categories, the NIST AI RMF Playbook, and NIST AI 600-1 GenAI Profile risks into auditable criteria the AI Auditor can test against.
- Translate EU AI Act 2024/1689 obligations (Articles 9 risk-management system, 10 data governance, 11 technical documentation, 12 record-keeping, 13 transparency, 14 human oversight, 15 accuracy / robustness / cybersecurity, 16–29 providers / deployers / importers / distributors, 43–44 conformity assessment, 55 systemic-risk GPAI, 61 registration, 72 post-market monitoring, 73 serious-incident reporting) into auditable criteria, aligned to the harmonised standards where available (CEN/CENELEC JTC 21) and the EU AI Office GPAI Code of Practice.
- Position sector regulation as additive audit-criteria overlays — US Fed SR 11-7 / OCC 2011-12 / SR 23-4 model-risk-management shape, FDA GMLP + PCCP and 21 CFR Part 820 adapted for AI/ML SaMD, HIPAA Security Rule adapted for AI, NAIC Model Bulletin on AI use by insurers, Colorado AI Act (SB 24-205) algorithmic-discrimination obligations, NYC LL144 AEDT independent bias audit, Illinois AI Video Interview Act, OMB M-24-10 and M-25-21 federal-agency AI inventory and CAIO obligations, UK AI governance White Paper, Canada AIDA, Singapore AI Verify, Japan AI Guidelines for Business, Korea AI Basic Act, India DPDPA / IndiaAI, Brazil PL 2338, China Interim Measures for Generative AI Services.
- Build a crosswalk register from one source framework to all peer frameworks (NIST AI RMF ↔ ISO/IEC 42001 ↔ EU AI Act ↔ sector overlays) so a single evidence artifact can be traced to all downstream audit criteria it supports — reusing the `senior-ai-governance-architect` (level 50) control-library architecture as the parent target-state.
- Cite and apply the IAASB AI assurance standards pipeline and the AICPA SOC-for-AI exposure drafts where published; note where the audit standard is still immature and professional judgment is required.
- Defer *down* to `ai-governance-analyst` (level 15) for the analyst-tier framework-crosswalk legwork this role consumes; defer *up* to `senior-ai-governance-architect` (level 50) for the enterprise control-library architecture the auditor audits against.

## Chapters

1. [`01-what-makes-a-criterion-auditable.md`](01-what-makes-a-criterion-auditable.md) — framework clauses vs. auditable criteria; the chapter-1 template that every later register and exercise uses.
2. [`02-iso-42001-clauses-and-annex-a-to-criteria.md`](02-iso-42001-clauses-and-annex-a-to-criteria.md) — translation playbook for ISO/IEC 42001 clauses 4–10, Annex A controls, and the Statement of Applicability.
3. [`03-nist-ai-rmf-and-genai-profile-to-criteria.md`](03-nist-ai-rmf-and-genai-profile-to-criteria.md) — GOVERN / MAP / MEASURE / MANAGE Subcategories, the AI RMF Playbook as an evidence-candidate list, and the NIST AI 600-1 GenAI Profile overlay.
4. [`04-eu-ai-act-articles-to-criteria.md`](04-eu-ai-act-articles-to-criteria.md) — scoping, Articles 9–15 high-risk obligations, actor-role obligations (16–29), conformity assessment, transparency, GPAI and systemic-risk GPAI, post-market monitoring and incident reporting; harmonised-standards alignment under Article 40 and the GPAI Code of Practice.
5. [`05-sector-and-jurisdictional-overlays.md`](05-sector-and-jurisdictional-overlays.md) — additive overlay criteria for SR 11-7, FDA GMLP/PCCP/QMSR, HIPAA, NAIC, Colorado, NYC LL144, Illinois, OMB M-24-10/M-25-21, and major international regimes.
6. [`06-crosswalk-register-authoring.md`](06-crosswalk-register-authoring.md) — the crosswalk register architecture: Design-A controls and Design-B evidence rows, cell content (citation / degree / linked criterion / evidence location), and testing the register itself.
7. [`07-iaasb-aicpa-ai-assurance-standards.md`](07-iaasb-aicpa-ai-assurance-standards.md) — the methodology stack today (ISAE 3000 / AT-C 205 / ISSA 5000), the AICPA SOC-for-AI pipeline, and where professional judgment carries the engagement until the pipeline lands.

## Exercises

- [`exercise-01-iso-42001-clause-to-criteria-translation.md`](exercises/exercise-01-iso-42001-clause-to-criteria-translation.md) — translate ISO/IEC 42001 clauses 4–6.1 plus selected Annex A controls for a health-tech first-cycle AIMS internal audit.
- [`exercise-02-nist-ai-rmf-and-genai-profile-to-criteria.md`](exercises/exercise-02-nist-ai-rmf-and-genai-profile-to-criteria.md) — build the criteria register for an AT-C 205 examination of a foundation-model provider's AI safety program, with the GenAI Profile overlay.
- [`exercise-03-eu-ai-act-articles-to-criteria-with-harmonised-standards.md`](exercises/exercise-03-eu-ai-act-articles-to-criteria-with-harmonised-standards.md) — author Articles-9-through-73 criteria for a high-risk recruitment AI provider, aligned to harmonised standards and the GPAI Code of Practice.
- [`exercise-04-sector-overlay-criteria-drill.md`](exercises/exercise-04-sector-overlay-criteria-drill.md) — layer SR 11-7, FDA GMLP/PCCP/QMSR, HIPAA + NAIC, Colorado, and NYC LL144 + Illinois overlays onto a multi-subsidiary insurance / financial group.
- [`exercise-05-framework-crosswalk-register-authoring.md`](exercises/exercise-05-framework-crosswalk-register-authoring.md) — assemble the crosswalk register across the prior exercises and audit the register itself for over-claims, gaps, and stale cells.
- [`exercise-06-iaasb-aicpa-assurance-standards-read.md`](exercises/exercise-06-iaasb-aicpa-assurance-standards-read.md) — standards map, pipeline notebook, engagement-letter paragraph suite, and independence memo for a GenAI examination at a mid-tier CPA firm.

## Role boundary (reminder)

- The `ai-governance-analyst` (level 15) produces the raw framework-crosswalk legwork this role consumes — refresh cycles, rolling crosswalk-cell maintenance, inventory scaffolding. The AI Auditor is a *buyer* of that work, not an author.
- The `senior-ai-governance-architect` (level 50) *designs* the enterprise control library, taxonomy, and crosswalk register the AI Auditor audits against. The auditor does not author the control library inside the engagement — if you find yourself doing so, see `mod-101` chapter 1 for the independence posture at risk.
- The AI Auditor's own output in this module is the *criteria layer* — the testable statements that connect external frameworks to the organisation's internal controls. The register is the junction.

## Structure

- Lecture chapters `01-…md` … `07-…md`.
- `exercises/` — hands-on prompts (solutions live in the paired `-solutions` repository).
- `labs/` — long-form hands-on labs (planned; see `labs/README.md`).
- `quizzes/` — knowledge checks (planned; see `quizzes/README.md`).
- [`resources.md`](resources.md) — primary standards, codes, crosswalks, and tooling references for every chapter and exercise.
