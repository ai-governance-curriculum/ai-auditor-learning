# NAIC Insurer and US State AI Audit Overlays — Colorado SB 24-205 and Illinois AIVIA

## Motivation

US AI regulation is organised through **three parallel strata**. Federal law is sectoral (FCRA, ECOA, FDA, SR 11-7); state law is becoming horizontal (Colorado SB 24-205, Illinois AIVIA, Connecticut, Utah, Texas AI Act, New York Executive Order 25, California AB 2013 / SB 1047-related legislation); and city law adds specific obligations (NYC LL144, Chapter 4). The insurance line of business adds a fourth layer through the **National Association of Insurance Commissioners (NAIC) Model Bulletin on the Use of Artificial Intelligence Systems by Insurers**, adopted by state Departments of Insurance (DOIs) with state-specific variants.

An auditor engaged by a regulated insurer, or by a deployer operating in Colorado or Illinois (and increasingly other states), must assemble an audit shape from the overlapping layers. This chapter is the auditor's shape across three defined overlays:

- **NAIC Model Bulletin** — the AI governance and risk management expectations for insurers, adopted by state DOIs with variations.
- **Colorado SB 24-205 (the Colorado AI Act)** — the first US horizontal law imposing an algorithmic-discrimination duty on **deployers** of high-risk AI systems, with a "reasonable care" affirmative defence.
- **Illinois AIVIA (and the Illinois AI in Employment Decisions amendments, HB 3773 / amended Illinois Human Rights Act)** — targeted statutes for AI-assisted video interviews and AI employment decisions.

Other state laws follow similar shapes but are not developed in this chapter; the shapes here are instructive for the broader state-law audit pattern.

## The NAIC Model Bulletin — insurer AI governance

The NAIC Model Bulletin on the Use of AI Systems by Insurers, adopted December 2023 and being transposed into state regulation across 2024–2026, is the common language DOIs use when supervising AI use by insurers. It is **sub-regulatory**: it is not law directly, but DOIs adopt it as supervisory guidance and in some states codify portions of it. <!-- needs-research: confirm the state-by-state adoption status of the NAIC Model Bulletin at reading time; Nebraska, Connecticut, Illinois, Rhode Island, New Hampshire, Alaska, Vermont, Washington, Colorado, Oklahoma, West Virginia and others have adopted or substantially aligned; adoption is ongoing -->

### The bulletin's five pillars

1. **Governance.** An AI Systems governance framework, board/senior-management oversight, written policies, documented procedures, clear accountability for AI systems, inventory of AI systems, risk-based prioritisation.
2. **Risk management and internal controls.** Risk assessment covering reliability, bias, interpretability, data-input quality, performance, fairness, transparency, consumer protection, privacy, cybersecurity; controls proportionate to inherent risk; risk-acceptance.
3. **Third-party AI systems and vendors.** Due diligence, contract provisions, ongoing monitoring; aligned to NAIC's broader vendor-oversight expectations and the FRB / FDIC / OCC SR 23-4 model (`mod-109` chapter 2).
4. **Consumer-protection controls.** Fair claims handling, non-discrimination, adverse-decision explanation, dispute and redress mechanisms, aligning to the Unfair Trade Practices Model Act and the Unfair Claims Settlement Practices Model Act.
5. **Reporting to the DOI.** On DOI request; some state variants require annual attestations or specific AI-use disclosures.

### Audit test shape

The NAIC-bulletin audit is a management-system audit close in shape to ISO 42001 (`mod-105`) but with insurer-specific controls:

- **AI system inventory.** Per-system: name, line of business (personal auto, commercial, life, health, annuities), function (underwriting, pricing, claims, marketing, fraud, customer service), data classes used, protected-class-related factors, vendor status, risk tier, policy owner.
- **Governance.** Board or committee minutes evidencing oversight; written AI policy; role and responsibility chart; training records for staff who use AI systems.
- **Risk assessment.** Per-tier methodology application; evidence of bias, interpretability, performance, consumer-protection, privacy, cybersecurity assessments.
- **Controls.** For each risk, documented controls with evidence of operation; controls proportional to tier.
- **Third-party due diligence and monitoring.** Diligence files per vendor-AI; contract terms (right-to-audit, data-use, model-change notification); ongoing monitoring; SR-23-4-shaped evidence.
- **Consumer-protection operation.** Adverse-decision explanation (when a model declines a claim or raises a premium, is the consumer informed and offered a review?); fair-claims-practices complaint review; complaints-and-grievances handling that reaches the AI decisioning.
- **DOI reporting.** Any required disclosures made; internal response capability to DOI information requests; attestation-of-AI-use records where state has adopted them.

