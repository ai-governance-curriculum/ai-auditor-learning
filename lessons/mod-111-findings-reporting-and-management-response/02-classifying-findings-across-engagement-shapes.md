# Classifying Findings — Severity Grades Across Engagement Shapes

## Motivation

A finding's shape — the five CCCER elements — is universal. A finding's **classification** is not. The same observation, carried through five different engagement types, picks up five different severity labels, each with its own definition, its own threshold, its own consequence for the certificate or opinion, and its own legal-weight language.

The auditor does not get to invent a classification scheme. Each engagement shape is governed by a standard that **mandates** the grading vocabulary. ISO/IEC 17021-1 fixes "nonconformity" and "opportunity for improvement" for AIMS certification. AICPA attestation literature and PCAOB AS 2201 fix "deficiency / significant deficiency / material weakness" for controls engagements. The U.S. Fed's SR 11-7 fixes the supervisory lexicon for Model Risk Management. ForHumanity's IAAIS fixes pass/conditional/fail for independent-audit certification. NYC Local Law 144 fixes the required summary content for a published bias audit. If the auditor uses the wrong vocabulary, the report is unusable to the audience that must act on it.

This chapter walks each scheme the AI auditor is likely to work in, names the definition that governs each severity level, states the decision consequence at the certificate / opinion / report level, and gives an AI-specific example.

## ISO/IEC 17021-1 — AIMS certification (ISO/IEC 42001)

**Standard.** ISO/IEC 17021-1:2015 "Conformity assessment — Requirements for bodies providing audit and certification of management systems" governs how a certification body audits an AIMS against ISO/IEC 42001. The standard fixes two mandatory categories of finding (nonconformity and, by negative implication, conforming) and provides a third category used widely in practice (opportunity for improvement).

### Major nonconformity

**Definition.** ISO/IEC 17021-1 clause 9.4.9 defines major nonconformity as a nonconformity that affects the capability of the management system to achieve the intended results. Indicators include:

- a significant doubt that effective process control is in place, or that products or services will meet specified requirements;
- a number of minor nonconformities associated with the same requirement or issue that could demonstrate a systemic failure and thus constitute a major nonconformity.

**Certificate consequence.** A certification body cannot recommend issuance (initial) or continuation (surveillance / recertification) of a certificate while a major nonconformity is open. The auditee must demonstrate correction, cause analysis, corrective action, and effectiveness — with the certification body verifying before closure. Typical timeline for closure review is on the order of weeks, not months, with on-site verification where warranted.

**AI example.** The AIMS risk-register process (ISO/IEC 42001 §6.1, read with §8.3 AI SIA) has not been executed for any in-scope AI system since the AIMS was declared operational twelve months ago. The intended result of §6.1 is not achieved: the organisation does not know its AI risks. **Major nonconformity.**

### Minor nonconformity

**Definition.** A nonconformity that does not affect the capability of the management system to achieve the intended results. Typical shape: a procedure is documented and generally applied, but an isolated failure has occurred; a single record is missing; a review was late by one cycle.

**Certificate consequence.** Correction and corrective action are required. The certificate can issue with minor nonconformities open subject to the certification body's closure procedures — usually a documented CAP with evidence of implementation to be reviewed on paper, with on-site verification at the next surveillance audit.

**AI example.** Seven of the forty in-scope AI systems have an AI SIA on file; the AI SIA for one of them (`support-chatbot-v2.1`) was completed 11 days after the system went live, in breach of the "before deployment" requirement in the organisation's procedure, but the SIA was performed and did not surface residual risks requiring design change. **Minor nonconformity.**

### Observation

A statement of fact noted during the audit that does not currently constitute a nonconformity but may, if the trend continues, become one. Observations are not required by ISO/IEC 17021-1 but are standard practice. Observations do not block the certificate and do not require a corrective action — though a managed response is good practice.

**AI example.** The AIMS has defined "decision-with-significant-effects" as the trigger for mandatory SIA, but the operational definition relies on the data-science team's self-classification at release time; four of the recent twenty classifications were reviewed and were consistent, but the trigger has no independent challenge. No current nonconformity; monitor for drift.

### Opportunity for improvement (OFI)

An OFI identifies a path to a stronger AIMS that is not required for conformity. The auditee is free to act on it or not. OFIs are not required reporting; many audit firms separate them from the audit report entirely to preserve the finding/OFI distinction.

**AI example.** The organisation could realise efficiency by consolidating three overlapping registers (AI inventory, risk register, model registry) into a single tool; current configuration is conformant.

### What the AIMS auditor avoids

