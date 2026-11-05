# Integrating with GRC-for-AI Platforms

## Motivation

The continuous-audit operating model from chapter 2 assumes the audit function can read risk and control data from somewhere. In most organisations, that somewhere is an enterprise GRC platform — Workiva, AuditBoard, ServiceNow GRC, MetricStream — now joined by a growing category of AI-governance-specific platforms (Credo AI, Holistic AI, ModelOp, Monitaur, ServiceNow AI Control Tower, IBM watsonx.governance, Fairly AI, Enzai, Trustible). These platforms promise an enterprise system of record for AI risk, controls, policies, assessments, and attestations.

For the audit function, the platforms are both a rich evidence source and a political one. They are implemented by the second line (risk / compliance) or by the first line (product / engineering); they are sometimes implemented by the audit function itself, which creates independence questions. Their data is only as good as the organisation's willingness to keep the platform current, and auditors who assume the platform is ground truth without reperformance get burned.

This chapter describes the GRC-for-AI landscape as the AI auditor sees it in 2026, the common data models, the integration patterns, the audit tests the platform enables, and the failure modes to anticipate.

## Landscape as of 2026

The platforms the AI audit function is likely to encounter fall into roughly four categories, with overlap:

### Enterprise GRC with AI modules

- **Workiva.** Public-reporting and controlled-document platform; AI-governance workflow via its platform extensibility; often used for AI-related financial-reporting disclosures.
- **AuditBoard.** Internal-audit, SOX, risk-management platform; AI-governance workflow via its RiskOversight / CrossComply modules.
- **ServiceNow AI Control Tower.** ServiceNow's AI-specific module, sitting on the Now Platform, that supports AI inventory, risk assessment, policy, control testing, and third-party risk for AI systems.<!-- needs-research: confirm ServiceNow AI Control Tower's current product boundaries and module names at reading time; the product has expanded quickly since launch. -->
- **IBM watsonx.governance.** IBM's AI-governance platform; integrates with watsonx.ai but also governs third-party models; model-lifecycle, model-card, and risk-assessment workflows.
- **Diligent / Riskonnect / MetricStream / OneTrust / Hyperproof.** Broader GRC platforms with AI-governance extensions; coverage varies.

### AI-governance-specific platforms

- **Credo AI.** AI governance platform emphasising use-case intake, risk classification, policy-as-code, and ongoing assessment aligned to NIST AI RMF and EU AI Act.
- **Holistic AI.** AI governance / audit platform with inventory, risk assessment, bias audit, and third-party assurance workflows.
- **ModelOp.** AI-model operations platform with governance, inventory, model-lifecycle, and monitoring features suited to banks and insurers with heavy SR 11-7 MRM obligations.
- **Monitaur.** AI assurance platform emphasising model monitoring, governance, and audit-ready evidence.
- **Fairly AI.** AI governance platform emphasising the EU AI Act lifecycle, use-case inventory, and conformity-assessment workflow.
- **Enzai.** EU-origin AI governance platform emphasising the AI Act compliance workflow for providers and deployers.
- **Trustible.** AI governance platform emphasising policy, risk assessment, and documentation.

### Evaluation / safety / observability platforms with governance adjacency

- Observability platforms (Arize, Fiddler, WhyLabs) are not GRC platforms but produce the drift and performance data a GRC-for-AI platform consumes.
- Red-team and evaluation platforms (Robust Intelligence, HiddenLayer, Patronus AI, Haize Labs, Prompt Security, Lakera, Protect AI) produce evaluation artefacts.
- Model registries (MLflow, SageMaker, Vertex, Databricks Unity Catalog) hold model provenance.

### Internal-build platforms

Many large organisations have built their own AI governance system rather than buying one. The audit function treats an internal-build as a GRC-for-AI platform for integration purposes and audits the build itself for completeness and controls.

The platform market is actively consolidating and extending; what the auditor needs to know is the *data model and workflow coverage* of the platform the organisation uses, not the vendor's marketing taxonomy.

## The common data model

Across platforms, the AI auditor can expect to find some version of each of these objects. Names differ; concepts converge.

