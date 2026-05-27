# Momentum and Comomentum Trading Strategy
Replication and enhancement of the momentum strategy proposed by Lou & Polk (2021).

## Overview

This project replicates and extends the findings of the paper:

> Lou, D. and Polk, C. (2021), *Comomentum: Inferring Arbitrage Activity from Return Correlations*.

The objective is to construct an enhanced momentum trading strategy using a simplified version of the paper’s **comomentum measure**, which captures abnormal return correlation among stocks commonly targeted by momentum traders.

The project was developed as part of the MSc coursework in quantitative finance and focuses on:

- Cross-sectional asset pricing
- Momentum factor construction
- Rolling factor regressions
- Fama-MacBeth methodology
- Statistical evaluation of trading strategies
- Risk-adjusted performance analysis

---

## Research Motivation

Traditional momentum strategies tend to experience periods of strong performance followed by severe crashes.  
Lou & Polk (2021) show that these variations can be partially explained by **comomentum**, a measure of synchronized arbitrage activity across momentum stocks.

The central hypothesis is:

- **Low comomentum → stronger future momentum returns**
- **High comomentum → weaker future momentum returns**

This project investigates whether incorporating comomentum information can improve the performance of a standard momentum factor.

---

## Data

The analysis uses weekly U.S. equity data:

- Weekly stock returns
- Company live/dead indicators
- Fama-French 3-factor returns
- Stock identifiers and dates

### Main Files

| File | Description |
|---|---|
| `US_Returns.csv` | Weekly stock returns |
| `US_live.csv` | Live/dead company indicator |
| `FamaFrench.csv` | Fama-French factor returns |
| `US_Dates.xlsx` | Weekly dates |
| `US_Names.xlsx` | Stock names |

---

## Methodology

### 1. Standard Momentum Construction

For each stock and each week:

- Compute cumulative returns over the previous 48 weeks
- Skip the most recent 4 weeks
- Construct cross-sectional momentum exposures

This approximates the classic:

- 12-month lookback
- 1-month skip

used in academic literature.

---

### 2. Fama-MacBeth Regressions

Weekly cross-sectional regressions are estimated:


$$ R_{i,t+1} = \alpha_t + \beta_t MOM_{i,t} + \epsilon_{i,t+1} $$

where:

- $R_{i,t+1}$ is the one-week ahead return
- $MOM_{i,t}$ is the lagged momentum exposure

The time series of estimated coefficients represents the momentum factor returns.

Missing observations and delisted firms are excluded dynamically at each date.

---

### 3. Comomentum Measure

For each stock:

1. Run rolling 52-week regressions on the Fama-French factors
2. Obtain abnormal return residuals
3. Compute pairwise residual correlations
4. Aggregate correlations into a market-wide comomentum measure

The implementation follows a simplified version of Lou & Polk (2021) without industry adjustment.

---

### 4. Enhanced Momentum Strategy

The standard momentum factor is adjusted using the comomentum signal.

The intuition is:

- Reduce momentum exposure during periods of elevated comomentum
- Increase exposure during periods of low comomentum

The adjusted strategy is then evaluated against the standard momentum benchmark.

---

## Performance Evaluation

The following metrics are computed:

- Annualized return
- Annualized volatility
- Sharpe ratio
- Cumulative returns
- Drawdowns
- Factor return comparison

---

## Technologies Used

- Python
- NumPy
- pandas
- statsmodels
- matplotlib
- scipy

---

## Key Concepts

This project applies techniques from:

- Empirical Asset Pricing
- Quantitative Trading
- Econometrics
- Statistical Arbitrage
- Factor Investing
- Time-Series Analysis

---

## Example Results

The project compares:

- Standard Momentum
- Comomentum-Adjusted Momentum

using cumulative factor return plots and risk-adjusted statistics.

(Insert figures here)

---

## Repository Structure

```text
src/
    data_loader.py
    momentum.py
    comomentum.py
    fama_macbeth.py
    performance.py
