# exercise-03: ISAE 3000 and AT-C 105 / AT-C 205 — Attestation Engagement Shape

**Estimated effort:** 2.5 hours

## Objective

Produce a draft engagement letter and a planning memo for an AI attestation engagement, executed under either ISAE 3000 (Revised) or AT-C 105 + AT-C 205. The deliverable is specific enough to be read by an engagement-quality-review partner — not a sketch.

## Prerequisites

- Chapter [`05-iaasb-and-aicpa-attestation-stack.md`](../05-iaasb-and-aicpa-attestation-stack.md)
- Chapter [`08-independence-and-ethics-posture.md`](../08-independence-and-ethics-posture.md)
- Read-access to:
  - IAASB International Framework for Assurance Engagements
  - ISAE 3000 (Revised)
  - Supporting ISAs 500, 530, 620, 320 (headline reading, not full)
  - AICPA AT-C 105 (Concepts Common to All Attestation Engagements)
  - AICPA AT-C 205 (Assertion-Based Examination Engagements)
  - IESBA International Code of Ethics (independence sections, headline)

## Scenario (pick one; write the deliverables for the one you pick)

### Scenario A — ISAE 3000 (international firm, EU subject matter)

A European-headquartered foundation-model company (**AegisAI GmbH**) engages your firm to issue a **reasonable-assurance report** under ISAE 3000 on management's assertion that during the period 1 Jul – 31 Dec 2026, AegisAI operated its model-safety program for the flagship Aegis-Large model in accordance with its documented control framework (which management has crosswalked to the NIST AI RMF 1.0 GenAI Profile and the GPAI Code of Practice signatory obligations the company has adopted).

Intended users: AegisAI's enterprise deployer customers (named in the engagement letter), the EU AI Office (upon request), and the AegisAI Board.

### Scenario B — AT-C 205 (US firm, US subject matter)

A US-headquartered health-tech SaaS company (**CareNet Analytics Inc.**) engages your firm to issue an **examination report** under AT-C 205 on management's assertion that during the period 1 Jan – 31 Dec 2026, CareNet operated its ML model-governance program (including model inventory, model validation, change management, monitoring, incident response) for its three FDA-cleared AI/ML SaMD products in accordance with CareNet's documented control framework (which management has crosswalked to FDA GMLP and 21 CFR 820).

Intended users: CareNet's hospital-system customers (named in the engagement letter) and the Audit Committee.

## Deliverables

### 1. Draft engagement letter (~3 pages)

Include at a minimum:

- Framework declaration (ISAE 3000 or AT-C 105 + AT-C 205).
- Three-party relationship: **responsible party**, **engaging party**, **intended users** (named per scenario).
- Underlying subject matter and subject-matter assertion (verbatim or close to it).
- Criteria (name the crosswalk — NIST AI RMF 1.0 GenAI Profile + GPAI CoP for A; FDA GMLP + 21 CFR 820 for B) and the assertion that criteria are suitable (relevant, complete, reliable, neutral, understandable).
- Level of assurance (reasonable or limited) and the corresponding report-conclusion language.
- Period of coverage.
- Division of responsibilities between management and auditor.
- Access to records, personnel, systems, logs.
- Use of auditor's experts under ISA 620 (A) or AT-C 105 (B) — scope, not names.
- Fees and billing (placeholder figures acceptable; structure must not be contingent on outcome).
- Independence confirmation and ethics-framework commitment (IESBA for A, AICPA Code for B).
- Reporting timeline and deliverable format.

### 2. Planning memo (~1,500 words)

Cover:

- **Risk assessment** — what types of misstatement could occur in the subject matter (think: overstated control operation, understated incident rate, undetected model drift, inconsistent evaluation methodology), and the risk of material misstatement for each.
- **Materiality for the subject matter** — qualitative framing (because this is non-financial), with explicit statement of what magnitude or nature of misstatement would affect user decisions, and the resulting performance-materiality threshold for engagement execution.
- **Overall engagement strategy** — scope of control operation testing (full period, dual purpose, sampling), the specific AI artifacts the team will inspect (logs, eval runs, incident tickets, model inventory records, monitoring configurations).
- **Sampling plan** at a high level (ISA 530 or analogous) — populations, selection method, planned sample size rationale.
- **Auditor's expert (ISA 620) scoping** — the type of expertise required (ML-engineering, red-team methodology, statistical calibration, privacy engineering — name what fits the scenario), scope boundary, review protocol, independence check.
- **Independence-and-ethics posture** — map the five threats (self-interest, self-review, advocacy, familiarity, intimidation) to this engagement's facts, note safeguards, name residual threats and basis for acceptance.
- **Written representations** the engagement will require from management at completion (per ISAE 3000 / AT-C 105).
- **Report-conclusion language** — a draft paragraph of the positive-assurance conclusion exactly as it would appear in the final report.

## Starter guidance

- Treat the engagement letter as a legal document; defensive phrasing matters. Where ISAE 3000 / AT-C 105 prescribes specific wording (the conclusion paragraph in particular), use the prescribed wording.
- The criteria crosswalk is a planning risk — if management cannot explain which control objective maps to which NIST AI RMF function or which FDA GMLP principle, your engagement cannot proceed without re-work. Call it out in the memo.
- For scenario A, the EU AI Act interaction is deliberately out of scope for the attestation itself (this is not an Article 43 conformity assessment) but intended users include the EU AI Office upon request — that shapes the independence considerations and the written representations.
- For scenario B, FDA GMLP guidance was drafted jointly with Health Canada and the UK MHRA; be careful about citing a specific version and date.
- Do NOT invent ISAE or AT-C clause numbers. Where you need to cite, cite accurately or mark `<!-- needs-research: cite exact clause of ISAE 3000.A45 at reading time -->` rather than guessing.

## Acceptance criteria

The deliverables are accepted when:

- The engagement letter correctly identifies the framework, three-party relationship, subject matter, criteria, level of assurance, period, and auditor/management responsibilities.
- The planning memo covers all eight bullets above, each with specific scenario-grounded detail.
- Report-conclusion language follows the prescribed shape for the chosen framework and level of assurance (positive vs. negative).
- Independence-posture mapping evaluates all five threats, not just the ones that happen to be nil in this scenario.
- Auditor's expert scoping names a specific type of expertise and defends it under ISA 620 / AT-C 105 reliance rules.
- No clause of a standard is invented; unverified citations are marked with `needs-research` rather than fabricated.
- Fee structure is non-contingent; any proposed structure is defensible under the framework's independence rules.

## Stretch goals

- Author a **second engagement letter** for the *other* scenario (if you did A, do B as a stretch), noting the three largest differences between the two.
- Produce a **report-shape matrix** comparing: ISAE 3000 reasonable assurance vs. ISAE 3000 limited assurance vs. AT-C 205 examination vs. AT-C 210 review vs. AT-C 215 AUP — showing for each the conclusion language, documentation requirement, and typical AI-engagement use case.
- Draft a **scoping objection letter** from the responsible party pushing back on one aspect of the engagement (criteria suitability, scope boundary, timing) and your response as engagement lead — in a shape the engagement-quality-review partner would accept.
