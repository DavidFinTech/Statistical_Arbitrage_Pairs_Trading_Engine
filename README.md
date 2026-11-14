# Energy ETF Pairs Trading

I tested six pairs of energy ETFs to see whether any had a spread I could use for a mean-reversion strategy. I picked FENY–VDE using 2021–2023 data, then backtested it on 2024–2025 data. The strategy returned **about 0.8% before trading and borrowing costs**.

## How I ran the backtest

1. I pulled adjusted closing prices with `yfinance` and tested the six pairs for cointegration using `statsmodels`. I used a Bonferroni-adjusted cutoff of 0.05/6 because I was testing multiple pairs.
2. I estimated the FENY–VDE hedge ratio with OLS on the training period and kept it fixed for the backtest.
3. I used a 20-day rolling Z-score of the spread to decide when to go long, go short, or stay flat. I shifted positions by one trading day so the signal took effect the next day.

The notebook plots the strategy's equity curve and the Z-score signals. It also reports the Sharpe ratio, the maximum drawdown, how many times the position changed, and how the return holds up at trading costs from 1 to 10 basis points per trade.

## Backtest assumptions

The backtest uses closing prices as an approximation and resizes positions daily so gross exposure equals account equity while invested. The headline return excludes commissions, bid–ask spreads, slippage, borrowing fees, and financing costs. The cost table at the end of the notebook adds a flat cost per trade, but borrowing fees for the short leg are still left out.

## Run the notebook

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
