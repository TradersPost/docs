---
description: >-
  Tradovate is a popular broker for trading futures due to their competitive
  margin requirements. Build automated trading strategies using TradersPost on
  top of your Tradovate account.
---

# Tradovate

{% hint style="warning" %}
The Tradovate integration is generally available for all TradersPost customers. Please remember that this integration is in <mark style="color:orange;">**BETA**</mark> and you may experience issues that we have not discovered yet. It is recommended to test with a paper account first. If you have any issues or questions, please email us at [support@traderspost.io](mailto:support@traderspost.io)
{% endhint %}

## Contact Information

Email: [support@tradovate.com](mailto:support@tradovate.com)

Phone: [+1 (844) 283-3100](tel:18442833100)

## Reliability

Tradovate is a new broker integration for TradersPost, but generally it has been stable so far.

## Supported Asset Classes

* Futures

## Limitations

The Tradovate integration comes with a few limitations compared to other integrations. These limitations may change in the future as we are able to improve the integration.

The TradersPost + Tradovate integration currently does not have quotes/market data. This may change in the future if we are able to implement market data. Without market data, we aren't able to implement the following features:

* Limit orders without a price in the signal. If limit orders are configured and the signal does not have a price, then a market order will be submitted.
* No trailing stop functionality.
* No Profit & Loss or current price data on open positions.
