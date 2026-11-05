# Auditing AI System Impact Assessment — Clause 6.1.4 and ISO/IEC 42005, with EU AI Act Article 27 Cross-Check

## Motivation

AI system impact assessment is where the AIMS crosses from internal risk-to-the-organisation framing into risk-to-people-and-society framing. **Clause 6.1.4** of ISO/IEC 42001 requires the organisation to define and apply a process to assess potential consequences for individuals, groups, and societies arising from AI system development or use. **ISO/IEC 42005** is the method reference for *how* to conduct that assessment, authored by the same SC 42 committee so the two standards compose cleanly. In parallel, the EU AI Act, in **Article 27**, requires certain deployers of high-risk AI systems to perform a fundamental-rights impact assessment (FRIA); where the organisation is in that scope, the FRIA and the ISO/IEC 42005 impact assessment overlap substantially and are often satisfied by a single, superset artifact.

The auditor's job: test that the impact-assessment process is defined, executed per the procedure, completed for every in-scope system, and that the outputs route into risk treatment (6.1.3), controls selection (Annex A and SoA), and operational monitoring (clause 9.1). Impact-assessment defects are among the most consequential findings an AIMS audit can raise because they signal the AIMS cannot speak to the risks the standard is primarily about — risks to affected people.

## Clause 6.1.4 — the audit requirement

**Requirement.** The organisation shall define and apply a process to assess the potential consequences for individuals, groups of individuals, and society of AI systems the organisation develops or uses. The organisation shall perform such assessments at identified points in the AI system life cycle. Results of the impact assessments shall be used in AI risk assessment and risk treatment. Documented information shall be retained.

**Clause 8.4 — operational execution.** Clause 8.4 of ISO/IEC 42001 requires the operational execution of impact assessments (the 6.1.4 process is executed on actual systems). The auditor tests the procedure at 6.1.4 and the execution at 8.4; the two interact tightly, and findings often sit on both clauses.

## The ISO/IEC 42005 shape

ISO/IEC 42005 provides a method for AI system impact assessment. The expected elements of an assessment conducted per 42005: <!-- needs-research: confirm final clause structure and terminology in the as-published ISO/IEC 42005 at reading time; the standard progressed through DIS/FDIS in the 2024–2026 window and the auditor should read the as-published text, not a draft -->

- **AI system description.** Purpose, intended use, context of use, technical configuration, data flows, boundaries with other systems.
- **Stakeholder and affected-party identification.** Direct users, data subjects, decision subjects, operators, downstream deployers, broader affected communities, workers, regulators.
- **Context and deployment setting.** Jurisdiction, sector, regulatory environment, mode of deployment (SaaS, on-premise, embedded), human-oversight model.
- **Intended use and reasonably foreseeable misuse.** What the system is designed to do; what it might be used for in practice (including by bad actors, by uninformed users, under failure of the intended controls).
- **Impact identification.** Categories of impact (physical, psychological, economic, legal, social, environmental); specific impacts under each category.
- **Impact analysis and evaluation.** Likelihood and severity per impact; cumulative and compound impacts; disproportionate impacts on vulnerable groups.
- **Mitigation.** Controls selected (often mapping to Annex A) and residual-impact assessment post-mitigation.
- **Residual-impact statement.** What impacts remain after mitigation; whether those residuals are acceptable; who accepts them.
- **Review triggers and cadence.** When the assessment must be refreshed (release, material change, incident, context shift, regulatory change, periodic).

The auditor expects the organisation's impact-assessment procedure to be consistent with these elements, and expects the actual assessments to produce evidence against each.

## Auditing the impact-assessment procedure (6.1.4 — process audit)

**Audit test — procedural walk.** Request the impact-assessment procedure. Walk against the checklist:

```
Procedural element                                      Present   Evidence
---------------------------------------------------------------------------
Scope of assessment (per system and per material change)  ?       Procedure §?
Required inputs                                           ?        §?
  - system description
  - intended use / reasonably foreseeable misuse
  - data flows
  - stakeholder identification method
Impact categories and definitions                         ?        §?
  - physical, psychological, economic, legal/rights,
    social, environmental (or equivalent coverage)
  - specific sub-categories for the sector
Impact analysis method                                    ?        §?
  - severity scale and definitions
  - likelihood scale and definitions
  - compound / cumulative treatment
Vulnerable-group consideration                            ?        §?
Mitigation and residual-impact method                     ?        §?
Review triggers and cadence                               ?        §?
Roles and approval                                        ?        §?
Retention of documented information                       ?        §?
Link to risk assessment (6.1.2) and risk treatment (6.1.3) ?       §?
Link to transparency / information provided to users      ?        §?
   (Annex A information-for-interested-parties control)
```

