<div align="center">

**Senior ML Engineer · Production Systems · Governance-First ML**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)]([https://linkedin.com/in/sidharthkriplani](https://www.linkedin.com/in/sidharth-kriplani/))
[![Email](https://img.shields.io/badge/Email-sidharthkriplani%40gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:sidharthkriplani@gmail.com)

</div>

---

## What I Build

I build **production-grade ML and AI systems** — not models in notebooks. Every project here is a complete platform: training, evaluation, governance, monitoring, serving, and fairness — with evidence artifacts that prove each component works.

My focus areas: **agentic LLM pipelines** with deterministic safety guarantees, **recommendation and ranking systems**, **credit and risk decisioning**, **developer intelligence tooling**, **experiment analysis platforms**, and **ML data quality auditing**.

---

## Platforms

### 🎯 PulseRank — Marketplace Ranking & Recommendation
[`pulserank_platform`](https://github.com/SidharthKriplani/pulserank_platform)

Production-simulated recommendation platform with IPS debiasing, MMR diversity reranking, delayed attribution, exposure governance, and offline A/B simulation.

- **IPS debiasing:** click × (1/propensity(rank)), clip max_weight=5.0 · Naive NDCG@10=0.134 → IPS-weighted NDCG@10=0.522
- **MMR diversity:** λ=0.70, max_per_seller=2, category_cap=50% · Seller Gini 0.74 → 0.582
- **A/B simulation:** 4,132 sessions, 650 items, 80 sellers, 33 JSON artifacts, 15 failure scenarios
- **A/B decision:** HOLD_SIMULATED (NDCG −7.9% relative, exceeds 5% threshold)

---

### 🔍 DevPulse — Developer Migration Intelligence
[`devpulse_platform`](https://github.com/SidharthKriplani/devpulse_platform)

RAG + agentic platform for version-safe developer change decisions. Detects conflicting documentation before LLM synthesis (LLM-Last architecture).

- **Hybrid retrieval:** BM25 + vector + RRF with version pre-filtering · Recall@5 = 0.97
- **Conflict detection:** 4 conflict types, 3 verdict levels (BLOCKED/RISKY/SAFE) · Wrong-version answer rate = 0.0
- **Goal Mode:** 6 agentic components, retry cap = 2, recovery actions · Macro F1 = 0.966
- **Semver utilities:** parse_semver, semver_lt, semver_distance (≥2 → CRITICAL, =1 → HIGH)

---

### 💳 RiskFrame — Credit Default Risk Decisioning
[`riskframe_platform`](https://github.com/SidharthKriplani/riskframe_platform)

Full ML lifecycle credit scoring platform on Home Credit dataset. Champion/challenger governance, ECOA fairness auditing, PSI drift monitoring, 5-gate promotion framework.

- **Champion XGBoost:** PR AUC = 0.2611, ROC AUC = 0.7663, ECE = 0.0046, Brier = 0.0673
- **Fairness:** Disparate Impact = 1.059 (ECOA safe harbor), SHAP-generated adverse action codes
- **Drift:** Day 14 PSI = 0.2296 (DRIFT ALERT > 0.20) → Policy v1.0 → v1.1 deployed
- **Challenger:** LightGBM 5/5 gates passed, HOLD (delta PR AUC = −0.0001, below material threshold)

---

### 📊 MetaSignal — A/B Experiment Analysis Platform
[`metasignal_platform`](https://github.com/SidharthKriplani/metasignal_platform)

Production experiment analysis platform with CUPED variance reduction, guardrail-first decisioning, A/A calibration, streaming early warning, and SRM detection.

- **CUPED:** Pre-experiment covariate adjustment · Variance reduction up to 40%
- **Guardrail-first:** Experiment blocked if any guardrail metric degrades beyond threshold
- **A/A validation:** 1,000 run calibration · False positive rate verified at α = 0.05
- **Streaming:** Early warning system with sequential testing (mSPRT)

---

## Libraries & Tools

### 📐 MetricLens — Metric Movement Decomposition
[`metriclens`](https://github.com/SidharthKriplani/metriclens)

DataFrame-native library for decomposing metric movements into mix shift vs. rate shift. Answers "a metric moved — where did it come from?"

```python
from metriclens import MetricLens
lens = MetricLens(df_before, df_after, segment_col="country", metric_col="conversion")
lens.decompose()  # → mix_effect, rate_effect, interaction_effect per segment
```

---

### 🧪 TrialCheck — A/B Experiment Readout Auditor
[`trialcheck_v0`](https://github.com/SidharthKriplani/trialcheck)

Platform-agnostic A/B experiment auditor. Catches SRM, underpowered tests, peeking violations, and multiple comparison issues before you ship a wrong decision.

```bash
trialcheck audit experiment_results.json --alpha 0.05 --min-power 0.80
```

---

### 🔬 FeatureLeakageLens — Pre-Training Leakage Detection
[`featureleakagelens_v0`](https://github.com/SidharthKriplani/featureleakagelens)

Pre-training tabular ML auditor for feature leakage. Detects target leakage, temporal leakage, train/test overlap, and near-duplicate features before you train.

```python
from featureleakagelens import LeakageAuditor
report = LeakageAuditor(df_train, df_test, target="label").audit()
```

---

### 🏆 GoldenSetAuditor — LLM/RAG Evaluation Dataset QA
[`goldensetauditor_v0`](https://github.com/SidharthKriplani/goldensetauditor)

Evaluation dataset quality auditor for LLM and RAG applications. Validates golden sets for answer completeness, question ambiguity, context coverage, and contamination.

```python
from goldensetauditor import GoldenSetAuditor
report = GoldenSetAuditor(golden_jsonl="eval_set.jsonl").audit()
```

---

### 📄 DocIngestQA — RAG Document Ingestion QA
[`docingestqa`](https://github.com/SidharthKriplani/docingestqa)

Pre-indexing QA auditor for RAG document ingestion. Runs 11 deterministic checks on exported chunks — missing pages, OCR noise, duplicates, encoding corruption, poor split boundaries.

```bash
pip install docingestqa
docingestqa audit chunks.jsonl --output report.html
```

---

### ⚖️ InferenceLens — Inference Cost/Quality Tradeoff Auditor
[`inferencelens`](https://github.com/SidharthKriplani/inferencelens)

Audits AI inference routing decisions — profiles calls across model configurations, finds the cost/quality Pareto frontier, and flags dominated configs with routing recommendations.

```python
from inferencelens import InferenceLens
report = InferenceLens(task_type="summarization").profile(prompts)
# → Pareto frontier, routing rules, PASS/WARN/FAIL verdict
```

---

## Applied Systems

Three production pipelines applying the same principles under domain pressure:

| System | Domain | Primary Failure Mode |
|--------|--------|----------------------|
| [`lendflow`](https://github.com/SidharthKriplani/lendflow) | Financial underwriting | When to stop or escalate |
| [`agentreliabilitylab`](https://github.com/SidharthKriplani/agentreliabilitylab) | Cyber threat triage | When to stop or escalate |
| [`nexussupply`](https://github.com/SidharthKriplani/nexussupply) | Supplier risk intelligence | Conflicting signal fusion |

Each uses LangGraph with deterministic-first architecture: scores are computed before LLM synthesis, escalation paths are explicit, and graceful degradation is guaranteed.

---

## The Thesis

Every project here addresses one of three failure modes in AI systems:

**① How does it know it's working correctly?**  
The system needs a verification signal independent of its own confidence.  
[`TrialCheck`](https://github.com/SidharthKriplani/trialcheck) · [`MetricLens`](https://github.com/SidharthKriplani/metriclens) · [`FeatureLeakageLens`](https://github.com/SidharthKriplani/featureleakagelens) · [`DocIngestQA`](https://github.com/SidharthKriplani/docingestqa) · [`GoldenSetAuditor`](https://github.com/SidharthKriplani/goldensetauditor) · [`RiskFrame`](https://github.com/SidharthKriplani/riskframe_platform) · [`PulseRank`](https://github.com/SidharthKriplani/pulserank_platform) · [`InferenceLens`](https://github.com/SidharthKriplani/inferencelens)

**② When should it stop or escalate?**  
The system needs explicit rules for when automated decisions require human judgment.  
[`MetaSignal`](https://github.com/SidharthKriplani/metasignal_platform) · [`LendFlow`](https://github.com/SidharthKriplani/lendflow) · [`AgentReliabilityLab`](https://github.com/SidharthKriplani/agentreliabilitylab)

**③ How does it handle conflicting information?**  
The system needs a deterministic anchor when multiple signals disagree.  
[`DevPulse`](https://github.com/SidharthKriplani/devpulse_platform) · [`NexusSupply`](https://github.com/SidharthKriplani/nexussupply)

> The original nine are domain-agnostic auditors. The three applied systems test the same thesis under production pressure.

---

## How the Projects Connect

```
Raw Application Data ──────────────────────────────────► RiskFrame
                                                          (risk scoring)

User Queries / Developer Questions ────────────────────► DevPulse
                                                          (version-safe answers)

Marketplace Events / Clicks ────────────────────────────► PulseRank
                                                          (ranking + debiasing)

A/B Experiment Results ────────────────────────────────► MetaSignal / TrialCheck
                                                          (experiment validity)

ML Training Data ──────────────────────────────────────► FeatureLeakageLens
                                                          (pre-training audit)

RAG Chunks / Eval Sets ─────────────────────────────────► DocIngestQA / GoldenSetAuditor
                                                           (data quality gates)

Metric Movement Explanation ───────────────────────────► MetricLens
                                                          (decomposition)
```

Every platform feeds downstream governance: PulseRank's A/B decisions are validated by MetaSignal's experiment framework. RiskFrame's evaluation data is audited by FeatureLeakageLens pre-training and GoldenSetAuditor post-training. DevPulse's RAG corpus passes through DocIngestQA before indexing.

---

## Engineering Standards

All repositories here follow a consistent production standard:

- **Tests:** pytest with golden scenarios, integrity tests, and property-based checks
- **Artifacts:** JSON evidence artifacts for all model and evaluation results
- **CI/CD:** GitHub Actions with lint, type-check, and test gates
- **Versioning:** Semantic versioning (major.minor.patch) with CHANGELOG
- **Documentation:** Defense documents, PRD documents, and README-level architecture diagrams

---

<div align="center">
<sub>All platforms are solo-built production simulations. Not deployed to production. Built to demonstrate production engineering depth.</sub>
</div>
