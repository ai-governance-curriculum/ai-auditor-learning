# What Makes a Criterion *Auditable* — Framework Clause to Testable Statement

## Motivation

The reader of your audit report is not looking at a framework. They are looking at a conclusion. The conclusion says *the subject matter conforms (or does not) to the criteria*. If the criteria you tested against were vague, overlapping, or impossible to evidence, the report cannot be defended — not under IAASB **ISAE 3000 (Revised)** paragraph 24 ("suitable criteria"), not under AICPA **AT-C 105** paragraph .25, not under **ISO/IEC 17021-1** clause 9.4. Every framework the AI Auditor is handed (ISO/IEC 42001, NIST AI RMF, EU AI Act, SR 11-7, HIPAA, Colorado AI Act) is a *source of criteria*, not a set of criteria. The auditor's first act of professional judgment is to translate framework clauses into **auditable criteria** — statements a procedure can be written against and an evidence artifact can satisfy. This chapter installs the translation discipline that the rest of the module uses on every framework in scope.

## The five suitability tests, from the assurance framework

The IAASB **International Framework for Assurance Engagements** paragraph 44 and AT-C 105 paragraph .25 both require criteria to be:

1. **Relevant** — the criterion contributes to a conclusion that is useful for the intended users' decision.
2. **Complete** — the criterion does not omit factors that affect the conclusion.
3. **Reliable** — the criterion allows reasonably consistent evaluation when used in similar circumstances by similarly qualified practitioners.
4. **Neutral** — the criterion is free from bias.
5. **Understandable** — the criterion is clear and not subject to significantly different interpretations.

A framework clause like **ISO/IEC 42001:2023 clause 6.1.2 "the organization shall establish and maintain AI risk assessment processes"** is relevant, but by itself it is not complete (what does "establish" require?), reliable (two auditors could score it differently), or understandable at the evidence level. The clause becomes an auditable criterion when it is restated with each of the five tests satisfied.

## The anatomy of an auditable criterion

Working template for every criterion in the module and the exercises:

```
Criterion ID:             <stable identifier, e.g., C-42001-6.1.2-01>
Source clause(s):         <framework + clause/article/control, with text or precise paraphrase>
Statement:                <testable assertion about the subject matter, present tense>
Evidence (expected):      <artifact(s) a procedure would collect: document, log, config, screenshot, interview memo, re-performance output>
Procedure (how tested):   <inquiry / observation / inspection / re-performance; sampling basis if applicable>
Measurable attributes:    <what the auditor records to score the criterion: pass/fail boolean, population size, exception count, tolerance>
Source hierarchy:         <per ISA 500 by analogy: external > internal + corroborated > internal > oral>
Owner (first/second line): <who owns the evidence inside the organisation>
Residual judgment:        <where professional skepticism still matters even if measurable attributes pass>
```

Two worked examples will anchor the rest of the module. The first is a *procedural* criterion drawn from ISO/IEC 42001; the second is a *measurable* criterion drawn from NIST AI RMF MEASURE. The pattern applies to every clause the module touches.

### Worked example 1 — ISO/IEC 42001:2023 clause 6.1.2 AI risk-assessment process

```
Criterion ID:             C-42001-6.1.2-01
Source clause:            ISO/IEC 42001:2023 clause 6.1.2 — "the organization shall establish and maintain a defined and documented AI risk assessment process".
Statement:                The organisation has a documented AI risk-assessment process that (a) is approved by a named accountable party, (b) names the inputs it consumes, (c) names the outputs it produces, (d) names the review cadence, and (e) has been executed at least once in the audit period producing current outputs traceable to AI systems in scope.
Evidence (expected):      Risk-assessment procedure document with version, approval signature, effective date; risk-assessment outputs (risk register entries) for each AI system in the Statement of Applicability; management review minutes showing output acceptance.
Procedure:                Inspect the procedure document; inspect sampled risk-assessment outputs (statistical sample from the population of AI systems in scope); inquire of the AIMS owner on the review cadence; corroborate with internal-audit workpapers under clause 9.2 if any.
Measurable attributes:    (a) procedure approved = yes/no; (b) inputs/outputs/cadence specified = yes/no; (c) number of AI systems with current outputs / total AI systems in scope.
Source hierarchy:         Procedure (internal); outputs (internal); management-review minutes (internal corroborated by board / audit-committee minutes if available).
Owner:                    Second line (risk or AI governance function), with first-line input to the risk register.
Residual judgment:        Even when (a)–(c) pass, the auditor exercises skepticism over whether the outputs are *used* (traceable into risk-treatment plan under 6.1.3) or shelfware.
```