- **AI system / use-case inventory.** Registered AI systems with purpose, risk classification, owner, deployment state, lifecycle status. Often the authoritative source for scoping an audit.
- **Risk register entries.** Identified risks per system, with likelihood / impact / treatment / owner.
- **Control catalogue.** Controls the organisation has defined — policy, process, technical, monitoring — with mapping to frameworks (NIST AI RMF, ISO/IEC 42001, EU AI Act, SR 11-7).
- **Policy register.** Policies, standards, procedures, with ownership, approval status, review cycle.
- **Assessment / questionnaire records.** Completed self-assessments, impact assessments, fundamental-rights impact assessments, DPIAs, model-risk assessments.
- **Control-test records.** Evidence that controls have been tested and the result.
- **Model lifecycle / lineage.** Where the platform integrates with the model registry; training data, training run, eval, approval, deployment.
- **Vendor / third-party risk.** AI-vendor assessments, attestation collection, continuous monitoring (`mod-109`).
- **Incident register.** AI-related incidents and near-misses (`mod-108`).
- **Findings and corrective actions.** Audit findings (where the platform is also used by the audit function), management responses, CAP tracking, closure (`mod-111`).
- **Crosswalks.** Mapping of controls to multiple frameworks so a single control satisfies several criteria.
- **Attestation / signature records.** Role sign-offs, policy acknowledgements, release approvals.

## Integration patterns

### Read-only API extract

The most common audit integration is a read-only pull from the platform's API or scheduled export, feeding the audit evidence store. The audit team gets the current state of inventory, risk register, control tests, and assessment records on a cadence (daily / hourly) and runs the CCM rules from chapter 2 against the extract.

Keys:

- Named service account with least-privilege read scope.
- API authentication with rotation.
- Rate limits respected (platforms may throttle).
- Export schema version pinned and monitored for change (platform upgrades silently change schemas).
- Reconciliation checks — row counts, timestamp consistency — to detect export failures.

### Event subscription

Where the platform supports event notification (webhook, event bus, pub/sub), the audit function subscribes to relevant events (a new system registered, a control-test failure, an incident declared). This reduces the latency between the event and the audit team's awareness.

### Shared observability

Some platforms expose their data through shared dashboards or shared workspaces. The audit function reads but does not write in the shared space; writes come later through the audit's own channel.

### Writing to the platform — with care

Where the audit function writes to the GRC-for-AI platform (adding findings, closing items, attaching reports), the write access is tightly scoped and separated from the audit's evidence collection. Audit findings should be added to the platform's finding register but in a way that preserves the audit function's independent record — the primary audit record stays in the audit function's system, with the platform entry as a mirror for enterprise visibility.

### Integration with the model registry

Where the GRC-for-AI platform is not tightly integrated with the model registry, the audit function runs its own reconciliation between the two. Models in the registry that are not in the AI inventory, or vice versa, are an exception the audit team investigates — commonly either shadow deployments or lifecycle-event races.

## What the platform makes auditable

With a well-populated GRC-for-AI platform, the audit function can run tests that would otherwise require manual document collection:

- **Inventory completeness.** Compare the AI inventory against production deployments (by cross-referencing deployment data from the MLOps platform, the model registry, or discovery scans). Gaps are findings.
- **Risk-assessment timeliness.** Each system's last impact assessment is within the required window; overdue systems are findings.
- **Control test coverage.** Each control has test evidence within the required frequency; untested or overdue controls are findings.
- **Crosswalk coverage.** Critical criteria (ISO/IEC 42001 clauses, EU AI Act articles) have at least one mapped control; uncovered criteria are findings.
- **Policy currency.** Policies are reviewed within the required cycle; overdue reviews are findings.
- **Attestation chain.** Role sign-offs exist for every release of an in-scope system; missing sign-offs are findings.
- **Incident register completeness.** Every incident flagged elsewhere (SIEM, support tickets) has a corresponding register entry; gaps are findings.

A CCM rule can encode each of these.

## What the platform cannot do for the auditor

A platform's data is a *representation* of the organisation's AI governance, not the governance itself. The auditor still needs to:

- **Reperform.** The platform says the control was tested; the auditor samples and reperforms the test. "The platform says so" is not evidence; the platform is a representation layer.
- **Inspect source systems.** Model inventory in the platform is tested against what is actually running in production. The platform is not the system of record for deployment state; the production environment is.
- **Interview.** Ownership records in the platform are tested against what the owner actually does when asked.
- **Observe.** Where the control requires manual activity (SIA review, red-team session, incident war-room), the auditor observes the activity as well as reads the record.

The platform is a very useful *efficiency* layer — it saves the auditor from reconstructing the state manually — but not a *sufficiency* layer. The IIA Standards and GAGAS evidence sufficiency requirements still apply.

## Independence and the audit function's role in the platform

Three independence postures to think through:

- **Audit is a consumer.** The audit function reads the platform; management owns the platform. This is the cleanest posture and the one that preserves independence.
- **Audit is a co-administrator.** The audit function has write access to platform configuration. Preserves independence only if the write access is constrained to audit-owned areas (audit findings, audit assessments) and does not extend to management's control catalogue or test records.
- **Audit implemented the platform.** The audit function led the platform selection and implementation. The Standards permit consultative work by internal audit, but a function that implemented the platform should not later provide assurance over that platform without a rotation / cooling-off period and disclosure (see `mod-101`).

