---
description: >-
  TradersPost allows third party applications like TradingView and TrendSpider
  to integrate with your connected brokers via webhooks.
---

# Webhooks

## What is a webhook?

Webhooks are automated messages sent from applications when something happens. They have a message that can contain a payload of data and are sent to a unique URL.

In the context of automated trading, the webhook message contains all the information about the trade signal like what ticker to buy and at what price.

## Required Fields

TradersPost requires a minimum required amount of fields in a webhook in order to function. You are required to send at a minimum the **ticker** and an **action**. Here is an example where we send a signal to buy AMD.

```json
{
    "ticker": "AMD",
    "action": "buy"
}
```

## Supported Fields

* **ticker** - The ticker symbol name. Example **AMD** (required)
* **action** - The signal action. Supported values are **buy,** **sell, exit, cancel or add** (required)
  * **buy** - Exit bearish position and optionally open bullish position
  * **sell** - Exit bullish position and optionally open bearish position
  * **exit** - Exit open position without entering a new position on the other side.
  * **cancel** - Cancel open orders
  * **add** - Add to existing open position
* **sentiment** - The sentiment of the position you should be in after a trade is executed (optional)
  * **bullish** - Open position after trade is executed should be bullish or flat.
  * **bearish** - Open position after trade is executed should be bearish or flat.
  * **flat** - No position should be open after trade is executed.
* **price** - The price of the buy or sell action. If you omit this value, the current market price will be used when the trade is executed (optional)
* **quantity** - The quantity to enter. If you omit this value, the quantity will be dynamically calculated or defaulted to 1. (optional)

## Examples

#### Enter Bullish

```json
{
    "ticker": "SQ",
    "action": "buy"
}
```

#### Exit Bullish

```json
{
    "ticker": "SQ",
    "action": "exit"
}
```

You can also use the sentiment field to exit a bullish position without entering a bearish position on the other side.

```json
{
    "ticker": "SQ",
    "action": "sell",
    "sentiment": "flat"
}
```

#### Enter Bearish

```json
{
    "ticker": "SQ",
    "action": "sell"
}
```

#### Exit Bearish

```json
{
    "ticker": "SQ",
    "action": "exit"
}
```

You can also use the sentiment field to exit a bearish position without entering a bullish position on the other side.

```json
{
    "ticker": "SQ",
    "action": "buy",
    "sentiment": "flat"
}
```

#### Cancel Open Orders

```json
{
    "ticker": "SQ",
    "action": "cancel"
}
```

#### Add to Open Position

```json
{
    "ticker": "SQ",
    "action": "add"
}
```

#### Signal Quantity

{% hint style="info" %}
The signal quantity will only be used if you check **Use signal quantity** in the strategy subscription settings in TradersPost.
{% endhint %}

```json
{
    "ticker": "SQ",
    "action": "buy",
    "quantity": 5
}
```

#### Signal Price

{% hint style="info" %}
The signal price is optional. If you omit a price from the signal, the current market price will be used if you have limit orders configured.
{% endhint %}

```json
{
    "ticker": "SQ",
    "action": "buy",
    "price": 60.30
}
```

## Third Parties

Because TradersPost works using standard webhooks, this enables users to integrate with third party platforms that support sending alerts as webhooks.

Here are some popular platforms that enable you to build strategies and send alerts as webhooks.

* [TradingView](tradingview.md) - TradingView is a social network of 30 million traders and investors using the world's best charts and tools to spot trading opportunities across global markets.
* [TrendSpider](trend-spider.md) - TrendSpider provides technical analysis software for retail traders and investors focused on the US equity and foreign exchange markets.

## Custom Code

In addition to sending webhooks from third parties, you can send webhooks to TradersPost from custom code using programming languages like [PHP](https://php.net) or [Python](https://www.python.org). Here is an example using [PHP](https://php.net) and the [Symfony HTTP Client](https://symfony.com/doc/current/http\_client.html).

This example uses [PHP](https://www.php.net/) and the [Composer](https://getcomposer.org/) package manager. First create a new directory to work inside of.

```bash
mkdir traderspost
cd traderspost
```

Now require the `symfony/http-client` package using composer.

```
composer require symfony/http-client
```

Now you are ready to create a file named `traderspost-test.php` and paste the following code inside of the file.

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

Now you are ready to send the webhook to TradersPost!

```bash
php traderspost-test.php
{"success":true,"id":"cd481b19-9bb7-4845-8227-523203971d47","payload":{"ticker":"AMD","action":"buy","price":85.50}}
```

This is a simple example, but you can combine this with a service like [Polygon.io](https://polygon.io) to get live real-time market data and build your own completely custom trading strategies and TradersPost can handle the integrations with your broker.

If you are interested building your own custom automated trading strategies, give TradersPost a try and [Register](https://traderspost.io/register) your free account today! If you have any questions, join our [Community](https://traderspost.io/community) or email us at [support@traderspost.io](mailto:support@traderspost.io).
