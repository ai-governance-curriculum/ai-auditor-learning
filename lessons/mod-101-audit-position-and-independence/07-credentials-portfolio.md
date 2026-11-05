# The AI-Auditor Credentials Portfolio

## Motivation

A level-45 AI Auditor rarely holds one credential — the role spans IIA, ISACA, IAASB/AICPA, and ISO stacks, and the market has produced a credentials portfolio to match. Buyers (CAEs hiring for internal AI audit practice leads; Big-4 partners staffing an AI assurance engagement; certification bodies maintaining an accredited auditor roster; sector regulators approving independent validators) each read a specific subset of credentials as load-bearing. Holding the wrong credentials for the engagement is as disqualifying as holding none. This chapter positions the credentials market and gives you the defensible combinations for each engagement type.

## The credentials landscape, in one map

The credentials fall into four groups:

### Internal-audit profession (IIA)

- **CIA — Certified Internal Auditor.** The IIA's anchor credential. Three-part exam (Essentials of Internal Auditing; Practice of Internal Auditing; Business Knowledge for Internal Auditing). Required or strongly preferred for internal audit roles in most medium-to-large organisations.
- **IIA AI-specific certificate** — the IIA has published AI-audit-specific credential offerings (names and exact structure have evolved; the student must cite the live offering). <!-- needs-research: confirm the current title, format, and prerequisite of the IIA's AI-audit credential as of reading time — the IIA has issued AI Auditing-related certificates and Topical Requirement-tied credentials during 2023–2026 -->
- **QIAL — Qualification in Internal Audit Leadership** (where available; its availability has changed over time). CAE-track credential; not the typical AI auditor path. <!-- needs-research: confirm current QIAL availability at reading time; the IIA has restructured its leadership-level credentials -->

### IT-audit profession (ISACA)

- **CISA — Certified Information Systems Auditor.** ISACA's anchor credential; the dominant IT-audit credential globally.
- **AAIA — Advanced in AI Audit.** ISACA's AI-specialisation credential. Prerequisite: current CISA (or qualifying equivalent). Launched 2024. See [`04-isaca-auditing-ai-and-aaia.md`](04-isaca-auditing-ai-and-aaia.md).
- **CISM, CGEIT, CRISC, CDPSE** — adjacent ISACA credentials (security management, enterprise IT governance, risk and information systems control, data privacy solutions engineer). Not required for AI audit specifically but frequent in a portfolio.

### AI-governance / AI-ethics profession

- **IAPP AIGP — Artificial Intelligence Governance Professional.** International Association of Privacy Professionals credential launched 2024. Covers AI governance across the IAPP body of knowledge (AI foundations, AI governance implementation, AI risk management, laws and standards, AI ecosystems).
- **IAPP CIPP (-E / -US / -A / -C) + CIPM + CIPT** — privacy credentials from IAPP that frequently appear alongside AIGP when privacy overlap dominates (GDPR Article 22, HIPAA-regulated AI, Colorado AI Act).
- **ForHumanity — FHCA / Fellow + IAAIS auditor certification.** ForHumanity Center for AI runs an independent auditor credentialing scheme and publishes audit schemes (criteria libraries) for specific AI laws and frameworks (e.g., NYC LL144, Colorado AI Act, EU AI Act readiness). Practitioners auditing under a ForHumanity scheme hold the credential required by that scheme. <!-- needs-research: the ForHumanity credential structure has been revised; confirm whether the current practitioner credential is "FHCA" or a successor name, and which audit schemes are actively published at reading time -->
- **BABL AI — Algorithm Bias Auditor / Certified Auditor.** BABL AI operates a dedicated credential for algorithmic bias auditors, notably used in NYC LL144 bias audits. <!-- needs-research: BABL AI has published multiple auditor credentials; confirm the current nomenclature and scope at reading time -->

### ISO/IEC 42001 management-system audit profession

- **ISO/IEC 42001 Lead Auditor.** Training-and-certification offering from independent training organisations (PECB, BSI, DNV, SGS, Bureau Veritas, IRCA-accredited providers). Required for lead-auditor placements on CB rosters executing 42001 certification audits.
- **ISO/IEC 42001 Lead Implementer.** Implementer-track variant — the practitioner is positioned to help an organisation design and implement an AIMS rather than audit one. Important distinction: an auditor who holds **only** the Lead Implementer credential should not be the lead auditor on the same client's certification engagement (self-review threat).
- **IRCA / Exemplar Global / NRCMSA auditor registrations** — personnel registration schemes that a certification body's auditors register under, independent of the training provider.

