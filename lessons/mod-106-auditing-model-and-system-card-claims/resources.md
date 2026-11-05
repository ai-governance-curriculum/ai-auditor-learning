# Resources for mod-106-auditing-model-and-system-card-claims

## Card formats

- **Mitchell, M., Wu, S., Zaldivar, A., Barnes, P., Vasserman, L., Hutchinson, B., Spitzer, E., Raji, I. D., Gebru, T. (2019).** *Model Cards for Model Reporting.* FAccT 2019. arXiv 1810.03993.
- **Gebru, T., Morgenstern, J., Vecchione, B., Vaughan, J. W., Wallach, H., Daumé III, H., Crawford, K. (2021).** *Datasheets for Datasets.* Communications of the ACM 64(12). arXiv 1803.09010.
- **Pushkarna, M., Zaldivar, A., Kjartansson, O. (2022).** *Data Cards: Purposeful and Transparent Dataset Documentation for Responsible AI.* FAccT 2022.
- **Hugging Face.** *Model Card Guidebook* and *Model Cards* documentation at `huggingface.co/docs/hub/model-cards`. <!-- needs-research: confirm current URL and canonical field list at reading time -->
- **Google.** *Model Card Toolkit* (`github.com/tensorflow/model-card-toolkit`) and *Data Cards Playbook* (`sites.research.google/datacardsplaybook/`).
- **Partnership on AI.** *ABOUT ML* and *Guidelines for Foundation Model Publication.*
- **OpenAI, Anthropic, Google DeepMind, Meta — system cards and release documents.** Per-release documents published by each developer; cite the specific release and retrieval date.
- **IEEE 7001-2021** *Standard for Transparency of Autonomous Systems.*

## Normative and regulatory references

- **ISO/IEC 42001:2023** *Information technology — Artificial intelligence — Management system.*
- **ISO/IEC 23894:2023** *Information technology — Artificial intelligence — Guidance on risk management.*
- **ISO/IEC 42005** *AI system impact assessment.* <!-- needs-research: confirm publication state at reading time -->
- **NIST AI 100-1 (AI Risk Management Framework 1.0, January 2023).**
- **NIST AI 600-1 (Generative AI Profile, July 2024).**
- **NIST AI 100-2e (Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations).**
- **EU Regulation 2024/1689 — Artificial Intelligence Act** — Articles 10 (data governance), 15 (accuracy, robustness, cybersecurity), 27 (fundamental rights impact assessment), Annex III (high-risk categories), Annex VII (conformity assessment).
- **NYC Administrative Code § 20-870 et seq. — Automated Employment Decision Tools (Local Law 144)** and the DCWP implementing rules. <!-- needs-research: cite the final-rule publication citation and any amendments at reading time -->
- **EEOC Uniform Guidelines on Employee Selection Procedures (29 CFR Part 1607, 1978)** — the four-fifths rule.
- **Colorado SB 24-205 — Colorado AI Act.** <!-- needs-research: confirm current statutory citation and effective date at reading time -->
- **HHS OCR Section 1557 final rule (2024)** — nondiscrimination in clinical-decision-support tools.
- **FDA Good Machine Learning Practice for Medical Device Development: Guiding Principles** (FDA / Health Canada / MHRA, October 2021) and the FDA Predetermined Change Control Plan guidance.
- **Federal Reserve SR 11-7 / OCC 2011-12** *Supervisory Guidance on Model Risk Management.*
- **NAIC Model Bulletin: Use of Artificial Intelligence Systems by Insurers (2023).**

## Attestation and audit standards

