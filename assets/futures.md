---
description: >-
  TradersPost supports buying, selling and shorting futures contracts for the
  NQ, MNQ, ES and MES tickers in TradeStation.
---

# Futures

{% hint style="info" %}
**Coming Soon!** Futures trading is currently only available for paper trading. If you would like to apply to be a part of the futures beta, email [support@traderspost.io](mailto:support@traderspost.io).
{% endhint %}

## Supported Symbols

TradersPost currently only supports trading with the following tickers. We plan to continually add more support for other tickers in the future.

| Symbol | Description                     | Exchange |
| ------ | ------------------------------- | -------- |
| NQ     | E-Mini Nasdaq 100 Future        | CME      |
| MNQ    | Micro E-Mini Nasdaq-100 Futures | CME      |
| ES     | E-Mini S\&P 500 Futures         | CME      |
| MES    | Micro E-Mini S\&P 500 Futures   | CME      |

If you would like to see other futures tickers supported, please email [support@traderspost.io](mailto:support@traderspost.io).

{% hint style="info" %}
**Futures contracts expire on the 3rd Friday of the expiration month.** It is your responsibility to ensure positions are exited before expiration or are rolled over manually.
{% endhint %}

## Symbol Format

TradersPost understands many different futures symbol formats. Since every broker and trading platform has subtle differences in the format we try to be as flexible as possible.

| Symbol  | Type                         |
| ------- | ---------------------------- |
| NQZ21   | 2 digit year (TradeStation)  |
| NQZ2021 | 4 digit year (TradersPost)   |
| NQ1!    | TradingView current contract |
| NQ2!    | TradingView next contract    |
| NQ\*0   | TrendSpider current contract |
| NQ\*1   | TrendSpider next contract    |

## Signals

It's easy to send signals to TradersPost using [Webhooks](../webhooks.md) from platforms like [TradingView](../tradingview.md) or [TrendSpider](../trend-spider.md). You just need to send JSON like the following to the webhook URL you create within TradersPost.

### Enter Bullish

The **buy** action is a bullish signal. When TradersPost receives a buy signal, we will **Buy To Cover** any bearish (short) position for the ticker and **Buy To Open** a bullish (long).

```json
{
    "ticker": "NQH2022",
    "action": "buy"
}
```

### Exit Bullish

The **exit** action will exit any open position. So for example if you have a long shares position open, then TradersPost will **Sell To Close** those long contracts.

```json
{
    "ticker": "NQH2022",
    "action": "exit"
}
```

### Enter Bearish

The **sell** action is a bearish signal. When TradersPost receives a sell signal, we will **Sell To Close** any bullish (long) position for the ticker and **Sell To Open** a bearish (short) position.

```json
{
    "ticker": "NQH2022",
    "action": "sell"
}
```

### Exit Bearish

The **exit** action will exit any open position. So for example if you have a short contracts position open, then TradersPost will **Buy to Cover** those short contracts.

```json
{
    "ticker": "NQH2022",
    "action": "exit"
}
```

### Full Signal Example

You can optionally include a **price** and **quantity** in the signal that can then be used in the calculated orders that we send to your broker. Here is a full example signal.

```json
{
    "ticker": "NQH2022",
    "action": "buy",
    "price": 1420.50,
    "quantity": 2
}
```

If you configure your strategy subscription to use limit orders and to use the signal quantity, then you will get a **Buy Limit** order for 2 contracts at a price of **$1420.50**.

## Supported Brokers

| Broker       | Live | Paper |
| ------------ | ---- | ----- |
| TradeStation | Yes  | Yes   |

{% hint style="info" %}
While TDAmeritrade supports futures via the [ThinkOrSwim](https://www.tdameritrade.com/tools-and-platforms/thinkorswim.html) platform, they unfortunately do not allow futures trading through their API. If you would like to see TD Ameritrade support futures trading through their api, please email their support team at [api@tdameritrade.com](<mailto:api@tdameritrade.com >).
{% endhint %}
