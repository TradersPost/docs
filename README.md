---
description: >-
  Welcome to TradersPost! Get started with TradersPost by familiarizing yourself
  with how the platform works.
cover: .gitbook/assets/TradersPost Banner
coverY: 0
---

# Introduction

{% embed url="https://www.youtube.com/watch?v=AWSImgUtw98" %}
Watch this video for a full demo of the platform and how to get started!
{% endembed %}

## What is TradersPost?

TradersPost is a trading tool that can automate your TrendSpider or TradingView strategies in stock brokers like TD Ameritrade, TradeStation and Alpaca.

## Who is TradersPost for?

* **Strategy Managers** - a person that is interested in creating automated trading strategies and connecting them to their broker.
* **Traders and Investors** - a person that is interested in connecting automated trading strategies to their broker without any coding knowledge.

## How does it work?

TradersPost is made of the following concepts. You can use them together to create automated trading strategies in your broker and allow other people to subscribe to your strategies.

* [Signals](./#signals) - Signals are buy or sell signal that can be produced by an automated algorithm or even a manual human trader.
* [Strategies](./#strategies) - Strategies define a group of signals. Users can subscribe to strategies and have the signals place trades directly in their broker.
* [Brokers](./#brokers) - Bring your own broker by connecting it to TradersPost. We support several brokers like **TD Ameritrade**, **Alpaca** and **TradeStation**.
* [Subscriptions](./#subscriptions) - Subscriptions allow you to connect a strategy to a broker, define your risk tolerance and position sizing.

## Signals

Signals are buy or sell instructions that can be produced by an automated algorithm or even a manual human trader. They require the following minimum information.

* **ticker** - The ticker symbol name. Example **AMD** (required)
* **action** - The signal action. (required)
* **price** - The price of the buy or sell action. If you omit this value, the signal defaults to a market order (optional)

Signals can be sent to TradersPost via [Webhooks](https://traderspost.io/docs#webhooks). A webhook is a signal sent from custom code or a 3rd party system like [TradingView.com](https://www.tradingview.com/?offer\_id=10\&aff\_id=26514).

### Supported Actions

* **buy** - open a new long position and/or exit a short position
* **sell** - exit a long position and/or open a new short position
* **exit** - exit open position if one exists
* **cancel** - cancel open orders if they exist
* **add** - add to open position if one exists

The **buy** and **sell** actions will only open a position on the opposite side after exiting the open position if the strategy subscription has BOTH sides enabled.

### Webhooks

> A webhook in web development is a method of augmenting or altering the behavior of a web page or web application with custom callbacks. These callbacks may be maintained, modified, and managed by third-party users and developers who may not necessarily be affiliated with the originating website or application.

You can use webhooks to send signals to TradersPost from your own custom code, or from a system like [TradingView](https://www.tradingview.com/?offer\_id=10\&aff\_id=26514) or [TrendSpider](https://trendspider.com/?\_go=traderspost). A webhook receives data in the JSON format. JSON is an open standard format, and data interchange format, that uses human-readable text to store and transmit data between systems.

Here is an example of what the JSON would look for a webhook signal for **AMD** to **buy** at a price of **$85.50**.

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

The values wrapped in **{{** and **}}** will be replaced dynamically by TradingView when the alert is sent to the webhook URL. With this, you can use something like the [Trend Following MOMO](https://www.tradingview.com/script/Jrw5Qegy-Trend-Following-MOMO/?offer\_id=10\&aff\_id=26514) strategy by Matt DeLong and place the MOMO trades directly in your broker!

### **Custom Code**

You can send webhooks to TradersPost from custom code using programming languages like [PHP](https://php.net) or [Python](https://www.python.org). Here is an example using [PHP](https://php.net) and the [Symfony HTTP Client](https://symfony.com/doc/current/http\_client.html).

```
$ composer require symfony/http-client
```

```php
<?php
// traderspost-test.php

require 'vendor/autoload.php';

use Symfony\Component\HttpClient\HttpClient;

$webhookUrl = 'https://traderspost.io/trading/webhook/9d9f8620-d60d-416e-827e-0ec01ef93532/9b5b8c4264421f5515fd4fcb6571af50';

$client = HttpClient::create();

$response = $client->request('POST', $webhookUrl, [
    'json' => [
        'ticker' => 'AMD',
        'action' => 'buy',
        'price' => 85.50,
    ]
]);

echo $response->getContent();
```

```
$ php traderspost-test.php
```

## Strategies

Strategies define a group of signals. Strategies are private by default. Strategy managers can publish their strategies and allow other users to subscribe to them. When a user subscribes to a strategy, the trades will be placed automatically in the broker linked to the subscription.

As a strategy manager, if you don't want to publish your strategy for the public to use, you can keep it as a private subscription.

## Brokers

TradersPost has a "bring your own broker" architecture. We are not a broker or an exchange. We do not hold your money and you are required to connect an existing brokerage to TradersPost in order to use the functionality. We have integrations with the following brokers.

* [Alpaca](https://alpaca.markets) - API for Stock Trading - Trade with algorithms, connect with apps, build services — all with commission-free stock trading API
* [TD Ameritrade](https://www.tdameritrade.com) - TD Ameritrade is a broker that offers an electronic trading platform for the trade of financial assets.
* [TradeStation](https://tradestation.com) - TradeStation offers state-of-the-art trading technology and online electronic brokerage services to active individual and institutional traders in the U.S. and worldwide.
* [Robinhood](https://robinhood.com) - Robinhood is a free-trading app that lets investors trade stocks, options, exchange-traded funds and cryptocurrency without paying commissions or fees.

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
