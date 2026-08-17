# Fama–French Factor Exposure & Alpha Attribution Engine

A Python-based quantitative research project that decomposes stock returns into systematic factor exposures and evaluates whether factor-adjusted alpha remains after controlling for market, size, value, profitability, investment, and momentum factors.

## Project Overview

This project implements a six-factor asset-pricing model using:

* Fama–French 5 factors
* Momentum factor
* Daily stock returns
* HAC/Newey–West robust inference
* 252-day rolling factor regressions
* VIF multicollinearity diagnostics
* Factor-return attribution
* Investment performance metrics

The analysis uses **Apple Inc. (AAPL)** as a case study, using daily data from **January 2021 through June 2026**.

## Research Question

> How much of AAPL's historical performance can be explained by systematic factor exposure, and is there evidence of persistent alpha after controlling for those factors?

## Factor Model

The project estimates AAPL's excess return using six systematic factors:

* **MKT-RF** — Market excess return
* **SMB** — Size factor
* **HML** — Value factor
* **RMW** — Profitability factor
* **CMA** — Investment factor
* **MOM** — Momentum factor

The model can be represented conceptually as:

```text
Excess Stock Return
        =
Alpha
+ Market Exposure
+ Size Exposure
+ Value Exposure
+ Profitability Exposure
+ Investment Exposure
+ Momentum Exposure
+ Error
```

The regression coefficients represent AAPL's sensitivity to each systematic factor.

## Data Sources

### Kenneth R. French Data Library

Daily factor data for:

* Fama–French 5 Factors
* Momentum Factor

### Yahoo Finance

Daily adjusted historical prices for AAPL.

### Final Sample

The analysis uses the overlapping period between the stock and factor datasets:

**January 5, 2021 – June 30, 2026**

with **1,377 usable daily observations**.

## Methodology

The analysis pipeline follows these steps:

1. Download Fama–French 5-factor data.
2. Download the Momentum factor.
3. Download AAPL adjusted historical prices.
4. Calculate daily stock returns.
5. Align stock and factor observations.
6. Calculate daily excess returns.
7. Estimate the six-factor OLS regression.
8. Apply HAC/Newey–West robust standard errors.
9. Calculate factor multicollinearity using VIF.
10. Estimate 252-day rolling factor exposures.
11. Calculate factor-return attribution.
12. Calculate investment performance metrics.
13. Generate research visualizations.
14. Export research outputs.

## System Architecture

```text
Kenneth French Data Library
        |
        +-- Fama–French 5 Factors
        |
        +-- Momentum Factor
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
        +-- HAC / Newey–West Inference
        |
        +-- Factor Betas
        |
        +-- Alpha
        |
        +-- t-statistics
        |
        +-- p-values
        |
        +-------------------+
        |                   |
        v                   v
  Rolling OLS         VIF Diagnostics
        |                   |
        v                   |
  Exposure Drift           |
        |                   |
        +---------+---------+
                  |
                  v
          Factor Attribution
                  |
                  v
       Charts and Research Outputs
```

## Technology Stack

### Programming

* Python

### Data Analysis

* pandas
* NumPy

### Financial Data

* yfinance
* Kenneth R. French Data Library
* requests

### Statistical Analysis

* statsmodels
* Ordinary Least Squares (OLS)
* HAC/Newey–West standard errors
* Variance Inflation Factor (VIF)
* Rolling regression

### Visualization

* matplotlib
* seaborn

### Development Environment

* Jupyter Notebook

## Results

### Performance

| Metric                |      Result |
| --------------------- | ----------: |
| CAGR                  |  **16.48%** |
| Annualized Volatility |  **27.69%** |
| Sharpe Ratio          |   **0.570** |
| Maximum Drawdown      | **-33.36%** |
| Observations          |   **1,377** |

### Factor Exposures

| Factor              |        Beta | t-stat | p-value |
| ------------------- | ----------: | -----: | ------: |
| Market (MKT-RF)     |  **1.2121** |  29.22 |  <0.001 |
| Size (SMB)          | **-0.1086** |  -2.11 |  0.0348 |
| Value (HML)         | **-0.4760** |  -6.58 |  <0.001 |
| Profitability (RMW) |  **0.4737** |   7.61 |  <0.001 |
| Investment (CMA)    |  **0.4281** |   3.86 |  0.0001 |
| Momentum (MOM)      | **-0.0941** |  -2.76 |  0.0059 |

### Interpretation

The regression indicates that AAPL exhibited:

* Strong positive exposure to market risk.
* Slight negative exposure to the size factor.
* Strong negative exposure to the value factor, consistent with a growth-oriented factor profile.
* Positive exposure to profitability.
* Positive exposure to investment.
* Slight negative exposure to momentum.

