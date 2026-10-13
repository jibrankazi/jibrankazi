# AI / ML Engineer Interview Portfolio — Evidence-First Preparation

**Career target:** Entry/associate AI Engineer, Applied AI Developer or Junior ML Engineer.
**What this page is:** A project selection and technical interview guide grounded in
actual code, published public data, GitHub Actions and known limitations. This is
not a certificate, an automated claim of competence, or evidence that the author
personally wrote every line of the repositories. Check each current workflow
before presenting it as passing.

## Which projects to demonstrate

| Rank | Project / access | What to demo | Measured source-backed evidence | Hard interview limit |
| --- | --- | --- | --- | --- |
| **1** | [Healthcare-ML](https://github.com/jibrankazi/Healthcare-ML), public | Data-to-five-model training, class mapping, CV-selected model, calibrated predictions, SHAP, saved-model inference | [Full train-to-saved-model inference CI](https://github.com/jibrankazi/Healthcare-ML/actions/runs/38342798962): 569 historical Wisconsin diagnostic samples, 30 original measurements, 114 held-out records; logistic AUROC 0.9874, AUPRC 0.9883 on *CI demo configuration* | No independent clinical cohort or deployed diagnostic model. Stored inference scores do **not** establish clinical calibration |
| **2** | [Original ULB Fraud benchmark](https://github.com/jibrankazi/data-analytics-portfolio/tree/main/fraud-detection-finance), public | Class imbalance, group-based duplicate isolation, train/validation/test, validation-only threshold, PR curves, false-positive trade-off | [Full OpenML train-to-fixed-policy evaluation](https://github.com/jibrankazi/data-analytics-portfolio/actions/runs/38342914993): 284,807 historical transactions, 492 frauds; 56,965 held out, 82 frauds; selected boosting test AP 0.7744, recall 61/82 | No forward-time test because this OpenML version lacks original `Time`; not live transaction fraud detection |
| **3** | [NeuroEvoRAG](https://github.com/jibrankazi/NeuroEvoRAG), public | Indexing, TF-IDF vs pretrained DistilBERT extraction, passage provenance, train-only retrieval selection | [Executed Stanford SQuAD QA](https://github.com/jibrankazi/NeuroEvoRAG/actions/runs/37997618487): 240 indexed passages, 16 held-out questions, 11/16 exact answers, token F1 0.7092 | Small deliberately favorable closed corpus; the QA model is **pretrained**; do not claim end-to-end RAG model training or NEAT evolution has been validated |
| **4** | [Smart Traffic Signals RL](https://github.com/jibrankazi/smart_traffic_signals_rl), **private** | Q-learning state/action/reward design, multi-seed baselines, assumption sensitivity, sim-to-real gap | [Original Toronto movement-count validation](https://github.com/jibrankazi/smart_traffic_signals_rl/actions/runs/38028070851): 12,000 published 15-minute traffic count rows fed to simulated queues | Real vehicle counts are *inputs*, not measured improvement in city traffic signals; recruiters cannot view a private repository unless separately granted access |
| **5** | [DiffRAG-SQL](https://github.com/jibrankazi/DiffRAG-SQL), public | Schema introspection, safe parameter binding, FK-path joins, source-independent execution metrics, reporting failure | [170 external SQL prompts](https://github.com/jibrankazi/DiffRAG-SQL/actions/runs/38331488243): 12/167 correct from original prompts (~7.2%), 4 correct generated joins | Low unrestricted-query generalization; SQL generator is a **bounded rule-based compiler** with ML intent predictor used diagnostically, NOT a trained general text-to-SQL decoder |

**Supporting projects:** [ECCC precipitation experiment](https://github.com/jibrankazi/flood_forecasting_ai) (private) demonstrates a valuable *negative* finding: held-out 2025 logistic rain AUROC 0.460, random-forest 0.488, so a simple forecasting use case did not become a successful flood predictor. [Adaptive Cyber Defense NLP](https://github.com/jibrankazi/adaptive_cyber_defense_rl_nlp) provides a genuine UCI historic phishing classifier and SMS classification, but no validated deployed defensive RL agent. [Power BI Auditor](https://github.com/jibrankazi/pbi-model-auditor-Public) and [WFM Schedule Optimizer](https://github.com/jibrankazi/wfm-schedule-optimizer) support the **software/operational engineering** narrative, not an assertion of trained production AI. Toronto 311 service-request records are not Cisco call records.

## The engineering bar to pass before saying "interview-ready"

For each featured project, independently reproduce and explain:

| Skill an interviewer may test | Evidence you should show | Reject these shortcuts |
| --- | --- | --- |
| Problem definition | Who benefits, predictive target, units and decision being supported | A name like "AI" or "causal" as proof |
| Source provenance | Publisher, date range, shape, feature provenance, source fingerprints | Synthetic rows presented as original observations |
| Leakage prevention | Why data are split this way, and which operations are fit **only** to training | Scaling, oversampling, feature selection or threshold tuning on heldout test |
| Baselines and selection | An explicit naive/classical baseline; choose hyperparameters only using train/validation | Show only a high best-model accuracy |
| Error analysis | Confusion matrix/FP-FN costs, class imbalance, probability calibration, slices and failure traces | Claim a score is production performance |
| Reproducibility | Environment, fixed seeds, configs, source links, rerun command, saved outputs | Screenshots with no code/results |
| Serving/inference | Trustworthy saved model, schema contract, correct class-1 interpretation, safe refusal, repeatable probabilities | Demo predictions using target labels as input |
| Safety and deployment | Responsible limitations, monitoring, privacy, drift, and decision-making boundaries | Calling a public research benchmark production software |

**Specific new engineering exercise:** Healthcare-ML now has `src/hchealth/infer.py` to reload the training-CV-chosen model, reject malformed feature CSVs, and serialize batch malignancy-class research probabilities with model/input hashes. Its CI workflow also re-computes each original public heldout probability independently after training. The [October 13 train-to-inference workflow](https://github.com/jibrankazi/Healthcare-ML/actions/runs/38342798962) **passed**, including independent original-Wisconsin-heldout `predict_proba` equality verification and schema/metadata refusals.

## Be able to answer these questions without notes

### 1. How did you avoid data leakage in the fraud study?

Explain that the 2013 ULB OpenML copy includes repeated anonymized feature vectors, so identical vectors are kept within the same split. The three-way split is train, validation, held-out test; model choice and decision threshold use validation only. No SMOTE is applied before splitting. The [October 13 original-source-to-cost-sensitivity job](https://github.com/jibrankazi/data-analytics-portfolio/actions/runs/38342914993) **passed**: the already-frozen test threshold reproduced **TN 56,872, FP 11, FN 21, TP 61**, and multiple clearly hypothetical FP/FN costs were evaluated **without selecting the threshold on test data**. **But** randomized grouping is not a chronological test. Explain why the business cost of missing fraud and false alerts makes average precision, false positives and thresholds more meaningful than overall accuracy.

### 2. Why does Healthcare-ML report multiple metrics?

The original Wisconsin outcome was recoded to **1 = malignant**, and the target mapping is checked by software tests. AUROC measures ranking; AUPRC emphasizes ranking with class imbalance; Brier measures squared probability error. Training-fold AUROC determines the explained model, **not** the best score on the one heldout set. A confidence interval on this historical holdout is not an external patient validation.

### 3. What happens between training and inference?

Explain exactly how a fitted estimator, metadata and feature names are persisted and later reloaded **from trusted local artifacts**. Demonstrate rejecting the wrong number or order of features, label metadata disagreement, NaNs and infinite values. Show a saved actual-public-dataset inference batch and verify it independently by direct `predict_proba`. **Do not deserialize arbitrary user-supplied joblib/pickle.**

### 4. What is the architecture of your RAG demonstration?

Published SQuAD paragraphs → TF-IDF retrieval selected with source-disjoint tuning questions → top-3 candidates → pretrained DistilBERT extractive answer extraction → original text-span citation → exact-match/token-F1 scoring. Explain that 16 questions from a gold-containing closed corpus, and an existing pretrained QA reader, are not independent production generalization evidence.

### 5. Did your reinforcement learning improve real city traffic?

No verified improvement to field traffic operation. Toronto 15-minute turning-movement counts are genuine; queue physics, green-phase control, policy rewards and baseline comparisons are simulated. Explain state discretization, transitions and sensitivity to assumed capacities. Regulatory, pedestrian and safety requirements prevent claims of operational readiness.

### 6. Your text-to-SQL accuracy is only around 7%. What did you learn?

Seventy percent *clause-label micro-F1* is not seventy percent correct SQL. The external AWS original-question execution benchmark correctly answered 12/167 executable gold queries (~7.2%) in an earlier expanded implementation. It can inspect unknown schemas, discover declared foreign-key paths, safely bind literal parameters and refuse unsupported requests, but it cannot parse arbitrary complex queries. Do not call it a trained universal SQL generator. Talk about diagnostics, failure modes, under-coverage and why source-independent execution checks change your view of a model.

### 7. What did YOU actually implement?

Be precise about which parts you personally designed, reviewed, changed, tested and can reconstruct. If automated coding assistance produced code, say so when relevant and then demonstrate your understanding of its behavior and limitations. The repository is evidence of software, **not proof of individual authorship**. Do not credit yourself with your manager's Erlang C or Cisco data work, and do not claim production deployment that has not happened.

## Practical technical interview rehearsals

Start with Healthcare-ML and ULB Fraud. Clone the source, create a clean Python environment and reproduce the cited workflows. Then, without reading the implementation, re-create a stratified train/validation/test pipeline, use `Pipeline` to prevent preprocessing leakage, compute AUROC/AUPRC/Brier and a confusion matrix, and implement a fail-closed inference interface. Next, draw and explain the RAG pipeline and rerun a source-disjoint retrieval test. Finally, practice how to report *negative* results with evidence rather than spinning them into a success story.

**Progress gate:** Count a project as ready only when you can rerun its benchmark on its documented environment, accurately explain its metrics, point to its exact artifacts, identify its primary failure mode, and work through code or design questions about it live. A green badge on its own does not satisfy the gate.

## All 19 repositories — portfolio positioning

These are the 19 accessible repository names during the October 2026 audit. Classification is about *how to present* each repository, not a claim that every pipeline has been rerun in this review.

| Repo | Position in interviews |
| --- | --- |
| `Healthcare-ML` | **Lead ML research-to-inference example** |
| `data-analytics-portfolio` | **Lead fraud-classification subproject** and Toronto 311 foundation |
| `NeuroEvoRAG` | **Lead retrieval/NLP project, with small-benchmark caveats** |
| `smart_traffic_signals_rl` | Research RL example; private; simulation-only outcome |
| `DiffRAG-SQL` | AI software evaluation and partial SQL generation; substantial accuracy gap |
| `adaptive_cyber_defense_rl_nlp` | Historic phishing/SMS ML; not live RL cybersecurity |
| `flood_forecasting_ai` | Real-data negative-model result and leakage-aware time splits |
| `market_risk_nlp_causal` | Negative financial classifier calibration finding; not proved causal or profitable |
| `ontario-health-causal-analysis` | Identification/provenance caution, not established policy causality |
| `open-banking-nlp-analysis` | Pretrained NLP exploratory classification; no labeled independent accuracy |
| `financial-forecasting-cadusd-corra-tsx` | Time-series baselines and public data QA |
| `wfm-schedule-optimizer` | Optimization, scheduling, privacy-aware operational engineering |
| `pbi-model-auditor-Public` | Static parser/compiler-adjacent tooling; not ML |
| `spotify-api-enhancer` | API/data-enrichment engineering; live auth unverified |
| `social-impact-funding-optimizer` | Mathematical optimization, not predictive ML |
| `toronto-climate-risk-assessment` | Descriptive official-source weather audit |
| `toronto-2025-data-science-portfolio` | Portfolio evidence index; not an independent ML project |
| `Tesla-GME-Dashboard-blob-main-final_project` | Financial visualization coursework; not an ML lead |
| `jibrankazi` | GitHub profile landing page |

**Priority for actual career preparation:** Make two deep project walkthroughs (Healthcare and Fraud) excellent, one NLP/RAG walkthrough credible, and one experimental RL demonstration technically transparent. Only then broaden to the rest of the repository list. Keep using honest public-source evidence and interview rehearsal rather than polishing status badges.
