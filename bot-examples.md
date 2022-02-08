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

## Python

```python
import requests

r = requests.post(
    'https://traderspost.io/trading/webhook/befc2575-b969-4022-b838-aebbf0873956/a1b8209cfe8e8c7342aeea7fc1319b6a',
    json={"ticker": "AMD", "action": "buy", "price": 85.50}
)

print(r.json())

```

If you are interested building your own custom automated trading strategies, give TradersPost a try and [Register](https://traderspost.io/register) your free account today! If you have any questions, join our [Community](https://traderspost.io/community) or email us at [support@traderspost.io](mailto:support@traderspost.io).
