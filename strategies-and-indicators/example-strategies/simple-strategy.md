---
description: >-
  A TradingView example strategy for firing many alerts to test how automated
  trading works on TradersPost.
---

# Simple Strategy

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption><p><a href="https://www.tradingview.com/chart/QIsX3O3T/">https://www.tradingview.com/chart/QIsX3O3T/</a></p></figcaption></figure>

To showcase how to send JSON messages for a strategy from TradingView, we have created this simple strategy that takes very frequent trades and can be tested on the 1 minute chart. It can also be tested on long only, short only, or both directions. [Head to this TradingView chart](https://www.tradingview.com/chart/QIsX3O3T/) to see the strategy. You can also create an alert from this chart and send the messages to your own webhook URL.

Steps to use it:

1. [Create a strategy](../../core-concepts/strategies.md) on your TradersPost account using the [stocks asset class](../../assets/stock-trading.md), if you plan to test stocks. Strategies are based on an asset class, so you'll need to make this choice first.
2. Then subscribe a paper broker to that strategy using a [strategy subscription](../../core-concepts/subscriptions.md).
   1. There will be default settings when you create the subscription. The settings you'll want to change are:
      1. Auto Submit: On
      2. Sides: Both (Bullish & Bearish)
      3. Entry order type: Market
      4. Exit order type: Market
3. When the subscription is successfully created, copy the [Webhook URL](../../core-concepts/signals/webhooks.md).
4. Create a new alert on TradingView from the [Simple Strategy Chart we provided](https://www.tradingview.com/chart/QIsX3O3T/).
   1. Under condition, choose the Simple Strategy (Both)
      1. It will say Both if the strategy settings are allowing long and short.
   2. The Message will say `{{strategy.order.alert_message}}`. Leave this alone the messages will be coming from your strategy settings and this placeholder is used to tell the strategy it should use the internal messages.
   3. Click the Notifications tab and check the box for Webhook URL. Paste in the webhook URL you copied.
   4. Hit Create.

You should now have trades coming in every minute to go long or short or exit those positions. Under your [subscriptions tab](https://app.traderspost.io/app/trading/strategies/subscriptions), you can click the Trades button next to your strategy to see the list of trades that are coming in. You can also review the [Webhooks log](https://app.traderspost.io/app/trading/webhooks) to see the messages we parsed as they came in.

Links:

* Add this [Simple Strategy](https://www.tradingview.com/script/Wq1r6KLV-Simple-Strategy/) example to your TradingView favorites.
* You can find the source code for this [simple strategy here](https://raw.githubusercontent.com/TradersPost/pinescript/refs/heads/master/strategies/Simple%20Strategy.pine).
