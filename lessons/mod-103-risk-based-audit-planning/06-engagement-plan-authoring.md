# Authoring the Engagement Plan — Team, Timing, Logistics, Evidence Requests, Meetings

## Motivation

Chapter 4 scoped a single AI-system audit; chapter 5 scoped an AIMS audit. Both chapters produced a signed scope memo. The scope memo is the *what*. The engagement plan is the *how* — the team, the calendar, the information-request list, the interview schedule, the evidence-request shape, the escalation path, the kickoff and closing meetings. **ISO 19011:2018** clause 6.3, **ISO/IEC 17021-1** clause 9.2.3, **ISAE 3000 (Revised)** paragraphs 40–44, **AT-C 105** paragraph .50, and **IIA Standards 2024** Standard 13.3 all require an engagement plan with roughly the same structure. The naming varies, the content converges.

The engagement plan is also a *coordination* artifact — the first-line and second-line owners who supply evidence need to see what is coming when, the audit committee needs to see commitment on timing, specialists need to be booked. Poorly-authored engagement plans cause fieldwork compression, late evidence, unavailable interviewees, and specialist-booking collisions — all of which erode independence and audit quality.

## The nine elements of an AI engagement plan

1. Team composition and responsibilities
2. Timing — the end-to-end timeline
3. Logistics — on-site / off-site / hybrid, access, tools
4. Information-request list (IRL)
5. Interview schedule
6. Evidence-request shape
7. Working-paper and evidence-handling conventions
8. Escalation path
9. Opening (kickoff) and closing meeting shape

The rest of the chapter walks each.

## 1. Team composition and responsibilities

The AI engagement team is composed under three constraints: competence (does the team have the skills?), independence (is the team free of threats for this subject matter?), and capacity (is the team available for the planned window?). The core roles:

- **Lead auditor / engagement leader** — accountable for the audit opinion. For certification work, ISO/IEC 42001 Lead Auditor credential; for internal work, IIA CIA (ideally with AI-audit credential); for ISAE 3000 / AT-C 205 work, the signing engagement partner. Workload: planning, team direction, review of all workpapers, report issuance.
- **Audit staff** — execute the planned procedures. For AI audits, typically 2–4 staff per engagement, each with a credentialed baseline (CIA / CISA / AAIA / ISO 42001 LA / CPA) and an AI-domain familiarity trained to the firm's AI-audit methodology.
- **Technical specialists under ISA 620 — AI / ML** — brought in for re-performance of eval suites, red-team tests, bias analyses, interpretability exercises. ISA 620 paragraph 9 requires the auditor to evaluate whether the expert has the necessary competence, capabilities, and objectivity; paragraph 11 requires agreement on the nature, scope, and objectives of the work.
- **Technical specialists — security / privacy** — brought in for ISO/IEC 27001 / 27701 integration points, model-serving infrastructure security, data-pipeline privacy controls.
- **Technical specialists — sector** — SR 11-7 MRM for banks, FDA GMLP + QMSR for medical-device makers, NAIC market-conduct for insurers, AEDT impact-ratio methodology for NYC LL144 bias audits.
- **Technical specialists — legal / regulatory** — EU AI Act applicability analysis, Colorado AI Act operator / developer classification, NYC LL144 covered-entity analysis. Where in-house, independence check for first- and second-line entanglement.
- **Independent reviewer / engagement quality reviewer (EQR)** — mandatory for certification audits under ISO/IEC 17021-1 clause 9.5 and for public-interest attestations under ISQM 2. For internal audits, IIA Standards 2024 Domain II on quality assurance and the function's quality-review process. The EQR is not on the engagement team — the review is independent of the work being reviewed.

The plan records, per role: the person assigned, the credentials held, the independence check outcome (no self-review threats from prior consulting / control-design work on this subject matter), the hours budgeted, and the fallback if the person becomes unavailable.

### An ISA 620 specialist-engagement checklist

For every ISA 620 specialist on the team the lead auditor documents:

- Competence (credentials, experience on comparable AI subject matter).
- Capabilities (access to tools, compute, data environments needed).
- Objectivity (no prior involvement in the control / model being audited; no financial or relational ties to the responsible party).
- Scope of work (procedures the specialist will perform; the work-product format).
- Direction (who directs the specialist; who reviews the work).
- Use of the specialist's work (whether the auditor adopts the specialist's findings, re-performs, or cites with reliance language).

The checklist is a workpaper. Specialists added mid-engagement get the same checklist before onboarding.

## 2. Timing — the end-to-end timeline

AI engagements have a long tail of pre-engagement activities and a long tail of post-fieldwork activities, both of which have to be budgeted. A realistic single-system engagement (reasonable-assurance examination, 450 hours from the chapter-2 worked row):

| Phase | Weeks | Primary activities |
|---|---|---|
| Pre-engagement | –4 to –1 | Scope sign-off, materiality workpaper, team confirmation, IRL drafting, independence checks, engagement letter |
| Fieldwork kickoff | 0 | Kickoff meeting, IRL delivery, interview-schedule lock, walkthrough |
| Fieldwork — controls design | 1 to 2 | Walkthroughs, design evaluation, documentation review |
| Fieldwork — operating effectiveness | 3 to 5 | Sampling execution, re-performance, specialist work |
| Preliminary findings | 6 | Factual accuracy clearance, management-response drafting |
| Reporting | 7 to 8 | Report drafting, EQR, issuance |
| Post-issuance | 9+ | Debrief, follow-up planning, archival |

For an AIMS Stage-2 engagement the fieldwork window is longer (per 42006 Annex A) and the preliminary-findings phase is more structured because non-conformity grading requires client dialogue. For continuous auditing the phases look very different and are covered in `mod-112`.

### Critical timing anchors

- **Independence checks before engagement acceptance**, not during fieldwork. Finding a specialist's conflict in week 4 means rework.
- **IRL delivered 3–4 weeks before fieldwork** so the responsible party can assemble evidence. Later delivery compresses fieldwork and the team either accepts weak evidence or drops procedures.
- **Interview-schedule lock 2 weeks before kickoff**. AI-system interviewees are typically ML engineers, product managers, SREs, security engineers, legal counsel — all calendars that fill fast.
- **Factual-accuracy review before closing meeting**. Each finding is cleared on fact with the responsible-party owner before the finding is reported.
- **EQR window after factual accuracy, before issuance**. EQR is not a rubber stamp; scope two weeks for a meaningful review.
- **Report distribution within the window promised in the engagement letter**. Late reports erode the audit function's credibility.

## 3. Logistics — on-site / off-site / hybrid

Logistics for AI audits have shifted dramatically post-2020. Most audit work is now hybrid; some fieldwork is still on-site. Decisions the plan makes:

- **On-site days** — walkthroughs of operations centres, incident-response simulations, management-review meetings attended in person, certain red-team exercises observed in a secure environment. ISO/IEC 42006 and 17021-1 clause 9.2 discuss acceptable off-site percentages for certification audits with risk-based constraints. <!-- needs-research: confirm the current remote-audit guidance applicable to ISO/IEC 42001 audits — IAF MD 4 and the IAF's remote-audit mandatory documents were updated in 2022–2024 -->
- **Off-site / remote days** — documentation review, inference-log inspection via secure data room, interviews via video, re-performance of eval suites in auditor's own compute environment.
- **Secure environment access** — model weights and training data often cannot leave the organisation's environment; the auditor needs a locked-down VM or workstation. Access requires provisioning lead time (often 2–4 weeks); the plan books it before fieldwork starts.
- **Tools** — the audit function's working-paper system, sampling tools, re-performance notebooks, evidence-handling conventions (chapter 6 §7).
- **Clearance** — for government or defence-adjacent audits, clearance requirements can add months. Handle at pre-engagement.
- **Confidentiality posture** — NDAs, information-handling, pre-release disclosure constraints. ISO/IEC 17021-1 clause 8.5 and ISAE 3000 paragraph 70 apply.

## 4. Information-request list (IRL)

The IRL is the single most-referenced engagement artifact in fieldwork. Structure:

```
ID    | Criterion     | Artifact                              | Owner        | Due         | Format           | Status
IR-01 | C-42001-6.1.2 | AI risk-assessment procedure v2.3     | AIMS owner   | 2027-01-10  | PDF              |
IR-02 | C-42001-6.1.2 | Risk-register extract (all systems)   | Risk mgr     | 2027-01-10  | CSV              |
IR-03 | C-42001-6.1.4 | FRIA for system INT-0042              | AI product   | 2027-01-15  | PDF              |
IR-04 | C-NIST-M-2.3  | Eval suite config INT-0042 v1.9       | ML eng       | 2027-01-15  | YAML + metrics   |
IR-05 | C-NIST-M-2.3  | Eval run log INT-0042 2026-Q4         | ML eng       | 2027-01-15  | JSONL            |
...
```

Attributes per item:

- **ID** — stable identifier.
- **Criterion** — the auditable criterion the artifact serves (traceability from `mod-102`).
- **Artifact** — a precise description, not "all evaluation evidence" — "eval suite configuration YAML for model version INT-0042 v1.9 as deployed in Q4 2026".
- **Owner** — named first-line or second-line owner.
- **Due date** — when the auditor needs it; typically 1–3 days before the procedure that consumes it.
- **Format** — document type, data format, access method. If the artifact cannot leave the organisation (model weights, raw PII), note the inspection method.
- **Status** — tracked through fieldwork (requested, received, received-incomplete, received-late, accepted).

