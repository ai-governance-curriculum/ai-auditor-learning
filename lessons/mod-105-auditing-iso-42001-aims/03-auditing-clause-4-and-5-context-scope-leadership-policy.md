# Auditing Clauses 4 and 5 — Context, AIMS Scope, Leadership, AI Policy, Roles

## Motivation

Clauses 4 and 5 sit at the top of the AIMS. **Clause 4** establishes what the AIMS is about and where its boundary is — context, interested parties, and scope. **Clause 5** establishes who owns it — top-management commitment, the AI policy, and the roles-and-responsibilities map. An auditor who gets these wrong at Stage-1 cannot run a clean Stage-2: the Stage-2 sampling frame is drawn from the clause 4.3 scope; the Stage-2 criteria for "legal and regulatory requirements" come from clause 4.1 and 4.2; the Stage-2 look-up for who should be accountable for each finding comes from the clause 5.3 role catalogue.

Clauses 4 and 5 are also where the most common first-year defects sit: generic context statements borrowed from ISO 27001, scope documents that do not match the AI system inventory, AI policies missing one or two of the clause 5.2 required commitments, and role charts that look like a RACI but have no owner assigned for the controls the Annex A SoA actually requires.

## Clause 4 — audit mechanics

### 4.1 — External and internal issues

**Requirement.** The organisation shall determine external and internal issues that are relevant to its purpose and that affect its ability to achieve the intended outcome(s) of its AIMS.

**Audit test.** Request the context-analysis document. Look for AI-specific entries (not just a re-used ISO 27001 context statement with "AI" appended). External issues the document should name, depending on the organisation's footprint: EU AI Act and its sector-specific implementing acts; Colorado SB24-205 and equivalent US state laws for deployers; NYC Local Law 144 for employment tools; applicable sector guidance (SR 11-7, FDA GMLP, NAIC Model Bulletin, OMB M-24-10 / M-25-21 for federal agencies); applicable standards (ISO/IEC 42001 itself, ISO/IEC 23894, ISO/IEC 42005); the organisation's third-party AI dependencies. Internal issues the document should name: AI maturity (first cycle vs. multi-cycle AIMS), data posture, talent availability, legacy system coupling, and the organisation's AI strategy. Verify a cadence of review exists and has been performed at least once.

**Common defects.** Generic context re-used across ISO certifications; external issues list that excludes the regulations the organisation is actually subject to; no evidence of periodic review. All typically minor; a complete absence of context analysis is major.

### 4.2 — Interested parties

**Requirement.** Identify interested parties relevant to the AIMS and the relevant requirements of those interested parties.

**Audit test.** Request the interested-parties register. For AIMS, expected entries include: regulators (EU AI Office, national competent authorities, sector regulators), impacted groups (end users, subjects of AI decisions, affected communities, worker representatives in employment-decision contexts), workforce (AI engineering, risk, compliance, operations), suppliers and vendors (model providers, data providers, cloud providers, red-team firms, third-party evaluators), customers, and shareholders. Check that each entry has the *requirements* the party holds against the AIMS, not just a name.

**Common defects.** Only customers and regulators listed; impacted groups missing; vendors listed without the AIMS-relevant requirements (data-processing terms, model-provider terms, DPAs for personal data).

### 4.3 — Determining the scope of the AIMS

**Requirement.** The organisation shall determine the boundaries and applicability of the AIMS to establish its scope. The scope shall be available as documented information.

**Audit test.** Request the AIMS scope document. The scope must name the AI systems in and out of scope with a defensible inclusion rule, the business units and legal entities in scope, the geographies, the processes, and any exclusions with rationale. Reconcile the scope against the AI system inventory. Walk a short list of the organisation's AI uses that an interested party could point to externally (press releases, product pages, careers listings mentioning AI roles, SEC 10-K AI disclosures) and verify each is correctly treated (in scope or defensibly out).

**Reconciliation procedure — the single most important Stage-1 workpaper:**

1. Obtain the AIMS scope document (`SCOPE.md` or equivalent).
2. Obtain the AI system inventory that feeds the SoA and risk register.
3. Obtain an external corroboration set: product-landing pages that mention AI, SEC/annual-report AI disclosures, the careers page (job postings often mention AI systems the auditor should ask about), vendor-management lists, help-desk ticket categories if an AI-support flag exists.
4. Build a reconciliation table: for each row, a system name, inventory status (yes/no), scope status (yes/no), and external-corroboration status (yes/no).
5. Expect every "yes" in external corroboration to match "yes" in both inventory and scope. Mismatches are findings. Missing inventory entries are the most common major-grade finding in this clause.

