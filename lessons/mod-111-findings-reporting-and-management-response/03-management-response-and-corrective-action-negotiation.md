# Negotiating Management Response and the Corrective-Action Plan

## Motivation

A finding becomes real only when management accepts it, writes a response, and commits to a corrective-action plan. The management-response step is where the audit is most alive — and most at risk. Management arrives with incentives to downgrade the finding ("that's an observation, not a nonconformity"), to defer root-cause work ("we'll address this in the next planning cycle"), to redefine the condition ("that's not what the system does"), and occasionally to refuse the finding outright. Auditors who do not have a disciplined posture lose findings here.

The posture is prescribed by the standards. The IIA Global Internal Audit Standards treat management action plans as a required element of the engagement communication but preserve the auditor's independence over the finding itself. AICPA attestation guidance requires management's written representation and permits the auditor to retract or modify the opinion if the representation is unsatisfactory. ISO/IEC 17021-1 fixes the certification body's authority to determine whether a corrective action closes a nonconformity, not the auditee's. SR 11-7 validators sit under the Fed's expectation that the first-line-and-validator relationship cannot capture the validator's classification. Yellow Book GAGAS 6.21 extends professional skepticism through the exit conference and the resolution of management's disagreements.

This chapter walks the negotiation from close-out meeting through corrective-action-plan sign-off to re-opened-finding mechanics, calling the independence boundary at each step.

## The close-out meeting as discipline, not debate

The purpose of the exit (close-out) meeting is to **share the draft findings**, confirm facts, and collect management's immediate reaction. It is not a venue for deciding whether findings stand. Auditors who treat it as a venue for deciding negotiate findings away.

### Preparation

Before the meeting, the engagement team:

- Finalises the draft CCCER findings with evidence references.
- Prepares a single-page summary per finding so management can orient quickly.
- Pre-agrees internally on which findings can accept factual-correction edits and which cannot.
- Pre-agrees on the materiality claim and classification; any downgrade will require a documented reason, not a room pressure response.

### Facilitation

In the meeting:

- Walk each finding at the condition level first. "Is the condition factually accurate?" If management disputes a fact, the auditor records the dispute and resolves on evidence after the meeting — not in the room.
- Confirm the criterion is the correct standard; if management argues a different criterion applies, record it as a methodology point to resolve.
- Present the cause and effect; invite reaction without conceding.
- Present the recommendation and invite management's proposed action — not a critique of the recommendation, but their statement of what they plan to do.
- Agree on a response-due date that is realistic but firm.

### What the auditor does not do in the meeting

- Downgrade a finding classification under social pressure.
- Agree to delete a finding because management says "we'll fix it, no need to write it up." Findings are the audit; management's commitment is the response.
- Soften language to be "collaborative." The auditor's language has to survive subpoena.
- Promise an opinion.

## The written management response

Within a defined window after the close-out meeting (commonly 10–20 business days; agreed in the engagement letter), management submits a written response per finding. The response is attached to the finding and forms part of the final report.

### What a usable response contains

For each finding, management states:

- **Acceptance or disagreement**, with a basis if disagreeing.
- **The corrective-action plan** — *what* will be done, *who* owns it (role, not individual), *when* it will be complete, and *how* the auditor will verify closure.
- **Any interim mitigation** that is being put in place while the full fix is pursued.
- **Any formal acceptance of risk** where management elects not to fix — with a documented sign-off at the appropriate level (risk owner, Model Risk Committee, audit committee).

The response is management's. The auditor does not write it. The auditor *reviews* it against the finding and determines whether it is adequate to close.

### The disagreement path

Management may disagree with a finding. The auditor's response to disagreement is not to concede; it is to re-test, to re-cite the criterion, or — where the auditor has made a factual error — to correct the finding. If management persists in disagreement after re-test:

- For an internal audit under the IIA Global Internal Audit Standards, the standard requires the finding to be reported with management's documented disagreement; the auditor does not drop the finding, and the audit committee resolves the dispute.<!-- needs-research: confirm the specific standard number in the Global Internal Audit Standards governing "resolution of disagreement" at reading time. -->
- For an ISO/IEC 42001 audit under ISO/IEC 17021-1, the certification body determines whether the finding stands; the auditee's recourse is the certification body's complaint and appeal process.
- For a SOC/attestation engagement, management's written representation is a required part of the engagement; where management's representation is contrary to evidence the auditor must resolve, the auditor may issue a modified opinion or withdraw.
- For an SR 11-7 validation, the validator reports the finding with the first-line's disagreement documented; escalation routes through the Model Risk Committee and, in persistent cases, to supervisory attention.

The auditor's posture is: findings supported by evidence stand. Disagreement is recorded. It does not dissolve the finding.

## Evaluating the corrective-action plan

The CAP is the specific commitment. The auditor evaluates it against criteria that are themselves standards-grounded.

### The CAP must address the cause

