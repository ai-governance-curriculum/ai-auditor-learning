# Authoring Audit Workpapers — Electronic Working-Paper Systems and Git-Tracked Repos

## Motivation

Workpapers are the only durable record of what the auditor did. ISA 230 — Audit Documentation (IAASB), AU-C 230 — Audit Documentation (AICPA), IIA Standard 14.5 (Documenting Engagement Information) and PCAOB AS 1215 (Audit Documentation, for registered firms) all require working papers to be prepared on a timely basis, sufficiently detailed that an experienced auditor having no prior connection with the engagement could understand *the nature, timing, and extent* of procedures performed, *the results and evidence obtained*, *the significant matters and conclusions reached*, and *the identity of preparers and reviewers*. The standards further require retention for a defined period (typically five years under IAASB; seven years for PCAOB engagements; longer in specific jurisdictions) and assembly of the final audit file within a set time after the report date.

For AI audit the standard does not change; the *shape* of the file does. An electronic working-paper system (Caseware, TeamMate+, Workiva, AuditBoard) is the typical tool for financial and SOC-style engagements. For AI-native engagements, teams increasingly complement the electronic system with a Git-tracked repository that holds reproducibility bundles, eval artifacts, sample seeds, and scripts — artifacts the electronic system is not designed to version well. This chapter installs the workpaper authoring discipline, maps it onto the electronic systems, and shows the Git-tracked companion repository that makes AI evidence replayable.

## The anatomy of a defensible workpaper

Every engagement workpaper carries six load-bearing fields plus a cross-reference apparatus. The field names come from standard practice; the prompts underneath each field are the AI-specific sharpening.

### 1. Objective

- Why does this workpaper exist? Which audit assertion does it address?
- Trace to the engagement plan (chapter from `mod-103`) and the criterion register (chapter from `mod-102`).
- One sentence, specific to the assertion. "Test that the production LLM application serves only governance-approved prompt templates during the audit period" — not "test prompt governance".

### 2. Criterion

- The explicit standard, regulation, control, or policy the subject matter is being tested against.
- Citation: standard clause / regulation article / control ID / policy section.
- The criterion wording quoted verbatim. Paraphrased criteria drift.

### 3. Procedure performed

- Step-by-step enumeration. Each step either inspects a specific artifact, re-performs a specific procedure, re-queries a specific store, or interviews a specific individual.
- For sample-based procedures (chapter 2): the population definition, frame, selection method, random seed, sample size, sample identifiers.
- For re-performance procedures (chapter 6): the reproducibility-bundle identifier and the hash of the bundle.
- For inquiry procedures: the individual, their role, the date, and the specific substantive content obtained — oral evidence is secondary and must be reduced to documentary.

### 4. Evidence inspected

- Each artifact: identifier, tier (chapter 4), grade (chapter 4), source, date obtained, hash (where content-addressable), and path (to electronic WP system node, or to repository path).
- Screenshots marked as derivative with a pointer to the original.
- Independent re-run artifacts linked to the reproducibility bundle.

### 5. Exception noted

- Deviations from the criterion found in the procedure.
- Qualitative analysis per deviation (chapter 2 §Evaluating deviations qualitatively): pattern, cause, intention, concealment, recurrence, management awareness.
- Severity banding (consistent with the engagement-level severity framework from `mod-111`).

### 6. Conclusion reached

- Whether the procedure provides sufficient appropriate evidence for the assertion.
- What the assertion says *given* the procedure's result — "control operates as designed throughout the period", or "control operates for high-volume cohort but breaks for the French-language cohort on 2026-07-14 through 2026-07-19" — specific, not generic.
- Impact on the overall opinion, if any.

### Cross-references

- References to other workpapers (planning memo, risk assessment, sampling workpaper, independent re-run bundle, management representations).
- References to the engagement letter and criterion register.
- Backward references from subsequent workpapers that build on this one (chapter 6 reproducibility bundles; chapter 7 chain-of-custody manifests).

### Preparer and reviewer

- Preparer's name, role, and date.
- Reviewer's name, role, date, and review notes resolved.
- Engagement quality reviewer, if the engagement is subject to EQR under ISQM 2 / QM 2 / PCAOB AS 1220, with date and clearance.

## Working inside the electronic working-paper system

Electronic working-paper systems — Caseware, TeamMate+, Workiva, AuditBoard — all share the same conceptual shape: a hierarchical file tree, locked index numbering, permission-controlled sign-off, assembly cut-off, and retention. The vendor differences are implementation; the discipline carries. The AI-specific considerations when authoring inside these systems:

