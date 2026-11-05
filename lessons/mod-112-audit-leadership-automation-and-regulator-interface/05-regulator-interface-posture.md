# Regulator Interface Posture

## Motivation

At senior scope, the AI auditor regularly faces regulators — directly, through designated channels, or indirectly through the audited entity's own regulator relationship. How that interface is run matters: regulators compare the organisations they supervise, and the audit function's posture during an examination shapes the regulator's perception of the entity for years. A posture that is defensive, evasive, or scatter-shot damages the entity. A posture that is calm, organised, and candid builds the kind of trust that affects enforcement decisions on the margin.

Regulator interface is also where the auditor is most tempted to operate outside the auditor's professional boundary. The regulator asks a question; the auditor answers. The regulator makes an observation; the auditor agrees or disagrees. Each of those moves can preserve or lose the auditor's independence, the entity's privilege, the entity's defence posture, and the regulator's trust in both parties. The senior auditor's job is to know where the line is in advance and to keep the engagement team on it.

This chapter walks the posture the AI auditor holds for scheduling, scope negotiation, information-request response, interview preparation for management, finding communication, and remediation plan tracking. Chapter 6 covers audience-tuning across the specific regulator landscape the AI auditor faces.

## The threshold question — who talks to whom

Before any posture question is settled, the organisation (and the engagement) establishes who may speak to the regulator about what. In most settings:

- **The regulated entity** communicates with the regulator through designated contacts — the Chief Compliance Officer, the General Counsel, the function head whose scope the examination covers, and the operations or regulatory-affairs team.
- **External counsel** often leads sensitive communications, especially where enforcement is likely, where privilege is at stake, or where the regulator's inquiry has implications beyond the current examination.
- **The internal audit function** communicates when asked by the entity's designated contacts, or when the auditor's role gives direct standing (notified-body-designated audits; certification-body witness audits; some sector-specific designated channels).
- **External audit firms** communicate under their engagement letter and the firm's regulatory-communications protocol; the engagement partner is the usual point of contact.
- **Line engineers, data scientists, product managers** should not talk to the regulator outside structured interview settings arranged by the entity's designated contacts, and even then with preparation (see below).

This threshold is restated at every engagement. It is restated to the team on the first day. It is enforced through the engagement's own escalation protocol: if a regulator contacts a team member directly, the team member says "I will get back to you" and escalates immediately.

## Scheduling

Regulators initiate examinations on their own schedule. The entity's job (and often the auditor's supporting role) is to respond professionally and to negotiate the practical terms of the examination.

### Receiving the notice

A regulatory notice typically specifies:

- The regulator's identity and the examiner-in-charge.
- The scope (what will be examined).
- The period under review.
- The on-site or virtual mode.
- The anticipated duration.
- The initial document request.
- Any specific personnel the examiner wants to interview.
- A request to acknowledge the notice.

The entity acknowledges promptly. Non-acknowledgement is not a delay tactic; it is read as non-cooperation and starts the examination badly.

### Negotiating the terms

Within the regulator's prerogatives, the entity can negotiate practical terms:

- **Timing** — a scheduled examination that conflicts with another regulator's active examination, a system outage, or a critical business event can be adjusted; the request has to be specific and reasonable.
- **Scope** — scope clarifications are legitimate (for example, "the examination covers the fraud-detection model" — is this the model, the system, or the underlying feature store?). Scope reductions are usually not available, but scope clarifications prevent later misalignment.
- **Modality** — virtual vs on-site; most regulators have returned to on-site for significant examinations, but hybrid modes are negotiable for specific interviews.
- **Information-request format** — how documents will be delivered (secure file transfer, on-site reading room, redacted paper). The entity has a right to a method that protects privileged material and sensitive data.
- **Interview scheduling** — specific personnel's availability; counsel's attendance; interpreter needs.

The auditor's role here is advisory to the entity. The auditor identifies what the engagement can and cannot produce by when, which drives the entity's negotiation.

## Scope negotiation

Scope negotiation is not disputing the regulator's authority; it is clarifying the subject matter so both sides are testing the same thing.

### What is in scope

Typical scope elements in an AI-regulator examination:

- Specific AI systems or categories (by name, deployment, use case).
- Specific controls or processes (impact assessment process; post-market monitoring; incident response).
- Specific obligations (an article of the EU AI Act; an SR letter requirement; an NYC LL144 publication).
- A review period.
- Specific populations or decision points.

### Scope clarification protocol

- The entity's designated contact confirms the scope in writing after an initial scope conversation with the examiner.
- Ambiguities are listed and clarified in writing before fieldwork starts.
- Scope changes during the examination are documented — in a scope-change log the entity maintains and shares with the examiner.

### The auditor's input