An AI-audit IRL is typically 80–200 line items for a single-system engagement, 300+ for a Stage-2 AIMS audit. The IRL is delivered 3–4 weeks before fieldwork with the engagement letter; the responsible party has a single point of contact to coordinate collection.

Late or missing artifacts are findings about the control environment, not just engagement nuisances. The IRL status log is a workpaper.

## 5. Interview schedule

AI engagements interview more roles than traditional financial audits. For a full-scope AI-system audit the typical interview list:

- **Top management or executive sponsor** — AIMS ownership, policy commitment, resource allocation.
- **AI governance analyst** (L15) — inventory, impact assessments, intake records.
- **Product / business owner** of the AI system — intended purpose, deployment context, user populations.
- **ML engineers / data scientists** — model development, training data governance, evaluation methodology.
- **AI risk engineer** (L25) — the hands-on fairness / privacy / robustness / red-team tooling for this system.
- **AI evaluation engineer** (L35) — release gates, pre-release eval procedures, go-no-go documentation.
- **MLOps / platform engineers** — model serving, monitoring stack, change management.
- **SRE / on-call** — incident records, post-mortems, runbooks.
- **Security / DFIR** — model-level security posture, adversarial-attack response.
- **Privacy / DPO** — DPIA, FRIA, data-flow mapping, cross-border data transfer.
- **Legal counsel** — regulatory classification, contractual obligations, user-communication posture.
- **Internal audit (prior cycle)** — prior-finding closure, management-response history.

Each interview is scheduled at a time that matches the procedure consuming it. Interviews are not fillable in the middle of fieldwork — they have fixed slots and preparation requirements. ISO 19011:2018 clause 6.4.3 covers interview conduct.

### Interview-memo discipline

Every interview produces a memo:

- Date, attendees, topics.
- Questions asked and answers summarised (not verbatim unless the transcript is held).
- Documents referenced.
- Follow-up items (additional evidence to request, inconsistencies to reconcile).
- Attendee confirmation of memo accuracy before the memo is filed.

The memo is a workpaper. Uncorroborated inquiry under ISA 500 (chapter `mod-102`) is low on the evidence hierarchy; the memo should name the corroboration the auditor sought or will seek.

## 6. Evidence-request shape

Beyond the IRL (which lists artifacts), the plan names the *shape* of evidence the engagement will accept:

- **Format and provenance** — documents in their native format with metadata (not screenshots of documents), logs with system-generated timestamps (not exported-and-edited CSVs), configuration as it existed in production at the sampled time (not the current version).
- **Chain of custody** — who extracted the evidence, from which system, at what time, by which query / command. For AI audit, the extraction query is often the audit sample selector (a specific SQL / API call / log query); the query itself is a workpaper.
- **Independence of evidence** — where possible, prefer evidence generated by systems the responsible party does not control (external attestations, immutable logs in a tamper-evident store, blockchain-backed audit trails where available). For most AI subject matter, evidence is first-line-generated; the auditor corroborates by re-performance.
- **Re-performance evidence** — the auditor's own notebook, dataset snapshot, model-inference log from the auditor's execution. ISA 500 paragraph A5 and ISA 530 cover this.
- **Specialist work-product** — ISA 620 specialist outputs are workpapers; the auditor records the specialist's procedures and findings in auditor-controlled storage.

The plan names a **rejection posture** — what evidence the engagement will not accept. Common rejections:

- Screenshots of inference logs without the underlying query.
- Verbal confirmations of control execution without a record.
- Evaluation metrics without the dataset, run configuration, and execution log.
- Vendor attestations whose scope does not match the organisation's use.
- Evidence created post-sample-date to backfill a control that was not operating.

## 7. Working-paper and evidence-handling conventions

The audit function has standing conventions; the engagement plan references them rather than restates them. The conventions cover:

- Workpaper naming and indexing.
- Evidence storage (approved tooling, encryption at rest, retention schedule).
- PII / sensitive-data handling (minimum-necessary principle; secure-destruction schedule).
- Version control and review-trail.
- Independent-reviewer sign-offs and their location in the workpaper.
- Report-issuance workflow and record-retention.

For regulated engagements the conventions must match the regulator's inspection expectations (PCAOB, PCA, national accreditation body for ISO work, DPA for privacy-adjacent AI audit).

## 8. Escalation path

The engagement will hit obstacles that the lead auditor cannot resolve inside the engagement. The plan names the escalation path explicitly:

