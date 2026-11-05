# NYC Local Law 144 — The Independent Bias Audit in the BABL AI Shape

## Motivation

New York City Local Law 144 of 2021 (**NYC LL144**), effective 5 July 2023, is the first US statute to require a **mandatory, publicly disclosed, independent bias audit** of an **Automated Employment Decision Tool (AEDT)** before an employer or employment agency may use it on NYC candidates or employees. The Department of Consumer and Worker Protection (DCWP) issued final implementing rules (6 RCNY Chapter 5 Subchapter T), published a sample disclosure template, and operates the enforcement regime.

The LL144 engagement is unlike any other in this module:

- **The scope is narrow.** The audit covers one AEDT, one use context, one audit period.
- **The methodology is statutory.** Selection rate and impact ratio calculations are prescribed, with the four-fifths rule as a reference threshold (the statute does not mandate "pass/fail" at 0.8 — the disclosure speaks for itself).
- **The independence test is statutory.** DCWP rules define who is **not** independent: anyone who used the tool for an employment decision, anyone who had a direct or indirect financial interest in the tool's development, anyone employed by or financially interested in the tool's developer, deployer, vendor. The auditor's independence certification is a legal statement.
- **The output is public.** A **summary of the results of the most recent bias audit** must be published on the employer's or employment agency's website before the AEDT is used, and must remain available for at least six months after the AEDT ceases to be used; the summary must include specified fields.
- **Candidate-notification obligations attach.** The deployer must notify NYC candidates and employees that the AEDT will be used, the job qualifications and characteristics the AEDT will use, and (if requested) information about the type and source of data collected and the data retention policy.

The auditor's practice around LL144 is captured most clearly by **BABL AI's** algorithmic-audit methodology — one of the most-cited independent LL144 auditor profiles — and this chapter uses that shape as the reference. Other audit firms execute LL144 engagements under similar shapes; the statute defines the minimum, the BABL shape illustrates the mature practice. <!-- needs-research: confirm BABL AI's current LL144 audit methodology publication at reading time, and any updated DCWP guidance including the Office of Technology and Innovation's involvement -->

This chapter is the auditor's shape for executing an LL144 bias audit: scoping the AEDT, meeting the independence test, performing the statutory calculations across race, gender, and intersectional categories, producing the summary, and preparing the deployer's registration and candidate-notification evidence.

## What is in scope — the AEDT definition

LL144 and the final rules define **AEDT** narrowly. The tool is covered when:

- it is a **computational process, derived from machine learning, statistical modelling, data analytics, or artificial intelligence**;
- it **issues a simplified output, including a score, classification, or recommendation**;
- it is used to **substantially assist or replace discretionary decision-making** for making employment decisions that impact NYC candidates or employees;
- and the output is used to screen candidates or employees for employment or promotion.

"Substantially assist or replace discretionary decision-making" is defined to mean one of:

1. **relying solely** on a simplified output (score, tag, classification, ranking) with no other factors considered;
2. **using a simplified output as one of a set of criteria where it is weighted more than any other criterion** in the set; or
3. **using a simplified output to overrule conclusions derived from other factors including human decision-making**.

The scoping test for whether a tool is an AEDT at all — before the bias audit is even planned — is a recurring audit question. Tools that provide **guidance without a simplified output** (e.g., a large-language-model that generates interview summaries but outputs no score/classification/recommendation) may fall outside. Tools whose simplified output is **not weighted more than other factors** may also fall outside. The DCWP rules are the authoritative scoping reference.

Audit test shape: before accepting the engagement, the auditor obtains a scoping memo that states the AEDT's simplified-output form, its use in the hiring or promotion workflow, and the weighting rule that places it inside the AEDT definition. An AEDT the engagement letter calls an AEDT but that cannot be defended as one under the DCWP definition fails the independence-and-scope precondition.

## The independence test — a statutory precondition

Under 6 RCNY Chapter 5 Subchapter T, an **independent auditor** is one who:

- is not and has not been employed or retained to develop, test, maintain, or market the AEDT (with limited de minimis exceptions);
- does not have an employment relationship with the employer, employment agency, or vendor;
- does not have a direct financial interest or material indirect financial interest in the employer, employment agency, or vendor;
- can exercise objective and impartial judgment on all issues within the scope of the bias audit.

