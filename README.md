# Fama–French Factor Exposure & Alpha Attribution Analysis

A quantitative finance project that analyzes stock returns using the Fama–French five-factor model extended with the Momentum factor.

The project uses Apple Inc. (AAPL) as a case study to estimate systematic factor exposures, evaluate statistical significance, analyze changing factor exposures over time, and investigate factor-adjusted alpha.

## Project Overview

This project applies a six-factor asset-pricing framework to AAPL daily returns.

The six factors analyzed are:

* Market
* Size
* Value
* Profitability
* Investment
* Momentum

The analysis combines financial data processing, regression analysis, robust statistical inference, rolling regressions, multicollinearity diagnostics, factor attribution, and performance analysis.

## Research Question

The main research question is:

**How much of AAPL's historical return can be explained by systematic factor exposures, and is there evidence of abnormal returns after controlling for those factors?**

The project investigates:

1. AAPL's exposure to each systematic factor.
2. The statistical significance of those exposures.
3. Whether the model identifies positive or negative alpha.
4. Whether factor exposures change over time.
5. How historical returns can be attributed to different factors.

## Data

### Stock Data

Stock price data is obtained for Apple Inc. (AAPL).

* Stock: AAPL
* Frequency: Daily
* Start: January 2021
* End: June 2026
* Usable observations: 1,377

### Factor Data

The analysis uses data from the Kenneth R. French Data Library.

Factors used:

* Market excess return
* Size (SMB)
* Value (HML)
* Profitability (RMW)
* Investment (CMA)
* Momentum (MOM)
* Risk-free rate

## Methodology

The analysis follows this workflow:

1. Obtain AAPL historical price data.
2. Calculate daily stock returns.
3. Obtain Fama–French factor data.
4. Add the Momentum factor.
5. Align stock and factor dates.
6. Calculate AAPL excess returns.
7. Run the six-factor regression.
8. Calculate HAC/Newey–West robust standard errors.
9. Examine factor significance using t-statistics and p-values.
10. Calculate Variance Inflation Factors.
11. Run rolling 252-day regressions.
12. Estimate factor contributions.
13. Calculate performance metrics.
14. Generate charts and research outputs.

## Six-Factor Model

The regression uses the following explanatory variables:

* Market excess return
* SMB
* HML
* RMW
* CMA
* MOM

The model estimates:

* Alpha
* Market beta
* Size beta
* Value beta
* Profitability beta
* Investment beta
* Momentum beta

A positive beta indicates positive sensitivity to a factor, while a negative beta indicates negative sensitivity.

## Statistical Analysis

The project uses Ordinary Least Squares regression to estimate factor exposures.

HAC/Newey–West standard errors are used to make statistical inference more robust to potential heteroskedasticity and autocorrelation in the regression residuals.

For each factor, the analysis reports:

* Estimated beta
* Standard error
* t-statistic
* p-value

This allows the statistical significance of individual factor exposures to be evaluated.

## Performance Results

The historical performance analysis produced the following results:

| Metric                | Result  |
| --------------------- | ------- |
| CAGR                  | 16.48%  |
| Annualized Volatility | 27.69%  |
| Sharpe Ratio          | 0.570   |
| Maximum Drawdown      | -33.36% |
| Observations          | 1,377   |

These metrics provide a basic assessment of historical return, volatility, risk-adjusted performance, and downside risk.

## Factor Exposure Results

The estimated factor exposures are:

| Factor              | Beta    |
| ------------------- | ------- |
| Market              | 1.2121  |
| Size (SMB)          | -0.1086 |
| Value (HML)         | -0.4760 |
| Profitability (RMW) | 0.4737  |
| Investment (CMA)    | 0.4281  |
| Momentum (MOM)      | -0.0941 |

### Interpretation

AAPL had a market beta above 1, indicating greater sensitivity to broad market movements during the sample period.

The negative HML exposure indicates a negative relationship with the Value factor and is consistent with a growth-oriented factor profile.

The positive RMW exposure indicates positive sensitivity to the profitability factor.

The positive CMA exposure indicates positive sensitivity to the investment factor.

The SMB and MOM coefficients are relatively small compared with the market, value, profitability, and investment exposures.

## Alpha Analysis

One of the main objectives of the project is to determine whether AAPL generated returns beyond those explained by the six systematic factors.

The model estimates an annualized alpha of approximately:

**4.62%**

However, the estimated alpha has a p-value of approximately:

**0.555**

Therefore, the estimated alpha is **not statistically significant at conventional significance levels**.

This means the analysis does not provide strong statistical evidence of persistent abnormal returns after controlling for the factors included in the model.

This distinction is important because a positive estimated alpha does not automatically mean that statistically significant alpha exists.

## Rolling Factor Exposure

The project also performs rolling regressions using a 252-trading-day window.

Rolling regressions allow factor exposures to be examined over time instead of relying only on one coefficient calculated over the entire sample.

This helps identify changes in:

* Market sensitivity
* Size exposure
* Value exposure
* Profitability exposure
* Investment exposure
* Momentum exposure

This provides a more dynamic view of AAPL's factor characteristics.

## Multicollinearity Analysis

Variance Inflation Factors (VIF) are calculated to assess potential multicollinearity between explanatory variables.

Multicollinearity can make individual regression coefficients less stable and more difficult to interpret.

Including VIF diagnostics provides an additional validation step for the factor regression.

## Factor Attribution

The project estimates the contribution of the different systematic factors to observed returns.

The attribution framework separates return into components associated with:

* Market exposure
* Size exposure
* Value exposure
* Profitability exposure
* Investment exposure
* Momentum exposure
* Alpha and residual performance

The attribution should be interpreted as a statistical decomposition rather than a claim of causal return generation.

## Visualizations

The project generates charts covering:

* Cumulative performance
* Factor exposures
* Rolling factor betas
* Factor contributions
* Drawdowns
* Regression diagnostics

The generated charts are stored in the `charts` directory.

## Project Structure

The repository contains:

* `Fama_French_Factor_Exposure_Analysis.ipynb` - Main research notebook
* `README.md` - Project documentation
* `requirements.txt` - Python dependencies
* `charts/` - Generated visualizations
* `outputs/` - Analysis outputs
* `LICENSE` - Project license
* `.gitignore` - Git configuration

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
* Ordinary Least Squares
* HAC/Newey–West standard errors
* Variance Inflation Factor
* Rolling regression

### Visualization

* matplotlib
* seaborn

### Environment

* Jupyter Notebook

## How to Run

### Step 1: Clone the Repository

```text
git clone https://github.com/siddharthsingh1052008-lang/fama-french-factor-analysis.git
```

### Step 2: Enter the Project Directory

```text
cd fama-french-factor-analysis
```

### Step 3: Install Dependencies

```text
pip install -r requirements.txt
```

### Step 4: Launch Jupyter Notebook

```text
jupyter notebook
```

### Step 5: Open the Notebook

Open:

`Fama_French_Factor_Exposure_Analysis.ipynb`

Run the notebook cells sequentially to reproduce the analysis.

## Key Takeaways

The analysis demonstrates how factor models can be used to understand stock returns beyond simple historical performance metrics.

The AAPL case study shows:

* Market beta was greater than 1.
* AAPL had negative exposure to the Value factor.
* AAPL had positive exposure to Profitability.
* AAPL had positive exposure to Investment.
* Factor exposures can change over time.
* The model produced a positive estimated alpha.
* The estimated alpha was not statistically significant.

The results demonstrate the importance of distinguishing between an estimated return premium and statistically significant evidence of abnormal performance.

## Limitations

The project has several limitations:

* The analysis focuses on one stock.
* Historical relationships may not continue in the future.
* Factor exposures depend on the selected model and dataset.
* The sample period may contain market conditions that are not representative of other periods.
* Regression-based factor attribution does not establish causality.
* Alpha estimates can change with the sample period, factor specification, and model assumptions.

## Future Improvements

Potential extensions include:

* Analyze multiple stocks.
* Compare factor exposures across industries.
* Build a portfolio-level factor model.
* Add out-of-sample testing.
* Compare the five-factor model with the six-factor model.
* Test different time periods.
* Build factor-neutral portfolios.
* Automate analysis across a larger stock universe.
* Add additional robustness tests.
* Compare model explanatory power across companies.

## Skills Demonstrated

This project demonstrates practical experience with:

* Quantitative finance
* Factor investing
* Asset pricing
* Financial econometrics
* Regression analysis
* Statistical inference
* Time-series analysis
* Risk analysis
* Portfolio analytics
* Python
* Data visualization
* Financial research

## Disclaimer

This project is intended for educational and research purposes only.

It does not constitute investment advice or a recommendation to buy or sell any security.

## License

This project is licensed under the MIT License.
