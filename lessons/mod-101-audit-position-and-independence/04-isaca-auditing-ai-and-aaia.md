# The ISACA Auditing AI Body of Knowledge and the AAIA Credential

## Motivation

In regulated-industry internal-audit departments — banks, insurers, healthcare systems, utilities, public-sector bodies — the technology-audit and IT-general-controls craft is overwhelmingly ISACA-trained, not IIA-trained. Any AI audit that touches technology general controls, change management, access management, data pipelines, cloud, or integration will be read by ISACA-credentialed reviewers. The IIA Framework gives you the governance-audit vocabulary; ISACA gives you the IT-audit vocabulary. You need both. This chapter installs ISACA's **Auditing Artificial Intelligence** body of knowledge and positions the **AAIA (Advanced in AI Audit)** credential as the ISACA-side complement to the IIA frame.

## The ISACA frame, in short

ISACA — historically the Information Systems Audit and Control Association — anchors the **IS audit** and **IT governance** professions through:

- **COBIT** — the Governance and Management Framework for Enterprise IT (COBIT 2019 revision in use at the time of authoring). Objective-based controls across governance and management of enterprise IT.
- **ITAF** — IT Audit Framework. ISACA's professional-practice standard analogue to the IIA Standards for IT auditors.
- **CISA (Certified Information Systems Auditor)** — the anchor credential. Required for most regulated-industry IT-audit roles and widely cited in external-audit firm hiring rubrics.
- **CISM, CGEIT, CRISC, CDPSE** — adjacent IT risk / governance / privacy credentials.

In AI audit, ISACA extends this with:

- **Auditing Artificial Intelligence** — ISACA's published white paper / audit program on AI audit. <!-- needs-research: confirm the current title, edition, and year of ISACA's "Auditing Artificial Intelligence" publication at reading time — ISACA has refreshed AI-audit publications across 2018–2026 -->
- **AAIA (Advanced in AI Audit)** — ISACA's advanced credential launched in 2024 for experienced IS auditors specialising in AI. The credential requires a current CISA (or other qualifying credential) as a prerequisite. <!-- needs-research: confirm current eligibility prerequisites and domain breakdown of AAIA at reading time -->

## The ISACA Auditing AI body of knowledge — what it covers

Read the ISACA AI audit program as a **controls-and-testing manual** keyed to the IT-audit mental model. Where the IIA Framework talks in governance-risk language, ISACA talks in control-and-test language. Expect coverage of:

- **AI governance controls** — AI strategy approval, ethics committee charter, policy library, roles and responsibilities. Audit test: existence, approval, communication, operation.
- **AI data controls** — data sourcing, quality, bias testing, privacy, retention, disposal. Audit test: data lineage walkthroughs, sample checks against the data policy.
- **AI model controls** — model selection, training, validation, deployment approval, change management, decommissioning. Audit test: inspect model inventory, re-perform sample model deployments against approval records.
- **AI operation controls** — monitoring (drift, fairness, accuracy), incident response, continuous validation. Audit test: review monitoring configuration, re-perform sample incident post-mortems.
- **AI security controls** — adversarial robustness, data poisoning resistance, model-extraction resistance, prompt injection, supply-chain integrity. Audit test: coverage review against MITRE ATLAS / NIST AI 100-2 / OWASP LLM Top 10.
- **AI regulatory alignment** — jurisdictional regulatory posture. Audit test: traceability from regulatory obligation to control to evidence.
- **Third-party AI controls** — vendor due diligence, SOC / ISO / IAAIS reliance, contract terms. Audit test: vendor inventory against AI usage, review of reliance decisions.

The structure maps cleanly to COBIT **governance** vs. **management** objectives, which is how ISACA-trained peers will read your workpapers. Where possible, cross-tag AI audit controls to the specific COBIT objectives they align to (EDM, APO, BAI, DSS, MEA families) — reviewers from the IT-audit side will accept that language faster than they will accept bespoke AI vocabulary.

## When ISACA is the primary frame, not the complement

In some departments and engagements, the ISACA frame is the **primary** professional authority and IIA is the complement:

- **Bank IT audit** functions are often jointly IIA- and ISACA-anchored, with the technology-audit subgroup (including AI audit) running primarily on ITAF + COBIT + SR 11-7. The AI auditor in that group typically holds **CISA + AAIA + CIA** (IIA) and reaches for IIA Standards for governance findings and ITAF for IT-general-control findings.
- **Public-sector IT audit** (US federal, EU national-audit institutions) similarly leans ISACA, with IIA Standards layered on for the audit-function governance. Yellow Book / GAGAS adds yet another layer for US federal audit work.
- **External IT audit for financial statements** — Big-4 audit teams supporting the financial-statement audit of AI-using organisations execute under PCAOB / IAASB financial-statement-audit standards, but the IT-audit sub-engagement is heavily ISACA-trained.

