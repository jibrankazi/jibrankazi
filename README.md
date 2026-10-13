# Applied AI & Machine Learning Development

**Python · Machine Learning · NLP / RAG · FastAPI · Docker · SQL · Data Engineering**

Toronto, Canada · [Project repositories](https://github.com/jibrankazi?tab=repositories)

I build and evaluate machine-learning applications and reproducible data systems, from original public-source data through model validation, API development, container packaging, testing and measurable results. My portfolio focuses on **working software, traceable experiments and clear engineering trade-offs**, not just notebook screenshots or green CI badges.

## Featured AI/ML projects

### 01 · [NeuroEvoRAG — document question answering with source citations](https://github.com/jibrankazi/NeuroEvoRAG)

**Local application:** Upload UTF-8 text, Markdown or searchable PDFs through a responsive browser interface; ask a question; inspect an exact quoted document span and its character offsets. The implementation includes bounded uploads, separate ephemeral workspaces, TF-IDF document retrieval, a pretrained DistilBERT extractive reader, FastAPI, deletion, refusal on unsupported questions, Docker and automated HTTP testing.

- **Executed NLP evaluation:** 1,200 real Stanford SQuAD passages indexed per seed; **360 heldout retrieval questions**, with **BM25 recall@3 = 91.67%**, and **34/72 exact neural answers (47.22%)** using the existing TF-IDF-selected pretrained-reader setup. Retrieval recall is *not* answer correctness; this is a favorable, closed-corpus research benchmark.
- **[Actual API/UI and Docker test](https://github.com/jibrankazi/NeuroEvoRAG/actions/runs/38348736092)** · [Architecture, demo instructions and screenshot](https://github.com/jibrankazi/NeuroEvoRAG/blob/main/docs/LOCAL_APP.md) · [Measured original-data QA benchmark](https://github.com/jibrankazi/NeuroEvoRAG/actions/runs/38344505317)
- **UI screenshot:** Open the first workflow and download the `local-document-api-working-ui-screenshot` artifact; it contains the **actual locally served browser capture**, not a mockup.

```bash
git clone https://github.com/jibrankazi/NeuroEvoRAG.git
cd NeuroEvoRAG
docker build -t neuroevo-local .
docker run --rm -p 127.0.0.1:8000:8000 neuroevo-local
# Open http://localhost:8000
```

### 02 · [Healthcare-ML — reproducible supervised learning to API serving](https://github.com/jibrankazi/Healthcare-ML)

**Training-to-inference lifecycle:** Fit five models on the original **569-row Wisconsin Breast Cancer public research dataset** with a fixed stratified split, choose a model by training-only cross-validation, evaluate **114 heldout records**, create explanation/diagnostic plots, serialize the model, build a Docker image and serve the same feature schema over an HTTP API.

- **Deployed-style demonstration:** `/predict`, `/schema`, `/health`, and `/metrics`; validates all 30 original feature names and the correct label direction (**1 = malignant in this dataset**). The aggregate-only monitor tracks sample counts, probability bins and training-reference envelope excursions; it does not store user records.
- **[Verified training → real Docker → actual HTTP inference and monitoring run](https://github.com/jibrankazi/Healthcare-ML/actions/runs/38348764840)** · [Architecture and exact setup](https://github.com/jibrankazi/Healthcare-ML/blob/main/docs/RESEARCH_SERVING.md) · [Independent training/heldout research workflow](https://github.com/jibrankazi/Healthcare-ML/actions/workflows/tests.yml)
- **Scientific boundary:** a historic public ML benchmark, **not a clinically validated prediction or patient-facing medical device**.

```bash
git clone https://github.com/jibrankazi/Healthcare-ML.git
cd Healthcare-ML
docker build -t wisconsin-research-api .
docker run --rm -p 127.0.0.1:8002:8000 wisconsin-research-api
# Open http://localhost:8002/docs to explore the API
```

### 03 · [Fraud Detection — imbalanced classification and decision analysis](https://github.com/jibrankazi/data-analytics-portfolio/tree/main/fraud-detection-finance)

**Original public ULB/Worldline historical transactions:** **284,807 genuine 2013 records**, including 492 labeled frauds; duplicate-group-aware train/validation/test partitions, validation-selected thresholds and a **56,965-record untouched holdout**. This is model-evaluation research, not banking-system access.

- Heldout selected model: **average precision 0.7744**, **61 actual frauds detected**, **21 missed**, **11 false alerts**, with illustrative *hypothetical* decision costs evaluated **without retuning on the holdout**.
- **[Reproduced original-source end-to-end workflow](https://github.com/jibrankazi/data-analytics-portfolio/actions/runs/38342914993)** · [Source, evaluation approach and limitations](https://github.com/jibrankazi/data-analytics-portfolio/tree/main/fraud-detection-finance)
- **Limit:** The source copy used here lacks original transaction timestamps; the evaluation is not forward-time validation, and toy cost assumptions are **not realized bank savings**.

## Engineering approach

| Area | Techniques used in the projects |
| --- | --- |
| **ML evaluation** | Training-only model selection; heldout testing; AUROC, average precision, Brier, error analysis |
| **Applied NLP** | Verbatim evidence citations, retrieval metrics, BM25/TF-IDF baselines, pretrained extractive QA |
| **AI application engineering** | FastAPI, local document upload and deletion, data-schema contracts, source-limited responses |
| **Reproducibility** | Public data provenance, GitHub Actions, Docker, deterministic experiments, model artifacts |
| **Operational safeguards** | Explicit scope boundaries, in-memory aggregate monitoring, bounded inputs and abstention |

## Architecture and real interface evidence

The projects include implementation diagrams and reproducible commands—not just design proposals:

- [NeuroEvoRAG local Q&A architecture, browser screenshots and API examples](https://github.com/jibrankazi/NeuroEvoRAG/blob/main/docs/LOCAL_APP.md)
- [Healthcare-ML end-to-end model lifecycle, container architecture and monitored HTTP examples](https://github.com/jibrankazi/Healthcare-ML/blob/main/docs/RESEARCH_SERVING.md)
- [Actual NeuroEvoRAG UI screenshot artifact, captured from the running API](https://github.com/jibrankazi/NeuroEvoRAG/actions/runs/38348736092)

These are **local, reproducible applications and research studies**, not publicly hosted SaaS, field-tested reinforcement-learning controllers or production medical/financial products.

## Other engineering work

[DiffRAG-SQL](https://github.com/jibrankazi/DiffRAG-SQL) (bounded natural-language-to-SQL and independent failure analysis), [Power BI Model Auditor](https://github.com/jibrankazi/pbi-model-auditor-Public) (static semantic/report auditing), [WFM Schedule Optimizer](https://github.com/jibrankazi/wfm-schedule-optimizer) (optimization and public municipal data analysis), and [Toronto 311 analysis](https://github.com/jibrankazi/data-analytics-portfolio/tree/main/toronto-311-analysis) (municipal service-request research) provide additional software and analytics experience. [View all repositories](https://github.com/jibrankazi?tab=repositories).

**Privacy:** No confidential municipal records, employer credentials, banking transaction accounts or private patient information should be committed or uploaded to these research demos.
