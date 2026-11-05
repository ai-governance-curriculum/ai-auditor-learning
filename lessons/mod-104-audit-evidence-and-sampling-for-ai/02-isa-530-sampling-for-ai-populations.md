# ISA 530 / AU-C 530 Sampling, Applied to AI Populations

## Motivation

AI auditors meet populations too large to test in full nearly every engagement: a trace store with 400 million inference records, a change log with 900 model-config updates in the period, a red-team catalog with 12,000 adversarial prompts, a training-data register with 60 million labelled rows. **ISA 530 — Audit Sampling** (IAASB) and **AU-C 530 — Audit Sampling** (AICPA) define the discipline that lets the auditor conclude on the population from a sample: how to pick the sample, how many to pick, what counts as a deviation, how to project deviations back to the population, and how to defend the conclusion when the sample is small.

The goal of this chapter is to install sampling methodology that would survive engagement-quality review and PCAOB-style inspection *while* respecting the shape of AI populations — populations that are not uniformly random, that have heavy tails, that drift over the audit period, and that an ML-literate specialist (chapter 3) is often the one who defines the stratification.

## The ISA 530 definitions the chapter uses

- **Audit sampling** — the application of audit procedures to less than 100% of items within a population of audit relevance such that all sampling units have a chance of selection, in order to provide the auditor with a reasonable basis on which to draw conclusions about the entire population.
- **Population** — the entire set of data from which a sample is selected and about which the auditor wishes to draw conclusions.
- **Sampling risk** — the risk that the auditor's conclusion based on a sample may be different from the conclusion if the entire population were subjected to the same audit procedure.
- **Tolerable rate of deviation** — a rate of deviation from a prescribed control set by the auditor in respect of which the auditor seeks to obtain an appropriate level of assurance that the actual rate is not exceeded.
- **Tolerable misstatement** — a monetary amount set by the auditor in respect of which the auditor seeks to obtain an appropriate level of assurance that the actual misstatement is not greater than that amount. For AI, the analogue is a *tolerable rate of deviation* on an attribute (e.g., "no more than 1% of change tickets lack approving-authority evidence") or a *tolerable difference* on a measurement (e.g., "measured fairness gap within 1 percentage point of claimed").
- **Statistical sampling** — an approach that uses random selection of items and the use of probability theory to evaluate sample results, including measurement of sampling risk.
- **Non-statistical (judgmental) sampling** — selection that does not meet the above criteria; still disciplined, still documented, but conclusions are not quantitative.
- **Stratification** — dividing a population into discrete sub-populations that each have an identifying characteristic. Used to reduce variability within each stratum and allow the auditor to direct audit effort toward items of greater value or risk.

ISA 530 paragraphs 6–15 (and the AU-C 530 mirror) govern design, selection, performance, evaluation of results, and documentation. The structure of this chapter follows that order.

## Two-by-two of AI sampling the auditor runs

| | Attribute (deviation exists / does not) | Variables (measurement with magnitude) |
|---|---|---|
| **Statistical sampling (random selection + evaluation)** | Change-ticket control compliance; incident-ticket completeness; trace-record policy-flag application | Fairness-metric delta vs. claimed; latency SLO conformance; cost per decision |
| **Judgmental sampling (targeted selection, non-random)** | Red-team catalog coverage; high-risk cohort exemplars; "worst-offender" retrieved-doc cases | Stress tests on pre-selected edge cases; benchmark drift on named high-sensitivity probes |

Most engagements use both. The auditor who uses only one is skipping risk. Statistical sampling defends the headline rate across a large population; judgmental sampling defends coverage of the tail — the tail is where AI failures live, and where a random sample from a long tail would miss the harm.

## Attribute sampling — the common AI shape

Attribute sampling tests whether a condition is or is not present. Classical use cases: a control operated or did not operate; a document is complete or is not; an approval is present or is missing. AI examples:

- Every production change to a model artifact, prompt template, retriever config, tool registry, or guardrail config in the period has: an approving authority on the approved-authority list; a test-evidence attachment; a rollback plan; an immutable change ticket.
- Every logged inference in the period passes through the input filter *before* model invocation.
- Every human-review-queued decision is actually reviewed by a human within the SLA.
- Every incident of severity ≥ S has an RCA document with the required fields filled.