The engagement letter and workpaper structure should name which frame is primary. An AI audit workpaper that says only "performed per IIA Standards" in a department that otherwise lives in ITAF will be flagged by internal QA.

## COBIT cross-tagging, in practice

Illustrative cross-tag examples auditors actually write up:

- AI model change management → **BAI06 Managed IT Changes** and **BAI07 Managed IT Change Acceptance and Transitioning**.
- AI monitoring and incident response → **DSS01 Managed Operations**, **DSS02 Managed Service Requests and Incidents**, **MEA01 Managed Performance and Conformance Monitoring**.
- AI third-party management → **APO10 Managed Vendors**, **APO14 Managed Data** (where the vendor supplies data).
- AI governance committee → **EDM01 Ensured Governance Framework Setting and Maintenance**, **EDM02 Ensured Benefits Delivery**.

<!-- needs-research: ISACA has published or signalled COBIT-plus-AI mappings — confirm the current title and reference at reading time rather than relying on these illustrative tags -->

## The AAIA credential — what it signals

The **Advanced in AI Audit (AAIA)** credential sits above CISA as a specialisation. What it signals to a buyer:

- **The holder has a current CISA** (the IS audit anchor) or equivalent prerequisite credential.
- **The holder has demonstrated AI-audit-specific knowledge** across domains that typically include AI governance and risk, AI operations and controls, and auditing AI tools and techniques.
- **The holder commits to the ISACA Code of Professional Ethics** and the Continuing Professional Education policy.

What it does **not** signal:

- It is not a certification of auditor independence — that is a separate, engagement-by-engagement assertion.
- It is not an engineering credential — it does not certify the holder to author ML / LLM evaluation methodology.
- It is not interchangeable with the IIA AI Audit certificate or the ForHumanity IAAIS credential; they credential different frames.

Expect buyers in regulated-industry IT-audit departments to require AAIA (or equivalent) for the AI-audit lead on an engagement; expect Big-4 AI-assurance practices to require AAIA plus one of the external-assurance credentials (CPA for AT-C work in the US, chartered-accountant status elsewhere) for signing partner / senior-manager roles.

## Example — using the ISACA frame to structure an AI audit of a vendor-provided LLM

Scenario: a US regional bank is implementing a third-party-hosted LLM to summarise internal customer-service notes. The AI auditor runs the engagement from an ISACA-primary posture.

- **Audit universe entry** per ISACA Auditing AI: AI system inventory, with vendor flag (third-party AI), use case (summarisation), data classification (customer confidential).
- **COBIT anchors** cited in the audit program: APO10 (vendor), APO13 (security), BAI06 (change), DSS01/DSS02/DSS04 (operations, incidents, continuity), MEA01 (monitoring and conformance).
- **AI-specific controls** keyed off ISACA Auditing AI: AI governance approval (CIO+CRO sign-off, AI ethics committee record), model documentation review (vendor model card, SOC 2 Type II or ISO/IEC 42001 certificate), prompt-and-response logging, data-leak prevention, incident-notification SLA with vendor, model-drift monitoring, fairness/accuracy sampling.
- **Testing** performed against each: inspection, observation, inquiry, re-performance where practical.
- **Workpapers** cross-tagged to COBIT and to ISACA Auditing AI control areas so peer QA reviewers (CISA / AAIA) can navigate the workbook without a bespoke orientation.

That engagement lands cleanly in an ITAF-primary department and is readable by ISACA-trained peers — exactly what you want when the AI audit is internally reviewed as part of the bank's annual IT audit plan.

## Summary

- **ISACA** provides the IT-audit frame most regulated-industry internal audit departments use; COBIT + ITAF + CISA is the baseline language.
- **ISACA Auditing Artificial Intelligence** provides the AI-audit controls-and-testing manual; cross-tag to COBIT governance and management objectives when the department is ISACA-primary.
- The **AAIA (Advanced in AI Audit)** credential signals AI-audit specialisation for CISA-anchored IT auditors.
- Use the IIA frame + ISACA frame together: IIA for the audit-function governance and the overall AI risk vocabulary, ISACA for the IT-general-control vocabulary and COBIT cross-tagging.
