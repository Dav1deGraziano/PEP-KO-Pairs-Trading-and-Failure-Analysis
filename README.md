# From Cointegration to Out-of-Sample Failure: A Pairs-Trading Case Study on PEP/KO

A case study of a cointegration-based pairs trading strategy on PepsiCo (PEP) and The Coca-Cola Company (KO), including policy optimisation, robustness testing, and out-of-sample failure analysis.

**Headline finding:** PEP and KO were significantly cointegrated over 2013–2018, and a threshold-based mean-reversion strategy calibrated on that relationship performed well in-sample (2018–2023). However, performance is concentrated almost entirely in the COVID-19 volatility shock, and a Deflated Sharpe Ratio of 0.423 shows that the in-sample edge does not have meaningful statistical evidence. Consistent with this, the strategy fails out-of-sample (2023–present) as the hedge ratio drifts and flips sign. *The evidence for an exploitable edge is weak.*

## Repository Contents

| File | Description |
|---|---|
| 📓 `Notebook.ipynb` | Jupyter notebook: data retrieval, statistical tests, strategy modelling and optimisation, backtesting, robustness checks, and OOS evaluation, with inline derivations and commentary. |
| 📄 `Reoprt.pdf` | Written report presenting the same analysis in academic paper format, with derivations, tables, and figures. |
| 📑 `Extended Report.pdf` | Compiled narrative-only rendering of the notebook (markdown/commentary and outputs; code cells omitted). |
| ⚖️ `MIT License (code)` | MIT License, covering the notebook's code. |
| ⚖️ `CC BY 4.0 License (content)` | CC BY 4.0 License, covering both PDF reports. |

## Analysis Stages

1. **Statistical analysis (2013–2018).** Test the log-price series for unit roots (Augmented Dickey–Fuller), test for cointegration (Engle–Granger), and characterise the resulting spread as a mean-reverting AR(1) process.
2. **Policy design and in-sample optimisation (2018–2023).** Translate the spread dynamics into a threshold-based entry/exit trading rule with explicit position sizing and transaction costs, and select the optimal thresholds by maximising the annualised net Sharpe ratio over a grid search.
3. **Robustness analysis.** Stress-test the selected policy via parameter sensitivity analysis, walk-forward validation across rolling folds, a COVID-19 exclusion check, and both the Adjusted Sharpe Ratio (non-normality) and Deflated Sharpe Ratio (selection bias).
4. **Out-of-sample test (2023–present).** Freeze every parameter from the earlier stages and evaluate the strategy on genuinely unseen data, including a diagnostic comparison of static vs. time-varying hedge ratios (rolling OLS and Kalman filter).

## Methodology Summary

- **Data:** Daily *adjusted* closing prices for PEP and KO, 2013–present, via `yfinance`.
- **Stationarity:** Augmented Dickey–Fuller test (AIC-selected lag order) on log-prices and log-returns.
- **Cointegration:** Engle–Granger two-step procedure with adjusted critical values; spread modelled as AR(1) to obtain equilibrium level, mean-reversion speed, and half-life.
- **Trading policy:** Entry/exit thresholds on the standardised spread z-score, volatility-based position sizing with a risk budget and exposure cap, and round-trip transaction costs deducted directly from equity.
- **Optimisation objective:** Annualised net Sharpe ratio, maximised over a threshold grid (901 candidate policies).
- **Robustness tools:** Parameter sensitivity grids (cost, risk budget, volatility window, max exposure), 3-fold walk-forward validation, COVID-window exclusion, Adjusted Sharpe Ratio, Deflated Sharpe Ratio.
- **Out-of-sample test:** All statistical and policy parameters frozen from earlier stages; evaluated on 2023–present data with both a static and a time-varying (rolling OLS, Kalman filter) hedge ratio.

## Requirements

```
numpy
pandas
yfinance
matplotlib
statsmodels
scipy
```

## License

This repository uses a split license:

- **Code** (`Notebook.ipynb`) is licensed under the [MIT License](MIT%20License%20(code)).
- **Written content** (`Report.pdf` and `Extended Report.pdf`) is licensed under [CC BY 4.0 License](CC%20BY%204.0%20License%20(content)). Reuse and adaptation are permitted with attribution.

## Author

D. Graziano
