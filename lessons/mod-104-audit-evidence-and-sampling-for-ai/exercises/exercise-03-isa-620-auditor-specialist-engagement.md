# exercise-03: ISA 620 Auditor Specialist Engagement

**Estimated effort:** 2 hours

## Objective

Decide whether an ML / AI specialist is needed on a given engagement, pick in-team vs. external, run the ISA 620 competence / capability / objectivity assessment on three candidates, and author the written scope-of-work agreement and the specialist-deliverable evaluation plan. Produce the artifacts the engagement file would carry under ISA 620 / AU-C 620.

## Prerequisites

- Chapter [`03-isa-620-using-the-work-of-an-ml-specialist.md`](../03-isa-620-using-the-work-of-an-ml-specialist.md)
- Chapter [`01-isa-500-evidence-applied-to-ai-artifacts.md`](../01-isa-500-evidence-applied-to-ai-artifacts.md) — to distinguish auditor's specialist (ISA 620) from management's expert (ISA 500 §8)
- `mod-101` chapter 8 (independence and ethics posture)

## Scenario

The engagement is an AT-C 205 examination of **Aster Credit Union's** consumer-loan recommendation model, scoped for the audit period 2026-01-01 to 2026-12-31. The firm issuing the opinion is a mid-tier assurance practice. The engagement opinion will cover two primary assertions:

1. The recommendation model's **group-fairness metrics** (approval rate disparity by self-reported protected class, false-approval rate disparity, and false-denial rate disparity) were within the organisation's published tolerance thresholds across the audit period.
2. The **LLM-as-judge** evaluator the organisation uses to score model explanations for "clarity to consumer" is calibrated against a human-reviewer panel at ≥ 0.80 agreement in the audit period.

The lead auditor (you) holds the CIA and the AAIA, has nine years of audit experience including two years on ML-adjacent engagements, but is not an ML specialist.

Three candidate specialists are available:

### Candidate A — Internal firm specialist

- Dr. Rina Oyelaran, a senior data scientist in the firm's AI-assurance practice. PhD in applied statistics; 6 years industry experience; 3 years at the firm. Independent of this client. Has led fairness-metric calibration on two prior engagements. Available for the full engagement period at 40% capacity. Carries the firm's independence log automatically.

### Candidate B — External contractor

- Ms. Jian Mao, principal of an independent ML-audit consultancy. 11 years industry experience including LLM evaluation calibration published in two peer-reviewed venues. Previously consulted for Aster Credit Union *on a separate loan-servicing analytics project* that concluded 2025-07. No ongoing financial relationship. Available at 60% capacity. Would need to be onboarded to the firm's independence process.

### Candidate C — External specialist firm

- SilverDigit AI Assurance LLC, a specialist firm offering ML-eval and fairness-audit capacity. Project-matched staff would be an engagement partner with a statistics PhD and two senior associates with applied ML experience. No prior relationship with Aster Credit Union. Firm-level independence confirmation available. Available at project-based engagement with a defined deliverable scope. Cost estimate 3× the other two candidates.

Management has handed the engagement team a **third-party eval report** authored by SilverDigit AI Assurance LLC in 2026-Q2, commissioned by Aster Credit Union directly, covering the fairness metrics of the recommendation model during 2025-Q4. This creates an obvious question about Candidate C's role.

## Requirements

