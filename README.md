# Fama–French Factor Exposure & Alpha Attribution Analysis

## Overview

This project analyzes the systematic drivers of stock returns using the Fama–French five-factor model extended with the Momentum factor.

The analysis uses Apple Inc. (AAPL) as a case study and estimates its exposure to:

- Market risk
- Size (SMB)
- Value (HML)
- Profitability (RMW)
- Investment (CMA)
- Momentum (MOM)

The project combines financial data analysis, econometric regression, statistical inference, rolling factor exposures, multicollinearity diagnostics, and factor-based return attribution.

---

## Research Question

How much of a stock's historical return can be explained by systematic factor exposures, and how much remains unexplained by the six-factor model?

The analysis focuses on three key questions:

1. What are AAPL's exposures to the major systematic risk factors?
2. Are these factor exposures statistically significant?
3. Does the factor model explain AAPL's historical excess returns, or is there evidence of alpha?

---

## Methodology

The project follows a standard quantitative asset-pricing workflow:

1. Obtain historical AAPL price data.
2. Calculate daily stock returns.
3. Obtain Fama–French factor data.
4. Align stock returns with factor observations.
5. Calculate AAPL's excess returns over the risk-free rate.
6. Estimate a six-factor regression.
7. Apply HAC/Newey–West standard errors for statistical inference.
8. Calculate rolling 252-day factor exposures.
9. Measure multicollinearity using Variance Inflation Factors (VIF).
10. Attribute returns to individual systematic factors.
11. Evaluate historical performance using standard risk-adjusted metrics.

---

## Factor Model

The model estimates AAPL's excess return using six systematic factors:

- Market Risk Premium (MKT)
- Size (SMB)
- Value (HML)
- Profitability (RMW)
- Investment (CMA)
- Momentum (MOM)

The regression can be expressed conceptually as:

**Excess Stock Return = Alpha + Market Exposure + Size Exposure + Value Exposure + Profitability Exposure + Investment Exposure + Momentum Exposure + Error**

The estimated coefficients represent the stock's sensitivity to each factor.

---

## Data

### Stock Data

- Security: Apple Inc. (AAPL)
- Frequency: Daily
- Analysis period: January 2021 to June 2026
- Observations: Approximately 1,377 daily observations

### Factor Data

The project uses Fama–French factor data together with the Momentum factor.

The risk-free rate is used to convert raw stock returns into excess returns before regression analysis.

---

## Key Results

### AAPL Performance

| Metric | Result |
|---|---:|
| CAGR | 16.48% |
| Annualized Volatility | 27.69% |
| Sharpe Ratio | 0.570 |
| Maximum Drawdown | -33.36% |

These statistics show that AAPL generated strong historical returns over the sample period while also experiencing substantial volatility and drawdowns.

### Estimated Factor Exposures

| Factor | Estimated Exposure |
|---|---:|
| Market | 1.2121 |
| Value (HML) | -0.4760 |
| Profitability (RMW) | 0.4737 |
| Investment (CMA) | 0.4281 |

The estimated market beta above 1 indicates that AAPL historically exhibited greater sensitivity to market movements than the market portfolio.

The negative Value exposure is consistent with a stronger growth-oriented profile relative to value stocks during the sample period.

The positive Profitability and Investment exposures indicate additional systematic characteristics captured by the five-factor framework.

---

## Statistical Inference

The project uses HAC/Newey–West standard errors to account for potential heteroskedasticity and autocorrelation in regression residuals.

For each factor, the analysis considers:

- Estimated coefficient
- Standard error
- t-statistic
- p-value
- Statistical significance

This provides a more robust assessment of whether observed factor exposures are distinguishable from sampling noise.

---

## Rolling Factor Exposure

Static regression coefficients provide an average exposure over the entire sample.

To examine whether AAPL's characteristics changed over time, the project also performs rolling 252-trading-day regressions.

This allows factor exposures to be analyzed dynamically and helps identify periods in which:

- Market sensitivity changed
- Growth/value characteristics shifted
- Profitability exposure changed
- Investment exposure changed
- Momentum exposure changed

---

## Multicollinearity Analysis

The project calculates Variance Inflation Factors (VIF) to assess potential multicollinearity among explanatory variables.

This is important because highly correlated factors can make individual coefficient estimates less stable and harder to interpret.

VIF diagnostics are therefore included as part of the regression validation process.

---

## Factor Attribution

The project decomposes estimated returns into contributions associated with the different systematic factors.

This helps distinguish between:

- Market-driven performance
- Style/factor-driven performance
- Stock-specific performance represented by the model intercept and residual component

Factor attribution is treated as a statistical decomposition rather than a claim of causal return generation.

---

## Visualizations

The project generates visualizations covering areas such as:

- Cumulative performance
- Factor exposures
- Rolling factor betas
- Factor contribution
- Drawdowns
- Regression diagnostics

These charts are available in the `charts/` directory.

---

## Project Structure

```text
fama-french-factor-analysis/
│
├── Fama_French_Factor_Exposure_Analysis.ipynb
├── README.md
├── requirements.txt
├── LICENSE
├── .gitignore
│
├── charts/
│   └── Generated analysis charts
│
└── outputs/
    └── Regression and analysis outputs
