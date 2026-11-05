# Scoping an AIMS Audit Against ISO/IEC 42001 — Stage-1, Stage-2, Surveillance, Recertification, Internal Variant

## Motivation

The single-system engagement in chapter 4 opines on one AI system. An AIMS audit opines on the **management system** that produces every AI system — the organisation's AI policy, objectives, roles, risk-assessment process, impact-assessment process, operational controls, monitoring, management review, and improvement under ISO/IEC 42001:2023. For certification bodies the audit shape is prescribed: **ISO/IEC 17021-1:2015** (horizontal management-system certification), **ISO/IEC 42006** (AIMS-specific CB requirements), **ISO 19011:2018** (guidelines for auditing MS). For internal auditors the shape is adapted — the same clause map is tested, but under IIA Standards 2024 and ISO/IEC 42001 clause 9.2 (internal audit), without the certification-body overlay. This chapter is the scope template for both.

A certification-body AIMS audit cycle is a **three-year cycle**: stage-1 (documentation review) and stage-2 (implementation audit) in year one, surveillance audits in years two and three, and recertification in year four opening the next cycle. An internal AIMS audit reuses the clause map but runs on the organisation's own cadence (typically annually under clause 9.2). The scoping questions change by phase; the clause map stays the same.

> **Boundary with later modules.** `mod-105-auditing-iso-42001-aims` is where the clause-by-clause audit mechanics live. This chapter is the *scope* layer — what the engagement is, before any fieldwork mechanics are selected. Keep the layering clean.

## The scoping axes common to all AIMS audits

An AIMS audit scope answers these in writing before any engagement letter is drafted:

- **Scope of the AIMS as declared by the organisation** — under clause 4.3, the organisation declares the AIMS boundary (which business units, which AI systems, which jurisdictions, which processes). The audit scope is anchored to this declaration; the audit does **not** redraw the AIMS boundary during fieldwork.
- **Certification scope** (for certification-body audits) — the text that will appear on the certificate, naming the scope in a form the market can read. Scope drafting is a significant pre-engagement activity; mis-drafted scope ends up on the certificate for three years.
- **Statement of Applicability (SoA)** — the organisation's selection of Annex A controls, with inclusion or exclusion rationale. The SoA is a primary input and a primary audit subject.
- **AI systems population** — the full list of AI systems inside the AIMS boundary at the audit date. Each is sampled or walked.
- **Sites / locations** — physical and cloud locations where the AIMS operates. Multi-site sampling under ISO/IEC 17021-1 clause 9.1.5 shapes the on-site plan.
- **Shift / cycle coverage** — whether the AIMS operates 24/7 and whether out-of-hours operations (incident response, monitoring, on-call) are in scope.
- **Period of coverage** — AIMS documents are point-in-time; evidence of operation is period-of-coverage. The two interact.
- **Integration with other management systems** — ISO/IEC 27001, 27701, 9001, 13485, 14971; the audit plan recognises integrated management-system audits where the organisation has them.

## Certification-body cycle — the four phases

### Phase 1 — Stage-1 audit (documentation review)

Stage-1 is a planning and readiness audit. **ISO/IEC 17021-1 clause 9.3.1.2** says Stage-1 is conducted to:

- audit the client's management-system documentation;
- evaluate the client's site-specific conditions;
- review the client's status and understanding of requirements, particularly regarding identification of key performance / significant aspects, processes, objectives, operation of the management system;
- collect necessary information on the scope, processes, locations, and related statutory and regulatory aspects;
- review the allocation of resources for stage-2 audit and agree with the client on the details of stage-2;
- provide a focus for planning stage-2 by gaining sufficient understanding of the client's MS and site operations in the context of possible significant aspects;
- evaluate if the internal audits and management reviews are being planned and performed, and that the level of implementation of the MS substantiates that the client is ready for stage-2.

For AIMS the Stage-1 scope therefore covers:

- **Mandatory documentation** — AI policy (5.2), roles and responsibilities (5.3), AIMS objectives (6.2), risk-assessment process (6.1.2), risk-treatment plan (6.1.3) with the SoA, AI system impact-assessment procedure (6.1.4, cross-referenced to ISO/IEC 42005), documented scope (4.3), context and interested parties (4.1 and 4.2), operational planning and control (8.1), AI system lifecycle controls (8.2 et seq.), performance evaluation (9.1), internal audit (9.2) and management review (9.3), nonconformity and corrective action (10.1).
- **AIMS readiness evidence** — an internal audit (clause 9.2) has been performed at least once covering the full AIMS, a management review (clause 9.3) has been conducted, corrective actions on prior-audit findings are in progress.
- **Site-specific conditions** — number of sites, number of AI systems, number of staff involved in the AIMS, the organisation's inventory shape, the first-line / second-line / third-line posture.
- **Stage-2 planning inputs** — sampling strategy for AI systems, SoA control selection sampling, interview schedule, evidence request list.

Stage-1 produces a **Stage-1 report** with:

- Observations on documentation adequacy against clauses 4–10 and Annex A.
- Areas of concern that could be classified as non-conformity at Stage-2.
- Confirmation that the organisation is ready for Stage-2 (or deferral).
- An agreed Stage-2 plan (team, duration, schedule, scope).

Stage-1 is typically off-site or partly on-site; AIMS-specific Stage-1 often requires at least one on-site day to understand the AI-system inventory in context.

### Phase 2 — Stage-2 audit (implementation audit)

Stage-2 evaluates whether the AIMS is **implemented** and **effective**. The scope:

- Walks each clause 4–10 requirement with evidence of implementation, not just documentation.
- Samples the AI-system population per the stage-1 sampling plan.
- Samples SoA controls — each included control tested on at least a sample of AI systems; excluded controls' exclusion rationale confirmed.
- Tests the evidence of operation — risk assessments executed, impact assessments completed, management reviews held, internal audits done, corrective actions closed, monitoring operating.
- Interviews first-line AI engineering teams, second-line governance / risk / compliance, top management, internal audit.
- Grades non-conformities: **major** (absent or systemic failure of a required element; failure of the AIMS to achieve its policy / objectives; a situation that raises significant doubt about the capability of the AIMS to achieve its intended outcomes) vs. **minor** (isolated non-conformity that does not raise significant doubt).
- Produces a certification recommendation: recommend, recommend with corrective actions, do not recommend.

Duration: **ISO/IEC 42006 Annex A** provides AIMS-specific audit-day tables conditioned on organisation size and complexity (AI-system count, AIMS maturity, risk category). <!-- needs-research: confirm the specific audit-day table in ISO/IEC 42006 at authoring time; final ISO/IEC 42006 Annex structure settled in the 2024–2025 window and may have been amended since --> The certification body is expected to document the audit-time calculation; this is the primary scope lever.

### Phase 3 — Surveillance audit (years 2 and 3)

Surveillance is shorter. **ISO/IEC 17021-1 clause 9.6.3** requires a surveillance audit at least once per calendar year except in the year of recertification. Scope:

- Internal audit (clause 9.2) and management review (clause 9.3) outputs since the last audit.
- Review of corrective actions on prior findings.
- Changes to the AIMS (scope changes, new AI systems, retired AI systems, new sites, regulatory-landscape changes affecting the AIMS, new standards).
- Risk-register and SoA updates.
- Monitoring and measurement outputs (clause 9.1).
- Complaints handling and incident records.
- A sample of AI systems and SoA controls proportionate to risk.
- The organisation's continued use of the certification mark and reference to certification in a way consistent with 17021-1 clause 8.3.

Surveillance can only identify non-conformities within its scope; it is not a full re-audit. Scope drift ("surveillance is just a check-in") undermines the cycle; it is a planned, documented, evidenced audit.

### Phase 4 — Recertification audit (end of year 3)

Recertification is a **full** audit of the AIMS, structured similarly to Stage-2 but informed by the three-year history of findings and improvements. Scope:

- Clauses 4–10 at full depth.
- Annex A controls at full depth, re-sampling across the population.
- Three-year trend review — are findings improving? is management-response history reliable?
- Confirmation of continued conformity with current ISO/IEC 42001 edition and current law (ISO publishes periodic updates; a mid-cycle ISO/IEC 42001 amendment or a new EU AI Act implementing act may change the audit terrain).
- Decision: recertify, recertify with CAPs, suspend, withdraw.

Duration under 42006 Annex A is typically shorter than initial Stage-2 (prior-cycle knowledge is leveraged) but not trivial. <!-- needs-research: confirm recertification audit-day reduction in ISO/IEC 42006 Annex A at authoring time -->

### Transversal certification-body obligations

Across all four phases the certification body carries obligations from ISO/IEC 17021-1 clauses 5–9 and ISO/IEC 42006:

- **Impartiality and independence** — 17021-1 clause 5; AIMS-specific impartiality concerns in 42006 around consulting vs. certification work and around multi-engagement independence (chapter 7).
- **Competence** — 17021-1 clause 7; AIMS-specific competence requirements in 42006 covering AI domain, AIMS clauses, and relevant sector regulation.
- **Audit-team composition** — lead auditor, technical experts for AI subject matter, independent reviewer per 17021-1 clause 9.5.
- **Confidentiality** — 17021-1 clause 8.5; the auditor sees model weights, training data, incident records, management commentary.
- **Appeals and complaints** — 17021-1 clauses 9.7 and 9.8.
- **Information provided to the accreditation body and the client** — 17021-1 clause 8.

## The internal-audit variant — same clause map, different cycle

An internal AIMS audit under ISO/IEC 42001 clause 9.2 and IIA Standards 2024 reuses the clause map but:

- Is **not a certification activity**. No certificate is issued; the output is an internal audit report to the audit committee.
- Is typically **annual at full scope** with mid-year follow-ups; some organisations run quarterly thematic AIMS audits covering a subset of clauses each quarter.
- Is **not subject to ISO/IEC 17021-1 or 42006** — the audit function reports under IIA Standards 2024, not certification-body standards. Independence is organisational (CAE reporting line, chapter 7), not certification-body independence.
- Serves a **readiness** function for the certification audits — internal audit evidence is one of the clause-9.2 inputs the certification body expects at Stage-1.
- Can cover **any clause at any depth** without the 42006 audit-day table — the internal CAE sizes the engagement to the function's capacity and the audit-committee priorities.

The internal AIMS audit scope memo looks like chapter 4's seven-element scope memo, with the subject matter being the AIMS rather than a single system:

```
Engagement:       AIMS Internal Audit — Annual Cycle FY27
Regime:           IIA Standards 2024 + ISO/IEC 42001 clause 9.2
Intended users:   Audit Committee; CRO as AIMS owner; top management
Purpose:          Provide reasonable internal-audit assurance over the design and operating effectiveness of the AIMS for FY27, informing audit-committee approval of the FY28 risk-based plan and certification-readiness for the FY28 Stage-2 audit.
Criteria:         ISO/IEC 42001:2023 clauses 4–10 and Annex A controls in the organisation's SoA v2.3; ISO/IEC 42005 impact-assessment methodology; organisation's AI policy v1.4
Boundaries in:    AIMS scope v2.1 (US + EU operations; 42 AI systems; 7 third-party AI vendors)
Boundaries out:   ISO/IEC 27001 ISMS (covered by separate ISMS internal audit); GDPR DPIA process (covered by privacy audit)
Period:           01 Jan 2027 – 31 Dec 2027 (operating-effectiveness); 31 Dec 2027 (documentation point-in-time)
Population:       per clause; see chapter 4 §5
Sampling:         per clause; ISA 530 / IIA 14.2 discipline
Limitations:      AIMS maturity (second cycle); reliance on first-line / second-line self-reporting for monitoring outputs
Deliverable:      Internal audit report with findings, management responses, follow-up plan
Team:             Lead auditor; two AIMS specialists; independent reviewer (chapter 6)
Materiality:      workpaper AIMS-FY27-Materiality-v1 (chapter 3)
Approvals:        CAE; Audit Committee chair
```

## Specialist roles across the AIMS audit

Across both certification-body and internal audits the AIMS audit requires a heterogeneous team:

- **Lead auditor** — ISO/IEC 42001 Lead Auditor credential for certification-body work; IIA CIA for internal lead. Accountable for the audit opinion.
- **Technical expert — AI / ML** — able to interrogate model-lifecycle controls (training data governance, eval design, monitoring).
- **Technical expert — security / privacy** — ISO/IEC 27001 and 27701 integration points.
- **Technical expert — sector** — SR 11-7 for banks, FDA GMLP for medical device makers, NAIC posture for insurers.
- **Independent reviewer** — the per-engagement quality review under ISO/IEC 17021-1 clause 9.5 (certification) or IIA Standards 2024 Principle 12 (quality assurance) for internal.

Team composition is a scope decision — scoping the engagement without the right team is a scope defect. Chapter 6 develops this.

## Stage-1 / Stage-2 scope decision points worth calling out

- **SoA sampling strategy** — the SoA may list 30+ Annex A controls. The Stage-2 plan samples across controls proportionate to inclusion, risk, and prior findings. The sampling plan is in the Stage-1 report.
- **AI-system sampling strategy** — rarely do the auditors test every AI system; the sample is stratified across population (internal / deployed / third-party / embedded / GPAI), risk band, lifecycle phase, and jurisdiction.
- **Integrated audits** — where the organisation holds ISO/IEC 27001, 9001, 13485, 14971 certifications under the same CB, the AIMS audit may be scoped as an integrated audit under 17021-1 clause 9.1.5.1 integration provisions, reducing duration but adding coordination overhead.
- **Readiness-vs-certification distinction** — an organisation may contract an audit *for readiness* without a certification path. That is **not a Stage-1 audit** under 17021-1 — it is a consulting or gap-assessment engagement, and the engagement letter must say so; otherwise the CB has created an independence impediment to the later certification audit.

## Common failure modes

- **Scope drifts between Stage-1 and Stage-2.** The Stage-1 report agrees scope v2.3; the Stage-2 fieldwork finds the client mis-represented scope and quietly audits scope v2.5. Report either goes out on wrong scope or is delayed to re-scope formally.
- **SoA accepted without challenge.** The organisation's exclusions are not interrogated; a necessary control (for an in-scope system) is excluded without defensible rationale.
- **AI-system sample skewed to easy systems.** The sample over-indexes on mature, well-documented systems; the audit cannot generalise to the full AIMS.
- **Surveillance treated as a desk review.** Field evidence is skipped and the surveillance misses an AIMS deterioration.
- **Internal AIMS audit duplicates the certification audit.** Internal audit tests the same controls in the same way at the same depth; audit-committee value is low. Internal audits should use coverage data from certification to focus where certification does not.
- **No independence check across engagements.** The CB auditor who ran a consulting-shaped gap assessment in Year N–1 then leads the Stage-2 in Year N; impartiality under 17021-1 clause 5.2 is at risk.

## Summary

- An AIMS audit is scoped against the organisation's declared AIMS scope and SoA, across clauses 4–10 and Annex A, with specific attention to the AI-system population, sites, period, and integration with other management systems.
- Certification-body audits run a **four-phase cycle** — Stage-1 documentation review, Stage-2 implementation audit, two annual surveillance audits, recertification — under ISO/IEC 17021-1 and 42006.
- Stage-1 is readiness and planning, not a dress rehearsal — its output is the Stage-2 plan and a documented confirmation of client readiness.
- Stage-2 grades non-conformities (major vs. minor) and recommends certification; **ISO/IEC 42006 Annex A** governs audit duration, with risk-band uplifts for complex AI operations.
- Surveillance is a shorter risk-based audit of change, monitoring, and prior findings; recertification is a full re-audit informed by three-year history.
- An **internal AIMS audit** reuses the same clause map under IIA Standards 2024 and ISO/IEC 42001 clause 9.2 — no certification output, flexible cycle, feeds into certification-readiness, scoped in a chapter-4 shape memo.
- Team composition, SoA sampling, AI-system sampling, integrated-audit opportunities, and the readiness-vs-certification distinction are all scope decisions made before the engagement letter is signed.