The clause text was not written to be tested. The criterion statement is.

### Worked example 2 — NIST AI RMF MEASURE 2.3 (demographic performance assessment)

```
Criterion ID:             C-NIST-MEASURE-2.3-01
Source:                   NIST AI RMF 1.0 MEASURE 2.3 — "AI system performance or assurance criteria are measured qualitatively or quantitatively and demonstrated for conditions similar to deployment setting(s). Measures are documented."
Statement:                For each AI system in scope, performance metrics are measured and documented on an evaluation set that is (a) representative of the deployment population by named demographic / use-case segments, (b) refreshed within the organisation's documented cadence, and (c) accompanied by a documented acceptability threshold against which the metric is compared.
Evidence (expected):      Evaluation suite configuration file; evaluation run log with timestamp, model version, dataset version; metrics output; documented acceptability thresholds (e.g., in model card or release gate); demographic / segment slicing documentation; evaluation-set representativeness analysis.
Procedure:                Inspect suite config and run log; re-perform a sampled evaluation run if feasible under engagement scope (requires auditor's-expert support under ISA 620); compare measured value to documented threshold; trace threshold back to a policy source.
Measurable attributes:    (a) demographic segments defined = yes/no; (b) segments cover expected deployment population per the impact assessment = yes/no; (c) measured vs. threshold deltas per segment; (d) age of most recent evaluation run vs. documented cadence.
Source hierarchy:         Evaluation run log + metrics output (internal corroborated by re-performance); representativeness analysis (internal).
Owner:                    Second line (eval / release-assurance) with first-line (model team) producing metrics.
Residual judgment:        Auditor retains professional skepticism over whether the demographic segments chosen actually reflect the deployment population or were chosen to pass; cross-check with the AI system impact assessment (ISO/IEC 42005) and any user-population research.
```

Note the **auditor's expert** footprint in Example 2: the re-performance step requires ML-evaluation expertise the audit team may not hold. The criterion anticipates this at translation time, not after fieldwork starts.

## Procedural criteria vs. measurable criteria

Most AI audit criteria fall into one of two shapes:

- **Procedural criteria** — the organisation has a defined, documented, executed process (ISO/IEC 42001 clauses 4–10 are overwhelmingly procedural). Evidence is document plus execution trace. Testing is inspection plus walkthrough plus sampled re-performance.
- **Measurable criteria** — the AI system exhibits a quantified property on a defined population within tolerance (fairness deltas, accuracy, robustness to adversarial perturbation, calibration error, latency, availability). Evidence is metric plus method plus dataset. Testing is inspection plus re-performance (often with auditor's expert).

A single framework clause frequently decomposes into *both* — the ISO/IEC 42001 Annex A controls, NIST AI RMF MEASURE categories, EU AI Act Article 15 ("accuracy, robustness, cybersecurity") all couple a procedural obligation ("the organisation shall establish a process to measure X") with a measurable obligation ("X meets the organisation's stated performance level"). Both halves must be translated.

## The "source hierarchy" layer, from ISA 500 by analogy

**ISA 500 — Audit Evidence** ranks evidence by reliability. For AI subject matter, the practical hierarchy is:

1. **External, independently obtained** — a third-party ISO/IEC 42001 certificate, an ISAE 3000 service-organisation report issued by another firm, a regulator's inspection report. Highest reliability if independence of the issuer can be confirmed.
2. **Internal evidence corroborated by an external source** — the organisation's model card plus auditor re-performance of its headline metric on the auditor's or the organisation's held-out dataset.
3. **Internal evidence generated by the control the auditor is testing** — the organisation's risk register, model-inventory extract, incident ticket.
4. **Management inquiry, uncorroborated** — lowest reliability; must be corroborated by (1)–(3) before it supports a conclusion.

Each criterion names the source type expected. A criterion whose only evidence is a management interview is suitable for planning purposes but will not support a reasonable-assurance conclusion.

## Measurability, materiality, and tolerance — the ISA 320 analogue

AI criteria frequently carry a metric with a stated tolerance ("within 5% demographic parity", "accuracy ≥ 92%"). The tolerance is the audit **materiality threshold** for that criterion. Treat it with the discipline of **ISA 320** materiality:

- The materiality threshold is set at planning, documented, and used consistently.
- Deltas smaller than the threshold are *inconsequential* and reported (if at all) as observations, not findings.
- Deltas at or above the threshold are *findings*; aggregation of smaller deltas into a material-in-aggregate finding is still possible.
- The threshold is reviewed if information obtained during the engagement suggests it was set wrongly.

The common failure mode: adopting a tolerance the organisation set for itself without professional challenge. The criterion is only suitable if the tolerance is defensible for the *intended users* of the report, not for the organisation's internal risk appetite alone.

## Criteria-authoring heuristics that keep you out of trouble

- **One assertion per criterion.** Compound statements ("the organisation has a process that is documented and reviewed quarterly and includes stakeholder input") produce split-finding ambiguity; break them into three.
- **No verbs the organisation can define on its own.** "Adequate", "effective", "appropriate" without a defined measurable attribute are not auditable; replace with observable conditions.
- **Evidence named before procedure.** If you cannot name the evidence artifact, the criterion is not yet testable.
- **Owner named.** A criterion with no first-line or second-line owner creates an orphan evidence request at fieldwork; name the owner at translation time.
- **Judgment preserved.** A measurable criterion that passes mechanically still needs a skepticism paragraph. Record where it belongs.
- **Period framing.** Every criterion is scoped to a period (point-in-time or period-of-coverage). ISAE 3000 reports require this explicitly; AT-C 205 reports do too.

## The role split, loud and in writing

This module repeatedly refers to three adjacent roles. Keep them straight:

- The **`ai-governance-analyst` (level 15)** does the analyst-tier legwork this role consumes — raw crosswalk tables from the issuing body's publications, stakeholder lists, inventory scaffolding. The AI Auditor is a *buyer*, not an author, of that analyst output. If you are producing it from scratch inside the engagement, the engagement scope and fee are wrong.
- The **`senior-ai-governance-architect` (level 50)** *designs the control library* the AI Auditor audits against. The architect's artifact (enterprise control taxonomy, policy-to-control-to-evidence mapping, exception register) is the second-line subject matter the auditor opines on — not something the auditor authors.
- The **AI Auditor (this role, level 45)** translates *external framework clauses* into *auditable criteria* that can be tested against *the organisation's internal control library*. The criterion lives at the junction of the two. Where the architect's control library is immature, the auditor still has to audit against the framework; in that case the audit finding is often that the control library itself does not yet support the framework obligation.

## Summary

- Suitable criteria under ISAE 3000 / AT-C 105 must be relevant, complete, reliable, neutral, understandable. Framework clauses are not criteria until translated to that standard.
- The auditable-criterion template (ID, source, statement, evidence, procedure, measurable attributes, source hierarchy, owner, residual judgment, period) is the unit of work for the rest of this module.
- Most criteria are either procedural (document + execution trace) or measurable (metric + method + dataset); many framework clauses decompose into both.
- Evidence reliability follows the ISA 500 hierarchy; uncorroborated inquiry supports planning, not a reasonable-assurance conclusion.
- Tolerances on measurable criteria are the audit materiality thresholds under ISA 320 analogy; adopt them consciously, not because the organisation did.
- The auditor translates *external frameworks* into *testable criteria* and consumes the analyst-tier and architect-tier work of adjacent roles — never co-authors what they are about to audit.
