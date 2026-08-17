\# Fama–French Factor Exposure \& Alpha Attribution Engine



A Python-based quantitative research project that decomposes stock returns into systematic factor exposures and evaluates whether factor-adjusted alpha remains after controlling for market, size, value, profitability, investment, and momentum factors.



\## Project Overview



This project implements a six-factor asset-pricing model using:



\* Fama–French 5 factors

\* Momentum factor

\* Daily stock returns

\* HAC/Newey–West robust inference

\* 252-day rolling factor regressions

\* VIF multicollinearity diagnostics

\* Factor-return attribution

\* Investment performance metrics



The analysis was conducted on \*\*Apple Inc. (AAPL)\*\* using daily data from January 2021 through June 2026.



\## Research Question



> How much of AAPL's historical performance can be explained by systematic factor exposure, and is there evidence of persistent alpha after controlling for those factors?



\## Factor Model



The project estimates:



\[

R\_{i,t} - R\_{f,t}

=================



\\alpha

\+

\\beta\_M(MKT-RF)\*t

\+

\\beta\_S SMB\_t

\+

\\beta\_H HML\_t

\+

\\beta\_R RMW\_t

\+

\\beta\_C CMA\_t

\+

\\beta\*{MOM} MOM\_t

\+

\\epsilon\_t

]



Where:



| Factor | Description               |

| ------ | ------------------------- |

| MKT-RF | Market excess return      |

| SMB    | Size factor               |

| HML    | Value factor              |

| RMW    | Profitability factor      |

| CMA    | Investment factor         |

| MOM    | Momentum factor           |

| RF     | Risk-free rate            |

| Alpha  | Factor-adjusted intercept |



\## Data Sources



\### Kenneth R. French Data Library



Daily:



\* Fama–French 5 Factors

\* Momentum Factor



\### Yahoo Finance



Daily adjusted historical prices for AAPL.



The final model uses the overlapping period between Yahoo Finance and the available factor datasets:



\*\*January 5, 2021 – June 30, 2026\*\*



with \*\*1,377 usable daily observations\*\*.



\## Technology Stack



```text

Python

Pandas

NumPy

Statsmodels

Matplotlib

yfinance

Requests

```



\## Methodology



The analysis pipeline follows these steps:



1\. Download Fama–French 5-factor data.

2\. Download the momentum factor.

3\. Download AAPL adjusted historical prices.

4\. Calculate daily stock returns.

5\. Align stock and factor observations.

6\. Calculate daily excess returns.

7\. Estimate the six-factor OLS regression.

8\. Apply HAC/Newey–West robust standard errors.

9\. Calculate factor multicollinearity using VIF.

10\. Estimate 252-day rolling factor exposures.

11\. Calculate factor-return attribution.

12\. Calculate investment performance metrics.

13\. Generate research visualizations.

14\. Export research outputs.



\## System Architecture



```text

Kenneth French Data Library

&#x20;       │

&#x20;       ├── Fama–French 5 Factors

&#x20;       └── Momentum

&#x20;               │

&#x20;               ▼

&#x20;       Factor Data Pipeline

&#x20;               │

&#x20;               │

Yahoo Finance ──┘

&#x20;       │

&#x20;       ▼

Adjusted Prices

&#x20;       │

&#x20;       ▼

Daily Returns

&#x20;       │

&#x20;       ▼

Excess Returns

&#x20;       │

&#x20;       ▼

Six-Factor OLS

&#x20;       │

&#x20;       ├── HAC Inference

&#x20;       ├── Factor Betas

&#x20;       ├── Alpha

&#x20;       ├── t-statistics

&#x20;       └── p-values

&#x20;       │

&#x20;       ├───────────────┐

&#x20;       ▼               ▼

Rolling OLS          VIF Diagnostics

&#x20;       │

&#x20;       ▼

Exposure Drift

&#x20;       │

&#x20;       ▼

Factor Attribution

&#x20;       │

&#x20;       ▼

Charts + Research Outputs

```



