# Leading an AI Audit Engagement at Senior-Practitioner Scope

## Motivation

At a certain career point the auditor stops being the person who performs the test and becomes the person who is answerable for everything the engagement produces. The reader of the final report sees the engagement lead's name; the Chief Audit Executive signs the engagement letter on the engagement lead's recommendation; the audit committee's trust in the audit function is built, one engagement at a time, out of how the lead runs the room.

AI audits raise the stakes. The subject is technically dense, evidence is heterogeneous, the standards are new or evolving, and the engagement can produce legal and reputational effects that reach well beyond the audit committee. A lead who runs the engagement loosely — with scope that drifts, a team that is not matched to the subject, and a quality review that happens at the end instead of continuously — produces findings that do not survive peer review and reports that the audit committee cannot trust under pressure.

This chapter covers the engagement-level responsibilities of a senior AI auditor: how the engagement is planned, how the team is composed and deployed, how progress is tracked against budget and scope, how quality is reviewed, how the closing meeting is run, how the engagement is delivered, and how the engagement lead interfaces with the Chief Audit Executive (CAE) and with external quality-assurance reviewers.

## Where "engagement leadership" lives in the standards

Two bodies of authoritative guidance set the baseline the auditor should assume.

- **The IIA's Global Internal Audit Standards (2024).** The standards consolidate the prior International Professional Practices Framework and set out principles and standards grouped into five Domains. Domain IV (Managing the Internal Audit Function) and Domain V (Performing Internal Audit Services) together describe the lead's responsibilities — planning the engagement, deploying resources, supervising, communicating, monitoring, and improving.<!-- needs-research: confirm exact Domain / Standard numbering at reading time; the IIA's renumbering is recent (effective 2025-01-09) and prior 2000-series citations like "Standard 2240 — Engagement Work Programme" have been consolidated. -->
- **The IAASB's ISAE 3000 (Revised)** governs assurance engagements other than audits or reviews of historical financial information, and its engagement-level sections prescribe acceptance, planning, evidence, conclusion, and reporting for the kind of attestation work that AI audits increasingly produce. ISAE 3000 pairs with the quality-management suite (ISQM 1, ISQM 2, ISA 220 Revised) that describes how a firm's quality system supports the engagement partner.
- **For government and performance audit shapes**, the GAO Yellow Book (2024 revision) carries engagement-planning, supervision, and reporting requirements that align with the IIA Standards at the engagement level.
- **For AI-specific overlays**, ISO/IEC 17021-1 (management-system certification bodies) and ISO/IEC 27006-1 / 42006 (management-system-audit scheme-specific requirements) describe how a lead auditor of an ISO management system engagement must plan, resource, and conduct the audit; the AI-specific requirements for ISO/IEC 42001 audits sit in ISO/IEC 42006.<!-- needs-research: verify publication status of ISO/IEC 42006 at reading time; AIMS certification scheme-specific requirements are in late-stage standardisation. -->

The lead's job is to make the engagement defensible under each of the bodies that will later inspect it — the CAE's internal quality assessment, the external IIA Quality Assessment, the PCAOB-style inspection where applicable, and, for ISO-regime engagements, the accreditation body's witness audit and file review.

## Phase 1 — Engagement planning

### Acceptance and continuance

