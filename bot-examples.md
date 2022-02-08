---
description: >-
  The examples in this document intend to demonstrate how you can send signals
  to TradersPost from custom programming languages like PHP, Python, etc.
---

# Custom Code Examples

## PHP

```bash
composer require symfony/http-client
```

```php
<?php

require 'vendor/autoload.php';

use Symfony\Component\HttpClient\HttpClient;

$webhookUrl = 'paste your webhook url';

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
    'paste your webhook url',
    json={"ticker": "AMD", "action": "buy", "price": 85.50}
)

print(r.json())

```

## Ruby

```ruby
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse("paste your webhook url")

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

If you are interested building your own custom automated trading strategies, give TradersPost a try and [Register](https://traderspost.io/register) your free account today! If you have any questions, join our [Community](https://traderspost.io/community) or email us at [support@traderspost.io](mailto:support@traderspost.io).