A procedure that is silent on vulnerable-group consideration, reasonably foreseeable misuse, or residual-impact approval is a **minor** or **major** depending on extent and the organisation's AI exposure.

## Auditing the executed impact assessments (8.4)

**Audit test — population and sampling.** The population is the set of AI systems in scope. Sampling discipline from `mod-104` chapter 2 applies. Draw a sample stratified across:

- Impact category (high-impact decisions, medium-impact, low-impact).
- Life-cycle stage (new system this audit period, refreshed assessment, legacy system).
- Jurisdiction (EU, US, other — EU systems get the Article 27 cross-check).
- Deployment mode (SaaS, on-prem, embedded, third-party integration).

For each sampled assessment:

1. **Completeness against the procedure.** Walk the assessment against the organisation's own procedure. Every required element present? Missing elements are findings against 8.4 and the procedure.
2. **Stakeholder identification quality.** Does the stakeholder list include *impacted* parties (decision subjects, affected communities, workers) and not only *involved* parties (users, operators, business)? A stakeholder list without impacted-party entries is a finding.
3. **Intended use + reasonably foreseeable misuse.** Both are required. Assessments that describe only intended use often get a reasonably-foreseeable-misuse paragraph that reads "as per the acceptable-use policy" without specific misuse scenarios. That is a finding.
4. **Impact coverage.** Did the assessment consider all applicable impact categories? Common gaps: economic impact on decision subjects (denials of credit, denial of coverage, pricing differentials), psychological impact (distress from algorithmic rejection or surveillance), social impact (displacement effects, trust erosion).
5. **Vulnerable-group analysis.** Where the system affects people, were vulnerable groups considered specifically? Which groups, and why those? Is there an explicit statement that no vulnerable group is disproportionately affected, or (more commonly) a named group with a specific mitigation?
6. **Residual-impact statement.** After mitigation, what remains? Who accepted it? When? Is the acceptance consistent with the organisation's risk-acceptance criteria?
7. **Traceability to risk assessment and SoA.** Does the impact assessment feed the 6.1.2 risk register and the 6.1.3 SoA? Impact-assessment findings that do not propagate into risk and control is a traceability finding on 6.1.4 ↔ 6.1.3 and often on clause 8.
8. **Freshness.** Date of assessment versus the system's current state. Systems that have had material changes (new training data, new deployment region, new user class) since the last impact assessment should have a refreshed assessment per the procedure's trigger rules.

## EU AI Act Article 27 cross-check

Article 27 of the EU AI Act requires certain deployers of high-risk AI systems — specifically bodies governed by public law, private entities providing public services, and deployers using systems referred to in points (b) and (c) of Annex III points 5 (creditworthiness, life/health insurance) — to perform a **fundamental-rights impact assessment (FRIA)** before deploying the system. <!-- needs-research: confirm the current scope of Article 27 obligation and the categories of deployer in the current Regulation text; the final text and subsequent implementing acts/guidance may have refined the perimeter -->

The Article 27 FRIA must include:

- A description of the deployer's processes in which the high-risk AI system will be used in line with its intended purpose.
- The period of time within which, and the frequency with which, each high-risk AI system is intended to be used.
- Categories of natural persons and groups likely to be affected.
- The specific risks of harm likely to impact the categories of affected persons.
- A description of the implementation of human oversight measures per the system's instructions for use.
- The measures to be taken in case the risks materialise, including internal governance arrangements and complaint mechanisms. <!-- needs-research: verify exact wording and element list against the as-adopted Article 27 text -->

**Audit test — Article 27 cross-check.** Where the organisation is in Article 27 scope, the auditor tests both ISO/IEC 42005 execution and Article 27 execution. Three outcomes are typical:

1. **One combined artifact.** The organisation has written its impact-assessment procedure to a superset satisfying both 42005 and Article 27, with a single assessment template that includes the Article 27 elements plus the 42005 elements. The auditor confirms the template covers both and that the assessments produced meet both. This is the strongest shape.
2. **Two artifacts, poorly aligned.** The organisation has an ISO-shape impact assessment and a separate legal-team FRIA, with inconsistencies between them (stakeholder lists differ, mitigation claims differ). This is a finding — the AIMS cannot speak consistently to its obligations if the two assessments disagree.
3. **ISO assessment with Article 27 gaps.** The organisation has the ISO assessment but has not addressed Article 27 elements (particularly the "measures in case risks materialise" and the complaints mechanism, which the ISO assessment often omits). Finding, with the regulatory exposure flagged.

