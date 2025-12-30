# Causal Flight Cancellation Prediction

A machine learning project that predicts flight cancellations and attributes them to specific causes using causal inference methods.

## Problem Statement

Most flight cancellation models only predict *if* a flight will be cancelled, but don't explain *why*. This project goes beyond correlation to identify causal relationships, answering:

- **What actually causes cancellations?** (not just what correlates)
- **How much does each factor contribute?** (weather vs. operations vs. other)
- **What can be done about it?** (intervention recommendations)

## Key Features

- **Prediction**: Forecast flight cancellations with high accuracy
- **Attribution**: Identify specific causes (weather, mechanical, crew, etc.)
- **Causal Analysis**: Quantify true causal effects, not just correlations
- **Intervention Insights**: Understand what actions prevent cancellations

## Technical Approach

1. **Baseline Models**: XGBoost, time series transformers
2. **Causal Inference**: Difference-in-differences, propensity score matching
3. **Attribution**: Shapley values, counterfactual analysis
4. **Evaluation**: Prediction accuracy + attribution accuracy

## Project Structure

```
flight-cancels/
├── data/           # Raw and processed data
├── notebooks/      # Jupyter notebooks for analysis
├── src/            # Source code modules
├── configs/        # Configuration files
└── requirements.txt
```

## Getting Started

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Set Up Data

- Get BTS API access (free): https://www.transtats.bts.gov/
- Get NOAA weather data (free): https://www.ncei.noaa.gov/
- Create `.env` file for API keys (if needed)

### 3. Run Analysis

Start with notebooks in order:
1. `01_data_collection.ipynb`
2. `02_eda.ipynb`
3. `03_feature_engineering.ipynb`
4. ...

## Timeline

- **Week 1**: Data collection & baseline models
- **Week 2**: Feature engineering & time series
- **Week 3**: Causal inference setup
- **Week 4**: Attribution model
- **Week 5**: Integration & evaluation
- **Week 6**: Documentation & portfolio

## Results

(To be updated as project progresses)

## License

MIT

