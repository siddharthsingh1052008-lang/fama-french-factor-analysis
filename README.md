# Fama–French Factor Exposure & Alpha Attribution Engine

A Python-based quantitative research project that decomposes stock returns into systematic factor exposures and evaluates whether factor-adjusted alpha remains after controlling for market, size, value, profitability, investment, and momentum factors.

---

## Overview

This project implements a **Fama–French 5-factor + Momentum** asset-pricing model using daily financial data.

The pipeline estimates:

* Market exposure
* Size exposure
* Value exposure
* Profitability exposure
* Investment exposure
* Momentum exposure
* Factor-adjusted alpha

It also includes:

* HAC/Newey–West robust inference
* 252-day rolling factor exposures
* VIF multicollinearity diagnostics
* Factor-return attribution
* Performance metrics
* Automated visualizations
* Exportable research outputs

### Research question

> **How much of AAPL's historical performance can be explained by systematic factor exposure, and is there evidence of persistent alpha after controlling for those factors?**

---

# Model

The project estimates the following six-factor time-series model:

```text
R(i,t) - R(f,t)
    = alpha
    + beta_M * (MKT-RF)
    + beta_S * SMB
    + beta_H * HML
    + beta_R * RMW
    + beta_C * CMA
    + beta_MOM * MOM
    + epsilon(t)
```

Where:

| Factor   | Description               |
| -------- | ------------------------- |
| `MKT-RF` | Market excess return      |
| `SMB`    | Size factor               |
| `HML`    | Value factor              |
| `RMW`    | Profitability factor      |
| `CMA`    | Investment factor         |
| `MOM`    | Momentum factor           |
| `RF`     | Risk-free rate            |
| `Alpha`  | Factor-adjusted intercept |

---

# Data Sources

## Kenneth R. French Data Library

Daily:

* Fama–French 5 Factors
* Momentum Factor

## Yahoo Finance

Daily adjusted historical prices for the target security.

For the completed AAPL analysis, the common sample was:

```text
January 5, 2021 → June 30, 2026
```

with:

```text
1,377 usable daily observations
```

The model automatically uses the overlapping period between the stock-price data and the factor data.

---

# Technology Stack

```text
Python
Pandas
NumPy
Statsmodels
Matplotlib
yfinance
Requests
```

---

# System Architecture

```text
Kenneth French Data Library
        |
        +-- Fama–French 5 Factors
        |
        +-- Momentum
        |
        v
   Factor Data Pipeline
        |
        |
Yahoo Finance
        |
        v
 Adjusted Prices
        |
        v
 Daily Returns
        |
        v
 Excess Returns
        |
        v
 Six-Factor OLS
        |
        +-- HAC / Newey-West Inference
        +-- Factor Betas
        +-- Alpha
        +-- t-statistics
        +-- p-values
        |
        +--------------------+
        |                    |
        v                    v
   Rolling OLS          VIF Diagnostics
        |
        v
 Factor Exposure Drift
        |
        v
 Factor Attribution
        |
        v
 Charts + Research Outputs
```

---

# Methodology

The analysis pipeline follows these steps:

1. Download daily Fama–French 5-factor data.
2. Download daily momentum data.
3. Download AAPL adjusted historical prices.
4. Calculate daily stock returns.
5. Align stock returns with factor observations.
6. Construct daily excess returns.
7. Estimate the six-factor OLS regression.
8. Apply HAC/Newey–West robust standard errors.
9. Calculate VIF multicollinearity diagnostics.
10. Estimate 252-day rolling factor exposures.
11. Calculate factor-return attribution.
12. Calculate investment performance metrics.
13. Generate research visualizations.
14. Export research outputs.

---

# Results — AAPL

## Performance

| Metric                |      Result |
| --------------------- | ----------: |
| CAGR                  |  **16.48%** |
| Annualized Volatility |  **27.69%** |
| Sharpe Ratio          |   **0.570** |
| Maximum Drawdown      | **-33.36%** |
| Observations          |   **1,377** |

---

## Factor Exposures

| Factor                |        Beta | t-stat | p-value |
| --------------------- | ----------: | -----: | ------: |
| Market (`MKT-RF`)     |  **1.2121** |  29.22 |  <0.001 |
| Size (`SMB`)          | **-0.1086** |  -2.11 |  0.0348 |
| Value (`HML`)         | **-0.4760** |  -6.58 |  <0.001 |
| Profitability (`RMW`) |  **0.4737** |   7.61 |  <0.001 |
| Investment (`CMA`)    |  **0.4281** |   3.86 |  0.0001 |
| Momentum (`MOM`)      | **-0.0941** |  -2.76 |  0.0059 |

### Interpretation

The estimated model indicates that AAPL historically exhibited:

* Strong positive market exposure
* Slight negative size exposure
* Strong negative value exposure
* Positive profitability exposure
* Positive investment exposure
* Slight negative momentum exposure

All six factor coefficients were statistically significant at the 5% level in this sample.

---

# Alpha Analysis

Estimated annualized alpha:

```text
4.62%
```

However:

```text
Alpha t-stat = 0.590
Alpha p-value = 0.555
```

Therefore, the estimated alpha is **not statistically significant**.

The analysis does not provide strong statistical evidence that AAPL generated persistent abnormal returns after controlling for the six systematic factors.

This highlights an important distinction in quantitative investing:

> **Strong historical returns do not automatically imply persistent alpha.**

---

# Model Fit

```text
R-squared          = 59.61%
Adjusted R-squared = 59.43%
```

Approximately 59.6% of the variation in AAPL's daily excess returns is explained by the six-factor model over the analyzed sample.

---

# Factor Attribution

Annualized mean excess-return attribution:

| Component     | Contribution |
| ------------- | -----------: |
| Market        |  **+14.06%** |
| Alpha         |   **+4.62%** |
| Size          |   **+0.29%** |
| Value         |   **-4.07%** |
| Profitability |   **+0.86%** |
| Investment    |   **+0.85%** |
| Momentum      |   **-0.82%** |
| Residual      |   **~0.00%** |

The market factor was the largest positive contributor, while the negative value exposure was the largest offsetting contribution.

---

# Multicollinearity Diagnostics

| Factor        |   VIF |
| ------------- | ----: |
| Market        | 1.322 |
| Size          | 1.497 |
| Value         | 1.998 |
| Profitability | 1.599 |
| Investment    | 1.709 |
| Momentum      | 1.112 |

The relatively low VIF values indicate that severe multicollinearity is not a major issue for this factor specification over the analyzed sample.

---

# Rolling Factor Exposure

A **252-trading-day rolling regression** is used to measure how AAPL's systematic factor exposures evolve through time.

The project generates rolling exposure series for:

* Market
* Size
* Value
* Profitability
* Investment
* Momentum

This allows factor exposure drift to be analyzed instead of assuming that AAPL's factor profile remained constant throughout the entire sample.

---

# Visualizations

## Rolling Factor Exposure

Tracks changes in each estimated factor beta through time.

![Rolling Market Beta](charts/rolling_market_beta.png)

## Alpha Significance

Shows annualized alpha together with its 95% HAC confidence interval.

![Alpha Significance](charts/alpha_significance.png)

## Factor Attribution

Shows the annualized contribution of alpha and each systematic factor.

![Factor Attribution](charts/factor_attribution.png)

## Realized vs Factor Model

Compares cumulative realized excess returns with cumulative factor-model-implied returns.

![Realized vs Factor Model](charts/realized_vs_factor_model.png)

Additional rolling-exposure charts are available in the [`charts`](charts/) directory.

---

# Repository Structure

```text
fama-french-factor-analysis/
|
├── README.md
├── LICENSE
├── .gitignore
├── requirements.txt
├── Fama_French_Factor_Exposure_Analysis.ipynb
|
├── charts/
│   ├── alpha_significance.png
│   ├── factor_attribution.png
│   ├── realized_vs_factor_model.png
│   ├── rolling_investment_beta.png
│   ├── rolling_market_beta.png
│   ├── rolling_momentum_beta.png
│   ├── rolling_profitability_beta.png
│   ├── rolling_size_beta.png
│   └── rolling_value_beta.png
|
└── outputs/
    ├── factor_attribution.csv
    ├── model_dataset.csv
    ├── ols_summary.txt
    ├── performance_metrics.csv
    ├── regression_statistics.csv
    ├── rolling_exposures.csv
    └── vif_diagnostics.csv
```

---

# Engineering Features

## Robust Data Ingestion

The pipeline dynamically parses the daily factor files from the Kenneth French Data Library and validates the resulting factor columns before modeling.

## Data Alignment

Stock returns and factor returns are aligned by trading date before the regression dataset is constructed.

## HAC Inference

HAC/Newey–West standard errors are used for statistical inference that is more robust to heteroskedasticity and autocorrelation.

## Rolling Estimation

A 252-day rolling regression estimates how factor exposures evolve through time.

## Multicollinearity Diagnostics

Variance Inflation Factors are calculated for every factor.

## Automated Research Outputs

The pipeline exports:

* Regression statistics
* Rolling exposures
* VIF diagnostics
* Factor attribution
* Performance metrics
* Full OLS summary

---

# Limitations

This analysis is intended for quantitative research and educational purposes.

Important limitations include:

* Results depend on the selected factor model.
* Historical factor exposure does not guarantee future exposure.
* Alpha significance is sample-dependent.
* Factor attribution is based on average return contributions rather than a full trade-level P&L decomposition.
* Rolling coefficients may become unstable during unusual market conditions.
* The analysis is in-sample and does not constitute an out-of-sample forecasting test.
* The regression does not establish causal relationships.

---

# Potential Extensions

## Multi-Stock Analysis

Extend the model to compare:

```text
AAPL
MSFT
NVDA
AMZN
META
GOOGL
```

and compare their factor fingerprints.

## Portfolio Analysis

Allow arbitrary portfolio weights and estimate portfolio-level factor exposure.

## Expanded Factor Models

Potential additions:

* Quality
* Low volatility
* Liquidity
* Short-term reversal
* Additional momentum specifications

## Advanced Statistical Analysis

Potential additions:

* Bootstrap confidence intervals
* Structural-break tests
* Regime analysis
* Expanding-window estimation
* Out-of-sample testing
* Rolling alpha confidence intervals

## Portfolio Construction

Use estimated factor exposures as inputs to a constrained portfolio optimization framework.

---

# Resume Description

**Fama–French Factor Exposure & Alpha Attribution Engine | Python, Pandas, Statsmodels**

Developed a six-factor quantitative asset-pricing pipeline using daily Fama–French 5-factor and momentum data; implemented HAC-robust OLS, 252-day rolling factor exposures, VIF multicollinearity diagnostics and factor attribution; analyzed AAPL over 2021–2026, obtaining 59.6% model R² and estimating 4.6% annualized alpha that was statistically insignificant.

---

# Key Takeaway

The analysis demonstrates how observed stock performance can be decomposed into systematic market and style-factor exposures rather than being automatically attributed to investment skill.

For AAPL, the model finds strong market exposure and meaningful style-factor exposures, while the estimated positive alpha is not statistically significant.

The project demonstrates the practical distinction between:

**Return ≠ Alpha**

and shows how quantitative factor models can be used to evaluate the sources of investment performance.