The audit finds against **the governance framework's operation**, not against specific models' performance (model-level findings go to the SR-11-7-shape audit of chapter 5 or to a specific actuarial validation).

### State-specific variants to anticipate

- **Colorado SB 21-169.** Colorado's prior insurance-specific algorithmic-discrimination statute predates the horizontal SB 24-205; insurers in Colorado remain subject to both.
- **New York DFS Circular Letter No. 7 (2024).** New York's Insurance Department guidance on the use of AI and ECDIS (external consumer data and information sources); specific additional expectations for insurers using AI in underwriting and pricing. <!-- needs-research: confirm NY DFS Circular Letter No. 7 (2024) at reading time -->
- **California Department of Insurance.** Bulletins and emerging regulations around AI use.

The audit's state-coverage workpaper maps each state of licensure to the applicable DOI's AI supervisory posture.

## Colorado SB 24-205 — the first US horizontal deployer duty

Colorado's SB 24-205 (signed May 2024, with substantive provisions phasing in; most provisions effective 1 February 2026) is the first US horizontal state law imposing a duty on **deployers** of **high-risk AI systems** to use **reasonable care** to prevent **algorithmic discrimination**. <!-- needs-research: confirm Colorado SB 24-205 effective-date status, any legislative amendments, and the AG's implementing rules at reading time -->

### Covered deployers and systems

- **Deployer** — any person doing business in Colorado that deploys a high-risk artificial intelligence system.
- **High-risk AI system** — a system that, when deployed, makes or is a substantial factor in making a **consequential decision** affecting a consumer, where consequential decision means a decision with material impact on provision or cost of education enrolment or educational opportunity, employment or employment opportunity, financial or lending service, essential government service, healthcare service, housing, insurance, or legal service.
- **Developer** — any person doing business in Colorado that develops or substantially modifies a high-risk AI system.

Both developers and deployers carry obligations; the deployer obligations are the shape most auditors encounter.

### The deployer's duty

A deployer must use **reasonable care to protect consumers from any known or reasonably foreseeable risks of algorithmic discrimination**. The statute creates a rebuttable **presumption** that reasonable care has been used if the deployer:

- implements and maintains a **risk-management policy and program** governing the deployment of each high-risk AI system;
- completes an **impact assessment** for each high-risk AI system meeting defined content requirements;
- notifies affected consumers of the AI's use and provides specific information;
- allows a consumer the opportunity to **correct personal data** that the system relied on;
- allows a consumer the **opportunity to appeal** adverse consequential decisions;
- discloses the use to the **Colorado Attorney General** on discovery of algorithmic discrimination within a defined time.

The deployer's affirmative compliance posture is thus a **structured policy, impact-assessment, consumer-notice, correction, appeal, and incident-disclosure** stack.

### Audit test shape for the deployer

The auditor's Colorado workpaper per high-risk system:

- **Risk-management policy and program evidence.** Written policy; named owners; periodic review; coverage of each high-risk system.
- **Impact assessment per system.** Content covering the system's intended use, data used, foreseeable algorithmic-discrimination risks, mitigation measures, monitoring plan, benefits analysed against risks. The impact assessment is updated annually and after substantial modifications.
- **Consumer-notice artefacts.** The notice as delivered to consumers; content against the statutory requirements; delivery evidence.
- **Correction mechanism.** Procedure a consumer uses to correct data; log of correction requests and dispositions.
- **Appeal mechanism.** Procedure a consumer uses to appeal an adverse decision; evidence of operation; outcomes.
- **Discovery-and-disclosure evidence.** Internal procedure for discovering algorithmic discrimination; time-clock from discovery to AG disclosure; disclosures made.

For developers, additional obligations apply around documentation provided to deployers, including a high-risk AI system documentation package the deployer uses in its impact assessment.

### Presumption and affirmative defence posture

The presumption of reasonable care is **rebuttable**. The AG can present evidence that the deployer failed in fact to use reasonable care. The audit's role is to document the deployer's affirmative posture — not just that the documents exist, but that the deployer's operation actually delivered on the statute's design.

