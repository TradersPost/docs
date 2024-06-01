---
description: >-
  This page documents the behavior of TradersPost when receiving different types
  of strategy signals.
---

# Order Behavior

## Buy

```json
{
    "ticker": "TSLA",
    "action": "buy"
}
```

* If there are open orders for TSLA, they will be canceled.
* If a short position is open for TSLA, then the open position will be exited with a Buy To Cover order and TradersPost will wait for the exit order to fill.
* If no long position is open for TSLA, then a Buy order will be sent.
* If there is no exit order, no entry order and no orders to cancel then the signal will be rejected.

## Sell

```json
{
    "ticker": "TSLA",
    "action": "sell"
}
```

* If there are open orders for TSLA, they will be canceled.
* If a long position is open for TSLA, then the open position will be exited with a Sell order and TradersPost will wait for the exit order to fill.
* If no short position is open for TSLA, then a Sell Short order will be sent.
* If there is no exit order, no entry order and no orders to cancel then the signal will be rejected.

## Limit Order

If you send a value in the price field then a limit order will be sent unless configured to be a market order in the strategy subscription configuration.

```json
{
    "ticker": "TSLA",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": 120.12
}
```

If you omit the `limitPrice` field in the JSON, then the resulting order will be limit order with the limit price set to the current market price.

## Quantity

Sending a quantity with your signal will work for both entries and exits. The quantity will only be used if you check the **Use signal quantity** checkbox in your strategy subscription.

### Entries

For entries, if you send a signal quantity and enable **Use signal quantity** in your strategy subscription, then the quantity from the signal will be used for your entry order.

```json
{
    "ticker": "TSLA",
    "action": "buy",
    "quantity": 5
}
```

If you omit the quantity field in the JSON, then the quantity will be dynamically calculated based on your strategy subscription configuration or if a quantity cannot be calculated, it will be defaulted to 1.

### Exits

Sending a quantity with your signal for exits looks the same and has the following behavior.

* If you send a quantity that is less than the total quantity of your open position, then a partial exit order will be submitted.
* If you send a quantity that is greater than or equal to the total quantity available, or you omit the quantity, then the full position will be exited.

```json
{
    "ticker": "TSLA",
    "action": "sell",
    "price": 700.00,
    "quantity": 5
}
```

## Partial Exits

You can't specify a quantity using `takeProfit` or `stopLoss` so instead you can partially exit a position like demonstrated on the example below. The first code block would be the entry, the second code block would be the partial exit.\
\
**Entry with 5 shares:**

```json
{
    "ticker": "TSLA",
    "action": "buy",
    "quantity": 5
}
```

**Partially exit 3 of the total 5 shares:**

```json
{
    "ticker": "TSLA",
    "action": "exit",
    "quantity": 3
}
```

## Sentiment

The JSON sentiment field in TradersPost allows you to specify what the sentiment of the position should be after executing the trade. When sending a webhook, you can include the `sentiment` field with a value of `flat` to exit a bullish or bearish position without entering the opposite position. This means that it will always exit the full quantity of the open position without entering a new position on the other side.

For example, if you send a JSON payload with `action` set to `sell` and `sentiment` set to `flat`, it will exit a bullish position without entering a bearish position. Similarly, if you send `action` as `buy` and `sentiment` as `flat`, it will exit a bearish position without entering a bullish position.

You are also able to have a `sentiment` of `bullish` or `bearish`. This is useful whenever you are partially exiting a position and you aren't fully exiting the position and you aren't changing sides. For example, if you are in a `bearish` short position with a quantity of 10 and you send a JSON payload with `action` set to `buy`, `quantity` set to `5` and sentiment set to `bearish`, this means that after executing the buy, you will still be in a `bearish` position with a quantity of 5.

## Add to position

You can add to existing open positions by enabling the **Allow add to position** checkbox in your strategy subscription.

Normally, if you for example have an existing open long position and you send another **buy** signal, the trade would be rejected. However, if you enable **Allow add to position**, then the signal won't be rejected and an order will be created to add to your existing position.

### Add Signal

