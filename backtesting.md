---
description: >-
  Backtesting is a critical tool for any trader that is running automated
  trading strategies. It uses historical data to determine the effectiveness of
  a strategy in different market conditions.
---

# Backtesting

## What To Measure

Backtesting can provide you with critical statistical feedback about a given system and how you should deploy the system depending on market conditions. For example, deciding which tickers to run the strategy on or whether or not to be long or short is a critical decision for the trader running the strategy. Here are some common backtesting statistics that you should be on the lookout for.

* **Net profit or loss:** __ Net percentage gained or lost
* [**Volatility**](https://www.investopedia.com/terms/v/volatility.asp) **measures:** __ Maximum percentage upside and downside
* **Averages:** Percentage average gain and average loss, average bars held
* [**Exposure**](https://www.investopedia.com/terms/m/marketexposure.asp)**:** Percentage of capital invested (or exposed to the market)
* **Ratios:** Wins-to-losses ratio
* [**Annualized**](https://www.investopedia.com/terms/a/annualize.asp) **return:** Percentage return over a year
* [**Risk-adjusted return**](https://www.investopedia.com/terms/r/riskadjustedreturn.asp)**:** Percentage return as a function of risk

## TradingView Backtesting

TradingView is one of many tools that exist in the market for  building strategies and backtesting them so that you can decide what tickers to run the strategy on and on what timeframes.

### Backtesting MOMO

You can find an example MOMO strategy backtester [here](tradingview.md#complex-strategy) that can be used with TradingView. You can explore TradingView [backtesting scripts](https://www.tradingview.com/scripts/backtesting/) as well to get ideas for how to backtest other strategy ideas.

{% embed url="https://www.youtube.com/watch?v=FKICHC0kF3o" %}
TradingView Strategy Tester Video
{% endembed %}

### Strategy Optimizers

There are tools that exist to roll through all the possible strategy input settings to automatically see which settings have the best performance for a strategy on a specific ticker and timeframe.

#### The Optimiser

The [TradingView Optimiser](https://chrome.google.com/webstore/detail/the-optimiser/emcpjechgmpcnjphefjekmdlaljbiegp) is a tool that will run through the values in a TradingView Strategy and change each value. It will then download the backtest results. It uses a Machine Learning technique to choose the best settings.

#### TradingView Strategy Finder

The [TradingView Strategy Finder](https://chrome.google.com/webstore/detail/tradingview-strategy-find/jdepgjdjpmpjljfdcmnbjmafkbckkhko?hl=en) is able to automatically backtest your TradingView strategies. This tool is highly customizable and you are able to test as much input values as you like. Start to find the best settings for you strategy to be even more profitable in your trading.

## TrendSpider Backtesting

Refine your automated trading performance by backtesting your strategies using TrendSpider's chart-based backtesting tool. Create technical buy and sell rules without knowing how to write code. [Learn more](https://trendspider.com/product/backtesting/).

{% embed url="https://www.youtube.com/watch?v=Cpvdd0fJKVI" %}
TrendSpider Strategy Tester Video
{% endembed %}

## Other Backtesting Tools

* [Python Backtrader](https://github.com/mementum/backtrader) - Backtrader is a Python framework with a plethora of features for backtesting trading strategies.
* [QuantConnect Lean](https://github.com/QuantConnect/Lean) - QuantConnect's Lean is an open-source algorithmic trading engine built for easy strategy research and backtesting.
* [PyAlgoTrade](https://github.com/gbeced/pyalgotrade) - PyAlgoTrade is a Python Algorithmic Trading Library that was started to focus on backtesting.
* [Python BT](https://github.com/pmorissette/bt) - Bt is a Python backtesting framework for testing quantitative trading methods. This framework makes it simple to develop strategies that combine various Algos.
* [finmarketpy](https://github.com/cuemacro/finmarketpy) - finmarketpy is a Python based library that enables you to analyze market data and also to backtest trading strategies using a simple to use API, which has prebuilt templates for you to define backtest.
* [Fastquant](https://github.com/enzoampil/fastquant) - Fastquant makes it simple to backtest investing strategies with as few as three lines of Python code. Its objective is to encourage data-driven investing by making quantitative finance analysis accessible to everyone.\
