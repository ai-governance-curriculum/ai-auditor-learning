# exercise-01: Condition / Criterion / Cause / Effect / Recommendation Authoring

**Estimated effort:** 2 hours

## Objective

Convert a loose, unshaped finding note from engagement fieldwork into three distinct audit findings, each authored in the CCCER structure prescribed by IIA Global Internal Audit Standards and GAO Yellow Book §9.17. Each finding must be supported by named evidence, cross-referenced workpapers, and a defensible materiality claim.

## Prerequisites

- Chapter [`01-cccer-finding-authoring-with-evidence-and-materiality.md`](../01-cccer-finding-authoring-with-evidence-and-materiality.md)
- Reading access to:
  - IIA Global Internal Audit Standards (2024), in particular the Domain governing Communicating Engagement Results
  - GAO Government Auditing Standards (Yellow Book), 2024 revision — paragraphs 9.16–9.19
  - ISO/IEC 42001:2023 clauses referenced in the scenario
  - EU AI Act (Regulation (EU) 2024/1689), Articles 9, 10, 13, 14, 15
- `mod-104` chapters on evidence reliability and sampling
- `mod-102` chapter on criteria sourcing

## Scenario

You are the engagement lead on a Stage-2 ISO/IEC 42001 audit of **RoutelineCare**, a company providing an AI-enabled triage assistant to EU hospital emergency departments. The system (`triage-assist-v4.2`) ingests chief-complaint free text and structured vitals, and outputs an acuity-tier recommendation (ESI-equivalent 1–5) plus a short clinical rationale. The system is classified as high-risk under the EU AI Act Annex III (Annex III point 5 — access to health services) and as a Class IIa medical device under the MDR.

Fieldwork has produced these raw notes from a senior engagement auditor:

> **Raw fieldnotes (2027-02-14).** On the triage-assist audit: eval report says accuracy is high but I cannot find how they measured per-group accuracy. The data-governance lead showed me the training data pipeline — the labels come from historical triage decisions at the three partner hospitals, 2019–2023. Nobody has looked at whether the 2019–2020 labels have different distributions than 2022–2023. Oversight: the ED nurse is supposed to be able to override within 30 seconds of the recommendation appearing, but when I shadowed the floor, two nurses did not know they could override and one said she had "stopped checking because it's always right." Model card lists accuracy of 0.92 for overall acuity assignment but the number isn't broken out by age, sex, or presenting complaint category, which is odd for a high-stakes system. The organisation's AIMS Impact Assessment procedure AIMS-PROC-007 §5 says per-subgroup performance analysis is required for health-service systems before the annual re-authorisation. No one's done it. These seem like three separate findings — fairness-eval gap, data drift gap, override awareness. Oversight gap.

## Deliverables

### 1. Three CCCER findings (~500–700 words each)

Author three separate findings from the raw notes. Each finding must:

- Have a stable finding ID in the shape `AIMS-2027-S2-XX`.
- State the subject precisely (model name, version, deployment context, observation window).
- Have a Condition section that describes **what was observed** in neutral, factual language with workpaper cross-references (invent workpaper IDs in the form `[WP-###]` but describe what each would contain).
- Have a Criterion section that cites the specific authority and clause — compose from ISO/IEC 42001:2023, the EU AI Act Articles, and the organisation's own AIMS procedure. Where you cannot verify an exact clause citation, use `<!-- needs-research: ... -->` rather than guessing.
- Have a Cause section that is **structural, not personal**, supported by a brief cause-analysis narrative and a named workpaper.
- Have an Effect section that makes an **explicit materiality claim** per the four factors in chapter 1 (regulatory stake, harm channel and footprint, risk appetite, pattern) and names the ISO/IEC 17021-1 classification you propose.
- Have a Recommendation section that is **control-level**, addresses the cause, names a role owner, and is testable at follow-up without prescribing engineering design.

### 2. Workpaper trail index (~200 words)

For each finding, enumerate the workpapers that would sit behind it:

- Planning memo entry.
- Criterion memo.
- Evidence workpaper(s).
- Cause-analysis workpaper.
- Materiality memo.

State briefly what each workpaper would contain. You are not writing the workpapers; you are documenting the trail the reader could request.

### 3. Pre-close-out self-review checklist (completed)

Produce a completed checklist showing that each finding has passed your self-review against the checklist at the end of chapter 1. Where a check cannot pass, state why and what you would need.

## Starter guidance

- **Three findings, three structural causes.** The three findings should surface three different structural gaps, not three facets of one gap. If you catch yourself repeating cause language, you may have one finding with three symptoms.
- **Materiality claims must be testable.** "This could harm patients" is not a claim. "The system makes ~800 acuity recommendations per month in each partner ED; ESI miscategorisation at the critical tier has well-documented downstream morbidity consequences" is a claim with a footprint and a channel.
- **Watch the Cause/Effect inversion.** A finding whose effect is "the organisation cannot demonstrate compliance" has a cause that should be below that layer. "Cannot demonstrate" is often a symptom; dig.
- **Independence posture on Recommendation.** You are not permitted to prescribe that the organisation adopt a specific statistical method, use a particular vendor, or re-architect the model. You are permitted to require that a control exist with a testable output.
- **Do not invent regulation.** Where a specific clause citation is beyond your verifiable knowledge, mark `needs-research` and move on; a finding with `needs-research` on a citation is still usable at Stage 2 feedback.

## Acceptance criteria

The deliverables are accepted when:

- Each of the three findings fills all five CCCER elements with the content discipline described in chapter 1.
- Condition statements name the model, version, environment, and observation window, and reference workpapers.
- Criterion statements cite ISO/IEC 42001, EU AI Act Articles, and / or the organisation's AIMS-PROC-007 at clause level (or carry `needs-research` where unverified).
- Cause statements are structural; no finding names an individual engineer or clinician as the cause.
- Effect statements make the four-factor materiality claim explicit and propose an ISO/IEC 17021-1 classification (major / minor / observation / OFI) with reasoning.
- Recommendation statements address cause rather than condition, remain at the control level, name a role owner, and are testable at follow-up.
- The workpaper trail index enumerates at least five workpaper references per finding with content descriptions.
- The self-review checklist passes for each finding or clearly marks what is missing.
- No citation is invented; unverified citations carry `needs-research`.

## Stretch goals

- Write a **before/after pair** for a fourth finding of your own choice drawn from the scenario, showing the unshaped field-note language and the CCCER version side by side.
- Produce the **close-out meeting walk-script** (~300 words) that the engagement lead would use to present these three findings to RoutelineCare's management — neutral tone, finding-by-finding, with a short script for handling the predictable pushback ("the eval report was adequate at launch").
- Draft the **materiality-memo text** (~400 words) for the finding you consider most material — explicitly working the four factors (regulatory stake, harm channel and footprint, risk appetite, pattern) with reasoning that would hold in an audit committee or notified-body challenge.
- Pair-review a peer's three findings against the acceptance criteria and write a brief review memo identifying one strength and one gap per finding.
