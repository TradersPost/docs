---
description: >-
  TradersPost supports buying, selling and shorting US Equities and Index ETFs
  through the following brokers.
---

# Stock Trading

{% embed url="https://www.youtube.com/watch?v=tJcY7M_YCmU" %}
TradersPost Automated Stocks Trading Setup
{% endembed %}

## Supported Brokers

* [TradeStation](../all-supported-connections/tradestation.md)
* [Alpaca](../all-supported-connections/alpaca.md)
* [Tradier](../all-supported-connections/tradier.md)
* [Interactive Brokers](../all-supported-connections/interactive-brokers.md)
* [Robinhood](../all-supported-connections/robinhood.md)

## Signals

It's easy to send signals to TradersPost using [Webhooks](../core-concepts/signals/webhooks.md) from platforms like [TradingView](../learn/signal-sources/tradingview.md) or [TrendSpider](../learn/signal-sources/trend-spider.md). You just need to send JSON like the following to the webhook URL you create within TradersPost.

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

## Stocks Asset Class Subscription Settings Walkthrough

The subscription settings page is where you edit all settings for your individual subscriptions. It's also where you can override the settings you've sent in your webhook signal.&#x20;

### Auto Submit

{% hint style="info" %}
Checking this will submit your subscription orders automatically to your broker. Otherwise, you will need to manually approve or reject each order.
{% endhint %}

### Allowed Tickers

You can allow any ticker that is in your asset class or you can filter a subscription to only trade tickers you've added.

{% hint style="info" %}
Stock tickers will need to be formatted like this: **SPY, TSLA, AAPL**
{% endhint %}

### Allowed Sides

{% hint style="info" %}
Choose which trade directions are allowed: take both bullish and bearish trades, or restrict to just one side.
{% endhint %}

* Both (Bullish and Bearish)
* Bullish
* Bearish
* None

<details>

<summary><mark style="background-color:$info;">Allow Side Swapping</mark> (Advanced)</summary>

{% hint style="warning" %}
Normally, if a signal comes in for the opposite side, TradersPost will treat it like an exit signal by closing your position and stopping there. When this is turned on, we'll exit what you have and immediately open a new position on the opposite side.
{% endhint %}

Example: You are long `50` shares and send the below JSON:

```
{
    "ticker": "SPY",
    "action": "sell",
    "quantity": "50",
    "price": "660",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
```

**Scenario 1**:

* [x] Allow side swapping

Your `50` share long will immediately be closed, all open orders cancelled, and you'll be entered into a `50` share short.

**Scenario 2**:

* [ ] Allow side swapping

Your `50` share long will immediately be closed and all open orders cancelled. You will be out of all positions and net flat.

</details>

<details>

<summary><mark style="background-color:$info;">Subtract Exit Quantity from Signal Quantity (Advanced)</mark></summary>

{% hint style="info" %}
When side swapping is enabled, enable this option to take the exit quantity and subtract it from the signal quantity before side swapping. (Sides must be set to Both and Side swapping and Use signal quantity are set to enabled)
{% endhint %}

Example: You are long `50` shares and send the below JSON:

```
{
    "ticker": "SPY",
    "action": "sell",
    "quantity": "100",
    "price": "660",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
```

**Scenario 1**:

* [x] Subtract exit quantity from signal quantity

All open orders will be closed and `100` shares will be subtracted from your open long, leaving you net short `50` shares.

**Scenario 2**:

* [ ] Subtract exit quantity from signal quantity

Your `50` share long will immediately be closed, all open orders cancelled, and you'll be entered into a `100` share short.

</details>

<details>

<summary><mark style="background-color:$info;">Sides Isolated</mark> (Advanced)</summary>

{% hint style="info" %}
If there is an open position on the opposite side, do not allow the trade signal to exit the position. (Sides must be set to Bullish or Bearish)
{% endhint %}

Example: You are short `50` shares, have this setting set to "Bullish" and send the below JSON:

```
{
    "ticker": "SPY",
    "action": "buy",
    "quantity": "50",
    "price": "660",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
```

