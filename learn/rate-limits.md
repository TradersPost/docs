# Rate Limits

TradersPost is **NOT** designed to be a high frequency trading platform. The minimum allowed timeframe to trade on is the 1 minute chart.

{% hint style="warning" %}
If you setup a strategy on anything less than the 1 minute chart or repeatedly violate the below rate limits, your account may be temporarily suspended or permanently banned if the issue is not addressed.
{% endhint %}

To ensure fair access and system integrity, please adhere to the following rate limits when using TradersPost webhooks:

| Interval | Allowed Requests |
| -------- | ---------------- |
| 1 Minute | 60               |
| 1 Hour   | 500              |

**When a webhook URL is rate-limited by TradersPost**, it means the endpoint has received too many requests in a short time and has triggered a protective threshold. As a result, any additional requests to that webhook URL (from TradersPost) will receive an HTTP **429 Too Many Requests** status code in the response and the response body will contain JSON that looks like the following.

```json
{
    "success": false,
    "messageCode": "too-many-requests",
    "message": "Too Many Requests"
}
```

Exceeding these limits may result in temporary suspension or banning. Always monitor your strategies and the amount of webhooks being sent to TradersPost to prevent violations. If you have any questions about our rate limits, please contact us at [support@traderspost.io](mailto:support@traderspost.io).

### Broker Rate Limits

Brokers implement rate limits to ensure fair usage and system stability, alongside any limitations from TradersPost. These rules control request frequency to prevent overload and maintain responsiveness, providing equitable access for users. Understanding these policies is vital for optimizing trading system communication and preventing rejected requests due to

| **Broker** | **Rate Limit** | **Reference / Notes** |
| ---------- | -------------- | --------------------- |

| **Alpaca** | 200 requests per minute | [Alpaca Docs](https://alpaca.markets/deprecated/docs/api-documentation/api-v2/#rate-limit) |
| ---------- | ----------------------- | ------------------------------------------------------------------------------------------ |

| **TradeStation** | Not strictly published as a single number; historically \~10 requests/second in many endpoints | <p><a href="https://api.tradestation.com/docs/fundamentals/rate-limiting/">TradeStation Docs</a><br>TradeStation dynamically applies rate limits. Exceeding limits typically returns <code>429 Too Many Requests</code>.</p> |
| ---------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| **Tradier** | 120 requests per minute (Basic); higher limits may apply for advanced/premium accounts | [Tradier Docs](https://documentation.tradier.com/brokerage-api/overview/rate-limiting) |
| ----------- | -------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |

| **Robinhood** | No explicit public number; unofficial sources suggest \~1 call/second and/or a broader per-minute limit | <p><a href="https://docs.robinhood.com/crypto/trading/#section/Pagination">Robinhood Docs</a><br>Official docs do not provide a hard numeric rate limit; behavior may vary across endpoints.</p> |
| ------------- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

| **Tradovate** | Enforced by a penalty system if you exceed short-term thresholds (e.g., \~10 requests/second) | <p><a href="https://api.tradovate.com/#tag/Access/Request-Rate-Limits-And-Time-Penalty">Tradovate Docs</a><br>Rate limits are enforced with increasing time penalties if exceeded.</p> |
| ------------- | --------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| **Coinbase** | Varies by endpoint; for Advanced Trade API, typically \~10 requests/second for private endpoints | <p><a href="https://docs.cdp.coinbase.com/advanced-trade/docs/rest-api-rate-limits/">Coinbase Docs</a><br>Public endpoints and private endpoints often have different limits and “burst” rules.</p> |
| ------------ | ------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| **E\*TRADE** | Not publicly documented | No official rate-limit statement available. |
| ------------ | ----------------------- | ------------------------------------------- |

| **Bybit** | Varies by API category (Spot, Futures, etc.); commonly cited \~50 requests/second in certain unified endpoints | <p><a href="https://bybit-exchange.github.io/docs/v5/rate-limit">Bybit Docs</a><br>Rate limits differ depending on the endpoint type and “IP or account” categories.</p> |
| --------- | -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

| **Kraken** | Varies; for Spot REST API, often \~15 calls in a 3-second window (i.e., \~5 calls/second) | <p><a href="https://docs.kraken.com/api/docs/guides/spot-ratelimits/">Kraken Docs</a><br>Additional tiers and advanced order endpoints may have different rules.</p> |
| ---------- | ----------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| **Binance** | Uses “request weight” system (e.g., 1,200 weight per minute on many Spot endpoints) | <p><a href="https://www.binance.com/en/support/faq/frequently-asked-questions-on-api-360004492232">Binance Docs</a><br>Different endpoints consume different “weights.” Exceeding leads to 429 errors.</p> |
| ----------- | ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| **IBKR** | Multiple “pacing violation” rules (e.g., \~50 messages/5 seconds), rather than a simple requests/minute threshold | <p><a href="https://www.interactivebrokers.com/campus/ibkr-api-page/webapi-doc/#pacing-limitations-10">IBKR Docs</a><br>Rules vary between TWS API vs. Client Portal API. Exceeding triggers “pacing violation” lockouts.</p> |
| -------- | ----------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### Important Notes

1. **Dynamic / Tiered Limits**\
   Some brokers apply multiple tiers or dynamic rules depending on the type of account, the specific endpoint (e.g., market data vs. trade placement), or your trading volume. Always confirm in the official documentation or by contacting the broker’s support.
2. **“Burst” vs. “Sustained” Rate**\
   Even when a broker provides a requests-per-minute limit, there may be a secondary per-second or per-burst threshold that can trigger errors if exceeded in short bursts.
3. **Penalties / Lockouts**\
   Many brokers return HTTP status code 429 (`Too Many Requests`) if you exceed the limit, and some impose temporary lockouts (“cool-down” periods) or progressively longer penalties for repeated excesses.