- **Index the workpaper against the engagement plan.** The systems' default indexing templates (financial-audit lineage) rarely map cleanly to an AI engagement. Create an engagement-specific index tree — Planning (A.xx), Risk Assessment (B.xx), AIMS clause / criterion register (C.xx), Fieldwork by criterion (D.xx with deeper subtrees), Findings (E.xx), Reporting (F.xx), Management Representations (G.xx), Sign-off (H.xx) — and document it in the engagement's index memo.
- **Attach, do not paste.** The systems' rich-text editors tempt copy-pasting an eval-metric table into a workpaper. Attach the original artifact (CSV, JSON, Parquet) with its hash in the attachment metadata, and reference it in the workpaper text. Pasted values rot; attachments survive assembly cut-off.
- **Lock the index after assembly.** The systems enforce an assembly cut-off — after cut-off, workpapers are read-only; corrections appear as *amendments* with their own audit trail. The lead auditor's calendar must respect the cut-off; a sloppy assembly invites PCAOB-style findings.
- **Use the system's review-notes feature, not email.** Review notes, clearance notes, and engagement-quality reviewer sign-offs live in-system. Email threads about workpaper content are a known compliance-risk vector.
- **Use the system's data-import connectors where safe.** Modern systems can pull from Jira, ServiceNow, cloud logs, and sometimes directly from a MLflow / registry endpoint. Direct ingestion reduces transcription errors; the auditor must still verify the connector's data-fidelity controls.
- **Mind the data-residency and confidentiality constraints.** Electronic WP systems are SaaS-hosted; AI engagements often involve sensitive model artifacts and traces. Verify the system's data-handling meets the engagement letter's constraints before loading evidence.

### An illustrative index for an AI engagement workpaper file

```
A. Engagement administration
   A.01 Engagement letter
   A.02 Independence confirmation (ISA 620 specialists, firm independence log)
   A.03 Engagement plan (from mod-103)
   A.04 Specialist scope-of-work letter (ISA 620)
B. Risk assessment
   B.01 Inherent-risk memo
   B.02 Residual-risk memo
   B.03 Risk register for this engagement
C. Criterion register
   C.01 Criterion register (from mod-102 output)
   C.02 Criterion-to-evidence map
D. Fieldwork by criterion
   D.01.<criterion-id> Objective / Criterion / Procedure / Evidence / Exception / Conclusion
   D.02.<criterion-id> …
   D.xx.SAMPLING  Sampling workpaper (chapter 2 shape)
   D.xx.REPRODUCE Reproducibility bundle manifest (chapter 6 shape; artifact attached)
   D.xx.SPECIALIST Specialist deliverables and lead-auditor evaluation
E. Findings and management response
   E.01 Finding log
   E.02 Management responses
   E.03 Follow-up schedule
F. Reporting
   F.01 Draft report
   F.02 Final report
G. Representations
   G.01 Written representation letter (ISA 580)
H. Sign-off
   H.01 Preparer / reviewer sign-off log
   H.02 Engagement quality reviewer sign-off (ISQM 2 / QM 2 where applicable)
```

The actual nodes should be systemised in the engagement's index memo and locked; deviations produce an amendment with rationale.

## Working inside a Git-tracked repo for AI-native engagements

Electronic WP systems are strong at structure, sign-off, and retention; they are weak at versioning binary artifacts, replaying commands, and hashing. For AI-native engagements, teams layer a **Git-tracked workpaper companion** that holds the reproducibility bundles (chapter 6), the sampling seeds (chapter 2), and the scripts the engagement authored. The companion is referenced from the electronic WP system and lives under the engagement's retention policy (typically mirrored into the firm's WORM store at assembly cut-off; chapter 7).

A workable companion-repo layout:

```
<engagement-id>-companion/
  README.md                            # one-page map; references electronic WP index
  engagement.yaml                      # engagement metadata; retention tag; sign-off ids
  criteria/                            # criterion register pinned
    criterion-register.yaml
  samples/                             # sampling workpaper companions
    sample-<criterion-id>/
      sample.md                        # the sampling workpaper narrative
      selection.sql                    # the query that produced the frame
      selection.json                   # the seed and resulting identifier list
      frame-reconciliation.md          # frame-to-definition reconciliation
  reproduce/                           # reproducibility bundles (chapter 6 shape)
    bundle-<assertion-id>/
      manifest.yaml                    # artifact hashes, env lock, seeds
      run.sh                           # the exact command the auditor ran
      logs/                            # the raw output
      metrics/                         # the per-item outputs and the aggregates
  specialist/                          # ISA 620 specialist deliverables
    <specialist-id>/
      scope-of-work.md
      deliverable-<n>.md
  attestations/                        # external attestations retained
    vendor-<id>-SOC2.pdf
    vendor-<id>-scope-note.md
  findings/
    <finding-id>.md                    # the finding narrative; cross-ref to workpaper
  manifests/
    evidence-manifest.yaml             # the full artifact-to-criterion manifest
    hash-chain.jsonl                   # chapter 7 hash-chain across the repo
  .gitattributes                       # large-file / binary handling (git-lfs / dvc)
  .gitignore
```

