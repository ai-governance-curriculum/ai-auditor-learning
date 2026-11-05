# exercise-02: Risk Register Audit Drill

**Estimated effort:** 2 hours

## Objective

Reperform the scoring on a sample of **AI-risk-register rows**, trace the signatory chain of the **risk-appetite statement**, reproduce the **portfolio aggregation**, and test the **sign-off routing** for both approvals and appetite-breaches. Produce the engagement workpaper that an audit-committee reviewer would read to decide whether the risk register is a defensible attestation artefact.

## Prerequisites

- Chapter [`02-auditing-the-risk-register.md`](../02-auditing-the-risk-register.md).
- Chapter [`01-auditing-the-harm-model-and-risk-taxonomy.md`](../01-auditing-the-harm-model-and-risk-taxonomy.md) — the harm-to-trace linkage carries into the register audit.
- `mod-104` evidence and sampling discipline.
- Familiarity with ISO/IEC 23894 Clause 6.4 (risk assessment) as the normative reference for scoring consistency.

## Scenario

**Meridian Brokerage** operates an AI-assisted trading-support product for retail investors in the US and UK. The product recommends asset-allocation shifts based on account data, user-declared risk appetite, and market signals. Meridian's second-line risk function maintains an AI-risk register of 73 rows across twelve risk owners; the register is in a bespoke GRC tool, exportable to CSV. Meridian has also published a one-page AI Risk Appetite Statement signed by the Chief Risk Officer in the prior calendar year and referenced in the Board Risk Committee minutes.

You are the lead auditor on an external limited-assurance engagement commissioned by Meridian's audit committee ahead of a UK FCA supervisory review. Your fieldwork step is the register audit.

For the exercise, substitute any accessible register: a published or publicly leaked AI risk register (where accessible); an open-source project's security risk register if no AI example is available; or a synthetic register you construct yourself containing at least 20 rows that reflect realistic risk statements. Attribute the subject at the top of the workpaper.

## Requirements

1. **Pin the register snapshot.** Export the current register, record the cutoff timestamp, number of rows, hash of the export, the risk-appetite statement's version and signatories. Record the ISO date of the snapshot.

2. **Test the twelve-field completeness** on every row. Chapter 2's twelve fields are: risk ID, harm linkage, risk statement, inherent score, controls, residual score, control-defeated score, treatment decision, risk owner, sign-off record, review cadence, appetite status, monitoring linkage, evidence pointer. Report completeness as the percentage of rows with all required fields and the per-field missing count. Rows missing one or more fields are candidate findings.

3. **Reperform scoring on a stratified sample of at least 15 rows.** Include every appetite-breach row, at least three rows per severity tier, at least one row per NIST AI 600-1 category (if GenAI) or per MIT Repository domain. For each sampled row:
   - Score inherent independently, using the organisation's methodology.
   - Score residual independently with controls assumed to be operating.
   - Score control-defeated independently.
   - Record delta vs. the register.
   - For deltas of more than one scale step, open a finding and document the rationale gap.

4. **Audit the risk-appetite signatory chain.** For the published appetite statement: identify the signatory, confirm the signatory's authority per the AI-governance charter at the signature date, confirm the signature pre-dates the register rows it governs, confirm the signature is cryptographically evidenced (or document the evidence form). If the appetite applies to inherent vs. residual, confirm the methodology states which and that register entries interpret the same way.

5. **Reproduce portfolio aggregation.** Apply the organisation's published aggregation rule to the register snapshot and compare to the figure the organisation most recently reported to its board. Record delta. If the delta is non-zero, trace the cause — rows added / retired after the reporting cutoff, methodology exceptions, aggregation-rule drift.

6. **Test sign-off routing.** Pull the workflow evidence for at least five recent register changes and five recent appetite-breach escalations. For each, trace the routing — drafter, reviewer, approver — against the documented RACI. Record missing or mis-routed cases as findings.

7. **Test closure.** For at least three "mitigated / closed" rows, trace the closure evidence — the mitigation artefact, the post-mitigation re-scoring, the re-signature. Rows closed without a post-mitigation re-score are findings.

8. **Test register-to-trace consistency.** For three sampled rows, pull the chapter-1 trace for the referenced harm and confirm the register row's evaluation / control / monitor references match the trace. Register-to-trace drift is a finding.

9. **Author the finding register** for the exercise: finding ID, severity under the organisation's scale (or escalated if the scale is absent), category (completeness / scoring / appetite / aggregation / routing / closure / trace), affected row(s), criterion reference, evidence pointer, recommended management response placeholder.

## Starter guidance

- If the subject register is synthetic, make the twelve-field completeness realistic — some rows should be fully populated, some should have gaps the exercise exposes.
- Reperformed scoring will often produce a two-step delta when the methodology is under-operationalised; this is the finding you are being paid to produce.
- A missing `control_defeated` column is the single most common finding in chapter-2 audits; expect to open it.
- The signatory-chain test often surfaces that the "appetite statement" is an executive memo rather than a board-ratified document; this is the governance finding.
- Portfolio aggregation reperformance requires a documented rule — if the organisation cannot produce one, the finding is against methodology before the numbers.
- Use the Python `pandas` / `openpyxl` / CSV tooling of your choice for register analysis; preserve the raw register artefact.

## Acceptance criteria

The deliverable is accepted when:

- The register snapshot is pinned (export timestamp, hash, row count, ISO date).
- The twelve-field completeness report is present with per-field missing counts.
- At least 15 rows have been scoring-reperformed with inherent / residual / control-defeated independent scores and delta vs. the register.
- The appetite-signatory chain is traced with each signatory's authority basis cited.
- The portfolio aggregation has been reperformed and the delta vs. the reported figure is recorded.
- Routing and closure samples are present with each step traced.
- Register-to-trace consistency sample is present.
- The finding register has at least one finding per category you identified (or an honest "no finding under this category" with rationale).
- Sampling justification is documented per `mod-104`.
- Every criterion reference cites a primary source (ISO 23894, NIST AI 100-1, the organisation's own methodology); `<!-- needs-research: ... -->` where you could not fully pin the source.

## Stretch goals

- Build a small Python script that, given the register export, flags rows where `residual == inherent − 1` (reflexive-step bias) or where `control_defeated == residual` (unmodelled bypass case).
- Draft the one-page **appetite-statement review memo** you would hand to the Chief Risk Officer, enumerating the signatory-chain gaps and the methodology ambiguities you found.
- Produce a **register version-diff** across two snapshots (today's and ninety days ago) and quantify how much of the register is stale (unchanged beyond its declared review cadence).
- Draft a **data-quality rubric** for the register's structural fields the organisation could adopt to prevent the common finding patterns (missing control-defeated, team-rather-than-person owner, within-appetite without threshold citation).
