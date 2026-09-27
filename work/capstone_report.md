# Capstone Report — Refresh / Content Opportunity Scoring

- **Author:** Anurag Panda
- **Lane:** REFRESH / CONTENT OPPORTUNITY SCORING
- **Repo:** [https://github.com/AnuragPanda700/flyrank-ml-internship](https://github.com/AnuragPanda700/flyrank-ml-internship)
- **Deployed Paper:** [https://anuragpanda700.github.io/flyrank-ml-internship/](https://anuragpanda700.github.io/flyrank-ml-internship/)
- **Date:** September 2026

---

## 0. Abstract

Can observational Google Search Console signals predict impending organic traffic decay to prioritize content refresh decisions across enterprise websites? Analyzing a multi-client portfolio of 92,548 content URLs from the FlyRank internship warehouse across March 2026, we framed a pre-decision observation window (Days 1–15) to detect a 20% or greater impression drop in the outcome window (Days 16–31). Using an honest grouped split across client domains to prevent identity leakage, we trained a balanced logistic regression classifier against pre-decision search volume, click engagement, ranking position, and active impression days. On unseen holdout clients, the model achieved a Precision@50 of 48.0% (ROC-AUC 0.5905, PR-AUC 0.4192), outperforming a transparent heuristic rule baseline (Precision@50 of 20.0%) and delivering a +11.0 percentage-point lift over the holdout base rate. The resulting Content Action Playbook translates calibrated risk probabilities into an editorial triage queue with diagnostic reason codes, content archetypes, and mandatory human-review guardrails for organic growth teams.

---

## 1. Problem framing

Enterprise content publishers manage catalogs of tens of thousands to hundreds of thousands of organic search URLs. In any given month, a substantial fraction of this inventory suffers from traffic decay due to content staleness, search intent drift, evolving competitor coverage, or algorithmic SERP layout changes.

However, editorial and SEO bandwidth is strictly constrained: an editorial team can realistically optimize only 20 to 50 URLs per week. Currently, content refresh decisions rely either on unassisted editorial intuition or simplistic heuristic rules (e.g., sorting by historical pageviews). This leads to two critical failure modes:
1. **Wasted Editorial Labor (False Alarms)**: Rewriting stable evergreen pages that did not actually decay, wasting expensive editorial hours.
2. **Ignored Catastrophic Collapse (Blind Spots)**: Missing high-exposure pillar URLs whose traffic plummeted silently because pre-decision monthly aggregates appeared satisfactory.

This capstone builds an **observational decision-support queue** that scores URL inventory, estimates decay probability, assigns human-understandable reason codes, and groups content into actionable strategic archetypes. The cost of a wrong call is substantial: autonomous publishing risks penalties from low-quality AI content, while ignoring collapsing pillar pages damages sitewide organic revenue. Machine learning helps by filtering 92,000+ candidate URLs down to a high-conviction queue of 50 URLs where human inspection yields the highest commercial payoff.

---

## 2. Data safety

This analysis utilizes the **FlyRank Internship Warehouse release (v20260703)**, hosted on Hugging Face (`hf://datasets/FlyRank/internship-warehouse`).
- **Underlying Fact Table**: `fact_content_daily_performance` (78.8M rows, grain: `report_date × client_hash_id × content_hash_id`).
- **Partition Evaluated**: Mid-panel partition `month=2026-03` (March 1–31, 2026).
- **Inclusion Filter**: Content items with `gsc_data_available IS TRUE` and cumulative observation impressions `imp_obs >= 50`, yielding **92,548 items across 40 distinct client domains**.

### Deliberate Exclusions & Public Data Safety
- All client identifiers (`client_hash_id`) and content identifiers (`content_hash_id`) are pseudonymous hashes used exclusively for grouping and joining, never as model features.
- Zero raw URLs, client domains, or private queries are ingested, stored, or displayed anywhere in `work/` or the public paper.
- The outcome variable (`imp_outcome`) is strictly quarantined to target label derivation; it is never used as an input feature.
- Label-derived fields (`trend_direction`, `trend_pct`) are completely excluded.
- Credentials (`HF_TOKEN`) are resolved exclusively through environment variables and never logged or committed.

---

## 3. Baseline

We compare against the **Transparent Heuristic Rule Baseline** developed in **ML-07**:
$$\text{Score}_{\text{baseline}} = 0.40 \cdot V + 0.25 \cdot F + 0.25 \cdot P + 0.10 \cdot C$$
where:
- $V$ is the percentile rank of log impressions (`visibility_score`).
- $F$ is the freshness risk derived from inactive days (`(15 - active_days_obs) / 15`).
- $P$ is position opportunity (`avg_position_obs` clipped to $[1, 50]$).
- $C$ is CTR deficit relative to impressions.

### Baseline Performance on Identical Holdout Test Set
Evaluated on the exact same 22,531 items from 8 unseen holdout clients:
- Precision@10: 20.00%
- Precision@20: 20.00%
- Precision@50: 20.00%
- Precision@100: 24.00%
- ROC-AUC: 0.4612
- PR-AUC: 0.3404
- Holdout Base Rate: 36.95%

The baseline rule performs substantially worse than random unassisted sampling in the top-50 queue (20.0% vs 37.0% base rate), because it conflates large impression volume with decay risk without accounting for protective click signals.

---

## 4. Model / analysis

### Target Label Definition
Traffic decay is defined as a 20% or greater relative contraction in organic search impressions between the observation window and outcome window:
$$\text{is\_declining} = \begin{cases} 1 & \text{if } \text{imp\_outcome} < 0.80 \times \text{imp\_obs} \\ 0 & \text{otherwise} \end{cases}$$

### Feature Space (5 Pre-Decision Signals)
1. `imp_obs`: Total impressions in Days 1–15 (scale and search exposure).
2. `clk_obs`: Total clicks in Days 1–15 (user intent fulfillment).
3. `active_days_obs`: Days with impressions $>0$ in Days 1–15 (freshness/stability proxy).
4. `avg_position_obs`: Average Google search ranking position.
5. `ctr_obs`: Observed click-through efficiency rate percentage.

### Modeling Method Choice
We employ a **Balanced Logistic Regression** pipeline with standard scaling (`StandardScaler`). Logistic regression was chosen because:
1. It produces calibrated, interpretable risk probabilities that directly support cost/value triage.
2. Individual feature coefficients map directly to transparent editorial reason codes.
3. In comparative testing in ML-08, Logistic Regression outperformed or matched non-linear alternatives (Decision Tree, MLP) while providing complete mathematical auditability and zero risk of memorizing noisy domain tokens.

---

## 5. Evaluation

### Grouped Split Architecture
To prevent **client identity leakage**, we implement a **GroupShuffleSplit by `client_hash_id`** ($80\%$ train, $20\%$ test, seed=42):
- **Train Set**: 70,017 items across 32 clients (Base rate: 25.97%).
- **Test Set**: 22,531 items across 8 unseen clients (Base rate: 36.95%).
- **Client Overlap**: Exactly 0 clients.

### Model vs Baseline Comparative Table (Identical Test Split)

| Method / Model | Holdout Base Rate | Precision@10 | Precision@20 | Precision@50 | Precision@100 | ROC-AUC | PR-AUC |
|---|---|---|---|---|---|---|---|
| **Holdout Base Rate (Random)** | 36.95% | 36.95% | 36.95% | 36.95% | 36.95% | 0.5000 | 0.3695 |
| **Heuristic Baseline (ML-07)** | 36.95% | 20.00% | 20.00% | 20.00% | 24.00% | 0.4612 | 0.3404 |
| **Logistic Regression (ML-08/10)** | **36.95%** | **50.00%** | **40.00%** | **48.00%** | **51.00%** | **0.5905** | **0.4192** |

### Error Analysis & Concrete Hard Cases
1. **High-Conviction False Positive (Zero-Click Query Intent)**: `content_34a70fea29d15f24` (Client `client_62f4a7e64f5e0096`). Observed: 73,639 impressions, 18 clicks, pos 2.8, CTR 0.02%. Outcome: 69,380 impressions (stable, did not decay). Model score was 0.9962 because low CTR simulated decay risk. In reality, the query was navigational/informational where users received immediate answers without clicking.
2. **Sudden Algorithmic Collapse (False Negative)**: `content_922f95c9418ff0ec`. Observed: 34,384 impressions, 231 clicks, pos 3.4, CTR 0.67%. Outcome: 20,227 impressions (-41% collapse). Model score was 0.0187 (deemed safe) because pre-decision metrics were pristine. The collapse was driven by external SERP layout changes (Google AI Overviews / competitor snippet loss) undetectable from historical Search Console logs.

---

## 6. Interpretation

### Feature Importance & Odds Ratios
- **Pre-Decision Clicks (`clk_obs`, Odds Ratio = 0.591, Coef = -0.5262)**: Clicks are the single strongest protective signal against traffic decline. Pages that capture clicks satisfy user intent and maintain search stability.
- **Impression Scale (`imp_obs`, Coef = +0.2768) + Low CTR (`ctr_obs`, Coef = -0.1363)**: High impressions with low CTR indicate search exposure without engagement, exposing pages to algorithmic testing and vulnerability.
- **Active Days Dropoff (`active_days_obs`, Coef = +0.2548)**: URLs exhibiting gaps in daily active impressions indicate fading indexation breadth prior to traffic decline.

### Surprises & Negative Results
- **Position Alone is Weak**: Average position has a negligible predictive weight (+0.0779) compared to click engagement. A page ranking #3 with zero clicks is far more vulnerable than a page ranking #8 with strong click capture.
- **Client Concentration**: Top 3 clients represent 52.4% of total volume. Ungrouped models achieve higher naive AUC (0.6173) by memorizing client domain authority, but collapse on unseen websites.

---

## 7. Recommendation

### Strategic Content Archetypes
1. **At-Risk Portfolio Pillar (`imp >= 1500`, `decay_risk >= 0.50`)**: Action: `PROTECT & AUDIT SERP`. Priority: **P1 (Urgent Gate)**. Mission-critical asset; mandatory dual human sign-off; inspect SERP for AI Overviews and competitor shifts.
2. **Striking Distance Opportunity (`4 <= pos <= 15`, `ctr < 2.0%`)**: Action: `IMPROVE SNIPPET & CTR`. Priority: **P2 (High ROI)**. Quick win; rewrite title tag hooks and meta descriptions.
3. **Fading Evergreen (`imp >= 250`, `active_days <= 12`, `decay_risk >= 0.45`)**: Action: `DEEP REWRITE / REFRESH`. Priority: **P2 (Planned)**. Update outdated facts and expand topical depth.
4. **Zero-Click Info Asset (`imp >= 250`, `clk <= 2`, `pos <= 5`)**: Action: `MONITOR INTENT (DO NOT REWRITE)`. Priority: **P3**. Preserves rankings; avoids unforced errors.
5. **Thin / Zombie Content (`imp < 100`, `pos > 20`, `active <= 7`)**: Action: `CONSOLIDATE / MERGE or PRUNE`. Priority: **P3**. 301-redirect into parent pillar or apply `noindex`.
6. **Stable Core Asset (`decay_risk < 0.35`, `active >= 12`)**: Action: `MONITOR ONLY`. Priority: **P3**. Leave untouched.

### Strict NO-GO Automation Guardrails
- **NO Autonomous Publishing**: Unreviewed AI rewrites violate Google Quality guidelines.
- **NO Autonomous Deletion (404/410)**: Destroys backlink equity and converting assets.
- **NO Autonomous 301 Merging**: Algorithmic redirects cause query mismatch and topical dilution.
- **NO Autonomous Changes to Core Pillar Pages**: Mission-critical URLs require human editorial and commercial review.

---

## 8. Reproducibility

Every result, metric, chart, and queue in this capstone is 100% reproducible from clean state:
- **Repository**: [https://github.com/AnuragPanda700/flyrank-ml-internship](https://github.com/AnuragPanda700/flyrank-ml-internship)
- **Deployed Research Paper**: [https://anuragpanda700.github.io/flyrank-ml-internship/](https://anuragpanda700.github.io/flyrank-ml-internship/)
- **Core Notebooks**:
  - `work/notebooks/capstone.ipynb` (Capstone analytical backbone)
  - `work/notebooks/w07_action_playbook.ipynb` (Action Playbook & Queue)
  - `work/notebooks/w06_validation_audit.ipynb` (Validation Audit & Leakage Confession)
  - `work/notebooks/w05_model.ipynb` (Modeling Lane & Comparison)
  - `work/notebooks/w04_baseline_score.ipynb` (Rule Baseline & Top-20 Review)
  - `work/notebooks/w03_data_contract.ipynb` (Data Contract & Grain Verification)
- **Committed Receipts**:
  - `work/outputs/playbook_metrics.json`
  - `work/outputs/baseline_metrics.json`
- **Seeds & Environment**: Python 3.12+, DuckDB 1.5+, Scikit-Learn 1.9+, Pandas 3.0+. GroupShuffleSplit `random_state=42`, LogisticRegression `random_state=42`, `class_weight='balanced'`.

---

## 9. Acknowledgments & data credit

This capstone research project was conducted as part of the **FlyRank AI Internship — Machine Learning Track** (Summer 2026).

**Built on the FlyRank ML Internship dataset**  
Data access, warehouse releases, and research guidance provided by [FlyRank AI (https://flyrank.ai)](https://flyrank.ai).
