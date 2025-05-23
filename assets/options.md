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

* [TradeStation](../core-concepts/brokers/tradestation.md)
* [Alpaca](../core-concepts/brokers/alpaca.md)
* [Tradier](../core-concepts/brokers/tradier.md)

## Symbol Format

This section outlines the different formats TradersPost supports for representing options contracts. Users are not required to use a specific format based on their connected broker. TradersPost parses and normalizes multiple formats internally and automatically converts them to the correct format required by each broker when submitting orders.

#### Example Contract

* **Underlying**: SPY
* **Contract Type**: Call
* **Strike Price**: $582.50
* **Expiration Date**: May 20, 2025

> **Note**: This specific contract is used for demonstration purposes only. A $582.50 strike price for SPY may not exist. The decimal is included to illustrate how different formats handle precision.

#### Format Comparison

<table><thead><tr><th width="153.13671875">Platform</th><th width="204.57421875">Example Format</th><th width="108.49609375">Date Format</th><th width="128.17578125">Strike Format</th><th width="264.71484375">Notes</th></tr></thead><tbody><tr><td><strong>TradersPost</strong></td><td><code>SPY 250520582.5</code></td><td>YMD</td><td>Decimal</td><td>Flexible input format. Trailing <code>.0</code> is optional.</td></tr><tr><td><strong>TDAmeritrade</strong></td><td><code>SPY_052025582.5</code></td><td>MDY</td><td>Decimal</td><td>Uses underscore between symbol and date.</td></tr><tr><td><strong>TradeStation</strong></td><td><code>SPY 250520C582.5</code></td><td>YMD</td><td>Decimal</td><td>Includes call/put indicator (<code>C</code> or <code>P</code>) before strike.</td></tr><tr><td><strong>Tradier</strong></td><td><code>SPY250520C00582500</code></td><td>YMD</td><td>Integer (scaled)</td><td>Strike is zero-padded and scaled (e.g., 582.5 → 00582500).</td></tr><tr><td><strong>TradingView</strong></td><td><code>SPY250520582.5</code></td><td>YMD</td><td>Decimal</td><td>Fully concatenated format without spaces.</td></tr></tbody></table>

#### Format Details

**Date Formatting**

* **YMD** = `YYMMDD` (e.g. May 20, 2025 → `250520`)
* **MDY** = `MMDDYY` (e.g. May 20, 2025 → `052025`)

**Strike Formatting**

* **Decimal Format**: Most formats use a decimal representation of the strike. Trailing zeroes are optional (`582.5` or `582`).
* **Scaled Integer Format** (Tradier): Strike is padded and scaled to four decimal places (e.g., `582.5` → `00582500`).

**Call/Put Indicator**

* Some formats include an explicit indicator for option type:
  * `C` = Call
  * `P` = Put

#### TradersPost Behavior

* Users can input any of the supported formats regardless of broker.
* TradersPost will parse, validate, and normalize the input.
* When sending the order to the broker, TradersPost will format the symbol according to the broker’s specific requirements.

**Examples of accepted user input:**

* `SPY 250520582.5`
* `SPY_052025582.5`
* `SPY250520C582.5`
* `SPY250520582.5`
* `SPY250520C00582500`

## Supported Option Types

When setting up a strategy within TradersPost you will have the ability to choose what kind of option to buy or sell when signals are received.

* **Both** - Buy calls when bullish (action=buy) and buy puts when bearish (action=sell).
* **Call** - Buy calls when bullish (action=buy) and sell calls when bearish (action=sell).
* **Put** - Buy puts when bearish (action=sell) and sell puts when bullish (action=buy).

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
* **Expiration = +3 months** will filter out any contracts that expire before 3 months out. If you want to trade same day expiration (0DTE) contracts, then you can enter **0 days** in the expiration field or leave the field blank and TradersPost will select the first expiration date returned by the broker. You can enter an expiration in the strategy subscription settings, click save, then you can see the example entry order and the contract that was selected at the top right of the page.
* **Strike Count** limits how many strikes to analyze per expiration date when we are scanning the option chain. This does not effect which strike gets selected, it just reduces the number of strikes that will be returned from the broker API for each expiration date. As such, there is no optimal value for this field that will change which strike is selected.
* **Strikes Away** with a value of **3** will select the 3rd contract away from At The Money.

![Options Asset Configuration Example](<../.gitbook/assets/Screen Shot 2022-02-11 at 10.06.21 PM.png>)

You are able to control the option chain scanning functionality from webhooks. Here is an example:

```json
{
    "ticker": "AAPL",
    "action": "buy",
    "expiration": "+6 months",
    "instrinsicValue": "itm",
    "optionType": "both",
    "strikesAway": 3
}
```

Or send the exact contract you want to trade instead of using the option chain scanning functionality:

```json
{
    "ticker": "AAPL",
    "action": "buy",
    "expiration": "2023-01-20",
    "optionType": "call",
    "strikePrice": 325
}
```

Or send the full option contract symbol in the `ticker` parameter:

```json
{
    "ticker": "AAPL 230120C325",
    "action": "buy"
}
```

## Webhook Signals

It's easy to send signals to TradersPost using [Webhooks](../core-concepts/webhooks.md) from platforms like [TradingView](../learn/tradingview.md) or [TrendSpider](../learn/trend-spider.md). You just need to send JSON like the following to the webhook URL you create within TradersPost.

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

If you configure your strategy subscription to use limit orders and to use the signal quantity, then you will get a **Buy To Open Limit** order for **5** contracts. If you don’t select entry market or exit market, then we will submit a limit order with the midpoint price.

## Paper Options Market Data

The TradersPost paper broker does not have options data by default. To get options support in the TradersPost paper broker, you can connect a broker that does have options support (like TD Ameritrade or TradeStation) and then choose that broker as the **Market data source** for the TradersPost paper broker and then you will have options support. Here is a quick video showing you how to do this.

{% embed url="https://www.youtube.com/watch?v=qqw5Olknra4" %}
How To Enable Options Support In The TradersPost Paper Broker
{% endembed %}
