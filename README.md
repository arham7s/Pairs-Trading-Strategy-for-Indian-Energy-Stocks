# Pairs-Trading-Strategy-for-Indian-Energy-Stocks

## Overview

Pairs trading is a popular market-neutral trading strategy based on the assumption that two historically correlated stocks will revert to their mean spread. In this project, we:
- **Download** historical price data for IOC.NS and BPCL.NS using the `yfinance` library.
- **Handle data issues** (e.g., missing "Adj Close" column for Indian stocks).
- **Test for cointegration** between the two stocks.
- **Determine a hedge ratio** using linear regression.
- **Generate trading signals** based on the spread deviation from a rolling mean and standard deviation.
- **Backtest the strategy** by computing cumulative returns.
- **Evaluate performance** using metrics such as the Sharpe Ratio and Maximum Drawdown.

## Motivation

- **Statistical Edge:** By exploiting the long-run equilibrium relationship between two cointegrated stocks, the strategy seeks to capture mean-reversion profit opportunities.
- **Risk Management:** The market-neutral nature of pairs trading reduces exposure to overall market movements.
- **Practical Application:** This project serves as a practical demonstration of quantitative finance techniques and is ideal for showcasing skills on GitHub and in a resume.

## Methodology

### Data Collection and Preprocessing

- **Data Source:** Yahoo Finance via `yfinance`.
- **Stocks:** `IOC.NS` and `BPCL.NS`
- **Date Range:** January 1, 2015 – January 1, 2023
- **Steps:**
  - Download historical data.
  - Check for the "Adj Close" column; if unavailable, use "Close".
  - Align and clean the data.

![carbon (3)](https://github.com/user-attachments/assets/bdc5450a-79ed-4e1f-a5c1-5249137cdb79)



### Cointegration Analysis

- **Objective:** Verify that IOC.NS and BPCL.NS share a long-run equilibrium.
- **Steps:**
  - Calculate correlation between the two stocks.
  - Perform the Engle-Granger cointegration test.
  - Use a linear regression (IOC.NS ~ BPCL.NS) to compute the hedge ratio (β):
    \[
    \text{spread} = \text{IOC.NS} - \beta \times \text{BPCL.NS}
    \]

### Signal Generation

- **Rolling Statistics:** Compute a 30-day rolling mean and standard deviation of the spread.
- **Trading Rules:**
  - **Long Signal (+1):** When the spread is below the lower threshold (mean - std).
  - **Short Signal (-1):** When the spread is above the upper threshold (mean + std).
  - **Hold:** Carry the previous signal until a reversal occurs.

### Backtesting the Strategy

- **Daily Returns:** Compute percentage returns for each stock.
- **Strategy Returns:** Based on the previous day's signal:
  \[
  R_t = \text{signal}_{t-1} \times \left( \Delta \text{IOC.NS}_t - \beta \times \Delta \text{BPCL.NS}_t \right)
  \]
- **Cumulative Returns:** Evaluate the growth of a $1 investment over the period.

### Performance Evaluation

- **Sharpe Ratio:** Annualized ratio to measure risk-adjusted returns.
- **Maximum Drawdown:** Largest percentage drop from peak cumulative return to assess risk.

## Results and Visualizations

Below are sample outputs obtained after running the script:
