# exercise-02: NIST AI RMF + GenAI Profile to Criteria

**Estimated effort:** 3 hours

## Objective

Translate a selected cross-section of **NIST AI RMF 1.0** Subcategories plus the **NIST AI 600-1 Generative AI Profile** overlay into auditable criteria using the chapter-1 template. The deliverable is a criteria register that could support an **AT-C 205 examination** (positive-assurance opinion) over a GenAI service organisation's AI safety program.

## Prerequisites

- Chapter [`01-what-makes-a-criterion-auditable.md`](../01-what-makes-a-criterion-auditable.md).
- Chapter [`03-nist-ai-rmf-and-genai-profile-to-criteria.md`](../03-nist-ai-rmf-and-genai-profile-to-criteria.md).
- **NIST AI RMF 1.0** and the **AI RMF Playbook** (NIST AI Resource Center) and **NIST AI 600-1** (Generative AI Profile) read end-to-end before starting.
- Chapter [`05-iaasb-and-aicpa-attestation-stack.md`](../../mod-101-audit-position-and-independence/05-iaasb-and-aicpa-attestation-stack.md) for the AT-C 205 engagement shape.

## Scenario

**AuriAI** is a fictitious US-based foundation-model provider that offers an LLM inference API to enterprise customers. It is engaging a Big-4 firm (where you are the engagement lead) to perform an **AT-C 205 examination** of its AI safety program for the period 1 Jan 2026 – 31 Dec 2026. The resulting report will be relied on by AuriAI's enterprise customers under their third-party-risk programs; distribution is not public.

Scope in scope for the examination:

- Pre-release safety evaluation of each model release (text + multimodal).
- Red-team / adversarial testing program (jailbreak, prompt-injection, dangerous-content elicitation, CBRN-screening where applicable).
- Content-safety classifier posture and policy routing.
- Post-release monitoring (abuse detection, incident tracking).
- Training-data provenance and PII posture (summary-level; deep data audit is out of scope).
- Serious-incident response and customer notification.

Out of scope for the examination:

- Infrastructure security (covered by a separate SOC 2 report).
- Financial controls.
- Model intellectual-property posture.

## Deliverables

1. **Criteria register** — chapter-1 template, with explicit coverage across:
   - **GOVERN**: at least three Subcategories (including GOVERN 6.1 third-party).
   - **MAP**: at least three Subcategories (including MAP 1.1 intended purpose and MAP 5.1 impact).
   - **MEASURE**: at least six Subcategories (including MEASURE 2.3, 2.6, 2.7, 2.11 at minimum).
   - **MANAGE**: at least three Subcategories (including MANAGE 4.1 post-deployment monitoring).
   - **GenAI Profile overlay**: at least four GenAI risk areas (confabulation; information security; information integrity; one other of your choice).
2. **Playbook evidence-candidate list**. For each MEASURE and GenAI Profile criterion, extract the AI RMF Playbook "Suggested Actions" that map to the Subcategory and list them as *evidence candidates* in the register's Evidence column (chapter 3 §"turning suggested actions into evidence expectations"). The Playbook is not the normative source; you are mining it for evidence shape.
3. **Suitability memo** (~500 words). Under ISAE 3000.A45 / AT-C 105 .25 suitability tests (relevant, complete, reliable, neutral, understandable), argue why NIST AI RMF (a voluntary framework without a conformance definition) is suitable criteria for this engagement — or where it is not and the engagement must adopt *specifically developed criteria* that extend the NIST baseline. Cite the AT-C 105 paragraph(s) you rely on.
4. **AT-C 205 report-form sketch** (~300 words). Draft the opinion paragraph of the examination report using the AT-C 205-prescribed positive-assurance language, naming the criteria you have authored. Do not write the full report; the opinion paragraph plus the criteria citation is enough to confirm the register aligns to the reporting standard.

## Minimum volume

- At least **15 criteria** across the Core.
- At least **6 criteria** in the GenAI Profile overlay.
- At least **8 measurable** criteria carrying metric + method + population + tolerance explicitly.
- At least **3 criteria** that depend on an auditor's ML/eval/red-team expert under ISA 620 analogy — flagged with expert scope.

## Starter guidance

- The MEASURE 2 cluster is the richest; do not write one catch-all criterion — split by trustworthy characteristic (accuracy, safety, security, fairness, privacy, explainability). Each gets its own metric / method / population.
- For the GenAI Profile, use the NIST AI 600-1 risk-to-action tables to see which Subcategories carry which GenAI actions; author criteria that cite the Subcategory as the Core anchor and the GenAI Profile risk as the overlay context.
- The scope excludes infrastructure security — do not author criteria that tread on the companion SOC 2. Flag the boundary in the suitability memo.
- Criteria for red-team / adversarial testing need a documented threat model; cite NIST AI 100-2, MITRE ATLAS, OWASP LLM Top 10 as the common reference pools, but let AuriAI name the suite in evidence rather than pre-naming it in the criterion.
- The AT-C 205 report-form sketch must match the examination-engagement language ("in our opinion, [subject matter] is fairly stated, in all material respects, in accordance with [criteria]") — not SOC 2 report language.
- Period framing matters. Every criterion is scoped to the 1 Jan 2026 – 31 Dec 2026 examination period.

## Acceptance criteria

The deliverables are accepted when:

- The criteria register uses the full chapter-1 template; no field is blank.
- Volume thresholds (15 + 6 criteria; 8 measurable; 3 expert-dependent) are met.
- Every criterion cites a specific Subcategory ID (e.g., MEASURE 2.11, not "MEASURE 2").
- GenAI Profile criteria cite both the Core Subcategory and the GenAI risk area.
- Playbook evidence candidates are referenced, not pasted as criteria (the Playbook is non-normative).
- The suitability memo applies all five AT-C 105 .25 tests and cites the standard.
- The report-form sketch uses AT-C 205 opinion-paragraph language and names the criteria correctly.
- Evidence columns name concrete artifacts (eval suite config, run log, threat-model document, finding ticket, remediation record) — not placeholder nouns.
- Any claim about current NIST AI RMF revisions, Playbook entries, or GenAI Profile risks that is not in the publications cited is marked `<!-- needs-research: ... -->`.

## Stretch goals

- Add a **re-performance sampling plan** per measurable criterion: how many items would you re-run on an independent evaluation set, with what statistical basis per ISA 530 analogy.
- Draft the **auditor's expert engagement letter paragraph** for the red-team / adversarial-testing expert, with scope, competence, objectivity, and review arrangements under ISA 620 analogy.
- Produce a **companion criteria set** for the companion SOC 2 report so the two reports do not overlap or contradict on infrastructure-security evidence — show the boundary.
- Draft the **management assertion** AuriAI's responsible party will sign, consistent with your criteria.
