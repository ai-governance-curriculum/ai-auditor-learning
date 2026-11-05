# exercise-07: Independent Replication Report Authoring

**Estimated effort:** 1 hour (short, but it is the capstone — do not shortcut structure or payload discipline)

## Objective

Produce the **independent replication report** that bundles exercises 01–06 into a single, multi-audience, signed deliverable: cover, executive summary, scope, approach, scope restrictions, results, findings, opinion/conclusion, appendices. The report is written to chapter-7 shape and to the attestation body the engagement runs under.

## Prerequisites

- Chapter [`07-the-independent-replication-report.md`](../07-the-independent-replication-report.md).
- Completed exercises 01–06, with their workpapers available.
- A chosen attestation body — for this exercise pick one of: IAASB ISAE 3000 (reasonable or limited), AICPA SSAE-19 (examination or review), NYC LL144 bias audit, or ForHumanity IAAIS. Document the choice at the top of the report.

## Scenario

Final deliverable of the Harbor-Triage-v2 (or your chosen subject) engagement. The audit committee has asked for a single document that:

- states the auditor's opinion or conclusion in the shape appropriate to the attestation body;
- cross-references every finding to its underlying workpaper;
- is suitable for the committee's internal review *and* produces a regulator-variant and a vendor-variant from the same source;
- discloses no adversarial payloads to unauthorised audiences.

## Requirements

1. **Produce the report in Markdown** (or an equivalent rendering target) with the thirteen chapter-7 sections:

   1. Cover and attestation.
   2. Executive summary (one page).
   3. Scope and criteria.
   4. Approach.
   5. Scope restrictions and limitations.
   6. Claim register and auditability grading (summary + full in appendix).
   7. Replication results.
   8. Calibration-methodology appendix (from exercise-06).
   9. Fairness audit (from exercise-04).
   10. Robustness / privacy / red-team audit (from exercises 03 and 05).
   11. Findings register.
   12. Auditor's opinion or conclusion.
   13. Appendices.

2. **Author the opinion / conclusion sentence** in the shape required by the chosen attestation body. For ISAE 3000 reasonable-assurance: "In our opinion, the published claims …"; for ISAE 3000 limited-assurance: "Based on the procedures performed, nothing has come to our attention …"; for ISO/IEC 17021-1 certification: a conclusion plus a certification recommendation; for LL144 bias audit: the computed impact ratios plus an independence statement; for ForHumanity IAAIS: a reasoned certification decision.

3. **Produce three variants from a single source**:
   - **audit-committee variant** (10–20 pages, including appendices; redacted payloads; hashes referenced);
   - **regulator variant** (shape appropriate to the chosen attestation body; in the LL144 case, the publication-shape BABL AI report);
   - **vendor variant** (full disclosure, including manifests, raw-artefact references, finding-register cross-links).
   
   The variants may be rendered from a single Markdown with conditional sections, or submitted as three files sharing a source-of-truth block. Whichever approach you take, the three variants carry the same finding IDs and the same signed-delta rows; only prose and payload disclosure differs.

4. **Apply the adversarial-payload discipline.** Every payload-bearing artefact appears only as:
   - a disclosure-class label;
   - a SHA-256 (or longer) hash;
   - a WORM-store reference;
   - an attack-class and outcome disclosure.
   
   No payload text appears in any variant visible outside the vendor variant.

5. **Sign the report.** For exercise purposes:
   - engagement-partner signature line (identity, engagement ID, date-time);
   - independent-reviewer signature line (identity, date-time);
   - subsequent-events statement (if applicable);
   - signed manifest-of-manifests (one YAML file listing every replication-manifest ID and its hash, signed by the engagement partner).

6. **Workpaper-to-report trace.** Every factual sentence in the report cites the workpaper it rests on (exercise-01 register row ID, exercise-02 manifest ID, exercise-03 matrix cell, exercise-04 table row, exercise-05 workpaper reference, exercise-06 appendix row). The trace format is consistent across the report; a reader should be able to walk from an executive-summary assertion to the raw artefact without ambiguity.

## Starter guidance

- Keep the executive summary to a single page. The opinion or conclusion sentence must appear on the first page.
- Scope restrictions belong on the first page or very early in the main body, not buried in an appendix. The reader must not reach the opinion before seeing the restrictions.
- The findings register condenses chapters 1–6 — at most a few dozen rows per typical engagement. Each row: finding ID, grade (major / minor / observation), criterion, condition, evidence reference, management response placeholder.
- Variants from a single source: a lightweight approach is a top-level Markdown with `[audit-committee]`, `[regulator]`, `[vendor]` section tags and a render script. For the exercise you may produce three files; keep them visibly consistent.
- Signatures need not be real digital signatures for the exercise. A signature line (`signed_by: ...`), a date-time, and an identifier is sufficient; a production engagement would use cosign / PGP / an attestation-body-approved method.
- Do not substitute "red-team" for "we ran garak." Attribute the toolchain explicitly; chapter 7's borrowing-and-attribution discipline is binding.
- Do not design the mitigation. The report states the finding. The management response placeholder is `<management response TBD — see mod-111>`.

## Acceptance criteria

The deliverable is accepted when:

- The report has all thirteen chapter-7 sections.
- The opinion or conclusion sentence is in the correct shape for the chosen attestation body and appears on the first page.
- All scope restrictions appear in section 5 (and are summarised in the executive summary).
- The three variants (audit-committee, regulator, vendor) are present and consistent — same findings, same deltas, different disclosure.
- No payload text appears in any variant visible outside the vendor variant.
- Every factual sentence traces to a workpaper (exercise-01 through exercise-06).
- Signatures (engagement partner, independent reviewer), date-times, and the manifest-of-manifests are present.
- The findings register is populated — every chapter-6 pattern finding candidate and every chapter-4 weak-graded claim is at minimum an observation.
- The language is skeptical, specific, and attributed; no ad-hominem phrasing; no hidden qualifier; no leaked payload.
- The report would survive an independent-reviewer re-read without the reviewer needing to open a restricted-variant artefact.

## Stretch goals

- Author the **management-response matrix** template the engagement hands the vendor — one row per finding, columns for root cause, corrective action, closure evidence, target date — in the shape `mod-111` operationalises.
- Author the **regulator-variant cover letter** — a half-page professional letter to the regulator (NYC DCWP, EU AI Office, FDA) accompanying the submission.
- Produce a **report-build Makefile or small render script** that materialises the three variants from a single source; include the signature-and-hash step in the pipeline.
- Draft the **"two-year retention and access-control plan"** for the engagement's workpaper and WORM artefacts — who may access what variant, for how long, under what approval; this is often the audit committee's follow-up question.
- Cross-walk the report's findings register to **ISO/IEC 42001 clauses and Annex A controls** (via `mod-105` chapter 6) so the engagement doubles as input to the AIMS audit; this is the most common second use of the card-claim audit's output.
