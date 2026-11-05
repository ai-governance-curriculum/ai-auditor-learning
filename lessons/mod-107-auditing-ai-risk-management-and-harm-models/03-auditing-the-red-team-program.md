# Auditing the Red-Team Program — Charter, Coverage, Cadence, and Closure

## Motivation

Red-teaming an AI system is now a routine artefact of a responsible-AI programme; every major release of a foundation-model-backed product carries a red-team report, and the EU AI Act Article 15 and NIST AI 100-1 "Manage" both read as if red-teaming is assumed. For the auditor the question is sharper than "did the organisation red-team?" — the question is whether the red-team *programme* is sufficient and reliable enough that the audit committee can rely on its outputs to understand the residual risk the organisation is accepting.

The auditor does *not* re-author the red-team program. Program authoring, novel attack cataloguing, and the threat-model-to-attack mapping sit with `ai-risk-engineer` (L25); the frontier capability-elicitation work sits with `agentic-safety-engineer` (L40). The auditor tests five properties of the programme: **charter**, **coverage**, **tool portfolio**, **cadence**, and **closure**. Each property has a canonical audit procedure.

## The charter test

Every reliable red-team programme has a written charter. The charter fixes scope, authority, independence, and reporting. The auditor tests:

- **Scope statement.** Which systems, which model versions, which deployments, which attack classes, which jurisdictions. A charter that silently excludes the deployed version from scope is a finding.
- **Authority.** Does the red team have data access, system access, and network egress to execute the planned attacks against the real system (or a representative pre-production replica)? Red teams restricted to a chatbox-only test posture cannot test tool-use, retrieval, or multi-modal paths.
- **Independence.** Are the red-teamers independent of the model trainers and the product team? Full independence is rare (and often implausible for the first wave of frontier-model internal red-teaming); the auditor records the degree of independence and whether external augmentation (ML-Cyber contractor, UK AISI, external red-team vendors) is retained.
- **Reporting line.** To whom does the red team report findings — the product team, the CISO, the audit committee? The reporting line should match the appetite statement (chapter 2); a red team whose findings route only to the team they tested is a governance finding.
- **Rules of engagement.** Which attack classes are authorised; which are prohibited; which data is in scope; which third-party systems may be interacted with; what the incident protocol is if a real harm emerges.
- **Deliverables.** What the red team produces at each engagement — a tracker of findings, a report, an executive summary, a reproduction bundle, a remediation closure record.
- **Quality assurance.** How the red-team outputs are themselves QA'd (peer review, calibration against known-plant attacks, inter-team agreement).

A charter missing any of the seven elements above is a documentation finding before the auditor tests a single attack.

## The coverage-matrix test

The coverage matrix is the auditor's most important red-team artefact to request. A coverage matrix is a two-dimensional (or three-dimensional) table that records every attack class the organisation has deemed in scope, cross-tagged to the external taxonomies. Industry convention at the time of writing cross-tags against:

- **OWASP Top 10 for LLM Applications.** Prompt injection (LLM01), sensitive-info disclosure (LLM02), supply-chain (LLM03), data/model poisoning (LLM04), improper output handling (LLM05), excessive agency (LLM06), system-prompt leakage (LLM07), vector/embedding weaknesses (LLM08), misinformation (LLM09), unbounded consumption (LLM10). <!-- needs-research: confirm current OWASP LLM Top 10 edition numbering at reading time; 2023 release numbered differently from 2024/2025 releases -->
- **OWASP Top 10 for Machine Learning.** ML01 input manipulation, ML02 data poisoning, ML03 model inversion, ML04 membership inference, ML05 model theft, ML06 corrupted packages, ML07 transfer learning, ML08 model skewing, ML09 output integrity, ML10 model poisoning. <!-- needs-research: confirm current OWASP ML Top 10 numbering at reading time -->
- **MITRE ATLAS.** The Adversarial Threat Landscape for Artificial-Intelligence Systems — a MITRE ATT&CK-style tactic-and-technique matrix covering reconnaissance, resource development, initial access, ML model access, execution, exfiltration, impact against AI systems. (`atlas.mitre.org`)
- **NIST AI 100-2 (Adversarial Machine Learning).** The NIST taxonomy of ML attacks: evasion, poisoning, privacy, abuse, and the sub-divisions by access level (white-box / grey-box / black-box) and by target (availability / integrity / privacy). <!-- needs-research: confirm the NIST AI 100-2 edition in force at reading time; the 2023 release and 2024 "e" revision differ in scope -->
- **HarmBench behaviours.** Mazeika et al. 2024 HarmBench enumerates ~400 behaviours across cybercrime, chemical, biological, misinformation, harassment, illegal activity, and refusal-bypass categories; coverage is tested per-category.

The coverage matrix the auditor expects to see:

| Attack class | OWASP LLM | OWASP ML | MITRE ATLAS | NIST AI 100-2 | HarmBench | In-scope? | Last run | Owner |
|--------------|-----------|----------|-------------|----------------|-----------|-----------|----------|--------|
| Indirect prompt injection via document | LLM01 | — | AML.T0051.001 | Evasion (black-box) | — | yes | 2026-09 | red-team |
| CSAM elicitation via roleplay | — | — | AML.T0051.002 | Abuse | harassment-csam subset | yes | 2026-10 | red-team |
| Membership inference via output LL scoring | — | ML04 | AML.T0024 | Privacy | — | partial | 2026-07 | ai-risk-eng |
| … | … | … | … | … | … | … | … | … |

The auditor's tests on the matrix:

1. **Taxonomic completeness.** Every OWASP LLM Top 10 category appears as at least one row; every OWASP ML Top 10 category appears as at least one row (for ML systems); MITRE ATLAS techniques relevant to the deployment appear as rows; NIST AI 100-2 attack families cover the deployment. Silent omission of a category is a finding; an "out-of-scope" rationale must be documented.
2. **In-scope rationale.** For each row, the "in-scope" decision has a documented basis — either a harm-model linkage (chapter 1), an eval benchmark it maps to (HarmBench / AIR-Bench / AgentDojo / InjecAgent), or a threat model.
3. **Recency.** "Last run" is within the methodology-declared cadence; a row that has not run in the declared window is a cadence finding.
4. **Owner.** Each row has a named owner (second-line or first-line); unowned rows are a finding.
5. **Linkage to the register.** Each in-scope row maps to a register row (chapter 2); orphan rows (in the matrix, not in the register) or vice-versa are trace-drift findings.

Depth on *what* each attack is sits in `ai-risk-engineer` (L25) and `mod-102` (criteria translation). The auditor tests that the matrix is complete and current.

## The tool-portfolio test

The organisation's red team runs its attack catalogues through tools. The auditor tests the portfolio against the industry-canonical open-source corpus:

### Canonical tools the auditor should recognise

- **garak** (`github.com/leondz/garak`, now under NVIDIA stewardship) — LLM vulnerability scanner for prompt injection, jailbreak, encoding, and leakage probes. The auditor expects garak evidence for LLM-01-through-LLM-07-shaped risks.
- **PyRIT** (`github.com/Azure/PyRIT`) — Microsoft AI Red Team's open-source framework for orchestrating multi-turn red-team conversations. The auditor expects PyRIT evidence for multi-turn and agentic red-team runs.
- **Promptfoo** (`github.com/promptfoo/promptfoo`) — evaluation and red-team harness with jailbreak suites. The auditor expects Promptfoo evidence for CI-gated red-team checks.
- **Inspect** (`github.com/UKGovernmentBEIS/inspect_ai`) — UK AI Security Institute's evaluation framework; HarmBench, AgentDojo, InjecAgent can be run through Inspect. The auditor expects Inspect runs as the reproducible evidence of record.

A programme that relies on one tool is likely under-covering; a programme that uses all four is likely well-covered but the auditor still checks that each tool is used for what it is best at. A programme that uses *no* reproducible tool and relies entirely on manual red-team notes is a reliability finding.

### Tool-evidence tests

For each listed tool in the programme:

- **Version pin.** The tool's exact release (or commit hash) is recorded for each run.
- **Suite pin.** The attack suite (garak probe list, PyRIT prompt set, Promptfoo configuration, Inspect benchmark) is version-pinned.
- **Environment pin.** Python version, model version, decoding configuration (temperature, top-p, seed where set).
- **Result capture.** The raw output log (attack prompts, model responses, judgement verdicts) is stored in WORM-capable evidence storage (`mod-104`).
- **Judgement capture.** If an LLM-judge is used, its identity, prompt, and version are recorded; the auditor applies chapter-4 calibration (mod-106) to the judge.

A run without a version pin is not reproducible; a non-reproducible run is thin evidence.

### Vendor tools and commercial platforms