1. **Scope decision.** State whether this engagement requires an ISA 620 specialist, naming the audit assertions that drive the need. Cite ISA 620 paragraph(s). If parts of the engagement can be executed without a specialist, name them.
2. **Candidate selection memo.** For each of the three candidates, run the competence / capability / objectivity assessment per chapter 3. One short paragraph per attribute per candidate; call out specific red flags.
3. **Independence / self-review resolution.** Address Candidate B's prior Aster engagement (does the 2025-07 conclusion date and the different scope resolve the threat, and under what cooling-off rule?). Address Candidate C's prior report commissioned by management (why cannot Candidate C simultaneously be the engagement's ISA 620 specialist on the same subject matter, and what posture would the engagement take instead?). Cite IESBA / AICPA ET independence rules by concept; `<!-- needs-research -->` for exact paragraph numbers if you need to verify.
4. **Final candidate pick and alternative-posture decision.** Pick the specialist for the engagement and name why. For the non-picked candidates, state the alternative posture (e.g., Candidate C's prior report treated under ISA 500 §8 as management's expert evidence rather than under ISA 620).
5. **Scope-of-work agreement letter.** Author the written agreement with the picked specialist per chapter 3 §Scope-of-work agreement. Cover the thirteen items listed there. 1–2 pages, professional tone. Date the letter.
6. **Specialist-deliverable evaluation plan.** Author the plan the lead auditor will use to evaluate the specialist's deliverables under ISA 620 §12: relevance to assertion, reasonableness of method and assumptions, source-data correctness, consistency with other evidence. Name the specific artifacts the lead auditor will inspect and the specific tests of consistency the lead auditor will run against other engagement evidence.
7. **Management-expert evaluation plan.** Author the separate plan for evaluating the SilverDigit-authored 2026-Q2 report *as management's expert evidence under ISA 500 §8*, naming the ISA 500 §A34–A48 competence/capability/objectivity assessment of the expert (performed as a reliability check on the entity evidence, not as an ISA 620 specialist engagement).

## Starter guidance

- The lead auditor's AAIA and nine years of experience satisfy the ISA 620 §11a understanding test for most of the engagement — but LLM-as-judge calibration is a specialist area where the lead auditor is in a position to interrogate the specialist, not to replace them.
- Candidate B's prior engagement for Aster is the classic cooling-off question. Most firms apply a one- or two-year cooling-off window for non-audit services that could create self-review threats; the exact rule differs by firm and jurisdiction. State the principle; do not invent a specific firm policy.
- Candidate C's prior report creates a self-review threat if Candidate C now audits its own earlier work. The 2026-Q2 report is a management-commissioned deliverable; it is entity evidence under ISA 500 §8, not an ISA 620 deliverable.
- The written scope-of-work agreement is a load-bearing document; the acceptance criteria below name its minimum content.
- The deliverable-evaluation plan should include reconciliation to the trace-store queries the engagement authors independently (chapter 6 reproducibility bundle).
- Use `<!-- needs-research -->` for specific IESBA / AICPA ET rule numbers if you need to verify them at engagement time.

## Acceptance criteria

The deliverable is accepted when:

- The scope decision names the specific assertions that require a specialist and cites ISA 620 explicitly.
- Each of the three candidates has a competence / capability / objectivity assessment with specific red flags identified.
- The independence resolution for Candidate B names the cooling-off principle and the engagement's handling (accept with safeguards, accept without, or reject).
- The independence resolution for Candidate C names the self-review threat and routes the prior report to ISA 500 §8 treatment.
- The picked candidate is named with reason; alternative-posture decisions for the non-picked are explicit.
- The scope-of-work agreement covers: engagement identification; objectives; scope; methodology; source data; assumptions; deliverables; roles; communications; confidentiality; fees/term; conflicts/independence; limitations. Missing any three is a failed acceptance.
- The specialist-deliverable evaluation plan names: relevance, method reasonableness, source-data correctness, and consistency-with-other-evidence tests — with specific artifacts and specific tests.
- The management-expert evaluation plan treats the 2026-Q2 report under ISA 500 §8 (not ISA 620) and names the competence/capability/objectivity reliability checks as entity-evidence reliability.
- `<!-- needs-research -->` placeholders are used rather than invented rule numbers.
- No fabricated independence policies or rule numbers.

## Stretch goals

- Draft the **three-month status-update cadence** the engagement would use with the picked specialist — agenda template, deliverable interim checks, escalation path.
- Write a **reconciliation workpaper** for the case where the specialist's independent re-run of the fairness metrics differs from the SilverDigit 2026-Q2 report's metrics by more than the engagement's tolerable difference — what happens next in the ISA 620 §12 evaluation?
- Author the **report-wording review note** that the engagement partner would make on the specialist's draft deliverable — specifically checking for any language that would create division-of-responsibility problems under ISA 620 §14.
- Propose the **companion-repo layout** (chapter 5) for the specialist's work (`specialist/<specialist-id>/`): scope-of-work, deliverables, evaluation memos.
