---
description: >-
  The examples in this document intend to demonstrate how you can send signals
  to TradersPost from custom programming languages like PHP, Python, etc.
---

# Custom Code Examples

## Custom Code

In addition to sending webhooks from third parties, you can send webhooks to TradersPost from custom code using programming languages like [PHP](https://php.net) or [Python](https://www.python.org). Here is an example using [PHP](https://php.net) and the [Symfony HTTP Client](https://symfony.com/doc/current/http_client.html).

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

## cURL

```bash
curl -H 'Content-Type: application/json; charset=utf-8' \
-d '{"ticker": "AMD", "action": "buy", "price": 85.50}' \
-X POST https://webhooks.traderspost.io/trading/webhook/8c9d9620-c50d-416e-926e-0ec01ee83522/a353c3e16f9e3ded7c58cfedd2c38d74
```

## PHP

```bash
composer require symfony/http-client
```

```php
<?php

require 'vendor/autoload.php';

use Symfony\Component\HttpClient\HttpClient;

$webhookUrl = 'https://webhooks.traderspost.io/trading/webhook/8c9d9620-c50d-416e-926e-0ec01ee83522/a353c3e16f9e3ded7c58cfedd2c38d74';

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
    'https://webhooks.traderspost.io/trading/webhook/8c9d9620-c50d-416e-926e-0ec01ee83522/a353c3e16f9e3ded7c58cfedd2c38d74',
    json={"ticker": "AMD", "action": "buy", "price": 85.50}
)

print(r.json())

```

## Ruby

```ruby
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse('https://webhooks.traderspost.io/trading/webhook/8c9d9620-c50d-416e-926e-0ec01ee83522/a353c3e16f9e3ded7c58cfedd2c38d74')

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

## JavaScript

```javascript
fetch('https://webhooks.traderspost.io/trading/webhook/8c9d9620-c50d-416e-926e-0ec01ee83522/a353c3e16f9e3ded7c58cfedd2c38d74', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        ticker: 'AMD',
        action: 'buy',
        price: 85.50
    })
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error(error));
```

## Go

```go
package main

import (
	"bytes"
	"encoding/json"
	"fmt"
	"net/http"
)

func main() {
	url := "https://webhooks.traderspost.io/trading/webhook/8c9d9620-c50d-416e-926e-0ec01ee83522/a353c3e16f9e3ded7c58cfedd2c38d74"
	data := map[string]interface{}{
		"ticker": "AMD",
		"action": "buy",
		"price":  85.50,
	}

	jsonData, err := json.Marshal(data)
	if err != nil {
		panic(err)
	}

	req, err := http.NewRequest("POST", url, bytes.NewBuffer(jsonData))
	if err != nil {
		panic(err)
	}
	req.Header.Set("Content-Type", "application/json")

	client := &http.Client{}
	resp, err := client.Do(req)
	if err != nil {
		panic(err)
	}
	defer resp.Body.Close()

	var result map[string]interface{}
	err = json.NewDecoder(resp.Body).Decode(&result)
	if err != nil {
		panic(err)
	}

	fmt.Println(result)
}
```

## C++

```cpp
#include <iostream>
#include <curl/curl.h>

int main() {
    CURL *curl;
    CURLcode res;

    curl_global_init(CURL_GLOBAL_ALL);

    curl = curl_easy_init();
    if (curl) {
        curl_easy_setopt(curl, CURLOPT_URL, "https://traderspost.io/trading/webhook/8c9d9620-c50d-416e-926e-0ec01ee83522/a353c3e16f9e3ded7c58cfedd2c38d74");

        struct curl_slist *headers = NULL;
        headers = curl_slist_append(headers, "Content-Type: application/json");
        curl_easy_setopt(curl, CURLOPT_HTTPHEADER, headers);

        const char *json_data = "{\"ticker\": \"AMD\", \"action\": \"buy\", \"price\": 85.50}";
        curl_easy_setopt(curl, CURLOPT_POSTFIELDS, json_data);

        res = curl_easy_perform(curl);
        if (res != CURLE_OK) {
            std::cerr << "curl_easy_perform() failed: " << curl_easy_strerror(res) << std::endl;
        }

        curl_easy_cleanup(curl);
    }

    curl_global_cleanup();

    return 0;
}
```

## C\#

<pre class="language-csharp"><code class="lang-csharp"><strong>class Program
</strong>{
    static async Task Main(String[] args)
    {
        var client = new HttpClient();
        client.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

        var json = "{\"ticker\": \"AMD"", \"action\": \"buy\", \"price\": 85.50}";

        var content = new StringContent(json, Encoding.UTF8, "application/json");

        var response = client.PostAsync("https://traderspost.io/trading/webhook/8c9d9620-c50d-416e-926e-0ec01ee83522/a353c3e16f9e3ded7c58cfedd2c38d74", content);

        string responseBody = response.ToString();

        Console.WriteLine(responseBody);
    }
}
</code></pre>

## Java

```java
import java.net.HttpURLConnection;
import java.net.URL;
import java.io.OutputStream;
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class Main {
    public static void main(String[] args) throws Exception {
        URL url = new URL("https://webhooks.traderspost.io/trading/webhook/8c9d9620-c50d-416e-926e-0ec01ee83522/a353c3e16f9e3ded7c58cfedd2c38d74");
        HttpURLConnection con = (HttpURLConnection) url.openConnection();
        con.setRequestMethod("POST");
        con.setRequestProperty("Content-Type", "application/json");

        String jsonInputString = "{\"ticker\": \"AMD\", \"action\": \"buy\", \"price\": 85.50}";

        con.setDoOutput(true);
        OutputStream os = con.getOutputStream();
        byte[] input = jsonInputString.getBytes("utf-8");
        os.write(input, 0, input.length);

        BufferedReader br = new BufferedReader(new InputStreamReader(con.getInputStream(), "utf-8"));
        StringBuilder response = new StringBuilder();
        String responseLine = null;
        while ((responseLine = br.readLine()) != null) {
            response.append(responseLine.trim());
        }
        System.out.println(response.toString());
    }
}
```

Take these examples and combine them with a service like [Polygon](https://polygon.io) or [Alpaca](https://alpaca.markets/data) to get live market data to build your own custom strategies and use TradersPost to manage the integration with your broker.

If you are interested building your own custom automated trading strategies, give TradersPost a try and [Register](https://traderspost.io/register) your free account today! If you have any questions, join our [Community](https://traderspost.io/community) or email us at [support@traderspost.io](mailto:support@traderspost.io).