Discipline the Git-tracked companion needs:

- **Signed commits.** The repository requires signed commits (GPG or Sigstore / `gitsign`). Unsigned commits do not land.
- **Protected branch and PR review.** All changes land through PR with at least one named reviewer; the engagement-quality reviewer's PR approval is the engagement-quality clearance for the companion.
- **Content addressing over paths.** Binary artifacts referenced by content hash, not path — the manifest resolves hashes to retrieval paths.
- **Retention mirror.** On assembly cut-off, the repository is tagged, signed, and mirrored into the firm's WORM store with a retention tag. Chapter 7 operationalises.
- **Secrets hygiene.** Trace excerpts, prompt text, and model outputs may contain secrets or PII. Secrets scanning on commit (git-secrets, gitleaks); per-engagement review of what is permitted into the repo; a committed data-handling note.
- **Cross-reference to the electronic WP system.** Every artifact in the companion repo has an `electronic_wp_ref` field in the manifest; every electronic WP workpaper that references the companion carries the commit hash and path.

### What goes where

| Artifact | Electronic WP system | Git-tracked companion |
|---|---|---|
| Engagement plan, risk memo, criterion register | Yes | Pinned copy |
| Workpaper narratives (Objective / Criterion / Procedure / Evidence / Exception / Conclusion) | Yes | Markdown mirror if needed |
| Sign-off and review notes | Yes | No |
| Attached artifacts (PDFs, Office docs) | Yes | Mirrored copies |
| Large binary artifacts (model manifest, eval output files, dataset manifests) | Reference | Yes (LFS / DVC) |
| Reproducibility bundles | Reference | Yes |
| Sampling seeds, queries, selection files | Reference | Yes |
| Specialist deliverables | Yes | Mirrored |
| Final report | Yes | Mirrored |
| Written representation letter | Yes | Mirrored |
| Hash-chain / evidence manifest | Reference | Yes |

The electronic WP system is authoritative for the *audit file* under the firm's QM1 / ISQM1 policies; the Git repo is authoritative for the *reproducibility* of AI-specific procedures. The two reference each other explicitly; neither replaces the other.

## Example workpaper — single criterion, end to end

A compressed example to show the shape in practice. Reuse the structure, not the specifics.

```
D.03.FAIRNESS-COHORT-FR
Workpaper: Fairness delta for French-language cohort — production retrieval-augmented chatbot
Preparer: <auditor-name>, Senior AI Auditor, 2026-11-22
Reviewer: <lead-auditor-name>, Audit Manager, 2026-11-25

Objective
  Test that the production chatbot's refusal-rate disparity between the English-language and
  French-language cohorts during the audit period 2026-01-01 to 2026-10-31 does not exceed the
  Colorado AI Act consequential-decision fairness-governance commitment the organisation
  has published (criterion C.07 in the criterion register).

Criterion
  Internal policy POL-AI-FAIRNESS-02, section 3.2: "Refusal-rate delta between the two highest-
  volume language cohorts shall not exceed 2 percentage points on a trailing 30-day basis."
  [Attached: POL-AI-FAIRNESS-02 v3.1, hash a4f2…]

Procedure
  1. Define the population: all chatbot sessions in the audit period, tagged by detected input
     language, excluding the pre-production canary cohort.
  2. Pin the frame: trace-store query selection.sql (companion-repo sample-C.07),
     reconciled to the dashboard count within 0.5% (frame-reconciliation.md).
  3. Statistical sample of 384 sessions per cohort (95% confidence, 5% tolerable error on the
     refusal-rate delta, pilot variance from a 2026-Q2 pilot). Selection: stratified random
     within month, seed 20261118.
  4. Independent re-run of the refusal-classifier on sampled sessions, with the classifier
     version and dataset pinned (reproducibility bundle RB-033).
  5. Aggregate the refusal rate per cohort per month; compute delta with a 95% bootstrap CI.

Evidence inspected
  - Policy POL-AI-FAIRNESS-02 v3.1 — Tier Original, Grade A — signed tag, Git ref abc1234.
  - Trace-store query results — Tier Original, Grade B — pinned to companion-repo
    (samples/sample-C.07/selection.json, hash 7d9c…).
  - Refusal-classifier run artifact — Tier Original, Grade B — reproducibility bundle RB-033
    (companion-repo reproduce/bundle-RB-033, hash e2a0…). Reconciles with management's
    monthly report within 0.3 pp.
  - Management's monthly fairness report — Tier Derivative, Grade C — attached to D.03 for
    reconciliation; not relied on as primary.

Exception noted
  One month, 2026-07, shows a refusal-rate delta of 3.1 pp on a trailing 30-day basis — above
  the 2 pp threshold. Qualitative: coincides with the deployment of guardrail config v4.3 on
  2026-07-08; management reverted on 2026-07-20 and the delta returned to 1.4 pp.
  Not anomalous — the deviation is systematic within the period 2026-07-08 to 2026-07-20.
  Sufficient severity to be a finding (severity Moderate, see finding F.07).

Conclusion reached
  Control operated during the audit period except for the 2026-07-08 to 2026-07-20 window.
  Finding F.07 recorded. Opinion: qualified as to the operation of the fairness control
  during that window.

Cross-references
  Engagement plan EP.01, criterion register C.07, sampling workpaper D.xx.SAMPLING-C.07,
  reproducibility bundle RB-033 (companion-repo), finding F.07, management response MR.07.

Preparer / Reviewer / EQR
  Preparer: <name>, 2026-11-22
  Reviewer: <name>, 2026-11-25, review notes cleared 2026-11-26
  EQR: <name>, 2026-11-28, no partner clearance comments
```

