# The IIA Three Lines Model and the Global Internal Audit Standards

## Motivation

If you execute even one engagement under the IIA banner — internal audit, co-sourced internal audit, or any engagement whose client expects "IIA-compliant" assurance — you are making a conformance claim against **mandatory** IIA guidance. A regulator, external-auditor peer, or audit-committee chair can and will ask "where in the Standards is that?" The answer has to be on the tip of your tongue. This chapter internalises the two pieces of IIA guidance you must know cold: the **Three Lines Model** (2020 revision) and the **Global Internal Audit Standards** (2024, effective 9 January 2025), including how the 2024 Standards reorganise what used to be called the IPPF.

## The Three Lines Model (2020 revision)

The IIA published the **Three Lines Model** in July 2020, replacing the 2013 "Three Lines of Defense" model. The headline changes you need to be able to recite:

1. **Renamed from "defense" to "lines"** to reflect that the model is about governance and value, not purely defensive risk mitigation.
2. **Governing body** (board / audit committee) is explicit at the top, with **management** and **internal audit** as the two operating pillars underneath it.
3. **Management** is split into:
   - **First line** — those who own and manage risks directly (operational managers delivering products and services, including the engineers building AI systems).
   - **Second line** — expertise, support, monitoring, and challenge on risk-related matters (risk, compliance, quality, model risk, safety, ethics). The second line is NOT independent — it reports into management.
4. **Internal audit** is the **third line** — independent assurance and advice to the governing body and senior management on the adequacy and effectiveness of governance and risk management.
5. **External assurance providers** are shown outside the three lines — regulators, external auditors, notified bodies, certification bodies — and the model acknowledges reliance can run both ways.
6. Six **principles** govern the model: governance; governing body roles; management + first-and-second-line roles; third-line roles; independence of internal audit; and creating + protecting value.

For AI work the model is read with one adaptation: AI governance in most organisations has layered second-line functions (AI ethics committee, model risk management, AI release assurance, AI compliance), and the third-line auditor has to resolve overlap. The resolution is always the same — the second line can be structured however it likes; the third line audits whether whatever is structured actually works.

## From the 2017 IPPF to the 2024 Global Internal Audit Standards

The IIA's professional-practices framework has two eras you must distinguish:

- **IPPF (International Professional Practices Framework)** — the structure in place through 2024. Composed of **mandatory guidance** (Core Principles, Definition of Internal Auditing, Code of Ethics, International Standards for the Professional Practice of Internal Auditing) and **recommended guidance** (Implementation Guidance, Supplemental Guidance including the Global Technology Audit Guides / GTAGs and Practice Guides).
- **Global Internal Audit Standards (2024)** — released January 2024, **effective 9 January 2025**. These consolidate and restructure the IPPF mandatory elements into a single set of Standards organised into **five Domains** and **fifteen Principles** (Domain I Purpose; Domain II Ethics and Professionalism; Domain III Governing the Internal Audit Function; Domain IV Managing the Internal Audit Function; Domain V Performing Internal Audit Services). The Code of Ethics and the definition of internal auditing are folded into the Standards themselves rather than sitting alongside them.

In authoring an audit opinion today you **cite the 2024 Standards**. Legacy workpapers, templates, and third-party references may still cite the pre-2024 IPPF; part of the work at level 45 is being fluent enough in both to map between them.

### Mandatory structure — what you must do

The 2024 Standards are organised around:

- **Purpose of Internal Auditing** — a single statement at the top of Domain I.
- **Ethics and Professionalism (Domain II)** — Integrity, Objectivity, Competency, Due Professional Care, Confidentiality. (These replace the old Code of Ethics.)
- **Governing the Internal Audit Function (Domain III)** — board / audit-committee oversight of the function, independence of the CAE, approval of the internal audit charter.
- **Managing the Internal Audit Function (Domain IV)** — CAE responsibilities: strategic plan, risk-based audit plan, resourcing, QA + improvement program, coordination with other assurance providers.
- **Performing Internal Audit Services (Domain V)** — engagement planning, engagement supervision, performing engagement work (evidence, analysis, documentation), communicating engagement results, monitoring + follow-up.

When an audit finding is challenged by management, you answer in the shape: *this Standard, this Principle, this Requirement, this Consideration for Implementation* — not from memory of "best practice".

### Recommended guidance that still matters for AI work

The IIA continues to publish **Topical Requirements** (new under the 2024 Standards framework), **Practice Guides**, and the historical **Global Technology Audit Guides (GTAGs)**. For an AI engagement, two Practice Guides are essential background:

