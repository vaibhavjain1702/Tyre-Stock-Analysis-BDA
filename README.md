# Stock Market Analysis — Tyre Industry (BDA Project)

Comprehensive exploratory analysis and predictive modeling for Indian tyre sector tickers (MRF, JK Tyre, CEAT, Apollo Tyres). The project builds features, trains multiple models, evaluates performance, and generates plots and comparison metrics.

## Project Structure

- api.py — Fetches recent news from NewsAPI for each company and scores headline sentiment with VADER. Requires the `NEWS_API_KEY` environment variable (see `.env.example`).
- data.py — Data prep, feature engineering, train/test split, and saving datasets
- intraday.py — Intraday data handling (optional)
- merge.py — Data merging/cleaning pipelines
- stock_analysis.py — EDA, modeling, training, evaluation, plots
- test_csv.py — Quick CSV checks/utilities
- models/ — Saved models, scalers, and cross-validation outputs
  - *.pkl — Trained models and scalers per ticker
  - model_comparison.csv — Cross-ticker model summary
  - model_cv_results.csv / model_cv_results_detailed.csv — CV metrics
  - summary_metrics.txt — Key metrics summary (per ticker/model)
- plots/ — Visual outputs (EDA + modeling)
  - closing_prices.png, trading_volume.png, daily_returns_distribution.png, volatility.png
  - [Ticker]_moving_averages.png, [Ticker]_predictions.png, [Ticker]_rmse_bar.png, [Ticker]_r2_bar.png
  - JK_Tyre_feature_importance.png (if tree-based models)
  - Model_Comparison_All_Tickers.png
- *.csv — Input datasets
  - tyre_stock_data.csv, tyre_intraday_data.csv, tyre_news_sentiment.csv, tyre_financials.csv, tyre_final_data.csv

## Setup

1) Python version
- Recommended: Python 3.9–3.11

2) Create and activate a virtual environment
- macOS/Linux:
  - python3 -m venv .venv
  - source .venv/bin/activate
- Windows (PowerShell):
  - python -m venv .venv
  - .venv\\Scripts\\Activate.ps1

3) Install dependencies
- pip install -r requirements.txt

## How to Run

The standard end-to-end flow (adjust as per your use case):

1. Merge/prepare data
- python merge.py

2. Feature engineering and dataset creation
- python data.py

3. Exploratory analysis and modeling (plots, metrics, models)
- python stock_analysis.py

4. Optional utilities
- python api.py
- python intraday.py
- python test_csv.py

Outputs:
- Plots saved under plots/
- Models and metrics saved under models/

## Data Inputs and Outputs

Inputs (CSV):
- tyre_stock_data.csv — Daily OHLCV and related stock data
- tyre_intraday_data.csv — Intraday ticks/intervals (if used)
- tyre_news_sentiment.csv — News sentiment features (if used)
- tyre_financials.csv — Financial indicators/features (if used)
- tyre_final_data.csv — Final merged/engineered dataset for modeling

Outputs:
- models/*.pkl — Trained models and scalers per ticker
- models/model_comparison.csv — Cross-ticker summary
- models/model_cv_results.csv, models/model_cv_results_detailed.csv — CV metrics
- models/summary_metrics.txt — Consolidated metrics
- plots/*.png — EDA and modeling visualizations

## Reproducibility Notes

- Set random seeds in training code (scikit-learn estimators use random_state) to ensure deterministic results.
- Ensure consistent date ranges for train/test splits across tickers for comparability.
- If external data is fetched (e.g., APIs), pin data retrieval dates to avoid evolving targets.

## Assumptions/Limitations

- Models are trained on historical features; real-time deployment requires data latency handling.
- Exogenous variables (macro/news) may be partial or noisy; interpretability should be corroborated with domain insights.
- Price levels are non-stationary; performance should be validated with robust splits and baseline checks.

## Regenerating Plots and Metrics

- Re-run stock_analysis.py to refresh plots in plots/ and metrics in models/.
- If you retrain, older models in models/ may be overwritten; archive if necessary.

## Citation and Sources

- Data sources: specify your vendors/APIs or files used (e.g., NSE/BSE data provider, yfinance, internal CSVs).
- If you used research code or templates, acknowledge accordingly.

## License

- Academic use only unless otherwise specified. Add a LICENSE file (e.g., MIT) if you plan to share publicly.
