# The AI Evidence Inventory — Original, Derivative, Corroborative

## Motivation

Chapter 1 installed the ISA 500 reliability generalisations ("original is more reliable than transformed; independent is more reliable than entity-internal; auditor-direct is more reliable than inferred"). This chapter operationalises those generalisations into a working **evidence inventory** the engagement team carries across every AI audit — a three-tier taxonomy of *original*, *derivative*, and *corroborative* evidence, with concrete AI artifacts mapped to each tier and a reliability-grading rubric the workpaper uses to defend sufficiency.

The taxonomy is not a reskin of ISA 500. ISA 500 is the standard; the taxonomy is the *working shape* teams use so that every workpaper line has a tier, every tier has a procedure expectation, and the engagement-quality reviewer can walk the inventory in one page without re-deriving the reliability ladder from first principles. In AI engagements the taxonomy earns its keep because management's hand-over almost always leads with derivative artifacts (screenshots, pasted tables, model cards, dashboards) and the auditor needs a crisp reason to push back to the original.

## The three tiers, defined

- **Original evidence** — an artifact that *is* the source. It was produced by a process the auditor can reconstruct, it is content-addressable or append-only, and no human transcription lies between the artifact and its downstream use. Reliable under ISA 500 generalisation 5 (original > transformed) and often under 2 (entity-internal with controlled preparation) or 1 (independent external source). The auditor's goal on key assertions is to reach the original.
- **Derivative evidence** — a view, screenshot, export, excerpt, or paraphrase of an original. It exists for human consumption; it is not the source. Derivative evidence can be *useful* (it indexes, it summarises, it is cheap) but it does not bear load on its own. Under ISA 500 generalisation 5 it is weaker than the original it derives from. When the original exists and is reachable, substituting derivative for original is a professional-skepticism failure.
- **Corroborative evidence** — a second, *independent* source that supports (or contradicts) another piece of evidence. Its role is to raise or lower the reliability of what it corroborates, not to stand alone. An independent third-party eval that reconciles with management's internal eval *corroborates* the internal eval; an unaffiliated regulator notice that confirms an incident *corroborates* management's incident record. Under ISA 500 generalisation 1 (independent external > entity-internal), corroboration from external sources is the strongest form.

