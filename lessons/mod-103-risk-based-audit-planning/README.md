# mod-103-risk-based-audit-planning: Risk-Based Audit Planning for AI Systems and AI Management Systems

**Estimated effort:** 14 hours

This module teaches the AI Auditor how to move from "an engagement was dropped on my desk" to "the audit committee approved a risk-based plan that defends why this engagement is here, with this scope, at this materiality, in this period, with this team". It is the discipline that connects the inventory kept by the `ai-governance-analyst` (level 15), the inherent-risk scoring kept by the `ai-risk-engineer` (level 25), and the control library designed by the `senior-ai-governance-architect` (level 50) into *your* annual plan, your scoped engagements, and your audit-committee communication. Everything in `mod-104` through `mod-112` and the three projects assumes you can produce and defend these planning artifacts in writing.

## Learning objectives

- Construct an AI audit universe from an enterprise AI inventory (consuming the AI-system intake and inventory the `ai-governance-analyst` (level 15) maintains) — covering internal AI systems, deployed AI systems, third-party AI procurement, embedded AI inside non-AI vendors, and GPAI model usage.
- Score audit priority on the universe using an inherent-risk + residual-risk assessment that reuses the `ai-risk-engineer` (level 25) scoring shape layered with audit-specific drivers (prior findings, management-response history, external-auditor coverage, regulator attention, change velocity) — producing a defensible annual audit plan the audit committee can approve.
- Apply ISA 320 / AU-C 320 materiality concepts to AI audit scope — quantitative materiality (financial impact, affected population size, decision volume), qualitative materiality (regulatory classification as high-risk, systemic-risk, safety-critical), performance materiality, and tolerable misstatement; tune materiality for ISO/IEC 42001 certification audit vs. EU AI Act conformity assessment vs. SOC-for-AI attestation vs. internal risk-based audit.
- Scope a single AI-system audit engagement — purpose, criteria, boundaries, period of coverage, population, sampling approach, inherent limitations, deliverable shape.
- Scope an AIMS audit engagement against ISO/IEC 42001 — Stage-1 documentation review, Stage-2 implementation audit, surveillance audit cycle, recertification — in the ISO/IEC 17021-1 / 42006 shape; scope a non-certification internal-audit variant that reuses the same clause map.
- Author the engagement plan — team composition (lead auditor, technical specialists, independent reviewer), timing, logistics, information-request list, interview schedule, evidence-request shape, escalation path, kickoff / closing meeting shape.
- Coordinate with the audit committee and the Chief Audit Executive on the plan — reporting cadence, communication protocol, change management on the plan, external-auditor coordination; defer enterprise audit-function leadership *up* to the CAE and audit-committee chair.

## Chapters

1. [`01-the-ai-audit-universe.md`](01-the-ai-audit-universe.md) — construct the AI audit universe from the analyst inventory and adjacent discovery sources; five populations; schema and discovery cycle.
2. [`02-audit-priority-scoring-and-annual-plan.md`](02-audit-priority-scoring-and-annual-plan.md) — the eight-term priority equation, weighting schemes, capacity, and the shape of the annual plan.
3. [`03-materiality-for-ai-audit.md`](03-materiality-for-ai-audit.md) — ISA 320 / AU-C 320 overall, performance, and specific materiality for AI; tuning by engagement type.
4. [`04-scoping-a-single-ai-system-engagement.md`](04-scoping-a-single-ai-system-engagement.md) — the seven scope elements of a single-system engagement under ISAE 3000 / AT-C 205 / IIA Standards.
5. [`05-scoping-an-aims-audit.md`](05-scoping-an-aims-audit.md) — Stage-1, Stage-2, surveillance, and recertification under ISO/IEC 17021-1 + 42006; the internal-audit variant under clause 9.2.
6. [`06-engagement-plan-authoring.md`](06-engagement-plan-authoring.md) — team composition, timing, logistics, IRL, interview schedule, evidence shape, escalation path, kickoff and closing meeting shape.
7. [`07-audit-committee-and-cae-coordination.md`](07-audit-committee-and-cae-coordination.md) — what goes up to the CAE and audit committee, when, in what shape; change management on the plan; external-auditor coordination; the deferring-up discipline.

## Exercises

- [`exercise-01-ai-audit-universe-from-ai-inventory.md`](exercises/exercise-01-ai-audit-universe-from-ai-inventory.md) — construct a universe from a provided inventory plus discovery sources; produce the universe-change log and discovery-methodology memo.
- [`exercise-02-audit-priority-scoring-and-annual-plan.md`](exercises/exercise-02-audit-priority-scoring-and-annual-plan.md) — score the universe, pick a weighting scheme, author the plan, and write the CAE audit-committee cover memo for the AI-audit section.
- [`exercise-03-materiality-tuning-drill-by-engagement-type.md`](exercises/exercise-03-materiality-tuning-drill-by-engagement-type.md) — four materiality workpapers for the same system across ISO/IEC 42001 certification, EU AI Act conformity assessment, SOC-for-AI attestation, and internal risk-based audit.
- [`exercise-04-ai-system-engagement-scope-authoring.md`](exercises/exercise-04-ai-system-engagement-scope-authoring.md) — scope memo and engagement letter for an AT-C 205 examination of a career-navigation AI, with scope-dispute and scope-change memos.
- [`exercise-05-iso-42001-stage-1-and-stage-2-plan-authoring.md`](exercises/exercise-05-iso-42001-stage-1-and-stage-2-plan-authoring.md) — Stage-1 and Stage-2 plans for an AIMS certification engagement plus the parallel internal-audit variant.
- [`exercise-06-engagement-plan-with-team-and-timing.md`](exercises/exercise-06-engagement-plan-with-team-and-timing.md) — complete engagement plan for a chosen engagement, with quarterly audit-committee briefing input and an event-driven escalation memo.

## Role boundary (reminder)

- The `ai-governance-analyst` (level 15) maintains the **AI inventory** the audit universe draws from. The AI Auditor is a buyer; if the inventory is wrong, that is a finding.
- The `ai-risk-engineer` (level 25) maintains the **inherent-risk scoring shape** the audit priority equation reuses. The AI Auditor does not re-invent the risk model during planning.
- The `senior-ai-governance-architect` (level 50) designs the **AIMS and control library** the auditor audits against. The audit function does not author the SoA or the control taxonomy inside an engagement.
- The **Chief Audit Executive** owns the audit-committee interface, the plan approval, and the enterprise audit strategy. The AI Auditor at level 45 supports, drafts, and executes — but does not own the relationship. Chapter 7 is explicit on this boundary.

## Structure

- Lecture chapters `01-…md` … `07-…md`.
- `exercises/` — hands-on prompts (solutions live in the paired `-solutions` repository).
- `labs/` — long-form hands-on labs (planned; see `labs/README.md`).
- `quizzes/` — knowledge checks (planned; see `quizzes/README.md`).
- [`resources.md`](resources.md) — primary standards, codes, and credential references for every chapter and exercise.
