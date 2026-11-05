# Auditing Third-Party AI Under SR 23-4

## Motivation

Most organisations do not train frontier models. They buy them — via API from OpenAI, Anthropic, Google, AWS Bedrock, Azure OpenAI, Databricks; via open-weight distribution from Hugging Face; via embedded vendors (ServiceNow Now Assist, Salesforce Einstein, Microsoft Copilot, Adobe Firefly); via specialist vendors (Harvey, Hippocratic AI, Ambience Healthcare). The auditor's risk surface is therefore less about internal model development and more about **the controls that attach to externally-sourced AI**.

In US banking, the controlling criterion is the **Interagency Guidance on Third-Party Relationships: Risk Management** issued in June 2023 by the Federal Reserve Board, FDIC, and OCC — commonly cited as **SR 23-4** at the Federal Reserve. This guidance replaced the fragmented prior agency guidance (OCC 2013-29, FRB SR 13-19, FDIC FIL-44-2008) with a unified, risk-tiered framework. It is written at the level of "third-party relationships" generically, so it applies to AI vendors the same way it applies to core-banking providers and payments processors. The guidance explicitly covers critical-activity relationships, data-sensitive relationships, and new-technology relationships — three categories that typically converge on the AI-vendor profile.

Even outside banking, SR 23-4 is a de facto global template. It is the clearest articulation of vendor-risk expectations any regulator has produced, and organisations under EU AI Act, DORA, HIPAA, NIS2, or simply mature ISO/IEC 42001 programmes often adopt SR-23-4-shaped controls because the guidance is well-engineered and auditable.

This chapter is the auditor's shape for testing an organisation's third-party AI controls against SR 23-4's five-phase lifecycle — planning, due diligence and third-party selection, contract negotiation, ongoing monitoring, and termination — plus the cross-cutting concerns of oversight and accountability, documentation, and reporting. The auditor's test is not "did the vendor send a diligence questionnaire response" — it is "does the organisation's vendor-risk evidence survive an independent walk through the engagement lifecycle and across the vendor book."

## The SR 23-4 criteria shape

The auditor's first workpaper is the SR 23-4 lifecycle map. The guidance sets out five phases, each with named control expectations. The auditor builds the map once and reuses it per sampled vendor.

