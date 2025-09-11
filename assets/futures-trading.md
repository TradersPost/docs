---
description: >-
  TradersPost supports buying, selling and shorting futures contracts with
  support for over 100 tickers.
---

# Futures Trading

## Supported Brokers

Click below to see the full list of supported futures brokers and prop firms.

{% embed url="https://traderspost.io/asset/futures" %}

## Supported Tickers

TradersPost currently supports trading with the following futures tickers through TradeStation.

{% hint style="info" %}
The ticker names are not always the same from TradingView to TradersPost. Because of this, it's recommended that you hard code your ticker symbol into your alerts instead of using the **\{{ticker\}}** TradingView variable. For example, Lumber with TradeStation is **LB** and on TradingView it's **LBR**.
{% endhint %}

Here is an example:

```json
{
    "ticker": "MNQU2025",
    "action": "buy"
}
```

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

TradingView has [recently added](https://www.tradingview.com/pine-script-reference/v6/#var_syminfo.current_contract) the variable `syminfo.current_contract` to Pine Script. This would return the underlying contract for the current symbol if it is a continuous futures contract (`na` otherwise).

***

## Futures Asset Class Subscription Settings Walkthrough

The subscription settings page is where you edit all settings for your individual subscriptions. It's also where you can override the settings you've sent in your webhook signal.&#x20;

### Auto Submit

{% hint style="info" %}
Checking this will submit your subscription orders automatically to your broker. Otherwise, you will need to manually approve or reject each order.
{% endhint %}

### Allowed Tickers

You can allow any ticker that is in your asset class or you can filter a subscription to only trade tickers you've added.

{% hint style="info" %}
Futures tickers will need to be formatted like this: **MNQ, NQ, MES**.&#x20;

Not **MNQ1! (continuous contract)** or **MNQU2025 (specific contract)**
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

Example: You are long `2` contracts and send the below JSON:

```
{
    "ticker": "MNQU2025",
    "action": "sell",
    "quantity": "2",
    "price": "23810.25",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
```

**Scenario 1**:

* [x] Allow side swapping

Your `2` contract long will immediately be closed, all open orders cancelled, and you'll be entered into a `2` contract short.

**Scenario 2**:

* [ ] Allow side swapping

Your `2` contract long will immediately be closed and all open orders cancelled. You will be out of all positions and net flat.

</details>

<details>

<summary><mark style="background-color:$info;">Subtract Exit Quantity from Signal Quantity (Advanced)</mark></summary>

{% hint style="info" %}
When side swapping is enabled, enable this option to take the exit quantity and subtract it from the signal quantity before side swapping. (Sides must be set to Both and Side swapping and Use signal quantity are set to enabled)
{% endhint %}

Example: You are long `2` contracts and send the below JSON:

```
{
    "ticker": "MNQU2025",
    "action": "sell",
    "quantity": "4",
    "price": "23810.25",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
```

**Scenario 1**:

* [x] Subtract exit quantity from signal quantity

All open orders will be closed and `4` contracts will be subtracted from your open long, leaving you net short `2` contracts.

**Scenario 2**:

* [ ] Subtract exit quantity from signal quantity

Your `2` contract long will immediately be closed, all open orders cancelled, and you'll be entered into a `4` contract short.

</details>

<details>

<summary><mark style="background-color:$info;">Sides Isolated</mark> (Advanced)</summary>

{% hint style="info" %}
If there is an open position on the opposite side, do not allow the trade signal to exit the position. (Sides must be set to Bullish or Bearish)
{% endhint %}

Example: You are short `2` contracts, have this setting set to "Bullish" and send the below JSON:

```
{
    "ticker": "MNQU2025",
    "action": "buy",
    "quantity": "2",
    "price": "23810.25",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
```

**Scenario 1**:

* [x] Sides Isolated

Your trade will fail and your short will not be exited.

**Scenario 2**:

* [ ] Sides Isolated

Your `2` contract short will immediately be closed, all open orders cancelled, and you'll be entered into a `2` contract long.

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

Example: You are in a 2 contract long that was entered during a trading window that ends at 4pm. It's now 4:01pm and the following signal is received:

```
{
    "ticker": "MNQU2025",
    "action": "sell",
    "quantity": "2",
    "price": "23810.25",
    "time": "2025-09-09T16:01:08Z",
    "interval": "5"
}
```

**Scenario 1**:

* [x] Allow exits and cancels outside of trading windows

Your `2` contract long will immediately be closed, all open orders cancelled, and you'll be net flat.

**Scenario 2**:

* [ ] Allow exits and cancels outside of trading windows

Your `2` contract long will remain open and your sell trade will reject.

</details>

***

### Position Size

<details>

<summary><mark style="background-color:$info;">Fixed Quantity</mark></summary>

{% hint style="info" %}
Hardcode a fixed quantity for each position instead of calculating a quantity dynamically.
{% endhint %}

This option allows you to specify a fixed quantity for your entries. For example, if you set the fixed quantity to `5`, the strategy will always enter a quantity of `5` contracts when the trade is entered.

</details>

<details>

<summary><mark style="background-color:$info;">Amount Per Position</mark></summary>

{% hint style="danger" %}
Not a compatible position size option for the Futures asset class
{% endhint %}

</details>

<details>

<summary><mark style="background-color:$info;">Risk Per Position</mark></summary>

{% hint style="danger" %}
Not a compatible position size option for the Futures asset class
{% endhint %}

</details>

<details>

<summary><mark style="background-color:$info;">Percent of Equity</mark></summary>

{% hint style="danger" %}
Not a compatible position size option for the Futures asset class
{% endhint %}

</details>

***

<details>

<summary><mark style="background-color:$info;">Use Fractional Quantity</mark></summary>

{% hint style="danger" %}
Not a compatible option for the Futures asset class
{% endhint %}

</details>

***

<details>

<summary>Allow Add To Position</summary>

{% hint style="info" %}
Allow adding to an existing open position. If this is not checked, trades will be rejected if there is already an open position.
{% endhint %}

Example: You are long 2 contracts and send the below JSON:

<pre><code><strong>{
</strong>    "ticker": "MNQU2025",
    "action": "buy",
    "quantity": "2",
    "price": "23810.25",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
</code></pre>

**Scenario 1**:

* [x] Allow Add To Position

Your `2` contract long will have `2` more contracts added to it, making it a net `4` contract long position.

**Scenario 2**:

* [ ] Allow Add To Position

Your `2` contract long will remain open, your add will reject, and you'll still be net `2` contracts long.

</details>

***

<details>

<summary>Signal Quantity Multiplier</summary>

{% hint style="info" %}
Multiply the signal quantity by a fixed number to scale position size up or down. For example, a signal with quantity 2 and a multiplier of 2.5 results in a final quantity of 5. Only applies when use signal quantity is enabled.
{% endhint %}

The **Signal Quantity Multiplier** allows you to scale the quantity provided in a trade signal up or down by a fixed decimal value.

This multiplier is applied _only if_ the “Use signal quantity” option is enabled. When enabled, TradersPost will take the `quantity` value from the incoming webhook signal and multiply it by the number you provide here.

Example: You send in the following JSON

```
{
    "ticker": "MNQU2025",
    "action": "buy",
    "quantity": "2",
    "price": "23810.25",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
```

**Signal quantity multiplier:** `2.5`

**Result:** TradersPost will submit a market order for **5 contracts** (2 × 2.5).

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

Example: You are long 2 contracts with a stop loss and take profit, and send the below JSON:

<pre><code><strong>{
</strong>    "ticker": "MNQU2025",
    "action": "sell",
    "sentiment": "flat",
    "quantity": "2",
    "price": "23810.25",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
</code></pre>

**Scenario 1:**

* [x] Disable canceling open orders

Your `2` contract long will be exited, but the stop loss and take profit will not be cancelled.

**Scenario 2**:

* [ ] Disable canceling open orders

Your `2` contract long will immediately be closed, all open orders cancelled, and you'll be net flat.

</details>

### Entries

<details>

<summary>Entry Order Type</summary>

{% hint style="info" %}
If the broker you are using does not support quotes (Tradovate and ProjectX) **you must always send a price in your signal if you are sending limit orders or bracket orders (ProjectX does not yet support brackets).**
{% endhint %}

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

{% hint style="danger" %}
Not supported for the Futures class
{% endhint %}

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
If the broker you are using does not support quotes (Tradovate and ProjectX) **you must always send a price in your signal if you are sending limit orders or bracket orders (ProjectX does not yet support brackets).**
{% endhint %}

For TradeStation (or other futures firms which support quotes) if you don't include a price and want to send a limit order or send a bracket with your entry, your choices are below for how you want TradersPost to estimate the signal price:

* Bid-ask midpoint
* Use ask for buys and bids for sells
* Always use ask
* Always use bid
* Use last price

</details>

### Exits

<details>

<summary>Entry Order Type</summary>

{% hint style="info" %}
If the broker you are using does not support quotes (Tradovate and ProjectX) **you must always send a price in your signal if you are sending limit orders or bracket orders (ProjectX does not yet support brackets).**
{% endhint %}

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

{% hint style="danger" %}
Not supported for the Futures class
{% endhint %}

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
If the broker you are using does not support quotes (Tradovate and ProjectX) **you must always send a price in your signal if you are sending limit orders or bracket orders (ProjectX does not yet support brackets).**
{% endhint %}

For TradeStation (or other futures firms which support quotes) if you don't include a price and want to send a limit order or send a bracket with your exit, your choices are below for how you want TradersPost to estimate the signal price:

* Bid-ask midpoint
* Use ask for buys and bids for sells
* Always use ask
* Always use bid
* Use last price

</details>

### Take Profit / Stop Loss

<details>

<summary>Take Profit</summary>

{% hint style="info" %}
If the broker you are using does not support quotes (Tradovate and ProjectX) **you must always send a price in your signal if you are sending bracket orders (ProjectX does not yet support brackets).**
{% endhint %}

Tradovate, TradeStation, and Tastytrade are the only futures brokers on TradersPost that support bracket orders (take profits / stop losses / trailing stops) that are attached with your entry or exit.

For take profits, you can have one of two choices:

* Take Profit Percent (based off the % of the underlying futures ticker)
* Take Profit Amount (based off of points on the underlying futures ticker)

**Scenario 1**:

You send this signal with a take profit % as `5%` in your subscription settings.

<pre><code><strong>{
</strong>    "ticker": "MNQU2025",
    "action": "Buy",
    "quantity": "2",
    "price": "23810.25",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
</code></pre>

You will be entered into a `2` contract long with a `2` contract limit sell at `25000` on MNQ.&#x20;

{% hint style="danger" %}
**The take profit % is not based on profit and loss on your portfolio, it's based on the underlying ticker.** Even a small % on a futures ticker like MNQ will be a relatively huge amount for most traders. Make sure you understand that we are placing your take profit relative to the price where your futures ticker is trading in the signal that you send. In the above example, 23810.25 x 5% is nearly 1,200 points on MNQ.
{% endhint %}

**Scenario 2**:

You send this signal with a take profit amount as `250` in your subscription settings.

<pre><code><strong>{
</strong>    "ticker": "MNQU2025",
    "action": "Buy",
    "quantity": "2",
    "price": "23810.25",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
</code></pre>

You will be entered into a `2` contract long with a `2` contract limit sell at `24060.25` on MNQ.&#x20;

{% hint style="danger" %}
**The take profit amount is not based on profit and loss on your portfolio, it's based on points on the underlying ticker.** If you type in `250` it doesn't mean $250 profit on your P/L. It means 250 points on MNQ which for 2 contract trade would be $1000 in profit on your P/L. It's up to you to figure out based on the number of contracts you're trading and the profit you want to achieve what value to write in the `amount` field.
{% endhint %}

</details>

<details>

<summary>Stop Loss</summary>

{% hint style="info" %}
If the broker you are using does not support quotes (Tradovate and ProjectX) **you must always send a price in your signal if you are sending bracket orders (ProjectX does not yet support brackets).**
{% endhint %}

Tradovate, TradeStation, and Tastytrade are the only futures brokers on TradersPost that support bracket orders (take profits / stop losses / trailing stops) that are attached with your entry or exit.

For the stop loss order type, there are three choices:

* Stop Market
* Stop Limit
* Trailing Stop

As far as where the order will be placed relative to your entry, you have two choices:

* Take Profit Percent (based off the % of the underlying futures ticker)
* Take Profit Amount (based off of points on the underlying futures ticker)

**Scenario 1**:

You send this signal with a stop loss % as `5%` in your subscription settings.

<pre><code><strong>{
</strong>    "ticker": "MNQU2025",
    "action": "Buy",
    "quantity": "2",
    "price": "23810.25",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
</code></pre>

You will be entered into a `2` contract long with a `2` contract sell (stop market, stop limit, or trailing stop) at `22619.75` on MNQ.&#x20;

{% hint style="danger" %}
**The stop loss % is not based on loss on your portfolio, it's based on the underlying ticker.** Even a small % on a futures ticker like MNQ will be a relatively huge amount for most traders. Make sure you understand that we are placing your stop loss / trailing stop relative to the price where your futures ticker is trading in the signal that you send. In the above example, 23810.25 x 5% is nearly 1,200 points on MNQ.
{% endhint %}

**Scenario 2**:

You send this signal with a stop loss amount as `250` in your subscription settings.

<pre><code><strong>{
</strong>    "ticker": "MNQU2025",
    "action": "Buy",
    "quantity": "2",
    "price": "23810.25",
    "time": "2025-09-09T14:07:08Z",
    "interval": "5"
}
</code></pre>

You will be entered into a `2` contract long with a `2` contract sell (stop market, stop limit, or trailing stop) at `24060.25` on MNQ.&#x20;

{% hint style="danger" %}
**The take profit amount is not based on profit and loss on your portfolio, it's based on points on the underlying ticker.** If you type in `250` it doesn't mean $250 profit on your P/L. It means 250 points on MNQ which for 2 contract would be $1000 in loss on your P/L. It's up to you to figure out based on the number of contracts you're trading and the profit you want to achieve what value to write in the `amount` field.
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
