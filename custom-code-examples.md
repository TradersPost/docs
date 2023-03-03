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

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

class Program
{
    static async Task Main(String[] args)
    {
        using var client = new HttpClient();

        var json = @"{\"ticker\": \"AMD"", \"action\": \"buy\", \"price\": 85.50}";

        using var content = new StringContent(json, System.Text.Encoding.UTF8, "application/json");

        using var response = client.PostAsync("https://traderspost.io/trading/webhook/8c9d9620-c50d-416e-926e-0ec01ee83522/a353c3e16f9e3ded7c58cfedd2c38d74", content);

        string responseBody = response.Content.ReadAsStringAsync();

        Console.WriteLine(responseBody);
    }
}
```

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
