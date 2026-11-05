# Materiality for AI Audit — ISA 320 / AU-C 320 Translated into the AI Setting

## Motivation

Materiality is the auditor's single most load-bearing scoping judgment. It determines what counts as a finding, what counts as an observation, what gets aggregated, what gets reported, and what gets left out. **ISA 320 — Materiality in Planning and Performing an Audit** (IAASB) and **AU-C 320 — Materiality in Planning and Performing an Audit** (AICPA, mirror standard) were written for financial-statement audits, but the materiality discipline carries across directly to attestation engagements under **ISAE 3000 (Revised)** / **AT-C 105** and to AIMS audits under **ISO 19011:2018** clause 6 and **ISO/IEC 17021-1** clause 9. Every regime the AI Auditor operates in expects materiality to be set, documented, and applied consistently.

For AI the harder question is what *quantity* materiality is measured in. Financial audit answers in money. AI audit answers in a layered set: money, affected population, decision volume, regulatory classification, safety outcomes, and public trust. Different engagement types weigh those layers differently. This chapter installs the discipline and tunes it for the four engagement types the AI Auditor runs.

## The three materiality concepts from ISA 320, restated

ISA 320 / AU-C 320 distinguishes:

- **Overall materiality** — the magnitude of a misstatement (or in attestation: a deviation of the subject matter from the criteria) that could reasonably be expected to influence the decisions of intended users.
- **Performance materiality** — a lower amount than overall materiality, set so that the *aggregate* of uncorrected and undetected deviations does not exceed overall materiality. Performance materiality absorbs sampling risk and the aggregation risk of multiple small deviations.
- **Specific materiality for particular classes of transactions, balances, or disclosures** — a separate threshold for items whose misstatement at a *smaller* amount than overall materiality would still influence user decisions (a qualitatively material disclosure, for instance).

All three apply to AI audit. The ISA 320 translation is:

- **Overall materiality** of an AI audit: the magnitude of criteria deviation that would change the intended user's decision about the AI system (or AIMS).
- **Performance materiality** of an AI audit: a lower threshold for individual criterion deviations, so that aggregation does not push total deviation past overall materiality.
- **Specific materiality** for particular criteria: a tighter threshold where the AI subject matter has a qualitatively material flavour — regulatory classification, safety-critical operation, fairness over a protected class, children's data, incident reporting.

## Quantitative materiality for AI — three primary bases

Financial audit has a stable base (profit before tax, revenue, net assets). AI audit has three primary bases, used alone or in combination depending on engagement:

### Base A — Financial impact

The traditional ISA 320 base, applied to the AI audit's financial context:

- Direct financial impact of the AI system's decisions (approved-loan value, insurance-claim value, procurement value, revenue attributed to recommendations).
- Regulatory-penalty exposure — EU AI Act Article 99 fines (up to 7% of global turnover for prohibited practices, up to 3% for high-risk non-compliance), GDPR Article 83 fines, Colorado AI Act penalties, NYC LL144 civil penalties.
- Litigation exposure — class-action potential in jurisdictions with private rights of action under anti-discrimination, consumer-protection, or AI-specific statutes.

Percent-of-base anchors from ISA 320 practice (0.5–1% of revenue; 5–10% of profit before tax) survive as *starting* anchors in financial-flavoured AI engagements, but should rarely be adopted unchallenged in AI work.

### Base B — Affected-population size

For AI audit, the scale of individuals affected by the system's decisions is a first-class materiality base:

- Number of distinct individuals impacted by the system in the audit period.
- Number of individuals in a protected class or vulnerable segment impacted.
- Reversibility of impact per individual (one-time vs. recurring; appeal-available vs. terminal).

A system that affects 50,000 people's hiring outcomes is materially different from a system that affects 5 people's hiring outcomes, even at the same dollar magnitude. Percent-of-base anchors are harder to standardise here — the organisation's own risk appetite and the regulatory classification drive the thresholds. A tight anchor used in practice: any deviation that would adversely affect ≥ 1% of the affected population, or ≥ 100 individuals, whichever is smaller, is at least performance-material; each engagement sets its own defensible number in writing.

### Base C — Decision volume

The frequency and cumulative volume of the system's decisions:

- Decisions per unit time, cumulative over the audit period.
- Decisions per unit with high-impact flag (loan approval vs. loan rejection; claim pay-out vs. claim denial; appointment vs. non-appointment; alert-triggered vs. not; account-suspension vs. not).

Decision volume is the base that captures *scale of exposure* independent of dollar value — a fraud-detection model making 10,000 decisions per second has different materiality from a quarterly pricing model.

### Combining the bases

