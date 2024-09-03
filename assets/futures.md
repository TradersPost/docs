---
description: >-
  TradersPost supports buying, selling and shorting futures contracts with
  support for over 100 tickers.
---

# Futures

{% embed url="https://www.youtube.com/watch?v=g0dB64iWTpA" %}
TradersPost Automated Futures Trading Setup
{% endembed %}

## Supported Brokers

* [TradeStation](../core-concepts/brokers/tradestation.md)
* [Tradovate](../core-concepts/brokers/broker-roadmap/tradovate.md)
* [Tastytrade](../core-concepts/brokers/tastytrade.md) (coming soon)

## Supported Tickers

TradersPost currently supports trading with the following futures tickers through TradeStation.

{% hint style="info" %}
The ticker names are not always the same from TradingView to TradersPost. Because of this, it's recommended that you hard code your ticker symbol into your alerts instead of using the **\{{ticker\}}** TradingView variable. For example, Lumber with TradeStation is **LB** and on TradingView it's **LBR**.
{% endhint %}

Here is an example:

```json
{
    "ticker": "LBR2024",
    "action": "buy"
}
```

[View our TradingView Watchlist with all available symbols.](https://www.tradingview.com/watchlists/109951165/)

## Symbol Format

TradersPost standardizes the futures symbol format to have a 4 digit year. We convert this symbol format back and fourth when communicating with each broker so you don't have to worry about the differences between brokers.

## Signals

It's easy to send signals to TradersPost using [Webhooks](../core-concepts/webhooks.md) from platforms like [TradingView](../learn/tradingview.md) or [TrendSpider](../learn/trend-spider.md). You just need to send JSON like the following to the webhook URL you create within TradersPost.

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

## Market Orders

{% hint style="danger" %}
While futures trading generally supports market orders, under certain conditions market orders may be <mark style="color:red;">**REJECTED**</mark> by your broker or exchange. For example, during major news announcements like unemployment or inflation numbers, the exchange can go into reserve and during this time market orders are not accepted.
{% endhint %}

During these market conditions, you may receive rejected orders with a reject reason of the following:

![Order type not permitted while the market is reserved](<../.gitbook/assets/Screen Shot 2022-07-13 at 9.17.30 AM (1).png>)

Whenever trading futures and you are facing upcoming volatile market conditions, you have two options:

1. Don't hold positions over upcoming major news announcements (CPI, FOMC announcements, etc)
2. Watch your positions and be ready to take manual action with limit orders if your market orders are rejected.

To keep track of the different news events that may cause the market to move in one direction or another you can use the following calendars.

* [https://www.federalreserve.gov/newsevents/calendar.htm](https://www.federalreserve.gov/newsevents/calendar.htm)
* [https://www.marketwatch.com/economy-politics/calendar](https://www.marketwatch.com/economy-politics/calendar)

## Contract Rollover

{% hint style="danger" %}
You are responsible for ensuring futures contract positions are exited before expiration or are rolled over manually. TradersPost does not automatically do anything special for futures contract positions based on expiration date.
{% endhint %}

In a recent release we made a change to improve how we handle continuous contract symbols and when we switch from the current contract to the next contract.\
\
We will now switch from the current contract to the next contract two days before the beginning of the expiration date. So take `MNQZ2023` for example. It has an expiration date of **Friday December 15th, 2023**.

* Before this change, `MNQ1!` switches to `MNQH2024` at the end of **December 15th, 2023**.
* After this change, `MNQ1!` switches to `MNQH2024` at the beginning of **December 13th, 2023**.
* If you want to trade a specific contract, then you can send **NQH2023** or **NQM2023** instead of **NQ1!** for example. Here is an example JSON.

```json
{
    "ticker": "NQH2023",
    "action": "buy"
}
```

{% hint style="info" %}
It is recommended to always specify the exact contract symbol you want to trade instead of using the continuous contract symbol. The logic for how TradingView and brokers/exchanges rollover from the current contract to the next contract may be different than how TradersPost handles rollovers. We hope to improve this in the future, but for now you should specify the exact contract symbol you would like to trade.
{% endhint %}
