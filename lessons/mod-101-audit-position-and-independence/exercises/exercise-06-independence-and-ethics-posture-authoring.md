# exercise-06: Authoring an Independence and Ethics Posture Statement for an AI Engagement

**Estimated effort:** 2 hours

## Objective

Author a signed independence-and-ethics posture statement for a complex AI assurance engagement with multiple threats across all five IFAC threat categories. The deliverable must be defensible under firm QA review, accreditation-body surveillance, and audit-committee scrutiny.

## Prerequisites

- Chapter [`08-independence-and-ethics-posture.md`](../08-independence-and-ethics-posture.md)
- Chapters [`05-iaasb-and-aicpa-attestation-stack.md`](../05-iaasb-and-aicpa-attestation-stack.md) and [`06-iso-19011-17021-and-42006.md`](../06-iso-19011-17021-and-42006.md) for engagement-framework context
- Headline reading of: IESBA International Code of Ethics (independence sections); AICPA ET §1.200 (independence) or IIA 2024 Standards Domain II (as applicable); ISO/IEC 17021-1 clause 5.2 (impartiality)

## Scenario

**Westmount Advisory LLP** — your fictitious US + UK professional-services firm — has been engaged to perform a reasonable-assurance report under ISAE 3000 (Revised) on management's AI governance program at **Parallax Semantics Ltd.**, a GPAI provider publishing a frontier LLM. Subject matter: Parallax's model-safety program during the period 1 Jan – 30 Jun 2027, against criteria that crosswalk Parallax's internal policy to the GPAI Code of Practice obligations the company has adopted and the NIST AI RMF 1.0 GenAI Profile.

Facts the engagement lead has surfaced during acceptance:

1. **Prior consulting.** Westmount's UK advisory practice provided a 9-month engagement during 2025-2026 helping Parallax design its model-safety governance structure (policy taxonomy, AI governance committee charter, escalation routing). Deliverables were published to Parallax in January 2026. The attestation subject matter now includes the operation of structures the advisory engagement helped design.
2. **Eval tooling provenance.** Westmount's US assurance innovation team maintains an open-source LLM-evaluation harness (fork of a public project) that Parallax's safety team uses in production. One Westmount engineer is a co-maintainer of the fork and has contributed configurations the Parallax team adopts.
3. **Retainer.** Parallax has a $6M/year open advisory retainer with Westmount for AI policy and regulator-engagement support. The attestation engagement is budgeted at $1.1M.
4. **Repeated engagement.** This is the third successive annual attestation. The engagement partner has signed the two prior reports and is proposed to sign this one.
5. **Client market power.** Parallax is one of six global frontier-model labs and is the largest Westmount client in the AI sector by revenue.
6. **Regulator-facing advocacy.** Westmount's Policy team has co-signed a public submission to the EU AI Office with Parallax on GPAI Code of Practice implementation during the current engagement period.
7. **Family relationship.** One of the proposed engagement-team seniors is the sibling of a Parallax ML engineer who works on the safety-classifier stack (not the model team being audited directly, but adjacent).
8. **Written representations history.** In the prior-year engagement, Parallax's safety lead delayed signing written representations by 6 weeks over disputed language, and verbally pressured the engagement team to soften a finding during the closing meeting.
9. **Auditor's expert.** Westmount proposes to use an external red-team methodology expert. The expert formerly worked at Parallax as a safety-eval engineer, ending employment 11 months before the engagement commencement date.

## Deliverables

### 1. Independence-and-ethics posture statement (~2,000 words, Markdown)

Follow the skeleton in chapter 8 and expand:

- **Engagement framework and governing ethics codes** — name all codes applicable (IESBA + AICPA depending on signing office + IIA Standards if any internal-audit-outsourcing component + ISO 17021-1 if any CB overlap) and name the most-restrictive overlay you are applying.
- **Threats identified** — for each of the five IFAC threats, enumerate the specific fact patterns from the scenario that trigger the threat. **Every one of facts 1-9 above must appear in this section**, tagged to the threat(s) it triggers.
- **Safeguards applied** — for each identified threat, name the firm-level, engagement-level, individual-level, and AI-specific safeguards. Where a safeguard is not sufficient, say so.
- **Residual threats accepted** — threats that remain above a trivial level after safeguards. For each, defend acceptance or say the engagement should be declined (you may decide the engagement is not acceptable for part or all of the subject matter; state the decision and the basis).
- **Decisions and recommendations to the engagement acceptance committee** — accept / accept with scope adjustment / decline, with specific basis.
- **Professional-skepticism commitment** — operating cues the team will follow, with AI-specific detail.
- **Signatures block** — placeholder lines for engagement lead, engagement partner, EQR partner (because this is a reasonable-assurance engagement), each team member, each auditor's expert.

### 2. Disclosures memo to those charged with governance (~500 words, Markdown)

The parallel memo that goes to the Parallax audit committee and board disclosing the residual threats you are accepting, the safeguards in place, and the basis for concluding the auditor can still issue an independent report. Written in a shape the audit committee would actually read.

### 3. Engagement-acceptance decision (~200 words)

A short recommendation to Westmount's engagement acceptance committee — accept, accept with specific scope adjustments (naming them), or decline. Defend the decision with explicit reference to the IESBA / AICPA / IIA independence requirements, naming specific threats and why safeguards are or are not sufficient.

## Starter guidance

- Fact 1 (prior consulting on the subject matter) is the hinge — you must have a defensible position on whether the attestation can proceed at all, or only after a cooling-off period, or only with a scoped-out subject matter.
- Fact 2 is subtler than it looks — contributing configurations to a tool the client runs can be a self-review threat on the attestation of the outputs of that tool, even if the tool itself is open source. Think through it carefully.
- Fact 3 is about commercial pressure; apply the IESBA / AICPA fee-dependence considerations and name any fee-dependence threshold your firm policy sets.
- Fact 4 triggers partner rotation under firm policy and under IESBA IISA rotation requirements for public-interest entities; GPAI providers may or may not be a PIE depending on jurisdiction — note the ambiguity.
- Fact 6 is advocacy; think through whether the Policy team's advocacy is severable from the engagement team.
- Fact 7 is familiarity at the individual level; the cooling-off and reassignment options are standard.
- Fact 8 is intimidation; name the firm's whistleblower / escalation route explicitly.
- Fact 9 is auditor's-expert independence — 11 months of separation is short; name the firm's typical required separation window and whether this expert can serve.
- Do NOT fabricate IESBA / AICPA / IIA clause numbers. Where you need to cite, cite accurately or mark `needs-research`.
- Write defensively but honestly — if the engagement should be declined, say so. The exercise accepts "decline" as a valid outcome if the posture statement defends it.

## Acceptance criteria

The deliverables are accepted when:

- Every one of facts 1-9 is addressed under at least one of the five threats in the posture statement.
- Safeguards are mapped to specific threats; blanket safeguards that do not address a specific threat are not credited.
- Residual threats are named explicitly; no threat is silently assumed to be eliminated.
- Engagement-acceptance decision is a specific recommendation (accept / adjust scope / decline) with a defended basis.
- Disclosures memo would be readable by a non-auditor audit-committee member; it does not hide the threats.
- Posture statement names a professional-skepticism commitment with at least four AI-specific operating cues.
- No clause of any ethics code is invented; unverified citations are marked `needs-research`.

## Stretch goals

- Author a **parallel posture statement for the alternative framework** — rewrite the posture statement assuming the engagement is an ISO/IEC 42001 certification audit at a CB (ISO/IEC 17021-1 + ISO/IEC 42006) instead of an ISAE 3000 attestation; note the ten largest differences.
- Produce a **what-if-facts-change log** — for each of facts 1-9, write one sentence describing how the posture would change if the fact's magnitude moved (e.g., prior consulting was 3 years ago instead of 1; retainer was $500K/year instead of $6M).
- Draft the **firm's internal escalation note** that would go to the general counsel if, after acceptance, the engagement team encountered a fact that re-triggered a previously mitigated threat — in a form the general counsel's office would route through engagement-quality-review processes.
