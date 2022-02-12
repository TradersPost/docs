---
description: >-
  TradersPost supports buying, selling and shorting US Equities and Index ETFs
  through the following brokers.
---

# Stocks

## Supported Brokers

| Broker        | Live | Paper | Fractional | Shorting |
| ------------- | ---- | ----- | ---------- | -------- |
| Alpaca        | Yes  | Yes   | Yes        | Yes      |
| TD Ameritrade | Yes  | No    | No         | Yes      |
| TradeStation  | Yes  | Yes   | No         | Yes      |
| Robinhood     | Yes  | No    | Yes        | No       |
| TradersPost   | No   | Yes   | Yes        | Yes      |

## Signals

It's easy to send signals to TradersPost using [Webhooks](../webhooks.md) from platforms like [TradingView](../tradingview.md) or [TrendSpider](../trend-spider.md). You just need to send JSON like the following to the webhook URL you create within TradersPost.

### Enter Bullish

```json
{
    "ticker": "SQ",
    "action": "buy"
}
```

### Exit Bullish

```json
{
    "ticker": "SQ",
    "action": "exit"
}
```

### Enter Bearish

```json
{
    "ticker": "SQ",
    "action": "sell"
}
```

### Exit Bearish

```json
{
    "ticker": "SQ",
    "action": "exit"
}
```
