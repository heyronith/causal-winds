# Causal Flight Cancellation Prediction: Project Plan

## First Principles Breakdown

### Core Problem
**What do we need to know?**
- What actually causes flight cancellations (not just what correlates)
- How much does each cause contribute?
- What can we do about it?

### Fundamental Questions
1. **Prediction**: Will this flight be cancelled?
2. **Attribution**: If cancelled, what caused it?
3. **Intervention**: What actions prevent cancellations?

---

## Project Structure

```
flight-cancels/
├── data/
│   ├── raw/              # Raw data files
│   ├── processed/        # Cleaned, feature-engineered data
│   └── external/         # Weather, airport data
├── notebooks/
│   ├── 01_data_collection.ipynb
│   ├── 02_eda.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_baseline_models.ipynb
│   ├── 05_causal_analysis.ipynb
│   └── 06_attribution_model.ipynb
├── src/
│   ├── data/
│   │   ├── collectors.py      # Data fetching
│   │   ├── processors.py      # Data cleaning
│   │   └── features.py        # Feature engineering
│   ├── models/
│   │   ├── baseline.py        # Simple prediction models
│   │   ├── causal.py          # Causal inference methods
│   │   └── attribution.py     # Attribution model
│   ├── evaluation/
│   │   ├── metrics.py         # Custom metrics
│   │   └── visualization.py   # Attribution plots
│   └── utils/
│       └── config.py          # Configuration
├── configs/
│   └── config.yaml            # Hyperparameters, paths
├── requirements.txt
├── README.md
└── PROJECT_PLAN.md
```

---

## 4-6 Week Timeline

### Week 1: Data & Foundation
**Goal**: Get data, understand it, build baseline

**Tasks**:
- [ ] Collect flight data (BTS or FlightAware API)
- [ ] Collect weather data (NOAA)
- [ ] Collect airport/airline metadata
- [ ] EDA: cancellation rates, patterns, correlations
- [ ] Build simple baseline (logistic regression, XGBoost)
- [ ] Establish evaluation metrics (precision, recall, F1, calibration)

**Deliverable**: Baseline model with 70%+ accuracy

---

### Week 2: Feature Engineering & Time Series
**Goal**: Create predictive features, handle temporal patterns

**Tasks**:
- [ ] Time-based features (hour, day, season, holidays)
- [ ] Weather features (precipitation, wind, visibility, temperature)
- [ ] Airport features (size, congestion, historical cancellation rate)
- [ ] Airline features (historical performance, fleet size)
- [ ] Route features (distance, popularity, alternatives)
- [ ] Lag features (cancellations in past 24h, 7d)
- [ ] Time series transformer (PatchTST or TST) for sequential patterns

**Deliverable**: Feature set + time series model (80%+ accuracy)

---

### Week 3: Causal Inference Setup
**Goal**: Identify causal relationships, not just correlations

**Tasks**:
- [ ] Build causal graph (what causes what?)
- [ ] Identify confounders (variables affecting both treatment and outcome)
- [ ] Implement propensity score matching
- [ ] Difference-in-differences for weather effects
- [ ] Instrumental variables (if applicable)
- [ ] Validate causal assumptions

**Deliverable**: Causal model quantifying weather vs. operational effects

---

### Week 4: Attribution Model
**Goal**: Attribute each cancellation to specific causes

**Tasks**:
- [ ] Shapley values for feature attribution
- [ ] Counterfactual analysis ("what if weather was better?")
- [ ] Build attribution classifier (weather vs. mechanical vs. crew vs. other)
- [ ] Quantify contribution percentages
- [ ] Validate attribution with known cancellation reasons (if available)

**Deliverable**: Attribution model that explains cancellation causes

---

### Week 5: Integration & Evaluation
**Goal**: Combine prediction + attribution, evaluate end-to-end

**Tasks**:
- [ ] Integrate prediction + attribution pipeline
- [ ] Build evaluation framework (prediction accuracy + attribution accuracy)
- [ ] Create visualizations (attribution plots, causal graphs)
- [ ] Test on held-out data
- [ ] Compare controllable vs. uncontrollable factors