Attribute sampling is the right shape when the control either applied or did not — binary — and the question is the *rate* of non-application.

### Sample-size determination for attribute sampling

Three parameters drive sample size under ISA 530 / AU-C 530:

- **Confidence level** (complement: *risk of over-reliance*): often 90% or 95% for substantive reliance work.
- **Tolerable rate of deviation**: the maximum rate of deviation the auditor is willing to accept and still conclude the control operates effectively (illustrative anchors: 5% for strong reliance, 10% for moderate, >10% for weak reliance only).
- **Expected rate of deviation in the population**: based on prior-year findings, control-testing history, change-management maturity, and AI-specific drivers (recent drift, recent incidents, recent personnel changes).

Standard attribute-sampling tables — e.g., **AICPA Audit Guide, *Audit Sampling*, Appendix A** (tables for attribute sample sizes at 90% / 95% / 99% confidence) — give sample-size reads directly. Illustrative anchors from such tables (verify the current table at engagement time):

- 90% confidence, tolerable 5%, expected 1% → sample ≈ 77
- 95% confidence, tolerable 5%, expected 1% → sample ≈ 93
- 95% confidence, tolerable 10%, expected 2% → sample ≈ 48
- 95% confidence, tolerable 5%, expected 0% → sample ≈ 59

The engagement workpaper names the parameters and the source table; the sample size is reproducible from the parameters.

### Selection method for attribute sampling

- **Random selection** — a random-number generator seeded and documented; every sampling unit has a known, non-zero chance of selection.
- **Systematic selection with a random start** — every *k*-th record from a random start; appropriate when the population is not ordered by a characteristic that would bias the selection.
- **Stratified random** — strata first (e.g., high-risk business unit, high-volume day, guardrail-off window), random within each.
- **Monetary-unit sampling (MUS)** — dollar-weighted; useful when the sampling unit has a magnitude (e.g., claim-value change tickets) and the auditor wants high-value items to have a higher chance of selection.

The selection method is recorded; the random seed is recorded; the query that produced the sample is recorded; the resulting row identifiers are pinned to the workpaper. A sample that cannot be reconstructed from the record is not a defensible sample.

### Evaluation and projection

- Count deviations found in the sample.
- Compute the **upper-limit deviation rate (ULDR)** or the **upper-bound deviation** — the point above which the auditor cannot be confident the population rate falls, at the stated confidence. Attribute-sampling tables give this directly from the sample size and the number of deviations.
- Compare the ULDR to the *tolerable rate of deviation*. If ULDR ≤ tolerable rate, the control passes the attribute test (subject to qualitative analysis of each deviation). If ULDR > tolerable rate, the auditor cannot rely on the control and must extend procedures, revise the risk assessment, or qualify the conclusion.
- Qualitative analysis of deviations is required regardless of the quantitative result: pattern, cause, intention, concealment, recurrence, management awareness. A single intentional deviation is often more consequential than a dozen clerical ones.

## Variables sampling — measurement-based claims

Variables sampling estimates a quantity (a mean, a total, a difference) with a confidence interval. For AI engagements the common shapes:

- Claimed fairness gap on a cohort; the auditor re-measures on an independent sample and estimates the population-level gap.
- Claimed accuracy / precision / recall on a benchmark; the auditor re-measures on a sample.
- Claimed cost per decision, latency per decision, token usage per request.
- Claimed drift between periods on a named metric.

Where the eval population is already small and fully re-runnable (e.g., a 1,000-item benchmark), the auditor's cheapest path is **100% re-performance** — chapter 6 covers this as a reproducibility bundle. When the population is large (millions of production traces) and the claim is a statistic over that population, variables sampling is the ISA 530-compliant path to a confidence interval around the auditor's independent estimate.

Sample-size determination for variables sampling is driven by:

- Confidence level (analogous to attribute).
- **Tolerable difference** — the maximum delta between the auditor's estimate and the claimed value the auditor is willing to accept.
- **Expected difference** — the auditor's a-priori expectation of how far off the claim will be, based on risk assessment.
- **Population variability** — the standard deviation of the metric across the sampling frame. For AI metrics, this often requires a *pilot sample* to estimate variability before the main-sample size can be computed.

