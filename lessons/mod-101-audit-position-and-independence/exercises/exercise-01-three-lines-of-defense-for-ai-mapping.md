# exercise-01: Three Lines of Defense for AI — Role and Artifact Mapping

**Estimated effort:** 2 hours

## Objective

Produce a defensible, written mapping of the IIA Three Lines Model (2020 revision) onto the AI roles, artifacts, and controls of a specified fictitious organisation, and defend the placement of the AI Auditor on that map. The deliverable is a one-page diagram plus a one-page memo of ~600 words, in a shape an audit-committee reader would accept.

## Prerequisites

- Chapter [`01-third-line-scope-and-boundaries.md`](../01-third-line-scope-and-boundaries.md)
- Chapter [`02-iia-three-lines-model-and-ippf.md`](../02-iia-three-lines-model-and-ippf.md)
- The IIA Three Lines Model (2020) document — read in full before starting

## Scenario

**NorthernMutual Life** is a fictitious mid-size US life insurer. It operates:

- A **claims-triage ML model** that classifies incoming claims into fast-track vs. standard review (deployed 2023, re-trained quarterly, logistic + gradient-boosted pipeline).
- A **customer-service LLM assistant** (deployed 2025, retrieval-augmented, uses a third-party foundation-model API with tool-calling for policy lookup).
- An **underwriting-support LLM** in pilot (not yet in production, assists human underwriters by summarising applicant medical records).

It has the following internal functions relevant to AI:

- Data Science team (reports to CDO) — authors and operates the ML models.
- ML Platform team (reports to CTO) — operates MLflow, feature store, inference serving, monitoring.
- Model Risk Management group (reports to CRO, aligned to SR 11-7 insurance-adapted practice) — validates models, operates the model inventory.
- AI Governance Committee (chaired by CRO, includes CCO, CLO, CDO) — approves AI use cases, reviews ethics escalations.
- AI Ethics Officer (reports to CLO) — co-chairs the ethics-escalation workstream.
- Information Security — operates SOC, DFIR, vulnerability management.
- Internal Audit — reports to the Audit Committee, administratively to the CFO. Three auditors, one of whom is being hired as the first AI Auditor.
- External parties: Big-4 financial-statement auditor; accredited certification body (NorthernMutual has engaged for ISO/IEC 42001 certification in 2027); NAIC state insurance regulator.

## Deliverables

1. **Mapping diagram** (one page, PDF, PowerPoint, or Markdown + Mermaid is acceptable). Place each internal function and each external party onto the Three Lines Model, including:
   - Governing body and senior management at the top.
   - First line, second line, third line distinctly marked.
   - External assurance providers shown outside the three lines.
   - For each AI artifact in scope (the three AI systems, their eval artifacts, the model inventory, the AIMS documentation, the AI Governance Committee's decision log, the MRM validation reports), name which line is **accountable** for it and which line(s) are **monitoring** it.

2. **Placement memo** (~600 words, Markdown). Argue:
   - Where the newly hired AI Auditor should sit on the map and what the auditor's engagement charter must prohibit to defend that placement.
   - One recurring boundary case you anticipate (from chapter 3 or your own identification) and how you would resolve it in the engagement letter.
   - One case where the second-line / third-line boundary is genuinely ambiguous in this organisation, and your proposed resolution.
   - At least two **citations** per argument: one to the IIA Three Lines Model principles, one to the 2024 Global Internal Audit Standards.

## Starter guidance

- Begin by listing every AI artifact in scope on the right side of a sheet and every internal function on the left side; then draw the three-lines boundary across the middle.
- The AI Governance Committee is deliberately ambiguous in this scenario; part of the exercise is defending its placement — do not simply assert it is second line, argue for it.
- For the External Auditor, be specific: the financial-statement audit team is outside the three lines, but the IT-audit sub-team of that engagement may interact with internal audit's work on AI — note the interaction without placing the external auditor *inside* the three lines.
- Keep the diagram readable. Favour clarity over density; three AI systems, ~8 internal functions, 3 external parties is the scope — do not add more.
- Cite the specific IIA Three Lines Model principle numbers (1-6) and specific 2024 Standards Domain / Principle numbers when making the arguments.

## Acceptance criteria

The deliverables are accepted when:

- Every AI artifact listed in the scenario appears on the diagram with accountability clearly assigned to one line.
- The diagram distinguishes governing body, management (split into first line + second line), third line (internal audit), and external assurance providers.
- The memo defends the AI Auditor's placement with at least two explicit IIA citations.
- The memo names at least one recurring boundary case and resolves it with a specific engagement-letter clause (quoted or paraphrased).
- The memo names at least one genuinely ambiguous case and argues the resolution rather than asserting it.
- Vocabulary follows the 2020 Three Lines Model (not the 2013 Three Lines of Defense). "Defense" is not used except historically.
- No regulatory standard is invented or misnamed.

## Stretch goals

- Add a **cross-tag column** to the diagram tying each internal function to the specific IIA 2024 Standards Domain whose requirements primarily bind it (e.g., AI Auditor → Domain V Performing Internal Audit Services; CAE / Audit Committee → Domain III Governing the Internal Audit Function).
- Produce a **second diagram** showing how the same organisation's three-lines map changes during the ISO/IEC 42001 certification audit — which external parties become relevant and where they sit.
- Produce a **third diagram** showing how the same map would look at a Big-4 firm performing an AT-C 205 examination over NorthernMutual's AI safety program — who is responsible party, who is engaging party, who are intended users (per AT-C 105 three-party relationship).
