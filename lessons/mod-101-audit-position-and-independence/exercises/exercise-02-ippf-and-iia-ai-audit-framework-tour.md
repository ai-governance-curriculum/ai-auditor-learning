# exercise-02: Guided Tour — 2024 IIA Standards, IPPF Legacy, and the AI Auditing Framework

**Estimated effort:** 2.5 hours

## Objective

Produce a reference crosswalk that lets you (and any teammate) navigate between the 2017 IPPF structure and the 2024 Global Internal Audit Standards while executing an AI audit grounded in the IIA AI Auditing Framework. The deliverable is a Markdown crosswalk file plus a short defensive-citation handbook you will keep on your desk.

## Prerequisites

- Chapter [`02-iia-three-lines-model-and-ippf.md`](../02-iia-three-lines-model-and-ippf.md)
- Chapter [`03-iia-ai-auditing-framework.md`](../03-iia-ai-auditing-framework.md)
- Read-access to:
  - IIA Global Internal Audit Standards (2024, effective 9 January 2025)
  - IIA IPPF structure (Core Principles, Definition, Code of Ethics, Standards — 2017 structure, the one in force through 2024)
  - IIA Artificial Intelligence Auditing Framework (three parts)
  - IIA guidance on Internal Audit's Role in Governance of AI (cite the version available at your reading time)

## Deliverables

### 1. Crosswalk table (Markdown, in your workbook)

A table with the following columns:

| 2017 IPPF element | 2024 Standards location | Change from 2017 | Working implication for an AI audit |
|---|---|---|---|

Populate it with **at least 12 rows**, covering at a minimum:

- Attribute Standard 1000 (Purpose, Authority, Responsibility) → 2024 Standards location
- Attribute Standard 1100 (Independence and Objectivity) → 2024 Standards location
- Attribute Standard 1200 (Proficiency and Due Professional Care) → 2024 Standards location
- Attribute Standard 1300 (Quality Assurance and Improvement Program) → 2024 Standards location
- Performance Standard 2000 (Managing the Internal Audit Activity) → 2024 Standards location
- Performance Standard 2100 (Nature of Work) → 2024 Standards location
- Performance Standard 2200 (Engagement Planning) → 2024 Standards location
- Performance Standard 2300 (Performing the Engagement) → 2024 Standards location
- Performance Standard 2400 (Communicating Results) → 2024 Standards location
- Performance Standard 2500 (Monitoring Progress) → 2024 Standards location
- Code of Ethics (Integrity, Objectivity, Confidentiality, Competency) → 2024 Standards location
- Mandatory Topical Requirement (if issued) — note the mapping

For each row the "working implication for an AI audit" cell should be one short sentence of how that Standard concretely binds an AI engagement (e.g., for 2300, "this is the source of authority to re-run eval metrics as evidence rather than relying on the model team's reported numbers").

### 2. AI Auditing Framework coverage matrix (Markdown, in your workbook)

A table mapping the **AI Auditing Framework Part II risk categories** (strategic, cyber, data quality / data governance, black-box / explainability, ethical, legal/regulatory, performance measurement, human factors) to:

- the module in this track (`mod-102` through `mod-112`) that primarily covers the risk, and
- at least one specific 2024 Standards Principle or Requirement the auditor cites when scoping the risk in an engagement, and
- at least one external criteria reference (ISO/IEC 42001 clause, NIST AI RMF function, EU AI Act article) you anticipate testing against the risk.

### 3. Defensive-citation handbook (Markdown, one page)

A one-page cheat-sheet listing **five likely management pushbacks** on AI audit findings (your choice of specific pushbacks — draw from your reading or author plausible ones) and for each: the Standard citation, the AI Auditing Framework risk category, and the one-sentence response you would deliver verbally in the closing meeting.

## Starter guidance

- The 2024 Standards are organised around Domains (I-V) and Principles; the 2017 IPPF used Standards numbered 1000-2600. There is no 1-to-1 numbering; your crosswalk has to describe the relationship (consolidated into, split across, retitled, folded in).
- When you cannot find an exact 2024 analogue for a 2017 element, record "folded into the Ethics and Professionalism Domain" or similar — this is a defensible crosswalk entry.
- The AI Auditing Framework was authored before the 2024 Standards; your handbook has to bridge the two.
- Do NOT invent Standard numbers or Framework risk categories; stop and verify against the source documents. Where a document is behind an IIA members-only wall, note the citation and the access route rather than fabricating detail.
- If Topical Requirements for AI are available at your reading time, cite them; if not, note their absence as a known gap.

## Acceptance criteria

The deliverables are accepted when:

- The crosswalk has at least 12 rows, each with a concrete 2024 Standards location (not just "somewhere in Domain IV").
- The crosswalk's "Change from 2017" column distinguishes consolidation, retitling, folding-in, and new-in-2024 explicitly.
- The AI Auditing Framework matrix covers all eight Part II risk categories.
- Each matrix row has a cited 2024 Standards reference and a cited external criteria reference.
- The defensive-citation handbook contains five distinct scenarios, each with Standard + Framework + response.
- No Standard number, Domain / Principle number, or Framework risk category is fabricated — all are traceable to the source documents.

## Stretch goals

- Add a **3rd axis** to the AI Auditing Framework matrix: for each risk category, cite the one specific **ISACA Auditing AI** control area that complements the IIA frame (see chapter 4).
- Produce a **2-column summary** for a CAE: "if you remember 10 things from the 2024 Standards for AI audit, remember these 10," ranked.
- Draft a **Topical Requirement mock-up** for AI — if the IIA has not yet published one at your reading time, draft a one-page proposal: scope, mandatory audit coverage, out-of-scope boundaries. Write it as the IIA would.
