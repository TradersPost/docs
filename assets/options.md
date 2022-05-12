# Options

{% hint style="info" %}
**Coming Soon!** Options trading is currently only available for paper trading by default. You can join the wait list [here](https://traderspost.io/wait-list/options). If you would like to apply to be a part of the live options beta, email [support@traderspost.io](mailto:support@traderspost.io).
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=Kbb37xqMwR4" %}
TradersPost Automated Options Trading Setup
{% endembed %}

## Symbol Format

TradersPost understands many different stock options symbol formats. Since every broker and trading platform has subtle differences in the format we try to be as flexible as possible.

| Symbol           | Type                      |
| ---------------- | ------------------------- |
| TSLA 210121C325  | TradeStation, TradersPost |
| TSLA\_210121C325 | TD Ameritrade             |

## Supported Option Types

When setting up a strategy within TradersPost you will have the ability to choose what kind of option to buy or sell when signals are received.

* **Both** - Buy calls when bullish (action=buy) and buy puts when bearish (action=sell).
* **Call** - Buy calls when bullish (action=buy) and sell calls when bearish (action=sell).
* **Put** - Buy puts when bearish (action=sell) and sell puts when bullish (action=buy.

{% hint style="info" %}
It can be a little confusing that when you configure a strategy to use puts, an action of **sell** will actually buy puts and an action of **buy** will sell puts. Essentially, a **buy** action indicates a bullish sentiment and a **sell** signal indicates a bearish sentiment.
{% endhint %}

## Option Chain Scanning

TradersPost offers a variety of different methods for scanning the option chain automatically to find contracts that fit your criteria.

In this example we have configured our strategy subscription to do the following:

* **Asset class = Options** will buy and sell options contracts.
* **Option Type = Both** will buy calls when bullish and buy puts when bearish.
* **Intrinsic value = In The Money** will filter out any Out Of The money contracts.
* **Expiration = +3 months** will filter out any contracts that expire before 3 months out.
* **Strike Count** limits how many strikes to analyze per expiration date when we're scanning the option chain.
* **Strikes Away = 3** will select the 3rd contract away from At The Money.

![Options Asset Configuration Example](<../.gitbook/assets/Screen Shot 2022-02-11 at 10.06.21 PM.png>)

## Signals

It's easy to send signals to TradersPost using [Webhooks](../webhooks.md) from platforms like [TradingView](../tradingview.md) or [TrendSpider](../trend-spider.md). You just need to send JSON like the following to the webhook URL you create within TradersPost.

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

If you configure your strategy subscription to use limit orders and to use the signal quantity, then you will get a **Buy To Open Limit** order for **5** contracts.

{% hint style="warning" %}
TradersPost does not currently support sending prices in signals for options. If you send a price in the signal, the value will not be used. If your strategy subscription is configured to send limit orders, then we will calculate the midpoint price between the bid and ask and use that price for the limit order.
{% endhint %}
