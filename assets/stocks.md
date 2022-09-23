---
description: >-
  TradersPost supports buying, selling and shorting US Equities and Index ETFs
  through the following brokers.
---

# Stocks

{% embed url="https://www.youtube.com/watch?v=tJcY7M_YCmU" %}
TradersPost Automated Stocks Trading Setup
{% endembed %}

## Signals

It's easy to send signals to TradersPost using [Webhooks](../webhooks.md) from platforms like [TradingView](../tradingview/) or [TrendSpider](../trend-spider.md). You just need to send JSON like the following to the webhook URL you create within TradersPost.

### Enter Bullish

The **buy** action is a bullish signal. When TradersPost receives a buy signal, we will **Buy To Cover** any bearish (short) position for the ticker and **Buy To Open** a bullish (long).

```json
{
    "ticker": "SQ",
    "action": "buy"
}
```

### Exit Bullish

The **exit** action will exit any open position. So for example if you have a long shares position open, then TradersPost will **Sell To Close** those long shares.

```json
{
    "ticker": "SQ",
    "action": "exit"
}
```

### Enter Bearish

The **sell** action is a bearish signal. When TradersPost receives a sell signal, we will **Sell To Close** any bullish (long) position for the ticker and **Sell To Open** a bearish (short) position.

```json
{
    "ticker": "SQ",
    "action": "sell"
}
```

### Exit Bearish

The **exit** action will exit any open position. So for example if you have a short shares position open, then TradersPost will **Buy to Cover** those short shares.

```json
{
    "ticker": "SQ",
    "action": "exit"
}
```

### Full Signal Example

You can optionally include a **price** and **quantity** in the signal that can then be used in the calculated orders that we send to your broker. Here is a full example signal.

```json
{
    "ticker": "SQ",
    "action": "buy",
    "price": 108.88,
    "quantity": 100
}
```

If you configure your strategy subscription to use limit orders and to use the signal quantity, then you will get a **Buy Limit** order for **100** shares at a price of **$108.88**.