The engagement workpaper carries the sample-size equation, the inputs, and the pilot-sample output if used. Classical formulae:

```
n ≈ (z * s / E)^2
```

where `z` is the confidence-level z-score (1.645 for 90%; 1.96 for 95%; 2.576 for 99%), `s` is the population standard deviation (from pilot or prior period), and `E` is the tolerable difference. Finite-population corrections and stratification adjust downward.

Where the metric is a *proportion* (e.g., toxicity rate), the sample size reduces to the attribute-sampling equivalent with the proportion playing the role of the rate.

## Judgmental (non-statistical) sampling — the tail and the edge

Statistical sampling is poor at coverage of the *tail*. The tail is where AI failures live. The deployer's committed harms are not in the modal case — they are in the under-represented cohort, the adversarial prompt, the retrieved document that is one-in-a-million, the agentic trajectory that chains three improbable tool calls.

Judgmental sampling under ISA 530 paragraph A3 (and AU-C 530 paragraph A3) remains valid *provided* the selection is not random. The auditor selects items by professional judgment, defends the basis, and documents the limitations.

Judgmental sampling in AI audit — the standard patterns:

- **Red-team catalog coverage**: the engagement selects a subset of the organisation's red-team catalog (or a `mod-107`-driven harm model) and tests whether the production system responds correctly. Selection is by harm-class (prompt injection, data exfiltration, jailbreak, biased output, hallucinated authority, dangerous instruction), not random.
- **Protected-class exemplars**: for fairness criteria, the auditor selects synthetic or real cases from each named protected class and inspects the system's behaviour. Random-uniform sampling would under-represent small classes.
- **Worst-offender retrieval**: the auditor queries the trace store for the *worst* cases on the metric in question (highest-toxicity, highest-latency, lowest-confidence, highest-cost-per-decision) and inspects those traces. This is a targeted test — "is the organisation aware of its own worst cases?" — and complements the random sample on the average case.
- **Edge-of-policy cases**: the auditor selects cases near policy boundaries (barely over the threshold / barely under; recently added policy rule; recent exception) and tests application. The modal case is often fine; boundaries are where errors concentrate.

Judgmental sampling results are **not projectable** to the population in the quantitative sense. A clean judgmental sample does not prove a clean population; a dirty judgmental sample proves the population contains those specific issues and prompts a scope expansion.

## Stratification for AI populations

ISA 530 encourages stratification where the population is non-homogeneous and the auditor can direct effort by stratum. AI populations are rarely homogeneous. Typical strata:

- **By risk**: high-stakes decisions vs. low-stakes; appeal-available vs. terminal; affecting a protected class vs. not.
- **By time**: pre- and post- a specific change (new model version, new prompt template, new guardrail); peak vs. off-peak; business hours vs. after-hours.
- **By cohort**: by business line, by geography, by language, by client segment, by vulnerable-user flag.
- **By pathway**: cache-hit vs. cache-miss; retriever-hit vs. retriever-empty; tool-use vs. no-tool-use; retry-after-guardrail-block vs. first-try.
- **By volume class**: near-zero-volume strata (rare classes) often warrant disproportionate sampling attention; otherwise their behaviour is invisible in a volume-weighted random sample.

Stratification bounds should be **set before selection** and drawn from the risk assessment in `mod-103`, not post-hoc. The engagement workpaper records the strata, the chosen sample size per stratum, and the rationale.

## Population definition — the hardest part in AI

ISA 530 paragraph 7 is pointed: "the auditor shall determine the appropriate population from which to sample." For AI, defining the population is often the bulk of the sampling work. Three recurring traps:

- **The dashboard says 10 million; the trace store says 12 million.** The dashboard filters by a successful-response code; the auditor needs to sample the full population including failures and timeouts. Reconcile the frame to the underlying store and pin the reconciliation.
- **"Human-reviewed decisions" is not what the auditor thought.** The organisation calls a decision "human-reviewed" when a reviewer has the task in their queue, not when they clicked. Define the population by the auditor's criterion, not the organisation's workflow label.
- **Period boundary and completeness**: a trace store that evicts after 90 days is incomplete for a 12-month engagement. The population frame must cover the audit period; where retention is shorter, extend procedures over the gap (direct observation during the period; management attestation with corroborating evidence).

