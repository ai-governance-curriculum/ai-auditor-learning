# The Independent Replication Report — Shape, Audiences, and Payload Discipline

## Motivation

The engagement's output is a report. Everything in chapters 1–6 — the claim register, the replication manifests, the signed-delta rows, the calibration appendix, the fairness summary, the robustness-privacy-red-team audit — converges in a single deliverable that the audit committee, the regulator (where applicable), and the vendor (for third-party audits) read to form their own opinions. A technically-sound engagement with a weak report leaves no durable artefact; a well-authored report makes the auditor's findings legible and defensible for years.

This chapter installs the independent-replication report's shape, the multi-audience variant discipline, and the adversarial-payload handling that keeps the report safe to distribute. Report authoring for the broader AIMS audit is `mod-111`; this chapter covers the card-claim replication specifically.

## The report's shape

A minimum section list the engagement should produce:

1. **Cover and attestation.** Engagement identity (client, period, report date, scope), the auditor's signatures, the body under which the audit was performed (IIA Standards 2024 / IAASB ISAE 3000 / AICPA SSAE-19 / ForHumanity IAAIS / NYC LL144 bias audit), the type of assurance (reasonable vs. limited; attestation vs. direct engagement; `mod-101` chapter 5).
2. **Executive summary.** One-page: subject, scope, approach, aggregate finding posture, auditor's opinion (or, for direct-report engagements, the auditor's conclusion).
3. **Scope and criteria.** The system(s) under audit, the cards replicated, the obligations the engagement tested against, the exclusions.
4. **Approach.** The methodology summary — claim-register construction, replication toolchain, calibration methodology, fairness-shape audit, robustness/privacy/red-team-shape audit. One or two sentences per chapter of this module.
5. **Scope restrictions and limitations.** The specific things the auditor could not do (vendor-withheld eval sets, API-routing drift on closed-weights endpoints, archived benchmarks, insufficient sample sizes). Each restriction cross-references the finding register.
6. **Claim register and auditability grading.** The chapter-1 register in summary form; counts of Grade A / B / C / D / E claims; link to the full register as an appendix.
7. **Replication results.** Chapter-3 benchmark deltas; chapter-5 fairness deltas; chapter-6 robustness/privacy results. Each with a signed-delta row and a status (within-noise-floor / within-claim-CI-outside-noise-floor / outside-both-CIs / unverifiable).
8. **Calibration-methodology appendix** (chapter 4). Sample sizes, judge-reliability estimates, CI reconstructions, overstatement grading.
9. **Fairness audit** (chapter 5). Obligation map, metric-appropriateness grades, protected-class coverage, intersectional reporting, replication deltas; the BABL AI or IAAIS report shape where applicable.
10. **Robustness / privacy / red-team audit** (chapter 6). Attack-surface coverage, adversarial-budget audit, DP-accountant replication, MIA cross-check, red-team coverage matrix, replay-bundle integrity.
11. **Findings register.** Every finding, graded major / minor / observation (`mod-105` chapter 2 definitions), with evidence reference and management response placeholder.
12. **Auditor's opinion or conclusion.** The attestation sentence appropriate to the engagement type.
13. **Appendices.** The claim register in full; the replication manifests (by ID, hashes in-report, full manifests in the engagement WORM store); the environment pin; the glossary; the applicable-standards list.

For Stage-2 ISO/IEC 42001 engagements this report is an input to the broader AIMS audit report (`mod-105` chapter 10). For stand-alone card-claim engagements it is the deliverable itself.

## The opinion vs. conclusion distinction

The attestation stack (`mod-101` chapter 5) determines what the final sentence says:

- **Reasonable-assurance engagement (ISAE 3000, SSAE-19 Examination).** "In our opinion, the published claims in the model card are, in all material respects, supported by the evidence inspected and replicated." (Modified: qualified, adverse, disclaimer.)
- **Limited-assurance engagement (ISAE 3000, SSAE-19 Review).** "Based on the procedures performed, nothing has come to our attention that would indicate the published claims are not, in all material respects, supported by the evidence."
- **Direct engagement (ISO/IEC 17021-1 certification).** The auditor's *conclusion* and *certification recommendation*, not an opinion. (`mod-105` chapter 10.)
- **NYC LL144 bias audit.** The auditor reports the computed impact ratios; the "pass / fail" framing is the deployer's regulatory reading, not the auditor's opinion. The audit itself is a *direct-reporting attestation* whose opinion is on the computation's faithfulness.
- **ForHumanity IAAIS.** Certification shape; the auditor issues a certificate or a reasoned non-issuance, under the ForHumanity criteria set.

