---
description: >-
  MT5 webhook automation is possible by using the TradersPostWebhookRequest
  library and sending you trade signals through to a broker of your choice at
  TradersPost.
---

# MetaTrader 5 - MT5

## MetaTrader 5 Expert Advisors (EA)

With its advanced charting capabilities, customizable indicators, and support for algorithmic trading through Expert Advisors (EAs), MT5 offers both novice and experienced traders a robust environment to execute their trading strategies efficiently and effectively. However, it's less apparent how you might automate a strategy in MT5 through any broker of your choice.

TradersPost can support futures, stock, and crypto trading from MT5 using a library we've written that can help build the JSON message that is sent through a [TradersPost webhook](../core-concepts/webhooks.md).

We have built an example EA that will trade on the next tick if it hasn't already and then never trade again after. It's meant to demonstrate only how you construct the JSON message and send the request to TradersPost.&#x20;

{% embed url="https://github.com/TradersPost/metatrader5/blob/main/MQL5/Experts/Advisors/TradersPostExample.mq5" %}

## Why automate MetaTrader 5 with TradersPost?

By integrating MT5 with TradersPost, users can automate their trading strategies across multiple asset classes, including stocks, futures, and cryptocurrencies. TradersPost supports a wide range of brokers such as TradeStation, Alpaca, Robinhood, E\*TRADE, tastytrade, IBKR, Webull, and futures brokers like Tradovate and NinjaTrader as well as crypto exchanges like Coinbase, Kraken, Bybit, and Binance. This integration allows users to send automated signals from MT5 directly to TradersPost, where they can manage trade execution with advanced strategy rules, risk management, and position sizing features.

Notably, [Bybit offers its own MT5 servers](https://www.bybit.com/future-activity/en/mt5), which means users can automate strategies on Bybit's MT5 platform and seamlessly route trades through their Bybit connection on TradersPost. This setup provides enhanced control and sophistication in trade execution, making it easy to automate strategies across different asset classes while utilizing TradersPost's robust automation tools. Although Bybit is currently the main broker supporting MT5 servers natively, users of other brokers supported by TradersPost can still leverage MT5 to create sophisticated automated strategies, taking full advantage of TradersPost's powerful automation framework.

#### Can I use an MT5 server with a broker that TradersPost doesn't support?

Yes! In the examples we provide below, we're using a StoneX Futures account and routing a manually constructed trade to a paper broker using TradeStation market data.

## Installing TradersPostWebhookRequest.mqh

Adding a library to the Include folder is fairly straight-forward.&#x20;

1. Ensure you have enabled algorithmic trading on MT5 and added the TradersPost webhook domain to your allowed WebRequest URLs. [Read more on this here](https://github.com/TradersPost/metatrader5?tab=readme-ov-file#enabling-traderpost-and-webrequests-in-mt5).
2. Add the TradersPostWebhookRequest.mqh file to your Include folder. [Read more on this here](https://github.com/TradersPost/metatrader5?tab=readme-ov-file#setting-up-traderspostwebhookrequest-in-mt5).
3. Then you can include TradersPostWebhookRequest.mqh in your EA scripts, define your webhook URL, and build JSON messages to send to TradersPost. See the [example EA here](https://github.com/TradersPost/metatrader5/blob/main/MQL5/Experts/Advisors/TradersPostExample.mq5).

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>TradersPostWebhookRequest.mqh goes into your data folder under MQL5/Include.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>Adding the <a href="https://github.com/TradersPost/metatrader5/blob/main/MQL5/Experts/Advisors/TradersPostExample.mq5">TradersPostExample EA</a> will demonstrate how a webhook request is made to buy 1 contract of NQZ2024 with a take profit and stop loss pre-configured.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption><p>In this example, the webhook request is sent immediately to TradersPost to automatically execute 1 contract of NQ with a take profit and stop loss order attached as a bracket order with the paper broker.</p></figcaption></figure>

If you are interested automating your MetaTrader 5 strategies, give TradersPost a try and [Register](https://traderspost.io/register) your free account today! If you have any questions, join our [Community](https://traderspost.io/community) or email us at [support@traderspost.io](mailto:support@traderspost.io).