- **IIA Artificial Intelligence Auditing Framework** — published 2017 in three parts (AI Overview, AI Risks, Assessing the Risks) — remains the IIA's canonical "how to think about auditing AI" document. Covered in [`03-iia-ai-auditing-framework.md`](03-iia-ai-auditing-framework.md).
- **IIA guidance on Internal Audit's Role in Governance of AI** — newer guidance published after the 2024 Standards to explicitly position internal audit across the AI-governance landscape. <!-- needs-research: confirm the exact title and publication year of the IIA "Internal Audit's Role in Governance of AI" document as cited in the AI-auditor track learning objectives — IIA titling has shifted between "AI Auditing Framework" and more recent AI Topical Requirements -->

## The 2024 Standards in practice — what changes day-to-day for an AI Auditor

Four operational shifts relative to the 2017 IPPF that directly affect AI engagements:

1. **Explicit stakeholder-engagement requirements.** Domain IV requires the CAE to actively engage the board and senior management on strategy and risks; at engagement level, Domain V tightens requirements for communicating with engagement clients during performance of the engagement — not just in the closing meeting. For an AI audit this means early engagement with first-line AI engineering, second-line ML-risk / release-assurance, and the AI ethics committee is now a Standards requirement, not a courtesy.
2. **Explicit requirement to use technology.** The 2024 Standards explicitly require the function to use appropriate technology in performing audit work. For AI auditors this closes the loop — data-analytics, continuous audit, log replay, and independent eval re-runs are no longer "modern practice", they are the default conformance posture.
3. **Topical Requirements.** The IIA introduced "Topical Requirements" — mandatory audit coverage expectations by subject area (the inaugural Topical Requirement covered cybersecurity). Future Topical Requirements for AI are expected. <!-- needs-research: check whether IIA has released an AI-specific Topical Requirement at the time of the student's reading; the inaugural Topical Requirement covered cybersecurity in 2024 but IIA has signalled AI as a future topic -->
4. **Strengthened quality-assessment expectations.** The CAE's **Quality Assurance and Improvement Program (QAIP)** — internal + external QA — remains mandatory, with external assessment at least every five years. For AI audits, a QAIP reviewer will look for defensible sampling of model/data artifacts, reproducibility of independent replications, and auditor-expert documentation under the specialist provisions.

## The "cite the Standard" discipline

When you write the audit report and — more importantly — when you negotiate management response, every assertion the auditor makes should track back to one of three sources:

- **Criterion** = the thing being audited against (ISO/IEC 42001 clause X, NIST AI RMF function Y, EU AI Act Article Z, firm policy A).
- **Methodology authority** = the Standard that authorises you to audit that way (IIA 2024 Standards Principle / Requirement, ISAE 3000, AT-C 105, ISO 19011, ISO/IEC 17021-1).
- **Evidence** = the artifact you tested and the test you performed.

A finding without all three is weak; management response can and will exploit the gap. This chapter installs the second of the three — the methodology authority — for internal-audit engagements. Chapters 5 and 6 install it for external-attestation and management-system-certification engagements.

## Example — defending an AI audit opinion under review

Scenario: the audit committee pushes back on a finding that the organisation's LLM red-team program does not cover adversarial prompt injection from indirect sources (retrieved content, tool outputs). Management argues the finding is "outside the scope of internal audit's mandate because it's engineering judgment."

The right structure of response:

- **Conformance anchor**: IIA Global Internal Audit Standards Domain V Principle on Performing the Engagement — the engagement objectives include the adequacy and effectiveness of controls over the risks identified. Red-team coverage is a control; coverage gaps are an engagement finding.
- **Criterion anchor**: the organisation's own AI risk register identifies indirect prompt injection as an in-scope risk, and the AI policy references OWASP LLM Top 10 — LLM01 is prompt injection including indirect variants.
- **Evidence anchor**: workpapers show (a) the red-team suite configuration reviewed, (b) the specific attack families absent, and (c) the control owner's confirmation in interview.
- **Independence anchor**: the engagement was performed by auditors with no first-line involvement in the red-team suite design; the engagement partner's independence declaration is on file.

That is what "defend the opinion under review" looks like — Standard citation + criterion citation + evidence citation + independence citation. The three-lines position and the IIA Standards together give you two of the four anchors for free.

## Summary

- The IIA **Three Lines Model (2020)** names the third line as independent assurance, with governing body and management + first/second lines above it; external assurance providers sit outside the model.
- The **2024 Global Internal Audit Standards** (effective 9 January 2025) replace the IPPF's structure with five Domains and fifteen Principles; cite these in current audit opinions.
- Day-to-day shifts for AI work: stakeholder engagement during performance, mandatory use of technology, Topical Requirements, and strengthened QAIP expectations.
- Every assertion in an IIA-governed AI audit opinion ties back to a **Standard, a criterion, and evidence** — this is the structure that survives review by the audit committee, external QA, and regulators.
