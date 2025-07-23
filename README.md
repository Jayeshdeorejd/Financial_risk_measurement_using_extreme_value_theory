# Financial Risk Measurement in Indian Stock Exchange

## Overview

This project analyzes **financial risk in the Indian banking sector** over five years (Oct 2019 – Sep 2024) using stock data from:
- **IDFC First Bank**
- **ICICI Bank**
- **State Bank of India (SBI)**
- **HDFC Bank**

We employ **Extreme Value Theory (EVT)** to model rare but significant events (extreme returns) and use **Value at Risk (VaR)** and **Expected Shortfall (ES/CVaR)** for risk estimation. Tail dependencies between banks are modeled using a **t-copula** approach.

## Objectives

- Quantify risk of extreme losses for individual banks and a portfolio using EVT (POT method).
- Estimate and interpret VaR and ES for each bank.
- Use **t-copula models** to analyze tail dependence and joint risk across banking assets.
- Compare risk metrics at both individual and portfolio levels.

## Data

- **Source:** Yahoo Finance (2019-10-01 to 2024-09-30)
- **Assets:** Daily stock prices for IDFCFIRSTB.NS, ICICIBANK.NS, SBIN.NS, HDFCBANK.NS
- **Tools:** R and packages `quantmod`, `ggplot2`, `extRemes`, `evd`, `copula`, `patchwork`

## Methodology

1. **Data Retrieval and Preprocessing**
   - Download daily price data for all four banks
   - Compute daily returns; clean missing values

2. **Descriptive Analysis**
   - Calculate mean, variance, min, max for all banks' daily returns
   - Plot time series, boxplots, and Q-Q plots for returns

3. **Normality Testing**
   - Perform Kolmogorov-Smirnov test (normality is rejected for all banks[2])

4. **Extreme Value Analysis: Peaks Over Threshold (POT)**
   - Select left-tail (negative) extreme returns below specific quantiles
   - Fit the **Generalized Pareto Distribution (GPD)** to model tail risk
   - Estimate GPD parameters (scale, shape) for each bank

5. **Risk Metrics**
   - Compute 95% VaR and Expected Shortfall for each bank using EVT
   - Compare with empirical risk and interpret in context

6. **Copula Modelling**
   - Transform returns to uniforms, fit a **multivariate t-copula**
   - Analyze pairwise tail dependence coefficients (lower and upper tail)
   - Simulate joint returns using the fitted t-copula
   - Construct an equally weighted portfolio and estimate overall VaR, CVaR

## Key Results

- **Normality rejected**: Returns of all banks exhibit fat tails and skewness, validating EVT usage for risk estimation.
- **VaR at 95% confidence level:**
  - IDFC: -5.57%
  - ICICI: -6.52%
  - SBI: -5.72%
  - HDFC: -4.45%
- **Expected Shortfall (CVaR):** Ranges from 7.0% to 9.3% across banks—losses could be significantly worse than VaR in the worst 5%.
- **Portfolio Risk:**
  - Portfolio VaR: -2.35%
  - Portfolio CVaR: -3.57%
  - Diversification across banks reduces overall portfolio risk relative to the worst individual asset.

- **Tail dependence:** Significant lower tail dependence exists, especially between HDFC and ICICI, indicating high likelihood of simultaneous extreme losses among some banks.

## File Structure

```
backend_code.R         # All code for data retrieval, analysis, plots, EVT, copula, simulations
```

## How to Run

1. Ensure R (latest version) is installed.
2. Install required packages:

   ```R
   install.packages(c("quantmod", "ggplot2", "patchwork", "extRemes", "evd", "copula"))
   ```

3. Run the `backend_code.R` script in R or RStudio.

   - The script will output analysis, test results, graphs, and VaR/CVaR figures for both individual banks and the portfolio.

## Interpretation

- **VaR:** "We are 95% sure that the loss will not exceed VaR in a day, under normal market conditions."
- **CVaR/ES:** "If losses do breach VaR, average loss in that scenario is the ES (generally more conservative and informative)."
- **Portfolio metrics** are lower due to diversification, but tail dependence among banks limits risk reduction, particularly during market stress.


**License:** For educational/non-commercial use only.

*Refer to the project report for deeper technical details, background, and interpretation of findings.*

[1] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/84150365/fa2b9fc0-18ed-4c85-af8a-cd254b76a3a4/backend_code.R
[2] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/84150365/ae8733e2-71bf-4cce-a321-15e44d2f470e/Group_3_FinalReport.docx
