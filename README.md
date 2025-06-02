---
description: TradersPost is your one-stop solution for automating your trading strategies.
---

# What is TradersPost?

Our mission is simple: to help you transform trade ideas into executed orders, effortlessly. With powerful tools like dynamic take profit and stop loss management, automated position adjustments, and an options contract screener, TradersPost simplifies and optimizes your trading workflow.

We empower traders to automate strategies from platforms like [TradingView](learn/tradingview.md), [TrendSpider](learn/trend-spider.md), [MT5](learn/metatrader-5.md), and custom programmatic approaches. With seamless integrations to brokers such as [TradeStation](core-concepts/brokers/tradestation.md), [Tradier](core-concepts/brokers/tradier.md), [Robinhood](core-concepts/brokers/robinhood.md), [Alpaca](core-concepts/brokers/alpaca.md), and [many more](https://traderspost.io/connections), TradersPost supports trading across Futures, Stocks, Options, and Crypto. Coming in 2025: Forex.

Whether you're fine-tuning risk management or automating entry and exit orders, TradersPost is here to ensure your trading strategy works just as you envision.

Let us handle the automation so you can focus on what really matters: **your trading success.**

## Who is TradersPost for?

* **Strategy Developers** - a person that is interested in creating automated trading strategies and connecting them to their broker.
* **Traders and Investors** - a person that is interested in connecting automated trading strategies to their broker without any coding knowledge.
* **Trading Communities -** a trading community can use TradersPost to send their trading signals to other TradersPost users where trades can be automated or manually approved or rejected.

{% hint style="warning" %}
TradersPost is **NOT** designed to be a high frequency trading platform. The minimum allowed timeframe to trade on is the 1 minute chart. You are allowed to send 60 requests per minute and 500 requests per hour. If you setup a strategy on anything less than the 1 minute chart, your account may be temporarily suspended or permanently banned if the issue is not addressed. Read more about our rate limiting behavior [here](learn/rate-limits.md).
{% endhint %}

## How does it work?

TradersPost is made of the following core concepts. You can use them together to create automated trading strategies in your broker and allow other people to subscribe to your strategies.

* Brokers - Use your own broker by connecting it to TradersPost. See our full list of [available connections here](https://traderspost.io/connections).
* [Webhooks](./#webhooks) - Webhooks are buy or sell signals that can be produced by an automated algorithm or even a manual human trader. They contain JSON messages with the instructions for how your trade should be executed.
* [Strategies](./#strategies) - Strategies are what get connected to a broker. Users can subscribe to strategies and have the webhook signals place trades directly in their broker.
* [Subscriptions](./#subscriptions) - Subscriptions allow you to connect a strategy to a broker, define your risk tolerance and position sizing.

If you prefer to watch a video demo of TradersPost to get a high level overview, this video is for you. If not, feel free to continue reading to get a high level overview.

{% embed url="https://www.youtube.com/watch?v=_q4fLhzRwWg" %}

## Brokers

TradersPost has a "use your own broker" architecture. We are not a broker or an exchange. We do not hold your money and you are required to connect an existing brokerage to TradersPost in order to use the functionality. We have integrations with over a dozen brokers and exchanges. The full list is availble below:

{% embed url="https://traderspost.io/connections" %}

Don't see your broker listed there? Check our [broker roadmap](broken-reference) for upcoming connections add yourself to a waitlist for other brokers listed [under the Coming Soon heading](https://traderspost.io/connections).

## Webhooks

Webhooks are signals that contain buy and sell instructions that can be produced by an automated algorithm or even a manual human trader. Signals are sent to TradersPost via webhooks using JSON.

You can use webhooks to send signals to TradersPost from your own custom code, or from a system like [TradingView](https://www.tradingview.com/?offer_id=10\&aff_id=26514) or [TrendSpider](https://trendspider.com/?_go=traderspost). A webhook receives data in the JSON format. JSON is an open standard format, and data interchange format, that uses human-readable text to store and transmit data between systems.

Here is an example of what the JSON would look like for **AMD** to **buy** 5 shares at a price of **$85.50** with a take profit and stop los&#x73;**.**

```json
{
    "ticker": "AMD",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": "85.50",
    "quantity": 5
}
```

Sending webhooks is easy! If you are a user of TradingView, you can configure an alert to send a webhook with a message like this.

```json
{
    "ticker": "{{ticker}}",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": "{{close}}"
}
```

The values wrapped in **\{{** and **\}}** will be replaced dynamically by TradingView when the alert is sent to the webhook URL. With this, you can use something like the [Trend Following MOMO](https://www.tradingview.com/script/Jrw5Qegy-Trend-Following-MOMO/?offer_id=10\&aff_id=26514) strategy by Matt DeLong and place the MOMO trades directly in your broker!

You can learn more about webhooks [here](core-concepts/webhooks.md).

{% hint style="info" %}
You can also send webhooks to TradersPost from custom code using programming languages like [PHP](https://php.net) or [Python](https://www.python.org). You can see some custom custom code examples for various programming languages [here](learn/custom-code-examples.md).
{% endhint %}

## Strategies

Strategies are what you connect to a broker in TradersPost. They are linked to a webhook and you can subscribe to a strategy to connect it to your broker. Strategies are private by default. Strategy managers can publish their strategies or individual control which users have access to the strategy. When a user subscribes to a strategy, the trades will be placed automatically in the broker linked to the subscription.

You can learn more about strategies [here](core-concepts/strategies.md).

## Subscriptions

A strategy subscription is how a user connects a strategy to a broker. Any signal associated with a strategy will create a new trade for the strategy subscribers and allow you to either auto submit the trade to your broker or get an email to review the trade before approving or rejecting.

You can learn more about subscriptions [here](core-concepts/subscriptions.md).

## Supported Asset Classes

* Stocks
* Futures
* Options
* Crypto

## Get Started

Ready to get started? [Register](https://traderspost.io/register) your free account today and head over to the [Getting Started](getting-started.md) tutorial.