The engagement letter (`mod-103`) fixes the type; the report's language conforms. Mismatch — e.g., an IAAIS-style certification sentence in a limited-assurance engagement — is a reportable auditor independence and competence issue.

## Multi-audience variants

A single engagement often requires several report variants with different disclosure classes:

### Audit-committee / board variant

- **Audience.** Internal audit committee, board, senior management.
- **Length.** Short — 10–20 pages plus appendices.
- **Content focus.** The opinion, material findings, management-response placeholder, aggregate-posture narrative.
- **Payloads.** Redacted; hashes with references into the WORM store for the committee's chief auditor only.
- **Delivery.** Via the client's audit-committee document system; access-logged.

### Regulatory variant

- **Audience.** EU AI Office (for Article 72 post-market monitoring), FDA (for SaMD), NYC DCWP (for LL144 bias audit publication), state insurance commissioners, etc.
- **Length.** As prescribed by the receiving regulator.
- **Content focus.** The specific attestation the regulator requires; references to the standards (EU AI Act Articles, NAIC Model Bulletin, etc.).
- **Payloads.** Per regulator — some require full disclosure under a confidentiality agreement; most prefer structured findings with controlled references.
- **Delivery.** Through the regulator's prescribed submission channel.

### Vendor variant (third-party audits)

- **Audience.** The audited vendor, their counsel, their technical team.
- **Length.** Full, including the appendices that let the vendor reproduce the auditor's work.
- **Content focus.** Full procedures, full replication manifests (so the vendor can independently re-run and respond), full finding register with evidence references.
- **Payloads.** Full — the vendor already owns them; the report returns them with hashes.
- **Delivery.** Through the engagement-letter's agreed channel, under non-disclosure / assurance-terms contract.

### Public variant (NYC LL144 publication, voluntary disclosure, PAI publication guidelines)

- **Audience.** The public.
- **Length.** The jurisdiction's prescribed template (LL144 has a specific posting shape).
- **Content focus.** Computations, numbers, methodology summary; findings in aggregate.
- **Payloads.** None. Adversarial payloads never appear in the public variant. Even summary statistics that might support an adversary are considered.
- **Delivery.** The deployer's website or the regulator's registry as required by law.

The engagement produces the variants from a *single source-of-truth artefact* — a canonical JSON / Markdown document that the report-build pipeline renders into each audience's variant. Each variant inherits the same signed-delta rows and finding IDs; only the surrounding prose and the disclosure of payloads varies.

## Adversarial-payload discipline in the report

Payload-bearing artefacts (from chapter 6):

- Jailbreak prompts and working outputs.
- Extraction-attack prefixes.
- Cyber-security-adjacent content (CyberSecEval).
- Dangerous-knowledge probes (WMDP).
- Red-team successful-attack transcripts.

For each the report:

- **Replaces the payload with its SHA-256 (or longer) hash and a WORM-store reference.** The reader cannot reconstruct the payload from the report text.
- **Discloses the attack *class* and the attack *outcome*,** not the attack verbatim. "The HarmBench behaviour B-142 (biothreat-adjacent) produced a successful attack with 1/50 prompt variants" is appropriate; the prompt itself is not.
- **Sanctions payload release to narrow audiences** — the vendor's secure-handling team, counsel under privilege, a regulator under a lawful request.
- **Records the audit trail of any disclosure** — who accessed, when, under what authority.

The author of the report is responsible for every payload on every page. A "quick appendix" that leaves in a working jailbreak is a professional-conduct incident even if the report is otherwise strong.

## Report signatures and attestations

The report carries structured signatures:

- **Engagement partner / lead auditor signature.** Human-readable and digitally signed (cosign / PGP) where the engagement's attestation body permits.
- **Independent reviewer signature.** Under ISO/IEC 17021-1 clause 9.5 (`mod-105` chapter 1), the certification decision requires an independent reviewer; for attestation engagements the engagement quality control reviewer (EQR / EQCR) plays the parallel role.
- **Date of attestation.** Not the same as the "as of" date of the subject matter; both appear.
- **Subsequent-events statement.** For attestation engagements, whether procedures were performed on subsequent events through the report date.
- **Signed replication-manifest manifest.** A single higher-level artefact that lists all replication-manifest hashes; signing it binds the collection.

Signatures are the minimum artefact that makes the report defensible against a vendor's dispute and against a regulator's challenge. Unsigned reports — however well-authored — carry less weight.

## Writing for professional skepticism

The report is written by a skeptical auditor for a skeptical reader. Two disciplines:

- **Separate findings from recommendations.** The report states findings. Where the engagement's remit permits, it may suggest *categories* of remediation; it does not design the remediation. `mod-111` operationalises management response.
- **Avoid "ad-hominem" phrasing.** "The vendor's methodology is sloppy" is not an audit sentence. "The methodology does not report the sample size required to support the published precision; this does not conform to [criterion]" is.
- **Quantify where quantifiable.** "Several claims" is weaker than "7 of 42 claims"; "many samples" is weaker than "23 of 500."
- **Attribute the toolchain.** "We ran HarmBench 2024-03 release under Inspect 0.3.52 on a pinned model revision abc1234; results below." Not: "We red-teamed the model."
- **Pin the dates.** Everything decays — the card at retrieval, the benchmark at pin, the model at revision, the regulation at as-of. The report dates each.
- **Admit uncertainty.** Where the auditor could not replicate, say so; a limited scope is a stronger report than a scope the auditor pretends to have covered.
- **Preserve the vendor's response space.** Where the engagement includes a management-response process (`mod-111`), the finding is drafted so the vendor has room to respond substantively.

## Workpaper-to-report trace

Every sentence in the report that claims a fact must trace to a workpaper:

```
Finding F-07 → calibration appendix row 14 → replication manifest ACME-…-REP-0014 → raw per-sample output hash 0xABC… → WORM store path s3://…/REP-0014/outputs.jsonl
```

The trace is what the independent reviewer walks. A finding that cannot be walked from the sentence to the raw artefact fails the ISA 230 / IAASB-and-AICPA documentation standards (`mod-104`).

## Failure modes with report authoring

- **The "review" that becomes a verification.** Using "we have audited" in a limited-assurance engagement is an engagement-type mismatch; the auditor confuses the standards the engagement runs under.
- **The headline that ran ahead of the evidence.** "Our audit found pervasive fairness violations" with two findings in a 42-claim register is unsupported in aggregate.
- **The hidden qualifier.** Appendix caveats that the executive summary did not inherit mislead the reader; whatever qualifies the opinion must appear on the cover page.
- **The duplicated finding.** A single evidence stem creating two findings inflates the finding count and can cause the reader to overcount materiality.
- **The missing cross-reference.** A finding citing "see appendix" without the appendix section number is sloppy on first read and expensive to resolve on second.
- **The pretend scope.** Writing as if closed-weights routing drift did not exist. The limitation becomes a vendor-dispute vulnerability.
- **The leaked payload.** Chapter 6 restated: payloads never appear in a disclosable variant.

## Summary

- The independent-replication report is the engagement's durable artefact; chapters 1–6 feed a single source-of-truth that renders into audience-specific variants.
- Attestation type (reasonable / limited / direct / certification / NYC LL144 bias audit / ForHumanity IAAIS) fixes the opinion / conclusion sentence shape; mismatch is itself a reportable issue.
- Variants cover audit-committee, regulatory, vendor, and public audiences; each inherits the same finding IDs, with disclosure class and surrounding prose varying.
- Adversarial payloads are hashed and WORM-stored; the report discloses attack class and outcome, never the payload verbatim; disclosures to narrow audiences are audit-logged.
- Signatures (lead auditor, independent reviewer, date, subsequent-events, replication-manifest manifest) and workpaper-to-report traceability make the report defensible against vendor challenge and regulator inquiry.