The decision to accept the engagement precedes planning. The lead advises the CAE (or the firm's independence partner for external engagements) on four acceptance questions.

- **Independence and conflicts.** The lead and the engagement team satisfy the independence requirements for the engagement's scheme (IIA, GAGAS, ISO/IEC 17021-1, ISAE 3000) and have no conflicts barring the specific assignment. See `mod-101` for the posture.
- **Competence.** The engagement team can cover the subject matter. For AI audits this typically means at least one lead auditor, at least one technical specialist (data science / ML engineering / safety / security, depending on scope), and access to counsel for criteria questions at the regulatory boundary.
- **Criteria availability.** The criteria the engagement will measure against are identifiable and defensible (`mod-102`). An engagement without stable criteria becomes advocacy.
- **Resources and timing.** The engagement can be delivered within the budget, scope, and timeline the sponsor has agreed. A lead who accepts a timeline that will not permit due professional care is the first failure mode of the engagement.

Acceptance is documented. The engagement letter (external) or engagement memorandum (internal) states the scope, criteria, team, independence posture, timing, deliverables, and fee / cost basis.

### The engagement work programme

The engagement work programme is the lead's operating plan. It names:

- **Objectives.** What the engagement will conclude on, in the shape of the audience's expected opinion type (`mod-111` chapter 4).
- **Scope.** Systems, processes, periods, and entities covered, with explicit boundary statements for what is *out* of scope.
- **Criteria.** The authorities the engagement will test against, drawn from `mod-102`.
- **Risk assessment.** Inherent and residual risk by audit area, driving sampling intensity (`mod-103`, `mod-104`).
- **Procedures.** Specific test procedures by control objective, with the evidence form each will produce.
- **Team deployment.** Who is doing what, and the planned hours by team member and by procedure.
- **Milestones.** Entry criteria, fieldwork start, interim review, draft findings, management response, closing meeting, final delivery.
- **Supervision plan.** Who reviews what, when, and to what standard.
- **Quality review.** The engagement-quality review (see Phase 4) by a reviewer independent of the engagement team.

The work programme is a living document. Changes to scope, criteria, or procedures during fieldwork are documented in the programme with the lead's approval; drift that is not documented is scope drift, and auditors who discover it late have no defence.

### Team composition for an AI audit

An AI audit team is a composite. The IIA Standards require the audit activity to collectively possess the knowledge, skills, and competencies to perform its responsibilities; for AI audits that composition typically includes:

- **Lead auditor (engagement lead).** Owns the engagement end-to-end; a certified audit professional (CIA, CISA, IRCA ISO 42001 lead auditor, or equivalent) with AI-audit experience.
- **Technical specialists.** Data scientists / ML engineers / safety engineers / security engineers brought in for subject-matter depth. Technical specialists may be inside the audit function, inside the organisation (seconded under independence guardrails), or external.
- **Independent reviewer.** A senior auditor who reviews the engagement's work and findings without being involved in their preparation — the engagement-quality review function.
- **Administrative support.** Workpaper coordination, evidence-request logistics, interview scheduling, document-request tracking, status reporting.

Where a specialist is seconded from a function the audit will later cover, the lead documents the rotation lock-out and the specialist's constrained role (specific tests they may perform; findings they may not sign) to preserve independence.

### Budget, schedule, and scope guardrails

The lead sets the engagement budget in hours (not just dollars) by phase and by team member. At kickoff the lead publishes to the team:

- Planned hours by team member.
- Planned hours by procedure.
- Milestone dates with entry and exit criteria for each.
- The change-control rule: any procedure change that moves hours by more than a stated threshold (commonly 10%) requires the lead's written approval.

Scope creep in AI audits is specific — a stakeholder asks for an "additional system to be included," or a technical finding opens a new line of inquiry that spans another team, or a regulator inquiry arrives mid-engagement. The lead records each request, decides whether to expand scope (with the sponsor's agreement and a budget amendment) or to defer to a later engagement, and documents the decision.

## Phase 2 — Fieldwork and supervision

### The daily operating rhythm

A well-run engagement runs on a short cadence. Typical patterns:

- **Daily stand-up** (15–20 minutes) — each team member reports progress against yesterday's commitments, blockers, and today's commitments. The lead captures decisions.
- **Weekly status** — written status to the sponsor and CAE with completion against plan, open risks, significant findings surfaced, and change requests.
- **Mid-engagement review** — formal review point at ~50% of budget. The lead presents to the CAE on scope confidence, findings pipeline, team utilisation, and risk to on-time delivery.

### Supervision of the team

Supervision in AI audits is heavier than in traditional audits because the technical specialists often operate at the edge of the lead's hands-on competence. The lead's job is not to redo the specialist's work but to supervise it to a professional-skepticism standard.

Specifically:

- **Review the specialist's test plan before execution.** A fairness test with a wrong population definition is worse than no test; catching the issue in test design is cheaper than catching it in reperformance.
- **Review the specialist's workpaper upon completion.** Does the condition statement match what the test can defensibly claim? Does the sample support the statement? Is the reperformance step documented?
- **Challenge conclusions.** Lead asks "what else could explain this?" and expects a documented answer. Where the specialist's conclusion rests on a methodology the lead cannot fully evaluate, the lead requires an independent cross-check — either a second specialist, or a peer-review from a colleague outside the engagement.
- **Document the supervision trail.** Workpapers are signed by the preparer and the reviewer, with the review notes attached. External inspectors look for this trail and its absence is a finding on the audit function itself.

### Evidence handling

The lead's job on evidence is to make the trail boring. Every piece of evidence has:

- A clear chain from the system of origin to the workpaper (`mod-104` chapter 1 on evidence reliability).
- A hash or signature where the evidence is a data export, so later verification is possible.
- A retention plan — how long the evidence is kept, by whom, under what access controls.
- A privilege classification where relevant — some evidence is privileged; the lead works with counsel on the handling.

### Managing scope drift

Scope drift during fieldwork is normal. What is not normal is unacknowledged drift. The lead maintains a scope-decision log with:

- Date of request.
- Requester.
- Request.
- Decision (in scope / deferred / rejected) with reasoning.
- Impact on budget and timeline.
- Sponsor acknowledgement (for in-scope changes).

The log is a workpaper and is reviewed at the engagement-quality review.

## Phase 3 — Findings development and management response

Findings pass through the lifecycle described in `mod-111`:

- Fieldwork surfaces a candidate finding.
- The preparer drafts the finding in CCCER structure.
- The lead reviews the finding against the chapter 1 checklist (`mod-111` chapter 1).
- Management is walked through the draft (preview, not negotiation) to validate facts.
- Management response and corrective-action-plan commitments are negotiated per `mod-111` chapter 3.
- Each finding goes to engagement-quality review.

The lead's job during findings development is twofold: own the overall finding slate (the set of findings is proportionate to the risk, the shape, and the audience), and protect individual findings from pressure (management attempts to re-characterise, the engagement team attempts to shade language).

### Closing meeting

The closing meeting is a controlled event. The lead prepares:

- **Agenda** — in writing, shared in advance.
- **Attendee list** — who, and why (a lead who allows unexpected attendees signals scope confusion; a lead who excludes a legitimate stakeholder signals process failure).
- **Walk-through of each finding** — condition, criterion, cause, effect, recommendation — followed by the management response and the agreed corrective-action plan.
- **Open items** — findings still in draft, evidence still outstanding, decisions still open.
- **Delivery timeline** — when the final report will issue, to whom, in what shape.
- **Minutes** — captured by the engagement team's administrative support, signed by the lead and management.

The closing meeting is not where the findings are debated for the first time. If a finding surfaces at the closing meeting that management has not seen, the lead has failed at communication during fieldwork.

## Phase 4 — Engagement-quality review

Before the report issues, the engagement passes through engagement-quality review (EQR). EQR is performed by a qualified reviewer independent of the engagement team. The reviewer evaluates:

- Whether the engagement plan was appropriate and whether changes during the engagement were documented and approved.
- Whether the work performed was sufficient and appropriate to support the conclusions.
- Whether findings are structured correctly and supported by the workpaper trail.
- Whether the report is consistent with the engagement conclusions and with the engagement scheme's reporting requirements.
- Whether significant judgements made by the lead were reasonable and documented.
- Whether independence was preserved throughout.

For ISAE 3000 engagements and ISO/IEC 17021-1 certification engagements, EQR is required at defined circumstances (high risk; significant judgement; regulator-sensitive subjects). For internal audits under the IIA Standards, the CAE establishes when EQR is required.

EQR notes are documented and resolved before issue. A disagreement between the reviewer and the lead that cannot be resolved rises to the CAE (or to the firm's quality function for external engagements) under the firm's consultation protocol.

## Phase 5 — Delivery and post-engagement

### Report issue

The report issues in the shape the engagement scheme requires (`mod-111` chapter 4). The lead confirms:

- The report matches the scheme's required elements.
- Distribution matches the engagement letter.
- The report cites the workpaper references the inspector will later ask to see.
- The final workpaper file is closed — no further changes except the documented closure of post-issue items.

### Engagement archive

The engagement file is archived within the firm's archival window (commonly 60 days of report issue for IIA; 60 days from the report release date under ISQM 1 for firm audits; longer per ISO/IEC 17021-1 and scheme-specific requirements for ISO engagements). The archived file is the record the subsequent peer review or inspection will test.

### Post-engagement review

Within a short window after issue, the lead conducts a short post-engagement review with the team:

- What worked.
- What did not work.
- What would be done differently next engagement.
- Feedback to the team's professional development.

The review feeds into the CAE's annual assessment of the audit function and into the firm's quality system (see chapter below).

## Coordinating with the Chief Audit Executive

The engagement lead's primary internal counterpart is the CAE. The relationship is governed by:

- **Function-level quality assurance.** The CAE is responsible for a Quality Assurance and Improvement Programme (QAIP) that covers all audit engagements. The engagement lead feeds the QAIP with engagement-level quality data — adherence to standards, adherence to the work programme, reviewer sign-offs, findings slate, time-to-close.
- **Resource and conflict decisions.** The CAE resolves resource constraints that the lead cannot resolve inside the engagement — bringing in additional specialists, arranging rotation of team members, deciding on scope changes that cross engagement boundaries.
- **Escalation.** Where management refuses to accept a finding, or where an external party challenges the engagement, the CAE is the escalation point. The lead's job is to brief the CAE with the full workpaper trail and to support the CAE's engagement with the audit committee.
- **External regulator interface.** Where a regulator inquiry touches the engagement, the CAE is often the signatory to correspondence; the lead provides content. See chapter 5 for the regulator-interface posture.

## External quality assurance

Internal audit functions and attestation firms are subject to external quality assessment.

- **IIA External Quality Assessment (EQA).** The IIA Standards require an EQA at least every five years, performed by a qualified independent reviewer. The engagement lead's archived files are the primary artefact the EQA reviewer inspects. A pattern of engagement-quality failures in the EQA yields a "does not conform" rating that is reported to the audit committee and often published.
- **PCAOB-style inspection (for firms performing public-company audits and some attest work).** The PCAOB inspects firms' selected engagement files annually or triennially. The AI-audit work the firm performs under ISAE 3000 or SOC may be within scope where the firm audits public companies. The inspection tests whether the engagement partner's judgements were supported.
- **IAF accreditation body witness audits and file reviews for ISO/IEC 17021-1 certification bodies.** Certification body auditors are observed during live audits by the accreditation body; their archived files are reviewed on cycle; the certification body loses accreditation for persistent lead-auditor file deficiencies.
- **Peer review for CPA firms performing SOC and attestation engagements.** The AICPA peer-review programme inspects partner-level engagement work.

The lead's job is to run every engagement as if an external inspector will land on it. In AI audits, which have the shortest standards history and the highest public salience, that inspection posture is not paranoia — it is normal operating assumption.

## A short rubric the engagement lead tests against

Before the report issues, the engagement lead can quickly test the engagement's defensibility against this rubric:

- Is the engagement letter / memorandum consistent with what the engagement actually did?
- Is the work programme updated to reflect scope and procedure changes, each with lead approval?
- Does every finding have the workpaper trail described in `mod-111` chapter 1?
- Is every workpaper signed by preparer and reviewer with notes resolved?
- Has engagement-quality review been performed by a qualified independent reviewer and documented?
- Is the report in the shape the scheme requires?
- Is independence documented from acceptance through delivery?
- Has the scope-decision log captured every change?
- Has the time-tracking record reconciled hours to plan, with variances explained?
- Is the archive ready?

A lead who answers yes to each item has an engagement that can survive external inspection. A lead who cannot answer yes has repair work to do before issue.

## Summary

- The engagement lead is accountable for the engagement end-to-end: acceptance, planning, fieldwork, findings, closing, delivery, and archive.
- Acceptance and planning are documented in the engagement letter and the work programme; team composition matches the subject with lead auditor, technical specialists, independent reviewer, and administrative support.
- Fieldwork is supervised on a daily and weekly cadence, with supervision workpapers documenting the lead's review of the team's work.
- Scope changes are captured in a scope-decision log; budget and schedule variances are tracked and explained.
- Findings pass through the CCCER lifecycle (`mod-111`) and through engagement-quality review by a qualified reviewer independent of the engagement team.
- The closing meeting is a controlled event that walks the agreed findings and management responses; surprises at the closing meeting indicate communication failure during fieldwork.
- The engagement archive is the record external inspectors will test — IIA EQA, PCAOB-style inspection, IAF witness audits, AICPA peer review.
- The lead coordinates with the CAE on function-level quality, resource and conflict decisions, escalation, and the regulator interface.
- A rubric check before report issue — engagement letter consistency, work programme currency, workpaper trail, reviewer sign-offs, EQR completion, report shape, independence documentation, scope-decision log, time variance, archive readiness — gives the lead a defensible engagement.
