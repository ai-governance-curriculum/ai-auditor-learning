# exercise-02: SR 23-4 Vendor Audit

**Estimated effort:** 3 hours

## Objective

Audit a third-party AI vendor engagement end-to-end against **SR 23-4** (the 2023 Interagency Guidance on Third-Party Relationships: Risk Management), producing the per-vendor engagement-walk workpaper chapter 2 describes — planning, due diligence, contract, ongoing monitoring, termination — plus the cross-cutting oversight, accountability, documentation, and reporting tests, and a concentration-risk pass across the vendor book.

The deliverable shows a reviewing partner that the organisation's reliance on the vendor is defensible (or isn't) across the five phases and that the broader AI vendor book has been reperformed against the inventory.

## Prerequisites

- Chapter [`02-auditing-third-party-ai-under-sr-23-4.md`](../02-auditing-third-party-ai-under-sr-23-4.md).
- `mod-101` on the three lines and the auditor's position.
- `mod-103` on engagement-letter scoping and materiality.
- `mod-104` on evidence discipline, ISA 500, ISA 530.
- Chapter 3 (assurance artifacts) for the phase-2 depth; this exercise references the chapter-3 patterns but keeps the deep SOC 2 / ISO / 42001 work to exercise 03.

## Scenario

**MetroBank**, a mid-sized regional bank, is a US bank-holding-company subsidiary subject to Federal-Reserve supervision. The bank uses:

- A foundation-model-provider API (vendor A) for an internal employee-productivity assistant.
- A specialist AI vendor (vendor B) for a credit-risk narrative-summarisation workflow that feeds adjudicator decisions.
- A moderation / safety-guardrail SaaS (vendor C) sitting in front of both A and B.

Vendor B is classified as a *critical activity* under SR 23-4; vendors A and C are *high*. The bank's third-party risk function (TPRF) maintains the vendor inventory and tiering methodology; the AI-risk second line owns AI-specific diligence overlays; internal audit (you) owns the independent reperformance.

If you prefer a different anchor, substitute a comparable organisation (insurer, healthcare system, large employer with vendor-dependence on AI). State the chosen subject at the top of the deliverable.

## Requirements

1. **Scope and criteria stacking.** Pin the engagement: organisation, vendor book, vendors sampled, SR 23-4 as the primary criterion, any applicable overlays (EU AI Act for EU customer-facing products, OMB chapter-7 if a federal contractor, NAIC bulletin for insurer analogues), and the engagement-letter materiality threshold.

2. **Tiering-methodology test.** Read the organisation's risk-tiering methodology. Build a one-page critique: are the factors sound (criticality, data sensitivity, customer impact, operational impact, concentration, newness, regulatory sensitivity)? Are AI-specific factors (autonomy, training-data exposure, model-change frequency, cross-border flow) built in? Are tier definitions specific enough to prescribe diligence depth / monitoring cadence / contract clauses / approval authority? Methodology findings are *program-level*.

3. **Vendor-inventory three-sweep reperformance.** Independently reconcile the AI vendor inventory against:
   - Accounts-payable records for the look-back period (filter on AI-vendor keywords and known providers).
   - Identity-and-access logs (OAuth grants, API keys issued, SSO application list, cloud marketplace subscriptions).
   - Engineering-and-product-lead interviews (at least three leads; capture their stack dependencies).

   Shadow vendors (in AP / IAM / stack but not in the inventory) are findings.

4. **Per-vendor engagement walk.** Sample vendors proportional to tier: at least one Critical, at least one High, and at least one Moderate; one Low is optional. For each sampled vendor, produce the chapter-2 engagement walk workpaper:
   - **Planning phase evidence.** Business case, inherent-risk assessment, tier assignment, approval-authority sign-off, alignment to the AIMS use-category inventory.
   - **Due diligence.** Reperform at least four claims from the diligence folder against corroborating evidence (financial health, assurance artefact presence, data-use terms, subcontractor list, red-team / safety-evaluation materials).
   - **Contract clause-level test.** Right-to-audit, data-use restrictions, model-version pinning and change notification, incident-notification SLA, subprocessor change notice, indemnification / insurance, confidentiality / IP ownership, termination.
   - **Ongoing monitoring.** For one monitoring event in the period, trace signal → triage → management action.
   - **Exit plan.** Confirm existence at onboarding, scenario coverage, alternate-vendor named, data return / destruction, prompt / fine-tune / derivative-artefact portability for AI vendors specifically.