- Using the ISO vocabulary ("major nonconformity") in an engagement that is not an ISO/IEC 42001 certification — e.g., calling an SR 11-7 finding a "major nonconformity" is a category error.
- Grading on severity-of-business-impact rather than on definition. ISO definitions are about *capability of the management system to achieve intended results*, not about how much money is at stake.
- Treating repeat minor nonconformities as still minor. Clause 9.4.9's second indicator explicitly promotes a pattern to major status.

## SR 11-7 — U.S. Fed MRM supervisory language

**Standard.** Federal Reserve SR 11-7 "Guidance on Model Risk Management" (2011), paralleled by OCC 2011-12, governs validation of models used in regulated U.S. banks. The supervisory vocabulary is layered — the MRM framework internally uses its own severity ratings, and the Fed's examiners overlay matter-requiring-attention / matter-requiring-immediate-attention / supervisory-letter language on top. SOX §404 and PCAOB AS 2201 overlay "significant deficiency / material weakness" when the model feeds financial statements (e.g., Current Expected Credit Loss models).

### Deficiency

A control weakness in the model lifecycle (development, implementation, use, validation, governance) that does not rise to significant or material level. The MRM function catalogues deficiencies, assigns owners and remediation dates, and tracks closure.

**AI example.** The LLM-based summarisation layer used in the internal credit-adjudication workbench has no documented validation beyond a developer's sample-based review; the layer does not directly feed the credit decision but materially shapes the presentation of the analyst's view. **Deficiency** — governance, documentation, and limited validation gap.

### Significant deficiency

A deficiency, or a combination of deficiencies, that is less severe than a material weakness yet important enough to merit attention by those responsible for oversight (the audit committee, the board, the Model Risk Committee). PCAOB AS 2201 and AICPA AU-C 265 provide the foundational definitions; the bank's MRM function applies them to models.

**AI example.** A portfolio-wide GenAI-assisted document-review tool materially shapes the analyst's reserving decision across the Expected Credit Loss (ECL) model, yet lacks an ongoing performance monitoring process; the pathway from tool output to ECL inputs has not been mapped. Audit committee attention warranted. **Significant deficiency.**

### Material weakness

A deficiency, or a combination of deficiencies, in internal control such that there is a reasonable possibility that a material misstatement of the entity's financial statements will not be prevented, or detected and corrected, on a timely basis. For AI-touching controls: a weakness in a model used to compute a financial-statement input is tested for materiality the same way any other ICFR deficiency is — against the prudent-person reasonable-possibility standard.<!-- needs-research: confirm the exact PCAOB AS 2201 paragraph for the "reasonable possibility / material" definition at reading time; the 2024 reclassification of AS 2201 into the AS 1000 series may have renumbered. -->

**AI example.** The CECL/ECL challenger-model benchmark is itself a GenAI-assisted scenario generator; the auditor cannot obtain evidence that the scenario set is representative of recessionary conditions, and the resulting ECL is a Level-3 estimate representing 14% of pre-tax income. **Material weakness** — the audit opinion on internal control will be qualified absent remediation.

### Supervisory language layered on

- **MRA (Matter Requiring Attention).** An issue the bank should address.
- **MRIA (Matter Requiring Immediate Attention).** An issue demanding prompt remediation with examiner follow-up.
- **SR / 4(m) letters.** Heightened supervisory scrutiny communicated by letter.

The MRM auditor who finds material weaknesses in AI models that feed financial statements should expect regulators to layer MRA/MRIA designations onto the finding; the auditor's finding itself remains in deficiency/significant/material vocabulary.

### What the MRM auditor avoids

- Mixing ISO "nonconformity" into an SR 11-7 validation report.
- Grading a model-governance deficiency as a material weakness without connecting it to a reasonable-possibility material-misstatement path. The grade has a legal threshold; do not borrow it.
- Letting the examiners' classification language substitute for the validator's own finding grading.

## SOC for AI (AT-C 105, SSAE 18 / SOC 2) — attestation vocabulary

**Standard.** AICPA SSAE No. 18 (as reissued under AT-C 105 and related sections) governs attestation engagements over subject matter, including SOC 1 (ICFR), SOC 2 (Trust Services Criteria), SOC 3, and sector variants. ISAE 3000 is the international analogue. The AICPA has been developing guidance for AI-specific attestation under these frames; the trust-services vocabulary applies directly.

### Deficiency in design

A control that would not meet its objective even if operated as described. Example: a bias-monitoring control is specified to run "when needed" with no defined trigger — a design that could not satisfy the control objective because triggers are undefined.

### Deficiency in operating effectiveness

A control that meets its design objective but was not operated as designed during the examination period. Example: the pre-deployment fairness evaluation control is defined correctly, but three of the twenty sampled releases proceeded without the evaluation being performed.