The engagement workpaper names: the *definition* of the population, the *frame* (the queryable artefact that enumerates it), the *reconciliation* of frame to definition, and the *handling of completeness exceptions*.

## Evaluating deviations qualitatively

ISA 530 paragraph 13 and AU-C 530 paragraph 14 require qualitative evaluation of each deviation:

- Is the deviation anomalous (demonstrably one-of-a-kind, with evidence) or systematic?
- Is there a pattern by business unit, time, operator, model version?
- Is management aware, and what has been done?
- Could a similar deviation misstate elsewhere in the population?

The anomalous-deviation determination is **not a default** — ISA 530 paragraph 13 requires the auditor to obtain a *high degree of certainty* that the deviation is not representative. In AI engagements, calling a deviation "anomalous" without the evidence to support it is a common finding against the audit itself in engagement-quality review.

## Documentation — what the workpaper must show

From ISA 530 paragraph 15 and the AU-C 530 mirror, the sampling workpaper records:

- The audit objective, assertion, and control or metric under test.
- The population definition, the sampling frame, and the frame-to-definition reconciliation.
- The tolerable rate (or difference) and the expected rate.
- The confidence level.
- The sample-size determination (table, formula, or judgmental rationale).
- The selection method, the random seed, and the resulting identifier list.
- The procedure applied to each sampled item.
- Deviations found, including the qualitative evaluation.
- The projection (attribute: ULDR; variables: estimate with confidence interval) and comparison to tolerable.
- The conclusion on the assertion and the implications for the overall opinion.

Chapter 5 shows the exact workpaper shape in Caseware / TeamMate+ / Workiva / AuditBoard and in a Git-tracked repo.

## Common failure modes

- **Population = frame, no reconciliation.** The auditor samples from the frame and concludes on the population without reconciling the two. Any gap in the frame becomes a scope gap the auditor did not see.
- **Random sampling the long tail.** A protected class that is 0.3% of the population has zero sample representation at 100 draws. The auditor must stratify or supplement with judgmental sampling.
- **Judgmental sampling treated as projectable.** A clean 20-prompt red-team pass does not say "the production system is safe" — it says "the system handled these twenty prompts". The workpaper must be explicit.
- **Sample size pulled from a round number.** "We tested 25" without a tolerable-rate / expected-rate / confidence-level justification fails engagement-quality review.
- **No qualitative evaluation of deviations.** Counting deviations is half the work. The engagement partner will ask "why did this happen" for every one.
- **Non-reproducible sampling.** The random seed is lost; the query is lost; the frame has moved. A year later, nobody can reconstruct the sample. Chapter 7 covers how to pin sampling artefacts into a chain of custody.
- **Statistical confidence without statistical selection.** A judgmental sample cannot report a confidence interval. If the engagement letter promises confidence, the selection must be random.

## Summary

- ISA 530 / AU-C 530 govern sampling for AI testing exactly as for financial testing: define the population, pick statistical or judgmental, size the sample from confidence-tolerable-expected inputs, select with a reproducible method, evaluate deviations quantitatively and qualitatively, project to the population, document.
- Attribute sampling fits binary AI controls (change-ticket completeness, policy-flag application, incident-RCA completeness); variables sampling fits re-measurement claims (fairness delta, accuracy, latency); judgmental sampling fits tail and edge coverage (red-team catalog, protected-class exemplars, worst-offender retrieval, edge-of-policy cases).
- Stratification is almost always needed for AI populations; by risk, time, cohort, pathway, or volume class. Strata are set before selection and drawn from the risk assessment.
- Population definition is the hardest step and the most common place sampling fails — reconcile the frame to the definition, name the completeness exceptions, and pin the reconciliation in the workpaper.
- Judgmental samples are *not projectable* in the quantitative sense. A clean judgmental pass does not prove a clean population; a dirty judgmental pass prompts scope expansion.
- The workpaper (chapter 5) records every parameter, selection, procedure, deviation, and projection. The engagement-quality reviewer will walk the chain end-to-end.