### External-assurance profession

- **Qualified accountant / CPA (US), CA (UK/CA/AU/NZ), equivalent.** Required for signing-partner / signing-senior-manager roles on IAASB / AICPA attestation engagements (ISAE 3000, AT-C 105 / AT-C 205 work). Not required for every team member but required for the engagement partner.
- **CPA licensure in good standing** plus **PCAOB registration** where the firm performs PCAOB-regulated work.

## Which combinations are load-bearing for which engagement type

The practical question at level 45: given an engagement, what credentials must the engagement lead and the team hold for the report to be defensible under the relevant oversight body's review?

### Engagement type 1 — Internal AI audit inside an organisation

- **Engagement lead**: CIA (IIA's anchor) **required**; **AAIA** (or equivalent AI-audit certification) **strongly preferred**; IT-general-controls subject matter → add **CISA**; privacy-heavy use case → add **IAPP CIPP + AIGP**.
- **Audit committee / CAE buyer signal**: CIA is the first-order signal; AAIA + AIGP demonstrate AI-specific preparation; IIA Topical Requirements compliance.
- **Independence note**: licensure by itself does not establish independence — see `08-independence-and-ethics-posture.md`.

### Engagement type 2 — ISO/IEC 42001 certification audit at a certification body

- **Lead auditor**: **ISO/IEC 42001 Lead Auditor** training-and-registration **required**; **IRCA / Exemplar Global registration** at the CB's accepted body **required**; underlying competence in auditing management systems (frequently demonstrated by **ISO 9001 or 27001 Lead Auditor** background prior to 42001) **expected**.
- **Audit team member**: ISO/IEC 42001 Lead Auditor or Internal Auditor training; technical experts under 17021-1 clause 7 may hold AI-engineering credentials in place of auditing credentials, with the lead auditor retaining the audit judgment.
- **Buyer signal**: the CB's accreditation body (UKAS, ANAB, DAkkS) tests this in CB surveillance; the holder's credentials appear in the CB's auditor roster.
- **Independence note**: Lead Implementer credential **does not** substitute, and in combination with the same engagement raises a self-review threat (see chapter 8).

### Engagement type 3 — ISAE 3000 / AT-C 205 external attestation (e.g., SOC for AI, bespoke AI-assurance report)

- **Engagement partner**: **CPA (US) / CA / qualified accountant** **required**; **CISA** on partners managing the IT-audit sub-engagement **expected**; **AAIA** or equivalent AI-audit specialisation **strongly preferred**.
- **Audit team**: mix of CISA + AAIA for the IT/AI subject matter, with ISA 620 auditor's experts for ML engineering, evaluation methodology, red-team methodology as needed.
- **Buyer signal**: partner credentials, firm quality-management system (ISQM 1 / QM 1) in place, ISAE 3000 / AT-C 105 report issued on firm letterhead.

### Engagement type 4 — EU AI Act Article 43 third-party conformity assessment at a notified body

- **Auditor**: competence per the notified-body designation requirements (evolving, implementing acts in progress). Expect a combination of ISO/IEC 42001 Lead Auditor + AI-specific technical competence (demonstrated by AAIA / AIGP / specific engineering background in the AI subject matter) + conformity-assessment-body credential background. <!-- needs-research: cite the implementing act or EU AI Office guidance that pins the specific notified-body auditor competence requirements at reading time; the Article 43 / 44 implementing acts were under development alongside Article 16-29 obligations at authoring time -->
- **Buyer signal**: notified-body designation under the EU AI Act, plus the body's accreditation at a national accreditation body.

### Engagement type 5 — NYC LL144 bias audit

- **Auditor**: an independent entity meeting the LL144 "independent auditor" definition. Common portfolios: **BABL AI** credential, **ForHumanity** IAAIS-equivalent + the NYC LL144 audit scheme, or a Big-4 team under an ISAE 3000 / AT-C engagement. <!-- needs-research: NYC DCWP has released additional guidance on LL144 "independent auditor" scoping since the law took effect; confirm the current interpretation at reading time -->
- **Buyer signal**: the published bias-audit summary identifies the auditor; employers under LL144 rely on it for their compliance posture.

### Engagement type 6 — SR 11-7-aligned independent model validation for a bank

- **Validator**: historically, candidates hold **FRM (Financial Risk Manager)** or **PRM (Professional Risk Manager)**, plus **CFA**, plus (for AI/ML specifically) **CISA + AAIA** or strong ML-engineering background. Independence is achieved by being outside the bank's first-line (model-owner) and second-line (MRM) functions.
- **Buyer signal**: validator credentialing is tested by bank-regulator examiners (Fed, OCC, FDIC) during SR 11-7 / OCC 2011-12 / SR 23-4 exam work.

### Engagement type 7 — FDA GMLP + PCCP audit for AI/ML SaMD

- **Auditor**: audit experience in medical-device regulation (21 CFR 820 / ISO 13485 lead-auditor credential) + AI/ML specialisation. Many practitioners hold **Lead Auditor ISO 13485** + **Regulatory Affairs Certification (RAC)** + AI-specific certifications on top. <!-- needs-research: FDA GMLP guiding principles and PCCP guidance are being finalised; confirm the current regulatory position at reading time -->

## The portfolio-shape heuristics

When advising someone building toward this role, four heuristics:

- **Hold one credential from each primary profession** you intend to practise in. Internal-audit profession: CIA. IT-audit profession: CISA (with AAIA on top for AI). ISO management-system profession: 42001 Lead Auditor (if certification-body work is in scope). External-assurance profession: CPA / CA (if public-practice attestation is in scope).
- **Add AI-specialisation credentials on top** of whichever anchor credentials you hold — AAIA, AIGP, ForHumanity IAAIS credential, BABL AI credential — picking the ones that match the engagement types you take on.
- **Credentials do not substitute for engagement-level independence.** The chapter on independence (`08-independence-and-ethics-posture.md`) lives on top of credentials, not below them.
- **CPD / CPE discipline.** Every credential has continuing-education requirements; letting a credential lapse while signing engagements that depended on it is a QA finding on the engagement and, potentially, a disciplinary matter with the credentialing body.

## Example — defending a credentials portfolio for a target role

Scenario: an AI Auditor is targeting a senior-manager role in a Big-4 AI assurance practice, with an engagement portfolio of SOC for AI (AT-C 205), ISO/IEC 42001 pre-certification readiness, and NYC LL144 bias audits.

Defensible portfolio:

- **CPA** (US) — required for sign-off on AT-C work.
- **CISA** — IT-audit anchor expected by the firm and relevant partners.
- **AAIA** — AI-audit specialisation signal, launched 2024, already becoming market-expected.
- **IAPP AIGP** — AI-governance vocabulary for client conversations, overlaps with LL144 risk framing.
- **ISO/IEC 42001 Lead Auditor** — enables the 42001 readiness engagement portfolio; declines into pre-certification advisory (not certification body work).
- **ForHumanity practitioner credential** or **BABL AI credential** — specialisation for LL144 bias audits (pick the one the firm has a published partnership with; firm policy often dictates).

Defending that to a hiring partner: CPA signs the attestation, CISA + AAIA cover the IT and AI subject-matter authority, AIGP signals governance fluency, 42001 Lead Auditor opens the AIMS pre-cert market, and the bias-audit credential specialises to LL144. Six credentials, each justified by a specific engagement type.

That is the depth and shape the role expects. Picking credentials without the engagement-type justification wastes effort — pick to the engagement list, re-evaluate as the engagement list evolves.

## Summary

- Credentials fall into four groups: IIA (internal audit), ISACA (IT audit), IAPP / ForHumanity / BABL (AI governance and specialist bias audit), ISO/IEC 42001 Lead Auditor (AIMS certification), plus the professional-accountant anchor (CPA / CA) for external attestation.
- The **load-bearing combination is engagement-type-specific**; there is no universal "right" portfolio.
- At level 45 expect to hold a multi-credential portfolio that spans professions you practise across; never substitute credentials for engagement-level independence.
- Keep continuing-education / CPD current — lapsed credentials on a signing engagement are a reviewable finding.
