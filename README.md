# stat-arb-mean-reversion
Statistical Arbitrage Strategy Using Mean Reversion and Cointegration Tests
# Market-Neutral Pairs Trading: Visa (V) vs Mastercard (MA)

> Mean-reversion strategy on the V–MA pair with robust walk-forward validation, volatility targeting, and risk/stress analysis.  
> **OOS Sharpe ≈ 0.57** (fixed thresholds, disjoint quarters). **Vol-targeted variant** achieves **Sharpe ≈ 0.75**.

---

## 🔎 TL;DR
- **Pair**: Visa (V) & Mastercard (MA)  
- **Signal**: log-spread z-score with cross-entry and exit band  
- **Backtest**: next-bar execution, **5 bps/leg** costs, ADF gating, min-trade rule  
- **Walk-forward**: train ≈2y, test ≈3m (disjoint), β re-fit per train  
- **Best variant**: vol-targeted 10% ann (60d vol, cap 2×) → **Sharpe ~0.75**, **MaxDD ~−10.6%**  
- **Diversification**: near-zero to negative market beta in 2024; low factor R²

---

## 📦 Repo structure
.
├── stat_arb.ipynb # final notebook (end-to-end)
├── artifacts_step5/ # walk-forward & vol-targeted outputs
│ ├── wf_tuned_oos_daily_returns.csv
│ ├── wf_fixed_oos_daily_returns.csv
│ ├── wf_tuned_params.csv
│ └── *_equity.png
├── artifacts_step6/ # evaluation plots & summary table
│ ├── step6_summary_metrics.csv
│ ├── equity_all.png
│ ├── drawdowns_all.png
│ ├── rolling_sharpe.png
│ └── monthly_heatmap.png
├── artifacts_step7/ # risk/stress & exposures
│ ├── subperiod_metrics.csv
│ ├── rolling_beta_spy.csv
│ ├── static_multifactor_coefs.csv
│ └── rolling_multifactor_coefs.csv
└── requirements.txt