A CAP that treats only the condition (fixing *this* instance) is cosmetic. "Re-run the fairness evaluation for the model that was flagged" fixes one data point; it does not fix the release-pipeline gap that permitted the model to deploy without evaluation in the first place. Auditors reject cosmetic CAPs explicitly and require a plan that addresses structural cause.

### The CAP must be executable

- Named role-owner with authority to act (not a RACI with four "Consulted" roles and no "Accountable").
- Completion date that is realistic and specific (date, not quarter).
- Measurable completion criterion the auditor can verify (deliverable, not state-of-mind).
- Dependencies and interim mitigations named.

### The CAP must be funded and prioritised

A CAP that lives on a risk-committee to-do list without budget or sponsor is a CAP that will slip. The auditor asks whether the organisation's budgeting and roadmap process has reserved capacity. If not, the CAP is likely to re-appear as a repeat finding next cycle. Repeat findings carry escalating classification (ISO/IEC 17021-1 §9.4.9 second indicator; IIA-pattern reporting to audit committee).

### The CAP must distinguish immediate correction from systemic corrective action

ISO/IEC 42001 terminology (inherited from Annex SL) distinguishes:

- **Correction.** The immediate act to eliminate the detected nonconformity (fix this record, re-run this control, re-issue this certificate).
- **Corrective action.** The action to eliminate the cause and prevent recurrence.

A CAP that has only a correction is incomplete. ISO auditors routinely refuse CAPs that do not separate the two. Other schemes track the same distinction under different names.

## When to re-open the finding

A CAP that the auditor has provisionally accepted still faces the closure review. On follow-up:

- The auditor tests the implementation evidence (chapter 6).
- If the CAP has been implemented but the finding is *still present* (the gate was added but it is not blocking; the procedure was updated but the behaviour is unchanged), the finding is **not closed**. The auditor re-opens.
- If implementation evidence is absent and management reports the fix as complete, the auditor re-opens the finding and may upgrade the classification.
- Repeat re-opening without progress is itself a material fact to communicate to the audit committee and (where applicable) the Chief Audit Executive.

The re-opened finding goes back into the register with a flag; its remediation now carries higher evidentiary weight.

## The cosmetic-response pattern and how auditors interdict it

A cosmetic response has one or more of the following tells:

- **Policy amendment with no control.** "We will update the policy to require X." No control enforces the policy; no evidence will be produced at follow-up.
- **Training as the corrective action.** "We will train the team on the importance of X." Training is a cause-of-knowledge intervention; most audit findings are cause-of-structure. Training can be *part* of a CAP, but is rarely sufficient alone.
- **Committee creation.** "We will form a review board." Governance without controls is theatre.
- **Future planning.** "This will be incorporated into the next planning cycle." Defers the action beyond the auditor's follow-up horizon.
- **Scope redefinition.** "The scope of the finding is narrower than described." Attempts to make the condition less material without fixing anything.
- **Platform migration promise.** "This will be resolved when we migrate to Platform Y." Platform migrations slip; the finding stays open behind them.

The auditor's response to cosmetic CAPs is explicit: the CAP is noted as **insufficient to close the finding**, the reason is stated, and the finding is not closed. The engagement report is clear that management's response is inadequate. The audit committee is the escalation path; the auditor does not fight the escalation at the manager level.

## Escalation paths

### To the audit committee

Where management refuses a finding, proposes only a cosmetic CAP, or allows a repeat finding to recur, the auditor escalates to the audit committee. IIA Global Internal Audit Standards and the SEC's expectations under the audit committee charter place the audit committee as the independent-channel recipient for such escalation. The escalation is:

- Factual (what the finding is, what management's response was, why it is inadequate).
- Without advocacy or editorialising.
- Delivered through the Chief Audit Executive where present; through engagement partner where the engagement is external.
- Documented in meeting minutes and in the engagement workpapers.

### To the certification body or the regulator

ISO/IEC 42001 certification audit findings that are not addressed route through the certification body's own processes to the market. SR 11-7 findings route through the Model Risk Committee to the Chief Risk Officer and (if material) to the supervisor. EU AI Act Article 16 provider obligations breaches identified by an internal or external auditor may trigger Article 20 corrective-action obligations and ultimately market-surveillance-authority notification. The auditor's role is to raise the finding at the correct severity; whether regulator notification is triggered is a *management* decision supported by *legal* counsel. The auditor does not freelance regulator notifications.

### To the board

Pervasive patterns — repeat findings across multiple cycles, systemic resistance to remediation, misstatements to the auditor — escalate to the board. In regulated institutions this is often governed by charter and by supervisory expectation (e.g., Fed's Heightened Standards for large banks). The auditor delivers facts; the board decides.

## Independence posture under negotiation

The auditor's independence is simultaneously **of mind** (SOCRATES: no bias, no undue influence) and **in appearance** (observers must be able to tell). The negotiation stage is where both are stressed.

- **The auditor does not draft the CAP.** Drafting implementation guidance is prohibited by AICPA, IIA, and ISO/IEC 17021-1 independence rules.
- **The auditor does not promise an opinion in exchange for a response.** "If you accept the finding we will downgrade it" is prohibited.
- **The auditor does not socialise findings informally to pre-negotiate away issues.** Pre-close-out one-to-one conversations with the auditee that soften findings are independence-of-appearance risks.
- **The auditor documents every negotiation touch-point.** Every meeting, call, and email that could later be read as the auditor conceding — logged with date, participants, and outcome.
- **The auditor's language stays neutral.** Negotiating language ("could we perhaps consider lowering…") is replaced with structural language ("the classification depends on the evidence of pattern; here is the evidence").

## Professional skepticism across the response cycle

Professional skepticism is required by Yellow Book GAGAS 6.21, by ISA 200, by AICPA AU-C 200, and by the IIA Global Internal Audit Standards. In the response cycle it means:

- Not accepting management's assertion that a condition is resolved without verification evidence.
- Not accepting a CAP commitment at face value without evaluating feasibility and funding.
- Weighing management's history of CAP execution (repeat-finding pattern) in the current response evaluation.
- Treating as a yellow flag any response that insists on redefining the condition rather than addressing it.

Skepticism is a professional stance, not a hostile one. It operates alongside the auditor's duty to be fair, to hear the auditee's facts, and to correct findings that are genuinely wrong. Professional skepticism and fairness are not opposites — they coexist in the auditor who weighs evidence rather than voices.

## Worked example — a response negotiation

Returning to the fraud-scoring finding from chapter 1 — the pipeline configuration gap that let a model deploy without the required AI SIA.

### Initial response (cosmetic)

> "Management acknowledges the finding. The AI SIA for `fraud-score-v3.2` will be completed retrospectively by 2026-12-31. The organisation will provide additional training on the AIMS procedure to the data-science team in Q1 2027."

**Auditor's assessment.** The response addresses the correction (retrospective SIA) and a cause-of-knowledge intervention (training). It does **not** address the structural cause (the release pipeline treats AIMS Owner sign-off as advisory rather than blocking). Without a pipeline-gate change, the same failure can recur tomorrow. The CAP is **insufficient**. The classification (major nonconformity, ISO/IEC 17021-1 §9.4.9 under the repeated-release pattern across four systems) is sustained.

### Revised response (acceptable)

> "Management accepts the finding at major-nonconformity classification. Corrective-action plan:
>
> 1. Correction: retrospective AI SIA performed for `fraud-score-v3.2` and for the three other in-scope releases since AIMS go-live. Owner: AIMS Owner. Due: 2026-11-30.
> 2. Corrective action: MLOps release pipeline configuration updated such that the 'promote-to-prod' action is gated on AIMS Owner sign-off for any release flagged as in-scope. Owner: Head of ML Platform. Due: 2027-01-31, with pipeline configuration diff and test evidence provided to the audit function on completion.
> 3. Corrective action: AIMS-PROC-004 §4.2 updated to specify the gating control and reviewed at the next AIMS management review. Owner: AIMS Owner. Due: 2027-02-15.
> 4. Interim mitigation: all in-scope releases between today and 2027-01-31 are subject to a manual AIMS Owner approval step enforced by a pre-release checklist review. Owner: Release Manager. Effective immediately.
> 5. Training will be provided to data-science staff on the revised procedure (secondary measure, not sole corrective action)."

**Auditor's assessment.** The response addresses correction and corrective action separately, names role-owners with dates, provides an interim mitigation while the gate is built, and verifies through evidence the follow-up test can reperform. **Acceptable for provisional close pending follow-up verification.**

## Interfaces to adjacent chapters

- Chapter 1 (CCCER) sets the finding content the response is negotiating over.
- Chapter 2 (classification) sets the vocabulary of the finding-level grade that the response sometimes tries to move.
- Chapter 4 (report authoring) determines the opinion type that flows from response adequacy.
- Chapter 6 (register and follow-up) is where the CAP tracks to closure.
- Chapter 7 (regulator-facing submissions) picks up when a finding and response jointly trigger a filing obligation.
- `mod-101` (audit position and independence) is the foundation of the posture this chapter prescribes.

## Summary

- The close-out meeting shares findings and collects reactions; it does not decide classifications.
- Management's written response per finding includes acceptance (or documented disagreement), a corrective-action plan separating correction from corrective action, a role-owner with a specific date, and a verifiable closure criterion.
- The auditor evaluates the CAP against cause-address, executability, funding, and the correction/corrective-action distinction; cosmetic CAPs are rejected on named grounds.
- When the response is inadequate, the finding is reported with the inadequate response attached; the audit committee (or equivalent oversight body) is the escalation path.
- Re-opening a finding is routine when CAP implementation does not clear the condition at follow-up; repeat openings carry escalating classification and board-level attention.
- Independence posture holds throughout: no CAP drafting, no opinion-for-response trades, no informal soften conversations, documented negotiation touch-points, neutral language.
- Professional skepticism per Yellow Book 6.21, AU-C 200, ISA 200, and the IIA Global Internal Audit Standards is the operating stance across the response cycle — weighing evidence, not voices.
