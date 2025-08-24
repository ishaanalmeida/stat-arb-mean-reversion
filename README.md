# stat-arb-mean-reversion
Statistical Arbitrage Strategy Using Mean Reversion and Cointegration Tests

# Market-Neutral Pairs Trading: Visa (V) vs Mastercard (MA)

> Mean-reversion strategy on the **V–MA** pair with robust walk-forward validation, volatility targeting, and risk/stress analysis.  
> **Walk-forward OOS** (fixed thresholds, disjoint quarters): **Sharpe ≈ 0.57**.  
> **Vol-targeted variant** (10% ann target): **Sharpe ≈ 0.75**.

---

## 🔎 TL;DR
- **Pair:** Visa (V) & Mastercard (MA)  
- **Signal:** log-spread *z-score* with cross-entry and exit band  
- **Backtest:** next-bar execution, **5 bps/leg** costs, ADF gating, min-trades rule  
- **Walk-forward:** train ≈ 2y, test ≈ 3m (disjoint), β re-fit each train window  
- **Best variant:** vol-targeted (10% ann, 60-day vol, leverage cap 2×) → **Sharpe ~0.75**, **MaxDD ~−10.6%**  
- **Diversification:** near-zero to negative market beta in 2024; very low factor R²

---

## 📦 Repo structure
.
├── README.md
├── requirements.txt
├── .gitignore
├── .gitattributes                 # (optional) if using Git LFS for *.png, *.csv
├── stat_arb.ipynb                 # final end-to-end notebook
│
├── artifacts_step5/               # walk-forward & vol-targeted outputs
│   ├── wf_tuned_oos_daily_returns.csv
│   ├── wf_fixed_oos_daily_returns.csv
│   ├── wf_tuned_params.csv
│   ├── vol_targeted_daily_returns.csv
│   ├── wf_tuned_oos_equity.png
│   ├── wf_fixed_oos_equity.png
│   └── vol_targeted_equity.png
│
├── artifacts_step6/               # evaluation plots & summary
│   ├── step6_summary_metrics.csv
│   ├── equity_all.png
│   ├── drawdowns_all.png
│   ├── rolling_sharpe.png
│   ├── monthly_heatmap.png
│   ├── Baseline_const_beta_returns.csv
│   ├── WF_Tuned_quarterly_returns.csv
│   ├── WF_Fixed_Params_returns.csv
│   ├── Vol_targeted_10pct_returns.csv
│   └── Portfolio_gated_voltargeted_returns.csv
│
└── artifacts_step7/               # risk/stress & exposures
    ├── subperiod_metrics.csv
    ├── rolling_beta_spy.csv
    ├── static_multifactor_coefs.csv
    ├── rolling_multifactor_coefs.csv
    ├── regime_trend_table.csv        # (optional, if saved)
    └── vix_quartile_table.csv        # (optional, if saved)
---

## 🧠 What this project does

- Builds a **log-price spread** of Visa and Mastercard via OLS hedge ratio (β), validates **cointegration** (Engle–Granger ADF + Johansen).  
- Trades a **z-score mean-reversion** signal with **cross-entry** and an **exit band**; realistic **transaction costs** modeled (5 bps per leg on regime changes).  
- Performs **walk-forward** validation (train ~2 years → test ~3 months, disjoint), re-estimating β each train window, with **ADF gating** and a **minimum trades** constraint to avoid degenerate fits.  
- Implements a **volatility-targeted** variant (target 10% annualized, 60-day vol, leverage cap 2×).  
- Extends to a small **multi-pair portfolio** gated by stationarity and half-life.  
- Evaluates performance (equity, drawdowns, rolling Sharpe), **sub-periods & regimes** (SPY 200-day, VIX quartiles), and **factor exposures** (SPY/QQQ/IWM/MTUM/VLUE/USMV/HYG/IEF).

---

## ✅ Why the project is useful

- Showcases an **end-to-end quant workflow**: hypothesis → stationarity tests → signal design → robust OOS validation → risk/factor analysis.  
- Demonstrates **overfitting control** (disjoint walk-forward, ADF gate, parameter-grid robustness).  
- Produces a **diversifying return stream** (low/negative market beta late-sample) and documents where the strategy performs best (sideways/high-vol regimes).  
- Fully **reproducible** with standard Python libraries and Yahoo Finance data.

---

## 🚀 How to get started

### 1) Setup

```bash
git clone https://github.com/ishaanalmeida/stat-arb-mean-reversion.git
cd stat-arb-mean-reversion

python -m venv .venv
# Windows: .venv\Scripts\activate
source .venv/bin/activate

pip install -r requirements.txt
