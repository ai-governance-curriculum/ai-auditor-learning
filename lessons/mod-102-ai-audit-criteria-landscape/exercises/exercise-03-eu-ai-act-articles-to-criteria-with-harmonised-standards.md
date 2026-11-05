# exercise-03: EU AI Act Articles to Criteria, with Harmonised-Standard Alignment

**Estimated effort:** 3 hours

## Objective

Translate the EU AI Act (**Regulation (EU) 2024/1689**) provider obligations for a specified high-risk AI system into auditable criteria using the chapter-1 template, aligning each criterion to the **CEN/CENELEC JTC 21 harmonised standard** where one is cited in the Official Journal and to the **EU AI Office GPAI Code of Practice** where the system touches a general-purpose AI dependency. Deliverable is a criteria register that could support an EU AI Act Article 43 **readiness** engagement.

## Prerequisites

- Chapter [`01-what-makes-a-criterion-auditable.md`](../01-what-makes-a-criterion-auditable.md).
- Chapter [`04-eu-ai-act-articles-to-criteria.md`](../04-eu-ai-act-articles-to-criteria.md).
- **Regulation (EU) 2024/1689** (EUR-Lex official text) — read Articles 5, 6, 9, 10, 11, 12, 13, 14, 15, 16, 17, 26, 27, 43, 47, 50, 71, 72, 73 at minimum.
- The current list of **CEN/CENELEC JTC 21 harmonised standards** cited in the OJ — confirm at reading time.
- The current **EU AI Office GPAI Code of Practice** — confirm at reading time.

## Scenario

**Vermeer-Rheno GmbH** is a fictitious Netherlands-headquartered AI *provider* that develops **RheinoResume**, an AI-driven candidate-screening system used by EU and UK employers to rank CVs for shortlisting. The system:

- Falls within **Annex III, point 4(a)** (AI systems intended to be used for the recruitment or selection of natural persons) — therefore **high-risk** under Article 6(2).
- Uses an **in-house fine-tuned open-weights foundation model** (so Title V GPAI-provider obligations touch upstream, but Vermeer-Rheno is also a GPAI *downstream integrator*, not a GPAI provider).
- Has been deployed in EU production since January 2025; your engagement window is a **readiness audit** before the Act's high-risk-system provisions fully apply.

You are an **external readiness practitioner** engaged by Vermeer-Rheno under an **ISAE 3000 (Limited Assurance)** engagement letter, delivering a written report that management will use to drive remediation before any notified-body conformity assessment. The report will not be publicly distributed; its intended user is Vermeer-Rheno's AI Compliance Steering Committee, with the Dutch AP as an observer.

## Deliverables