**Scenario 1**:

* [x] Sides Isolated

Your trade will fail and your short will not be exited.

**Scenario 2**:

* [ ] Sides Isolated

Your `50` share short will immediately be closed, all open orders cancelled, and you'll be entered into a `50` share long.

</details>

***

### Trading Window

<details>

<summary>Trading Window</summary>

{% hint style="info" %}
Define your trading windows. Trade signals received outside these windows will be ignored. "From" is inclusive; "To" is exclusive.
{% endhint %}

When trading windows are defined, any trading signals submitted **outside** those windows are ignored by default.

Enabling the "Allow exits and cancels outside of trading windows" option allows **exit** or **cancel** signals to be processed even if they occur outside the defined trading windows. This is helpful if you want to ensure entries happen within your window but still allow exits or cancellations at any time.

Example: You are in a 50 share long that was entered during a trading window that ends at 4pm. It's now 4:01pm and the following signal is received:

```
{
    "ticker": "SPY",
    "action": "sell",
    "quantity": "50",
    "price": "660",
    "time": "2025-09-09T16:01:08Z",
    "interval": "5"
}
```

**Scenario 1**:

* [x] Allow exits and cancels outside of trading windows

Your `50` share long will immediately be closed, all open orders cancelled, and you'll be net flat.

**Scenario 2**:

* [ ] Allow exits and cancels outside of trading windows

Your `50` share long will remain open and your sell trade will reject.

</details>

***

### Position Size

<details>

<summary><mark style="background-color:$info;">Fixed Quantity</mark></summary>

{% hint style="info" %}
Hardcode a fixed quantity for each position instead of calculating a quantity dynamically.
{% endhint %}

This option allows you to specify a fixed quantity for your entries. For example, if you set the fixed quantity to `50`, the strategy will always enter a quantity of `50` shares when the trade is entered.

</details>

<details>

<summary><mark style="background-color:$info;">Amount Per Position</mark></summary>

{% hint style="info" %}
Calculate a quantity of shares using a total dollar amount&#x20;
{% endhint %}

The amount per position dynamic quantity calculation method is used to calculate a quantity based on a desired total notional dollar amount. If you want to buy `$1000` worth of `AAPL` and the price of `AAPL` is currently `$100`, then the quantity would be calculated at `10` shares. This option can be combined with "Use fractional quantity" (below)

</details>

<details>

<summary><mark style="background-color:$info;">Risk Per Position</mark></summary>

{% hint style="info" %}
Calculate the quantity of shares to buy or sell&#x20;
{% endhint %}

Example:

You have a value of 100 in the "Risk Per Position" setting and send the below JSON when Apple is trading at $100:

```
{
    "ticker": "AAPL",
    "action": "buy",
    "price": "660",
    "stopLoss": {
        "stopPrice": 90
    }
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
```

The number of shares TradersPost will send to your broker will be 10 ($100 of risk / $10 in stop loss)

</details>

<details>

<summary><mark style="background-color:$info;">Percent of Equity</mark></summary>

{% hint style="info" %}
Enter a percent of equity to use per position. This will be used to determine the amount per position and the resulting calculated quantity per position.
{% endhint %}

This option dynamically calculates a quantity based on a desired percentage of your equity. For example, if you set the percent of equity to 10%, the strategy will calculate the quantity based on your equity so that the total value of the position is 10% of your equity.

For example, you can buy `10%` of your equity worth of AAPL shares. If you have a `$10000` account and the current price of `AAPL` is `$100`, the quantity will be calculated as `10`.

</details>

***

<details>

<summary><mark style="background-color:$info;">Use Fractional Quantity</mark></summary>

{% hint style="info" %}
Use a fractional quantity if the broker supports it. If the broker does not support fractional trading, the calculated quantity will be rounded down to a whole number.
{% endhint %}

By default, TradersPost will round down quantities to whole numbers when they are fractional. If you would like to use fractional quantities, you can enable this feature by checking the `Use fractional quantity` checkbox. When enabled, TradersPost will use the exact quantity up to the allowed number of decimals that the broker or ticker allows.