Auditor's test — before the engagement letter is signed:

- Prior-engagement sweep: has the firm ever developed, tested, maintained, or marketed this AEDT or any variant? Including consulting on the bias question for the tool's developer? If yes, the engagement is impermissible.
- Employment-and-contract sweep: does any engagement-team member hold any current employment or contract position with the deployer, developer, or vendor?
- Financial-interest sweep: direct (stock, equity grants, options, revenue-share) and material indirect (fund positions, family holdings) interests in the deployer, developer, or vendor.
- Objectivity representation: the lead auditor signs a representation that the engagement team can exercise objective and impartial judgment on all issues within scope, with reasoned disclosure of any residual threats and safeguards.

The independence file is the first exhibit the DCWP would request on an enforcement action. It must stand alone, dated, and signed, with the five-threat mapping (self-interest, self-review, advocacy, familiarity, intimidation) under IESBA / AICPA shape per `mod-101`.

## The statutory calculations

The bias audit measures **selection rate** and **impact ratio** across protected categories. The calculations are prescribed.

### The categories

Required at minimum:

- **Sex / gender categories** the EEO-1 report recognises — male and female (binary EEO-1 classification). <!-- needs-research: confirm DCWP rules' current treatment of non-binary and sex categories at reading time; the DCWP has taken positions in sub-regulatory guidance -->
- **Race / ethnicity categories** the EEO-1 report recognises — Hispanic or Latino, White (not Hispanic or Latino), Black or African American (not Hispanic or Latino), Native Hawaiian or Other Pacific Islander (not Hispanic or Latino), Asian (not Hispanic or Latino), Native American or Alaska Native (not Hispanic or Latino), two or more races (not Hispanic or Latino).
- **Intersectional categories** — the Cartesian product of sex × race/ethnicity (DCWP's amendments to the initial rules added intersectional analysis).

### The selection rate

Selection rate for a category = **number of selections in the category** / **number of applications in the category**. "Selection" is defined per the AEDT's output: for a classifier, "selected" might be "passing a threshold"; for a scoring system, "selected" might be "advanced to next stage"; the rules define this operationally and the deployer's workflow fixes it.

### The impact ratio

For **scoring systems**: the impact ratio = selection rate of a category / selection rate of the most-selected category.

For **classification systems** (e.g., categorical outputs): the impact ratio = scoring/success rate of a category / scoring/success rate of the most-selected category. The amendments and DCWP sub-regulatory guidance specify how classifier outputs are mapped.

### The four-fifths rule

Under US EEOC enforcement convention, an impact ratio **below 0.80** is evidence of **adverse impact**. The LL144 disclosure uses the four-fifths rule as the **reporting threshold** that triggers specific summary-of-audit disclosures; the statute does not prohibit AEDTs with impact ratios below 0.80 — it mandates the **public disclosure** of them.

### Data used — historical, test, and the historical-data condition

The audit is performed on:

- **Historical data** — the deployer's or employment agency's own data showing selections made by the AEDT for actual applicants/employees over a defined period; **OR**
- **Test data** — a representative data set, with specified conditions.

The deployer may use test data only if the audit "explains why the deployer or an employment agency does not have historical data available" **and** the test data is representative. The audit must disclose which type of data was used.

### Missing-category reporting

Where a category has fewer than a defined threshold of candidates in the dataset (the DCWP rules address small-category handling), the audit reports the count as "insufficient" rather than computing an unreliable rate.

### Scope of the audit period

The audit covers the period the deployer specifies, at most 365 days before the AEDT's use. The audit must be performed **no more than one year** before the AEDT's use for any given employment decision (hence the "annual bias audit" shorthand).

## The data the auditor demands

For a historical-data audit, the auditor demands from the deployer:

- Candidate dataset over the audit period: unique candidate ID (pseudonymised or hashed per privacy design), application date, job requisition ID, AEDT output (score / classification / recommendation), AEDT version, candidate self-identified sex, candidate self-identified race / ethnicity, downstream decision outcome (if used in selection).
- Data-collection methodology: how self-identification was captured; how the candidate was informed and what opt-outs applied; what reconciliation was performed with other deployer data (ATS, HRIS).
- Workflow description: where the AEDT sits in the decision workflow; how its output is combined (or not) with other factors; the selection operationalisation.
- AEDT documentation: vendor documentation of the model, version pinning, release notes within the audit period, any retraining events, any guardrail changes.
- Prior-audit evidence: for a repeat engagement, prior audit's findings and any remediation.

For a test-data audit, the auditor demands: the test dataset with representativeness evidence, the deployer's explanation for the absence of historical data, the AEDT access the auditor was given to produce outputs.

## The audit calculation workbook

The deliverable spine is a calculation workbook:

1. **Data audit tab.** Raw counts, missingness, category assignment, exclusions (duplicates, invalid, outside-period), remaining sample. Audit trail of decisions with named rationale.
2. **Selection rate tab.** Category-by-category selection counts and rates. Confidence intervals where sample sizes permit.
3. **Most-selected category tab.** Identifies the reference (most-selected) category used as the denominator.
4. **Impact ratio tab.** Impact ratios per category relative to most-selected; flag impact ratios below 0.80.
5. **Intersectional analysis tab.** Cartesian product of sex × race/ethnicity cells, selection rate, impact ratio, insufficient-count indicator.
6. **Sensitivity tab.** Robustness checks — alternative threshold selection, alternative definition of "selection" (if operationally ambiguous), alternative handling of missing self-identification.
7. **Summary tab.** The numbers that will appear in the publicly-disclosed summary.

The workbook is executed by the auditor, not by the deployer; the deployer supplies data and methodology context; the computations are the auditor's work.

## The publicly disclosed summary

The deployer (or employment agency) must publish the **summary of the results of the most recent bias audit** on its website before using the AEDT and keep the summary available for at least six months after use. DCWP's sample summary and the rules require:

- **Date** of the most recent bias audit.
- **Source and explanation of the data used** (historical vs. test; the deployer's rationale for test-data use where applicable; the date range).
- **Selection rates** for each category.
- **Impact ratios** for each category.
- **Intersectional** analysis selection rates and impact ratios.
- **The number of individuals assessed** who fall within an unknown category.
- **Distribution date of the AEDT** (or similar information identifying the version).

The auditor does not publish the summary — the deployer does. But the auditor **authors** the summary content and attests it reflects the audit.

## The candidate-notification obligations

Independent of the summary, the deployer must notify NYC candidates and employees:

- That an AEDT will be used in connection with the assessment or evaluation of the candidate or employee — **at least 10 business days** before use.
- The job qualifications and characteristics the AEDT will use.
- If requested by the candidate or employee (within 10 business days of such notice), information about the **type of data collected, source of the data, and the deployer's data retention policy**.

The auditor often also inspects the notification artefacts because an LL144 compliance claim fails if the notification is defective — the auditor's reports to the deployer typically note notification observations even though the audit is scoped to the bias calculation.

## AEDT registration — DCWP's practical question

DCWP does not operate a central AEDT registry; the summary-of-audit publication on the deployer's own website plus the required candidate notification are the regulatory touchpoints.  The DCWP's enforcement posture is complaint-driven and audit-record-driven. On an enforcement action, DCWP would request:

- The summary of the most recent bias audit from the deployer's website.
- The underlying audit report and workbook.
- The independent-auditor representation.
- The candidate notifications given during the period in dispute.
- Any discovery of candidates who were not notified or categories that were not analysed.

Audit test shape: the deployer's "evidence file" covering each of these DCWP touchpoints must be complete and retained. <!-- needs-research: confirm whether a central NYC AEDT registry or similar has been established at reading time, and any changes to the DCWP enforcement regime -->

## Common failure modes

- **Not actually an AEDT.** Tool is in scope of the engagement but its use does not meet the DCWP's "substantially assist or replace" test; the audit is performed for a tool that does not require it. The opposite is also seen — a tool that does meet the definition but is scoped out of the audit.
- **Independence evidence thin.** Engagement team has prior consulting history with the developer; the independence file does not disclose it. DCWP finding on enforcement.
- **Selection-rate operationalisation missing.** "Selection" is not clearly defined per the workflow; the auditor computes a rate under one definition but the deployer operates under another; the audit does not reflect reality.
- **Intersectional analysis skipped.** Early-period audits sometimes omitted intersectional; the DCWP amendments require it; omission is a finding.
- **Insufficient-count categories hidden.** Categories with very small counts are reported with an impact ratio anyway; the number is noisy and misleading; auditor must report "insufficient" rather than a spurious number.
- **Historical-vs-test justification missing.** Deployer uses test data; audit does not explain the absence of historical data as the rules require.
- **Repeat audit recomputes stale data.** The next-year audit uses the same dataset as the prior year; the rules require coverage of the most recent period.
- **Summary not current.** Summary on the deployer's website is older than one year; the deployer continues to use the AEDT.
- **Candidate notification omitted.** Notifications not sent within the 10-business-day window; auditor observes but engagement letter does not scope notifications; the deployer's overall compliance claim fails anyway.
- **Developer disclosure confused with deployer disclosure.** Developer publishes a bias audit of its tool; deployer relies on it; the disclosure obligation attaches to the deployer, not the developer; deployer still needs its own LL144 summary.

## The BABL shape — mature practice

Mature practitioners (BABL AI is the most-cited; others include ORCAA, Eticas, HireVue's own published audits, and a growing set of firms) execute LL144 engagements with:

- A **data readiness phase** before fieldwork, including de-identification review and candidate-self-identification completeness.
- A **statistical-rigour layer** on top of the statutory calculation — confidence intervals, sensitivity analysis, comparison to historical baselines.
- **Documentation of definitions** — what "selection" means in this workflow, how edge cases are resolved, which candidates are in and out of population.
- **A written reproducibility statement** — enough detail that a second auditor could re-run the calculation if asked.
- **A narrative report** that goes beyond the summary (for the deployer's internal use and for legal counsel) covering risks, limitations, and recommended follow-up — distinct from the public summary.
- **Interface with other audits** — IAAIS (chapter 3), ISO 42001, SR 11-7 (chapter 5 for AEDTs used by financial institutions), EU AI Act (chapter 1 for the same AEDT used in the EU as a high-risk Annex III employment system).

## Boundary with EU AI Act and other regimes

LL144 and the EU AI Act Annex III employment category (point 4, AI systems intended to be used for recruitment or selection of natural persons, in particular to analyse and filter job applications, and to make decisions affecting terms of work-related relationships, promotion and termination) often target the **same tool** used across jurisdictions. The audits are not substitutes:

- **LL144** delivers a bias-audit calculation and a public summary; a narrow, prescriptive, local engagement.
- **EU AI Act Annex III** (chapter 1) delivers a conformity assessment including risk-management, data governance, transparency, human oversight, and technical documentation.

An AEDT used in both jurisdictions needs **both** audits. The auditor coordinates evidence reuse where possible — the bias examination under Article 10 can reuse LL144 evidence if methodology is adequate; the LL144 audit cannot reuse the Article 10 bias examination because LL144 has its own statutory form.

## Summary

- NYC LL144 requires a public, independent bias audit of AEDTs used to screen or promote candidates and employees in NYC, under DCWP's final rules; the audit covers the period up to one year before use.
- The scope is tight (one AEDT, one use), the independence test is statutory, the calculations (selection rate, impact ratio, four-fifths, intersectional) are prescribed, and the output is a public summary with specific required fields.
- Independence sweeps cover prior engagements, employment and contract relationships, direct and material indirect financial interests, and an objectivity representation; the file is dated and signed and stands alone.
- Data is historical by default, test only with documented rationale and representativeness; insufficient-count categories are reported as insufficient rather than with noisy numbers.
- The deployer publishes the summary and gives candidate notifications (at least 10 business days in advance plus additional information on request); the audit records the deployer's compliance evidence.
- Mature practice adds statistical rigour, reproducibility documentation, and narrative reporting alongside the public summary; LL144 does not substitute for EU AI Act Annex III, ISO 42001, or SR 11-7 engagements that may also apply to the same tool.
