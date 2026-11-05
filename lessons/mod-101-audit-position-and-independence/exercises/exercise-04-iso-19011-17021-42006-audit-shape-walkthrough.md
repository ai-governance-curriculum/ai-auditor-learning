# exercise-04: ISO 19011, ISO/IEC 17021-1, and ISO/IEC 42006 — AIMS Audit-Shape Walkthrough

**Estimated effort:** 2.5 hours

## Objective

Walk a fictitious ISO/IEC 42001 certification engagement from acceptance through Stage 1 under the three-standard stack (ISO 19011 + ISO/IEC 17021-1 + ISO/IEC 42006). Produce the artifacts a certification body's lead auditor would actually hand to a QA reviewer.

## Prerequisites

- Chapter [`06-iso-19011-17021-and-42006.md`](../06-iso-19011-17021-and-42006.md)
- Chapter [`08-independence-and-ethics-posture.md`](../08-independence-and-ethics-posture.md)
- Read-access to:
  - ISO 19011:2018
  - ISO/IEC 17021-1:2015 (plus any amendments current at reading time)
  - ISO/IEC 42006 (cite the latest published or under-development version; mark `needs-research` where the version is in flux)
  - ISO/IEC 42001:2023 (headline — clauses 4-10 and Annex A, for context)

## Scenario

**Clearwater Mobility** is a fictitious European urban-mobility operator (electric vehicles + autonomous shuttles in pilot). They have engaged **TrustCert e.V.** — your fictitious accredited certification body — for initial ISO/IEC 42001 certification. Scope statement proposed by Clearwater:

> The design, development, deployment, operation, and improvement of AI systems supporting Clearwater Mobility's demand-forecasting, dynamic-pricing, fleet-dispatching, and autonomous-shuttle-pilot services, at the Amsterdam and Rotterdam locations.

AI systems in scope (4):

1. Demand-forecasting ML model (production).
2. Dynamic-pricing ML model (production).
3. Fleet-dispatching optimisation + ML routing (production).
4. Autonomous-shuttle pilot stack (6 shuttles, pilot operation on fixed routes in Rotterdam only).

Integrated management systems in place at Clearwater:

- ISO 9001 (certified, current).
- ISO/IEC 27001 (certified, current).
- No ISO/IEC 27701, no ISO 14971 (not applicable; no medical devices).

Audit team you are assembling as lead auditor:

- Lead auditor (you) — ISO/IEC 42001 Lead Auditor, prior ISO 9001 + ISO 27001 lead-auditor background, AI-audit CPD current.
- Second auditor — ISO 9001 + ISO 27001 lead-auditor, AI-audit specialist in training.
- Technical expert — ML engineer (external contractor), for the autonomous-shuttle stack specifically.

## Deliverables

### 1. Engagement acceptance package (Markdown)

Include:

- **CB impartiality screen** (ISO/IEC 17021-1 clause 5.2 and Annex H) — list the fact patterns to check: has TrustCert provided consulting to Clearwater in the prior 2 years? Does any TrustCert personnel have a familial or employment relationship with Clearwater? Does TrustCert hold a stake in Clearwater? Are there commercial pressures? For each fact pattern, state what you would verify and the acceptable outcome.
- **Individual-auditor independence declarations** — a template form each auditor and the technical expert signs; adapt the template from chapter 8.
- **Scope-definition memo** (one page) — does the proposed scope statement meet ISO/IEC 42001's scope-definition requirements (clauses 4.3-4.4) *and* support a defensible certification statement per ISO/IEC 17021-1 clause 9.6? Specifically, is the autonomous-shuttle pilot "in" or "out" of the AIMS — defend the call.
- **Audit-time calculation memo** — start from the ISO/IEC 17021-1 Annex B baseline for Clearwater's organisation size and complexity. Apply the ISO/IEC 42006 AIMS-specific overlay (more AI systems → more time; higher-risk AI systems → more time). Show your working as a short table. Where ISO/IEC 42006 has not yet published the overlay quantitatively, cite the clause you would reference once published and mark `needs-research`.
- **Audit-team competence memo** — map each team member's competence to the ISO 19011 clause 7 criteria and the ISO/IEC 42006 AI-specific competence criteria. Identify the technical-expert scope narrowly (autonomous-shuttle stack only).

