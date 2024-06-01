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

The TradersPost + Tradovate integration currently does not support market data so we are not able to fetch quotes. This means we have the following limitations:

### Limit orders without a price in the signal

This means you are required to send a price in your signal since we aren't able to fetch quotes. In the following example, since we are entering with a market order and we don't know what price you will be filled at, we will use the `signalPrice` to calculate the limit order limit price of `$18600`.

{% hint style="warning" %}
If limit orders are configured and the signal does not have a price, then a market order will be submitted.
{% endhint %}

```json
{
    "ticker": "MNQ",
    "action": "buy",
    "orderType": "market",
    "signalPrice": 18500,
    "takeProfit": {
        "amount": 100
    }
}
```

And if you are using limit orders, then the entry limit price will be used to calculate the take profit limit price. In this example, a take profit limit order will be calculated with a limit price of `$18600`.

```json
{
    "ticker": "MNQ",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": 18500,
    "takeProfit": {
        "amount": 100
    }
}
```

### No Profit & Loss or current price data on open positions.

Since we aren't able to use your market data or fetch quotes, we aren't able to show open position P\&L.