- **Scope dispute** — responsible party contests scope mid-engagement. Escalate to engagement leader → CAE (internal) / engagement partner (external) → audit committee chair / responsible party's AIMS owner.
- **Access impediment** — responsible party cannot or will not produce evidence. Escalate to CAE / engagement partner; under ISAE 3000 paragraph 73 and AT-C 105 paragraph .70 this can be a reportable scope limitation.
- **Independence threat emerges mid-engagement** — a team member discovered to have prior involvement. Remove and replace, document, consider rework.
- **Suspected fraud or illegal act** — ISA 240 (fraud), ISA 250 (laws and regulations) by analogy. Report path for AI subject matter typically runs to the audit committee and legal counsel; in some jurisdictions (US SOX, EU, UK) there are specific external-reporting duties.
- **Significant deficiency discovered mid-engagement** — early communication to management under ISA 265 / AT-C 105 obligations.
- **Specialist unavailability** — fallback specialist or re-sized procedure.
- **Regulator contact during engagement** — regulator requests information from the engagement team or opens an inquiry. Legal-counsel involvement is immediate.

Each escalation path names the trigger, the decision owner, the communication channel, and the documentation required.

## 9. Opening (kickoff) and closing meeting shape

### Kickoff

- Attendees: engagement team; responsible-party sponsor; AIMS / system owner; first- and second-line evidence coordinators; internal audit (if an external engagement at an organisation with an internal audit function); CAE (if internal).
- Agenda: scope recap; criteria recap; timeline recap; IRL walkthrough; interview schedule confirmation; logistics; escalation path; communication protocol; expected finding-communication cadence; confidentiality and independence reminders.
- Output: kickoff minutes, signed; action items; confirmed next steps.

### Closing

- Attendees: as kickoff, plus EQR and audit-committee representative (internal) or the engaging party decision-maker (external).
- Agenda: preliminary findings; factual-accuracy confirmation; management responses; residual issues; path to final report; distribution list; follow-up cadence; expected re-audit cycle; lessons-learned.
- Output: closing minutes; agreed action-item list; agreed report-issuance timeline.

Both meetings are workpapers and audit evidence. ISO 19011:2018 clauses 6.4.4 and 6.4.10 shape them for ISO audits; the shape carries forward for internal and attestation engagements.

## Putting it together — a compact engagement-plan skeleton

```
Engagement:        <scope memo ref>
Team:
  Lead:             <name, credentials, hours>
  Staff:            <name, credentials, hours> × N
  ISA 620 experts:  <name, scope, hours> × M
  EQR:              <name, credentials>
  Independence:     <memo ref>
Timing:
  Kickoff:          <date>
  Fieldwork:        <start–end>
  Prelim findings:  <date>
  Closing:          <date>
  Report:           <date>
Logistics:
  On-site days:     <count, location, purpose>
  Access:           <provisioning plan>
  Tools:            <wp system; sampling; re-performance env>
IRL:                <attached; version>
Interview schedule: <attached; version>
Evidence shape:     <conventions; rejection posture>
Conventions:        <audit-function standing-conventions ref>
Escalation path:    <per trigger; decision owner; comm channel>
Kickoff shape:      <agenda; attendees; output>
Closing shape:      <agenda; attendees; output>
Approvals:          <lead auditor; CAE / engagement partner; responsible party scope sign-off>
Date:               <plan date; revision log>
```

## Common failure modes

- **IRL delivered late.** Fieldwork compresses; evidence is thin; findings are weak; management legitimately complains.
- **Specialist booked without independence check.** Discovered mid-fieldwork; rework or scope-limitation.
- **Interview schedule not locked.** Interviewees unavailable; interviews pushed into reporting phase; factual accuracy compressed; EQR squeezed.
- **Escalation path implicit.** The lead auditor hits a dispute and resolves it informally; audit-committee visibility is zero; defensibility collapses.
- **Kickoff doesn't actually walk the plan.** The responsible party is surprised by the IRL or timing; cooperation erodes.
- **Factual-accuracy phase skipped.** Findings are reported with errors; management-response letter retracts findings; audit function's credibility hit.
- **EQR treated as a signature.** The reviewer does not review; a weak workpaper is issued; regulator inspection surfaces the weakness.
- **Follow-up not scheduled.** Findings close on paper without implementation evidence; next cycle re-finds them.

## Summary

- The engagement plan converts the scope memo into an executable programme: team, timing, logistics, information-request list, interview schedule, evidence-request shape, working-paper conventions, escalation path, kickoff and closing meeting shape.
- Team composition balances competence (credentialed AI-audit roles plus **ISA 620** specialists), independence (per-role checks before acceptance), and capacity.
- Timing anchors on pre-engagement independence checks, IRL delivery 3–4 weeks before fieldwork, interview-schedule lock, factual-accuracy phase, and EQR window.
- IRL is the most-referenced engagement artifact and the IRL status log is a workpaper and a potential finding source.
- Interview and evidence discipline — memo per interview, format and chain-of-custody per artifact, rejection posture for backfilled evidence — is what separates a defensible engagement from an opinion.
- Escalation paths are named by trigger with decision owner and channel; ad-hoc escalation is the failure mode most engagements fall into.
- Kickoff and closing meetings are structured, minuted, signed, and are evidence.
