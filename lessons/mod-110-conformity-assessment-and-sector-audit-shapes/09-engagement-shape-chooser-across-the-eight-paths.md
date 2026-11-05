# Engagement-Shape Chooser Across the Eight Paths

## Motivation

A client arrives with: an AI system, a regulatory classification (sometimes several), an audience (board, customers, regulators, public), a timeline, and a budget. Behind them are the eight audit shapes this module and `mod-105` cover:

1. ISO/IEC 42001 certification audit (`mod-105`).
2. EU AI Act Article 43/44 conformity assessment (chapter 1).
3. EU AI Act Article 55 GPAI with systemic risk / Code of Practice adherence (chapter 2).
4. ForHumanity IAAIS engagement (chapter 3).
5. NYC LL144 independent bias audit (chapter 4).
6. SR 11-7 independent model validation (chapter 5).
7. FDA GMLP + PCCP audit / submission readiness (chapter 6).
8. NAIC / Colorado SB 24-205 / Illinois AIVIA / HB 3773 / state-overlay audit (chapter 7).
9. SOC-for-AI attestation under SSAE 18 + AT-C 205 / ISAE 3000 (chapter 8).

<!-- the chapter numbering continues ISO 42001 as "shape 1" from mod-105, so there are nine shapes across the two modules; this chapter is the integrator -->

The auditor who cannot choose between them cannot lead the engagement. The wrong choice fails on either regulatory adequacy or audience usefulness. This chapter is the chooser — a defensible decision procedure that moves from the client's facts to a single selected audit shape (or an **ensemble** of shapes where the facts require it), with the reasoning the engagement letter will record.

## The decision procedure

### Step 1 — Classify the subject matter

The auditor's first question is *what the audit is about*.

- **A management system for AI across the organisation?** The subject is the AIMS — ISO 42001 (shape 1) is the primary candidate.
- **A specific AI system placed on the EU market in a high-risk Annex III category?** The subject is a product — EU AI Act Article 43/44 (shape 2) is the primary candidate.
- **A GPAI model at Union level, especially one above the systemic-risk threshold?** The subject is a model — Article 55 / Code of Practice (shape 3) is the primary candidate.
- **A specific AI system being deployed at a US employer under LL144?** The subject is an AEDT — LL144 (shape 5) is the primary candidate.
- **A specific ML/LLM/GenAI model used at a Fed-supervised institution?** The subject is a model under SR 11-7 (shape 6).
- **An AI/ML SaMD heading for or already on the US market?** FDA GMLP + PCCP (shape 7).
- **An AI system used by an insurer, a Colorado deployer, or an Illinois employer?** State overlay (shape 8).
- **An entity-wide AI control environment for distribution to customers and procurement counterparties?** SOC for AI (shape 9).
- **A cross-stakeholder audit with ethics/trust/bias/privacy/security dimensions?** IAAIS (shape 4).

Where the subject matter spans multiple domains, the auditor moves to step 2 with multiple candidates.

### Step 2 — Determine the regulatory classification

For each candidate shape, confirm the client's facts place them within the shape's scope.

- **ISO 42001.** Any organisation can certify an AIMS; the question is not scope but desirability.
- **EU AI Act Article 43.** The system must be high-risk per Article 6 / Annex III, placed on the EU market or put into service in the Union, and the provider must be the regulated party (deployers face a different obligation set, Article 26).
- **Article 55.** The model must be GPAI (Article 3(63)) and designated as systemic-risk (Article 51); otherwise Article 53 baseline applies.
- **IAAIS.** Any system can be audited; the question is whether the client needs the FHCA criteria specifically.
- **LL144.** The tool must be an AEDT per DCWP's definition; the employer or employment agency uses it for NYC candidates or employees.
- **SR 11-7.** The institution must be Fed-/OCC-/FDIC-supervised, or otherwise adopt SR 11-7 as its MRM framework; the AI system must meet the model definition.
- **FDA GMLP.** The software must meet the FDA device definition and be in SaMD scope under FDA jurisdiction (US market).
- **State overlay.** The deployer must operate in the relevant state and the system must fit the state statute's scope (high-risk under Colorado; AEDT under NYC; video-interview under AIVIA; employment-decision under Illinois HB 3773; insurance use under NAIC-adopting state).
- **SOC for AI.** Any client wishing an attestation; the auditor must be a CPA firm (US) or an equivalent accounting firm (international) operating under IAASB/AICPA standards.

