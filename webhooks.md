---
description: >-
  TradersPost allows third party applications like TradingView and TrendSpider
  to integrate with your connected brokers via webhooks. What are webhooks?
---

# Webhooks

> Webhooks are automated messages sent from applications when something happens. They have a message that can contain a payload of data and are sent to a unique URL.

TradersPost requires a minimum amount of information in a webhook. Here is an example where we **buy** AMD at **85.50**.

```json
{
    "ticker": "AMD",
    "action": "buy",
    "price": "85.50",
    "quantity": 5
}
```

* **ticker** - The ticker symbol name. Example **AMD** (required)
* **action** - The signal action. Supported values are **buy** and **sell** (required)
* **price** - The price of the buy or sell action. If you omit this value, the signal defaults to a market order (optional)
* **quantity** - The quantity to enter. If you omit this value, the quantity will be dynamically calculated or defaulted to 1. This only works with entry orders and not exit orders. (optional)

You can send webhooks to TradersPost in a few different ways.

## Third Parties

You can send webhooks to TradersPost from third party tools like [TradingView](https://tradingview.com/?offer\_id=10\&aff\_id=26514) and [TrendSpider](https://trendspider.com/?\_go=traderspost). Read more about how to do this with TradingView [here](https://traderspost.io/docs/trading-view).

## Custom Code

In addition to sending webhooks from third parties, you can send webhooks to TradersPost from custom code using programming languages like [PHP](https://php.net) or [Python](https://www.python.org). Here is an example using [PHP](https://php.net) and the [Symfony HTTP Client](https://symfony.com/doc/current/http\_client.html).

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
{"success":true,"id":"cd481b19-9bb7-4845-8227-523203971d47","payload":{"ticker":"AMD","action":"buy","price":85.50}}
```

This is a simple example, but you can combine this with a service like [Polygon.io](https://polygon.io) to get live real-time market data and build your own completely custom trading strategies and TradersPost can handle the integrations with your broker.

If you are interested building your own custom automated trading strategies, give TradersPost a try and [Register](https://traderspost.io/register) your free account today! If you have any questions, join our [Community](https://traderspost.io/community) or email us at [support@traderspost.io](mailto:support@traderspost.io).