Most AI engagements use at least two of the three (financial + affected-population for lending, affected-population + decision-volume for content moderation, financial + decision-volume for recommendation systems). The engagement letter documents which bases are in play and the threshold on each. Specific materiality for individual criteria is set on the base most relevant to that criterion.

## Qualitative materiality for AI

ISA 320 paragraph A4 is explicit that qualitative factors can make a smaller-magnitude deviation material. For AI, the qualitative lenses with teeth in a modern engagement are:

- **Regulatory classification of the system** — EU AI Act prohibited / high-risk / systemic-risk GPAI, Colorado AI Act consequential decisions, NYC LL144 AEDT, FDA SaMD Class II/III, NAIC market-conduct-covered, SR 11-7 material-model.
- **Safety-critical operation** — autonomous driving, medical diagnosis / treatment selection, critical infrastructure, child protection.
- **Fundamental-rights exposure** — decisions on employment, housing, credit, education, insurance, benefits, criminal-justice intake.
- **Children's data or children as users** — COPPA, UK Age-Appropriate Design Code, EU DSA under-18 risk assessment.
- **Biometric data** — EU AI Act Annex III biometric categorisation, US state biometric laws.
- **Public-interest information** (misinformation / elections / health).
- **Prior incident at this organisation or at a peer** that elevates the criterion's visibility.
- **Regulator attention** (open inquiry, enforcement pattern).
- **Disclosure materiality** — whether the finding would need to appear in the organisation's regulatory disclosures regardless of its quantitative size.

A deviation that is quantitatively below overall materiality can still rise to material by one of these qualitative tests. The engagement workpaper names the qualitative lenses in play at planning time, not after fieldwork surfaces them.

## Performance materiality and tolerable misstatement for AI

Performance materiality is overall materiality reduced to absorb aggregation risk and sampling risk. ISA 320 paragraph A13 and AU-C 320 practice set performance materiality typically at 50–75% of overall materiality for first-time engagements, with wider latitude as auditor experience accumulates.

In AI audit the analogue is:

- **Performance materiality** — the per-criterion threshold below which a deviation is noted but not reported individually; aggregation across criteria is measured against overall materiality.
- **Tolerable misstatement** — the per-criterion threshold used to set *sample sizes*. For sampling-heavy AI audits (fairness evaluation across demographic slices, incident-handling sample across the period, access-review sample), tolerable misstatement drives ISA 530 statistical sampling calculations and the specialist's re-performance effort.

Worked example — a residual-risk audit of an underwriting AI with overall materiality set at "any deviation that would adversely affect ≥ 500 individuals in the audit period":

- Performance materiality (first-cycle) ≈ 60% × 500 = 300 individuals per criterion.
- Tolerable misstatement for a fairness-slice re-performance ≈ 5% absolute parity delta where the policy tolerance is set at 10%, giving sampling-planning headroom.
- Specific materiality for a criterion on children's-data handling: any single deviation is material regardless of individual count, by qualitative classification.

## Tuning materiality by engagement type

The four engagement types the AI Auditor operates in weigh the bases and the qualitative lenses differently. The table below is a tuning aid, not a rulebook.

### 1. ISO/IEC 42001 certification audit (certification body under 17021-1 + 42006)

- **Primary quantity**: conformity vs. non-conformity of the AIMS to ISO/IEC 42001 clauses 4–10 and the SoA. Materiality is operationalised through the **grading of non-conformities**: major (systemic failure or likely to result in significant failure of the AIMS) vs. minor (isolated, non-systemic).
- **Quantitative base**: AIMS is not scored on financial impact at all. Severity is scored on breadth (how many AI systems affected), depth (which clause), and systemic character.
- **Qualitative lens**: strong — any clause failure that threatens achievement of the AIMS policy or the organisation's stated objectives is a major non-conformity even if seemingly isolated. ISO 19011:2018 clause 6.4.8 and 17021-1 clause 9.4.9.1 shape the grading.
- **Performance materiality analogue**: the certification-body auditor may accumulate minor non-conformities and promote the aggregate to major if the pattern points to a systemic weakness.

### 2. EU AI Act Article 43–44 conformity assessment (notified body)

- **Primary quantity**: conformity to Annex III high-risk obligations and the harmonised standards under Article 40. Each Essential Requirement (Articles 9–15) is binary — conformity is established or it is not.
- **Quantitative base**: not financial. The notified body is not pricing risk, it is attesting conformity. The materiality decision is whether a residual deviation permits conformity to be declared with a corrective-action plan or refuses conformity.
- **Qualitative lens**: regulatory classification is the backdrop. For Annex III systems the standard is high throughout; for GPAI with systemic risk under Article 55 the standard is Article 55 obligations and the Code of Practice.
- **Specific materiality**: Articles 6–7 prohibited-practice drift is categorically material; any such finding voids conformity.