Classification is where misassignments happen — "high-risk Annex III" misread, AEDT scope misread, model vs. system confusion for GPAI. Chapter 4 is explicit on the LL144 definition; chapter 1 is explicit on Annex III; chapter 2 is explicit on Article 51 thresholds. Re-read those before this step.

### Step 3 — Determine the audience

The audit's audience often decides between otherwise-eligible shapes.

- **Regulator** — the audit output must be the shape the regulator accepts. EU AI Act notified-body certificate for market surveillance; FDA submission artefacts for CDRH; DOI examination evidence for insurance; DCWP summary for LL144; AG disclosures for Colorado; AI Office reports for Article 55.
- **Board / Audit Committee** — most shapes produce audit reports a board can consume; ISO 42001, SOC for AI, SR 11-7 validation, and IAAIS are typical board-audience choices.
- **Customers / procurement** — SOC 2 / SOC for AI is the usual procurement vocabulary; ISO 42001 certificates are used alongside; IAAIS has growing procurement recognition.
- **Public** — LL144 summary is published by the deployer; Code-of-Practice adherence statements by signatories; some IAAIS engagements. SOC 2 reports are typically restricted-use; SOC 3 is general-use but shallower.
- **Internal** — internal audit; IIA Standards shape the engagement; shape 1 (ISO 42001) and shape 6 (SR 11-7) are the usual internal-audit vehicles.

Where a single engagement must satisfy multiple audiences, the auditor usually concludes with an **ensemble** in step 4.

### Step 4 — Decide single-shape vs. ensemble

An **ensemble** is multiple shapes executed over the same AI system or program — ISO 42001 plus SOC for AI, LL144 plus Colorado SB 24-205 plus NYC-LL144 plus IAAIS, FDA GMLP plus EU MDR plus EU AI Act (under sectoral integration), SR 11-7 plus NAIC.

Ensembles are appropriate when:

- **Multiple regulatory regimes bind the same facts** — AEDTs in NYC and Colorado, SaMD in US and EU, GPAI with systemic risk also sold as a system in Annex III.
- **Audiences differ substantively** — the regulator needs the EU AI Act conformity assessment and the customer needs a SOC 2; both audits run.
- **Evidence reuse is practical** — ISO 42001 AIMS produces evidence that feeds both a SOC for AI attestation and an Article 17 QMS conformity assessment; running all three together is more efficient than any one alone.

Ensembles are *not* appropriate when:

- **One audit is enough.** Adding IAAIS to an already-complete ISO 42001 + SOC for AI delivers diminishing marginal value; auditor should recommend against.
- **The shapes are incompatible on independence.** If the same firm cannot execute two shapes because of self-review restrictions (e.g., the firm consulted on the ISO 42001 AIMS; it cannot attest under SOC for AI without strict team separation and even then may fail IESBA independence tests).
- **The budget does not support.** An ensemble requires honest resourcing; a thinly-resourced ensemble produces thin findings across the board.

### Step 5 — Independence, competence, and conflict check

Before confirming the shape(s), the auditor runs the independence posture (`mod-101` chapter 7) and competence check:

- **Independence.** Is the firm, lead auditor, and team independent from the client under the shape's rules? LL144 has a statutory independence test. ISO 42001 has 17021-1 clause 5 restrictions. SOC has IAASB/AICPA independence. FDA has agency-specific rules for third-party reviewers. IAAIS has ForHumanity-scheme rules.
- **Competence.** Does the firm have the credentials and demonstrable competence? AICPA licence for SOC; FHCA for IAAIS; BABL-/independent-auditor-for-LL144 experience; 42006 competence for ISO 42001 certification; medical-device regulatory credentials for FDA.

Independence and competence failures at step 5 send the auditor back to step 4 (change the shape, change the firm, change the team).

### Step 6 — Timeline, budget, and reporting cycle

- **Timeline.** CE marking deadline; LL144 annual cycle; SR 11-7 validation cadence; FDA submission date; customer-SOC-report due date.
- **Budget.** Honest audit-day estimate; the LL144 is typically a small engagement; EU AI Act Annex VII is substantial; SR 11-7 for a new GenAI model can be large.
- **Reporting cycle.** Annual, triennial, event-driven; some ensembles align to a single reporting cycle to reduce client overhead.