| Phase | Control areas (SR 23-4) | What the auditor expects to see |
|-------|-------------------------|---------------------------------|
| 1. Planning | Strategic alignment, risk assessment of the activity, inherent risk tiering, business case | Written assessment of the proposed AI use, inherent-risk tier (per the organisation's risk-tiering methodology), approval authority proportional to the tier, criticality-of-activity determination |
| 2. Due diligence and third-party selection | Legal and regulatory compliance, financial condition, business experience, operations and internal controls, risk management, information security, management of information systems, resilience, incident reporting, physical security, human-resources management, reliance on subcontractors, insurance, conflicts of interest | Documented due-diligence evidence proportional to tier: financials, SOC 2 / ISO / 42001 reports (chapter 3), security questionnaires (SIG, CAIQ, HECVAT), model-provider documentation (chapter 5), AI-specific diligence (training-data sources, evaluation results, red-team summary, incident history), site visits or management interviews for critical activities |
| 3. Contract negotiation | Scope of arrangement, performance measures, right-to-audit, confidentiality and ownership of information, information-security requirements, customisation of services, limits on subcontracting, incident notification, resilience and business continuity, indemnification and insurance, dispute resolution, termination | Executed contract (MSA + order form / DPA / BAA / AI-vendor addendum), right-to-audit clause and audit-execution evidence, data-processing terms, model-change and version-pinning terms, training-use-of-customer-data terms, incident-notification SLA, service-level-agreement (SLA) commitments, carve-out for serious-incident reporting cadence |
| 4. Ongoing monitoring | Continuous assessment proportional to risk, performance monitoring, control-environment monitoring, reassessment of due diligence, subcontractor monitoring, risk-tiering refresh | Monitoring plan per vendor tier, performance-metric dashboards or vendor-reported KPIs, annual (at least) reassessment, exception-based monitoring triggered by vendor events (incidents, breach disclosures, control-report publication), evidence the monitoring produces management action |
| 5. Termination | Transition planning, data return/destruction, continuity of service, communication to customers | Exit plan (built at onboarding, refreshed annually), termination scenarios (vendor insolvency, breach, performance failure, strategic exit), alternate-vendor identification, data-return/destruction attestation, customer-impact plan |
| Cross-cutting | Oversight and accountability, documentation and reporting, independent reviews | Vendor inventory, tiering methodology documented, board / senior-management reporting cadence, internal-audit coverage of the third-party program (this audit) |

<!-- needs-research: confirm SR 23-4's exact section names and the enumerated due-diligence factors against the June 2023 final interagency guidance text at reading time -->

The map is not the audit — the audit happens per vendor. The map ensures that when the auditor samples a vendor, every row in the workpaper has a named criterion.

## Risk tiering as the audit's hinge

SR 23-4 does not prescribe a single risk tier for all AI vendors. The guidance frames expectations as *proportional to risk* — a fringe vendor used once gets lighter diligence than a critical-activity vendor whose failure interrupts a core business function. The auditor's second step is to test the organisation's risk-tiering methodology before testing any individual vendor engagement.

The methodology must specify:

- **The factors that drive tier assignment.** Expected factors: criticality of activity, data sensitivity (PII, PHI, PCI, confidential business data), customer impact, operational impact, concentration risk, newness of technology, regulatory sensitivity. AI-specific factors the organisation should add: model autonomy (does the vendor model take action vs. advise?), training-data-exposure risk (does the vendor use customer data to train the model?), model-change frequency (is the vendor on a rapid-release cadence?), cross-border data flow (vendor's training and inference locations).
- **The tier definitions.** A three- or four-tier structure (e.g., Critical / High / Moderate / Low) is typical. Each tier must define the diligence depth, monitoring cadence, contract clauses, and approval authority it triggers.
- **The reassessment cadence.** Tiers are not permanent. When a vendor's role expands, the tier escalates; when it contracts, the tier can be downgraded. The methodology must specify when reassessment happens.
- **The ownership.** A named role authors the tiering, with a second named role approving. Un-owned tier assignments are a structural finding.

The auditor tests the methodology document, then samples tier assignments and reperforms. A vendor the organisation has tiered as "Low" that actually processes sensitive customer data on behalf of the organisation is a *tiering-evidence* finding — the methodology is sound but the application failed. A vendor the organisation has tiered as "Low" because the methodology does not consider training-data-exposure risk is a *methodology* finding.

## The vendor inventory as the sampling frame

An auditor cannot sample what the organisation cannot list. The third fieldwork step is the **vendor inventory reperformance**.

The auditor requests the complete AI-vendor inventory. Expected fields per row: vendor identity, product / API consumed, activity category, tier, data classes processed, contract reference, inherent-risk score, residual-risk score, last due-diligence date, next reassessment due, named relationship owner, named control owner, incident count year-to-date.

The inventory is reperformed by three independent sweeps:

1. **Accounts-payable sweep.** Pull AP records for the look-back period, filter for keywords matching AI vendors and known AI-vendor providers, reconcile against the inventory. Vendors appearing in AP but not in the inventory are *shadow vendors* — a known failure mode for the AI book, where a team procures an API via credit card or a monthly cloud bill.
2. **Identity-and-access sweep.** Pull OAuth-grant logs, API-key-issuance logs, SSO application lists, cloud-bill subscription lists, Hugging Face / W&B / cloud-provider-model-garden access logs. Compare against the inventory. A Hugging Face token granted to a production service for a model not in the inventory is a shadow-model finding.
3. **Engineering-and-product sweep.** Interview a sample of engineering and product leads; ask for the AI dependencies in their stack by product line. Compare to the inventory. Out-of-inventory dependencies are shadow-vendor findings and also raise an oversight-and-accountability finding against the inventory maintainer.

Shadow AI is the most common audit-time finding in the third-party AI book and often the single biggest reason an organisation's SR 23-4 claim fails. The auditor's three-sweep reperformance surfaces it reliably.

## Walking an engagement — the per-vendor fieldwork pattern

Having tested methodology and inventory, the auditor samples vendors stratified by tier and walks each engagement end-to-end. Minimum sample: all Critical-tier vendors, a stratified sample of High, a convenience sample of Moderate, one or two Low to cover the floor.

For each sampled vendor the auditor fills in the **engagement walk workpaper**. The workpaper has one row per SR 23-4 phase and one column per evidence artefact.

### Planning phase evidence

- Business case / proposed-use memo.
- Inherent-risk assessment at the activity level (what breaks if this fails?).
- Tier assignment and the methodology application that produced it.
- Approval authority who signed off.
- For AI-specific use: an alignment check — does this use fall under an AIMS-defined use category (ISO/IEC 42001 clause 4.2 "needs and expectations of interested parties" and clause 8 "operation"); is the use in the AI inventory the ISO/IEC 42005 impact-assessment work produced?

A planning phase that starts after procurement has committed is a finding against the governance structure — procurement locked the organisation in before risk sign-off could meaningfully refuse.

### Due-diligence evidence

The auditor does not read the diligence folder; the auditor *tests* it. For each tier, SR 23-4 specifies a diligence depth. The auditor reperforms by picking a diligence claim and demanding corroborating evidence.

- *Claim: "Vendor has SOC 2 Type II and ISO 27001."* Test: pull the report; check it's current, not expired; check scope (chapter 3 is the deep dive); check carve-outs; check bridge-letter coverage.
- *Claim: "Vendor financial health is stable."* Test: financial statements, D&B rating, press coverage. For a startup vendor, this often matters more than for enterprise incumbents — the exit-plan test (below) presumes vendor failure modes.
- *Claim: "Vendor has incident-reporting processes aligned with ours."* Test: vendor's incident-response plan document, prior-period incident disclosures, SLA for notification.
- *Claim: "Vendor does not use customer data to train its model."* Test: the DPA / AI-addendum clause, the vendor's published data-use policy, the API's per-request opt-out flag configuration, evidence the configuration is actually set in production.
- *Claim: "Vendor subcontractors are vetted."* Test: vendor's subcontractor list, the clauses binding subcontractors to equivalent controls, the audit-cascade clause.
- *AI-specific claim: "Vendor shares model-card and evaluation data."* Test: the model-card artefact (per chapter 1 provenance test), the evaluation data, the red-team summary, the published safety-evaluation results. Chapter 5 extends this for GPAI-provider documentation to downstream deployers.

A diligence folder with claims unsupported by corroborating evidence is a "paper diligence" finding — the shape SR 23-4 was written to prevent.

### Contract evidence

The auditor reads the contract, but the test is *reperformance* of the clauses that encode controls. Named clauses to find and test:

- **Right to audit.** Is it present? Has it been exercised in the current period if the tier calls for it? Has it ever been exercised? A right-to-audit clause never exercised in a five-year relationship on a Critical vendor is a monitoring finding.
- **Data-use restrictions.** Does the vendor's AI addendum restrict use of customer data for training / improvement / evaluation? What exceptions does it carve? Are the exceptions technically enforced (e.g., per-request `training: false` flag)?
- **Model-version pinning and change-notification.** Does the contract pin the vendor to a specific model version or model family, with change notification? Vendor-side model-swap (silent GPT-X → GPT-X+1 rolls) is a change-management risk SR 23-4 reaches through the "change management" / "ongoing monitoring" factors.
- **Incident-notification SLA.** How quickly does the vendor commit to notifying the organisation of security incidents affecting the organisation's data? Of AI-specific incidents (jailbreak publication, evaluation failures, model recalls)? The SLA must be short enough to let the organisation meet its own regulatory clocks (EU AI Act Article 73, HIPAA, state breach-notification laws).
- **Subprocessors.** List maintained, with change-notification lead time.
- **Termination for cause and for convenience.** Terms, notice period, data-return / destruction obligations, transition-assistance obligations.
- **Indemnification and insurance.** Who bears liability for an AI-harm event? Is the vendor's cyber / tech-E&O policy adequate? Is there AI-specific coverage (emerging market)?
- **Confidentiality and IP ownership.** Who owns prompts, completions, fine-tunes, derived artefacts? The answer differs across vendors and matters at exit.
- **Jurisdiction, governing law, dispute resolution.** Standard commercial but sometimes materially relevant for cross-border data-flow and AI Act scope questions.

Contract reperformance is read-only on the executed document; the test is whether the organisation can *produce* the executed version (not a draft), whether it's signed by authorised signatories on both sides, and whether amendments (which are frequent in AI vendor relationships) are tracked and consolidated.

### Ongoing-monitoring evidence

SR 23-4 insists monitoring is risk-proportionate and continuous. The auditor's test is whether monitoring produces management action, not whether monitoring produces dashboards.

- **Performance monitoring.** SLA-tracking against the contract — availability, error rate, latency, accuracy if measurable. Evidence that SLA breaches trigger the vendor's remediation duty under the contract.
- **Control-environment monitoring.** New-period SOC 2 / ISO reports pulled and reviewed when published; bridge letters obtained for coverage gaps; the review is documented in a memo, not just filed.
- **Incident monitoring.** Vendor-notified incidents in the period, classified against the organisation's incident taxonomy, correlated to any customer-impact events, routed through the organisation's own incident process (`mod-108` chapter 3 shape).
- **Public-signal monitoring.** News coverage, security-researcher disclosures, academic papers that bear on the vendor's model safety (e.g., a published jailbreak for a specific vendor model; a published evaluation of a vendor's safety claims that undermines them).
- **Reassessment cadence.** Due-diligence refresh per the tier's declared cadence — at least annual for Critical vendors; evidence the refresh happened and that it moved the risk-register entry (or documented why it did not).
- **Subcontractor-change monitoring.** Vendor subprocessor-list changes acknowledged and assessed; a new critical subprocessor can escalate the tier.

Monitoring-without-action is a chronic failure mode — vendor reports arrive, are filed, and never influence the risk register or the audit-committee reporting. The auditor's test closes this loop: for one monitoring event per vendor, show the chain from signal to management decision.

### Exit-plan evidence

This is the phase organisations most often fail. SR 23-4 is explicit that exit planning begins at onboarding. The auditor tests:

- **Exit plan exists at onboarding.** Not a document written when the relationship goes sour — one written when the contract is signed.
- **Exit plan covers scenarios.** Voluntary termination, performance-triggered termination, vendor insolvency, security breach, regulatory enforcement, strategic shift.
- **Exit plan names an alternate.** Concentration risk (below) demands at least one named alternative for Critical AI vendors — an alternate API provider, an alternate vendor model, a documented fallback (rule-based system, deferred-to-human path, downgraded-service mode).
- **Data return / destruction.** Mechanism and schedule; attestation form; keys for encrypted-at-rest data retained or destroyed per schedule.
- **Transition plan.** Timing, team ownership, customer-communications plan, operational-continuity plan, financial model for the transition.

For AI vendors specifically the exit plan must also cover **prompt / fine-tune / derivative-artefact portability**. Fine-tunes done on a vendor's base model are not portable to a different vendor without re-training; the exit plan must declare the cost / timeline / data for re-training on an alternate.

## Concentration risk

SR 23-4 names concentration risk as a specific factor — too much reliance on one vendor across multiple critical activities. The AI book's concentration pattern is distinctive:

- One foundation-model provider underpins multiple internal products.
- One cloud provider underpins both the vendor-API usage and the organisation's own infrastructure.
- One embedding-model provider underpins multiple retrieval systems.
- One guardrail / moderation vendor sits in front of multiple inference paths.

The auditor's concentration-risk reperformance:

- **Count distinct dependencies.** From the vendor inventory, compute the number of critical activities that depend on each vendor. One vendor backing five critical activities is a concentration posture that must be explicitly accepted.
- **Correlation of failures.** Identify dependencies that correlate — a GPU-provider outage can simultaneously disable the primary and a putative "alternate" that runs on the same cloud. The exit plan must consider correlation, not just presence of alternates.
- **Board-level visibility.** The organisation's concentration posture is reported to the board (or an appropriate committee) for AI vendors above the materiality threshold. Where it is not, finding against the oversight-and-accountability requirement.

A single-cloud AI book is permissible under SR 23-4, but it must be explicitly chosen, documented, communicated upward, and reflected in risk-register residual-risk scoring.

## Cross-cutting: oversight, accountability, documentation, reporting

The final SR-23-4 shape the auditor tests is cross-cutting:

- **Board / senior management oversight.** Is the AI vendor book visible to the board? Is the reporting cadence proportional to the materiality? Are the critical vendors named in the reports, not aggregated into a "third parties" footnote?
- **Named accountability.** Each vendor has a named relationship owner (business), control owner (risk), and operations owner (engineering). All three must appear in the inventory. Un-owned vendors (common for shadow-sourced) are findings.
- **Documentation retention.** Diligence files, contracts, monitoring reports, incident records, and termination records are retained through the relationship's life plus the longer of the contract's retention clause and the organisation's own records policy.
- **Independent review.** The third-party-risk program itself is independently reviewed — this audit, or an equivalent one. The auditor records the function doing the review and whether it is independent of the second-line that operates the program (`mod-101` on three-lines structure).

## The engagement-walk workpaper shape

The auditor's deliverable for each sampled vendor is a one-vendor workpaper. The workpaper is structured so a reviewing partner can read without needing the auditor's commentary:

- **Vendor identity block** — name, API / product, activity, tier, contract reference, relationship-owner identity, assessment period.
- **Phase-by-phase table** — one row per SR 23-4 phase; three columns per row: *evidence sampled*, *status (complete / partial / absent / inconsistent)*, *pointer to the evidence*.
- **Clause-level contract test table** — the clauses enumerated above; present / absent; where present, operational-evidence pointer.
- **Finding candidates block** — one row per finding; columns: finding ID, title, SR 23-4 phase / factor, severity, evidence pointer, management-response-requested shape.
- **Residual-risk summary** — residual-risk score per the organisation's methodology, change from prior period, drivers.
- **Open items** — items the auditor could not resolve in the period (`<!-- needs-research: ... -->` markers inline, consolidated here).

## Common failure modes

- **Shadow AI book.** Vendors live in AP / in SSO / in engineering stacks that never reached the inventory.
- **Tier-applied-incorrectly.** Tiering methodology sound; application lazy — a Critical vendor tagged "Moderate" because nobody remembered to escalate at the activity change.
- **Paper diligence.** Diligence folder full of vendor-authored claims with no independent corroboration.
- **Right-to-audit never exercised.** The clause is present; the audit has never happened; the organisation has no basis for believing the vendor's control environment is what the vendor says it is.
- **No training-data-use term.** The contract is silent on whether the vendor trains on customer data; the vendor's public ToS controls by default; the ToS may be revised unilaterally.
- **Model-change surprise.** Vendor silently promotes a new model version; the organisation's regression evaluation is caught flat-footed; the risk register was never updated.
- **Monitoring-without-action.** SOC 2 renewals filed but never read; incident reports logged but never triaged; the vendor's control environment degrades without the organisation noticing.
- **Exit plan absent or stale.** The exit plan is a cover memo from onboarding, two years out of date.
- **Concentration posture invisible.** The organisation runs four critical AI paths through one foundation-model provider; the board does not know.
- **Cross-reliance on another vendor's assurance.** The organisation relies on the API provider's SOC 2 for a sub-processor whose risk the SOC 2 does not actually cover (chapter 3 deep-dive).

## Interfaces to adjacent chapters

- **Chapter 1 (provenance)** feeds the AI-specific-diligence rows under phase 2: vendor-shared model-card, datasheet, evaluation data, SLSA level, ML-BOM.
- **Chapter 3 (assurance artifacts)** extends phase 2's "SOC 2 / ISO / 42001" row — scope, carve-outs, user-entity controls, bridge letters.
- **Chapter 4 (malicious artefacts)** extends phase 2 for open-weight vendors — what scans the organisation ran against vendor-distributed artefacts.
- **Chapter 5 (GPAI deployer obligations)** extends phase 2 and phase 4 for GPAI model usage — the specific EU AI Act Articles 51–55 obligations and the Code of Practice.
- **Chapter 6 (signing / registry gates)** is the specific technical control the auditor tests at phase 2 (diligence that the vendor signs its artefacts) and phase 4 (ongoing monitoring that signatures continue to validate).
- **Chapter 7 (OMB)** is the US-federal-agency / contractor overlay — M-24-18, M-25-22, M-25-21 add acquisition-specific obligations on top of the SR 23-4 structure.
- **`mod-108` chapter 3 (incident response)** picks up the incident-notification clock on the organisation's side after the vendor-initiated notification arrives.

## Summary

- SR 23-4 (the 2023 Interagency Guidance) is the US-banking-authored but globally-influential vendor-risk criterion; the AI book maps cleanly onto its five-phase lifecycle plus cross-cutting factors.
- Risk tiering is the audit's hinge — the methodology must be sound and the application must be reperformed, with AI-specific factors (autonomy, training-data exposure, model-change frequency, cross-border flow) built in.
- The vendor inventory is reperformed by three independent sweeps (AP, identity-and-access, engineering) because the auditor cannot sample what the inventory does not list; shadow-AI findings dominate this reperformance.
- Each sampled vendor is walked end-to-end: planning, due diligence, contract, ongoing monitoring, termination; the test is evidence that each phase produces action, not evidence that artefacts exist.
- Contract reperformance is clause-by-clause, with attention to AI-specific terms — training-data use, model-version pinning, incident SLAs, subprocessor-change notice, prompt / fine-tune / derivative-artefact ownership.
- Concentration risk is a distinctive AI-book pattern: foundation-model, cloud, embeddings, guardrail concentrations must be surfaced, correlated, and communicated upward.
- Chapter 3 picks up the assurance-artifact deep dive; chapter 5 picks up the GPAI-specific overlay; chapter 7 picks up the OMB-federal overlay.
