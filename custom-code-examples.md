---
description: >-
  The examples in this document intend to demonstrate how you can send signals
  to TradersPost from custom programming languages like PHP, Python, etc.
---

# Custom Code Examples

## cURL

```bash
curl -H 'Content-Type: application/json; charset=utf-8' \
-d '{"ticker": "AMD", "action": "buy", "price": 85.50}' \
-X POST https://traderspost.io/trading/webhook/8c9d9620-c50d-416e-926e-0ec01ee83522/a353c3e16f9e3ded7c58cfedd2c38d74
```

## PHP

```bash
composer require symfony/http-client
```

```php
<?php

require 'vendor/autoload.php';

use Symfony\Component\HttpClient\HttpClient;

$webhookUrl = 'https://traderspost.io/trading/webhook/8c9d9620-c50d-416e-926e-0ec01ee83522/a353c3e16f9e3ded7c58cfedd2c38d74';

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

## Python

```python
import requests

r = requests.post(
    'https://traderspost.io/trading/webhook/8c9d9620-c50d-416e-926e-0ec01ee83522/a353c3e16f9e3ded7c58cfedd2c38d74',
    json={"ticker": "AMD", "action": "buy", "price": 85.50}
)

print(r.json())

```

## Ruby

```ruby
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse('https://traderspost.io/trading/webhook/8c9d9620-c50d-416e-926e-0ec01ee83522/a353c3e16f9e3ded7c58cfedd2c38d74')

header = {'Content-Type': 'text/json'}

signal = {
   ticker: 'AMD',
   action: 'buy',
   price: 85.50
}

http = Net::HTTP.new(uri.host, uri.port)
request = Net::HTTP::Post.new(uri.request_uri, header)
request.body = signal.to_json

response = http.request(request)

puts response.body
```

Take these examples and combine them with a service like [Polygon](https://polygon.io) or [Alpaca](https://alpaca.markets/data) to get live market data to build your own custom strategies and use TradersPost to manage the integration with your broker.

If you are interested building your own custom automated trading strategies, give TradersPost a try and [Register](https://traderspost.io/register) your free account today! If you have any questions, join our [Community](https://traderspost.io/community) or email us at [support@traderspost.io](mailto:support@traderspost.io).