A shape that is substantively right but financially or temporally unsupportable gets flagged; the engagement letter must reflect any scope reduction explicitly.

## The decision as a table

The following table summarises the primary selection logic:

| Client fact | Primary shape | Common ensemble partners |
|-------------|---------------|--------------------------|
| Any mature AI organisation seeking certification | ISO 42001 | SOC for AI; sector overlays |
| Annex III high-risk AI system on the EU market | EU AI Act Article 43/44 | ISO 42001; sector overlay (Annex I Section A) |
| GPAI model above systemic-risk threshold | Article 55 / Code of Practice | AI Office engagement; ISO 42001 |
| Non-regulatory multi-audience audit, US context | IAAIS | ISO 42001; state overlays |
| AEDT used for NYC candidates / employees | LL144 | IAAIS; SOC for AI; Colorado overlay |
| ML/LLM at Fed-supervised institution | SR 11-7 | SR 23-4 vendor assessment; SOC for AI |
| AI/ML SaMD in US market | FDA GMLP + PCCP | QMSR / ISO 13485; EU MDR + AI Act sectoral |
| Insurer | NAIC Model Bulletin (as adopted) | SR 11-7-shaped validation; state AI overlays |
| Colorado deployer of high-risk AI | Colorado SB 24-205 | LL144 if AEDT; NAIC if insurer; IAAIS; SOC for AI |
| Illinois employer using AI employment decisions | AIVIA + HB 3773 | LL144 if NYC; Colorado if there; IAAIS |
| Entity-wide AI control attestation for customers | SOC for AI | ISO 42001; state overlays |

## Defending the choice — the engagement-letter paragraph

The engagement letter should include a short paragraph defending the chosen shape(s):

> *The engagement is executed under [shape] against [criteria], covering [scope], over [period], for the benefit of [intended users]. We considered [other candidate shapes] and selected [chosen shape] because [defensible reason: regulatory classification, intended-user vocabulary, independence posture, ensemble fit]. Where this engagement is one of an ensemble ([list]), we coordinate evidence per [engagement coordination plan].*

The paragraph is the auditor's record of the decision. A later challenge — regulator, litigant, or reviewing partner — reads it first.

## Common shape-choice failure modes

- **Treating ISO 42001 as a substitute for the EU AI Act.** The AIMS certificate is not a conformity assessment; a provider placing a high-risk Annex III system on the EU market needs the Article 43 route regardless of ISO certification.
- **Treating LL144 as a comprehensive bias audit.** LL144 is narrow (one AEDT, prescribed calculation, public summary); it is not an ethics or fairness audit; combining with IAAIS or a Colorado impact assessment is often needed.
- **Running SOC for AI without ISO 42001 or an equivalent control framework.** Clients sometimes propose SOC for AI *instead of* ISO 42001; SOC for AI tests the operation of the controls, but needs the controls to exist — an immature client is often not yet attestable.
- **Picking IAAIS to avoid a mandatory regime.** A deployer under Colorado SB 24-205 cannot substitute an IAAIS engagement for the statutory posture; IAAIS is persuasive evidence of reasonable care but is not a substitute for the statute's own deliverables.
- **Executing SR 11-7 as if it substitutes for an attestation.** SR 11-7 is validation — internal effective challenge; it is not an attestation to external users; a bank distributing an SR 11-7 validation to customers has structured the governance confusingly.
- **Executing an attestation on criteria that are not suitable.** Attestation frameworks require criteria meeting suitability; the client's internal framework is often not public enough to meet suitability — the auditor must insist on crosswalk to a public framework or on criteria-development that produces a suitable set.
- **Scoping an audit against an AI system that is in multiple regulatory regimes to only one of them.** The audit serves one audience; the other regulators' expectations are left unaddressed; client has unresolved compliance exposure.
- **Not running the independence check at step 5.** Firm's prior consulting disqualifies the attestation shape; auditor discovers at delivery.

## A worked example — a mid-market healthcare AI startup

