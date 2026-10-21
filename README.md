# Statistical Arbitrage: Pairs Trading Research

A reproducible research notebook investigating whether economically related US banking stocks exhibit an out-of-sample mean-reversion trading signal after transaction costs and risk controls.

> **Research status:** Exploratory. None of the ten candidate pairs passed the conventional 5% Engle–Granger cointegration threshold in the training period. The backtest is **not** evidence of a validated cointegrated strategy or live-trading profitability.

## Research design

- **Universe:** JPM, BAC, C, GS, MS (daily adjusted prices, 2018–2025)
- **Training (2018–2021):** Screen ten pairs with the Engle–Granger cointegration test; select the lowest training p-value.
- **Validation (2022–2023):** Select lookback and entry threshold using validation-period net Sharpe.
- **Test (2024–2025):** Evaluate the frozen configuration once on an out-of-sample period.
- **Signals:** Rolling hedge ratio, spread and Z-score; position targets formed using information available at date *t* and applied to the next close-to-close return interval.
- **Risk and costs:** Entry/exit thresholds, Z-score stop, maximum holding period, daily rebalancing and turnover-based transaction costs.

## Key findings

The training screen selected **GS (Y) / BAC (X)**, with a cointegration p-value of **0.2014**. This does **not** meet the 5% significance threshold.

The validation-selected configuration used a 120-day lookback, 2.5 entry Z-score, 0.5 exit threshold, 4.0 Z-score stop, 20-day maximum holding period and 5 bps turnover cost.

| Out-of-sample metric (2024–2025) | Net result |
| --------------------------------- | ---------: |
| Annualized return                 |      5.52% |
| Annualized volatility             |      4.01% |
| Sharpe ratio                      |       1.36 |
| Maximum drawdown                  |     -2.17% |
| Trade entries                     |          7 |

These are historical simulated results from one test window with a small number of trades, not forecasts. Figures may vary with data vendor, run date and settings.

## Repository contents

- `pairs_trading_research.ipynb` — Python research notebook (rename your original `.ipynb` file to this name, or update this README to match its actual name).
- `requirements.txt` — Python dependencies.
- `reports/` — Optional PDF export of the notebook.
- `figures/` — Optional charts exported by the notebook.

## How to run

1. Clone or download this repository.
2. Create a Python environment and install dependencies:

   ```bash
   python -m pip install -r requirements.txt
   ```
3. Open `pairs_trading_research.ipynb` in VS Code with the Jupyter extension and run cells from top to bottom.
4. The notebook downloads data using `yfinance` (internet access required) and writes CSV tables and figures to `pairs_trading_outputs/`.

## Limitations

- The selected pair is **not statistically validated as cointegrated** at the 5% level; screening ten pairs also introduces multiple-testing risk.
- Adjusted closing prices are not executable quotes. The simulation does not fully model bid–ask spreads, short borrow fees, financing, slippage, market impact, overnight gaps or realistic order fills.
- The test period is short and has few entries; performance estimates may be fragile.
- Sensitivity checks on the test period are diagnostic, **not** a second round of parameter optimization.

## Possible extensions

Investigate walk-forward pair reselection, bootstrap confidence intervals, cointegration stability, alternative price vendors, benchmark comparisons and more realistic execution/borrow models.

## Data and tools

Data: Yahoo Finance via `yfinance` (subject to provider availability and terms).
Tools: Python, pandas, NumPy, SciPy, statsmodels, Matplotlib and yfinance.

**Disclaimer:** For educational and research purposes only; not investment advice.
