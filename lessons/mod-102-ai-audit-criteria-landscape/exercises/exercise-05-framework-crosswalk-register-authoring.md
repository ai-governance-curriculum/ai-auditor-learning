# exercise-05: Framework Crosswalk Register — Authoring and Testing

**Estimated effort:** 4 hours

## Objective

Author a **crosswalk register** that maps a plausible AI-platform control library to every framework and overlay in scope for a multi-regime organisation, then test the register itself against the suitability criteria in chapter 6. The deliverable is (a) the register as a structured artifact and (b) an auditor's test memo that exposes gaps, over-claims, and silent omissions. The register integrates outputs from exercises 01–04.

## Prerequisites

- Chapter [`06-crosswalk-register-authoring.md`](../06-crosswalk-register-authoring.md).
- Completed registers from exercises 01 (ISO/IEC 42001), 02 (NIST AI RMF + GenAI Profile), 03 (EU AI Act), 04 (sector overlays).
- The `senior-ai-governance-architect` (L50) control-library concept — see the mod-101 chapter 1 role-boundary discussion.

## Scenario

**Meridian Enterprise AI Platform** is the shared-services platform used by all Meridian subsidiaries in exercise 04. The platform engineering group (reporting to CTO, functionally to the Enterprise AI Architecture function) maintains a documented control library with ~60 controls spanning:

- Policy and governance (AI policy, acceptable-use, procurement).
- Life-cycle (requirements, data, training, evaluation, red-team, release, deployment, monitoring, decommissioning).
- Risk and impact assessment (process + per-system execution).
- Security (platform, identity, API, prompt-injection, model-extraction).
- Third-party (foundation-model vendor, data vendor, labelling vendor, deployer).
- Documentation (model cards, datasheets, release notes, incident records).
- Incident response and post-market monitoring.
- Quality management (overall AIMS clause-9 performance evaluation, clause-10 improvement).

The architect has produced a Design-A register row for every control. The AI Auditor's job for this exercise is to walk the register, test cells, raise findings, and extend it with Design-B evidence rows for one Meridian subsidiary (Specialty Lending credit-risk model).

## Deliverables

1. **Crosswalk register (Design A rows)** — a structured artifact covering at least **25 controls** from the control library. Each row has:
   - Control ID, title, objective, type, owner, frequency, population scope.
   - Expected evidence artifact(s).
   - Framework-criterion columns: **ISO/IEC 42001** (clauses + Annex A controls), **NIST AI RMF** (Subcategories), **NIST GenAI Profile** (risks), **EU AI Act** (Articles + harmonised standards), and the sector overlays in scope for the control.
   - Cell content: **citation**, **degree** (fully / partially / supports), **linked criterion ID** (from your exercises 01–04 registers), **evidence location**.
2. **Crosswalk register (Design B rows)** — at least **10 evidence-artifact rows** for the Meridian Specialty Lending credit-risk model, joining to the Design A rows that produce or consume each artifact. Each row carries artifact ID, system of record, retention location, owner, controls it supports, framework-criterion columns, and last-tested history.
3. **Register test memo** (~800 words) — audit the register itself under criterion `C-CROSSWALK-01` (chapter 6). The memo must:
   - List at least **three framework criteria** without any mapped control (gaps against the library).
   - List at least **three "fully satisfies" cells** that on inspection should be "partially" or "supports" (over-claims).
   - List at least **two excluded Annex A controls** or NIST Subcategories with boilerplate justifications and challenge each.
   - List at least **two stale cells** — citations to framework versions no longer current — and name the correct citation.
   - Propose **register-level findings** for the architect to remediate, each with a finding grade (minor NC / major NC / OFI) consistent with ISO/IEC 17021-1 definitions where applicable.
4. **Testing plan excerpt** (~300 words) — for five specific controls, write the audit procedure that would test both the control's operation *and* the register's claim that the control satisfies the mapped criteria.

## Minimum volume

- At least **25 Design A rows**.
- At least **10 Design B rows**.
- Cells populated across at least **four framework columns** (ISO/IEC 42001, NIST AI RMF, EU AI Act, one or more sector overlays).
- At least **40% "partially"** cells across the register — a Design A row with only "fully" cells is evidence the author over-claimed.
- Every cell cites both the external framework citation and the internal linked-criterion ID.

## Starter guidance

- Begin with Pass 2 from chapter 6 — walk each control and populate framework columns. Only after Pass 2 is complete should you begin Pass 3 Design B rows for Specialty Lending.
- Use NIST's published crosswalks (AI RMF ↔ ISO/IEC 42001; AI RMF ↔ ISO/IEC 23894; AI RMF ↔ OECD; AI RMF ↔ OMB/EO federal instruments) as Pass-1 seed data, not final content. Validate each crosswalk entry you reuse.
- A single control almost never fully satisfies a composite framework criterion. Default to "partially" with named companion controls; reserve "fully" for atomic criteria.
- Evidence-location columns must point to concrete repositories (GRC tool ticket IDs, SharePoint paths, Confluence pages, model-card URLs). "In the eval system" is not an evidence location.
- The test memo should feel like a professional auditor's workpaper — specific, neutral in tone, every finding citable.
- Include at least one control that maps to zero frameworks — a control the organisation runs because of its own risk appetite, not an external requirement. This is defensible but should be visible.
- The Specialty Lending Design B rows will overlap NIST + ISO/IEC 42001 + EU AI Act (if EU borrowers) + SR 11-7 + Colorado — this is where the crosswalk pays off, as one validation report may satisfy a dozen criteria.

## Acceptance criteria

The deliverables are accepted when:

- The register meets volume thresholds (25 Design A + 10 Design B; ≥40% "partially" cells).
- Every cell carries citation + degree + linked criterion ID + evidence location (no bare "X").
- At least one control is mapped to zero external frameworks and defended in writing.
- The test memo lists all required categories (gaps, over-claims, excluded-control challenges, stale cells, register-level findings) with the minimum counts.
- Register-level findings are graded (minor NC / major NC / OFI) with reasoning consistent with ISO/IEC 17021-1 definitions.
- The testing-plan excerpt describes procedures that test *both* control operation and register-claim accuracy — not just one.
- No framework citation is invented; where the standard is moving (harmonised standards, OMB memos, NAIC state adoption, AICPA SOC-for-AI status), the cell carries `<!-- needs-research: ... -->` with the specific fact to re-verify.

## Stretch goals

- Implement the register in a **spreadsheet** (CSV or Excel) with one sheet per framework and a joining sheet, and submit the file alongside the Markdown. Confirm cell-formula integrity (no broken links).
- Add a **change-log sheet** for the register with the first three change entries dated and reasoned, as the architect would maintain it.
- Author the **engagement-letter paragraph** that defines the auditor's rights to review the register and raise register-level findings — framing it so the architect is accountable without the auditor co-authoring.
- Produce a **stakeholder-report view** (~300 words) extracted from the register that the Audit Committee would read: top five register-level findings with regulatory and operational impact.