A startup makes an AI/ML diagnostic SaMD for US hospitals and is expanding to the EU. Its investor board wants an annual third-party attestation for customer procurement. Its US regulatory posture requires FDA 510(k) with a PCCP. Its EU expansion lands it as a high-risk Annex III device with MDR + AI Act sectoral integration. The startup has mature engineering practices but no formal AIMS.

Step 1 — subject matter: the SaMD product plus the organisational control environment.

Step 2 — classification: FDA device, EU MDR / AI Act Annex I Section A regulated product, mid-market startup not yet subject to SR 11-7 or NYC LL144.

Step 3 — audience: FDA for US clearance; EU notified body for MDR + AI Act; customers and investors for an entity-wide attestation; board for governance.

Step 4 — ensemble: FDA GMLP + PCCP audit path (shape 7), EU MDR + AI Act sectoral conformity assessment (shape 2, sectoral-integrated), SOC for AI (shape 9), ISO 42001 (shape 1, optional but desirable for AIMS coherence).

Step 5 — independence: the firm attesting SOC for AI cannot have built the control framework; the firm doing FDA readiness can be separate from the SOC firm; the notified body is distinct from either.

Step 6 — timeline and budget: FDA readiness in Q2; 510(k) submission in Q3; EU MDR + AI Act assessment in Q4; SOC for AI period Jan–Dec with report in Q1 next year; ISO 42001 Stage 1 in Q1, Stage 2 in Q2.

The engagement-letter paragraph:

> *The engagement portfolio covers (i) FDA GMLP + PCCP audit of readiness for the Q3 510(k) submission; (ii) support for the EU notified body's MDR + AI Act Annex I Section A sectoral conformity assessment in Q4; (iii) ISO/IEC 42001 AIMS certification engagement (Stage 1 Q1, Stage 2 Q2, Surveillance Y2); (iv) SOC for AI examination under SSAE 18 + AT-C 205 for the period 1 January – 31 December against the client's documented control framework crosswalked to ISO/IEC 42001 and the NIST AI RMF 1.0 GenAI Profile. We considered IAAIS and SR 11-7 shapes; neither was adopted because IAAIS does not reach the FDA or MDR audiences and SR 11-7 does not fit the client's regulatory classification. The four engagements are coordinated under a single evidence-sharing plan, with independence partition between the ISO 42001 certification body and the SOC attestation firm maintained per ISO/IEC 17021-1 clause 5 and IAASB independence standards.*

The paragraph is defensible to any of the client's regulators, to the board, and to the client's investors.

## When the chooser rejects the audit entirely

Sometimes no audit shape fits because the client is **not audit-ready**:

- **No criteria.** The client has no documented control framework and no interest in adopting one. Attestation and certification are both impossible until criteria exist.
- **No management system.** ISO 42001 cannot be attempted at a client with no AIMS.
- **Regulatory classification uncertain.** The client is not sure whether their system is high-risk Annex III or an AEDT; audit proceeds only after classification is fixed.
- **Independence impossible.** The firm has consulting history that cannot be segregated; the engagement goes to a different firm.
- **Scope cannot be defined.** The client cannot describe the AI system in scope; readiness consulting precedes audit.

Declining the engagement — or deferring it to a readiness engagement — is sometimes the right output of the chooser.

## Summary

- The chooser is a six-step procedure: classify the subject matter; determine the regulatory classification; determine the audience; decide single-shape vs. ensemble; run independence, competence, and conflict checks; and confirm timeline, budget, and reporting cycle.
- Ensembles are appropriate when multiple regulatory regimes bind the same facts, when audiences differ substantively, or when evidence reuse is practical; inappropriate when one audit suffices, when shapes are independence-incompatible, or when budget cannot support honest work.
- The engagement-letter paragraph defends the chosen shape(s) against alternatives; it is the first thing a later challenge reads and the auditor's record of the decision.
- Common shape-choice failure modes include treating ISO 42001 as a substitute for the EU AI Act, LL144 as a comprehensive bias audit, SOC for AI as a replacement for the control framework itself, IAAIS as a replacement for a statutory regime, SR 11-7 as an external attestation, attestation on unsuitable criteria, scoping to one regime where several apply, and skipping independence checks.
- The chooser is the module's capstone — chapters 1–8 and `mod-105` are the shapes; this chapter is the integrator the auditor uses to lead the engagement.
