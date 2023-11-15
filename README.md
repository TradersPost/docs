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

TradersPost is made of the following core concepts. You can use them together to create automated trading strategies in your broker and allow other people to subscribe to your strategies.

* [Brokers](./#brokers) - Bring your own broker by connecting it to TradersPost. We support several brokers like **TD Ameritrade**, **Alpaca** and **TradeStation**.
* [Webhooks](./#webhooks) - Webhooks are buy or sell signals that can be produced by an automated algorithm or even a manual human trader.
* [Strategies](./#strategies) - Strategies are what get connected to a broker. Users can subscribe to strategies and have the webhook signals place trades directly in their broker.
* [Subscriptions](./#subscriptions) - Subscriptions allow you to connect a strategy to a broker, define your risk tolerance and position sizing.

If you prefer to watch a video demo of TradersPost to get a high level overview, this video is for you. If not, feel free to continue reading to get a high level overview.

{% embed url="https://www.youtube.com/watch?v=AWSImgUtw98" %}
Watch a demo of TradersPost if you prefer a video.
{% endembed %}

## Brokers

TradersPost has a "bring your own broker" architecture. We are not a broker or an exchange. We do not hold your money and you are required to connect an existing brokerage to TradersPost in order to use the functionality. We have integrations with the following brokers.

* [TradeStation](core-concepts/brokers/tradestation.md)
* [Alpaca](core-concepts/brokers/alpaca.md)
* [Interactive Brokers](core-concepts/brokers/interactive-brokers.md)
* [Tradier](core-concepts/brokers/tradier.md)
* [TD Ameritrade](core-concepts/brokers/tdameritrade.md)
* [Coinbase](core-concepts/brokers/coinbase.md)
* [Robinhood](core-concepts/brokers/robinhood.md)

Don't see your broker listed here? Check our full list of [supported brokers](https://traderspost.io/brokers) and our [broker roadmap](core-concepts/brokers/broker-roadmap/).

## Webhooks

Webhooks are signals that contain buy and sell instructions that can be produced by an automated algorithm or even a manual human trader. Signals are sent to TradersPost via webhooks using JSON.

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

You can learn more about webhooks [here](core-concepts/webhooks.md).

{% hint style="info" %}
You can also send webhooks to TradersPost from custom code using programming languages like [PHP](https://php.net) or [Python](https://www.python.org). You can see some custom custom code examples for various programming languages [here](learn/custom-code-examples.md).
{% endhint %}

## Strategies

Strategies are what you connect to a broker in TradersPost. They are linked to a webhook and you can subscribe to a strategy to connect it to your broker. Strategies are private by default. Strategy managers can publish their strategies or individual control which users have access to the strategy. When a user subscribes to a strategy, the trades will be placed automatically in the broker linked to the subscription.

You can learn more about strategies [here](core-concepts/strategies.md).

## Subscriptions

A strategy subscription is how a user connects a strategy to a broker. Any signal associated with a strategy will create a new trade for the strategy subscription and allow you to either auto submit the trade to your broker or get an email to review the trade before approving or rejecting.

You can learn more about subscriptions [here](core-concepts/subscriptions.md).

## Supported Asset Classes

* Stocks
* Futures
* Options
* Crypto

## Get Started

Ready to get started? [Register](https://traderspost.io/register) your free account today and head over to the [Getting Started](getting-started.md) tutorial.