1. **Criteria register** — chapter-1 template, covering:
   - **Scoping** (Articles 2, 3, 6, 50): at least one criterion on the AI-system classification trace.
   - **Article 9** risk-management system: at least two criteria (one procedural, one on continuous operation).
   - **Article 10** data and data governance: at least three criteria (relevance/representativeness, bias examination, special-category-data safeguards).
   - **Article 11 + Annex IV** technical documentation: at least two criteria (presence of every Annex IV point; freshness with life-cycle change).
   - **Article 12** record-keeping: at least one criterion.
   - **Article 13** transparency to deployers: at least two criteria.
   - **Article 14** human oversight: at least two criteria.
   - **Article 15** accuracy / robustness / cybersecurity: at least four criteria (one each for the three characteristics, plus one on the declared level under Article 15(2)).
   - **Article 17** quality management system: at least one criterion.
   - **Article 26 / 27** deployer obligations + FRIA cross-reference: at least one criterion (the provider's duty to furnish deployer with information enabling FRIA).
   - **Article 43 + 47 + 48 + 71** conformity assessment, declaration, CE marking, EU-database registration: at least two criteria.
   - **Article 50** transparency to natural persons (candidates): at least one criterion.
   - **Articles 72, 73** post-market monitoring and serious-incident reporting: at least two criteria.
   - **GPAI dependency note**: at least one criterion covering Vermeer-Rheno's obligation to know its upstream GPAI model's compliance posture (Article 53 information-to-downstream-provider trace).
2. **Harmonised-standards alignment column**. For each criterion, cite the applicable CEN/CENELEC JTC 21 harmonised standard if cited in the OJ, mark `pending` if not yet cited, and mark `n/a` for criteria where no harmonised standard is contemplated.
3. **Limited-assurance report-form sketch** (~300 words). Draft the conclusion paragraph in the negative-assurance language required by ISAE 3000 for limited-assurance engagements, naming the criteria and the limitations.
4. **Posture memo** (~500 words) covering:
   - Whether Vermeer-Rheno's Annex III classification is defensible under its current deployment.
   - What Article 43 route the provider will follow (Annex VI internal control vs. Annex VII notified-body) and why.
   - Where the harmonised-standards pipeline would materially simplify the criteria set once published.

## Minimum volume

- At least **22 criteria** across the Act (do not spread thinner than that).
- At least **6 measurable** criteria carrying metric + method + population + tolerance explicitly.
- At least **3 criteria** that would require an auditor's expert under ISA 620 analogy (flag expert scope).
- Scoping, Article 15, and Articles 72/73 must each carry at least one measurable criterion.

## Starter guidance

- Start from scoping — if Vermeer-Rheno's Annex III classification is wrong, every downstream criterion is misdirected. Make the scoping criterion explicit even though it's Vermeer-Rheno's analyst (L15) who authored the raw classification.
- Article 10(5) special-category-data safeguards are *the* trap for CV-screening: bias testing often needs protected-attribute inference. Author a criterion that can detect the "we inferred gender/ethnicity for bias testing with no 10(5) safeguard" finding.
- Article 15(2)'s *declared* levels of accuracy, robustness, cybersecurity are a named-value commitment in the instructions for use. The criterion ties the *declaration* to the *measured value* within tolerance. Watch out for "we declared ≥85% and measured 82%".
- Article 72 post-market monitoring + Article 73 serious-incident reporting overlap NIST MANAGE 4.1 and ISO/IEC 42001 clauses 9.1 + 10.1. Write the criterion so one piece of evidence satisfies all three — flag it for the crosswalk exercise (exercise 05).
- The harmonised-standards column requires freshness. Any cell citing a standard that is not yet cited in the OJ at reading time must be marked `pending` with a `<!-- needs-research: ... -->` tag.
- For the limited-assurance report sketch, do not use positive-assurance language. The ISAE 3000 negative-form ("nothing has come to our attention that causes us to believe...") is mandatory for limited assurance.

## Acceptance criteria

The deliverables are accepted when:

- The criteria register uses the full chapter-1 template with the harmonised-standards column added; no field is blank.
- Volume thresholds (22 criteria, 6 measurable, 3 expert-dependent) are met.
- Every criterion cites a specific Article and paragraph (e.g., Article 15(4), not "Article 15").
- Scoping, Article 10(5), Article 15(2) declared levels, and Articles 72/73 all carry at least one criterion each.
- The GPAI-dependency criterion is present and cites Article 53 information-to-downstream-provider.
- The posture memo answers all three required questions with reasoned citation.
- The report-form sketch uses ISAE 3000 limited-assurance (negative-form) conclusion language; no positive-assurance verbs.
- Harmonised-standards cells are either cited with OJ reference, marked `pending`, or marked `n/a` — no silent blanks.
- No Article number, Annex point, or standard reference is invented or misnamed; where uncertain, mark `<!-- needs-research: ... -->`.

## Stretch goals

- Add a **deployer-overlay section** — for one named EU deployer (fictional) that uses RheinoResume, author at least five Article 26 deployer-obligation criteria.
- Author the **fundamental-rights impact assessment (FRIA)** criterion set under Article 27 that the deployer would use, and map it to the provider's Article 13 information obligations.
- Produce a **gap-remediation plan skeleton** — for each expected gap in a 2026 readiness audit, name the remediation owner (L15 analyst, L25 engineer, L35 release assurance, L50 architect, legal, regulatory affairs).
- Draft a **notified-body-engagement-readiness checklist** showing which criteria would move from internal assessment to notified-body evidence if Vermeer-Rheno's product ever shifted to an Annex VII conformity route.
