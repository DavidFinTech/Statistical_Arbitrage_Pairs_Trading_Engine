# Statistical Arbitrage & Pairs Trading Engine
![Python](https://img.shields.io/badge/python-3.8+-blue.svg)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=flat&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=flat&logo=numpy&logoColor=white)
![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=flat&logo=jupyter&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=flat&logo=Matplotlib&logoColor=black)
![Statsmodels](https://img.shields.io/badge/statsmodels-lightgrey.svg)
![yfinance](https://img.shields.io/badge/yfinance-lightgrey.svg)

An algorithmic trading engine built in Python that identifies and exploits mean-reverting relationships between cointegrated equity pairs. This project specifically analyzes the historical relationship between the Fidelity MSCI Energy Index ETF(FENY) and the Vanguard Energy ETF (VDE) to generate actionable trading signals.

### Project Overview

This engine automates the core quantitative research and backtesting pipeline for statistical arbitrage. It ingests historical market data, tests for statistical cointegration, estimates a fixed training-period hedge ratio, and simulates a complete trading strategy using rolling Z-scores to trigger long and short positions. 

### Key Features

*   **Data Ingestion:** Automated retrieval of historical adjusted close prices using `yfinance`.
*   **Statistical Cointegration:** Utilizes `statsmodels` to perform Augmented Dickey-Fuller (ADF) tests (via `coint`) to verify long-term mean-reverting relationships between asset pairs.
*   **Fixed Hedge Ratio with dynamic Z Score signals:** Calculates the beta between assets using Ordinary Least Squares (OLS) regression to construct a stationary spread.
*   **Signal Generation:** Uses a 20-day rolling Z-score to generate short-spread (−1), flat (0), and long-spread (+1) positions.*   
*   **Strategy Backtesting:** Uses separate training/testing periods and delays positions by one trading day. Results exclude trading and borrowing costs.
*   **Performance Visualization:** Generates comprehensive Matplotlib visualizations comparing the portfolio equity curve directly against the Z-score signal tripwires.

### Tech Stack

*   **Language:** Python
*   **Data Manipulation:** Pandas, NumPy
*   **Quantitative Modeling:** Statsmodels
*   **Data Visualization:** Matplotlib
*   **Financial Data API:** yfinance

### Methodology & Limitations

- **Training (2021–2023):** Tested six ETF pairs using a Bonferroni-adjusted significance threshold of 0.05/6. Selected FENY–VDE and estimated a fixed OLS hedge ratio.
- **Testing (2024–2025):** Applied that hedge ratio with 20-day rolling Z-score signals. Positions are delayed by one trading day.
- **Execution:** Uses closing prices as an approximation. Execution at the signal-generating close is not guaranteed.
- **Position sizing:** Compounded returns assume daily resizing so gross exposure equals account equity while invested.
- **Costs:** Excludes commissions, bid–ask spreads, slippage, borrowing fees, and financing costs.
- **Scope:** This is a historical research backtest, not evidence of future profitability.

### Installation & Usage

1. Clone the repository:

   ```bash
   git clone https://github.com/DavidFinTech/Statistical_Arbitrage_Pairs_Trading_Engine.git
   cd Statistical_Arbitrage_Pairs_Trading_Engine
   ```

2. Create and activate a virtual environment:

   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

   On Windows, activate it with `.venv\Scripts\activate`.

3. Install the dependencies:

   ```bash
   python -m pip install -r requirements.txt
   ```

4. Launch Jupyter:

   ```bash
   python -m notebook
   ```