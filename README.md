# Applied AI, Python and Data Analytics

Toronto, Canada | [GitHub projects](https://github.com/jibrankazi?tab=repositories)

I work with Python, SQL, Power BI, machine-learning evaluation, data ingestion and reproducible analytics. The repositories below contain a mixture of working tools, original public-source analysis and experimental prototypes. **A completed data import or CI unit test is not proof of an entire system or deployable model.**

## Projects with executed original-source checks

| Project | Verified scope and evidence | Limit |
| --- | --- | --- |
| [Toronto 311 analysis](https://github.com/jibrankazi/data-analytics-portfolio/tree/main/toronto-311-analysis) | [2025 public service-request audit passed](https://github.com/jibrankazi/data-analytics-portfolio/actions/runs/37936583459) | Multiple request channels; not a telephone-staffing dataset |
| [Power BI Model Auditor](https://github.com/jibrankazi/pbi-model-auditor-Public) | [Original Microsoft PBIT static integration passed](https://github.com/jibrankazi/pbi-model-auditor-Public/actions/runs/37936674017) | Not a tenant-credential/live refresh |
| [Healthcare-ML](https://github.com/jibrankazi/Healthcare-ML) | [Full public Wisconsin Breast Cancer research run](https://github.com/jibrankazi/Healthcare-ML/actions/runs/37940182428) — train, heldout evaluation, SHAP/plots and LaTeX | Experimental research only, not clinical deployment; improvements remain under [PR #3](https://github.com/jibrankazi/Healthcare-ML/pull/3) |
| [Ontario Health Causal Analysis](https://github.com/jibrankazi/ontario-health-causal-analysis) | [Checked-in observational dataset analysis CI passed](https://github.com/jibrankazi/ontario-health-causal-analysis/actions/runs/37936780062) | Does not independently establish causal effect or original source provenance |
| [NeuroEvoRAG](https://github.com/jibrankazi/NeuroEvoRAG) | [Genuine Stanford SQuAD retrieval benchmark passed](https://github.com/jibrankazi/NeuroEvoRAG/actions/runs/37892312991) | Not end-to-end generated answer or LLM-NEAT validation |
| [DiffRAG-SQL](https://github.com/jibrankazi/DiffRAG-SQL) | [Real SQuAD extractive QA passed](https://github.com/jibrankazi/DiffRAG-SQL/actions/runs/37936638206) | SQL grounding and differentiable retrieval unverified |
| [WFM Schedule Optimizer](https://github.com/jibrankazi/wfm-schedule-optimizer) | [Observed Toronto 311 request timestamps audited](https://github.com/jibrankazi/wfm-schedule-optimizer/actions/runs/37936594132) plus separate synthetic scheduling tests | No actual call-arrival, employee roster or operational staffing trial |

Additional repositories use official ECCC climate data, Toronto traffic surveys, Bank of Canada FX and press feeds, Canadian grants, and real historical market-price checks. The sources and **precise nonvalidated boundaries** for all 17 substantive projects are recorded in the [portfolio evidence index](https://github.com/jibrankazi/toronto-2025-data-science-portfolio). An [index update under review](https://github.com/jibrankazi/toronto-2025-data-science-portfolio/pull/3) expands that status matrix.

## Engineering focus

- Reproducible research pipelines, honest provenance and source-contract validation
- SQL, Python ETL, statistical modelling and explainable ML
- Power BI model diagnostics and municipal service analytics
- Reliable API integration and conservative handling of unavailable source systems

All reported results should be checked against the individual GitHub Actions execution and artifact for the **same commit**. Simulated experiments and tests are explicitly labeled; no confidential municipal or banking records should be published.
