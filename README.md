# Time Series and Demand Forecasting

Time series analysis and demand forecasting on daily WTI oil price data, covering trend and seasonality detection, decomposition, and short-horizon demand forecasting with several classical methods.

## Overview

This repository contains a single Jupyter notebook, `forecasting.ipynb`, that walks through a full time series analysis workflow on the [Daily Oil Price dataset](https://www.kaggle.com/c/store-sales-time-series-forecasting/data?select=oil.csv). 

It covers:
- **Data exploration** — plotting the full series and zooming into shorter windows to inspect structure.
- **Trend extraction**
  - Semi-average method
  - Moving average (`rolling`, with and without `min_periods`)
  - Simple linear regression (both a from-scratch implementation and scikit-learn's `LinearRegression`)
  - Exponential smoothing at several values of alpha (0.5, 0.05, 0.001)
- **Seasonality analysis** — monthly means and seasonal index computation.
- **Time series decomposition** — additive, multiplicative, and STL (Seasonal-Trend decomposition using LOESS).
- **Demand forecasting** — holding out the last two weeks of data as a test set and comparing forecasts from:
  - Moving average (window = 5)
  - Linear regression (full training set and a shorter recent window)
  - STL + ARIMA
  - STL + Exponential Smoothing

  Forecast accuracy is evaluated using Mean Squared Error (MSE) against the held-out test values.

## Repository contents

```
forecasting/
├── forecasting.ipynb   # Main analysis notebook
├── oil.csv             # Daily WTI oil price data (not included — see Data below)
└── README.md
```

## Data

The notebook expects a file named `oil.csv` in the working directory, with two columns:

- `date` — daily date (`YYYY-MM-DD`)
- `dcoilwtico` — WTI crude oil price for that date

`oil.csv` is one of the supplementary files from Kaggle's [Store Sales - Time Series Forecasting](https://www.kaggle.com/c/store-sales-time-series-forecasting/data?select=oil.csv) competition. Missing values are handled via `na_values = ['na', '-', '.', '']` on read and dropped where needed for modeling. 

## Requirements

- Python 3
- `numpy`
- `pandas`
- `matplotlib`
- `scikit-learn`
- `statsmodels`

Install everything with:

```bash
pip install numpy pandas matplotlib scikit-learn statsmodels
```

## Usage

1. Clone the repo and place `oil.csv` in the root directory.
2. Launch Jupyter and open the notebook:

   ```bash
   jupyter notebook forecasting.ipynb
   ```

3. Run the cells in order. The notebook is organized into clearly labeled sections (data exploration, trend, seasonality, decomposition, forecasting) that can be run top to bottom.

## Results

The forecasting section prints MSE values for each method (moving average, linear regression, ARIMA via STL, and exponential smoothing via STL) on the two-week held-out test set, allowing direct comparison of forecast accuracy across methods.
