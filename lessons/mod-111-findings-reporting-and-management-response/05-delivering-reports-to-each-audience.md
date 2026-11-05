# Delivering Audit Reports — Opening, Closing, Audit Committee, Board, Regulator, Public

## Motivation

The report is written for multiple audiences, but each audience receives it through a different *delivery* — a different meeting, a different format, a different concession to privilege and confidentiality, a different question-and-answer posture. An auditor who writes the report but leaves delivery to chance loses the engagement's communicative force. An auditor who treats delivery as choreography loses the integrity of the content. This chapter walks each delivery shape with the preparation and posture required.

Delivery is not optional. The IIA Global Internal Audit Standards obligate internal audit to communicate engagement results to appropriate parties. ISO/IEC 17021-1 clauses on opening and closing meetings prescribe specific delivery events for certification audits. SR 11-7 expects validation findings to reach the board or appropriate committee. EU AI Act Article 21 contemplates the provider's cooperation with competent authorities. AICPA attestation guidance expects communication with those charged with governance. The format of the delivery is shaped by the audience — some audiences receive the report in a formal written-only form; others require a live walk-through with questions; some must have the report tabled in a specific statutory shape.

## Opening meeting

The opening meeting (sometimes called the entrance conference, the kick-off, or the Stage-2 opening) is the first formal engagement event with the auditee. It is attended by the audit team lead, the engagement sponsor, management of the subject-matter area, and (for certification audits) the certification body's representative.

### Purpose

- Confirm the scope, criteria, and schedule.
- Introduce the audit team and the auditee's primary points of contact.
- Walk the audit plan and the expected evidence requests.
- Confirm independence, confidentiality, and conflict-of-interest declarations.
- Set the escalation path for in-engagement disputes.
- Confirm the exit / closing-meeting date and attendees.

### AI-audit-specific considerations

- Confirm which **models, versions, and environments** are in scope; a single "AI system" often expands into a ranker + LLM + retriever + prompt stack during Stage 2.
- Confirm access to **model-development artefacts** — training-data lineage, eval reports, model cards, release logs, monitoring telemetry — with named custodians.
- Confirm access for **reperformance** where applicable — compute environment, held-out samples, model invocation permissions.
- Confirm handling of **sensitive data** in evidence (protected classes, PII, confidential claims) — data room shape, redaction protocol, retention after engagement close.
- Confirm handling of **generative outputs** collected as evidence — the auditor's workpaper repository may need to hold prompt-response samples, which have their own confidentiality and copyright considerations.

### What the auditor does not do in the opening meeting

- Pre-judge findings.
- Commit to an opinion.
- Agree to scope expansions without a change-request.
- Share the firm's prior engagements' findings with this auditee as "benchmarks."

## Closing meeting (exit conference)

The closing (exit) meeting follows fieldwork and precedes the final report. For ISO/IEC 42001 certification audits, ISO/IEC 17021-1 §9.4.8 makes the closing meeting mandatory and lists required content; for other engagement shapes, firm methodology typically mandates it.

### Purpose

- Share **draft findings** in CCCER shape.
- Collect management's immediate factual-correction input.
- Set expectations for the written management response (chapter 3).
- Confirm the final-report timeline.
- Ensure the audit committee or equivalent oversight body is prepared to receive the report.

### Agenda

A typical closing-meeting agenda:

1. Engagement objective and scope recap.
2. Audit methodology summary.
3. Findings walk-through — one by one, with the five CCCER elements each.
4. Classification per the engagement's scheme.
5. Positive observations where applicable.
6. Overall engagement assessment / opinion direction.
7. Management response process and dates.
8. Open items and next steps.

### The discipline of the closing meeting

The closing meeting is high-pressure. Management often marshals a team of SMEs to challenge each finding. The auditor's job is:

- Hear factual corrections without conceding materially.
- Acknowledge when a finding needs re-test rather than defending it defensively.
- Hold the line on classifications when evidence sustains them.
- Keep the discussion per-finding, not aggregate.
- Record disputes without deciding them in the room.
- End with clear next steps — response date, closure date, follow-up schedule.

ISO/IEC 42001 certification auditors carry the ISO/IEC 17021-1 clause 9.4.8 content checklist to the meeting; attestation auditors carry the firm's exit-conference template; internal auditors carry the IAF's standard engagement exit-meeting protocol.