**Deliverable**: End-to-end system with evaluation

---

### Week 6: Documentation & Portfolio
**Goal**: Make it portfolio-ready

**Tasks**:
- [ ] Write comprehensive README
- [ ] Create demo notebook with examples
- [ ] Build simple dashboard/visualization
- [ ] Document methodology and findings
- [ ] Prepare presentation slides
- [ ] Deploy model (optional: Streamlit/Flask)

**Deliverable**: Portfolio-ready project with documentation

---

## Technical Stack

### Core
- **Python 3.9+**
- **Pandas, NumPy**: Data manipulation
- **Scikit-learn**: Baseline models, preprocessing
- **XGBoost/LightGBM**: Gradient boosting

### ML/DL
- **PyTorch/TensorFlow**: Deep learning
- **Transformers (HuggingFace)**: Time series transformers
- **DoWhy/EconML**: Causal inference
- **SHAP**: Attribution

### Data
- **Requests/BeautifulSoup**: Web scraping
- **SQLite/PostgreSQL**: Data storage (if needed)

### Visualization
- **Matplotlib, Seaborn**: Static plots
- **Plotly**: Interactive visualizations
- **NetworkX**: Causal graph visualization

---

## Key Metrics

### Prediction Metrics
- **Accuracy**: Overall correctness
- **Precision**: Of predicted cancellations, how many actually cancelled?
- **Recall**: Of actual cancellations, how many did we catch?
- **F1-Score**: Balance of precision/recall
- **Calibration**: Do predicted probabilities match actual rates?

### Attribution Metrics
- **Attribution Accuracy**: How often do we correctly identify the cause?
- **Causal Effect Size**: Quantified impact of each factor
- **Counterfactual Accuracy**: How well do counterfactuals match reality?

---

## Data Sources

### Primary
1. **Bureau of Transportation Statistics (BTS)**
   - Free, comprehensive flight data
   - Includes cancellation reasons
   - API: https://www.transtats.bts.gov/

2. **NOAA Weather Data**
   - Free, historical weather
   - API: https://www.ncei.noaa.gov/

### Secondary
3. **FlightAware API** (if free tier available)
4. **OpenSky Network** (flight tracking)
5. **Airport/airline websites** (scraping for operational data)

---

## Causal Framework

### Causal Graph Structure
```
Weather → Cancellation
Operations → Cancellation
Airport Capacity → Cancellation
Time/Season → Weather, Operations, Cancellation
```

### Identification Strategy
1. **Weather effects**: Use instrumental variables (distant weather as instrument)
2. **Operational effects**: Difference-in-differences (compare similar flights)
3. **Confounders**: Control for time, route, airline characteristics

### Validation
- Compare causal estimates to known cancellation reasons (BTS data)
- Sensitivity analysis (robustness checks)
- Placebo tests (random weather shouldn't affect cancellations)

---

## Success Criteria

### Minimum Viable
- [ ] 75%+ prediction accuracy
- [ ] Identifies top 3 cancellation causes
- [ ] Quantifies weather vs. operational contributions

### Stretch Goals
- [ ] 85%+ prediction accuracy
- [ ] Real-time prediction system
- [ ] Intervention recommendations
- [ ] Multi-airline comparison dashboard

---

## Risk Mitigation

| Risk | Mitigation |
|------|------------|
| Data access issues | Start with BTS (free, reliable) |
| Causal inference complexity | Use established libraries (DoWhy) |
| Time constraints | Focus on 1-2 causal methods, not all |
| Attribution validation | Use BTS cancellation reason codes |

---

## Next Steps

1. **Set up project structure** (run commands below)
2. **Get API keys/access** (BTS, NOAA)
3. **Collect sample data** (1 month to start)
4. **Begin Week 1 tasks**

---

## First Principles Checklist

- [x] Defined core problem (causation, not correlation)
- [x] Identified fundamental questions (prediction, attribution, intervention)
- [x] Built from ground up (data → features → models → causal → attribution)
- [x] Validated assumptions (causal inference requires careful setup)
- [x] Measured what matters (prediction + attribution accuracy)

