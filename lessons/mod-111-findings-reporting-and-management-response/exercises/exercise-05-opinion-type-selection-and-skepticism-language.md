# exercise-05: Opinion Type Selection and Professional-Skepticism Language

**Estimated effort:** 2 hours

## Objective

Given six engagement fact-patterns, select the correct opinion type under the governing standard (ISA 705 / AU-C 705 / SSAE / ISAE 3000) for each, and draft the opinion paragraph with the professional-skepticism language the standard expects. Produce a decision workpaper documenting the materiality, pervasiveness, and evidence-sufficiency reasoning behind each selection.

## Prerequisites

- Chapter [`04-audit-report-shapes-and-opinion-types-by-audience.md`](../04-audit-report-shapes-and-opinion-types-by-audience.md)
- Access to:
  - ISA 705 (Revised) "Modifications to the Opinion in the Independent Auditor's Report" and the corresponding AU-C 705
  - AICPA SSAE 18, AT-C 205 for examination engagements
  - ISAE 3000 (Revised) for international attestation engagements
  - AU-C 200 and ISA 200 for professional skepticism
  - Yellow Book GAGAS §6.21 and §9.17

## Scenarios

For each of the six fact-patterns below, select the opinion type and draft the opinion paragraph.

### Pattern 1 — SOC 2 Type II, isolated exception

Service organisation operates an AI-enabled transcription service. Examination period 12 months. 47 controls tested across Security, Availability, Processing Integrity, Confidentiality. All 47 are suitably designed. 46 operated effectively. One control (CC7.2 — pre-deployment model-card review for releases to production) had 2 exceptions out of 24 sampled releases; remediation is in flight. The exceptions are not tied to a security or availability incident.

### Pattern 2 — SOC 2 Type II, pervasive control-failure

Service organisation operates a GenAI-assisted contract-review service. Examination period 6 months. 38 controls tested. 7 controls had operating-effectiveness exceptions, including change management (CC8.1), logical access (CC6.1), and model monitoring (PI1.5). Exceptions were not isolated — they span multiple TSC categories and multiple months. Management has committed to remediation but has not yet implemented.

### Pattern 3 — ISAE 3000, limited-assurance on a bias claim

Reasonable-assurance would require the auditor to obtain access to training data for independent reperformance of the bias claim. The engagement letter specifies limited assurance only. The auditor performed inquiries, inspection of the provider's bias-audit workpapers, and limited reperformance on a sample. Nothing has come to the auditor's attention that the bias claim is not fairly stated.

### Pattern 4 — ISAE 3000 reasonable assurance, scope limitation that cannot be removed

Auditor is engaged to provide reasonable assurance on a model-card accuracy claim for an AI service. The provider cannot grant the auditor access to the training data because it is held by a third-party pre-training provider under confidentiality terms that the provider cannot unilaterally waive. The auditor cannot reperform the key subject-matter test. Limited-assurance scope-adjustment is declined by management.

### Pattern 5 — ISO/IEC 42001 recertification audit

Audit team identifies one major nonconformity (pre-deployment control gap, chapter 1 example) and three minor nonconformities (documentation completeness in Annex A controls). Management has provided an acceptable CAP for the major nonconformity that will take 60 days to implement; minor NCs have CAPs that will take 30 days. ISO/IEC 17021-1 allows the certification body's committee to recommend continuation subject to CAP closure.

### Pattern 6 — AT-C 205 examination on fairness assertion, material-and-pervasive exception

Service organisation makes a public assertion that its AI-enabled hiring tool satisfies the four-fifths rule across protected classes. Auditor's examination finds the four-fifths-rule ratio is 0.66 for one protected class (below 0.80). The exception is not isolated — it is the central assertion of the engagement.

## Deliverables

### 1. Opinion-selection decision workpaper (~800 words)

For each of the six patterns, document:

- The standard governing the engagement.
- The materiality judgement — is the exception / issue material?
- The pervasiveness judgement — is it pervasive to the subject matter overall?
- The evidence-sufficiency judgement — could the auditor obtain sufficient appropriate evidence?
- The resulting opinion type: unmodified, qualified, adverse, disclaimer.
- The reasoning in two or three sentences per pattern.

