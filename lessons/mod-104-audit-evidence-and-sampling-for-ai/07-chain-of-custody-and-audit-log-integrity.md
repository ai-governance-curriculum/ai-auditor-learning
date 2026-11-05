# Chain of Custody and Audit-Log Integrity — Defending the File Against Tampering

## Motivation

A workpaper file that could have been edited after the fact is a workpaper file that cannot be trusted. **ISA 230 paragraph 15** and **AU-C 230 paragraph 15** require the auditor to assemble the final audit file on a timely basis and, *after assembly*, to retain documentation such that the file is protected against unauthorized alteration; **PCAOB AS 1215** paragraph 15 and the firm's quality-management policies tighten the discipline further. For AI engagements the threat is sharper: the artifacts in play (model weights, eval runs, trace stores, Git commits, logs) are *more* mutable than most financial-audit artifacts and *more* commonly in the hands of the party being audited. Defending the audit file end-to-end is an ISA 500 reliability question applied to time: if the evidence at the time of inspection is not the evidence at the time of procedure, the opinion cannot be defended.

Chain of custody is the discipline that answers *where has this evidence been, who touched it, when, and can I prove it has not been altered?* This chapter installs the practical shape: WORM storage, hash-chained evidence manifests, tamper-evident logs, Git-pinned workpapers, and the professional-skepticism prompts that detect tampering before it ends up in the file. It is where chapters 1 (ISA 500), 5 (workpapers), and 6 (reproducibility bundles) converge.

## The chain-of-custody promise

A defensible chain-of-custody record provides, for every piece of evidence in the audit file:

1. **Identity** — what it is (hash, identifier, description).
2. **Provenance** — where it came from (source system, query, operator, timestamp).
3. **Transit** — how it moved from source to audit file (what tool, what path, what controls).
4. **Custody** — who had access while it was in the audit file, and when.
5. **Integrity** — proof that the artifact at inspection time is the same artifact at receipt time (cryptographic hash, signature, hash chain).
6. **Disposition** — what will happen to it (retention tag, destruction schedule).

A workpaper note like "obtained the eval report from the model owner" is not chain of custody. The six fields, each verifiable years later, are.

## WORM storage and append-only stores

**WORM** ("write once, read many") storage is the baseline for the archived audit file and for the engagement-period evidence that must be preserved against alteration. Modern implementations:

- **Object-store retention locks** — AWS S3 Object Lock (Compliance mode, not Governance mode, for engagements subject to regulated retention), Azure Blob Storage with immutability policies, Google Cloud Storage Bucket Lock. Compliance-mode lock cannot be shortened by a user with console access; the retention is enforced by the service.
- **Append-only database tables** — purpose-built stores like Amazon QLDB, Azure SQL Ledger, or an external commit log (Kafka with an immutable topic configuration) for log-style evidence.
- **Append-only ticket systems** — Jira with a locked-history workflow, ServiceNow with audit-only write permissions. Not strictly WORM but "visible-history" — any edit is recorded as an event rather than overwriting the field.
- **The audit firm's internal WORM store** — most firms maintain a WORM store for assembled audit files; the engagement's assembled workpaper file (electronic WP system export plus companion-repo mirror; chapter 5) is landed here at assembly cut-off.

The audit practice is to **land evidence in WORM at receipt**, not at assembly. Eval run artifacts, trace-store query results, change logs, and incident records should be WORM-pinned as the auditor collects them. Delays between receipt and WORM landing are the tampering window; the window must be short, documented, and the auditor must verify no mutation occurred across it.

## Hash-chained evidence manifests

A **hash chain** is a sequence of evidence records where each record cryptographically binds to the previous one, so that any mutation of a prior record breaks the chain and is detectable by anyone with the current head.

A working hash-chain record:

```
{
  "seq": 204,
  "timestamp": "2026-11-19T10:37:14Z",
  "actor": "<auditor-id>",
  "event": "bundle-closed",
  "bundle_id": "RB-033",
  "artifact_sha256": "e2a0…",
  "prev_hash": "a51f…",
  "this_hash": "7bd4…"
}
```