The statistical results indicate that all six estimated factor exposures are statistically significant at conventional significance levels in the fitted model.

## Alpha Analysis

A key objective of the project is to determine whether AAPL generated returns beyond those explained by the six systematic factors.

The model estimates an annualized alpha of approximately:

**4.62%**

However, the estimated alpha has a **p-value of approximately 0.555**.

This means the estimated alpha is **not statistically significant at conventional significance levels**.

Therefore, the analysis does not provide strong statistical evidence that AAPL generated persistent abnormal returns beyond the systematic factors included in the model during the sample period.

This distinction is important: a positive estimated alpha does not automatically imply statistically significant alpha.

## Rolling Factor Exposure

A static regression provides average factor exposure over the full sample.

To examine whether AAPL's factor characteristics changed over time, the project performs **252-trading-day rolling regressions**.

This allows the analysis to identify changes in:

* Market sensitivity
* Size exposure
* Value/growth exposure
* Profitability exposure
* Investment exposure
* Momentum exposure

Rolling exposures provide a more dynamic view of the stock's factor characteristics than a single full-period regression.

## Multicollinearity Analysis

The project uses **Variance Inflation Factors (VIF)** to assess potential multicollinearity among the explanatory variables.

This is important because highly correlated factors can make individual coefficient estimates less stable and more difficult to interpret.

VIF diagnostics are therefore included as part of the regression validation process.

## Factor Attribution

The project decomposes estimated returns into contributions associated with the different systematic factors.

This provides a framework for distinguishing between:

* Market-driven performance
* Size-related performance
* Value/growth-related performance
* Profitability-related performance
* Investment-related performance
* Momentum-related performance
* Factor-adjusted residual performance

Factor attribution is treated as a statistical decomposition rather than a claim of causal return generation.

## Visualizations

The project generates visualizations covering areas such as:

* Cumulative performance
* Factor exposures
* Rolling factor betas
* Factor contribution
* Drawdowns
* Regression diagnostics

Generated charts are available in the `charts/` directory.

## Project Structure

```text
fama-french-factor-analysis/
|
+-- Fama_French_Factor_Exposure_Analysis.ipynb
+-- README.md
+-- requirements.txt
+-- LICENSE
+-- .gitignore
|
+-- charts/
|   +-- Generated analysis charts
|
+-- outputs/
    +-- Regression and analysis outputs
```

## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/siddharthsingh1052008-lang/fama-french-factor-analysis.git
cd fama-french-factor-analysis
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Launch Jupyter Notebook

```bash
jupyter notebook
```

### 4. Open the analysis notebook

Open:

```text
Fama_French_Factor_Exposure_Analysis.ipynb
```

Run the notebook cells sequentially to reproduce the analysis.

## Key Takeaways

This project demonstrates how a multi-factor asset-pricing framework can be used to move beyond simple historical return analysis.

The analysis of AAPL shows:

* Market exposure above 1, indicating greater sensitivity to broad market movements.
* Strong negative exposure to the Value factor.
* Positive exposure to Profitability and Investment factors.
* Statistically significant exposure estimates across the six-factor model.
* A positive estimated alpha that is not statistically significant.
* Factor exposures that can vary over time when examined through rolling regressions.

The results demonstrate why factor-based analysis can provide a more structured explanation of stock returns than standalone performance metrics.

## Limitations

This analysis has several limitations:

* The case study focuses on a single stock.
* Historical factor exposures do not guarantee future exposures.
* Factor definitions depend on the underlying factor datasets.
* The sample period may contain regime-specific market conditions.
* Regression-based attribution should not be interpreted as a causal decomposition of returns.
* Estimated alpha can be sensitive to model specification, sample period, and factor selection.

## Future Improvements

Potential extensions include:

* Expanding the analysis to multiple stocks.
* Comparing factor exposures across sectors.
* Building portfolio-level factor models.
* Adding out-of-sample testing.
* Comparing five-factor and six-factor model performance.
* Testing alternative sample periods.
* Developing factor-neutral portfolio strategies.
* Automating the analysis for a larger stock universe.
* Adding additional robustness tests.

## Skills Demonstrated

This project demonstrates practical experience with:

* Quantitative finance
* Factor investing
* Asset pricing
* Financial econometrics
* Linear regression
* Statistical inference
* Time-series analysis
* Risk analysis
* Portfolio analytics
* Python
* Data visualization
* Research methodology

## Disclaimer

This project is for educational and research purposes only.

The analysis does not constitute investment advice or a recommendation to buy or sell any security.

## License

This project is licensed under the MIT License.
