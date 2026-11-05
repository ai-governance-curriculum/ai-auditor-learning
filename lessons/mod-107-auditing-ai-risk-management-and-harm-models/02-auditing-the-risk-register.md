# Auditing the Risk Register — Scoring, Appetite, Aggregation, and Sign-off

## Motivation

The risk register is the document the audit committee, the regulator, and the deploying organisation reach for first when they want to know what the risks are, how big they are, and who owns them. For the auditor the register is a *reperformance target*: every scored row is an assertion that `ai-risk-engineer` (L25) and the organisation's second-line functions have applied the organisation's own scoring methodology consistently, that the risk-appetite boundaries have been approved by the right governance audience, that portfolio-level aggregation is reproducible, and that sign-off routing has executed.

This chapter installs the discipline the auditor uses to test the register. It is not a re-authoring exercise; the register is authored by `ai-risk-engineer` to the organisation's own methodology (and to ISO/IEC 23894). The auditor tests whether the authored register holds together on its own terms.

The register audit comes *after* the harm-model audit (chapter 1) because an incomplete harm model is a register precondition finding — an unmitigated scope gap leaks through every register row.

## What a well-formed register row looks like

Before testing, the auditor should know what to expect. A register row with full governance hygiene carries:

- **Risk ID** — stable identifier.
- **Harm linkage** — one or more harm-model category references (chapter 1).
- **Risk statement** — "if … then … leading to …" shape.
- **Inherent risk score** — severity × likelihood × velocity (or the organisation's defined components), scored *before* any control.
- **Current controls** — pointer list into the control catalogue (feeds `mod-105` SoA, chapter 6).
- **Residual risk score** — the same components, scored with controls operating as designed.
- **Control-defeated risk score** — the same components, scored assuming the control fails or is bypassed. (This is the shape `ai-risk-engineer` L25 is expected to produce; many early-maturity registers omit it.)
- **Risk-treatment decision** — accept / mitigate / transfer / avoid.
- **Risk owner** — a named accountable executive (not a team).
- **Sign-off record** — approver identity, date, decision pointer.
- **Review cadence** — when the row is next re-scored.
- **Appetite status** — within appetite / breach / under escalation.
- **Monitoring linkage** — which metrics the operational monitor emits (feeds chapter 1's trace and `mod-108`).
- **Evidence pointer** — link to the evaluation (`eval` repository / Inspect run / HarmBench ASR), to prior-period test results, to vendor attestations, to the SoA reference.

A register row without one of the twelve fields above is a documentation finding. A register row that *has* all twelve but where any field is internally inconsistent with the others is a more severe finding — the row looks complete but is not.

## Scoring consistency — the three-column test

The core scoring test is comparing **inherent, residual, and control-defeated** scores across rows and against the methodology.

### Methodology check

The organisation should have a published scoring methodology (ISO/IEC 23894 Clause 6.4.3 is the normative reference) that fixes:

- The severity scale and the operationalisation of each level (what does "catastrophic" mean here in dollars, in affected individuals, in regulatory consequence).
- The likelihood scale and its time horizon (per deployment / per 1,000 interactions / annualised).
- The combination rule (matrix lookup, product, sum of logs, FAIR-style loss expectation).
- The scoring cadence and review trigger.
- The required inherent / residual / control-defeated framing.

A methodology that is implicit ("we use high / medium / low because everyone does") is itself a finding against ISO 23894 and NIST AI 100-1 "Measure 2.3."

### Consistency reperformance

For a sample of register rows the auditor reperforms the scoring:

1. **Score inherent.** Apply the organisation's methodology to the risk statement with controls disabled. Compare to the register's inherent score. A delta of more than one scale step without a documented rationale is a finding.
2. **Score residual with declared controls operating.** Apply the methodology with the current controls assumed to be operating as designed. Compare.
3. **Score control-defeated.** Apply the methodology assuming the controls are bypassed. This is the step most often absent in practice; the auditor should expect to open either an "absent control-defeated score" finding or a "control-defeated scored inconsistently" finding.
4. **Cross-row consistency.** Pull two rows with similar severity narratives and compare their severity scores. Rows with similar narrative but divergent scores are a methodology-application finding.

ISO 23894 and NIST AI 100-1 both make "repeatable" a requirement of a defensible risk-management function; the reperformance test is how the auditor evidences repeatability.

### Scoring inflation and deflation

Common failure patterns the auditor should recognise:

- **Severity inflation on new risks, deflation on inherited risks.** New risks get a high initial score to attract remediation funding; old risks stay low because down-scoring is politically easier than fresh escalation.
- **Residual = inherent minus a constant.** The organisation applies a reflexive "controls reduce by one step" even when the controls are weak or untested.
- **Control-defeated = residual.** The organisation does not actually model the bypass case; the control-defeated column is a copy.
- **Aggregation changes the per-row score.** The portfolio roll-up includes a correction factor that the per-row score does not reflect.

Each pattern lands as a specific finding against ISO 23894 / NIST 100-1 "Measure."

## Risk-appetite calibration

The risk appetite is the organisation's declared boundary: scores up to level X are tolerated; scores above X require mitigation; scores above Y require escalation to the board. The auditor's tests on appetite:

- **Appetite is written.** A verbal or inferred appetite fails the test; appetite is a document (often a risk-appetite statement signed by the board and referenced in the AI policy).
- **Appetite is calibrated by audience.** Different risks require different oversight (cybersecurity → CISO / audit committee; discrimination → compliance committee / regulator; frontier-safety-adjacent risks → RSPB / board AI committee). A single appetite threshold for all risks is a calibration finding.
- **Appetite is approved by the audience named in the governance charter.** The auditor traces the signature chain: the appetite statement should be signed by the body with authority per the AI-governance charter. A statement signed only by the risk function and not ratified by the named oversight body is a governance finding (and often the most consequential finding of the engagement).
- **Appetite thresholds appear in the register.** Each row's "within appetite / breach / escalation" field uses the signed thresholds; a row flagged "within appetite" with a score above the signed threshold is a register-to-appetite inconsistency.
- **Appetite applies to inherent OR residual (and the methodology specifies which).** Some organisations run appetite on inherent risk (requiring high residual-risk items to still be escalated even if the control is strong); others run it on residual. The methodology must say which; silent inconsistency is a finding.

### Signatory audit

The auditor pulls each approval signature in the appetite chain and confirms:

- The signatory had the authority at the time of signature (not retroactive promotion).
- The signature date predates the register rows the signature governs.
- The signatory is identified in the governance charter (`mod-101` chapter on governance), not just by job title.
- The signature is cryptographically evidenced where required (ISO/IEC 42001 management-review minutes), not merely an initial on a PDF.

A missing or weak signatory chain is the finding that carries forward into `mod-111` (management response).

## Portfolio aggregation reproducibility

The register is read at two levels: per-row (what is this specific risk?) and at the portfolio level (what is our overall posture?). The portfolio aggregation is a *reproducibility* target.

### What aggregation looks like

The organisation's aggregation methodology could be any of:

- **Heat-map count.** Number of risks in each colour cell of the severity-likelihood matrix.
- **Weighted sum.** Sum of (severity × likelihood × weight) across all residual-risk scores.
- **FAIR-style loss expectation.** Sum of expected single-loss expectancies across risks that are financially quantifiable; qualitative overlay for non-quantifiable.
- **Top-N listing.** The N highest residual-risk rows, with aggregate narrative.
- **Trend aggregation.** Point-in-time counts with change-from-previous-period.

Whichever is used, the methodology must be documented and reproducible.

### Reperformance

For the aggregation to be reproducible, the auditor should be able to:

- Pull the register snapshot as of a declared date (ISO-dated).
- Apply the published aggregation rule.
- Produce the same portfolio figure the organisation reported to its board.

A delta between the auditor's reperformed aggregation and the reported figure is a finding; common causes include rows added or removed after the reporting cutoff without version control, rows re-scored without changing the register history, or an aggregation rule that is applied with manual "exceptions" that are not part of the documented methodology.

### Version control

A register without version control (git repository, immutable workflow system, signed PDF snapshots with a chain-of-custody log, or similar) cannot support reproducible aggregation. The auditor tests whether:

- Each row has a last-modified timestamp and modifier identity.
- Each portfolio snapshot has a declared cut-off timestamp.
- Prior snapshots are retrievable and tamper-evident.

Absence of version control is a severity-dependent finding; for an ISO/IEC 42001 engagement it is a Clause-7.5 / Clause-9 nonconformity.

## Sign-off routing

Each register row's sign-off routing is a workflow: the risk statement is drafted, scored, control-mapped, routed for approval, approved (or rejected), and the result is recorded. The auditor's routing audit:

- **The route is documented.** A RACI or an equivalent workflow diagram is present.
- **The route actually executes in practice.** For a sample of rows the auditor traces the artefacts: the draft record, the review comments, the approver identity, the decision timestamp. Rows that are "approved" without a traceable approval record are a finding.
- **Routing matches risk size.** High-severity risks route to the audience identified by the appetite statement; low-severity risks may route to a lower-level approver; the configured routing table matches the appetite.
- **Escalation triggers.** A score above the appetite-escalation threshold triggers escalation; the auditor samples breaches and traces the escalation record.
- **Closure.** Mitigations identified in the row have a closure record (completion evidence, re-scoring post-mitigation). Rows that record a mitigation action without closure are a finding.

ISO/IEC 42001 Clause 5 (leadership) and Clause 6 (planning) make the sign-off routing explicitly auditable; the auditor cites those clauses when framing the routing finding.

## Linking register rows to evaluations, controls, and monitors

Every register row's monitoring and evidence linkage must match chapter 1's trace. The auditor cross-references:

| From the register row | Expected target | Chapter-1 trace equivalent |
|-----------------------|-----------------|-----------------------------|
| Evidence pointer       | Published eval result (Inspect run, HarmBench ASR, Fairlearn report) | Evaluation locus |
| Control pointer        | SoA / control-catalogue entry (`mod-105`) | Control locus |
| Monitoring pointer     | Telemetry metric, alert rule (`mod-108`) | Monitor locus |
| Harm linkage           | Harm-taxonomy category (chapter 1) | Harm category |

Rows where the chapter-1 trace exists but the register points elsewhere are *trace drift* findings — one of the two must be wrong and the auditor reports the inconsistency rather than silently picking a winner.

## The register-sampling plan

Sampling follows `mod-104`:

- **Stratify by severity.** At minimum: all rows with residual score above appetite; a random sample of within-appetite rows.
- **Stratify by family.** At least one row per NIST AI 600-1 category (for GenAI); at least one row per MIT Repository domain.
- **Stratify by owner.** Coverage across second-line owners so no owner's rows are untested.
- **Include the full "breach" population.** Every appetite-breach row is in scope — these are the rows that most require defensible scoring.
- **Include at least one closed row.** Closure testing is often the weakest link; a closed row with no closure evidence is a finding.

Record sample size, population size, and the resulting assurance level. ISA 530 / AU-C 530 apply.

## Common failure modes

- **Scoring once, reviewing never.** A register populated at the start of the AI programme and never re-scored. The auditor tests review cadence as a first-order procedure.
- **The register is a slide deck.** A register in a non-queryable format cannot support aggregation reperformance; the finding is against ISO/IEC 42001 Clause 7.5 (documented information).
- **The owner is a team, not a named executive.** Accountability requires a named person; team-owned rows are frequently mis-escalated.
- **"Within appetite" without the number.** A row is flagged within appetite but no appetite threshold is cited. The auditor requires the threshold reference per row.
- **Mitigation closure recorded without re-scoring.** A control is implemented but the residual score is not re-computed. The register stays "high residual" after a strong mitigation, or vice-versa.
- **Treating the register as the whole risk programme.** The register is one artefact; the programme also comprises the harm model, the controls, the monitors, the incident log, and the governance minutes. The auditor's scope is the programme; the register audit is a slice of it.

## Summary

- A well-formed register row has twelve fields; missing any is a documentation finding, and internal inconsistency across fields is a more severe finding.
- Scoring consistency is tested by methodology check + per-row reperformance + cross-row consistency; expect to find "control-defeated" scoring absent or equal to residual.
- Risk appetite is a signed document approved by the audience named in the governance charter; thresholds must appear in the register and classification flags must match the thresholds.
- Portfolio aggregation must be reproducible from the published methodology against a version-controlled register snapshot.
- Sign-off routing is a documented workflow; sampled rows must trace from draft to approval to closure.
- Every register row must link to the same evaluation, control, and monitor identified in chapter 1's trace; trace drift is its own finding.
- Sampling follows `mod-104` discipline — stratified by severity, by family, by owner, and including the full appetite-breach population.