## Management response and the report-finalisation cycle

Between the closing meeting and the final report, management submits its written response (chapter 3). The auditor:

- Reviews the response against the finding.
- Determines adequacy and whether the finding can close or stands open.
- Updates the report: attaches the response, notes adequacy, modifies the overall opinion if warranted.
- Issues the final report with the response attached, to the designated distribution.

### Common cycle traps

- Management stretches the response deadline; the auditor extends the final-report date; the engagement drifts beyond the standard-permitted window (ISO/IEC 42001 CAP windows are typically short — weeks, not quarters — and the certification body's own procedures may force closure).
- Management's response arrives in a form that cannot be attached (a slide deck instead of a per-finding written response); the auditor requests the correct form.
- Management re-litigates the finding in the response letter. The auditor does not re-open the finding from the response alone; disagreements follow chapter 3's escalation.

## Audit committee report-out

The audit committee of the board is the organisation's **independent oversight channel**. For internal audits, the IIA Global Internal Audit Standards position the audit committee as the reporting line that preserves independence of the Chief Audit Executive. For external attestations, the audit committee reviews the engagement before it is signed off. For SR 11-7 MRM, the audit committee receives the validation report through the Model Risk Committee, usually with an escalation path for material-weakness findings. For ISO/IEC 42001, the audit committee receives the certification outcome at the top-management review.

### Preparing the audit committee pack

- **Executive summary** (one page) — scope, overall opinion, number of findings by classification, key themes, management response summary.
- **The report itself** — attached in full.
- **Appendix of findings** — each in CCCER shape.
- **CAP summary** — the schedule of commitments and target closure dates.
- **Prior-cycle follow-up status** — showing whether the function closed last cycle's findings or has repeat patterns.
- **Auditor's recommendations to the committee** — including any items escalated per chapter 3 (cosmetic responses, disputes, resource gaps, independence concerns).

### The audit committee presentation

- 20–30 minutes typical, depending on the committee's capacity.
- One auditor (the engagement lead, or the CAE for internal) presents; others attend but defer.
- Management is present for the walk-through of findings; they get to respond in real time.
- **A private session with the audit committee, excluding management, is scheduled**. This is where the auditor shares material that is uncomfortable to share with management in the room — resource adequacy of the audit function, independence pressures, concerns about management's cooperation, ethics matters. The IIA Global Internal Audit Standards explicitly reference the executive-session practice for the CAE; SOX §204 codifies it for external auditors of U.S. issuers.

### Audit committee charter interactions

The committee's charter may fix:

- Which findings require committee pre-approval of the CAP (often all major nonconformities / material weaknesses / significant deficiencies).
- Which findings are tabled for information (minor nonconformities / low-rated findings).
- The committee's authority to engage external advisors to independently evaluate a disputed finding.
- The committee's authority to compel the Chief AI Officer or equivalent to attend.
- The committee's reporting line to the full board.

The auditor reads the charter and pitches the report to match.

## Board-level reporting

Board-level reporting typically carries two shapes:

- **Routine reporting** — a summary of the audit function's output across the period, tabled in the board minutes.
- **Escalated reporting** — a specific engagement's findings tabled to the full board because the audit committee determined it warrants board-level attention.

### What rises to the board

- Material weaknesses in ICFR with AI pathway.
- Major nonconformities on the AIMS that affect the certification outcome.
- Pervasive patterns of repeat findings.
- Independence or integrity concerns about management.
- Regulatory exposure that the organisation has not elected to disclose.
- Serious incidents (EU AI Act Article 73-shape, SR 11-7 incident, ICFR restatement risk).

### Board-level communication style

The board is not the audit committee. Many members are not audit-literate. The communication is:

- Shorter.
- More context around "what is the AIMS," "what is model risk," "what are we required to do."
- Framed in the business-risk shape rather than the technical-finding shape.
- Accompanied by what the board is asked to decide / acknowledge / direct.

The auditor's job is still to deliver the facts. The framing helps; the content must not drift into reassurance.

## Regulator-facing submission

Some engagement outputs are filed with regulators. The shape of the regulator-facing submission is covered in detail in chapter 7. Delivery to the regulator typically runs:

- Through management (the provider / registrant / regulated entity), with the auditor's report attached as an exhibit — not direct auditor-to-regulator.
- Under a representation that the content is complete and accurate.
- Within a statutory deadline.
- With specific content elements the regulation prescribes.

The auditor's role at delivery is **preparing the exhibit**, confirming the content, and (in some cases) being available to the regulator for questions — not drafting the filing letter.

Direct auditor-to-regulator delivery is the exception, not the rule. ISO certification bodies do route findings to accreditation bodies; EU notified bodies route to market surveillance authorities in specific circumstances (certificate refusal, certificate withdrawal, surveillance findings that implicate Article 73 shape). The auditor's role is governed by the standard and the designation agreement; freelancing to the regulator outside those channels is prohibited.

## External-stakeholder publication

Some reports are **published**. NYC LL144 bias-audit summaries are published on the employer's website. ISO/IEC 42001 certificates are commonly published in the certification body's public registry. SOC 3 reports are designed for public distribution. EU AI Act Article 71 requires registration of high-risk AI systems in the public EU database.

### What the auditor controls in publication

- The content that forms the auditor's report or certificate.
- The scope statement.
- The opinion / certificate language.
- Where applicable, the restriction-on-use language ("This report is intended solely for…"). SOC 2 reports commonly carry a restriction clause limiting the audience to specified parties; SOC 3 reports do not.

### What the auditor does not control

- How management summarises or references the report in marketing.
- Whether management publishes the report in part, in full, or with its own commentary.
- Downstream relying parties' interpretation.

Management will often want to cite findings as marketing. The auditor's engagement letter and the firm's guidelines on name use prescribe what is allowed. Egregious misstatement by management ("we received an unqualified SOC 2 opinion with zero findings" when the report had exceptions) is an issue the auditor must address through the engagement letter's remedies.

## A delivery matrix — which audience, which event, which form

| Audience | Delivery event | Form | Live walk-through |
| --- | --- | --- | --- |
| Engagement sponsor / subject-matter management | Opening meeting | Oral + audit plan doc | Yes |
| Engagement sponsor / subject-matter management | Closing / exit meeting | Oral + draft findings | Yes |
| Engagement sponsor / subject-matter management | Final report | Written | Walk-through if requested |
| Audit committee | Scheduled committee meeting | Written pack + oral | Yes, with private session |
| Full board | Board meeting (or written only) | Written + oral if escalated | If escalated |
| Certification body / accreditation body | Submission packet | Written | Per protocol |
| Regulator (indirect) | Management filing | Written exhibit | Rare |
| Regulator (direct, certification/notified body) | Statutory channel | Written | Per designation agreement |
| Public (where required) | Website / registry publication | Written | No |
| Customers / prospects | Under NDA | Written (SOC 2) or public (SOC 3) | Occasionally |
| Litigation | Discovery / subpoena | Written workpapers | Deposition if required |

Each row has its own cadence, its own confidentiality posture, its own privilege considerations (see below), and its own evidentiary weight.

## Privilege, confidentiality, and the "candour" tension

Internal audit reports and findings are sometimes claimed as subject to attorney-client privilege or work-product doctrine where counsel has structured the engagement with privilege in view. Privilege is **not automatic**; it depends on:

- Who requested the work (counsel).
- For what purpose (giving legal advice).
- Structure of the engagement (reporting to counsel).
- Documentation of the arrangement.

Audits performed outside this structure — the vast majority — are *not* privileged. The auditor should assume findings and workpapers are discoverable. Compliance Monitorships and Deferred-Prosecution-Agreement (DPA) audits frequently have specific disclosure rules by the government. The auditor:

- Does not assume privilege absent explicit documented structure.
- Documents findings with the discipline of litigation-anticipated writing — factual, neutral, well-referenced.
- Does not editorialise, speculate, or assign blame.
- Does not reference prior-engagement internals beyond what is explicitly permitted.

Confidentiality is distinct from privilege. Engagement letters prescribe who may receive the report and under what restriction. The auditor's firm's quality-management policies prescribe retention. External attestation reports commonly carry a "Use restriction" clause limiting the report's use to specific parties.

## Delivery when the audit team disagrees with management's response

Where management's response is inadequate, chapter 3 established the escalation. In delivery terms:

- The final report attaches the response verbatim.
- The auditor's assessment that the response is inadequate is **in the auditor's text**, not in a footnote. The reader must be able to see that the auditor evaluated the response and found it insufficient.
- The audit committee is pre-briefed if the engagement lead expects management to attempt to dilute the finding at the committee meeting.
- Private session with the audit committee is the venue for independent-channel escalation (resource adequacy, independence pressures, retaliation concerns).

## Specific delivery adaptations by engagement shape

### ISO/IEC 42001 certification

- Opening and closing meetings are mandatory and have ISO/IEC 17021-1 content requirements.
- Certification decision is made by the certification body's committee, not the audit team; the audit team recommends.
- Certificate publication is in the certification body's registry.

### SOC 2 Type II

- Opening is often less formal (a kick-off call).
- Closing is a "clearing comments" meeting where exceptions are walked and management's description is confirmed.
- Final report is a controlled distribution document under the Use Restriction clause.
- Customers often request a direct read-out with the service auditor; the service auditor's engagement letter governs what is permitted.

### SR 11-7 validation

- Validation findings route to the Model Risk Committee first.
- Material findings reach the Chief Risk Officer and the audit committee.
- Supervisor examination is a separate channel; the validator's report is read at examination.

### EU AI Act Article 43 (Annex VII)

- Opening and closing meetings follow notified-body procedure.
- The certificate decision is the notified body's committee; the audit team recommends.
- Certificate is registered; the provider then issues the EU Declaration of Conformity (Article 47), affixes the CE marking (Article 48), and registers the system in the EU database (Article 71).

### Internal audit

- Opening is the kick-off with the business owner.
- Closing is the exit conference with the business owner and SMEs.
- Audit committee delivery is scheduled against the committee's calendar, commonly quarterly.

### NYC LL144

- There is no opening / closing meeting with a "regulator." Delivery is to the employer, who publishes the summary and retains the full report.
- The employer's distribution to candidates is governed by LL144's notice rules — a notice to candidates that an AEDT is in use and that a bias audit has been performed, usually with a link.<!-- needs-research: confirm current LL144 candidate-notice content requirements at reading time. -->

## Common delivery failure modes

- **Closing meeting skipped.** Engagement moves from fieldwork to report without the auditee seeing findings; unsurprising surprise in the management response.
- **Audit committee presentation without a private session.** Independence channel is silently closed.
- **Board report framed as reassurance.** Material weaknesses described as "areas for continued attention"; board does not understand the gravity.
- **Regulator-facing exhibit drafted by the auditor rather than the regulated entity.** Blurs the lines; creates privilege and independence issues.
- **Public publication with marketing commentary.** Management attaches marketing text referring to the report; auditor does not object; name-use rules violated.
- **Direct auditor-to-regulator back channel.** Prohibited outside specific designation agreements.

## Interfaces to adjacent chapters

- Chapters 1–4 produce what is being delivered.
- Chapter 6 picks up follow-up — the register that tracks the delivered findings through to closure.
- Chapter 7 covers the regulator-facing submission formats.
- `mod-101` covers the independence posture that governs every delivery event.
- `mod-112` picks up the audit-leadership layer that carries delivery patterns across engagements.

## Summary

- Opening and closing meetings are the formal engagement events where the auditor transfers understanding to the auditee; for ISO/IEC 42001 they are mandatory with prescribed content.
- Management response and report finalisation is a disciplined cycle with firm deadlines; cosmetic responses are addressed in the report, not negotiated into disappearance.
- Audit committee report-outs include a private session with the committee excluding management — the independence channel for resource, retaliation, and integrity matters.
- Board-level reporting is framed for a non-audit-literate audience without drifting into reassurance; what rises to the board is material, systemic, or regulatorily disclosable.
- Regulator-facing delivery normally routes through the regulated entity with the auditor's report as an exhibit; direct auditor-to-regulator delivery is limited to specific designation agreements.
- External publication (LL144 summaries, ISO certificates, SOC 3 reports, EU database entries) is distinct from distribution; the auditor controls the content, not the surrounding marketing.
- Privilege and confidentiality are distinct and not automatic; the auditor writes assuming discoverability and attends to the engagement letter's use restrictions.
- Each engagement shape has its own delivery adaptations — ISO, SOC, SR 11-7, EU AI Act Article 43, internal audit, LL144 — summarised in the delivery matrix.