Many organisations use commercial red-team platforms in addition to the open-source corpus. The auditor records the vendor and tests vendor attestations the same way `mod-109` tests any third party (vendor's SOC 2 / ISO 27001 / 42001 status, data-handling terms, attack-library provenance, false-positive / false-negative calibration data if available). Commercial platforms are *supplementary* to the open-source evidence stream, not a substitute.

## The cadence test

Red-teaming is a recurring activity, not a one-off. Cadence expectations the auditor validates against the organisation's methodology:

- **Pre-release red-team.** A full red-team run against the release candidate before promotion to production; for frontier systems this is the subject of the Responsible Scaling Policy / Preparedness Framework pre-deployment evaluation (chapter 8). Missing a pre-release red-team is the most severe cadence finding.
- **Post-release periodic red-team.** The organisation's methodology declares the cadence (quarterly / semi-annual / annual / triggered); the auditor samples prior-period evidence to confirm execution at the declared cadence. A programme with a declared quarterly cadence that has produced two runs in the last twelve months is in breach.
- **Trigger-based red-team.** Material deployment changes (new model version, new tool, new jurisdiction, new user segment) should trigger a targeted red-team run; the auditor samples recent material changes and confirms a targeted run followed.
- **External augmentation cadence.** Where the programme includes external red-team support (UK AISI, AI-Security contractor, DEF CON AI Village-style sprint), the cadence of that augmentation is audited to the methodology.

### Cadence sampling

The auditor's cadence procedure:

1. Pull the methodology's declared cadence table.
2. For each row, pull the last three executed runs and their artefacts.
3. Confirm each run meets the declared time window, scope, and output.
4. Record cadence deviation as a finding.

A programme with "when we feel like it" cadence is a methodology finding first; the execution tests follow.

## The finding-triage test

A red-team run produces findings. The triage process the auditor expects:

- **Finding intake.** Each red-team-discovered issue is logged in a tracker (JIRA, GitHub issues, custom workflow) with severity, affected system, reproduction steps, evidence links.
- **Severity classification.** Findings are classified per the organisation's severity scale (same scale as the register, ideally — otherwise a cross-mapping is documented). The auditor samples findings and reperforms the severity classification.
- **Triage decision.** Each finding has a triage decision — accept, mitigate, defer, close-as-duplicate, close-as-not-reproducible — with the rationale and the deciding owner recorded. Silent "won't fix" closures are a finding.
- **Correction linkage.** Findings designated for mitigation link to a change ticket, a control update, a model retraining, or a guardrail update. Findings with no linked corrective action after the declared triage window are a closure finding.
- **Re-test on remediation.** Each remediated finding is re-tested (ideally by the red team, not by the development team) to confirm the finding no longer reproduces. A finding closed without a re-test is a closure finding.

Chapter 2's risk-register testing and this chapter's triage testing meet at one point: a red-team finding must either (a) feed a register row, or (b) be documented as below the register-threshold with explicit rationale.

## The evidence-of-execution test

The chapter's hardest audit test is whether the red-team programme *actually executes* at the claimed depth, as opposed to producing a report that reads like a red-team report but with thin evidence underneath. Procedures:

- **Request the raw run logs for a sample of recent runs.** Not the executive summary — the raw tool output. Compare against the summary; a summary that mentions findings not present in the raw log is a finding (and a serious one).
- **Spot-reproduce one or two attacks.** Within the auditor's independence envelope (mod-106 chapter 6 and mod-104 chapter on specialist use), the auditor reruns one or two of the organisation's reported attacks against the current system and confirms reproduction or documents the delta.
- **Compare to a public baseline.** For the common attack catalogues (HarmBench behaviours, AgentDojo tasks, InjecAgent tasks), the auditor is not surprised to see the organisation's results; the auditor is surprised if the organisation reports attack-success-rates that diverge materially from published baselines for comparable models. A large undisclosed delta is a calibration finding.
- **Check for payload discipline.** Red-team payloads are sensitive; the auditor confirms the organisation handles them per `mod-104` adversarial-payload discipline, with WORM storage, access control, and non-disclosure to unauthorised audiences.

## Common failure modes

- **Charter-less red-team programme.** A programme that functions on institutional habit rather than a written charter cannot be relied on at audit-committee level.
- **Matrix out of date.** The coverage matrix was built eighteen months ago and has not been updated for OWASP LLM Top 10 2025 or the current ATLAS techniques.
- **Report-only evidence.** The red-team report is well-written but the raw run logs do not exist or are not retained.
- **LLM-judge without calibration.** The programme relies on LLM-judge verdicts to grade attack success without the kappa / agreement-with-human analysis (mod-106 chapter 4).
- **Tool bias.** The programme uses only one tool and so only finds the attacks that tool is good at.
- **Triage queue purge.** Old findings are closed as "no longer reproducible" without a reproduction attempt.
- **Findings never reach the register.** The triage lives in a parallel universe from the chapter-2 register; the audit committee sees one view, the red team sees another.
- **External red-team findings are "filtered."** The external red-team's own report is not shared with the audit committee; only the internally rewritten summary is. This is a governance finding against independence.

## Summary

- Five properties of a red-team programme are the auditor's targets: charter, coverage, tool portfolio, cadence, closure.
- The coverage matrix cross-tags attack rows against OWASP LLM Top 10, OWASP ML Top 10, MITRE ATLAS, NIST AI 100-2, and HarmBench; silent omissions are findings.
- The tool portfolio is expected to cover garak, PyRIT, Promptfoo, and Inspect at minimum, each with version-pinned suites and WORM-stored run logs.
- Cadence is driven by the organisation's own methodology — pre-release, periodic, trigger-based, and external-augmentation — and sampled by the auditor against the declared cadence table.
- Finding triage must link each red-team finding into the chapter-2 register or close it with a documented rationale.
- Evidence-of-execution is tested against the raw run logs, not the summary; the auditor spot-reproduces at least one attack within the independence envelope.
- The auditor does not re-author the programme — authoring sits with `ai-risk-engineer` (L25). The auditor tests sufficiency and reliability.
