# exercise-05: Workpaper Authoring in Electronic and Git-Tracked Systems

**Estimated effort:** 3 hours

## Objective

Author a complete engagement workpaper node for a single AI-specific criterion, in both the electronic working-paper system shape (Caseware / TeamMate+ / Workiva / AuditBoard) and in the Git-tracked companion-repo shape. Produce the cross-references and sign-off scaffolding that a PCAOB-style inspector could walk years later.

## Prerequisites

- Chapter [`05-authoring-workpapers-electronic-and-git-tracked.md`](../05-authoring-workpapers-electronic-and-git-tracked.md)
- Chapter [`01-isa-500-evidence-applied-to-ai-artifacts.md`](../01-isa-500-evidence-applied-to-ai-artifacts.md)
- Chapter [`04-ai-evidence-inventory-original-derivative-corroborative.md`](../04-ai-evidence-inventory-original-derivative-corroborative.md)

## Scenario

Pick **one** of the three criteria below for the engagement; if you are running the module in sequence, pick the one that aligns with the system you worked with in exercises 01, 02, or 04 so the scenarios compose.

### Criterion A — Prompt-template governance for a clinical-note summarisation LLM

> "All production invocations of the clinical-note summarisation assistant during the audit period 2026-01-01 through 2026-09-30 used a prompt template formally approved by the AI Governance Committee, and no unapproved prompt-template revisions were deployed."

Available evidence: a Git repository with the committed prompt-template files, an immutable AIGC meeting-minutes repository, a trace-store carrying the SHA-256 of the prompt template used per request, a CI pipeline log history.

### Criterion B — Model-version promotion for a mortgage pre-approval model

> "Every model-version promotion to production during the audit period 2026-01-01 through 2026-09-30 was authorised by a Model Risk Committee member on the current authorisation matrix, had documented pre-promotion test suite results, and was recorded in the model registry with the model artifact hash."

Available evidence: the engagement's sampling workpaper (from exercise-02), an MLflow registry, a Jira project `MRC`, the Model Risk Committee charter and current authorisation matrix, pre-promotion test-suite outputs.

### Criterion C — Retriever-index refresh for a customer-service chatbot

> "The retriever index serving the customer-service chatbot during the audit period 2026-07-01 through 2027-06-30 was refreshed from the governance-approved source on the published cadence, and no unapproved source additions were present in the index at any period checkpoint."

Available evidence: the Airflow DAG history, the vector-store snapshot archive, the governance-approved source register, a quarterly index-audit script the organisation runs in-house, a monthly first-line health report.

## Requirements

1. **Electronic working-paper node.** Author the workpaper for the chosen criterion in a text file formatted as if it were the body of a node inside Caseware / TeamMate+ / Workiva / AuditBoard. Use the chapter-5 six-field shape (Objective / Criterion / Procedure / Evidence / Exception / Conclusion). Include preparer / reviewer / EQR identities (name placeholders are fine), dates, and cross-references. Length: 500–900 words.
2. **Companion-repo structure.** Lay out the matching companion-repo structure (chapter 5 §Working inside a Git-tracked repo). Create the directory tree and the required files, populating each with its expected content (the `README.md`, `engagement.yaml`, the per-criterion subfolder, the sample / reproduce / specialist / attestations / findings / manifests subfolders used for this criterion). You do not need to run anything; the expected content of each file is what you author.
3. **Manifest cross-references.** Include the `manifests/evidence-manifest.yaml` entry for this criterion — hashes (placeholder-format fine), retrieval paths, tier/grade, retention tag, and hash-chain sequence reference (forward to chapter 7).
4. **Sign-off log.** Author the `H.01` sign-off log entry showing preparer / reviewer / EQR sign-offs with dates and notes-cleared records. Include the branch-protection discipline the companion repo enforces to carry the sign-off into Git.
5. **Reviewer-walkability test.** Author a short note (≤ 200 words) addressed to the engagement-quality reviewer explaining how to walk the workpaper: start in the electronic system at the index node, pivot to the companion repo via the cross-reference, verify the evidence-manifest entry, re-compute a named hash, and clear the node. The note should show that a stranger can follow the trail.

## Starter guidance

- The six-field workpaper shape (Objective / Criterion / Procedure / Evidence / Exception / Conclusion) is the backbone; chapter 5 §Example workpaper is the reference.
- The companion-repo tree in chapter 5 §Working inside a Git-tracked repo is the template; adapt the directory names to the chosen criterion.
- Procedures are *verbs with objects*: "inspect", "re-compute", "reconcile", "re-run", "sample", "query" — not "review".
- Hash values can be short illustrative placeholders (`sha256:3d7a…`) — the schema and position are what matter, not real bytes.
- The conclusion addresses the assertion ("control operates throughout the period, with the exception of …") — not the completion of the procedure ("procedure performed").
- Where the scenario does not specify something you would need (team member names, exact MLflow schema), use `<!-- needs-research -->` or clearly marked placeholders.
- The reviewer-walkability note is the test that the workpaper is self-contained; think about what a stranger needs to know to walk it.

## Acceptance criteria

The deliverable is accepted when:

- The electronic workpaper covers all six fields (Objective / Criterion / Procedure / Evidence / Exception / Conclusion) plus cross-references and preparer / reviewer / EQR.
- The Procedure field is enumerated step-by-step with concrete artifacts and procedures (not generic prose).
- The Evidence field names every artifact with tier (chapter 4), grade (chapter 4), hash (placeholder), source, and retrieval path.
- The Conclusion addresses the assertion, not the completion of the procedure.
- The companion-repo tree matches the chapter-5 layout at the top level and includes at least `criteria/`, `samples/<criterion>/`, `reproduce/<assertion>/` or equivalent, `manifests/`, and `findings/`.
- At least one file in the companion repo carries actual content (e.g., a sample `selection.sql` or a reproducibility `manifest.yaml`); no files are left as pure stubs.
- The evidence-manifest entry includes tier, grade, hash placeholder, retrieval path, retention tag, and hash-chain-sequence reference.
- The sign-off log includes preparer, reviewer, EQR with dates and cleared notes; the branch-protection discipline is referenced.
- The reviewer-walkability note is ≤ 200 words and shows an end-to-end traceable path.
- No fabricated vendors, metrics, or identities.

## Stretch goals

- Author the **amendment protocol** (chapter 7 §Common failure modes names post-assembly amendments) — what the engagement would do if a dated-after-cut-off fact changed the conclusion; which commits land, which workpaper node is amended, how the original is preserved.
- Add a **PCAOB-style inspection walkthrough** for this single node — write the inspection prompts (12–15 of them) a reviewer would ask, with the expected location of the answer in the file.
- Write the **cross-engagement reuse memo** — when the next year's engagement picks up this criterion, how do the companion-repo tag and the workpaper node compose with the next year's work?
- Draft the **confidentiality and data-handling note** for the companion repo on this engagement — what secrets must not land in Git, what PII appears in trace-store excerpts, and the scanning discipline that catches leaks before commit.