### 3. SOC-for-AI attestation (under SSAE 18 / AT-C 205 or ISAE 3000 Revised)

- **Primary quantity**: deviations from the described controls and trust services criteria (or AI-specific criteria) at the service organisation. The engagement team sets quantitative materiality on the service-user population exposure.
- **Quantitative base**: a blend of financial-impact (customer financial exposure to the service), affected-population (number of end users exposed through the service user), and decision volume (service-level request volume).
- **Qualitative lens**: strong on disclosure, since the report is a Type 2 attestation that service users rely on for their own compliance posture.
- **Performance materiality**: traditional 50–75% of overall, adapted to the AI domain; tolerable misstatement drives sample sizing for control operating effectiveness tests.

### 4. Internal risk-based audit (under IIA Standards 2024)

- **Primary quantity**: residual risk exposure relative to the organisation's risk appetite. The audit committee's risk-appetite statement (where it exists) is the baseline; where it does not, the engagement team proposes a threshold and gets audit-committee endorsement at the engagement acceptance stage.
- **Quantitative base**: all three — financial, affected-population, decision-volume — with weights chosen per engagement by subject matter.
- **Qualitative lens**: strong on management-response history, regulator attention, and incident history (from chapter 2 priority scoring), because the audit's intended user is the audit committee and the committee cares about *control environment* even where quantitative deviation is small.
- **Specific materiality**: low for any criterion that touches a known management-response weakness or a known regulator focus.

## The materiality workpaper the engagement letter cites

Every engagement produces a materiality workpaper the engagement letter references. The minimum elements:

- The engagement type and the standards being applied (ISO/IEC 17021-1 + 42001, ISAE 3000 Revised, AT-C 105 + AT-C 205, IIA Standards 2024, with sector overlays).
- The intended user(s) of the report and the decisions the report will inform.
- The quantitative bases chosen, the threshold on each, and the rationale.
- The qualitative lenses in play and the criteria they attach to.
- The performance materiality value and the tolerable misstatement values for sampling-heavy criteria.
- The specific materiality values (where set) and their rationale.
- The circumstances that would cause materiality to be re-assessed during the engagement and the escalation path for doing so.

The workpaper is signed by the engagement leader (external) or the lead auditor and the CAE (internal), and dated at planning. Changes during the engagement are recorded as revisions, not silent edits.

## Common failure modes

- **Adopting the organisation's own tolerance as materiality.** The organisation's internal risk-appetite threshold is an input, not the answer. Materiality must serve the intended user of the audit report, which is usually not the organisation.
- **Single-base thinking.** Using only financial-impact materiality on a system whose main exposure is affected-population scale or fundamental-rights exposure under-reports deviations with large real-world consequence.
- **No qualitative lens.** The planning workpaper is a quantitative table; the engagement surfaces a children's-data misclassification and the team has no framework for treating it as material.
- **Performance materiality skipped.** Only overall materiality is set, and the engagement reports every deviation at the overall threshold — aggregation goes unmeasured.
- **Materiality is re-written to fit the finding.** If the engagement loosens materiality post-hoc so a finding drops below threshold, the planning workpaper was wrong and the audit committee should be told.
- **No specific materiality for high-visibility criteria.** The engagement treats a bias-audit criterion the same as a routine documentation criterion; a small bias delta that is qualitatively material gets filed as an observation.

## Summary

- **ISA 320 / AU-C 320** materiality translates directly into AI audit: overall materiality, performance materiality, specific materiality for qualitatively material items.
- AI quantitative materiality uses **three primary bases** — financial impact, affected-population size, decision volume — alone or in combination.
- Qualitative materiality for AI is anchored on regulatory classification, safety criticality, fundamental-rights exposure, children's data, biometrics, incident history, regulator attention, and disclosure visibility.
- Materiality is tuned by engagement type — ISO/IEC 42001 certification audits grade non-conformities; EU AI Act conformity assessment attests binary conformity; SOC-for-AI uses blended quantitative + qualitative with SSAE 18 / ISAE 3000 discipline; internal risk-based audit anchors on residual risk vs. audit-committee risk appetite.
- Every engagement produces a signed, dated materiality workpaper the engagement letter cites; changes during the engagement are recorded, not silently absorbed.
- The common failure modes — single-base thinking, missing qualitative lens, skipped performance materiality, post-hoc re-writing — are each a credibility hit the audit committee will notice.
