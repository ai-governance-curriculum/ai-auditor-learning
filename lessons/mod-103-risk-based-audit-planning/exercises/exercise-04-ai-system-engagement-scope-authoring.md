# exercise-04: AI-System Engagement Scope Authoring

**Estimated effort:** 3 hours

## Objective

Author a complete scope memo and engagement-letter draft for a single AI-system audit engagement, covering all seven chapter-4 elements — purpose, criteria, boundaries, period, population, sampling, inherent limitations and deliverable shape — to a standard a signing engagement leader could execute. The scenario deliberately contains scope traps you must resolve rather than ignore.

## Prerequisites

- Chapter [`04-scoping-a-single-ai-system-engagement.md`](../04-scoping-a-single-ai-system-engagement.md)
- Chapter [`03-materiality-for-ai-audit.md`](../03-materiality-for-ai-audit.md)
- `mod-102` criteria register discipline (chapters 1–7)

## Scenario

**StreetGuide** is a fictitious US employment-services vendor operating an AI-powered career-navigation product sold to municipal and state workforce boards. Its flagship system **PathFind** is:

- A retrieval-augmented LLM assistant plus a classification pipeline that recommends training programmes and job postings to jobseekers.
- Deployed to 7 state workforce agencies covering ≈ 2.4M jobseekers; one of those states is Colorado. The product has an "AI assistant" surface and a backend "routing score" that participating employers use.
- Routes jobseekers to specific training providers; the system influences enrolment decisions.
- Uses OpenAI GPT-4-class models via Azure OpenAI for generation; uses an in-house classification model for routing scores; retrieval over a provider-catalogue vector index.
- Classified by StreetGuide as **Colorado AI Act consequential decision** (education / employment) in the Colorado deployment; the other six states vary.
- Not classified by StreetGuide as an NYC LL144 AEDT — StreetGuide argues the routing is advisory and does not substantially assist employment decisions. Audit disputes.
- Subject to a recent class-action notice-of-intent from a plaintiff's firm alleging disparate impact on jobseekers with disabilities (publicly filed last month; StreetGuide's legal counsel is engaged).
- Has an incident register, a weekly monitoring dashboard, retrains the classification model quarterly, and deploys prompt-level LLM updates weekly.

### The engagement

StreetGuide has contracted a mid-tier assurance firm for an **AT-C 205 assertion-based examination** of PathFind. Intended users are StreetGuide's workforce-agency customers who need external assurance of PathFind's fairness, transparency, and incident-handling claims. Clerestory-type certification work is not in scope; this is a US SSAE 18 / AT-C 205 engagement.

Mid-cycle complication: StreetGuide's VP of Engineering has just informed the engagement team that PathFind's backend model was *migrated* from an in-house classification pipeline to a fine-tuned OpenAI model two months into the period of coverage.

## Requirements

1. **Scope memo** in the chapter-4 skeleton. Include every element.
2. **Engagement letter** draft (≤ 4 pages) suitable for the signing engagement partner. Include:
    - Three-party relationship (responsible party, engaging party, intended users)
    - Subject matter and criteria
    - Period and deliverable
    - Scope boundaries and explicit exclusions
    - Materiality reference
    - Inherent limitations paragraph
    - Independence representation
    - Reliance-on-specialists paragraph (ISA 620)
    - Report distribution and restriction
    - Fee basis (notional)
3. **Scope-dispute resolution memo** (≤ 1 page) on the NYC LL144 applicability question — document the StreetGuide position, the audit position, and your scope resolution.
4. **Scope-change memo** (≤ 1 page) on the mid-period model migration — scope impact, procedure impact, period-of-coverage impact, deliverable impact; recommend acceptance, rejection, or renegotiation of the engagement.

## Starter guidance

- Chapter 4's seven elements must each appear in the scope memo. Omitting any is a fail.
- Period of coverage: a mid-period model migration is a classic scope trap. Two acceptable resolutions — scope narrows to a sub-period around one model version with a new engagement for the other, or scope keeps both versions with a disclosure that the subject matter changed mid-period. Argue the one you pick, do not assume.
- Population definition: the LLM-chat population and the classification-routing-score population are different populations with different criteria. The engagement will probably need both.
- Sampling: the chapter-4 §6 options apply. Choose one approach per criterion category (fairness, transparency, incident handling, change management) and name tolerable misstatement.
- Boundaries: Azure OpenAI is a cloud-provider interface to a GPAI model. The scope out list must say what you are *not* testing (the GPT-4-class model internals) and what you *are* testing (StreetGuide's usage: prompts, guardrails, logging, usage-control, contractual posture, reliance on vendor evidence).
- NYC LL144 applicability dispute: resist both extremes (do not accept StreetGuide's characterisation on faith; do not unilaterally extend scope to include an AEDT bias audit without a renegotiation). The scope-dispute memo documents your position and the path to resolution.
- Reliance on specialists: an ML specialist under ISA 620 is near-certain; a legal specialist on Colorado AI Act applicability is likely; a disability-domain specialist may be appropriate given the class-action context.
- The pending class-action is not a reason to decline the engagement, but it is a scope-shaping and inherent-limitation driver — document accordingly.
- Deliverable shape: AT-C 205 is an examination (reasonable assurance). Confirm the procedures proposed are consistent with reasonable assurance; downshifting to a review (AT-C 210) or AUP (AT-C 215) requires renegotiation.
- Where the scenario does not specify (e.g., exact Colorado AI Act operator-vs-developer classification), use `<!-- needs-research -->` markers.

## Acceptance criteria

- The scope memo contains all seven chapter-4 elements, each in the explicit form named in the chapter (not merged or implied).
- The engagement letter is suitable for a signing partner — it does not contain hedging that would make the opinion unreliable; it does not contain overreach that would make independence indefensible.
- The three-party relationship is correctly named: responsible party (StreetGuide), engaging party (StreetGuide), intended users (StreetGuide's workforce-agency customers). The AT-C 105 three-party construct is honoured.
- The NYC LL144 scope-dispute memo takes a position with a documented path to resolution (regulator interpretation, legal opinion, renegotiation, scope-out with disclosure) — it does not simply defer.
- The model-migration scope-change memo picks one of the acceptable period resolutions and defends it; silent continuation on both model versions without disclosure is a fail.
- The sampling plan names an approach and a tolerable misstatement per criterion category.
- Inherent limitations list is specific to PathFind (opaque GPT-4-class internals; non-stationarity from weekly prompt updates; third-party-provider reliance; pending-litigation posture) — not a boilerplate list.
- The ISA 620 specialist roles are named with their scope of work and objectivity check.
- No fabricated statutes, regulatory deadlines, or firm-policy quotations.
- At least two `<!-- needs-research -->` markers are present where the scenario legitimately underspecifies.

## Stretch goals

- Author the **pre-engagement independence memo** for the engagement team under AICPA independence rules, considering that the mid-tier firm has provided a prior consulting-shaped readiness assessment for StreetGuide 14 months ago.
- Draft the **auditor-committee-communication plan** between the firm and StreetGuide's governance body (StreetGuide is private; there is no SEC audit committee; design the equivalent communication rhythm).
- Produce a **report-restriction paragraph** that permits workforce-agency customers to rely on the report but restricts distribution beyond them — including the specific decision each intended user is permitted to make with the report.
