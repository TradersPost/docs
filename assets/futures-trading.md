---
description: >-
  TradersPost supports buying, selling and shorting futures contracts with
  support for over 100 tickers.
---

# Futures Trading

{% embed url="https://www.youtube.com/watch?v=g0dB64iWTpA" %}
TradersPost Automated Futures Trading Setup
{% endembed %}

## Supported Brokers

* [TradeStation](../all-supported-connections/tradestation.md)
* [Tradovate](../all-supported-connections/tradovate.md)
* [Tastytrade](../all-supported-connections/tastytrade.md) (coming soon)

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

It's easy to send signals to TradersPost using [Webhooks](../core-concepts/webhooks.md) from platforms like [TradingView](../learn/signal-sources/tradingview.md) or [TrendSpider](../learn/signal-sources/trend-spider.md). You just need to send JSON like the following to the webhook URL you create within TradersPost.

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

{% hint style="info" %}
It is recommended to always specify the exact contract symbol you want to trade instead of using the continuous contract symbol. The logic for how TradingView and brokers/exchanges rollover from the current contract to the next contract may be different than how TradersPost handles rollovers. We hope to improve this in the future, but for now you should specify the exact contract symbol you would like to trade.\
\
Please see our [Blog Post](https://blog.traderspost.io/article/trading-continuous-futures-contracts-from-tradingview-on-traderspost) on our recommendations for trading continuous futures on TradingView.
{% endhint %}

In 2023, we made a change to improve how we handle continuous contract symbols and when we switch from the current contract to the next contract.\
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

## Determining the Continuous Futures Contract Symbol

To address the challenge of identifying the specific futures contract referenced by a continuous contract symbol (e.g., GC1!, NQ1!), we’ve developed an **experimental Pine Script solution**. This script dynamically determines the current front-month contract by comparing the continuous contract’s price and volume data with individual contract data, helping traders align their automated strategies with the exact contract being traded on TradingView.

### Why This Matters

TradingView’s continuous contract symbols (e.g., GC1! for gold futures) automatically resolve to the front-month contract based on its internal rollover logic. However, this resolved contract symbol (e.g., GCJ2025) is not directly accessible in Pine Script via `syminfo`. Additionally, TradersPost handles contract rollovers differently—switching to the next contract two days before the expiration date—while TradingView’s rollover timing can vary and is not transparent. This mismatch can lead to unexpected behavior in automated trading strategies. Our experimental script aims to bridge this gap by identifying the exact contract in real-time.

### How It Works

The script:

1. Uses syminfo.root (e.g., GC for gold, NQ for NASDAQ) to build ticker symbols for all 12 months of the current year, based on the standard futures contract naming convention (e.g., GCH2025 for March 2025 gold).
2. Requests open price and volume data for each monthly contract using `request.security()`, adjusted to disable back-adjustments for accurate comparisons.
3. Compares these values against the continuous contract’s open price and volume (e.g., GC1!), identifying the matching contract.
4. Outputs the resolved contract symbol (e.g., GCJ2025), which can be used in your strategy or passed to TradersPost via a webhook.

Here is the code snippet you can add to your pine script v6:

```
contract(int mth) =>
    mth_sym = switch mth
        1  => 'F' // Jan
        2  => 'G' // Feb
        3  => 'H' // Mar
        4  => 'J' // Apr
        5  => 'K' // May
        6  => 'M' // Jun
        7  => 'N' // Jul
        8  => 'Q' // Aug
        9  => 'U' // Sep
        10 => 'V' // Oct
        11 => 'X' // Nov
        12 => 'Z' // Dec

    str.format('{0}{1}{2}', syminfo.root, mth_sym, str.tostring(year(timenow)))

front_contract() =>
    var contract = ''

    [op, vlm] = request.security(ticker.modify(syminfo.tickerid, '', adjustment.none, backadjustment.off), '', [open, volume])
    
    for i = 1 to 12
        sym = contract(i)
        
        [op_, vlm_] = request.security(sym, '', [open, volume], ignore_invalid_symbol = true)
        
        if op == op_ and vlm == vlm_
            contract := sym
            break

    contract

// front_contract() will return the ticker symbol for the futures contract in question.
```

In this example, the script identifies the current contract (e.g., GCJ2025), which becomes available when using the `front_contract()` function.&#x20;

{% embed url="https://youtube.com/live/sJinXCBorz4" %}

#### Limitations and Caveats

* **Real-Time Only:** The script uses the current time (not the time of the current bar) to fetch the current year, making it suitable for live trading but **not backtesting**.&#x20;
* **Resource Usage:** The script makes up to 13 `request.security()` calls (1 for the continuous contract and 12 for monthly contracts), out of Pine Script’s limit of 40. If your strategy already uses many requests, you may exceed this limit.
* **Experimental Nature:** This solution is provided for educational purposes and has not been extensively tested in live trading. We recommend running it in a demo environment first to verify behavior, especially during rollover periods.
* **Rollover Variability:** TradingView’s rollover timing may still differ from TradersPost’s, and this script assumes the continuous contract’s data reflects the front-month contract. Edge cases (e.g., low-volume contracts with identical prices) could potentially misidentify the contract, although that seems unlikely.

### Future Improvements

We’re exploring ways to optimize this solution, such as reducing the number of security requests or creating a Pine Script library for easier integration.&#x20;

We also hope TradingView will eventually expose the resolved contract symbol in `syminfo`, rendering this workaround unnecessary.

### Get the Script

You can find the full script [here](https://www.tradingview.com/script/82WdxE57-TradersPost-Futures-Contract-Rollover-Example/). Feel free to adapt it to your needs and share feedback with us via support, Discord, or YouTube comments.&#x20;

### Community Feedback

This solution was inspired by community questions during our weekly show Office Hours. If you encounter issues, have suggestions, or want to see new features, let us know—we’re committed to improving automation for futures trading.