\# Results



\## Performance



| Metric                |      Result |

| --------------------- | ----------: |

| CAGR                  |  \*\*16.48%\*\* |

| Annualized Volatility |  \*\*27.69%\*\* |

| Sharpe Ratio          |   \*\*0.570\*\* |

| Maximum Drawdown      | \*\*-33.36%\*\* |

| Observations          |   \*\*1,377\*\* |



\## Factor Exposures



| Factor              |        Beta | t-stat | p-value |

| ------------------- | ----------: | -----: | ------: |

| Market (MKT-RF)     |  \*\*1.2121\*\* |  29.22 |  <0.001 |

| Size (SMB)          | \*\*-0.1086\*\* |  -2.11 |  0.0348 |

| Value (HML)         | \*\*-0.4760\*\* |  -6.58 |  <0.001 |

| Profitability (RMW) |  \*\*0.4737\*\* |   7.61 |  <0.001 |

| Investment (CMA)    |  \*\*0.4281\*\* |   3.86 |  0.0001 |

| Momentum (MOM)      | \*\*-0.0941\*\* |  -2.76 |  0.0059 |



\### Interpretation



AAPL exhibited:



\* Strong positive market exposure.

\* Slight negative size exposure.

\* Strong negative value exposure, consistent with a growth-oriented factor profile.

\* Positive profitability exposure.

\* Positive investment exposure.

\* Slight negative momentum exposure over the sample.



All six factor coefficients were statistically significant at the 5% level in the estimated model.



\## Alpha Analysis



Estimated annualized alpha:



\*\*4.62%\*\*



However:



```text

Alpha t-stat = 0.590

Alpha p-value = 0.555

```



The estimated alpha is therefore \*\*not statistically significant\*\*.



The analysis does not provide sufficient statistical evidence that AAPL generated persistent abnormal returns after controlling for the six systematic factors.



This illustrates the central purpose of factor analysis:



> Strong historical returns do not necessarily imply persistent alpha once systematic exposures are taken into account.



\## Model Fit



```text

R-squared          = 59.61%

Adjusted R-squared = 59.43%

```



Approximately 59.6% of the variation in AAPL's daily excess returns is explained by the six-factor model over the analyzed sample.



\## Factor Attribution



Annualized mean excess-return attribution:



| Component     | Contribution |

| ------------- | -----------: |

| Market        |  \*\*+14.06%\*\* |

| Alpha         |   \*\*+4.62%\*\* |

| Size          |   \*\*+0.29%\*\* |

| Value         |   \*\*-4.07%\*\* |

| Profitability |   \*\*+0.86%\*\* |

| Investment    |   \*\*+0.85%\*\* |

| Momentum      |   \*\*-0.82%\*\* |

| Residual      |   \*\*\~0.00%\*\* |



The market factor was the largest positive contributor, while the negative value exposure was the largest offsetting factor contribution.



\## Multicollinearity Diagnostics



| Factor        |   VIF |

| ------------- | ----: |

| Market        | 1.322 |

| Size          | 1.497 |

| Value         | 1.998 |

| Profitability | 1.599 |

| Investment    | 1.709 |

| Momentum      | 1.112 |



The relatively low VIF values indicate that severe multicollinearity is not a major issue for this factor specification over the analyzed sample.



\## Rolling Factor Exposure



A \*\*252-trading-day rolling regression\*\* is used to measure how AAPL's systematic factor exposures evolve through time.



The project generates rolling exposure charts for:



\* Market

\* Size

\* Value

\* Profitability

\* Investment

\* Momentum



This makes it possible to identify changes in AAPL's factor profile across different market periods.



\## Visualizations



The project generates:



\### Rolling Factor Exposure



Shows how each factor beta changes over time.



\### Alpha Significance



Shows annualized alpha with a 95% HAC confidence interval.



\### Factor Attribution



Shows annualized contributions from alpha and each systematic factor.