The workpaper is terse but complete — the engagement-quality reviewer can walk it end to end in one read. The companion-repo bundles are what the reviewer uses to verify the re-run.

## PCAOB-style inspection posture

Audit firms subject to the **PCAOB** (US) or analogous inspection regimes (FRC in the UK, CPAB in Canada, ACPR in France, equivalent national bodies elsewhere) must produce workpapers that survive inspection months or years after the engagement. The inspection posture is harsh: inspectors pick a sample of engagements, re-perform selected procedures from the workpapers alone, and challenge gaps. For AI engagements, the extra inspection vectors are:

- **Reproducibility of the metric claim.** Can the inspector independently reproduce the auditor's re-run from the companion-repo manifest? If the reproducibility bundle does not survive inspection re-performance, the opinion does not survive.
- **Sampling defensibility.** Can the inspector regenerate the sample from the seed and the frame query? Can the inspector reconcile the frame to the population? Any failure here is a sampling-standard finding.
- **Specialist use.** Can the inspector walk the ISA 620 scope-of-work letter, the specialist's deliverables, and the auditor's evaluation of those deliverables? Division-of-responsibility language or missing evaluations are the common findings.
- **Evidence tier and grade.** Can the inspector see what was original, derivative, corroborative, and how the engagement upgraded C-grade evidence where load-bearing? Workpapers that do not name tier and grade are routinely challenged.
- **Chain of custody.** Can the inspector trust that what is in the file is what was in the file at assembly cut-off? Chapter 7 operationalises.

Audit documentation is not just about the engagement; it is about the engagement's ability to be defended *to a stranger, under adversarial review, years later*.

## Common failure modes

- **"Procedure" that is a list of nouns.** "Reviewed the eval report." Which report? With what procedure? Which fields verified? Procedures are verbs with objects.
- **Conclusion that is restated procedure.** "Procedure performed with no exceptions." A conclusion addresses the assertion, not the completion of the procedure.
- **Evidence-tier omissions.** The workpaper lists artifacts without tier or grade; sufficiency cannot be aggregated.
- **Unlocked index that drifts.** The engagement index changes mid-field; cross-references rot; assembly is rushed.
- **Review notes in email.** Out-of-system review threads lose the audit trail.
- **Companion repo and electronic WP out of sync.** The repo has a reproducibility bundle; the electronic WP references a prior version; the inspector finds the delta.
- **Hashes recorded but not verified.** The workpaper carries the hash; the engagement team never re-computed the hash on inspection; chapter 7 is the fix.
- **Signed representation letter obtained late.** ISA 580 representations are required to be dated as near as practicable to the date of the auditor's report; late-dated representations are a reporting-standard finding.

## Summary

- Workpapers are the audit's durable record under ISA 230 / AU-C 230 / IIA Standard 14.5 / PCAOB AS 1215. Each workpaper carries Objective, Criterion, Procedure, Evidence, Exception, Conclusion, cross-references, and preparer/reviewer identification.
- Electronic working-paper systems (Caseware, TeamMate+, Workiva, AuditBoard) provide the structure, sign-off, and retention; attach originals rather than paste, lock the index after assembly, keep review notes in-system.
- For AI-native engagements, a Git-tracked companion repository holds reproducibility bundles, sampling seeds, queries, specialist deliverables, and manifests — cross-referenced from the electronic WP system, signed, protected-branched, and mirrored into WORM at assembly cut-off.
- The electronic WP file is authoritative for the audit file under QM1/ISQM1; the companion repo is authoritative for AI reproducibility. Neither replaces the other.
- PCAOB-style inspection asks whether a stranger could re-perform the engagement from the file alone. Reproducibility, sampling defensibility, specialist use, evidence tier/grade, and chain of custody are the usual inspection vectors.
- Chapter 6 dives into the reproducibility bundle; chapter 7 operationalises chain of custody across the electronic and Git-tracked systems.