Where the organisation is just standing up its AI governance and uses the audit function's AI expertise in the build, the CAE decides the rotation posture in advance; otherwise the audit function has disabled its own future assurance scope.

## Failure modes

- **Stale inventory.** The AI inventory becomes a reporting artefact that nobody updates; the platform shows 40 systems while 120 are running. The audit function's reconciliation to the model registry and deployment data is the detection.
- **Vendor-managed-service drift.** The platform vendor updates the data model or API; the audit function's extraction silently breaks. Pipeline-health monitoring (chapter 2) catches this.
- **Framework-mapping rot.** Crosswalks drift as frameworks update (NIST AI RMF revisions, EU AI Act implementing acts, ISO/IEC 42001 amendments). The audit function reviews crosswalks on each framework update.
- **Over-trust.** The audit function stops reperforming because "the platform's control testing is already there." Over-trust on the platform is the fastest path to a findings-slate that does not survive external review.
- **Framework-conflating crosswalks.** A single control mapped as satisfying both ISO/IEC 42001 §8.3 and EU AI Act Article 27 when the two requirements have different scope and different evidence expectations. The auditor tests the control against each criterion separately.
- **Workflow bypass.** The platform has a workflow for release approval; teams generate releases outside the workflow because the workflow is slow. The audit function samples recent releases against the platform's workflow record and reconciles.
- **Shadow systems.** Teams that know their systems will be subject to the governance workflow sometimes avoid registering them. Discovery (traffic analysis, model-registry scans, SaaS-use scans) is the detection.
- **Role concentration.** The same person owns the control, tests the control, and approves the control. The platform may permit this; the audit function catches it in a segregation-of-duties review.

## Evaluating a platform's fitness for the audit's purposes

Where the organisation is selecting or evaluating a GRC-for-AI platform (and the audit function is consulted), the lead can assess fitness against:

- **Data-model coverage** for the objects the audit function needs.
- **API maturity** — read access, event subscriptions, export formats, schema stability.
- **Audit trail** — the platform's own audit log of configuration changes, record edits, and user actions.
- **Framework mappings** maintained by the vendor — depth and freshness.
- **Attestation / SOC reports** — SOC 2 Type II on the platform itself; ISO/IEC 27001; where applicable, ISO/IEC 42001 on the vendor's AIMS.
- **Independence support** — can the platform preserve the audit function's independent record, or does it force the audit's findings to live only inside management's system.
- **Interoperability** — integrations with MLOps platforms, model registries, observability platforms, SIEM, document management.

The audit function's input is advisory; the selection decision belongs to the business.

## A note on open-source and standards-based alternatives

Not every organisation buys a platform. The audit function may encounter — and support — an open-source or standards-based approach:

- **OSCAL** (Open Security Controls Assessment Language) for machine-readable control catalogues, SSPs, APs, ARs, POA&Ms (see chapter 4 and `mod-111` chapter 7). Federal agencies and some private sector organisations encode their AI controls in OSCAL.
- **Internal tooling** on top of a document-management system, a data warehouse, and a workflow tool. More labour-intensive but more auditable because the function owns the stack.
- **Spreadsheet-based** registers. Common in smaller organisations; auditable only to the extent they are controlled; findings here are often "the register is the control environment."

The chapter-4 tooling layer describes how the audit function builds its own tooling where the organisation's platform choice does not cover the need.

## Summary

- The GRC-for-AI platform market in 2026 spans enterprise GRC with AI modules, AI-governance-specific platforms, adjacent evaluation / observability / registry tools, and internal builds; what matters to the auditor is the data model and workflow coverage, not the vendor.
- The common data model includes inventory, risk register, control catalogue, policy register, assessments, control tests, model lifecycle, vendor risk, incidents, findings, crosswalks, and attestations; the AI auditor maps the local platform to this model.
- Integration patterns — read-only extract, event subscription, shared observability, limited writes — feed the continuous-audit evidence store from chapter 2.
- The platform makes many tests efficient (inventory completeness, assessment timeliness, control-test coverage, crosswalk coverage, policy currency, attestation chain, incident register completeness) but the auditor still reperforms, inspects, interviews, and observes to meet sufficiency requirements.
- Independence postures range from consumer to co-administrator to implementer; the audit function preserves future assurance scope by setting rotation and cooling-off in advance when it implements the platform.
- Common failure modes — stale inventory, vendor drift, crosswalk rot, over-trust, workflow bypass, shadow systems, role concentration — are the audit function's recurring work.
- Where the organisation uses OSCAL or an internal build, the audit function integrates on the same patterns and builds its own tooling (chapter 4) around the platform rather than around the vendor.
