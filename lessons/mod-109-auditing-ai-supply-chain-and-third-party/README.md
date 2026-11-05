# mod-109-auditing-ai-supply-chain-and-third-party: Auditing the AI Supply Chain and Third-Party AI Vendors

> Scaffolded by `aicg org execute-plan`. Lecture chapters and exercise content are authored on subsequent autonomous cycles.

**Estimated effort:** 14 hours

## Learning objectives

- Audit AI supply-chain provenance — data provenance (datasheets, dataset signing), model provenance (Hugging Face model cards, signed weights with Sigstore, ML-BOM with CycloneDX, SPDX 3.0 AI profile, SLSA levels), training-pipeline integrity — well enough to trace a deployed model back to its inputs and to detect a provenance gap
- Audit third-party model / API usage against SR 23-4 interagency third-party-risk guidance — vendor due diligence, contractual controls, ongoing monitoring, exit planning, concentration-risk assessment; independently test the organisation's vendor-risk-assessment evidence rather than reading it
- Audit AI-vendor assurance artifacts the organisation relies on — SOC 2 Type II, SOC 2 + AI (where published), ISO/IEC 27001 certification, ISO/IEC 42001 certification, ForHumanity IAAIS reports, PCI DSS (where applicable), HITRUST CSF (where applicable) — testing scope adequacy, carve-outs, user-entity controls, bridge-letter coverage, and the delta between the vendor's assurance scope and the AI system's actual risk footprint
- Audit defence against malicious model artifacts — testing that the organisation's model-ingestion pipeline uses Protect AI ModelScan, Hugging Face picklescan, and signature verification; sampling the model registry for unsigned or unscanned artifacts; auditing the fine-tuning pipeline for supply-chain poisoning vectors (dataset back-doors, training-data injection, LoRA-weight tampering)
- Audit GPAI model usage under EU AI Act Articles 51-55 (general-purpose AI model obligations, systemic-risk thresholds, model-provider documentation to downstream deployers) — testing the organisation's downstream deployer obligations against the GPAI Code of Practice
- Audit model-signing and registry-ingestion gates — Sigstore, in-toto, SLSA levels — as the evidence that only approved artifacts reach production; this is the auditor's complement to the `ai-infra-security` / `security-learning` (level 35) runtime-hardening work
- Audit OMB M-24-18 / M-25-22 / M-25-21 federal-agency AI inventory and third-party-AI acquisition obligations where the organisation is a US federal agency or federal contractor

## Structure

- `01-…md` … `0N-…md`: lecture chapters.
- `exercises/`: per-exercise prompts.
- `labs/`: long-form hands-on labs.
- `quizzes/`: knowledge checks.
- `resources.md`: external references.
