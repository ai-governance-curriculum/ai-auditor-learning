# exercise-05: ISO/IEC 42001 Stage-1 and Stage-2 Audit Plan Authoring

**Estimated effort:** 3 hours

## Objective

Author the Stage-1 audit plan **and** the Stage-2 audit plan for an ISO/IEC 42001 certification engagement at a fictitious organisation, under ISO/IEC 17021-1 and ISO/IEC 42006 shape. Then write a parallel **internal-audit variant plan** for the same organisation using the IIA Standards 2024 / clause 9.2 framing. The deliverable is three plan documents plus a one-page comparison memo contrasting what differs between certification-body and internal shapes.

## Prerequisites

- Chapter [`05-scoping-an-aims-audit.md`](../05-scoping-an-aims-audit.md)
- Chapter [`04-scoping-a-single-ai-system-engagement.md`](../04-scoping-a-single-ai-system-engagement.md) (for the per-system sampling under the AIMS plan)
- `mod-101` chapter 6 (ISO 19011 / 17021-1 / 42006)
- `mod-102` chapter 2 (ISO/IEC 42001 clauses and Annex A to criteria)

## Scenario

**Meridian Logistics**, a fictitious European mid-cap logistics firm, has declared its AIMS in scope for ISO/IEC 42001 certification. Current state:

- Group HQ in Rotterdam; operations in NL, DE, FR, PL, ES.
- AIMS declared scope: all AI systems operated by the Supply Chain, Pricing, and Operations business units, across all five countries.
- 23 AI systems in the AIMS inventory covering demand forecasting, dynamic pricing, dock-door routing, driver-safety monitoring (in-cab video analytics), fraud detection on customer onboarding, and an internal customer-service chatbot powered by a GPAI provider.
- Driver-safety monitoring system uses biometric recognition features in some operating modes; Meridian treats it as EU AI Act **high-risk (biometric categorisation)**; two EU DPAs have had questions.
- Pricing and demand-forecasting systems are classified as *not* high-risk under the Act; one business unit disputes the classification.
- The organisation holds ISO/IEC 27001 and ISO 9001 certificates; the same CB is contracted for integrated audit scheduling.
- The AIMS has been operating for 14 months; internal audit (clause 9.2) was executed six months ago covering the full AIMS; management review (clause 9.3) was held four months ago.
- No major non-conformities are visible in the organisation's self-assessment; several minor NCs on documentation currency are known.

### The engagements

- **E-A** — Stage-1 audit for ISO/IEC 42001 certification by the contracted accredited CB.
- **E-B** — Stage-2 audit for ISO/IEC 42001 certification by the same CB, planned for ≈ 10 weeks after Stage-1.
- **E-C** — Meridian's internal audit function will run its own next-cycle AIMS internal audit (clause 9.2) in parallel, approximately four weeks after E-A.

## Requirements

### For E-A — Stage-1 plan

Produce a Stage-1 audit plan document that:

1. Names the client, AIMS scope, certification-scope draft wording, applicable standards (ISO/IEC 42001:2023, 17021-1, 42006, 19011).
2. Names the audit team — lead auditor, technical expert(s), independent reviewer (for the certification decision stage); credential expectations per 42006; the impartiality-check outcome.
3. Lists the Stage-1 objectives in the form of ISO/IEC 17021-1 clause 9.3.1.2 bullet points, concrete for this organisation.
4. Names the AIMS documentation to be reviewed (every mandatory artifact under clauses 4–10, SoA, impact assessments for biometric driver-safety system, internal audit and management review records).
5. Proposes a Stage-2 sampling plan for AI systems and SoA controls (systems × stratification).
6. Proposes Stage-2 team composition and estimated audit days under ISO/IEC 42006 Annex A. <!-- needs-research: confirm the Annex A duration table for AIMS at the time of authoring -->
7. Names the Stage-1 deliverable shape (Stage-1 report; findings categories; readiness confirmation or deferral).
8. Includes an integrated-audit note on ISO/IEC 27001 and 9001 coordination under 17021-1 clause 9.1.5.1.

### For E-B — Stage-2 plan

Produce a Stage-2 plan building on the Stage-1 output that:

