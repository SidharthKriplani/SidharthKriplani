# Contribution Log — Sidharth Kriplani

> All work here is solo-built unless otherwise noted. This log summarizes the engineering contributions across each repository in chronological order.

---

## RiskFrame Platform

**Repo:** `riskframe_platform`
**Focus:** Credit default risk scoring, model governance, ECOA fairness

| Contribution | Description |
|-------------|-------------|
| Feature engineering pipeline | 7-step pipeline: missingness drop, categorical encoding, ratio features (credit_income_ratio, annuity_income_ratio, credit_term, days_employed_pct), median imputation, SelectKBest top-40 |
| XGBoost champion training | HPO grid search over learning_rate × subsample; PR AUC = 0.2611, ROC AUC = 0.7663, ECE = 0.0046 |
| LightGBM challenger | Matched hyperparameters, 5-gate promotion evaluation, HOLD decision (delta PR AUC = −0.0001) |
| Shadow deployment system | 17-day shadow window (Day 10 – Day 27), 3,247 applications scored in parallel, no live decision impact |
| PSI drift monitoring | Score-level and feature-level PSI; Day 14 DRIFT ALERT (PSI = 0.2296 > 0.20 threshold) |
| Policy management | v1.0 → v1.1 migration triggered by drift; APPROVE threshold 0.08 → 0.06, DECLINE 0.25 → 0.28 |
| ECOA fairness framework | Disparate Impact ratio = 1.059 (safe harbor), ongoing batch-level DI monitoring |
| Adverse action codes | SHAP-based reason code generation (AA01–AA05), model-grounded per-application attribution |
| 5-gate promotion framework | Gates: PR AUC, ROC AUC, Brier Score, DI ratio, approval rate delta |
| Golden scenario suite | 12/12 golden scenarios pass; covers APPROVE, REFER, DECLINE, fairness, shadow routing, missingness |
| Integrity tests | 10/10 integrity tests; score range, DI bounds, NaN-free, threshold monotonicity, SHAP additivity |
| 18 JSON artifacts | Complete evidence trail from training through governance board decision |

---

## PulseRank Platform

**Repo:** `pulserank_platform`
**Focus:** Marketplace recommendation, ranking debiasing, exposure governance

| Contribution | Description |
|-------------|-------------|
| IPS debiasing | Inverse propensity scoring with rank-based propensity model; click × (1/propensity(rank)), max_weight=5.0 |
| Bias measurement | Naive NDCG@10 = 0.134 vs IPS-weighted NDCG@10 = 0.522 (3.9× gap exposed) |
| MMR diversity reranking | λ=0.70, max_per_seller=2, category_cap=50%, novelty_bonus=0.04 |
| Fairness metrics | Seller Gini 0.74 → 0.582 (21% reduction); Catalog Coverage@10: 0.150 → 0.226 (50% increase) |
| Offline A/B simulation | 4,132 sessions, 650 items, 80 sellers; HOLD_SIMULATED (NDCG −7.9% relative) |
| Delayed attribution system | Attribution with configurable delay window; distinguishes observed vs. attributed clicks |
| 33 JSON artifacts | Evidence artifacts for all pipeline stages |
| 15 failure scenarios | Complete failure mode catalog for ranking, attribution, and governance systems |

---

## DevPulse Platform

**Repo:** `devpulse_platform`
**Focus:** RAG-based developer migration intelligence, version-safe answers

| Contribution | Description |
|-------------|-------------|
| LLM-Last architecture | Grounding + conflict detection before LLM synthesis; prevents wrong-version hallucination |
| Hybrid retrieval | BM25 + vector + RRF with version pre-filtering; Recall@5 = 0.97 |
| Conflict detection engine | 4 conflict types: same_api_different_behavior, version_ordering_violation, version_deprecation_conflict, stale_doc_detected |
| Verdict engine | 3-level verdicts: BLOCKED / RISKY / SAFE with evidence citations |
| Goal Mode | 6 agentic components: GoalParser, DependencyDeltaDetector, TaskPlanner, TaskExecutor, RecoveryDecider, PlanSummaryReporter |
| Semver utilities | parse_semver, semver_lt, semver_distance (≥2 → CRITICAL, =1 → HIGH) |
| Recovery logic | Retry cap = 2; 4 recovery actions: skip_and_escalate / retry_with_related_evidence / retry_cross_source / mark_escalated |
| Evaluation | Wrong-version answer rate = 0.0, Macro F1 = 0.966 |
| 70 JSON artifacts | Complete evaluation and pipeline evidence trail |
| 19 failure scenarios | Failure mode catalog for retrieval, conflict detection, and agentic recovery |