### 2. Stage-1 audit plan (Markdown)

Include:

- Stage-1 objectives per ISO/IEC 17021-1 clause 9.3 (documentation review, site conditions, auditee readiness for Stage 2, scope confirmation, resource planning for Stage 2).
- Stage-1 schedule — half-day or full-day blocks; specify dates (placeholder OK), locations (Amsterdam vs. Rotterdam), participants (names/roles), and activity per block.
- **Documentation review checklist** against ISO/IEC 42001 clauses 4-10 and Annex A — list the documented information you will request, by clause.
- **AI systems inventory check** — you will inspect Clearwater's AI inventory and confirm it reconciles to the four systems named in the scope. Describe your test.
- **Integrated-MS considerations** — since ISO 9001 and ISO/IEC 27001 are already certified, call out which clauses of the AIMS audit can leverage existing MS evidence (e.g., document control, management review, internal audit function) and which require AIMS-specific new evidence.
- **Opening-meeting agenda** — per ISO 19011 clause 6.4.
- **Closing-meeting agenda** — per ISO 19011 clause 6.4 (for Stage 1 closing; Stage 2 planning follows).

### 3. Stage-1 findings template (Markdown)

A one-page template the audit team will populate during Stage 1. Columns: clause, documented-information reference, auditor observation, readiness assessment (ready / minor gap / major gap / blocker to Stage 2), action required by Clearwater before Stage 2.

## Starter guidance

- The three-standard stack has overlap; your audit plan must cite which standard you are leaning on for each decision. A plan that says only "per ISO 19011" without the 17021-1 and 42006 cross-references will be a QA finding.
- Impartiality is tested at the CB level and at the individual auditor level. Do both.
- The autonomous-shuttle pilot is the most interesting scope call — it is in operation, so it probably belongs in the AIMS, but the organisation may argue the pilot is pre-production. Defend the call either way.
- Audit-time calculation under ISO/IEC 42006 is evolving; where the quantitative overlay is not yet published, cite the clause reference you would use when available and mark `needs-research`.
- Integrated-management-system audits are the norm for 42001 engagements layered on 27001/9001; do not re-audit what the 9001/27001 audits have already covered unless AIMS-specific evidence requires it.
- Do NOT confuse Stage 1 with a Stage 2 implementation audit — Stage 1 is documentation, readiness, and planning. Stage 2 operating-effectiveness is deliberately out of scope for this exercise.

## Acceptance criteria

The deliverables are accepted when:

- The impartiality screen identifies at least five concrete fact patterns and names the verification approach for each.
- Individual-auditor independence declarations cover prior employment, familial relationships, financial interest, prior consulting, and (for the technical expert) prior authorship of any artifact in Clearwater's AIMS.
- Scope-definition memo makes a defensible call on the autonomous-shuttle pilot and cites ISO/IEC 42001 clauses 4.3-4.4 and ISO/IEC 17021-1 clause 9.6.
- Audit-time calculation shows a baseline + overlay structure and either cites a published ISO/IEC 42006 quantitative basis or marks `needs-research`.
- Stage-1 plan includes all the sub-elements listed in Deliverable 2.
- Documentation-review checklist covers all of clauses 4-10 and Annex A — no clause is silently omitted.
- Findings template has clear readiness bands and action-required column.
- Every artefact names the ISO standard and clause being relied on for each decision.

## Stretch goals

- Author a **companion Stage-2 plan** at a sketch level (1 page), showing what increments over the Stage-1 plan Stage-2 adds (sampling of AI systems, operating-effectiveness testing, interviews across locations).
- Author a **surveillance-audit plan** for year 1 post-certification — what gets re-audited, at what sample size, on what cadence.
- Draft a **CB impartiality committee** paper that would be tabled at the next quarterly meeting if Clearwater subsequently asks TrustCert to also perform an EU AI Act Article 43 third-party conformity assessment on the autonomous-shuttle stack — identify the impartiality considerations and propose the committee's decision.
