# exercise-03: Materiality Tuning Drill by Engagement Type

**Estimated effort:** 2 hours

## Objective

Author four separate signed-and-dated materiality workpapers for the same underlying AI system under four different engagement types — ISO/IEC 42001 certification audit, EU AI Act Article 43 conformity assessment, SOC-for-AI attestation under SSAE 18 / AT-C 205, and internal risk-based audit under IIA Standards 2024 — so the tuning choices become explicit. The deliverable is four workpapers plus a one-page comparison memo contrasting the four.

## Prerequisites

- Chapter [`03-materiality-for-ai-audit.md`](../03-materiality-for-ai-audit.md)
- `mod-101` chapter 5 (IAASB and AICPA attestation stack) and chapter 6 (ISO 19011 / 17021-1 / 42006)
- `mod-102` chapter 7 (IAASB / AICPA AI assurance standards)

## Scenario

**Clerestory Health**, a fictitious multi-hospital US health system with a growing EU operations footprint, operates an AI system named **TriageVision**:

- Deep-learning image classifier assisting emergency-department triage on chest-X-ray intake; outputs a priority score and routes radiologist review order.
- Deployed in 14 US hospitals (≈ 1.8M scans/year); EU pilot (3 hospitals; ≈ 180K scans/year started six months ago).
- Human-on-the-loop: a radiologist signs off before the clinician acts.
- Trained internally; running on Clerestory's own GPU cluster plus an on-prem inference deployment; no GPAI usage.
- Classified as **FDA 510(k)-cleared AI/ML-based SaMD Class II** in the US with a Predetermined Change Control Plan (PCCP) in place.
- Classified as **EU AI Act Annex III high-risk (health)** in the EU operation; conformity assessment under Article 43 is required before expansion to a fourth EU country.
- No single decision exceeds a few thousand dollars in direct financial impact, but a false low-priority routing can have patient-safety consequences.
- Processes special-category data under GDPR Article 9; HIPAA-covered under US use.
- Has been in production 26 months; monitoring-dashboard review happens weekly; an incident register is maintained.

### The four engagements

- **E-A** — Clerestory's accredited certification body is running the Stage-2 audit of Clerestory's AIMS; TriageVision is one of the AI systems in scope.
- **E-B** — A notified body is contracted to perform the EU AI Act Article 43 conformity assessment on TriageVision for the EU pilot, pre-expansion.
- **E-C** — Clerestory contracts a Big-4 firm for an SSAE 18 / AT-C 205 SOC-for-AI attestation over TriageVision to share with payer partners and self-insured-employer customers.
- **E-D** — Clerestory's internal audit function is running an AI-system audit of TriageVision this cycle under IIA Standards 2024.

## Requirements

1. **Four materiality workpapers** — one per engagement, using the template at the end of chapter 3:
    - Engagement type and standards applied
    - Intended user(s) and decisions
    - Quantitative bases chosen (financial impact, affected population, decision volume) with thresholds
    - Qualitative lenses in play and the criteria they attach to
    - Performance materiality value
    - Tolerable misstatement for sampling-heavy criteria
    - Specific materiality items and rationale
    - Re-assessment triggers
    - Approval and date
2. **One-page comparison memo** — side-by-side contrast of:
    - What quantitative base is dominant, and why
    - How each engagement handles the patient-safety qualitative lens
    - How each engagement handles the FDA PCCP qualitative lens
    - How each engagement handles the EU AI Act regulatory-classification qualitative lens
    - Where overall materiality is lowest and highest and why
    - The one qualitative lens that materially differentiates one of the four from the other three

## Starter guidance

- The ISO/IEC 42001 engagement (E-A) does not use financial materiality. Grading is on NC severity under ISO 19011 clause 6.4.8 and 17021-1 clause 9.4.9.1 — major vs. minor. Explain how qualitatively-material items could lift an otherwise-minor finding to major for TriageVision specifically.
- The EU AI Act conformity assessment (E-B) is close to binary on Articles 9–15. Document the materiality as a conformity threshold, not a dollar figure. Explain how Article 15 (accuracy, robustness, cybersecurity) interacts with the patient-safety lens.
- The SOC-for-AI attestation (E-C) blends financial, affected-population, and decision-volume bases. Intended users are the payer partners and self-insured employers; write the overall-materiality threshold from *their* decision perspective, not Clerestory's.
- The internal audit (E-D) anchors on residual risk vs. the audit committee's risk appetite. The audit committee at a hospital system will almost certainly treat patient-safety risk differently from a bank's audit committee. Make that specific.
- Performance materiality is not optional; set it in each workpaper.
- Tolerable misstatement should drive a sample size for at least one criterion in each workpaper (a fairness or accuracy-slice criterion is the natural choice given the subject matter).
- Specific materiality must appear for the qualitative lenses — patient safety, children (paediatric chest X-rays are in population), special-category data.
- Where the scenario does not supply enough detail (e.g., exact FDA PCCP wording, exact harmonised-standard citations for E-B), use `<!-- needs-research -->` markers rather than invent.

## Acceptance criteria

- Four workpapers delivered, each dated and signed in the template from chapter 3.
- Each workpaper names the standards it applies under and the intended user(s).
- Each workpaper has a distinct quantitative-base profile — the four are not the same workpaper with the heading changed.
- Each workpaper carries at least one piece of specific materiality tied to a qualitative lens (patient safety; regulatory classification; special-category data; PCCP).
- Performance materiality is set in each workpaper; tolerable misstatement drives at least one sample-size calculation per workpaper.
- The comparison memo is one page and actually contrasts — it does not summarise each workpaper in isolation.
- Where materiality cannot be set in a dollar amount (E-A, E-B), the operational threshold (NC severity, conformity threshold) is explicit.
- The internal-audit materiality (E-D) explicitly links to the audit-committee risk appetite in the organisation's risk-appetite statement (or names the absence of such a statement and the proposed interim threshold).
- No fabricated regulations, enforcement actions, or ISO audit-day tables.
- No workpaper over-relies on financial-impact materiality for a patient-safety subject matter; if it does, the memo flags that as the failure mode.

## Stretch goals

- Author a **materiality-revision scenario** — a plausible finding emerges mid-engagement that triggers re-assessment of overall materiality in one of the four engagements. Produce the one-page revision memo (original threshold, new threshold, evidence that prompted the change, impact on completed and remaining procedures, communication to the responsible party under ISA 320 paragraph 12 by analogy).
- Produce a **cross-engagement coordination note** — the four engagements are running within six months of each other; what evidence can be shared? What independence posture prevents sharing? Where would a shared materiality posture create an audit risk?
- Author a **public-facing SOC-for-AI materiality disclosure paragraph** (E-C) that would appear in the AICPA report's "basis for conclusion" section without over-disclosing internal thresholds.
