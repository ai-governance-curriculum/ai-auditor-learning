# exercise-01: EU AI Act Article 43 and 44 — Conformity Assessment Walkthrough

**Estimated effort:** 4 hours

## Objective

Execute a complete notified-body-style Annex VII conformity-assessment walkthrough for a fictional high-risk AI system. Produce the three artefacts the engagement would deliver: the QMS audit report, the technical-documentation assessment report, and the CE-marking decision memo — plus a one-cycle surveillance audit plan.

## Prerequisites

- Chapter [`01-eu-ai-act-articles-43-and-44-notified-body-conformity-assessment.md`](../01-eu-ai-act-articles-43-and-44-notified-body-conformity-assessment.md)
- Reading access to:
  - Regulation (EU) 2024/1689 (EU AI Act), full text or Annex III, Annex IV, Annex VII, and Articles 8–17, 43, 44, 47, 48, 71, 72, 73
  - Harmonised standards published in the OJ for AI Act (headline list; full reading not required) — e.g., prEN/EN standards on AI trustworthiness, risk management, bias, logging. <!-- needs-research: the OJ harmonised-standards list for the AI Act is still being populated; at reading time, consult the European Commission's current list -->
  - ISO/IEC 42001:2023 (for QMS mapping)
  - ISO/IEC 23894:2023 (AI risk management)
  - ISO/IEC 42005 (AI system impact assessment)
- `mod-104` chapter on evidence reliability
- `mod-105` chapter 1 (ISO 42001 audit frame) — the Article 17 QMS audit will sit beside it

## Scenario

**AegisBio Hiring-AI** is a provider of an AI-enabled resume-screening and candidate-ranking tool distributed to EU employers. The tool is used across Member States for high-volume hiring (10,000+ applications per month per enterprise customer) and produces a composite "fit score" that recruiters use to shortlist candidates. The system falls within Annex III point 4(a) (AI systems intended to be used for recruitment or selection of natural persons, in particular to analyse and filter job applications, and to evaluate candidates). AegisBio uses a proprietary transformer-based ranker fine-tuned from an open-weight foundation model, with structured-data features, LLM-generated candidate summaries, and an ensemble layer.

AegisBio is applying for Union technical documentation assessment under Annex VII (they have *not* applied harmonised standards in full) and has notified a notified body designated under Article 28. You are the lead notified-body auditor. The Stage-1-equivalent document review is complete; you are now planning and executing the Annex VII QMS assessment, the technical-documentation assessment, and the certification decision.

## Deliverables

### 1. QMS audit report (~2,500 words)

Structured per Article 17 (a)–(m). For each Article 17 sub-point:

- Procedure(s) tested.
- Evidence sampled (describe artefacts you would request).
- Design and operating conclusion (adequate / partial / non-conforming).
- Any finding, graded against a scheme comparable to ISO 17021-1 (major / minor / observation) and justified.
- The QMS-level conclusion (recommend for TDA / recommend remediation / decline).

### 2. Technical-documentation assessment report (~3,000 words)

Structured per Annex IV sub-points 1–9. For each sub-point:

- Content expected.
- Evidence sampled.
- Completeness assessment.
- Consistency with the system's actual behaviour (auditor's reperformance of claims where applicable — e.g., Article 15 accuracy metrics verified against the auditor's held-out sample).
- Findings.

Within the report, include focused subsections that treat Articles 9, 10, 12, 13, 14, 15 as separate deep-dives. Each article subsection names the auditor's test procedure, the evidence collected, and the conclusion.

### 3. CE-marking decision memo (~1,500 words)

Addressed to the notified body's certification committee. Must cover:

- Scope statement (provider, system, version, technical documentation reference).
- Certificate-or-not decision with reasoned justification.
- Conditions on the certificate (if any) — e.g., mandatory corrective actions with a defined closure deadline.
- Validity period (up to four years per Annex VII point 4.6) — justify length.
- Harmonised standards declaration — list standards applied in full, in part, or not at all; note the solutions adopted in place.
- Interaction with Article 47 Declaration of Conformity, Article 48 CE marking, Article 71 EU database registration.

### 4. Surveillance audit plan (~800 words)

For year 1 of the certificate's validity under Annex VII point 5. Must cover:

- Scope of the surveillance audit — what the auditor samples on the year-1 visit.
- Expected evidence per Articles 20 (corrective action), 21 (cooperation), 72 (post-market monitoring), 73 (serious-incident reporting).
- Triggers for unannounced audit under Annex VII point 5.
- Triggers for re-evaluation under Article 43(4) substantial modification.
- Reporting line back to the notified body.

## Starter guidance

- **Treat Annex IV as a checklist, not a theme.** Each sub-point is a row in the auditor's workpaper. Missing sub-points are findings regardless of how strong the rest of the dossier is.
- **Article 15 cybersecurity is AI-specific.** Generic ISO 27001 posture is not enough. Expect the audit to ask what the provider does about data poisoning, model extraction, adversarial examples, and prompt injection on the LLM-summarisation layer.
- **Article 10 bias examination is reperformable or it is not evidence.** If the provider's bias examination cannot be re-run by the auditor given the documentation retained, flag it — that is the pattern the NB audit was designed to interdict.
- **Instructions-for-use is a deployer-facing document.** The Article 13 test is whether an employer in the Netherlands, acting in good faith, could discharge Article 26 obligations using the IFU alone. If they would have to call AegisBio, Article 13 is not satisfied.
- **Human oversight is testable.** Article 14 is not an interface. The auditor should ask: "Given this specific candidate ranking, can a human recruiter actually override it, within what latency, with what logging?"
- Do NOT invent certification numbering, Article wording, or sub-point content. Cite accurately or mark `<!-- needs-research: ... -->` and move on.

## Acceptance criteria

The deliverables are accepted when:

- Lane selection (Annex VI vs. Annex VII) is explicitly addressed with an argument for Annex VII based on the scenario facts (no harmonised standards fully applied).
- The QMS audit report covers each Article 17 sub-point with a procedure and a conclusion; findings are graded consistently; the overall QMS conclusion is reasoned.
- The technical-documentation assessment covers every Annex IV sub-point and includes deep-dives on Articles 9, 10, 12, 13, 14, 15 each with named audit procedures.
- The CE-marking decision memo defends the certificate decision, its conditions, and its validity period; harmonised-standards treatment is explicit; interactions with Articles 47, 48, 71 are explicit.
- The surveillance audit plan covers Articles 20, 21, 72, 73 and the substantial-modification trigger of Article 43(4); unannounced-audit triggers are named.
- Findings are scenario-specific, not generic — they refer to AegisBio's resume-screening use, its LLM summarisation layer, its structured-data features, its high-volume operational context.
- No Article is invented; unverified citations are marked `needs-research` rather than guessed.

## Stretch goals

- Write a **second, parallel deliverable** assuming AegisBio has applied the harmonised standards in full — how does the audit differ? Where does the presumption of conformity narrow the auditor's work?
- Produce a **report-shape comparison** between the Annex VII certificate here and an ISO 42001 certificate — for the same provider, what each attestation covers and what neither covers.
- Author a **scope-objection letter** from AegisBio's regulatory counsel disputing the auditor's finding on Article 15 cybersecurity, and your response as engagement lead.
- Draft an **Article 73 serious-incident notification template** the provider would use post-certification — grounded in the chapter and in Article 73's enumerated content.