### 2. Six drafted opinion paragraphs (~250–400 words each)

Draft each opinion paragraph with:

- The standard's expected opening ("In our opinion…" / "Based on the procedures performed and the evidence obtained, nothing has come to our attention…" / "Our examination was conducted…").
- The specific subject-matter identification.
- The explicit opinion sentence, with the correct modification.
- Where modified, the "Basis for Qualified / Adverse / Disclaimer Opinion" section preceding the opinion paragraph.
- Professional-skepticism language anchored in the standard's own phrases.
- The independence declaration (where the standard calls for it in the opinion rather than elsewhere in the report).

### 3. Professional-skepticism language catalogue (~400 words)

Catalogue the professional-skepticism phrases the drafted opinions rely on, mapped to their standard-specific origins. For each phrase, note:

- Where the standard anchors the phrase (paragraph / clause citation, with `needs-research` where unverified).
- Why the phrase matters — what signal it sends to regulators or litigation.
- Common omissions that weaken an opinion (e.g., omitting "sufficient and appropriate evidence" from an ISAE 3000 opinion).

## Starter guidance

- **The decision rule is mechanical.** Chapter 4: material? → pervasive? → evidence sufficient? → opinion type. Walk the rule; do not freestyle.
- **Limited-assurance has its own voice.** The ISAE 3000 limited-assurance opinion is phrased in the negative ("nothing has come to our attention") — do not write it in the affirmative of reasonable-assurance.
- **Scope limitations that management will not remove are disclaimer territory.** Reasonable-assurance that cannot be performed because evidence is inaccessible is a disclaimer, not a modified qualified. Pattern 4 is the trap.
- **ISO/IEC 42001 does not have "qualified" certificates.** Pattern 5 is binary at the certificate level; the question is whether to recommend continuation subject to CAP closure, decline, or require immediate remediation before recommendation.
- **AT-C 205 and ISAE 3000 differ in jurisdictional reach; both have the same decision rule but different boilerplate.** Pattern 6 could be written under either; pick one and stick to its phrases.
- **Do not editorialise in the opinion.** Opinion language is standard-prescribed. Decorative phrases undermine the opinion's legal weight.

## Acceptance criteria

The deliverables are accepted when:

- The decision workpaper walks the materiality / pervasiveness / evidence-sufficiency chain for every pattern.
- Opinion-type selections are defensible under the governing standard's decision rule; Pattern 2 is adverse (pervasive exceptions); Pattern 4 is disclaimer (scope limitation precluding sufficient evidence); Pattern 6 is adverse (material and pervasive to the central assertion); Pattern 1 is qualified (isolated, material exception); Pattern 3 is unmodified limited assurance; Pattern 5 is "recommend continuation subject to CAP closure" (not the ISA 705 vocabulary).
- Drafted opinion paragraphs use the standard's own phrases and modifications; qualified and adverse opinions include a preceding "Basis for Modified Opinion" paragraph with specific exception description.
- The limited-assurance opinion in Pattern 3 is written in the expected negative voice.
- Each opinion includes professional-skepticism language anchored to the standard's expected phrasing.
- The skepticism-language catalogue anchors each phrase to a specific standard paragraph (with `needs-research` where the exact paragraph citation is beyond verifiable knowledge).
- No invented clause citations; `needs-research` marks are used where appropriate rather than guessed references.

## Stretch goals

- Rewrite the opinions for Patterns 2 and 6 in both **AT-C 205 (U.S.)** and **ISAE 3000 (international)** shapes side by side, exposing the phrasing differences.
- Produce a **"bad opinion"** version of each drafted paragraph — the sloppy opinion an inexperienced auditor would write — and annotate what is specifically wrong with it.
- Author a **short note to the audit committee** for Pattern 4 explaining why the auditor is issuing a disclaimer and what that means for the organisation's ability to represent the model-card claim to customers going forward.
- Draft the **withdrawal letter** the auditor would send if management refused to accept the disclaimer in Pattern 4 and insisted on an unmodified opinion.
