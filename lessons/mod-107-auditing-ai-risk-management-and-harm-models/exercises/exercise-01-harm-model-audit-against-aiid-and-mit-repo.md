# exercise-01: Harm Model Audit Against the AI Incident Database and the MIT AI Risk Repository

**Estimated effort:** 2 hours

## Objective

Audit an organisation's documented **harm model** (or risk taxonomy) against five published corpora — the AI Incident Database, the OECD.AI Incidents Monitor, the MIT AI Risk Repository, the AIRO ontology, and the NIST AI 600-1 Generative AI Profile — and produce the two artefacts chapter 1 describes: a **completeness grid** with cell-level grounding, and a **harm → evaluation → control → monitor trace** for a sample of harms.

The deliverable reads like the workpaper a lead auditor would hand to the audit-committee pack as the opening section of the Stage-2 fieldwork report.

## Prerequisites

- Chapter [`01-auditing-the-harm-model-and-risk-taxonomy.md`](../01-auditing-the-harm-model-and-risk-taxonomy.md).
- `mod-102` on criteria translation (so the harm model terms can be mapped to the applicable obligation surface).
- `mod-104` on evidence discipline and sampling.

## Scenario

**Luminos Health** is a mid-size US regional health system deploying a clinical-decision-support tool it has built on top of a frontier-lab API (model vendor withheld in the public announcement). The tool reads clinical-note summaries, prior-encounter history, and insurance information, and produces a non-binding clinical-reasoning aid for the attending clinician. Luminos has published an internal "AI risk taxonomy" document, dated Q3 of the prior year, enumerating 24 harm categories organised around *clinical quality*, *patient safety*, and *regulatory exposure*.

You are the lead auditor on an ISO/IEC 42001-aligned internal audit engagement commissioned by Luminos's board AI committee. Your Stage-2 fieldwork opens with testing the harm model against external corpora.

For the exercise, you may use Luminos as given, or substitute the harm-model document from any organisation that has one published (OpenAI usage policies, Anthropic AUP, Google DeepMind safety framings, a healthcare-AI deployer's published AI governance document, a bank's AI policy, or your own employer's internal taxonomy with suitable redaction). State the chosen subject at the top of the deliverable.

## Requirements

1. **Pin the subject taxonomy.** Record the document name, URL or internal reference, retrieval date, hash (or version identifier), and the section headings. Note any `needs-research` where the subject is a draft or has superseded editions.

2. **Build the completeness grid** — a markdown table with the organisation's harm categories as rows and five columns: AIID, OECD AIM, MIT Repository domain, AIRO concept, NIST AI 600-1 category. For each cell record `covered` / `partial` / `uncovered` plus a citation (AIID case ID, OECD AIM record ID, MIT domain label, AIRO concept URI, AI 600-1 category name). Minimum: 20 harm-category rows (or justify a smaller taxonomy with a documented rationale).

3. **Spot-check five recent AIID incidents** from the last 12 months against the taxonomy. For each incident, record the incident ID, the harm category the taxonomy would place it in, and whether that placement is a *clean fit*, a *forced fit*, or an *orphan*. Orphans are parochialism findings.

4. **Spot-check each NIST AI 600-1 category** against the taxonomy. For every AI 600-1 category not represented, record whether the organisation has a scope-exclusion rationale and whether the rationale is defensible for the deployment.

5. **Run the trace test** on a sample of five harms. For each sampled harm, produce the four-column trace table:
   - Harm description (verbatim).
   - Evaluation locus (HarmBench behaviour / AIR-Bench category / AgentDojo task / InjecAgent category / WMDP subset / MLCommons AILuminate hazard / internal eval; or "none" as a finding).
   - Control locus (input / output / tool guardrail / policy / training mitigation).
   - Monitor locus (telemetry metric and alert rule).
   - Trace status (complete / broken at eval / broken at control / broken at monitor / monitor-off-target).

6. **Record findings.** Each parochialism observation, each AI 600-1 silent omission without rationale, each broken trace produces a finding. For each, record: finding ID, severity under the organisation's severity scale, affected harm category, criterion reference (which corpus or clause), evidence pointer, and recommended management response. Do not author the response.

7. **Record sampling justification.** Which stratification you used, which population you sampled from, and the resulting assurance level. ISA 530 / AU-C 530 shape.

## Starter guidance

- Chapter 1's "common failure modes" list the patterns you are likely to encounter; do not merely replicate the chapter's examples, but use them as a mental checklist.
- Use the public-corpus wording in the grid (e.g., "Privacy & Security" rather than a paraphrase); the grid is for traceability to the published source.
- An AIID "spot-check" is not a comprehensive coverage test — the goal is to see whether the taxonomy *can* represent a representative sample of real recent incidents.
- When a harm trace breaks at the monitor layer, often the monitor exists elsewhere (in chapter 5 fairness programme or chapter 7 guardrail) without the taxonomy knowing. Record both.
- Where you find a clean trace, keep the table row — audit evidence is as much about confirming what works as flagging what doesn't.

## Acceptance criteria

The deliverable is accepted when:

- The subject taxonomy is pinned (URL / reference, retrieval time, version or hash).
- The completeness grid has at least 20 rows, and the five-column coverage is populated with a citation per non-empty cell (not just `yes` / `no`).
- At least one `uncovered` cell is identified per the AIID / AIM / 600-1 columns, or the taxonomy is honestly comprehensive and that fact is stated.
- The five AIID spot-checks are present with orphan calls.
- Every NIST AI 600-1 category not represented has either an organisation-documented exclusion rationale or a finding.
- The trace table covers at least five sampled harms with full four-column entries and a trace-status column.
- Each finding has a severity classification against the organisation's scale (or a note that the scale is absent and that is itself a finding).
- Sample selection and sample size are justified per `mod-104` discipline.
- No incident, benchmark, or criterion is cited without a primary reference; `<!-- needs-research: ... -->` is used where a claim cannot be fully pinned.

## Stretch goals

- Build a small Python / shell script that pulls the current AIID RSS or API feed and automatically flags incidents from the last 90 days that do not map to any of the organisation's harm categories (parochialism-drift monitoring).
- Draft the one-page **management response template** the organisation would use to rebut or accept each category of finding you identified (parochialism, omission without rationale, broken trace).
- Produce a **version-diff** across the taxonomy's publication history — pull the prior version and flag which categories were added, retired, or re-scoped. This surfaces whether the organisation's harm-model-authoring process is itself alive.
- Draft the **crosswalk artefact** mapping the organisation's harm model to ISO/IEC 23894 Clause 6 risk-source categories, so that the chapter-2 register audit can consume the same mapping.