### Type I vs Type II opinions

A SOC 2 **Type I** report expresses an opinion on the suitability of control design at a point in time; a **Type II** report adds operating effectiveness over a period (commonly six or twelve months). An AI-system Type II examination sampling period must be long enough that monitoring controls have a chance to detect drift events; the auditor's engagement letter fixes the period explicitly.

### Opinion types

- **Unmodified (unqualified).** Controls are suitably designed and operating effectively.
- **Qualified.** Specific controls or specific criteria are excepted; the exception is described.
- **Adverse.** Controls are not suitably designed or not operating effectively overall; the report reads as a negative opinion.
- **Disclaimer.** The auditor cannot obtain sufficient appropriate evidence to express an opinion.

### AI example

Across an AI-enabled SaaS provider's Type II examination period (twelve months), the pre-deployment model-card review control (CC7.1-coded) failed in 4 of 18 deployments. Design is suitable; operating effectiveness has exceptions. The auditor issues a **qualified** opinion, with the exceptions listed and the remediation disclosed in management's description.

### What the SOC-for-AI auditor avoids

- Substituting ISO nonconformity language for AICPA deficiency language.
- Expressing an opinion the vocabulary cannot sustain (e.g., calling an opinion "qualified" when the exceptions are not sufficiently described; calling a single failure a "material weakness" without the ICFR path).
- Confusing "exception" (a deviation) with "deficiency" (a design or operating-effectiveness gap). Exceptions aggregate into deficiencies; one exception is not automatically a deficiency.

## ForHumanity IAAIS — Independent Audit of AI Systems

**Standard.** ForHumanity is a non-profit that publishes the **Independent Audit of AI Systems (IAAIS)** certification scheme, including criteria organised around risks, rules, oversight and controls. Certified Auditors of AI Systems (FHCAs) deliver engagements against ForHumanity criteria, with the classification scheme fixed by the scheme owner.<!-- needs-research: confirm the ForHumanity IAAIS classification vocabulary current at reading time; ForHumanity's criteria and certification scheme have evolved across releases, and the auditor should pull the scheme-owner's current binding text for severity grading terms. -->

### Pass

The system satisfies the criteria tested. Certification issues against the specific criteria set covered.

### Conditional

The system substantially satisfies the criteria but has open items requiring remediation within a defined window to reach pass. The auditor describes the open items and the remediation plan; the scheme owner's rules determine whether an interim certificate issues.

### Fail

The system does not satisfy the criteria. No certification issues. The report describes the gaps and the path forward.

### AI example

An IAAIS engagement against the ForHumanity criteria for an AI-enabled hiring system identifies gaps in the Article-13-equivalent transparency criterion and in the harm-mitigation criterion. The system otherwise satisfies the tested criteria. **Conditional** — the report names the two gaps, the remediation window, and the retest shape.

### What the IAAIS auditor avoids

- Using ISO or AICPA vocabulary instead of the scheme-owner's grades.
- Issuing the certificate before the scheme owner's independence, competence, and conflict-of-interest declarations have been satisfied.

## NYC Local Law 144 — bias-audit publication language

**Standard.** NYC Local Law 144 of 2021 and 20 RCNY §5-301 (DCWP rule) require employers and employment agencies using an "automated employment decision tool" (AEDT) in a NYC-adjacent hiring or promotion decision to commission an *independent bias audit* annually and publish a summary of the most recent audit on the employer's website.

### Required summary content

The published summary must include at least:

- The date of the most recent bias audit.
- The source and the explanation of the data used.
- The *selection rates* and *impact ratios* for all categories required under the rule, per the computation methodology defined in §5-301.<!-- needs-research: confirm the current 20 RCNY §5-301 required subgroup categories (sex, race/ethnicity, and their intersections) at reading time; DCWP rule changes are infrequent but do occur. -->
- The distribution date for the AEDT.

### Classification language

LL144 does not use a pass/fail/conditional vocabulary. The summary reports **the numbers**. The reader derives the implication. The auditor's professional role is to ensure the numbers are computed per the rule's methodology, published in the required shape, and signed in a way the employer can defend if challenged.

### What the LL144 auditor avoids

- Substituting ISO or FHCA language for the rule's required computation and disclosure.
- Publishing a summary that comments on acceptability — the rule is a disclosure instrument, not a conformity determination.
- Omitting the distribution date, the data source explanation, or any required subgroup; omissions expose the employer to the $500–$1,500-per-day penalty per §20-872.

## IIA Global Internal Audit Standards — internal audit function