The audit function's prior work on scoping (inventory, risk classification, control mapping) often informs the entity's understanding of what the examination covers. Where the examination cites a system the audit function has already looked at, the function's prior findings and status are produced promptly. Where the examination cites a system the audit function has not yet covered, the function may be asked to accelerate its work — a scope decision that rises to the CAE and the audit committee (see chapter 1 and chapter 8).

## Information-request response posture

Regulatory information requests are the most time-consuming and the most risk-laden part of the interface. The posture:

### Centralised intake

All information requests come in through the entity's designated contact, not to individual team members. The intake log captures:

- Request ID assigned by the entity.
- Request date.
- Requester (specific examiner).
- Request text (verbatim).
- Scope and period.
- Due date.
- Owner inside the entity.
- Legal review status.
- Response date.
- Response contents (document IDs, record counts, redactions, Bates range).
- Follow-up requests on the same thread.

### Response discipline

Each request is answered in writing, through the designated channel, by the deadline. The posture:

- **Deliver what was asked for.** Not more, not less. Delivering more creates new inspection surface; delivering less creates a non-cooperation signal.
- **Provide the document, not a summary.** The regulator inspects the primary artefact, not a paraphrase.
- **Redact per the privilege and confidentiality rules.** Counsel owns the redaction decisions; the audit function provides the technical support (identifying privileged content; applying redactions; producing a redaction log).
- **Produce a Bates numbering trail.** Each produced document has a stable identifier the examiner can reference.
- **Preserve chain-of-custody.** The produced document's provenance is documented so later questions can be answered.
- **Track open items.** Where a request requires time, the entity communicates the plan and the estimated delivery date; silence is read as stalling.

### What the audit function produces

For AI-specific requests, the function typically produces:

- Workpapers from completed engagements (within the function's own production protocol).
- Reports and executive summaries.
- Findings registers and corrective-action status.
- Evidence of specific tests (fairness evaluations; red-team sessions; impact assessments).
- Interview memos (with interviewee review).
- Continuous-audit output (CCM exception reports; dashboards).

Audit workpapers are typically protected to some extent by the audit function's own protection claim (auditor's privilege varies by jurisdiction and scheme). Production of audit workpapers to a regulator is a counsel-directed decision; the audit function does not freelance production.

### What the audit function does not produce

