# 📈Pairs-Trading-Strategy-for-Indian-Energy-Stocks

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

### Cointegration Analysis

- **Objective:** Verify that IOC.NS and BPCL.NS share a long-run equilibrium.
- **Steps:**
  - Calculate correlation between the two stocks.
  - Perform the Engle-Granger cointegration test.
  - Use a linear regression (IOC.NS ~ BPCL.NS) to compute the hedge ratio (β):
    \[
    \text{spread} = \text{IOC.NS} - \beta \times \text{BPCL.NS}
    \]
    ![carbon (4)](https://github.com/user-attachments/assets/01db9306-e5ca-4129-a04f-3d4439a27f43)


### Signal Generation

- **Rolling Statistics:** Compute a 30-day rolling mean and standard deviation of the spread.
- **Trading Rules:**
  - **Long Signal (+1):** When the spread is below the lower threshold (mean - std).
  - **Short Signal (-1):** When the spread is above the upper threshold (mean + std).
  - **Hold:** Carry the previous signal until a reversal occurs.
    ![carbon (5)](https://github.com/user-attachments/assets/f3e3e2b6-a934-4037-98b5-652c5883e9af)


### Backtesting the Strategy

- **Daily Returns:** Compute percentage returns for each stock.
- **Strategy Returns:** Based on the previous day's signal:
  \[
  R_t = \text{signal}_{t-1} \times \left( \Delta \text{IOC.NS}_t - \beta \times \Delta \text{BPCL.NS}_t \right)
  \]
- **Cumulative Returns:** Evaluate the growth of a $1 investment over the period.
  ![carbon (6)](https://github.com/user-attachments/assets/e5a4aa21-9fe0-40eb-903c-5d6a309ef7a7)

### Performance Evaluation

- **Sharpe Ratio:** Annualized ratio to measure risk-adjusted returns.
- **Maximum Drawdown:** Largest percentage drop from peak cumulative return to assess risk.
  ![carbon (7)](https://github.com/user-attachments/assets/7a62705c-e733-41fd-94b8-92e383163e62)




## Results and Visualizations

Below are sample outputs obtained after running the script:

- ![download (1)](https://github.com/user-attachments/assets/2ebe39c0-cc30-45d4-9bc6-d553cbff5fe7)
- ![download (2)](https://github.com/user-attachments/assets/3f461a8f-90d8-4eb7-8a64-38eca6c9b330)
- ![download (3)](https://github.com/user-attachments/assets/401a341d-2ae3-4a17-b59e-2855c86a1b6f)
- ![download (4)](https://github.com/user-attachments/assets/e7388cdd-2a19-41b5-a628-ac182b1951e3)

## Key Performance Metrics and Their Implications

- **Annualized Sharpe Ratio: -0.3163**
  - A **negative Sharpe Ratio** means that the strategy's average returns are below the risk-free rate (or below zero if using 0% as the risk-free rate).
  - This indicates that the strategy does not adequately compensate for the risk taken, with volatility outweighing any gains.

- **Maximum Drawdown: -69%**
  - A **-69% drawdown** signifies a very large loss from peak to trough in the strategy's cumulative returns.
  - Such a steep drawdown suggests that the strategy is highly risky and could lead to substantial losses during adverse periods.

- **Overall Implications**
  - The current configuration of the strategy is **unprofitable** and **highly risky**.
  - The results suggest a need to revisit key parameters (e.g., thresholds, rolling window size) and incorporate risk management measures such as stop-loss rules or dynamic position sizing.
  - Additional steps like including transaction costs, performing out-of-sample testing, or further optimization might help improve the strategy's performance.