**Standard.** The IIA's **Global Internal Audit Standards** (effective 2025-01-09, replacing the 2017 IPPF Standards) govern an internal-audit function's work.<!-- needs-research: confirm the current naming and numbering; the 2024 release is the Global Internal Audit Standards, and IIA may release updates. --> The IIA standards do not mandate a specific severity vocabulary; the IAF's charter and the audit committee's preferences fix it. Common schemes:

- **Rating by risk.** High / Medium / Low (or 1–3, 1–5) — defined in the IAF's methodology, applied to each finding by its residual risk after controls.
- **Rating by action urgency.** Priority 1 (immediate remediation) / Priority 2 (next cycle) / Priority 3 (continuous improvement).
- **Rating by engagement opinion.** Satisfactory / Needs improvement / Unsatisfactory, used at engagement level to summarise all findings together.

What the IIA Standards *do* require: that the IAF's engagement reports contain the elements specified under the current Communicating Results standard (condition / criteria / cause / effect / recommendations and management action plans), and that overall opinion language — if used — is supported by sufficient evidence. The IAF cannot inherit an outside scheme's vocabulary unless its own methodology adopts it.

### AI example

An internal-audit function audits the organisation's AIMS ahead of the ISO/IEC 42001 surveillance audit. Internal findings use the IAF's standing rating (H / M / L). When the engagement report moves to the audit committee, the opinion sentence reads: "The AIMS is **assessed as Needs Improvement** — one high-rated finding on the pre-deployment control gap and three medium-rated findings on documentation completeness were raised." The ISO vocabulary (major / minor) is *not* used; the ISO audit will apply its own vocabulary separately.

## Internal consistency — the auditor's tracker

A multi-engagement AI auditor often carries the same underlying observation across several engagements: the ISO surveillance audit records a minor nonconformity; the SOC 2 Type II sees a control deficiency; the internal-audit function rates the issue Medium; the Fed MRM validation views the model portfolio and sees a significant deficiency. All four classifications are correct, for their respective schemes.

The auditor's internal tracker (chapter 6) records the classification per scheme so that nothing collapses into a single grade; each engagement reports in its native vocabulary; the aggregate pattern feeds the enterprise AI-risk picture at the Model Risk Committee or equivalent forum.

## Common failure modes

- **Cross-vocabulary smuggling.** "Minor nonconformity in the SR 11-7 validation" is not a sentence in any standard. Fix by choosing the scheme's own word.
- **Severity inflation.** Grading an isolated process miss as a major nonconformity because the auditor is annoyed. The definitions are not elastic.
- **Severity deflation.** Grading a systemic pattern as minor because an executive is powerful. The second indicator in ISO/IEC 17021-1 §9.4.9 is a trap door against this; so is PCAOB AS 2201's aggregation guidance.
- **Opinion-type mismatch.** Qualifying a SOC 2 opinion when the exceptions pattern merits adverse; expressing an unqualified ISO 42001 recommendation while a major nonconformity sits open.
- **LL144 summary editorialising.** Adding "the system is fair" to a bias-audit summary. The rule does not authorise that language.

## Interfaces to adjacent chapters

- Chapter 1 (CCCER) fixes the *shape* of a finding; this chapter fixes the *label* it carries.
- Chapter 3 (management response) handles the negotiation that determines whether a classification is sustained or re-opened.
- Chapter 4 (report authoring) picks the overall opinion that these per-finding classifications roll up into.
- Chapter 7 (regulator-facing submissions) maps the classifications into the forms regulators consume.
- `mod-110` (sector shapes) set up each engagement shape in the first place; this chapter is the vocabulary that flows out.

## Summary

- Finding severity vocabulary is **engagement-shape-specific**; the auditor uses the scheme-owner's word, not a generic one.
- ISO/IEC 17021-1 for AIMS audits: major nonconformity (blocks certificate), minor nonconformity (requires CAP), observation, opportunity for improvement.
- SR 11-7 / MRM: deficiency, significant deficiency, material weakness — with the PCAOB-anchored definitions where models feed financial statements, and MRA/MRIA supervisory language layered on by regulators.
- SOC for AI under AT-C 105 / ISAE 3000: deficiency in design, deficiency in operating effectiveness; Type I vs Type II; unmodified / qualified / adverse / disclaimer opinion types.
- ForHumanity IAAIS: pass / conditional / fail per the current scheme-owner's binding scheme text.
- NYC LL144: not a pass/fail scheme; required computation and summary-publication shape fixed by 20 RCNY §5-301.
- IIA Global Internal Audit Standards: IAF-defined ratings (H/M/L or similar), overall engagement opinion if the IAF uses one; cannot borrow another scheme's vocabulary without adopting it in methodology.
- Internal tracker records each engagement's native classification so the enterprise view can aggregate without collapsing distinctions.