</details>

***

<details>

<summary>Allow Add To Position</summary>

{% hint style="info" %}
Allow adding to an existing open position. If this is not checked, trades will be rejected if there is already an open position.
{% endhint %}

Example: You are long 50 shares and send the below JSON:

<pre><code><strong>{
</strong>    "ticker": "SPY",
    "action": "buy",
    "quantity": "50",
    "price": "660",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
</code></pre>

**Scenario 1**:

* [x] Allow Add To Position

Your `50` share long will have `50` more shares added to it, making it a net `100` share long position.

**Scenario 2**:

* [ ] Allow Add To Position

Your `50` share long will remain open, your add will reject, and you'll still be net `50` shares long.

</details>

***

<details>

<summary>Signal Quantity Multiplier</summary>

{% hint style="info" %}
Multiply the signal quantity by a fixed number to scale position size up or down. For example, a signal with quantity 2 and a multiplier of 2.5 results in a final quantity of 5. Only applies when use signal quantity is enabled.
{% endhint %}

The **Signal Quantity Multiplier** allows you to scale the quantity provided in a trade signal up or down by a fixed decimal value.

This multiplier is applied _only if_ the “Use signal quantity” option is enabled. When enabled, TradersPost will take the `quantity` value from the incoming webhook signal and multiply it by the number you provide here.

Example: You send in the following JSON:

```
{
    "ticker": "SPY",
    "action": "buy",
    "quantity": "50",
    "price": "660",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
```

**Signal quantity multiplier:** `2.5`

**Result:** TradersPost will submit a market order for **125 shares** (50 × 2.5).

\
**Use Cases**

* You want to follow a signal provider’s trades, but your account is larger or smaller than theirs.
* You want to scale _all_ trade sizes from a strategy, regardless of what quantity it sends.
* You want to reduce exposure (e.g. use `0.5` to take half-size positions).

**Notes**

* Supports decimal values like `0.1`, `1.5`, `2`, `10`, etc.
* Can be used to **scale down** as well as up.
* Works with both whole and fractional quantities (if your broker supports fractional trading and "Use fractional quantity" is enabled).
* If the calculated final quantity results in a decimal and your broker does not support fractional shares/contracts, the value will be rounded **down**.

**Tip**

If you don't want to use the quantity from the signal, you can leave "Use signal quantity" **disabled** and configure your own quantity calculation method instead.

</details>

### Cancel

<details>

<summary>Cancel</summary>

{% hint style="info" %}
Check this if you do not want TradersPost to cancel open orders before submitting new orders. Beware that if you disable this and you use take profit or stop losses in your broker and you send an exit signal, the broker may reject your exit order due to the take profit or stop loss orders still being open.
{% endhint %}

Example: You are long 50 shares with a stop loss and take profit, and send the below JSON:

<pre><code><strong>{
</strong>    "ticker": "SPY",
    "action": "sell",
    "sentiment": "flat",
    "quantity": "50",
    "price": "660",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
</code></pre>

**Scenario 1:**

* [x] Disable canceling open orders

Your `50` share long will be exited, but the stop loss and take profit will not be cancelled.

**Scenario 2**:

* [ ] Disable canceling open orders

Your `50` share long will immediately be closed, all open orders cancelled, and you'll be net flat.

</details>

### Entries

<details>

<summary>Entry Order Type</summary>

Choose the order type to use for entry orders. Your choices are below:

* Limit
* Market
* Stop Market
* Stop Limit
* Trailing Stop

{% hint style="info" %}
For Trailing Stop orders, you'll also need to add one of the following
{% endhint %}

* Entry Trail Amount (in points on the underlying futures ticker)
* Entry Trail Percent (based off the % of the underlying futures ticker)



* [ ] Allow entry extended hours

{% hint style="info" %}
Entry orders will be sent to your broker as extended hours limit orders when the market is closed. If you also select the "Market" order type, then extended hours limit orders will be used when the market is closed and market orders will be used when the market is open.
{% endhint %}

By default, entry orders are submitted to your broker with extended hours disabled. By checking the `Allow entry extended hours` checkbox in your strategy settings, you can enable extended hours trading for your entry orders.

When this setting is combined with an `Entry order type` of `Market`, the entry order will be submitted as a market order when the market is open and an extended hours limit order when the market is closed.

</details>

<details>

<summary>Entry Time In Force</summary>

{% hint style="info" %}
By default, TradersPost will send the appropriate time in force of either `gtc` or `day` depending on the scenario and broker
{% endhint %}

Choose the entry time in force to use for entry orders. Your choices are below:

* Good For Day: The order is valid for the trading day and will be canceled if not executed by the end of the trading day
* Good Until Cancelled: The order is good until canceled and will remain active until it is executed or canceled.Fill Or Kill
* Immediate Or Cancel: The order is immediate or canceled, meaning it must be executed immediately or canceled.
* Fill Or Kill: The order is fill or kill, meaning it must be executed immediately in its entirety or canceled.

</details>

<details>

<summary>Entry Price</summary>

{% hint style="info" %}
Choose what quote price to use as the current market price for entries if the signal does not have a price.
{% endhint %}

**When your signal does not have a price**, TradersPost will fetch a quote from the broker and use the configured market price type from the strategy settings instead of using the price from the signal. By default, the `Bid-ask midpoint` will be used. For example, if you have `limit` orders configured and you send a signal without a `limitPrice`, then TradersPost will use the the price from the quote.

If you specify a `limitPrice`, then that value will be used.

```
{
    "ticker": "AAPL",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": 100
}
```

</details>

### Exits

<details>

<summary>Entry Order Type</summary>

Choose the order type to use for exit orders. Your choices are below:

* Limit
* Market
* Stop Market
* Stop Limit
* Trailing Stop

{% hint style="info" %}
For Trailing Stop orders, you'll also need to add one of the following
{% endhint %}

* Exit Trail Amount (in points on the underlying futures ticker)
* Exit Trail Percent (based off the % of the underlying futures ticker)



* [ ] Allow exit extended hours

By default, exit orders are submitted to your broker with extended hours disabled. By checking the `Allow exit extended hours` checkbox in your strategy settings, you can enable extended hours trading for your exit orders.

When this setting is combined with an `Exit order type` of `Market`, the exit order will be submitted as a market order when the market is open and an extended hours limit order when the market is closed.

</details>

<details>

<summary>Exit Time In Force</summary>

{% hint style="info" %}
By default, TradersPost will send the appropriate time in force of either `gtc` or `day` depending on the scenario and broker
{% endhint %}

Choose the exit time in force to use for entry orders. Your choices are below:

* Good For Day: The order is valid for the trading day and will be canceled if not executed by the end of the trading day
* Good Until Cancelled: The order is good until canceled and will remain active until it is executed or canceled.
* Immediate Or Cancel: The order is immediate or canceled, meaning it must be executed immediately or canceled.
* Fill Or Kill: The order is fill or kill, meaning it must be executed immediately in its entirety or canceled.

</details>

<details>

<summary>Exit Price</summary>

{% hint style="info" %}
Choose what quote price to use as the current market price for entries if the signal does not have a price.
{% endhint %}

**When your signal does not have a price**, TradersPost will fetch a quote from the broker and use the configured market price type from the strategy settings instead of using the price from the signal. By default, the `Bid-ask midpoint` will be used. For example, if you have `limit` orders configured and you send a signal without a `limitPrice`, then TradersPost will use the the price from the quote.

If you specify a `limitPrice`, then that value will be used.

```
{
    "ticker": "AAPL",
    "action": "sell",
    "orderType": "limit",
    "limitPrice": 100
}
```

</details>

### Take Profit / Stop Loss

<details>

<summary>Take Profit</summary>

For take profits orders, you can have one of two choices:

* Take Profit Percent (based off the % of the underlying stock ticker)
* Take Profit Amount (based off of points on the underlying stock ticker)

**Scenario 1**:

You send this signal with a take profit % as `5%` in your subscription settings.

<pre><code><strong>{
</strong>    "ticker": "SPY",
    "action": "Buy",
    "quantity": "10",
    "price": "660",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
</code></pre>

You will be entered into a `10` share long with a `10` share limit sell at `693` on MNQ.&#x20;

{% hint style="danger" %}
**The take profit % is not based on profit and loss on your portfolio, it's based on the underlying ticker.** Make sure you understand that we are placing your take profit relative to the price where your stock ticker is trading.
{% endhint %}

**Scenario 2**:

You send this signal with a take profit amount as `10` in your subscription settings.

<pre><code><strong>{
</strong>    "ticker": "SPY",
    "action": "Buy",
    "quantity": "50",
    "price": "660",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
</code></pre>

You will be entered into a `50` share long with a `50` share limit sell at `670` on SPY.&#x20;

{% hint style="danger" %}
**The take profit amount is not based on profit and loss on your portfolio, it's based on the underlying ticker.** It's up to you to figure out based on the number of shares you're trading and the profit you want to achieve what value to write in the `amount` field.
{% endhint %}

</details>

<details>

<summary>Stop Loss</summary>

For the stop loss order type, there are three choices:

* Stop Market
* Stop Limit
* Trailing Stop

As far as where the order will be placed relative to your entry, you have two choices:

* Take Profit Percent (based off the % of the underlying stock ticker)
* Take Profit Amount (based off of points on the underlying stock ticker)

**Scenario 1**:

You send this signal with a stop loss % as `5%` in your subscription settings.

<pre><code><strong>{
</strong>    "ticker": "SPY",
    "action": "Buy",
    "quantity": "50",
    "price": "660",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
</code></pre>

You will be entered into a `50` share long with a `50` contract sell (stop market, stop limit, or trailing stop) at `627` on SPY.&#x20;

{% hint style="danger" %}
**The stop loss % is not based on loss on your portfolio, it's based on the underlying stock ticker.** Make sure you understand that we are placing your stop loss / trailing stop relative to the price where your stock ticker is trading.
{% endhint %}

**Scenario 2**:

You send this signal with a stop loss amount as `10` in your subscription settings.

<pre><code><strong>{
</strong>    "ticker": "SPY",
    "action": "Buy",
    "quantity": "50",
    "price": "660",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
</code></pre>

You will be entered into a `50` share long with a `50` contract sell (stop market, stop limit, or trailing stop) at `670` on MNQ.&#x20;

{% hint style="danger" %}
**The stop loss profit amount is not based on profit and loss on your portfolio, it's based on points on the underlying ticker.** If you type in `10` it doesn't mean $10 loss on your P/L. It's up to you to figure out based on the number of contracts you're trading and the profit you want to achieve what value to write in the `amount` field.
{% endhint %}

</details>

### Retry

<details>

<summary>Retry</summary>

When TradersPost executes a trade, the first thing it does is communicate with the broker to fetch the state of the broker account and "plan the trade". This includes fetching current open positions, open orders, account balances, and any other information required to execute the trade. TradersPost then uses this information to determine the plan for executing the trade, which includes deciding whether to cancel any open orders for the ticker, exit the open position if it exists, or enter a new position. If there were any problems communicating with the broker or processing the trade plan, you will see this message.

Here is a list of the available retry settings:

* `Max retries` - The maximum number of times the system will retry the trade. If the trade fails after the maximum number of retries, the trade will be marked as failed.
* `Delay in milliseconds` - The delay between each retry attempt. The system will wait for this amount of time before retrying the trade.
* `Delay multiplier` - The multiplier to apply to the delay between each retry attempt. The system will multiply the delay by this value after each retry attempt. For example, if the delay is set to `1000` milliseconds and the delay multiplier is set to `2`, the system will wait `1000` milliseconds before the first retry, `2000` milliseconds before the second retry, `4000` milliseconds before the third retry, and so on.
* `Max delay in milliseconds` - The maximum delay between retry attempts. If the delay calculated by the delay multiplier exceeds this value, the system will use this value as the delay.

</details>

<a href="stock-trading.md#supported-brokers" class="button primary">New button</a>