5. **Right-to-audit exercise history.** Confirm whether the right-to-audit clause has ever been exercised for each Critical vendor. A Critical right-to-audit clause unexercised across the engagement period is a monitoring finding.

6. **Concentration-risk pass.** From the full vendor inventory, compute concentration counts — foundation-model, cloud, embedding, guardrail concentrations. Identify correlated dependencies (cloud underlying multiple "alternate" vendors). Confirm that the organisation's board / senior-management reporting reflects the concentration posture at materiality.

7. **Cross-cutting tests.** Named relationship / control / operations owners per vendor. Documentation retention. Independent review (which is this engagement). Board / senior-management visibility.

8. **Findings register.** Columns: finding ID, title, SR 23-4 phase / factor cited, affected vendor (or "program"), severity, evidence pointer, management-response-requested shape. Classify each finding as vendor-specific or program-level.

9. **Sampling and workpaper hygiene.** Record stratification, ISA 530 sampling-size justification, retrieval timestamps, redaction / sensitivity notes.

## Starter guidance

- SR 23-4 is a risk-proportionate framework — do not hold a Low-tier vendor to a Critical-tier diligence depth; do flag when a Low-tier vendor is mistakenly tiered.
- Shadow AI usually has the highest finding count in this work. Build the three-sweep reperformance carefully and name the specific shadow vendor(s) found.
- The right-to-audit test often reveals that the clause is present but never exercised — the finding is monitoring-maturity, not contract.
- Concentration risk is a *posture* finding; frame it as "the posture is X, it has not been board-reported at the applicable materiality." Do not recommend a specific concentration ceiling — that is management's call.
- Exit plans tend to be the weakest phase. Specifically check for *prompt / fine-tune / derivative-artefact portability* in the AI vendor context — a plan that assumes the vendor's model is interchangeable with an alternate is often wrong.
- Where the chapter-3 depth (SOC 2 / ISO 42001 scope and carve-outs) is material to a finding, pin it with a pointer and defer the deep work to exercise 03.

## Acceptance criteria

The deliverable is accepted when:

- Scope and criteria stacking are pinned with the SR 23-4 phases as the primary audit backbone.
- Tiering methodology is tested at the program level with a one-page critique.
- Vendor-inventory three-sweep reperformance covers AP, IAM, and engineering, and produces named findings for shadow vendors or an explicit "no shadow vendors detected" conclusion.
- At least three vendors are walked across the full five-phase lifecycle, with clause-level contract testing.
- Right-to-audit exercise history is reperformed for Critical vendors.
- Concentration-risk pass is documented with counts and correlated-dependency notes.
- Cross-cutting tests (ownership, retention, independent review, board visibility) are each addressed.
- Findings are stated against the specific SR 23-4 phase / factor and classified vendor-specific or program-level.
- Sampling and workpaper hygiene per `mod-104`.
- `<!-- needs-research: ... -->` markers appear where primary sources do not resolve a claim.

## Stretch goals

- Author the **per-vendor residual-risk worksheet** — inherent risk, controls, residual risk, change vs. prior period, drivers — for each sampled vendor, consistent with `mod-107` chapter 2 scoring methodology.
- Draft a **template update** for the organisation's AI-vendor diligence questionnaire that closes the three highest-severity findings.
- Produce a **concentration-risk heat map** suitable for the board pack, showing the concentration posture across the AI vendor book.
- Write a **≤500-word memo** on when the right-to-audit clause should be exercised for AI vendors, including the AI-specific triggers (model-version swap, published jailbreak, change of subprocessor including foundation-model provider).
