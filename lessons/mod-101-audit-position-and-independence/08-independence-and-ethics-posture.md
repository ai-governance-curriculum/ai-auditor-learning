# Independence, Ethics, and Professional Skepticism for an AI Engagement

## Motivation

A third-line audit opinion exists only because someone trusted that the auditor was independent of the thing being audited. Lose that and the opinion loses its force. Independence in AI engagements is harder than in traditional audits because the engineering talent pool is small and the auditor has often previously consulted, researched, or built the very tooling now being audited. This chapter builds the independence-and-ethics posture statement an AI auditor must author and sign at engagement acceptance, map by threat category, with safeguards and the professional-skepticism test applied to AI-specific fact patterns.

## The four reference ethics frameworks you work across

AI engagements live simultaneously under multiple ethics codes. The vocabulary rhymes across them; the operating detail differs enough that you must know which one is in force for the engagement.

- **IIA Global Internal Audit Standards 2024 Domain II — Ethics and Professionalism.** Integrity, Objectivity, Competency, Due Professional Care, Confidentiality. Applies to internal audit engagements.
- **IESBA International Code of Ethics for Professional Accountants (including the International Independence Standards).** Five fundamental principles (Integrity, Objectivity, Professional Competence and Due Care, Confidentiality, Professional Behaviour), the conceptual framework, and the Independence Standards for audit and assurance engagements. Applies to IAASB (ISAE 3000) engagements via national adoption.
- **AICPA Code of Professional Conduct (ET).** The US analogue to IESBA — principles and rules for members in public practice and in business. The Independence Rule (ET §1.200) and related interpretations govern AT-C work.
- **ISO/IEC 17021-1 clause 5.2 Impartiality** (plus Annex H guidance on time-limited impartiality constraints). Applies to management-system certification bodies and their auditors.
- **ISACA Code of Professional Ethics.** Applies to CISA / AAIA holders; integrates with the IT-audit workflow.
- **ForHumanity, BABL AI, and scheme-specific codes.** Apply to practitioners auditing under those schemes; typically layer on top of one of the four above.

If an engagement touches more than one framework, your posture statement cites each applicable one and how the firm's / function's / individual's independence satisfies all of them. In mixed engagements the operating rule is the most restrictive.

## The five threats to independence (shared vocabulary)

The IFAC / IESBA framework names five threats to objectivity and independence. Every other code uses variants of the same list; memorise the IFAC naming and translate as needed:

1. **Self-interest threat** — financial or other interest inappropriately influencing judgment or behaviour (e.g., contingent-fee arrangements, significant client revenue dependence, equity or compensation tied to engagement outcomes).
2. **Self-review threat** — auditor evaluates results of a previous judgment they (or their firm) made (e.g., auditor previously consulted on the AI governance design now being audited; auditor previously performed the eval suite now relied on as evidence).
3. **Advocacy threat** — auditor promotes a client's position to the point that objectivity is compromised (e.g., auditor publicly defends the client's model against regulator inquiry while running the attestation engagement).
4. **Familiarity threat** — long association with the client creates sympathy or close identification (e.g., the same lead auditor recurs on the same AIMS certification engagement year after year; the engagement partner has a spouse in the client's ML team).
5. **Intimidation threat** — actual or perceived pressure from the client inhibiting the auditor's judgment (e.g., threatened replacement of the auditor, aggressive legal posture, significant-client economic dependence).

## AI-specific fact patterns that trigger each threat

The five threats are not abstractions in AI work. Each has a predictable AI pattern:

- **Self-review via prior consulting.** The AI auditor, a colleague in the same firm office, or an auditor's expert previously co-authored the organisation's AI policy, AIMS risk-assessment procedure, red-team playbook, or eval harness. Any audit that would opine on the design or operating effectiveness of that artifact carries a self-review threat. The ISO/IEC 17021-1 two-year CB cooling-off rule and the AICPA / IESBA prohibitions on structuring or operating a client's accounting records are the operational equivalent.
- **Self-review via eval-tooling overlap.** The auditor's firm maintains an open-source or commercial eval harness the client uses; or the auditor's expert previously authored the garak / PyRIT / Inspect configuration now in production at the client. The eval tooling's provenance has to be documented and the threat evaluated.
- **Self-interest via retainer fees.** The AI auditor is engaged on a multi-year retainer to deliver ongoing AI-risk advisory alongside the audit engagement. Fees on the advisory side exceed the audit-engagement fee; the auditor's economic dependence on the retainer makes the audit finding commercially costly to issue. The AICPA independence rules on non-audit services and IESBA independence standards both constrain this.
- **Familiarity via repeated engagements.** The same lead auditor recurs on the client's ISO/IEC 42001 certification audit through three-year cycles; relationships with first-line engineers deepen. ISO/IEC 17021-1 anticipates auditor rotation; firm policies and IESBA standards layer on top.
- **Intimidation on big-client engagements.** The AI engagement is on a frontier model lab with significant market power; the engagement partner fears losing the account if the opinion is adverse. The firm's engagement-quality review and the regulator's inspection rights are the structural counterweights.
- **Advocacy threat on regulator-facing work.** The AI auditor's firm is also advising the client on EU AI Office engagement. The firm promotes the client's position in regulator correspondence while also issuing an ISAE 3000 report the regulator will read. The firm's independence policy will restrict this; the engagement letter must disclose.

## Safeguards — what you actually put in place

Safeguards must be **effective** (actually reduce the threat to an acceptable level) and **documented** (so the review can verify the operation of the safeguard). Standard safeguards, mapped to threats:

- **Firm-level** — engagement acceptance screening against a conflicts database, independence policy incorporating IESBA / AICPA / IIA / ISO 17021-1 constraints, firm-wide quality-management system (ISQM 1 / QM 1), impartiality committee at a CB, rotation policy, prohibition on contingent-fee work for audit clients.
- **Engagement-level** — written independence confirmation from every engagement team member and every auditor's expert at acceptance; engagement-quality review by an independent partner on reasonable-assurance engagements; separation of advisory and assurance teams; ring-fencing of client information between teams; cooling-off periods on rotation; disclosure to those charged with governance (audit committee, CB impartiality committee, regulator).
- **Individual-level** — personal declarations from each auditor (no prior employment, no close family in client ML teams, no personal financial interest, no pending offer of employment from the client); professional-skepticism training current; CPD current; no personal advocacy on the client's behalf.
- **AI-specific additions** — provenance declaration for eval tooling used by the auditor and by the client, disclosure of any training-data provenance that includes the auditor's own prior work, written representation that the auditor's expert is not the author of any artifact in scope of the engagement.

## The professional-skepticism test

Professional skepticism is the IAASB / AICPA / IIA concept of "an attitude that includes a questioning mind, being alert to conditions which may indicate possible misstatement due to error or fraud, and a critical assessment of audit evidence". In AI engagements, four operating cues:

1. **Treat management's own eval metrics as management assertions, not as evidence.** Metrics in a model card are *what management claims*. Evidence is what you (or an auditor's expert under your supervision) independently obtains or re-performs. The professional-skepticism test is: can you separate the claim from the evidence that supports or does not support it?
2. **Interrogate convenient explanations.** The team claims a drop in a fairness metric is due to a "data distribution shift" that resolves itself. The skepticism test: ask for the quantitative evidence, the regression fixture, the monitoring record of the shift resolving. Accept nothing on narrative.
3. **Favour corroboration from independent sources.** A single interview with the model team is weaker evidence than interview + documentation + log inspection + re-performance. Where the AI engagement scope permits it, insist on corroboration.
4. **Document the skepticism trail.** Skepticism without workpaper evidence is not visible to review. Record where you probed, what you asked, what you accepted, what you did not accept, and why. This is what survives external QA inspection.

## The posture statement — content and shape

