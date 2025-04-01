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