Audit findings against Colorado SB 24-205 are not findings of "violation" (the AG will make that determination); they are findings that the deployer's posture would not support the presumption under adversarial review.

### Interface with insurance supervision

Colorado-domiciled insurers deploying AI in underwriting, pricing, claims, or marketing face Colorado SB 21-169 (insurance-specific), the NAIC Model Bulletin as adopted by the Colorado DOI, and SB 24-205 (horizontal deployer duty). The audit must integrate all three; the SB 24-205 impact assessment covers ground a Colorado SB 21-169 compliance evaluation already covers, and the auditor must reuse evidence efficiently.

## Illinois — AIVIA and HB 3773

Illinois has two targeted employment-context AI statutes.

### Artificial Intelligence Video Interview Act (AIVIA)

AIVIA (820 ILCS 42) applies to employers who use AI analysis to evaluate applicant video interviews for positions based in Illinois. Required:

- **Notification** to the applicant that AI may be used to analyse their video interview;
- **Information** about how the AI works and the characteristics it uses to evaluate applicants;
- **Consent** before the AI analysis is conducted;
- **Limited sharing** of the video to those with expertise or technology necessary to evaluate it;
- **Destruction** of the video within 30 days of applicant request;
- **Report** to the Illinois Department of Labor for employers that rely solely on AI analysis to determine whether an applicant will be selected for an in-person interview, including racial/ethnic demographic data of applicants afforded and not afforded interviews. <!-- needs-research: confirm whether the AIVIA reporting-to-IDOL requirement remains in force and its current form at reading time -->

### Illinois AI in Employment Decisions (HB 3773 — Illinois Human Rights Act amendments)

HB 3773, signed August 2024 with effective date 1 January 2026 (as amended), extends the Illinois Human Rights Act to prohibit employers from using AI in employment decisions in a manner that has the effect of subjecting employees to discrimination on the basis of protected classes. Required:

- Notification to employees and applicants when AI is used in employment decisions (recruitment, hiring, promotion, discharge, discipline, tenure, or terms, privileges, or conditions of employment).
- Non-discriminatory use of AI with respect to protected characteristics. <!-- needs-research: confirm final effective date and Illinois Department of Human Rights rulemaking status at reading time -->

### Audit test shape

The auditor's Illinois workpaper:

- **AIVIA applicability.** Does the employer use AI to evaluate video interviews of Illinois-based applicants?
- **AIVIA notification, information, consent.** Pre-interview text; consent capture; evidence per applicant.
- **AIVIA sharing and destruction.** Access logs; destruction records on applicant request.
- **AIVIA IDOL reporting.** For employers relying solely on AI for the interview advancement decision, the demographic reporting.
- **HB 3773 applicability.** Does the employer use AI in employment decisions involving Illinois employees or applicants?
- **HB 3773 notification.** The notice to employees and applicants.
- **HB 3773 non-discrimination testing.** Evidence the AI does not have discriminatory effect on protected classes, analogous to the LL144 impact-ratio analysis but less prescriptive (Illinois Department of Human Rights rulemaking may add specifics).

### Illinois AIVIA and HB 3773 interface with NYC LL144 and Colorado SB 24-205

An AEDT used by an employer operating in NYC, Illinois, and Colorado faces LL144 (bias audit + public summary + candidate notification), AIVIA (if video-interview analysis), HB 3773 (non-discriminatory use + notice), and SB 24-205 (deployer duty for employment-related high-risk AI). The audit integrates evidence across the regimes, with specific statutory outputs in each.

## State overlay audit — the integrated workpaper

For a national deployer, the auditor's state-overlay workpaper:

| State | AI regime | Deliverable | Timing |
|-------|-----------|-------------|--------|
| NYC (within NY State) | LL144 | Public summary of bias audit; candidate notification | Annual |
| Colorado | SB 24-205 | Risk-management program; impact assessment; consumer notice; correction & appeal; AG disclosure on incident | Ongoing with annual IA update |
| Illinois | AIVIA | Notice; information; consent; destruction; IDOL report if applicable | Per applicant / annually |
| Illinois | HB 3773 (IHRA amendments) | Notice; non-discriminatory use evidence | Ongoing from effective date |
| Any state w/ adopted NAIC bulletin | Insurer bulletin | Governance program; risk assessment; third-party controls; consumer protection; DOI reporting | Ongoing with on-request reporting |
| Any state w/ its own insurance AI statute | State-specific | Varies | Ongoing |
| Connecticut | AI statute (as adopted) | Varies | State-specific |
| Utah AI Policy Act | Varies | Disclosure of AI use; interaction with state licensure | State-specific |
| California | Multiple (AB 2013, ADS regs) | Varies | State-specific |
| Texas | AI Act (as adopted) | Varies | State-specific |

<!-- needs-research: at reading time, several states will have added specific AI statutes not included above; the state-overlay workpaper must be refreshed against the current legislative map -->

The integrated workpaper is the output a general counsel's office uses to plan the deployer's compliance posture; the auditor's role is to populate the workpaper with per-state evidence.

## Governance, reporting, and the DOI / AG interface

Insurer and deployer audits terminate in two external-reporting touchpoints:

- **DOI reporting** — on request (NAIC bulletin), annual attestations (state-specific), rate-filing disclosures (state-specific), and examination responses.
- **AG reporting** — Colorado SB 24-205 algorithmic-discrimination disclosures; other state attorneys-general where state AI statutes add direct AG reporting.

The audit reviews the deployer's capability to respond to these touchpoints — both the records required and the process for producing them within the regulatory clock.

## Common failure modes

- **NAIC bulletin treated as non-binding.** State DOI has adopted the bulletin; insurer treats it as "guidance"; DOI examination finds the governance shape missing.
- **Shadow AI book at the insurer.** Vendor claim-triage AI deployed by a business line without routing through the governance framework.
- **Colorado SB 24-205 impact assessment template boilerplate.** Impact assessments are structural copy-paste with no system-specific analysis; presumption of reasonable care would not survive AG challenge.
- **Correction and appeal mechanism nominal.** Mechanism exists in policy; no operational evidence; audits must see actual requests and dispositions.
- **AIVIA consent bundled with other employer consents.** Consent is not specific to AI analysis of the video; AIVIA requires specific AI-disclosure consent.
- **HB 3773 testing shaped to LL144.** Testing uses LL144 methodology without checking whether Illinois Department of Human Rights has issued its own methodology; findings may be mis-scoped.
- **State-overlay workpaper stale.** New state statutes enacted since the last audit; coverage gap.
- **Insurer DOI information-request latency.** Insurer cannot assemble the AI-governance evidence quickly enough to meet DOI information requests; examination escalates.
- **Developer / deployer boundary confused at Colorado.** Deployer treats a vendor's documentation as satisfying its own impact-assessment duty; the statute requires the deployer's own impact assessment.
- **Double-counting evidence across regimes.** LL144 bias audit reused for Colorado SB 24-205 impact assessment without reconciling statutory shape differences; audit must document reuse explicitly.

## Summary

- US state and local AI audits overlay on sectoral federal regulation; insurers face the NAIC Model Bulletin as adopted by state DOIs; Colorado deployers face SB 24-205's reasonable-care duty for high-risk AI; Illinois employers face AIVIA (AI video-interview analysis) and HB 3773 (IHRA amendments on AI in employment decisions); NYC employers face LL144 (chapter 4).
- The NAIC Model Bulletin audit resembles ISO 42001 in shape but with insurer-specific controls: governance, risk management, third-party oversight (SR-23-4-aligned), consumer protection, DOI reporting; findings go to the governance framework's operation, not to model-level performance.
- Colorado SB 24-205's deployer duty is satisfied through a documented posture — risk-management program, impact assessment per high-risk system, consumer notice, correction and appeal, and incident disclosure to the AG — creating a rebuttable presumption of reasonable care that the audit defends against adversarial review.
- Illinois AIVIA requires AI-specific notification, information, consent, sharing limitations, destruction on request, and (for employers relying solely on AI for interview decisions) demographic reporting to IDOL; HB 3773 extends IHRA's non-discrimination rules to AI-enabled employment decisions and adds notice obligations.
- An integrated state-overlay workpaper per deployer maps each state of operation to the applicable regime and the specific statutory deliverable; the workpaper is refreshed against the current legislative map because state AI statutes continue to be enacted.
- Common failure modes include treating sub-regulatory NAIC as non-binding, boilerplate Colorado impact assessments, nominal consumer-correction and appeal mechanisms, AIVIA consent bundled with other consents, confusion between developer and deployer obligations, and stale state-overlay coverage.