Every AI engagement opens with a documented **independence-and-ethics posture statement** authored by the engagement lead and signed by every team member and expert. Suggested skeleton (customise to the engagement's governing framework):

```
INDEPENDENCE AND ETHICS POSTURE — [ENGAGEMENT NAME], [DATE]

1. Engagement framework and governing ethics codes
   - Framework(s): [IIA 2024 Standards | ISAE 3000 | AT-C 105 + AT-C 205 | ISO/IEC 17021-1 + 42006 | NYC LL144 scheme | ...]
   - Ethics code(s): [IESBA / AICPA / IIA / ISACA / ISO 17021-1 cl. 5.2 / scheme-specific]
   - Most-restrictive overlay applied where codes conflict

2. Threats identified
   For each of the five threats (self-interest, self-review, advocacy, familiarity, intimidation),
   list AI-specific fact patterns identified at this engagement
   (prior consulting, eval tooling provenance, retainer relationship, repeated engagement,
   client market power, regulator-facing advocacy work)

3. Safeguards applied
   Firm-level, engagement-level, individual-level, AI-specific — each threat addressed

4. Residual threats accepted and basis
   Where a threat remains above a trivial level, the basis for acceptance and the
   disclosure made to those charged with governance

5. Professional-skepticism commitment
   Operating cues the engagement team will follow; documentation discipline

6. Signatures
   Engagement lead, engagement partner / CAE, each team member, each auditor's expert
```

Keep this in the workpaper file at Section A (planning). External QA, firm inspection, accreditation-body surveillance, and in extreme cases regulator inquiry will ask for it; the absence of a signed posture statement by itself is a finding.

## Worked micro-examples

### A — Prior consulting, bank internal AI audit

Fact pattern: an internal auditor spent 2022 helping the bank's second-line MRM function draft the AI risk-assessment procedure. In 2026 the same auditor is proposed as engagement lead for the internal audit of operating effectiveness of that procedure. Analysis:

- **Threat**: self-review (strong).
- **Safeguards possible**: reassign engagement lead to a different internal audit colleague; cooling-off period on the auditor's involvement with the specific procedure; limit the auditor to adjacent scope (e.g., AI monitoring) where prior design involvement is not present.
- **Acceptable outcome**: auditor is reassigned. Posture statement records the reassignment and the basis.
- **Unacceptable outcome**: auditor remains as lead with no safeguard — the audit opinion on the procedure's design would be audit of one's own work.

### B — Retainer relationship, external attestation

Fact pattern: a Big-4 firm has a $4M annual AI advisory retainer with a client and is engaged to issue a $500K AT-C 205 examination report on the client's AI safety program. Analysis:

- **Threats**: self-interest (retainer dependence), self-review (if the advisory team's deliverables are inputs to the attestation subject matter).
- **Safeguards**: strict separation of advisory and attestation teams (different partners, different working teams, information barriers); confirmation that the attestation subject matter is not the advisory deliverable itself; engagement-quality review by an independent partner; disclosure to the audit committee.
- **Acceptable outcome**: separation effective and documented; EQR partner signs off; posture statement records the arrangement.
- **Unacceptable outcome**: advisory team's work product is the subject matter — treat as self-review threat unresolvable; decline the engagement or move the subject matter.

### C — Repeated certification engagement at a certification body

Fact pattern: the same lead auditor has executed the client's ISO/IEC 42001 certification audit each year for the 3-year cycle and is proposed for recertification. Analysis:

- **Threat**: familiarity.
- **Safeguards**: auditor-rotation policy per ISO/IEC 17021-1 Annex H; new lead auditor for the recertification; prior lead auditor stays on team for continuity but not in the lead role.
- **Acceptable outcome**: rotation per policy; posture statement records the rotation.

### D — Frontier-safety advocacy, large-model engagement

Fact pattern: an AI audit firm regularly participates in public policy advocacy on frontier AI safety alongside the client (same policy position, co-signed letters). The firm is engaged on an ISAE 3000 report on the client's safety program. Analysis:

- **Threat**: advocacy (strong).
- **Safeguards**: separation of the policy-advocacy practice from the attestation team; prohibition on firm-level public advocacy during the engagement period; disclosure to users of the attestation report.
- **Acceptable outcome**: policy practice is severable; engagement team has no overlap; posture statement records the separation.
- **Unacceptable outcome**: advocacy is at engagement-team level and inseverable — decline the engagement.

## Where chapter 8 lives in the engagement file

Everything in this chapter instantiates as **a signed artifact in the workpaper file**. The chapter's chapters 1-7 install the *what* and the *why*; the posture statement is the *how* — the documented commitment, named by engagement, signed by team, available to review. A level-45 AI Auditor authors these quickly and defensibly because the model is internalised; they do not improvise the posture mid-engagement.

## Summary

- Multiple ethics codes apply simultaneously — **IIA, IESBA, AICPA, ISO/IEC 17021-1, ISACA, scheme-specific**. In conflict, apply the most-restrictive overlay.
- The **five threats** (self-interest, self-review, advocacy, familiarity, intimidation) have predictable AI-specific fact patterns; evaluate each at engagement acceptance and when facts change.
- **Safeguards** operate at firm, engagement, individual, and AI-specific levels; they must be effective and documented.
- **Professional skepticism** operates on four cues in AI work: metrics-as-claims, convenient-explanations, corroboration, documentation.
- Every engagement opens with a **signed independence-and-ethics posture statement** in the workpaper file.