**Reporting the cross-check.** Non-conformity against the EU AI Act itself is a legal matter, not a certification matter. But the AI policy under clause 5.2(c) commits to meeting applicable requirements. Failure to execute an Article 27 obligation the organisation is subject to is therefore a clause 5.2 finding (the policy commitment is not met), a clause 6.1.4 finding (the impact-assessment procedure does not cover Article 27), and a clause 8.4 finding (operational impact assessments do not meet the Article 27 element list). The grading depends on extent — a single omission from one assessment is likely minor; a procedure that does not acknowledge Article 27 at all is major.

## Vulnerable-group analysis — the detail that most often sinks assessments

The single most frequent impact-assessment weakness is thin treatment of vulnerable groups. The auditor's test:

- Does the assessment name the groups considered (children, older adults, persons with disabilities, persons in protected categories, non-native speakers, low-literacy users, users with low-bandwidth access, users in high-stakes-context like detainees or applicants for public benefits)?
- Does it analyse *why* each group may be affected differently (data representation, interface accessibility, decision stakes, power imbalance)?
- Does it specify *mitigations* for each affected group and a *monitoring* plan for whether the mitigations work?

An assessment that lists groups without the second and third elements is a weak assessment; an assessment with no vulnerable-group section is a finding.

## Monitoring triggers — the interface with clause 9

Impact assessments are not one-off. The procedure's review triggers (new system, material change, incident, context shift, regulatory change, periodic) have to be *executed*. The auditor tests:

- A material change occurred (new deployment region, new user class, new training data). Did the trigger fire? Was the assessment refreshed?
- An incident occurred with human impact. Did the trigger fire?
- A regulator issued guidance affecting the system's context (e.g., EU AI Office GPAI code-of-practice update, FTC guidance, state AI law). Did the trigger fire?

Missing trigger execution usually surfaces at Stage-2 as patterns rather than isolated — multiple "stale" assessments point to a trigger-management failure that is a major against 6.1.4.

## The engineering-evidence depth question

The auditor is not the risk engineer. The `ai-risk-engineer` (L25) is the role that produces the hands-on impact-assessment work — identifying affected groups, analysing impacts, authoring mitigations, coordinating with privacy, product, and legal. The auditor's role is to test *whether the process was followed*, not to re-do the engineering analysis. Where the auditor needs to test the *substantive quality* of a given impact finding (e.g., is this claim about "no disparate impact on protected classes" defensible?), the auditor's specialist (ISA 620, `mod-104` chapter 3) is brought in.

## Common failure modes

- **Impact assessment confused with risk assessment.** The organisation runs a risk assessment, labels it "impact assessment", and submits it under 6.1.4. The two are related but distinct — risk is about the organisation, impact is about affected parties. A risk-register-only artifact is a 6.1.4 finding.
- **Intended-use statement without reasonably foreseeable misuse.** Required by 42005 and by prudent practice; its absence is a finding.
- **Stakeholder list without impacted parties.** Covered above.
- **Residual-impact statement missing or unapproved.** Without an approved residual, the organisation has no formal record of what harm it has decided is acceptable.
- **Article 27 obligation unaddressed in applicable EU deployment.** Covered above.
- **Impact assessments not routed to risk treatment.** Covered above — a traceability finding on 6.1.4 ↔ 6.1.3.
- **GPAI usage not impact-assessed.** The organisation treats GPAI (ChatGPT Enterprise, Copilot, Claude for Work) as "someone else's AI" and skips the impact assessment on *its use*. The organisation is the deployer; the impact assessment is on the deployed use, not on the model.

## Summary

- Clause 6.1.4 defines the impact-assessment *process*; clause 8.4 covers its *execution*. ISO/IEC 42005 is the method reference.
- The auditor tests procedural shape against the 42005 element list, then tests execution by sampling across impact category, life-cycle stage, jurisdiction, and deployment mode.
- The high-frequency findings cluster around: thin vulnerable-group analysis, missing reasonably-foreseeable-misuse, stakeholder lists without impacted parties, missing residual-impact approval, and impact-assessment outputs that do not propagate into risk treatment and SoA.
- For EU AI Act Article 27 deployers, the ISO impact assessment and the FRIA should be a single superset artifact or two tightly-aligned artifacts; divergence is a finding.
- Review triggers must fire — material changes, incidents, regulatory events — and the auditor tests trigger execution, not just the procedure's text.
- The `ai-risk-engineer` produces the substantive analysis; the auditor's role is to verify the process was followed, with specialist support where substantive technical challenge is needed.
