---
description: >-
  We have assembled a list of basic strategies and indicators for you to draw
  from in building your own strategy. Our theory is that simple strategies are
  often the best.
---

# Example Strategies

## Simple Strategy

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption><p><a href="https://www.tradingview.com/chart/QIsX3O3T/">https://www.tradingview.com/chart/QIsX3O3T/</a></p></figcaption></figure>

To showcase how to send JSON messages for a strategy from TradingView, we have created this simple strategy that takes very frequent trades and can be tested on the 1 minute chart. It can also be tested on long only, short only, or both directions. [Head to this TradingView chart](https://www.tradingview.com/chart/QIsX3O3T/) to see the strategy. You can also create an alert from this chart and send the messages to your own webhook URL.

Steps to use it:

1. [Create a strategy](../core-concepts/strategies.md) on your TradersPost account using the [stocks asset class](../assets/stocks.md).
2. Then subscribe a paper broker to that strategy using a [strategy subscription](../core-concepts/subscriptions.md).
   1. There will be default settings when you create the subscription. The settings you'll want to change are:
      1. Auto Submit: On
      2. Sides: Both (Bullish & Bearish)
      3. Entry order type: Market
      4. Exit order type: Market
3. When the subscription is successfully created, copy the [Webhook URL](../core-concepts/webhooks.md).
4. Create a new alert on TradingView from the [Simple Strategy Chart we provided](https://www.tradingview.com/chart/QIsX3O3T/).
   1. Under condition, choose the Simple Strategy (Both)
      1. It will say Both if the strategy settings are allowing long and short.
   2. The Message will say `{{strategy.order.alert_message}}`. Leave this alone.
   3. Click the Notifications tab and check the box for Webhook URL. Paste in the webhook URL you copied.
   4. Hit Create.

You should now have trades coming in every minute to go long or short or exit those positions. Under your [subscriptions tab](https://app.traderspost.io/app/trading/strategies/subscriptions), you can click the Trades button next to your strategy to see the list of trades that are coming in. You can also review the [Webhooks log](https://app.traderspost.io/app/trading/webhooks) to see the messages we parsed as they came in.

You can find the source code for this [simple strategy here](https://raw.githubusercontent.com/TradersPost/pinescript/refs/heads/master/strategies/Simple%20Strategy.pine).

## Scheduled Alert - TradingView Indicator

Allows you to send an alert signal at a time you specify, useful for closing all open positions at the end of a trading session or before a particular event. The script can be used as a standalone or you can copy and paste the code into your own scripts.

{% embed url="https://youtube.com/live/Z0Y5quEdKJ0" %}

* [View on TradingView](https://www.tradingview.com/script/wEYIjdUI-TradersPost-Scheduled-Alert/)

## Simple Trend Lines - TradingView Indicator

A walkthrough of our newest indicator, Simple Trend Lines, made for TradingView. Designed to allow the automation of trend lines for use in algorithmic trading. Check out the source code on TradingView [here](https://www.tradingview.com/script/ny3RIRSs-TradersPost-Simple-Trend-Lines/).

{% embed url="https://www.youtube.com/watch?v=yHjJNJc4HaI" %}

### 8-55 EMA Crossover NQ Futures Strategy

This automated strategy was built from a discretionary strategy by Brett Glover. Don't miss our interview of Brett and his journey to becoming a full time futures trader: [Creating Income Trading NQ Futures with Brett Glover - Trading Bot Sessions (EP 004)](https://www.youtube.com/watch?v=514gnyuO1TM)

* [View on TradingView](https://www.tradingview.com/script/tubAmq4X-8-55-EMA-Crossover-NQ-Futures-Strategy/)
* [View on GitHub](https://github.com/TradersPost/pinescript/blob/master/strategies/8-55-EMA-Crossover-NQ-Futures-Strategy.pinescript)

{% embed url="https://www.youtube.com/watch?v=61mYTkmM8XU" %}

### High-Low Range Trend-Following

This basic trend following strategy looks for large ranges of trading on a single period and follows the trend if price is ascending. When the opposite conditions exist, it exits. Designed only to showcase how to set up strategies in TradingView and trade stocks on TradersPost, this strategy can be copied and modified to your liking.

* [View on TradingView](https://www.tradingview.com/script/ouTuH5zc-TradersPost-High-Low-Range-Strategy/)
* [View on GitHub](https://github.com/TradersPost/pinescript/blob/master/strategies/HighLowRangeTrendFollowing.pinescript)

{% embed url="https://youtu.be/02hBkacKSkA" %}

### Confluence of Alerts

A walkthrough of our newest indicator, Confluence of Alerts, made for TradingView. Designed to enhance TradingView alert system. Read more in our [blog post](https://blog.traderspost.io/article/new-indicator-confluence-of-alerts) and view the source code on TradingView [here](https://www.tradingview.com/script/bVt6wNeG-TradersPost-Confluence-of-Alerts/).

{% embed url="https://www.youtube.com/watch?v=nKVavKVFV60" %}

## Easily Turn a Channel into an Automated Trading Strategy

Execute buy and sell trades in your broker's account simply using trend lines and TradersPost.

{% embed url="https://www.youtube.com/watch?v=rHvRkfdYNfE" %}

## Automated Channel

A walkthrough of our newest indicator, Automated Channel, made for TradingView. Designed as an alternative to the native channel tool for traders looking to automate a channel trading strategy. Read more in our [blog post](https://blog.traderspost.io/article/new-indicator-automated-channel) and view the source code on TradingView [here](https://www.tradingview.com/script/vMJPxHfn-TradersPost-Automated-Channel/).

{% embed url="https://www.youtube.com/watch?v=2uflxOuF0ds" %}

## Using SSL Hybrid in an Automated Trading Strategy

Learn how to use the popular SSL Hybrid indicator as the base for an automated trading strategy using TradersPost.

{% embed url="https://www.youtube.com/watch?v=t2SbQosGgl0" %}

## Algorithmic Trading with Engulfing Candles from TradingView to TradersPost

Use the native bullish and bearish engulfing candle indicators from TradingView in algo trading on TradersPost. View the source code on TradingView [here](https://www.tradingview.com/script/DkXZdTPO-My-Super-Bollinger/).

{% embed url="https://www.youtube.com/watch?v=_k-EMFzXa6Y" %}

## Automate a Trading Strategy Using Supertrend and Bollinger Bands

Combining Supertrend and Bollinger Bands into a simple automated trading strategy using Pine Script on TradingView and TradersPost. Check out the source code on TradingView [here](https://www.tradingview.com/script/DkXZdTPO-My-Super-Bollinger/).

{% embed url="https://www.youtube.com/watch?v=KwPJ4Np67lw" %}

## Convert EMA Crossovers into an Automated Strategy

A step-by-step guide for automating EMA crosses using TradingView.

{% embed url="https://www.youtube.com/watch?v=tpNYxXoymsU" %}

## Automatically Range Trade using the Heikin Ashi RSI Indicator

A step-by-step guide for automatically trading a range using HARSI on TradingView.

{% embed url="https://www.youtube.com/watch?v=SD_hShzM6N0" %}

## Execute LuxAlgo SMC Trade Signals in your Brokerage Account

Turn any LuxAlgo signal into live trades executed in your brokerage account.

{% embed url="https://www.youtube.com/watch?v=8wEJA7vXm7Y" %}