- **IAASB ISAE 3000 (Revised)** *Assurance Engagements Other Than Audits or Reviews of Historical Financial Information.*
- **AICPA SSAE-19** *Attestation Standards.*
- **ISO/IEC 17021-1:2015** *Conformity assessment — Requirements for bodies providing audit and certification of management systems.*
- **ISO/IEC 42006** *Requirements for bodies providing audit and certification of AI management systems.* <!-- needs-research: confirm publication status at reading time -->
- **IIA Standards 2024** *Global Internal Audit Standards.*
- **ISA 500 / AU-C 500** — audit evidence.
- **ISA 530 / AU-C 530** — audit sampling.
- **ISA 620 / AU-C 620** — using the work of an auditor's expert.
- **ISA 230** — audit documentation.
- **ForHumanity Independent Audit of AI Systems (IAAIS) criteria** at `forhumanity.center`. <!-- needs-research: inventory current IAAIS criteria set at reading time -->
- **BABL AI** *Bias Audit Methodology for Automated Employment Decision Tools* and related publications. <!-- needs-research: confirm current methodology publication at reading time -->

## Benchmarks

- **HarmBench.** Mazeika, M., Phan, L., Yin, X. et al. (2024). *HarmBench: A Standardized Evaluation Framework for Automated Red Teaming and Robust Refusal.* ICML 2024. arXiv 2402.04249. `github.com/centerforaisafety/HarmBench`.
- **AIR-Bench 2024.** Zeng, Y., Yang, Y., Zhou, A. et al. (2024). *AIR-Bench 2024: A Safety Benchmark Based on Regulation and Policies Specified Risk Categories.* arXiv 2407.17436.
- **AgentDojo.** Debenedetti, E., Zhang, J., Balunović, M. et al. (2024). *AgentDojo: A Dynamic Environment to Evaluate Attacks and Defenses for LLM Agents.* NeurIPS 2024 Datasets and Benchmarks.
- **InjecAgent.** Zhan, Q., Liang, Z., Ying, Z., Kang, D. (2024). *InjecAgent: Benchmarking Indirect Prompt Injections in Tool-Integrated Large Language Model Agents.* ACL Findings 2024. arXiv 2403.02691.
- **WMDP.** Li, N., Pan, A., Gopal, A. et al. (2024). *The WMDP Benchmark: Measuring and Reducing Malicious Use With Unlearning.* ICML 2024. arXiv 2403.03218.
- **MLCommons AILuminate** at `mlcommons.org/benchmarks/ai-safety/`. <!-- needs-research: cite current release and version -->
- **Meta CyberSecEval 1/2/3** — Meta AI Research publications and the `PurpleLlama/CybersecurityBenchmarks` repo on GitHub. <!-- needs-research: cite current version at reading time -->
- **METR.** `metr.org` — public task suite for autonomy evaluations. <!-- needs-research: cite the current public task set at reading time -->
- **SWE-bench Verified.** Jimenez, C. E., Yang, J., Wettig, A. et al. SWE-bench project — *github.com/princeton-nlp/SWE-bench*; Verified subset announced by OpenAI (2024).
- **MMLU, GLUE, SuperGLUE, HELM (Stanford CRFM), Big-Bench, Big-Bench-Hard** — general reference benchmarks the card may cite.

## Replication toolchain — upstream references

- **garak.** `github.com/leondz/garak` (now under NVIDIA stewardship). Derczynski, L. et al.
- **PyRIT.** `github.com/Azure/PyRIT`. Microsoft AI Red Team.
- **Promptfoo.** `github.com/promptfoo/promptfoo`.
- **Inspect.** `github.com/UKGovernmentBEIS/inspect_ai`. UK AI Security Institute. <!-- needs-research: confirm AISI name and repo at reading time -->
- **ART — Adversarial Robustness Toolbox.** `github.com/Trusted-AI/adversarial-robustness-toolbox`. IBM / LFAI Trusted AI.
- **TextAttack.** `github.com/QData/TextAttack`. Morris, J. et al.
- **CleverHans.** `github.com/cleverhans-lab/cleverhans`. Papernot, N., Goodfellow, I. et al.
- **Counterfit.** `github.com/Azure/counterfit`. Microsoft (archived upstream in 2023). <!-- needs-research: confirm maintenance status at reading time -->
- **Fairlearn.** `fairlearn.org`. Microsoft-sponsored open-source project.
- **AI Fairness 360 (AIF360).** `aif360.res.ibm.com`. IBM / LFAI.
- **Holistic AI library.** `github.com/holistic-ai/holisticai`.
- **SHAP.** `github.com/shap/shap`. Lundberg, S., Lee, S.-I.
- **Alibi.** `github.com/SeldonIO/alibi`. Seldon.
- **LIME.** `github.com/marcotcr/lime`. Ribeiro, M. T., Singh, S., Guestrin, C.
- **Opacus.** `opacus.ai`. Meta.
- **TensorFlow Privacy.** `github.com/tensorflow/privacy`. Google.
- **ML Privacy Meter.** `github.com/privacytrustlab/ml_privacy_meter`. NUS Secure and Trustworthy ML group.
- **Presidio.** `github.com/microsoft/presidio`. Microsoft.
- **Sigstore / Cosign.** `sigstore.dev`. OpenSSF / LFX.
- **Hugging Face Hub.** `huggingface.co/docs/hub`.