- Privileged material directed by counsel (attorney-client, work-product).
- Personal notes not incorporated into workpapers (treated carefully — if they are in fact relied upon, they are workpapers).
- Draft findings that were not finalised (unless the regulator's inquiry specifically covers the drafting process).
- Opinions on what the regulator should do.

## Interview preparation for management

The regulator will interview management. The audit function prepares management for the interview the way it would prepare an interviewee in its own engagement.

### Preparation session

- **Scope reminder.** What the interview covers and what it does not.
- **Facts review.** The facts management should know cold — the system's purpose, lifecycle, controls, testing, incidents, remediation.
- **The honesty standard.** Answers must be truthful and based on direct knowledge; "I do not know" is a valid answer; speculation is not.
- **The scope-of-answer standard.** Answer the question asked; do not volunteer beyond. Overflow invites follow-up and creates new surface.
- **Tone.** Calm, cooperative, specific. Not defensive; not casual.
- **Privilege reminders.** What is privileged and should not be discussed; how to flag privilege if asked.
- **Who else is in the room.** Counsel's attendance; the entity's designated contact's attendance; a note-taker.
- **Documents.** What documents will be in front of the interviewee and how to refer to them.

### Rehearsal

For significant interviews (executive interviews; model-risk-officer interviews; post-incident interviews), the audit function may run a mock interview with the interviewee, using plausible questions from the regulator's typical approach. The rehearsal:

- Surfaces knowledge gaps the interviewee can close before the real interview.
- Identifies risky question patterns (leading questions; multi-part questions; questions that smuggle premises).
- Reinforces the discipline on scope-of-answer.
- Is documented as preparation, not as coaching — the interviewee is preparing to tell the truth accurately, not to tell a story.

### What the auditor does during the interview

If the auditor attends (sometimes designated, sometimes present as a supporting note-taker):

- Takes clean notes.
- Flags to counsel any question that approaches privilege.
- Does not answer on the interviewee's behalf.
- Does not correct the interviewee on the record unless specifically asked; corrections are handled through the entity's designated contact after the interview.

## Finding communication to the regulator

When the regulator closes an examination, there is an exit meeting, an examination report, and a response cycle.

### Exit meeting

The regulator walks their findings. The entity (with the auditor if the auditor is designated):

- Listens.
- Takes notes.
- Asks clarifying questions where the finding is genuinely unclear.
- Does not argue finding-by-finding at the exit meeting.
- Thanks the examination team.

Arguments and counter-positions are reserved for the formal response.

### Examination report

The regulator issues a report. The entity's response window is finite (varies by regulator; commonly 30 days). The response:

- Acknowledges receipt and the issue dates.
- Addresses each finding individually.
- Accepts or disputes each finding with reasoned basis.
- Commits to specific remediation with named owners and dates.
- Preserves the entity's position on findings it does not accept.

The audit function's content supports the response. The function may have prior findings that pre-date the regulator's finding — these are produced to show the entity was already aware and working on remediation. The function may disagree with the regulator's finding — the disagreement is documented, routed through counsel, and reflected in the response if the entity so chooses.

### Finding classification cross-walk

Regulator findings have classifications (MRA / MRIA for Fed; Class I / II / III for FDA 483; critical / high / medium / low for most other regulators). The audit function cross-references regulator classifications to its own classification (`mod-111` chapter 2) so remediation tracking (next section) can proceed on the entity's own system.

## Remediation plan tracking

Regulator-issued findings generate remediation commitments the regulator will later inspect for closure. The audit function tracks:

### The regulator-finding register

Separate from (or an overlay on) the audit's internal findings register:

- Finding ID (regulator's and entity's).
- Classification.
- Due date for initial response.
- Response committed remediation.
- Owner inside the entity.
- Milestone dates.
- Status.
- Evidence of completion (artefact IDs, workpaper references).
- Verification date and verifier.
- Regulator closure letter reference (where the regulator formally closes).

### Continuous update to the audit committee

The audit committee sees the regulator-finding register alongside the audit's internal findings register. Repeated or overdue items are escalated. Chapter 8 details the reporting shape.

### Regulator revisits

Many regulators revisit specific findings in follow-up examinations. The audit function anticipates:

- Which findings the next examination is likely to cover (recent closures; disputed items; high-classification items).
- What evidence will be produced to demonstrate closure (the evidence is produced *before* the next examination, stored, and ready).
- What the entity will say about residual risk or implementation challenges.

### Pattern analysis

The audit function monitors patterns across regulator findings — repeat findings across cycles signal deep structural issues; cross-regulator-overlap findings signal enterprise risk that no single regulator sees. Pattern analysis is a workpaper that supports the CAE's annual report to the audit committee.

## Common failure modes

- **Direct channel between a team member and the examiner.** Prohibited outside the entity's designated contacts.
- **Over-production.** Delivering more documents than the request asked for; creates inspection surface.
- **Under-production.** Delivering less than the request asked for; non-cooperation signal.
- **Summary instead of primary.** Giving the examiner a summary memo in place of the primary document.
- **Freelance redaction.** Someone redacts without counsel's direction; privilege is waived or over-protected.
- **Freelance interview.** An engineer is cornered in the hallway and answers freely; the entity's position is inadvertently established.
- **Freelance commitment.** Someone commits to a remediation timeline in the exit meeting; the commitment is binding.
- **Freelance interpretation.** Someone opines on how the regulator will likely react; treated as entity position.
- **No preservation.** Relevant records are not preserved from the moment of notice; destruction after notice is sanctionable.
- **Loose handling of parallel examinations.** Multiple regulators examining in parallel; responses inconsistent across regulators.

## Document preservation

From the moment of examination notice (and often earlier, when there is "reasonable anticipation" of an examination or investigation), the entity preserves records relevant to the scope. The audit function:

- Supports the preservation hold by preserving its own workpapers.
- Suspends routine destruction policies for in-scope records.
- Documents the preservation action.
- Resumes routine destruction only when counsel directs.

## Summary

- Senior AI auditors face regulators regularly; the interface has a professional posture that preserves the entity's position, the audit function's independence, and the regulator's trust.
- Communication flows through the entity's designated contacts; direct channels between team members and examiners are prohibited outside those contacts.
- Scheduling and scope negotiation address timing, modality, and scope clarity in writing; the audit function's prior work informs scoping.
- Information-request response is centralised, deadline-disciplined, and document-primary; the audit function produces workpapers under counsel's direction with Bates numbering and chain-of-custody.
- Management is prepared for interviews on scope, facts, honesty standard, scope-of-answer discipline, and privilege reminders; rehearsals address predictable question patterns.
- Finding communication starts at the exit meeting (listening, clarifying, not arguing), proceeds to the examination report and the entity's written response, and continues into a tracked regulator-finding register overlaid on the audit's internal register.
- Remediation is tracked continuously; evidence of closure is prepared before the regulator's revisit; pattern analysis identifies structural issues across cycles.
- Common failure modes — direct channels, over- or under-production, summaries in place of primaries, freelance redaction, interview, commitment, interpretation; insufficient preservation; inconsistent cross-regulator responses — are the senior auditor's recurring focus.
- Document preservation from notice (or reasonable anticipation) is enforced across the audit function's workpapers and across the entity's records in scope.
