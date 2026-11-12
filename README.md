# Serbia Inflation Time-Series Analysis and Forecasting

A Jupyter Notebook project exploring monthly inflation and consumer-price-index data for Serbia. It compares a seasonal SARIMAX forecast with a simple drift baseline and uses time-series diagnostics to examine stationarity, trend, seasonality, and autocorrelation.

## Project notebooks

- **`in_11_2023_lancani (2).ipynb`** — analyzes monthly chain-index changes as an inflation rate. It applies STL decomposition, ADF and Ljung–Box tests, ACF/PACF diagnostics, and SARIMAX forecasting. It also compares a fixed holdout forecast with a drift baseline and performs walk-forward evaluation.
- **`in_11_2023_projekat_bazni.ipynb`** — analyzes the CPI base index (2006 average = 100), using log transformation, STL decomposition, stationarity checks, and an ARIMA forecast compared with a drift baseline.

The notebooks use different index definitions and data files, so their values and forecast metrics should not be compared as if they were the same target.

## Data

The `data/` directory contains the CSV inputs used by the notebooks:

- `Train.csv` — read by the chain-index notebook.
- `inflacija.csv` — read by the base-index notebook.

The project attributes its statistical data to the [Statistical Office of the Republic of Serbia](https://www.stat.gov.rs/). The notebooks expect the CSV files to remain in `data/` relative to the repository root.

## Methods and results

The chain-index notebook creates an 80/20 chronological train/test split and fits a SARIMAX model with order `(1, 1, 1)` and seasonal order `(0, 1, 1, 12)`. In the saved notebook output, the fixed-holdout forecast reports **MAE 0.47** and **RMSE 0.59**; the drift baseline reports **MAE 0.73**. Its walk-forward evaluation reports **MAE 0.3292** and **RMSE 0.4601**. These are results recorded in the notebook, not a guarantee of future performance.

The base-index notebook fits an ARIMA `(1, 1, 1)` model and compares its forecast with a drift baseline. It also explores log transformation, STL decomposition, and ADF stationarity tests.

## Run the notebooks

From the repository root, create a Python environment, install the libraries used by the notebooks, and launch Jupyter:

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
python -m pip install jupyter pandas numpy matplotlib statsmodels scikit-learn
jupyter notebook
```

Open either notebook and run its cells from top to bottom. No external credentials are required. The repository does not currently pin dependency versions, so results may vary across environments.

## Limitations and next steps

These are exploratory, notebook-based analyses of historical univariate data. The models do not incorporate potential explanatory factors such as exchange rates, interest rates, or energy prices, and the evaluation results depend on the chosen data and validation period. Possible extensions include testing alternative forecasting specifications, documenting the data period and index definitions more fully, and comparing against additional baselines.
