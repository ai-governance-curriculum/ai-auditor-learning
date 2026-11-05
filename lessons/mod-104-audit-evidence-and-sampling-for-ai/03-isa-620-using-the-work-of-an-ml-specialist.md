# ISA 620 / AU-C 620 — Using the Work of an ML/AI Specialist on the Engagement

## Motivation

An AI audit almost always needs expertise the lead auditor does not carry alone. The question is not *whether* a specialist is on the engagement — it is whether the specialist's work can bear the auditor's conclusion. **ISA 620 — Using the Work of an Auditor's Expert** (IAASB) and **AU-C 620 — Using the Work of an Auditor's Specialist** (AICPA) govern that reliance: how to assess the specialist's competence, capability, and objectivity; how to agree scope, deliverables, and confidentiality; how to evaluate the specialist's output; and how to retain sole responsibility for the audit conclusion. The ISA uses "auditor's expert" and AU-C uses "auditor's specialist"; the substance is the same, and this chapter uses "specialist" throughout.

The chapter also installs the two neighbour standards the AI Auditor confuses with ISA 620 in the field and must not: **ISA 610 (Revised) — Using the Work of Internal Auditors** (reliance on the organisation's internal audit function, not the specialist you hired) and the concept of **management's expert** under ISA 500 paragraphs 8 and A34–A48 (the organisation's own ML specialist whose work the auditor evaluates as evidence, not relies on as an auditor's expert). The three regimes have different rulebooks; applying the wrong one voids the reliance.

## The three regimes the AI Auditor must distinguish

| Regime | Standard | Who is the person | What the auditor is doing |
|---|---|---|---|
| **Auditor's specialist** | ISA 620 / AU-C 620 | Someone engaged by the firm (or the internal audit function) to assist on this engagement — can be *external* (contractor, specialist firm) or *internal* (a specialist in the firm's AI practice) | Using their work as part of the firm's own evidence |
| **Management's expert** | ISA 500 §8, A34–A48 | Someone the audited organisation engaged to produce a deliverable the audit is examining (e.g., a third-party eval report commissioned by the model owner) | Evaluating their work as *evidence from the entity*; reliability driven by the ISA 500 generalisations and ISA 500 paragraph 8 tests |
| **Internal audit function reliance** | ISA 610 (Revised) / AU-C 610 | The organisation's own internal auditors (another function at the audited entity) | Using their procedures as audit evidence after assessing competence, objectivity, and the function's QA programme |

Applying ISA 620 to a management-engaged specialist is a category error — the auditor is not engaging that person, and the appropriate posture is ISA 500 evaluation of the specialist's output as entity evidence. Applying ISA 500 to an auditor-engaged specialist short-circuits the independence and scope-of-work requirements of ISA 620.

## ISA 620's structural requirements, restated

ISA 620 paragraphs 7–13 (AU-C 620 paragraphs 7–13 mirror) require:

1. **Scope determination** — whether to use a specialist, based on the engagement's nature, complexity, risks of material misstatement, and the required competence.
2. **Competence, capability, and objectivity assessment** — before relying on the specialist's work.
3. **Agreement with the specialist** — nature, scope, objectives of the specialist's work; roles and responsibilities of the auditor and the specialist; nature, timing, and extent of communication; confidentiality requirements. In writing, for engagements where the matter is significant.
4. **Understanding of the specialist's field** — enough to evaluate the adequacy of their work for the auditor's purposes.
5. **Evaluation of the specialist's work** — relevance and reasonableness of findings; consistency with other audit evidence; if the work involves use of significant source data, assumptions, and methods, the relevance and reasonableness of those.
6. **Sole responsibility for the audit opinion** — no division of responsibility in the report. ISA 620 paragraph 14 forbids reference to the specialist in an unmodified auditor's report; AU-C 620 paragraph 15 allows reference only in certain circumstances. The engagement letter and audit report language need to be reviewed against the applicable standard.

## Competence, capability, and objectivity — the AI assessment

ISA 620 paragraph 9 names the three attributes. For an ML / AI specialist:

### Competence

- **Technical grounding** — formal training, publications, industry experience in the specific AI domain the engagement covers. ML engineer vs. applied data scientist vs. ML safety researcher vs. AI risk engineer are not interchangeable.
- **Modality match** — the specialist's experience should match the audit subject matter. A classical-ML specialist is not automatically a generative-AI specialist; an LLM-application specialist is not automatically a foundation-model training specialist; an explainability specialist is not automatically a fairness specialist.
- **Audit-adjacent experience** — the specialist does not need to be an auditor, but experience under evidence-grade constraints (regulatory submission, model-risk validation under SR 11-7, FDA SaMD submission, EU AI Act technical documentation) materially upgrades the specialist's usability in audit.
- **Credentials** — formal credentials corroborate but do not replace track record. The AICPA's **Information Technology Certificate**, **AWS / Azure / Google ML certifications**, academic degrees, and vendor-neutral credentials from CNCF, LF AI & Data, or ISTQB-AI add to the dossier.