where `this_hash = SHA-256( concat(seq, timestamp, actor, event, bundle_id, artifact_sha256, prev_hash) )`. The head of the chain is published to a less-mutable medium (signed Git tag in the companion repo, an external notary, or a public transparency log like Sigstore's Rekor) at engagement checkpoints.

Properties the chain earns:

- **Tamper detection** — if any prior record is altered, its `this_hash` changes, every subsequent `prev_hash` breaks, and a reviewer walking the chain detects the break at the first altered record.
- **Timestamp anchoring** — when the head is anchored to an external transparency log, the engagement can prove "this was in the chain as of <date>" to a third party.
- **Reviewer walkability** — the engagement-quality reviewer and PCAOB-style inspectors can walk the chain in order and spot inconsistencies.

For AI engagements the chain's events typically include:

- Evidence receipt (artifact hashed and landed).
- Query execution (trace-store query pinned).
- Sample selection (seed, frame hash, selection output hash).
- Bundle closure (reproducibility bundle manifest hash).
- Workpaper sign-off (workpaper hash, preparer/reviewer identity).
- Finding record creation and modification.
- Assembly-cut-off tagging.
- Post-assembly amendment (rare; records the ISA 230 paragraph 16 circumstances).

The hash-chain file lives in the companion repo at `manifests/hash-chain.jsonl`. It is append-only. It is signed at every append.

## Git-pinned workpapers

Git is natively content-addressed. A Git commit's SHA-1 (migrating to SHA-256 as Git support matures) is a hash over the tree of files at that commit; a signed tag binds the hash to an identity. The companion repo in chapter 5 is Git-tracked precisely so that every workpaper, bundle, and manifest in the audit file can be referenced by its Git object identifier, which cannot be altered without producing a different identifier.

Operational discipline:

- **All commits signed.** GPG keys or Sigstore (`gitsign`) signatures on every commit. Unsigned commits are rejected by the branch protection.
- **Signed tags at checkpoints.** The engagement signs tags at kickoff, fieldwork checkpoints, draft report, final report, and assembly cut-off. Each tag is anchored to an external transparency log when available.
- **Branch protection.** Changes land through pull request; direct pushes blocked; required reviewers named in the repo settings; the engagement-quality reviewer's approval is required on the assembly branch.
- **No history rewriting.** Force pushes blocked; rebases blocked on protected branches; amendments add commits, they do not rewrite them. Any post-assembly change is an **amendment commit** with a referenced ISA 230 §16 rationale.
- **Mirror at cut-off.** At assembly cut-off, the repo is tagged (`engagement-<id>-final`), pushed to the firm's WORM mirror, and the tag's hash is noted in the electronic WP system's sign-off node.

## Tamper-evident logs — reading the organisation's logs with skepticism

The audit team not only *produces* tamper-evident records; it also *reads* the organisation's logs and must assess whether those logs are themselves tamper-evident. Three AI-adjacent log categories the engagement commonly touches:

- **Model-registry logs.** Does the registry record every artifact promotion, every tag assignment, every metadata edit? Does it log deletions and *failed* deletions? Is the log append-only or editable by registry admins?
- **Inference / trace logs.** Does the trace store retain records for the audit period? Does the retention policy allow in-flight deletion by any role? Are correlation IDs stable across retention events?
- **Change-management logs.** Do the change tickets carry an immutable history (every field change logged as an event), or do fields overwrite silently?

For each category, the auditor's test is in two parts: (a) *does the log have the integrity property* (append-only, audited access, retention enforced)? and (b) *does the engagement rely on the log for evidence in a way that requires the integrity property to hold*? Reliance without integrity is a reliance gap.

## Tampering signals — what professional skepticism looks like in practice

ISA 240 paragraph 13 and AU-C 240 paragraph 15 require professional skepticism against fraud, including *backdated documents, altered records, and inconsistencies in the pattern of evidence*. For AI the signals that most warrant skepticism:

### Back-dated commits

- **Git commit timestamps that pre-date the commit's parents** — Git records committer-set dates; a hand-crafted date can predate upstream commits the commit relies on. Detection: inspect the GPG signature timestamp and compare to the committer-set date; inspect the commit's presence in build/CI logs with their own trustworthy timestamps.
- **Commit messages reference events that post-date the claimed commit date** — a commit dated 2026-05-01 that references an incident report from 2026-06-15.
- **The commit does not appear in the CI build log for the claimed date** — the organisation's CI is itself evidence of when a commit existed.

### Replaced model artifacts

- **The registry record names an artifact hash that does not match the current artifact bytes** — the artifact was replaced after the record was written; the record's provenance assertion is false.
- **The registry allows overwrite under the same identifier** — identifier `model-v2.3` points at one artifact on Monday and another on Friday. The audit needs the *point-in-time* identifier; a mutable identifier is a reliability failure.
- **Build-pipeline attestations missing or mis-matched** — the SLSA or in-toto attestation does not reconcile with the artifact; the attestation chain is broken.

### Log mutation

- **Trace-store counts that do not reconcile with aggregate counters** — the `count` of records across the audit period differs from a reasonable business-volume estimate, or differs from the organisation's own monthly report, with no explanation.
- **Gaps in correlation-ID sequences** — the trace store's correlation IDs skip a range.
- **Edited incident tickets with no edit history** — the ticket says "Resolved" but the comments show a different status earlier with no transition record.
- **Dashboard values that do not reconcile with the underlying query** — the dashboard shows 1.5 pp fairness delta; the underlying query returns 3.1 pp. The dashboard is a *view* and the view is misconfigured (benign) or altered (not benign). The engagement investigates.

### Evidence that is "too clean"

Fraud literature warns against evidence that is suspiciously tidy. For AI: an eval history that shows only green runs for months; a change log with every ticket neatly closed with the same resolution text; an incident log with zero incidents when the industry baseline predicts some. "Too clean" is a prompt to expand sampling or to request raw-source evidence rather than the summary.

### Pattern across findings

- Findings concentrated in a single team / time window with identical narratives.
- Management responses that repeat boilerplate text across unrelated findings — a signal that responses were produced by template, possibly without engagement with the finding.

## The evidence manifest — cross-reference index

The engagement team maintains an **evidence manifest** at `manifests/evidence-manifest.yaml` that cross-references every artifact in the audit file to:

- The criterion it supports.
- The workpaper node it appears in.
- The tier (chapter 4) and grade (chapter 4).
- The hash and the retrieval path.
- The chain-of-custody hash-chain sequence number where the artifact was landed.
- The retention tag (regulatory basis for the retention period).
- The disposition at retention end.

The manifest is small, structured, and committed to the companion repo. The electronic WP system's export at assembly cut-off should also index back to the manifest so that an inspector can start from either system and walk to the other.

## Retention and destruction

Retention periods:

- **IAASB / ISA 230** — at least five years from the date of the auditor's report.
- **AICPA / AU-C 230** — at least five years from the report release date.
- **PCAOB AS 1215** — at least seven years from the report release date.
- **IIA** — retention per the audit charter; commonly ≥ three years, often longer.
- **Sector overlays** — SR 11-7 engagement documentation retained per bank policy (often longer); FDA SaMD under 21 CFR 820.180 kept for device-lifetime plus two years; EU AI Act Article 18 imposes ≥ 10 years on the *provider's* documentation, with downstream implications for the auditor's evidence.
- **Jurisdictional overlays** — some jurisdictions impose longer periods (e.g., UK FRC-regulated engagements, Canadian CPAB-regulated engagements).

The engagement's retention tag is the *maximum* applicable period; destruction requires both the period to expire and the engagement's disposition procedure (verify no legal hold, verify no open regulator inquiry, destroy under dual control, record the destruction). AI engagements involving personal data under GDPR/CCPA must reconcile retention with data-minimisation; an engagement workpaper may retain hashed cohort pointers rather than the raw cohort records.

## A tamper-detection drill the engagement team runs

A simple drill the audit team runs at the mid-point of the engagement and again at assembly cut-off:

1. Pick five recently landed artifacts at random from the evidence manifest.
2. For each, independently re-compute the hash from the current bytes in WORM storage.
3. Reconcile to the manifest's recorded hash.
4. For Git-tracked artifacts, verify the signed-commit identity.
5. For hosted-model artifacts (chapter 6), re-read the provider's current model page and verify the model identifier is still live and not deprecated or silently updated.
6. For hash-chain records, walk from the head back three records and verify each `prev_hash` resolves.
7. Record the drill's outcome in the engagement file.

A failed drill is not necessarily fraud — it may be a storage migration, a provider deprecation, a signing-key rotation — but it *is* a required-resolution event. Unresolved failures convert to scope limitations or findings.

## Common failure modes

- **Workpaper sign-off but no cryptographic integrity.** The electronic WP system's sign-off proves the signer clicked; without cryptographic hashing of the file contents, it does not prove the file at inspection is the file at sign-off.
- **Companion-repo without signed commits.** Git provides content addressing by default, but without signed commits an attacker with repo access can rewrite history.
- **WORM in Governance mode when Compliance mode is required.** Governance mode allows a sufficiently privileged user to shorten retention. Regulated retention needs Compliance mode or equivalent.
- **No landing of evidence into WORM at receipt.** Evidence sits in mutable storage for days before assembly; the tampering window is open.
- **Hash-chain not anchored externally.** A purely internal hash chain can be re-forged if the entire system is compromised. External anchoring (transparency log, external notary, periodic publication of the head) prevents full re-forgery.
- **Over-reliance on Git signatures without identity rotation discipline.** Signing keys shared across the team; departed team members' keys not revoked; any committer is any committer.
- **Dashboard counts accepted without reconciling to the underlying store.** The most common place log-mutation goes undetected.
- **Hosted-model identifier accepted without response-header capture.** The provider mutates the model under the identifier; the engagement has no proof of the model at run time (chapter 6).
- **No tamper-detection drill.** The engagement assumes the file is intact; nobody re-computes the hashes until inspection, when it is too late to resolve.

## Summary

- Chain of custody is the engagement's defence of evidence integrity across time: identity, provenance, transit, custody, integrity, disposition — verifiable years later.
- WORM storage (S3 Object Lock Compliance mode, Azure Blob immutability, QLDB / Ledger tables, firm WORM) is the baseline. Land evidence in WORM at receipt, not at assembly.
- Hash-chained evidence manifests bind every event in the engagement's custody record to its predecessor; the head is anchored to an external transparency log where possible. The chain is append-only, signed at every append, walkable by the engagement-quality reviewer and inspectors.
- Git-pinned workpapers inherit content addressing; signed commits, branch protection, no history rewriting, signed checkpoint tags, and WORM mirror at cut-off keep the companion repo tamper-evident.
- Tamper signals the auditor runs skepticism on: back-dated commits, replaced artifacts, log mutation, "too-clean" patterns, boilerplate responses. ISA 240 skepticism is operated procedure-by-procedure.
- Retention is driven by the most restrictive applicable standard (ISA 230, AU-C 230, PCAOB AS 1215, sector overlays, jurisdictional overlays); destruction is under dual control after period expiry and no legal hold / open inquiry.
- Run the tamper-detection drill at engagement mid-point and at assembly cut-off; a failed drill is a required-resolution event, not a warning.
- With chapters 1–7, the AI Auditor has the evidence programme the rest of the module — AIMS auditing, model/system-card auditing, harm-model auditing, monitoring/incident auditing, supply-chain auditing, conformity assessment, reporting, and audit leadership — assumes as the working foundation.