---

## MetaSignal Platform

**Repo:** `metasignal_platform`
**Focus:** A/B experiment analysis, CUPED, guardrail-first decisioning

| Contribution | Description |
|-------------|-------------|
| CUPED implementation | Pre-experiment covariate adjustment; variance reduction verified up to 40% |
| Guardrail-first framework | Experiment blocked if any guardrail metric (latency, error rate, revenue) degrades beyond threshold |
| A/A calibration | 1,000-run A/A simulation; false positive rate verified at α = 0.05 |
| SRM detection | Sample ratio mismatch detection with chi-square test and diagnostic attribution |
| Sequential testing | mSPRT streaming early warning system for continuous monitoring |
| Evidence layer | FastAPI serving layer for experiment result retrieval and audit trail |

---

## MetricLens

**Repo:** `metriclens`
**Focus:** Business analytics metric decomposition

| Contribution | Description |
|-------------|-------------|
| Mix/rate decomposition | Decomposes metric changes into mix_effect + rate_effect + interaction_effect per segment |
| DataFrame-native API | Works directly on pandas DataFrames without schema declaration |
| Waterfall visualization | Matplotlib/plotly waterfall chart generation from decomposition results |
| v0.2 test suite | Golden scenarios for decomposition correctness, edge cases for single-segment and equal-split scenarios |

---

## TrialCheck

**Repo:** `trialcheck_v0`
**Focus:** A/B experiment readout auditing

| Contribution | Description |
|-------------|-------------|
| SRM detection | Chi-square test for sample ratio mismatch with expected vs. observed traffic split |
| Power analysis | Post-hoc power calculation; flags underpowered tests |
| Multiple comparison correction | Bonferroni and BH correction for multi-metric experiments |
| Peeking detection | Sequential test boundary violation detection |
| CLI interface | `trialcheck audit` command with JSON and HTML output modes |
| v0.2.0 release | PyPI published; GitHub Actions CI/CD pipeline |

---

## FeatureLeakageLens

**Repo:** `featureleakagelens_v0`
**Focus:** Pre-training feature leakage detection

| Contribution | Description |
|-------------|-------------|
| Target leakage detection | Mutual information and correlation-based detection of features that directly encode the label |
| Temporal leakage detection | Column name pattern matching + statistical tests for features that encode post-event information |
| Train/test overlap | Row-level hash comparison for dataset contamination |
| Near-duplicate feature detection | Pairwise correlation matrix with configurable threshold |
| v0.4.0 release | Version bump with expanded test coverage |

---

## GoldenSetAuditor

**Repo:** `goldensetauditor_v0`
**Focus:** LLM/RAG evaluation dataset quality auditing

| Contribution | Description |
|-------------|-------------|
| Answer completeness check | Detects empty, too-short, or template-filled answers in golden sets |
| Question ambiguity detection | Flags questions with multiple interpretable meanings |
| Context coverage validation | Ensures referenced context passages contain the answer span |
| Contamination detection | Near-duplicate detection between evaluation set and training corpus |
| JSONL/JSON input support | Flexible input format handling for diverse RAG evaluation formats |
| v0.5.0 release | Version bump with coverage expansion |

---

## DocIngestQA

**Repo:** `docingestqa`
**Focus:** Pre-indexing RAG document ingestion QA

| Contribution | Description |
|-------------|-------------|
| 11 deterministic checks | Missing pages, OCR noise, duplicates, encoding corruption, poor split boundaries, metadata completeness |
| Multi-format output | JSON, Markdown, HTML report generation from a single audit run |
| CLI interface | `docingestqa audit` command with configurable check selection |
| PyPI package | Published to PyPI; installable via `pip install docingestqa` |
| v0.2.0 release | Expanded checks + test coverage |

---

*Last updated: May 2026*