1. Names the Stage-2 scope confirmed from Stage-1 (and any changes).
2. Provides the **AI-system sampling schedule** — which of the 23 systems are tested, with stratification by regulatory classification, business unit, country, and system lifecycle phase.
3. Provides the **SoA control sampling schedule** — which Annex A controls are tested, on which systems, with what procedures.
4. Interview schedule — top management, AIMS owner, business-unit owners, first-line engineers, DPO, internal auditor (prior-cycle); per-interviewee prep requirements.
5. Information-request list — minimum 40 line items in the chapter-6 §4 shape.
6. On-site vs. off-site plan under IAF MD 4 remote-audit guidance. <!-- needs-research: confirm applicable IAF MD 4 revision and any ISO/IEC 42006 overlay for remote AIMS audits -->
7. Non-conformity grading procedure — major vs. minor, promotion-of-minor rules, closing-meeting protocol for findings.
8. Certification recommendation decision pathway and independent reviewer involvement.
9. Risk register for the engagement itself (specialist availability, interviewee availability, evidence-production risk, confidentiality).

### For E-C — internal-audit variant plan

Produce the internal-audit plan under IIA Standards 2024 / clause 9.2 that:

1. Uses the same clause 4–10 and Annex A map but *not* the 17021-1 certification process.
2. Articulates how the internal audit **differs in purpose** from the certification audit (reports to the audit committee; drives remediation; informs certification readiness).
3. Chooses a sampling strategy that is **not redundant** with the certification Stage-2 — pick clauses or controls the certification audit will sample lightly, or sample systems the certification audit will not reach.
4. Names a team and specialists under the chapter-6 team-composition shape.
5. Produces its own IRL (minimum 30 line items) and interview schedule.
6. Names the audit-committee reporting shape and the chapter-7 communication path (draft findings timeline, management-response cadence, follow-up shape).
7. Declares the independence posture explicitly — the internal auditor *was* involved in some pre-certification readiness work; document the independence impact (if any) and the safeguards used.

### Comparison memo

One page, Markdown, contrasting:

- Purpose and intended users
- Independence posture and framing
- Deliverable shape and finding grading
- Sampling and audit-day sizing
- Audit-committee / accreditation-body interface
- Where the two engagements can share evidence (clause 9.2 internal audit evidence feeding Stage-2) and where they cannot

## Starter guidance

- Stage-1 is **not** a preview of Stage-2 findings. Avoid grading documentation deficiencies that should be found at Stage-2; Stage-1's job is readiness confirmation.
- Draft the certification-scope wording carefully — this text lands on the certificate and in public-facing announcements. Name the business units, countries, and system categories; do not generalise ("all AI at Meridian").
- The biometric driver-safety system is likely to be the highest-risk sample unit; ensure it is in the Stage-2 sample at full depth.
- The business-unit dispute over EU AI Act classification is a Stage-1 finding candidate or a scope-dependency candidate — handle explicitly.
- For the internal-audit plan, avoid duplicating the certification audit's procedures. Design for *audit-committee value-add* — coverage the certification audit does not deliver.
- Independence: an internal auditor who co-drafted the SoA cannot lead that section of the internal audit. If one of the team members did pre-cert readiness work, document and route around.
- `<!-- needs-research -->` markers for ISO/IEC 42006 Annex A specifics and IAF MD 4 current revision.

## Acceptance criteria

- Three plan documents delivered, each in the shape its standards expect.
- Stage-1 plan correctly treats readiness confirmation as the objective; does not slip into Stage-2 testing procedures.
- Stage-2 plan has a defensible AI-system sampling stratification and an SoA control sampling schedule; sampling is not uniform-random without rationale.
- Stage-2 IRL has at least 40 line items in the chapter-6 §4 shape; Stage-1 IRL has the AIMS-documentation set at a minimum.
- Internal-audit plan does not duplicate Stage-2 procedures; it adds coverage the certification audit does not.
- Independence posture is declared explicitly in both the CB plans (impartiality check per 17021-1 clause 5.2) and the internal-audit plan (any prior consulting-shaped involvement).
- Integrated-audit coordination with ISO/IEC 27001 and 9001 is addressed, not ignored.
- Audit-day estimates reference ISO/IEC 42006 Annex A with a `<!-- needs-research -->` marker for the specific table.
- Non-conformity grading rules are named (major vs. minor; promotion of accumulated minors).
- No fabricated accreditation bodies, CB names, or 17021-1 clause numbers.

## Stretch goals

- Author the **Stage-1 report template** (not the actual report) — the fields the CB must populate, under 17021-1 clause 9.3.1.3.
- Author a **surveillance-audit plan** for year 2 of the certification cycle, showing how the audit scope shifts from Stage-2.
- Produce an **integrated-audit schedule** for the three ISO certifications (42001, 27001, 9001) with shared evidence and shared audit days, maximising efficiency while maintaining independence of opinion per certificate.