The competence assessment is documented in the engagement file: CV, selected prior work, references, credential list, and an explicit statement by the lead auditor of why this specialist is competent for *this* engagement.

### Capability

- **Capacity** — does the specialist have the time to complete the agreed work within the engagement timeline?
- **Infrastructure** — does the specialist have access to the compute, tools, and environments needed? An LLM-eval specialist without access to a GPU runtime or a trace-store query console cannot execute the planned procedures.
- **Clearance** — can the specialist clear the organisation's security review and data-access vetting in the engagement window?

Capability is not a one-time check; it is re-tested when scope changes.

### Objectivity

- **No current engagement with the audited party** on the matter being audited. An ML consultant who helped build the system cannot be the ISA 620 specialist on its audit.
- **No recent engagement within the firm-independence cooling-off window**. Firm-independence rules (ISQM 1 / IESBA code / AICPA ET rule applicable) govern.
- **Financial independence** — no material financial interest in the audited party; no contingent-fee arrangement on the audit outcome.
- **AI-specific threats** — the specialist's publishing record or public advocacy should not create an advocacy threat on the controversial areas of the engagement (e.g., a specialist who has publicly advocated against a particular eval benchmark cannot be the specialist opining on that benchmark's results).

Objectivity is documented alongside competence; the specialist signs an independence confirmation at engagement acceptance and refreshes it at significant scope changes.

## Scope-of-work agreement — the ISA 620 §11 document

ISA 620 paragraph 11 requires an agreement with the specialist. For significant matters, in writing. A workable AI-specialist scope letter contains:

- **Engagement identification** — audit client, period, subject matter, lead auditor.
- **Objectives of the specialist's work** — the specific audit assertions the specialist is helping test, quoted from the engagement plan.
- **Scope** — what the specialist will do (procedures, artifacts inspected, re-runs performed, samples drawn), and explicitly what the specialist will *not* do (opine on management's control design; author management's fix; opine on the audit conclusion).
- **Methodology** — the techniques the specialist will apply (e.g., independent re-run with pinned seed; disparate-impact estimation on auditor-selected cohort; red-team catalog execution).
- **Source data** — what data the specialist will use, where it comes from, how it is validated.
- **Assumptions** — the specialist's working assumptions, named and reviewable.
- **Deliverables** — the shape of the specialist's output (memo, re-run artifact, workpaper, data summary); the required workpaper fields; the signed assertion from the specialist.
- **Roles and responsibilities** — who is the lead auditor; who is the specialist; who reviews whose work; who signs the final audit report (the firm, not the specialist).
- **Communication** — cadence, format, escalation.
- **Confidentiality and data handling** — NDAs, data-residency, data-destruction post-engagement, log retention.
- **Fees and term** — contract shape.
- **Conflicts and independence** — the signed independence confirmation and the process for re-affirming at scope changes.
- **Limitations** — what the specialist cannot opine on and the implications for the audit.

The scope letter is an engagement artifact and lives in the workpaper file.

## In-team ML specialist vs. external contractor — the decision

A firm with an internal AI-assurance practice can staff ISA 620 specialists in-team; the alternative is engaging an external contractor or specialist firm. The decision drivers:

- **Independence** — an in-team specialist is subject to firm-wide independence rules automatically; an external contractor must be onboarded to those rules and the paperwork is heavier.
- **Depth of domain match** — the in-team specialist may be a generalist; the external contractor may be a deep specialist (e.g., a biometric-ML specialist for an FDA SaMD biometric authentication system). Pick for depth where the engagement needs it.
- **Capacity** — in-team specialists are constrained by firm staffing; external capacity can scale.
- **Repeatability** — in-team specialists accumulate audit-adjacent knowledge across engagements; external contractors re-learn the engagement each time.
- **Cost** — in-team specialists carry firm overhead; external contractors carry contract margins. Simple magnitudes do not pick a winner; engagement budget and risk do.
- **Objectivity on this organisation** — if the in-team specialist has a prior relationship with the audited party (built a model for them, consulted on their AIMS), that specialist is out and the engagement goes external.

A defensible pattern: **in-team specialist as default; external contractor when in-team depth is insufficient, in-team capacity is unavailable, or in-team independence is compromised on this organisation.**

## Interpreting the specialist's output into audit conclusions

ISA 620 paragraph 12 requires the auditor to evaluate the adequacy of the specialist's work for the auditor's purposes. For AI specialists, that evaluation has four load-bearing steps:

1. **Relevance to the assertion** — the specialist tested what the engagement needed tested. Example: the engagement needs evidence on fairness over a protected class under the Colorado AI Act; the specialist's re-run must be on the protected-class cohort, with a cohort definition consistent with the Act's text. A re-run on an unrelated cohort is work, but not evidence for this assertion.
2. **Reasonableness of assumptions and methods** — the specialist's approach is defensible. Example: a cohort fairness measurement using a 95% bootstrap confidence interval is a reasonable method; a point estimate without variance is not. The lead auditor need not be able to execute the method, but must be able to defend that it is reasonable.
3. **Reasonableness and completeness of source data** — the specialist's inputs are the inputs the auditor intended. Example: the specialist used the auditor-pinned model artifact hash, the auditor-pinned dataset hash, and the auditor-authored query to produce the cohort. If the specialist pulled a different dataset or different model, the work is out of scope and must be repeated on the correct inputs.
4. **Internal consistency and consistency with other audit evidence** — the specialist's findings do not contradict other evidence without explanation. Example: the specialist reports a fairness gap of 0.2, management's monitoring dashboard shows 0.05, and the system vendor's attestation shows 0.08. The three should be reconciled; the specialist's work is accepted only after the reconciliation.

The lead auditor's workpaper carries the evaluation of each of these four. The specialist's report is an attachment to the audit workpaper, not a substitute for the audit workpaper.

## The understanding-the-specialist's-field test — ISA 620 §11a

ISA 620 paragraph 11(a) requires the auditor to have "sufficient understanding of the field of expertise of the auditor's expert to enable the auditor to determine the nature, scope and objectives of that expert's work for the auditor's purposes" and "to evaluate the adequacy of that work for the auditor's purposes".

For AI engagements, "sufficient understanding" does not require the lead auditor to be an ML specialist. It does require:

- **Conceptual fluency** — the lead auditor can state the eval method, the metric, the assumptions, and the known limitations in their own words.
- **Interrogation capacity** — the lead auditor can ask the specialist the questions that would catch an incorrect method or an incorrect dataset without being an ML expert themselves.
- **Decision authority** — the lead auditor can decide whether the specialist's work addresses the audit assertion, and whether a scope change is warranted.

The portfolio of chapters in `mod-103`, `mod-104`, `mod-106`, `mod-107` and the peer chapters at `model-evaluation-engineer` (level 30) and `ai-eval-engineer` (level 30) build this fluency — the AI Auditor is not an ML engineer, but is not a layperson, either.

## When the specialist disagrees with management

The ISA 620 specialist's work can produce findings that contradict management's representations. The ISA 620 paragraph 13 posture is to resolve the contradiction before concluding — additional procedures, additional evidence, reconciliation meetings with management, further specialist work. If resolution is not possible, the audit opinion is modified (qualified, adverse, or disclaimer) to reflect the unresolved contradiction.

A specialist disagreement that is quietly resolved by scope reduction, or by accepting management's reconciliation without independent verification, is a professional-skepticism failure the engagement-quality reviewer will catch.

## Common failure modes

- **Specialist treated as co-author of the opinion.** The report wording suggests divided responsibility. ISA 620 paragraph 14 forbids this in unmodified reports.
- **Scope letter missing or informal.** No written agreement on what the specialist will do; the specialist's work drifts; the engagement cannot defend relevance at review.
- **Competence assessment on credentials only.** Credentials without track record on the specific modality are necessary but not sufficient.
- **Objectivity assumed from firm employment.** An in-team specialist who worked with this client in the prior year on a first-line assignment is not objective for this engagement, regardless of firm.
- **Lead auditor abdicates the ISA 620 §11a understanding.** "I don't know ML, so I'll trust the specialist." Failing the understanding test fails the engagement.
- **ISA 620 applied to a management-engaged specialist.** Treating a management-commissioned third-party eval report as an ISA 620 deliverable rather than as entity evidence to be evaluated under ISA 500.
- **ISA 500 applied to an auditor-engaged specialist.** Treating the firm's own contracted specialist's work as entity evidence; the specialist is part of the audit team and the audit retains sole responsibility.
- **Reconciliation gap unresolved.** The specialist's number differs from management's; the delta is not investigated; the audit silently adopts one or the other. Every delta is a workpaper line.

## Summary

- ISA 620 / AU-C 620 govern the auditor's use of a specialist's work; ISA 610 governs reliance on the internal audit function; ISA 500 §8 governs evaluation of a management-engaged expert's output as entity evidence. The three regimes are not interchangeable.
- For AI audits, the specialist must be *competent* on the specific modality, *capable* in capacity and infrastructure, and *objective* under firm, IESBA, AICPA, and AI-specific threat tests. Document the assessment.
- The scope-of-work agreement (ISA 620 §11) names objectives, scope, methodology, source data, assumptions, deliverables, roles, communications, confidentiality, and limitations. In writing. In the engagement file.
- In-team specialist is the default; external contractor is right when depth, capacity, or client-specific objectivity make in-team unworkable.
- The auditor evaluates the specialist's work on relevance, method reasonableness, source-data correctness, and consistency with other evidence. The auditor retains sole responsibility for the opinion.
- The lead auditor must satisfy the ISA 620 §11a understanding test — conceptual fluency, interrogation capacity, decision authority — without being an ML specialist.
- Chapter 4 continues the evidence discipline into the AI-specific evidence inventory and reliability grading; chapter 6 shows how the specialist's re-run plugs into a reproducibility bundle.
