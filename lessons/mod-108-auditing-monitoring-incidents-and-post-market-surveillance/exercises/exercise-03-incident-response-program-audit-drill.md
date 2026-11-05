# exercise-03: AI Incident-Response Program Audit Drill

**Estimated effort:** 3 hours

## Objective

Audit an organisation's **AI incident-response program** against the plural criteria chapter 3 enumerates — EU AI Act Article 73, NAIC Model Bulletin, FDA MDR (adapted for AI/ML SaMD), SR 11-7, ISO/IEC 42001 Clause 10.1, and NIST AI RMF MANAGE 4.3. Produce the four workpaper artefacts chapter 3 describes: the **incident-definition breadth test**, the **triage audit**, the **RCA-and-post-mortem quality audit**, and the **Clause 10.1 corrective-action-loop walk**.

This exercise is program-level. Exercise 04 reperforms the program against a sample of specific incidents.

## Prerequisites

- Chapter [`03-auditing-the-incident-response-program.md`](../03-auditing-the-incident-response-program.md).
- Chapter [`01-auditing-the-continuous-monitoring-program.md`](../01-auditing-the-continuous-monitoring-program.md) — monitoring is the main intake into incident response.
- `mod-105` chapter 9 on Clause 10.1 / 10.2.
- `mod-107` chapter 2 on the risk register (incidents feed register updates).

## Scenario

Pick one, or substitute. State the chosen subject at the top.

**Scenario A — EU GPAI-with-systemic-risk provider.** A frontier-lab-equivalent organisation that offers a general-purpose model with systemic risk and has adopted the GPAI Code of Practice. Incident programme spans Article 73 (through downstream high-risk deployers), AI Office reporting, Frontier Safety Framework post-incident processes, and SOC-2 auditor reporting to customers.

**Scenario B — US multi-state insurer.** A P&C insurer deploying AI for underwriting, claims triage, and fraud detection. In scope: NAIC Model Bulletin in six adopting states, SR 11-7 (model-risk-material), state insurance-commissioner direct reporting, state market-conduct regulators. One of the AI systems also has health-screening features triggering FDA SaMD interest. <!-- needs-research: confirm SaMD boundary for insurance health screening at reading time -->

**Scenario C — Medical-device SaMD manufacturer.** AI/ML-enabled medical device under FDA PCCP, CE-marked under MDR 2017/745 with EU AI Act high-risk classification, operating in the US and EU. In scope: FDA MDR, EU AI Act Articles 72–73, MDR Article 83 PMS, ISO 14971 risk-management integration.

## Requirements

1. **Pin the subject.** Record the organisation, its regulatory position across the criteria surface, the incident-management tooling (ServiceNow / Jira / PagerDuty / Opsgenie / GRC-for-AI platform), and the incident-policy document reference(s). Include the current incident-definition text verbatim.

2. **Incident-definition breadth test.** Produce a crosswalk table — rows are each applicable regulator's incident-trigger term (Article 3 serious-incident definition; NAIC "adverse consumer outcome"; FDA MDR "reportable event"; SR 11-7 "model issue"; Clause 10.1 "nonconformity"; NIST AI RMF MANAGE 4.3 "incidents and errors"); columns are "scope under the organisation's definition" (covered / partial / uncovered). Each `uncovered` row is a Day-1 finding candidate.

3. **Triage audit.** Request the triage policy, the triage SLA, the on-call rotation, and the intake channels. Produce:
   - A one-page triage-flow diagram or structured description.
   - A sample of five triage decisions from the audit period (randomly selected from the full triage log).
   - For each, verify named owner, time-to-triage against SLA, rubric citation, decision recorded, Article 73 applicability determination made (if system in-scope) within the first reporting window.

4. **RCA-and-post-mortem quality audit.** Sample at least five post-mortems from the period. For each, test:
   - RCA method named and applied.
   - Multi-layer causal analysis (model / system / process / external).
   - Counterfactual stated.
   - Evidence pointers to traces, logs, red-team reproductions, code commits.
   - Standard post-mortem structure.
   - Blameless framing of organisational causes.
   - Regulator-shareable summary section present (for Article-72-scope systems).
   - Sign-off by named authority.

5. **Permanent-regression-fixture back-feed audit.** For each sampled post-mortem, confirm the three-layer fixture: unit / integration test added, eval scenario added, monitor assertion added. Produce the commit SHAs or equivalent pointers. A post-mortem committing to add fixtures without the fixtures ever appearing is a Clause 10.1 closure defect.

6. **Clause 10.1 corrective-action loop walk.** For each sampled post-mortem, walk the five Clause 10.1 steps:
   1. React to nonconformity (immediate mitigation).
   2. Evaluate cause (RCA).
   3. Implement action.
   4. Review effectiveness.
   5. Change the AIMS, if necessary.
   Produce a table with one row per sampled incident and one column per step, with evidence pointer and status.

7. **Regulator-reporting quality review.** For any Article 73 / MDR / NAIC / SR 11-7 filings in the period, review the filing against:
   - Timeliness against the applicable reporting window.
   - Completeness against the required content.
   - Consistency with the internal post-mortem.
   - (Where relevant) non-contradiction with model-card and system-card public claims.

8. **Incident-taxonomy audit.** Confirm the organisation taxonomises incidents across harm category, root-cause layer, trigger source, severity grade, regulatory categorisation, and Chapter III Section 2 article (for high-risk systems). Audit a sample of five incidents for taxonomy consistency.

9. **Findings register.** Column shape identical to exercise 01, with a *criterion-source* column distinguishing Article 73, MDR, NAIC, SR 11-7, Clause 10.1, NIST AI RMF, and internal-policy findings.

## Starter guidance

- The definition-breadth test often surfaces Day-1 findings — organisations commonly inherit SecOps definitions that exclude AI-specific incidents like hallucination-at-scale or guardrail evasion.
- Clause 10.1 step 4 (effectiveness review) is the most commonly skipped step. Expect to find corrective actions closed in the tracker without an effectiveness-review artefact.
- "Blameless" is a cultural posture, not a required artefact; the auditor's test is whether organisational-cause analysis happens, not whether the word "blameless" appears.
- For Article 73 applicability determinations, the auditor is looking for a named role with regulatory-reporting authority — not a committee, not an engineer on the on-call rotation.
- Regulator filings can be reviewed in redacted form if the auditor's engagement letter permits; pre-arrange the redaction protocol.

## Acceptance criteria

The deliverable is accepted when:

- The subject and scope are pinned with the incident-definition verbatim.
- The incident-definition breadth test crosswalks every applicable regulator with a covered / partial / uncovered status per row.
- Triage audit samples five decisions with time-to-triage reperformance and Article 73 clock verification.
- RCA-and-post-mortem quality audit samples five post-mortems with multi-layer causal analysis evaluation.
- Permanent-regression-fixture back-feed audit produces commit / eval / monitor pointers for each sampled post-mortem.
- Clause 10.1 loop walk is a five-column × five-row (minimum) table.
- Regulator-reporting quality review covers every filing in the period (or documents the absence of filings with a population-completeness check).
- Incident-taxonomy audit tests consistency across five incidents.
- Findings are stated against the specific criterion-source.
- `<!-- needs-research: ... -->` is used where a factual claim cannot be verified from primary sources.

## Stretch goals

- Produce a **side-by-side comparison** of the organisation's AI-incident definition against the Partnership on AI AIID classification schema, identifying categories the AIID recognises that the organisation does not.
- Author a **sample-size and rationale memo** justifying the chosen sample under ISA 530 / AU-C 530, including the stratification decisions.
- Draft an **effectiveness-review template** for Clause 10.1 step 4 that the organisation could adopt, aligned to ISO/IEC 42001 Clause 10.1 and SR 11-7 ongoing-monitoring expectations.
- Build a **cross-regulator notification matrix** for a hypothetical incident that triggers Article 73, MDR, NAIC, and SR 11-7 reporting simultaneously, with the sequencing, content differences, and timing constraints the organisation would need to execute.