Additionally, you can explicitly add to an existing position by using the **add** action. Here is an example where we add a quantity of 5 to the existing position. If no position is open then the trade will be rejected and no order will be sent to the broker.

```json
{
    "ticker": "TSLA",
    "action": "add",
    "price": 700.00,
    "quantity": 5
}
```

## Both Sides

When you receive a **buy** signal and you are trading both sides of a strategy, the following will happen:

* If there are open orders for TSLA, they will be canceled.
* If a short position is open for TSLA, then the open position will be exited with a **Buy To Cover** order and TradersPost will wait for the exit order to fill.
* If no long position is open for TSLA, then a **Buy** order will be sent.
* If there is no exit order, no entry order and no orders to cancel then the signal will be rejected.

The same is true for short positions. Here is what happens when you receive a **sell** signal:

* If there are open orders for TSLA, they will be canceled.
* If a long position is open for TSLA, then the open position will be exited with a **Sell** order and TradersPost will wait for the exit order to fill.
* If no short position is open for TSLA, then a **Sell to Open** order will be sent.
* If there is no exit order, no entry order and no orders to cancel then the signal will be rejected.

### Exiting Without Swapping Sides

If you have both sides enabled in your strategy subscription and you want to exit the open position without entering a new position on the other side, then you can use the **exit** action.

```json
{
    "ticker": "TSLA",
    "action": "exit",
    "price": 700.00
}
```

{% hint style="info" %}
When trading both sides of a strategy (bullish and bearish), TradersPost will wait for 2 minutes for the exit order to fill before submitting the entry order. If the exit order takes longer than 2 minutes to fill, the trade will fail and the exit order will remain open.
{% endhint %}

### Manually Manage Both Sides

You can accomplish the both sides functionality by manually managing the entries and exits on both sides yourself instead of relying on the TradersPost both sides functionality. Keep in mind you are responsible for waiting long enough in between exits and entries, otherwise your entry could get rejected due to the exit order not being filled yet.

{% hint style="warning" %}
It is important that if you setup a strategy in this way, that there is time in-between the exit and entry signals. If you send both the exit and entry signal at the same exact time, you may experience unexpected behavior.
{% endhint %}

#### **LONG**

To open a long position, send a **buy** action to the webhook.

```json
{
    "ticker": "TSLA",
    "action": "buy"
}
```

To exit a long position, send an **exit** action to the webhook.

```json
{
    "ticker": "TSLA",
    "action": "exit"
}
```

#### **SHORT**

To open a short position, send a **sell** action to the webhook.

```json
{
    "ticker": "TSLA",
    "action": "sell"
}
```

To exit a short position, send an **exit** action to the webhook.

```json
{
    "ticker": "TSLA",
    "action": "exit"
}
```

## Take Profit & Stop Loss

TradersPost has the ability to send take profit and stop loss orders with your initial entry order. This is useful for strategies where your entry, take profit and stop loss levels are all pre-defined and you want these orders to be sitting in your broker ahead of time.

{% hint style="warning" %}
If you are sending your take profit and stop loss to the broker with your entry order, it is recommended to not also have your strategy send duplicate exit signals to TradersPost when the take profit or stop loss level is hit in your strategy. Since the broker is executing your take profit & stop loss, there is no need to send a webhook to TradersPost to exit the position when the take profit or stop loss is hit in your strategy.
{% endhint %}

This functionality is only supported by brokers that support complex conditional order types that are often referred to as OTO (One Triggers Other), OSO (Order Sends Order), or OCO (One Cancels Other). It is currently supported by the following brokers within TradersPost.

* TradeStation
* Alpaca
* Tradier
* Tradovate
* Interactive Brokers

### How are take profit & stop loss orders calculated?

TradersPost supports the ability for you to send pre-calculated absolute prices for your take profit & stop loss or you can send relative values to us like a dollar amount or percentage and we will calculate the price to send to the broker.

For example, if you use a $10 stop loss amount and you enter at $100, then your stop loss stop price will be calculated at $90. If you buy 10 shares of a stock with an entry at $100 and a stop loss stop price at $90, then the most you can theoretically lose on the trade will be $100. Here is an example of how you could execute that trade:

```json
{
    "ticker": "TSLA",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": 100,
    "stopLoss": {
        "type": "stop",
        "amount": 10
    }
}
```

{% hint style="info" %}
When TradersPost calculates a take profit or stop loss price using a relative value like a dollar amount or percentage, the entry price we use to do the calculation will be the following in these scenarios:

* If limit order, we will use the price from the webhook signal or the midpoint price from the latest quote if the webhook signal does not have a price.
* If market order, we will use the midpoint price from the latest quote.
{% endhint %}

You can configure your strategy subscription to include your take profit & stop loss settings, or you can send your take profit & stop losses with your webhook signal. Take a look at the [Webhooks](../core-concepts/webhooks.md#signal-take-profit) documentation learn more about how to send your take profit & stop losses with your webhook signal.

## Min Move / Min Tick Size

Brokers often enforce what is a called a `Min Move` or `Min Tick Size.` This is a rule that controls how precise the price can be when sending orders to the broker. For example, the futures product `M6E` has a `Min Move` of `0.0001` (4 decimal places).

TradersPost will round prices to the nearest precision automatically for you so that the broker will not reject the order. For example, if you sent a `sell` signal with a price of `1.07375` and the `Min Move` is `0.0001` , then TradersPost will round the price up to `1.0738`.

{% hint style="info" %}
TradersPost will round up to the nearest precision for **sell** orders and down for **buy** orders. You can control the rounding on your side in your strategy and send a price with the exact precision to control the logic for rounding.
{% endhint %}

You can view what the `Min Move` value is in TradersPost by viewing the quote for the ticker you are trading.

<figure><img src="../.gitbook/assets/Screenshot 2023-09-06 at 8.24.35 AM.png" alt=""><figcaption></figcaption></figure>

This data can also be viewed in TradingView by clicking the three dots at the top of the chart and then clicking `Symbol Info` from the dropdown. Additionally, in TradingView PineScript, you can get what the `Min Move` is by using the `syminfo.mintick` variable.

<figure><img src="../.gitbook/assets/Screenshot 2023-09-06 at 8.29.22 AM.png" alt=""><figcaption></figcaption></figure>

## Trade Retries

We have the ability to retry trades that fail during trade planning. You can configure how many times to retry and how long to wait in between retries. This will only retry a trade if an API call fails when communicating with the broker during trade planning, it will not retry trades if the API fails after trade planning during execution. For example, if the broker API fails when we send an exit or entry order, we will not retry the trade. This is because we don't have a way currently to guarantee that the order creation did not actually succeed, even though we received a failure response back from the broker.

We will only retry trades that fail during trade planning if the broker API responds with one of the following status codes:

* 0 - Timeout / Network error
* 429 - Too Many Requests
* 500 - Internal Server Error
* 502 - Bad Gateway
* 503 - Service Unavailable
* 504 - Gateway Timeout

<figure><img src="https://2220089858-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FfaGHqKUfUy1dxnpnFnAi%2Fuploads%2Fi0hAhHEwhBLDvrjSaR9C%2FScreenshot%202023-08-28%20at%201.57.52%20PM.png?alt=media&#x26;token=7f94f8a5-0c55-4e04-b930-e735592d3635" alt=""><figcaption></figcaption></figure>

## Isolate Sides

In the strategy subscription settings you can check the `Isolate sides` checkbox so that when paired with the `Sides` dropdown, you can limit a strategy subscription from touching a position on the opposite side of the `Sides` you have selected.

For example, if you have `Sides` set to `Bullish` and `Isolate sides` checked, the strategy subscription will not be allowed to close a `Bearish` short position if there was one open. Or if you have `Sides` set to `Bearish` and `Isolate sides` checked, the strategy subscription will not be allowed to close a `Bullish` position if there was one open.

Without the `Isolate sides` checkbox checked, if you have an open position on the other side of your `Sides` selection, TradersPost will first close the open position before entering on the other side. With `Isolate sides` checked, TradersPost will not be able to exit the open position and therefore will not be able to enter a new position on the other side and the trade will be rejected with a message as such.