The three tiers are not mutually exclusive — an independently produced re-run can be both original (it is a source) and corroborative (it is independent of management's). The point of the taxonomy is to tag each artifact with its load-bearing role on the engagement.

## The AI artifact → tier mapping

The table below is the working inventory for an AI engagement. Each row names the artifact, the typical tier, the criterion types it supports, and a one-line reliability note. Chapter 1's artifact catalogue sits behind this view; chapter 5 shows how the inventory lands in the workpaper.

| Artifact | Typical tier | Supports criterion type | Reliability note |
|---|---|---|---|
| Git commit, signed tag, or signed release | Original | Change control, identity of config | Content-addressed, cryptographically signed when properly configured |
| In-toto / SLSA / Sigstore attestation of model build | Original | Model identity, build provenance | Externally verifiable; one of the strongest AI originals |
| Model artifact with content hash reconcilable to the registry | Original | Model identity, deployment provenance | Original when the registry and build pipeline chain back to Git |
| Dataset manifest with per-shard hash + datasheet | Original | Data governance, eval validity, fairness | Original when hashed and versioned |
| Eval run artifact (per-item outputs + config + seeds + env lock) | Original | Metric claims (accuracy, fairness, toxicity, latency) | Original when complete and reproducible |
| Trace-store record retrieved by auditor-authored query | Original | Operating effectiveness, policy application | Original when the store is append-only and the query is pinned |
| Immutable change ticket with artifact-hash cross-refs | Original | Change control | Original when the ticket system is append-only and the cross-refs resolve |
| Immutable incident ticket with artifact-hash and timeline cross-refs | Original | Incident mgmt, serious-incident reporting | Original under the same conditions |
| Infrastructure-as-code (IaC) config at the versioned commit used in deploy | Original | Config governance | Original; the deployed value is a corroborating runtime read-back |
| Access-log event under append-only retention | Original | Access control, segregation of duties | Original; retention and immutability must be validated |
| Vendor SOC 2 / SOC 3 / ISO 42001 certificate within scope and period | Corroborative (external) | Vendor control reliance | External-source corroboration; scope and period must match |
| Third-party bias audit / red-team / eval report commissioned independently of management | Corroborative (external) | Fairness, robustness, safety | Strong corroboration when the engaging party is independent of the AI owner |
| Regulator notice / inspection letter / public enforcement record | Corroborative (external) | Any criterion whose record is public | Strong corroboration under ISA 500 §A31(a) |
| Model card maintained by the model owner | Derivative | Narrative framing of a model | Not primary; a map to the artifacts |
| System card maintained by the application owner | Derivative | Narrative framing of a system | Not primary; a map to the artifacts |
| Monitoring dashboard screenshot | Derivative | Operating effectiveness | A view of the underlying query result; not primary |
| Pasted metric table in a slide deck or memo | Derivative | Metric claims | Entirely replaceable by the eval run artifact |
| Management-authored summary of incident counts | Derivative | Incident mgmt | A paraphrase; reach for the ticket chain |
| Management-authored audit response / representation | Derivative | Any | Not evidence of the control; evidence that management asserts the control |
| Independent re-run by the audit team | Original and corroborative | The specific metric claim | The single strongest upgrade to evidence appropriateness (chapter 6) |
| Interview notes from the first-line owner | Derivative | Conceptual understanding | Not primary; reach for documentary artifacts |

The inventory is not exhaustive; it is a *default view*. When a new AI artifact appears in an engagement (a trace-store format the auditor has not met before; a novel attestation shape), the engagement team places it in the inventory with the tier and the reliability note *before* using it as evidence.

## Reliability-grading rubric — four bands

The engagement workpaper carries a reliability grade on each piece of evidence. Four bands keep the grading defensible without over-engineering:

- **A — High reliability.** Original, auditor-direct or externally sourced, with controls over preparation that the engagement has tested or that can be presumed strong (signed cryptographic artifacts, independently maintained ledgers). Example: a Sigstore-verified model attestation reconciled to a Git-signed tag reconciled to a build pipeline the auditor can trace end-to-end.
- **B — Moderate reliability.** Original, entity-internal, with controls over preparation that have not been explicitly tested but that the control environment makes plausible (CI-produced eval artifacts in a MLflow instance that writes to retention-locked object storage). Example: an eval run artifact pulled from such a pipeline.
- **C — Limited reliability.** Derivative, or original but with weak controls over preparation (eval metrics in a shared drive with write access for the whole team; dashboard screenshots; vendor SOC 2 with a scope gap). Example: a model-card metric that cannot be traced to a reproducible run.
- **D — Insufficient.** Oral-only, uncorroborated management representations, or evidence that cannot be verified. Example: a verbal assertion that the eval was run quarterly with no artifact to point at.

Grades A and B can bear load for an audit conclusion. Grade C can corroborate but not stand alone. Grade D is not evidence. The engagement team writes the grade on the workpaper line for each artifact; the engagement-quality reviewer can walk the grades and spot where an A+C+C stack is really a C+C+C stack dressed up.

## The upgrade paths — moving evidence to a higher grade

The point of grading is to drive procedure. Each grade has a specific upgrade path:

- **From C to B** — reach for the original. Replace the dashboard screenshot with the query result; replace the model-card metric with the eval run artifact; replace the pasted table with the per-item output file.
- **From B to A** — add external corroboration or auditor-direct re-performance. Request the vendor's independent audit; request the regulator's public record; or perform the independent re-run (chapter 6). Verify the controls over preparation if not already tested.
- **From D to C** — ask for a written artifact that memorialises the oral representation; convert interview substance into a documentary fact; obtain management's written representation letter (not primary evidence, but memorialises the assertion for completeness).
- **Deciding not to upgrade** — if the risk is low and the materiality is loose, a C-grade piece of evidence may be acceptable; the workpaper records the decision not to upgrade with the risk-and-materiality justification.

## The scope-of-reliance line — what *not* to rely on

ISA 500 paragraph 11 requires the auditor to consider the reliability of information produced by the entity when the auditor is using it as evidence, including (A50-A52) the accuracy and completeness of the information and the controls over it. For AI engagements, three recurring "do-not-rely-on" postures:

- **Management attestations as evidence of control operation.** Management attests under the engagement letter that controls operated; the attestation memorialises the assertion. The attestation is not evidence that the control actually operated.
- **"Our dashboards say so" as evidence of a metric.** The dashboard is a view. The metric claim stands on the underlying data and the metric definition.
- **Model-card metrics as evidence of production performance.** Model cards usually cite eval-set metrics, not production metrics. A model card claim about production performance is a claim about a different population; verify the population first.

## Vendor attestations — the scope-and-period test

Vendor attestations (SOC 2 Type II, SOC 3, ISO/IEC 42001 certificate, bespoke AI-assurance reports) are corroborative external evidence when they are in scope — but "in scope" is not a one-line check. The scope test:

- **Period** — the attestation's audit period must overlap the engagement's audit period. For gaps, a **bridge letter** from the vendor's auditor (or a management representation if a bridge letter is unavailable) closes the gap; without either, the gap is a scope limitation.
- **Subject matter** — the attestation must cover the vendor's AI feature the engagement is relying on. SOC 2 scoped to "payroll processing" does not cover the vendor's AI summariser.
- **Trust services criteria / controls** — the specific TSCs or control objectives tested must align with what the engagement is relying on. A SOC 2 on security says little about the vendor's processing integrity on AI outputs unless processing integrity was tested.
- **Complementary user entity controls (CUECs)** — the attestation lists controls the user organisation must operate for the vendor's controls to be effective. The audit must verify the organisation operates its CUECs; failing to verify is a well-known scope gap.
- **Sub-service organisations** — the attestation names sub-service organisations and whether they are carved out or inclusive. For carved-out sub-service organisations, the audit must obtain separate reliance on those sub-service organisations' controls.

`mod-109-auditing-ai-supply-chain-and-third-party` operates this at depth; this chapter installs the gating test.

## Management representations vs. evidence — ISA 580 interface

**ISA 580 — Written Representations** (IAASB) and **AU-C 580 — Written Representations** (AICPA) require written representations from management at engagement conclusion. For AI engagements the representations cover items like "management has provided all AI systems in scope"; "management is unaware of material incidents during the period that have not been disclosed"; "management is unaware of pending regulator inquiries that have not been disclosed"; "management acknowledges responsibility for the design and operation of the controls covered by the engagement".

Representations are **required** but are **not a substitute** for other audit evidence on the matters represented. The engagement cannot conclude on fairness with a management representation that fairness was tested — the eval run artifact is the evidence; the representation memorialises management's assertion that the eval was run.

## Common failure modes

- **Over-weighting model cards.** Treating the model card as if it were the eval report; downstream readers of the audit assume the engagement verified the card's claims when the engagement only read them.
- **Dashboard screenshots stacked across the workpaper.** A workpaper full of screenshots passes a casual review and fails engagement-quality review. The originals must be reachable from the workpaper.
- **Corroboration without independence.** Using a vendor's self-report to corroborate the vendor's self-report. Corroboration requires a genuinely independent second source.
- **Grade stacking.** Four C-grade artefacts do not compose into an A-grade conclusion. Adding derivative evidence does not substitute for the original.
- **Period and scope misalignment on vendor attestations.** Accepting a SOC 2 Type II out of period, or out of subject-matter scope, as if it covered the engagement's reliance. Read the scope.
- **Treating management representations as evidence of the represented control.** Representations memorialise; they do not substantiate.
- **Not naming the tier and grade on the workpaper line.** Without the tier and grade, the engagement cannot defend sufficiency; the engagement-quality reviewer cannot aggregate.

## Summary

- The AI evidence taxonomy is three tiers — *original*, *derivative*, *corroborative* — mapped onto the AI artifact catalogue the engagement will meet in the field.
- Grade every piece of evidence A / B / C / D on reliability. A and B can bear load; C corroborates but does not stand alone; D is not evidence. The grade is on the workpaper line.
- Drive procedure by upgrade path: C→B is "reach for the original"; B→A is "add external corroboration or auditor-direct re-performance"; D→C is "memorialise the oral". Decide explicitly when *not* to upgrade.
- Vendor attestations corroborate externally but only within their scope and period; the CUEC is almost always a reliance gap waiting to happen.
- Management written representations under ISA 580 are required but are not substantive evidence for the matters represented.
- Next chapters: the workpaper that carries this inventory (chapter 5), the reproducibility bundle that upgrades metric claims from C/B to A (chapter 6), and the chain-of-custody discipline that keeps originals original across the engagement (chapter 7).