**Common defects.** Scope document silent on the inclusion rule (so the client can later argue any system in or out); scope misaligned with the AI system inventory; GPAI usage ("our staff use ChatGPT via the enterprise plan") not addressed with either "in scope with controls" or "out of scope with policy prohibition".

### 4.4 — Artificial intelligence management system

**Requirement.** The organisation shall establish, implement, maintain, and continually improve an AIMS, including the processes needed and their interactions, in accordance with the requirements of this document.

**Audit test.** 4.4 is often satisfied implicitly by the rest of the AIMS being in place; a finding specifically against 4.4 usually accompanies a broader AIMS defect. The auditor should still inspect the AIMS process map (if the organisation has one) or sequence-of-processes document to confirm the AIMS is conceived as a process-based system, not as a collection of documents.

## Clause 5 — audit mechanics

### 5.1 — Leadership and commitment

**Requirement.** Top management shall demonstrate leadership and commitment with respect to the AIMS by: taking accountability; ensuring the policy and objectives are established and compatible with the strategic direction; ensuring the integration of AIMS requirements into business processes; ensuring resources are available; communicating the importance; ensuring the AIMS achieves its intended outcomes; directing and supporting persons to contribute; promoting continual improvement; supporting other relevant management roles.

**Audit test.** 5.1 is tested through interviews and corroborating documentary evidence, not by the policy signature alone. Interview a top-management representative (CRO, CTO, CEO's delegate, Chief AI Officer where one exists) with specific questions:

- What are the AIMS's intended outcomes, in your words?
- How does the AIMS budget sit relative to other risk-management budgets in your organisation?
- What is the most recent decision top management took about the AIMS?
- Which AIMS objective are you personally tracking this quarter?
- When was the last management review you attended and what came out of it?

Corroborate with: budget evidence, board-pack extracts on AI topics, top-management attendance at the last management review (clause 9.3), the last AI-related decision that top management made and documented.

**Common defects.** Interview answers that bounce the question down ("the AI risk committee handles that"); no documented top-management AIMS decision in the audit period; top management absent from the management review of record.

### 5.2 — AI policy

**Requirement.** Top management shall establish an AI policy that: (a) is appropriate to the purpose of the organisation; (b) provides a framework for setting AI objectives; (c) includes a commitment to satisfy applicable requirements; (d) includes a commitment to continual improvement of the AIMS. The AI policy shall: (i) be available as documented information; (ii) be communicated within the organisation; (iii) be available to interested parties, as appropriate.

**Audit test — the policy completeness walk.** This is the auditor's most mechanical test in clause 5. Read the policy top-to-bottom with a checklist. For each required element, mark present / absent / weak:

```
Policy element                                          Present   Evidence location
---------------------------------------------------------------------------------
Statement of purpose, specific to the organisation       ?         Section ?
Framework for setting AI objectives                      ?         Section ?
Commitment to satisfy applicable requirements            ?         Section ?
   (incl. legal, regulatory, voluntary standards)
Commitment to continual improvement of the AIMS          ?         Section ?
Approval by top management (signature or minuted)        ?         Approval evidence
Documented and version controlled                        ?         Doc control ref
Communicated within the organisation                     ?         Communication record
Available to interested parties, as appropriate          ?         Publication location
```

A policy missing one required element is **minor**; missing more than one, or missing the commitment to applicable requirements in a regulated organisation, is **major**.

**Freshness test.** Check the policy's date and reconcile against the current legal landscape and current AI system inventory. A 2023 policy that commits to "our AI systems" without reference to the EU AI Act, in an organisation that places EU AI-Act high-risk systems on the EU market, is non-current and may be a 5.2(c) finding regardless of what the policy *says*.

**Communication evidence.** Communication to the workforce must be evidenced — intranet post with read-receipt or acknowledgement log, training completion records referencing the policy, supplier contract clauses incorporating the policy. Interview a sampled set of staff (across functions, not just the AI team) to confirm reach.

### 5.3 — Roles, responsibilities, and authorities

**Requirement.** Top management shall ensure that responsibilities and authorities for relevant roles are assigned and communicated. Specifically: for ensuring the AIMS conforms to the requirements of this document; for reporting on the performance of the AIMS to top management.

**Audit test.** Request the AIMS roles-and-responsibilities document, typically a RACI map or an org chart with AIMS roles annotated. Expected roles for an organisation at any scale:

- AIMS owner (typically the CRO or equivalent, with the Chief AI Officer where one exists reporting in).
- AI policy owner (often the same, sometimes a separate governance lead).
- AI risk management function (second line; corresponds to `ai-risk-engineer` L25 and `ai-governance-analyst` L15 in the broader role catalogue).
- Operational AI engineering (first line; model teams).
- AI release-assurance / second-line evaluation (`ai-evaluation-engineer` L35 and `model-evaluation-engineer` L30).
- Impact-assessment function (often the same as risk, sometimes a separate privacy-and-ethics function).
- Internal audit (third line; independent of the AIMS owner per clause 9.2).
- Top-management representative (reporting line into the board or board committee).

For each role: verify assignment (named person or named role in the document), verify authority (what decisions the role is authorised to make), verify communication (the person knows they hold the role; peers know). Reconcile the RACI against the Annex A SoA — every included control must have an owner in the role catalogue.

**Common defects.** AIMS owner is nominal (CRO on paper, but a product manager is doing the day-to-day work with no delegation document); internal audit reports to the AIMS owner (independence failure under clause 9.2 and IIA Standards 2024); Annex A controls without owners.

## AIMS scope reconciliation — a worked example

Consider a hypothetical SaaS organisation:

- The AIMS scope document names: "All AI-powered features in Product P in production in US and EU markets, as operated from our Dublin and Portland sites, during the audit period 2026-01-01 to 2026-12-31."
- The AI system inventory lists 14 systems.
- The careers page lists a "Prompt Engineer, Sales Enablement" role and a "Senior ML, Internal Tools" role.
- Public product pages mention "AI-powered insights", "AI assistant", and "AI-powered search".
- The vendor-management list includes an enterprise GPT subscription.

The reconciliation surfaces:

- The three "AI-powered" product features are in the inventory. Good.
- The "Sales Enablement" prompt engineer is working on a sales-copilot tool not in the inventory. The scope says "all AI-powered features in Product P" — is Sales Enablement in Product P? Check. If not, the scope is drawn narrowly; the auditor records the fact but does not raise a finding against ISO/IEC 42001 if the scope document is defensible. If the tool *is* part of Product P, it is an inventory gap and likely a major finding.
- The "Senior ML, Internal Tools" role suggests at least one internal AI system; is it in scope ("as operated from our sites") and in the inventory? If the scope wording captures internal systems and the inventory does not list it, finding.
- The enterprise GPT subscription is a usage of a GPAI system. Is enterprise-GPT usage in scope? If so, is there a control over it (acceptable-use policy, DLP, logging, model-registry entry for approved GPAI use cases)? If scope is silent, finding against 4.3.

This reconciliation drives the Stage-2 sampling frame. Chapter 10 picks it up for the Stage-2 plan.

## Communication-reach sampling for clause 5.2

If communication of the AI policy is a key assertion (it usually is in the first-cycle Stage-2), the audit uses a small sample to test reach. The sample is drawn across the workforce:

- 3 engineers on AI product teams.
- 2 engineers on non-AI product teams (the policy applies to the whole organisation).
- 2 non-engineering staff.
- 1 supplier representative (where supplier-contract communication is used).

Interview each: do they know the AI policy exists? Can they describe its main commitments? If 6 of 8 cannot, the communication is not effective; if the organisation has not operationalised the policy to the workforce, a minor is at least warranted and the pattern should be aggregated with other 5.2 evidence.

## Common failure modes

- **Context analysis re-used from ISO 27001.** Information-security context is a poor fit for AIMS context; re-use without adaptation is a finding against 4.1.
- **Scope document silent on GPAI / third-party AI use.** With GPAI increasingly embedded in product and workforce workflows, scope documents that do not name GPAI inclusion/exclusion are out of date.
- **Policy signed but not communicated.** A policy that lives in a document-management system but has no communication record fails 5.2(ii).
- **Role catalogue without reporting line.** Clause 5.3 requires a role for reporting AIMS performance to top management; a role catalogue silent on reporting is a minor.
- **Internal audit reporting to the AIMS owner.** Clause 9.2 independence breach; often grades major.
- **"CRO owns the AIMS" without delegation documentation.** If the CRO is the AIMS owner but a product manager is running it day-to-day, there must be a documented delegation.

## Summary

- Clause 4 fixes the AIMS boundary; the auditor's single most important Stage-1 workpaper is the reconciliation of the clause 4.3 scope document against the AI system inventory and external corroboration.
- Clause 5 fixes who owns the AIMS; 5.2 is tested by a policy-completeness walk against a fixed checklist, and 5.3 is tested by reconciling the role catalogue against the Annex A SoA so every included control has an owner.
- Common findings cluster around re-used ISO 27001 context, scope documents that miss GPAI or internal AI, policies missing one of the clause 5.2 required commitments, and role catalogues without reporting lines or internal-audit independence.
- The reconciliation workpapers produced in Stage-1 drive the Stage-2 sampling frame for the AI-system population; chapters 6 and 10 pick them up.