\### Realized vs Factor Model



Compares cumulative realized excess returns with cumulative model-implied excess returns.



\## Repository Structure



```text

fama-french-factor-analysis/

│

├── README.md

├── Fama\_French\_Factor\_Exposure\_Analysis.ipynb

│

├── charts/

│   ├── rolling\_market\_beta.png

│   ├── rolling\_size\_beta.png

│   ├── rolling\_value\_beta.png

│   ├── rolling\_profitability\_beta.png

│   ├── rolling\_investment\_beta.png

│   ├── rolling\_momentum\_beta.png

│   ├── alpha\_significance.png

│   ├── factor\_attribution.png

│   └── realized\_vs\_factor\_model.png

│

└── outputs/

&#x20;   ├── factor\_attribution.csv

&#x20;   ├── performance\_metrics.csv

&#x20;   ├── regression\_statistics.csv

&#x20;   ├── rolling\_exposures.csv

&#x20;   ├── vif\_diagnostics.csv

&#x20;   └── ols\_summary.txt

```



\## Engineering Features



\### Robust Data Ingestion



The project dynamically parses the daily factor files from the Kenneth French Data Library and validates the resulting factor columns before modeling.



\### Data Alignment



Stock returns and factor returns are aligned by trading date before the regression dataset is constructed.



\### HAC Inference



HAC/Newey–West standard errors are used to make statistical inference more robust to heteroskedasticity and autocorrelation.



\### Rolling Regression



A 252-day rolling regression estimates how factor exposures evolve over time rather than assuming constant exposures.



\### Multicollinearity Diagnostics



Variance Inflation Factors are calculated for every factor.



\### Automated Research Outputs



The pipeline exports:



\* Regression statistics

\* Rolling exposures

\* VIF diagnostics

\* Factor attribution

\* Performance metrics

\* Full OLS summary



\## Limitations



This analysis is intended for quantitative research and educational purposes.



Important limitations include:



\* Results depend on the selected factor model.

\* Historical factor exposure does not guarantee future exposure.

\* Alpha significance is sample-dependent.

\* Factor attribution is based on average return contributions rather than a full trade-level P\&L decomposition.

\* Rolling coefficients may become unstable during unusual market conditions.

\* This analysis is in-sample and does not constitute an out-of-sample forecasting test.

\* The regression does not establish causal relationships.



\## Potential Extensions



\### Multi-Stock Analysis



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



\### Portfolio Analysis



Allow arbitrary portfolio weights and estimate portfolio-level factor exposure.



\### Expanded Factor Models



Add:



\* Quality

\* Low volatility

\* Liquidity

\* Short-term reversal

\* Additional momentum specifications



\### Advanced Statistical Analysis



Add:



\* Bootstrap confidence intervals

\* Structural-break tests

\* Regime analysis

\* Expanding-window estimation

\* Out-of-sample testing

\* Rolling alpha confidence intervals



\### Portfolio Construction



Use factor exposures as inputs to a constrained portfolio optimization framework.



\## Resume Description



\*\*Fama–French Factor Exposure \& Alpha Attribution Engine | Python, Pandas, Statsmodels\*\*



Developed a six-factor quantitative asset-pricing pipeline using daily Fama–French 5-factor and momentum data; implemented HAC-robust OLS, 252-day rolling factor exposures, VIF multicollinearity diagnostics and factor attribution; analyzed AAPL over 2021–2026, obtaining 59.6% model R² and estimating 4.6% annualized alpha that was statistically insignificant.



\## Key Takeaway



The analysis demonstrates how observed stock performance can be decomposed into systematic market and style-factor exposures rather than being automatically attributed to investment skill.



For AAPL, the model finds strong market exposure and meaningful style-factor exposures, while the estimated positive alpha is not statistically significant.



The project therefore demonstrates the practical distinction between:



\*\*Return ≠ Alpha\*\*



and shows how quantitative factor models can be used to evaluate the source of investment performance.



