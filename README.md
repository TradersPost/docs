---
description: >-
  TradersPost is an automated trading platform that can automate your
  TradingView or TrendSpider strategies in brokers like TD Ameritrade,
  TradeStation, Tradier, Robinhood, and Alpaca.
cover: .gitbook/assets/Documentation Cover.jpeg
coverY: 0
---

# What is TradersPost?

{% hint style="warning" %}
TradersPost is **NOT** designed to be a high frequency trading platform. Your strategy needs to run on a higher timeframe. Please do not setup strategies on 1 minute chart or less and send hundreds of signals to TradersPost in a short amount of time. These types of strategies do not work due to slippage and rate limiting with the underlying broker APIs.\
\
While we do not currently rate limit traffic to webhooks, we may contact you and disable your webhooks and strategy subscriptions if we determine that your account is sending too many trades.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=WucPurodgk8" %}
TradersPost Explainer Video
{% endembed %}

## Who is TradersPost for?

* **Strategy Developers** - a person that is interested in creating automated trading strategies and connecting them to their broker.
* **Traders and Investors** - a person that is interested in connecting automated trading strategies to their broker without any coding knowledge.

## How does it work?

TradersPost is made of the following concepts. You can use them together to create automated trading strategies in your broker and allow other people to subscribe to your strategies.

* [Signals](./#signals) - Signals are buy or sell signal that can be produced by an automated algorithm or even a manual human trader.
* [Strategies](./#strategies) - Strategies define a group of signals. Users can subscribe to strategies and have the signals place trades directly in their broker.
* [Brokers](./#brokers) - Bring your own broker by connecting it to TradersPost. We support several brokers like **TD Ameritrade**, **Alpaca** and **TradeStation**.
* [Subscriptions](./#strategy-subscriptions) - Subscriptions allow you to connect a strategy to a broker, define your risk tolerance and position sizing.

If you prefer to watch a video demo of TradersPost to get a high level overview, this video is for you. If not, feel free to continue reading to get a high level overview.

{% embed url="https://www.youtube.com/watch?v=AWSImgUtw98" %}
Watch a demo of TradersPost if you prefer a video.
{% endembed %}

## Signals

Signals are buy and sell instructions that can be produced by an automated algorithm or even a manual human trader. Signals are sent to TradersPost via webhooks using JSON.

> A webhook in web development is a method of augmenting or altering the behavior of a web page or web application with custom callbacks. These callbacks may be maintained, modified, and managed by third-party users and developers who may not necessarily be affiliated with the originating website or application.

You can use webhooks to send signals to TradersPost from your own custom code, or from a system like [TradingView](https://www.tradingview.com/?offer\_id=10\&aff\_id=26514) or [TrendSpider](https://trendspider.com/?\_go=traderspost). A webhook receives data in the JSON format. JSON is an open standard format, and data interchange format, that uses human-readable text to store and transmit data between systems.

Here is an example of what the JSON would look like for **AMD** to **buy** 5 shares at a price of **$85.50** with a take profit and stop loss**.**

```json
{
    "ticker": "AMD",
    "action": "buy",
    "price": "85.50"
}
```

Sending webhooks is easy! You can send webhooks with any computer that has internet access using widely available tools like [curl](https://curl.se) or programming languages such as [PHP](https://php.net) or [Python](https://www.python.org). Here is an example using [curl](https://curl.se) from the command line.

```bash
$ curl -H 'Content-Type: application/json; charset=utf-8' -d '{"ticker": "AMD", "action": "buy", "price": 85.50}' -X POST https://traderspost.io/trading/webhook/9d9f8620-d60d-416e-827e-0ec01ef93532/9b5b8c4264421f5515fd4fcb6571af50
```

Or if you are a user of TradingView, you can configure an alert to send a webhook with a message like this.

```json
{
    "ticker": "{{ticker}}",
    "action": "buy",
    "price": "{{close}}"
}
```

The values wrapped in **\{{** and **\}}** will be replaced dynamically by TradingView when the alert is sent to the webhook URL. With this, you can use something like the [Trend Following MOMO](https://www.tradingview.com/script/Jrw5Qegy-Trend-Following-MOMO/?offer\_id=10\&aff\_id=26514) strategy by Matt DeLong and place the MOMO trades directly in your broker!

You can learn more about TradersPost webhooks [here](core-concepts/webhooks.md).

{% hint style="info" %}
You can also send webhooks to TradersPost from custom code using programming languages like [PHP](https://php.net) or [Python](https://www.python.org). You can see some custom custom code examples for various programming languages [here](learn/custom-code-examples.md).
{% endhint %}

## Strategies

Strategies are what get connected to a broker with a strategy subscription. Strategies are private by default. Strategy managers can publish their strategies and allow other users to subscribe to them. When a user subscribes to a strategy, the trades will be placed automatically in the broker linked to the subscription.

As a strategy manager, if you don't want to publish your strategy for the public to use, you can keep it as a private subscription.

## Brokers

TradersPost has a "bring your own broker" architecture. We are not a broker or an exchange. We do not hold your money and you are required to connect an existing brokerage to TradersPost in order to use the functionality. We have integrations with the following brokers.

* [Alpaca](broken-reference) - API for Stock Trading - Trade with algorithms, connect with apps, build services — all with commission-free stock trading API
* [TD Ameritrade](broken-reference) - TD Ameritrade is a broker that offers an electronic trading platform for the trade of financial assets.
* [TradeStation](broken-reference) - TradeStation offers state-of-the-art trading technology and online electronic brokerage services to active individual and institutional traders in the U.S. and worldwide.
* [Tradier](broken-reference) - Tradier provides a full range of services in a scalable, secure, and easy-to-use REST-based API for businesses and individual developers. It’s unlike anything you’ve seen before.
* [Robinhood](broken-reference) - Robinhood is a free-trading app that lets investors trade stocks, options, exchange-traded funds and cryptocurrency without paying commissions or fees.

Don't see your broker listed here? Email [support@traderspost.io](mailto:support@traderspost.io) if you would like to see support for your broker added to TradersPost.

## Strategy Subscriptions

A strategy subscription is how a user connects a strategy to a broker. Any signal associated with a strategy will create a new trade for the strategy subscription and allow you to either auto submit the trade to your broker or get an email to review the trade before approving or rejecting.

Before the trade is placed in the connected broker, it is passed through the TradersPost order and risk management system which gives you the ability to fine tune your entry, position size, take profit and stop loss.

#### What happens when you get a subscription trade?

1. **Cancel Open Orders** - Open orders for the ticker will be canceled if one of the following is true
   * There is no open position for the ticker.
   * There is an open position and it is on the opposite side of the signal. For example you have an open long stocks position and you receive an `action=sell` signal. Any take profit or stop loss sell orders will be canceled before exiting the long stocks position.
   * The signal is an explicit cancel signal where `action=cancel`.
2. **Exit Current Position** - Any open position for the ticker in the signal will be exited based on the configuration details in your subscription. For example, if you have a long stocks position open for AMD and you get an `action=sell` signal, the long position will be closed with a sell order.
3. **Enter New Position** - A new position will be entered with an order based on the configuration details in your subscription.

**Ready to get started?** [Register](https://traderspost.io/register) your free account today!
