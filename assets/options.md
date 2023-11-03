---
description: >-
  Automate directional options trading strategies with TradersPost. Buy and sell
  calls or puts based on strategies in TradingView or TrendSpider.
---

# Options

{% embed url="https://www.youtube.com/watch?v=Kbb37xqMwR4" %}
TradersPost Automated Options Trading Setup
{% endembed %}

{% hint style="info" %}
TradersPost currently only supports directional options trades. This means that you can only buy and sell calls or puts and you can't have multiple options positions open at the same time on the same underlying ticker in the same broker account.\
\
Some customers separate the positions in separate broker accounts to work around this limitation.
{% endhint %}

## Supported Brokers

* [TD Ameritrade](../brokers/tdameritrade.md)
* [TradeStation](../brokers/tradestation.md)
* [Tradier](../brokers/tradier.md)

## Symbol Format

TradersPost understands many different stock options symbol formats. Since every broker and trading platform has subtle differences in the format we try to be as flexible as possible.

<table><thead><tr><th width="212.54110898661565">Symbol</th><th>Type</th></tr></thead><tbody><tr><td>TSLA 210121C325</td><td>TradeStation, TradersPost</td></tr><tr><td>TSLA_210121C325</td><td>TD Ameritrade</td></tr></tbody></table>

## Supported Option Types

When setting up a strategy within TradersPost you will have the ability to choose what kind of option to buy or sell when signals are received.

* **Both** - Buy calls when bullish (action=buy) and buy puts when bearish (action=sell).
* **Call** - Buy calls when bullish (action=buy) and sell calls when bearish (action=sell).
* **Put** - Buy puts when bearish (action=sell) and sell puts when bullish (action=buy.

{% hint style="warning" %}
It may seem counterintuitive that an action of **sell** will actually buy puts and an action of **buy** will sell puts. Essentially, a **buy** action indicates a bullish sentiment and a **sell** signal indicates a bearish sentiment.\
\
This is important for compatibility with TradingView since strategies are always running on the underlying ticker so the generated action is always buy or sell. What kind of order is created and sent to your broker based on the action, is determined by your strategy subscription settings in TradersPost.
{% endhint %}

## Option Chain Scanning

TradersPost offers a variety of different methods for scanning the option chain automatically to find contracts that fit your criteria.

In this example we have configured our strategy subscription to do the following:

* **Asset class = Options** will buy and sell options contracts.
* **Option Type = Both** will buy calls when bullish and buy puts when bearish.
* **Intrinsic value = In The Money** will filter out any Out Of The money contracts.
* **Expiration = +3 months** will filter out any contracts that expire before 3 months out. If you want to trade same day expiration (0DTE) contracts, then you can enter **0 days** in the expiration field or leave the field blank and TradersPost will select the first expiration date returned by the broker. You can enter an expiration in the strategy subscription settings, click save, then you can see the example entry order and the contract that was selected at the top right of the page.\
  **Strike Count** limits how many strikes to analyze per expiration date when we are scanning the option chain. This does not effect which strike gets selected, it just reduces the number of strikes that will be returned from the broker API for each expiration date. As such, there is no optimal value for this field that will change which strike is selected.
* **Strikes Away** with a value of **3** will select the 3rd contract away from At The Money.

![Options Asset Configuration Example](<../.gitbook/assets/Screen Shot 2022-02-11 at 10.06.21 PM.png>)

## Signals

It's easy to send signals to TradersPost using [Webhooks](../learn/webhooks.md) from platforms like [TradingView](../learn/tradingview.md) or [TrendSpider](../learn/trend-spider.md). You just need to send JSON like the following to the webhook URL you create within TradersPost.

Inside of TradersPost when setting up a strategy you can configure what kind of option contracts to buy when you receive a signal. Here are the signals you can send and the resulting behavior.

### Enter Bullish

The **buy** action is a bullish signal. When TradersPost receives a buy signal, TradersPost will **Buy To Close** or **Sell To Close** any bearish position for the ticker whether that is short calls or long puts and enter bullish with **Buy To Open** long calls or **Sell To Open** short puts.

```json
{
    "ticker": "SQ",
    "action": "buy"
}
```

### Exit Bullish

The **exit** action will exit any open position. So for example if you have a long call position open, then TradersPost will **Sell to Close** those calls.

```json
{
    "ticker": "SQ",
    "action": "exit"
}
```

### Enter Bearish

The **sell** action is a bearish signal. When TradersPost receives a sell signal, TradersPost will **Sell To Close** or **Buy To Close** any bullish position for the ticker whether that is long calls or short puts and enter bearish position with **Buy To Open** long puts or **Sell To Open** short calls.

```json
{
    "ticker": "SQ",
    "action": "sell"
}
```

### Exit Bearish

The **exit** action will exit any open position. So if you have a long puts position open, then TradersPost will **Sell to Close** those puts.

```json
{
    "ticker": "SQ",
    "action": "exit"
}
```

### Full Signal Example

You can optionally include a **quantity** in the signal that can then be used in the calculated orders that we send to your broker. Here is a full example signal.

```json
{
    "ticker": "SQ",
    "action": "buy",
    "quantity": 5
}
```

If you configure your strategy subscription to use limit orders and to use the signal quantity, then you will get a **Buy To Open Limit** order for **5** contracts. If you don’t select entry market or exit market, then we will submit a limit order with the midpoint price.\


{% hint style="warning" %}
TradersPost does not currently support sending prices in signals for options. If you send a price in the signal, the value will not be used. If your strategy subscription is configured to send limit orders, then we will calculate the midpoint price between the bid and ask and use that price for the limit order.
{% endhint %}

## Paper Options Market Data

The TradersPost paper broker does not have options data by default. To get options support in the TradersPost paper broker, you can connect a broker that does have options support (like TD Ameritrade or TradeStation) and then choose that broker as the **Market data source** for the TradersPost paper broker and then you will have options support. Here is a quick video showing you how to do this.

{% embed url="https://www.youtube.com/watch?v=qqw5Olknra4" %}
How To Enable Options Support In The TradersPost Paper Broker
{% endembed %}