## Methodology references

- **Mitchell, T. M. (1997).** *Machine Learning.* McGraw-Hill. (Foundations.)
- **Dwork, C., Roth, A. (2014).** *The Algorithmic Foundations of Differential Privacy.*
- **Abadi, M., Chu, A., Goodfellow, I. et al. (2016).** *Deep Learning with Differential Privacy.* CCS 2016.
- **Mironov, I. (2017).** *Rényi Differential Privacy.* CSF 2017.
- **Gopi, S., Lee, Y. T., Wutschitz, L. (2021).** *Numerical Composition of Differential Privacy.* NeurIPS 2021.
- **Carlini, N., Chien, S., Nasr, M., Song, S., Terzis, A., Tramèr, F. (2022).** *Membership Inference Attacks from First Principles.* IEEE S&P 2022.
- **Carlini, N., Tramèr, F., Wallace, E. et al. (2021).** *Extracting Training Data from Large Language Models.* USENIX Security 2021.
- **Kleinberg, J., Mullainathan, S., Raghavan, M. (2016).** *Inherent Trade-Offs in the Fair Determination of Risk Scores.* ITCS 2017. arXiv 1609.05807.
- **Chouldechova, A. (2017).** *Fair Prediction with Disparate Impact: A Study of Bias in Recidivism Prediction Instruments.* Big Data 5(2).
- **Landis, J. R., Koch, G. G. (1977).** *The Measurement of Observer Agreement for Categorical Data.* Biometrics.
- **Efron, B., Tibshirani, R. J. (1993).** *An Introduction to the Bootstrap.* Chapman & Hall.
- **Cohen, J. (1988).** *Statistical Power Analysis for the Behavioral Sciences* (2nd ed.).
- **Wilson, E. B. (1927).** *Probable inference, the law of succession, and statistical inference.* JASA 22.
- **Brown, L. D., Cai, T. T., DasGupta, A. (2001).** *Interval Estimation for a Binomial Proportion.* Statistical Science 16.

## Threat taxonomies

- **MITRE ATLAS.** `atlas.mitre.org`.
- **OWASP Top 10 for LLM Applications.** `owasp.org/www-project-top-10-for-large-language-model-applications/`. <!-- needs-research: cite current edition at reading time -->
- **AI Incident Database.** `incidentdatabase.ai`. Partnership on AI.
- **AVID — AI Vulnerability Database.** `avidml.org`.

## Reporting shapes

- **Treasury Board of Canada Secretariat — Directive on Automated Decision-Making** and the Algorithmic Impact Assessment tool. `canada.ca/en/government/system/digital-government/digital-government-innovations/responsible-use-ai/algorithmic-impact-assessment.html`.
- **AICPA — SOC for AI** (where applicable). <!-- needs-research: confirm whether a published AICPA SOC for AI framework exists at reading time; several consultancies have proposed drafts -->
- **ISO/IEC TS 25058 / ISO/IEC 25059** — AI system quality model references for structuring metric reporting.

> Where a claim in this module could not be fully pinned to a primary source at authoring time, the chapter carries a `<!-- needs-research: ... -->` marker. Re-verify those citations against the as-published source at reading time before relying on them in a live engagement.
