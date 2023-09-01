---
description: >-
  This page documents the behavior of TradersPost when receiving different types
  of strategy signals.
---

# Order Behavior

{% hint style="info" %}
The details on this page are written under the context of buying and selling stocks. The behavior for other asset classes can vary depending on how your strategy is configured.
{% endhint %}

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

## Price

If you send a value in the price field then a limit order will be sent unless configured to be a market order in the strategy subscription configuration.

```json
{
    "ticker": "TSLA",
    "action": "buy",
    "price": 420.69
}
```

If you omit the price field in the JSON, then the resulting order will be limit order with the last quoted price if it exists or the ask for a buy and the bid for a sell.

## Quantity

Sending a quantity with your signal will work for both entries and exits. The quantity will only be used if you check the **Use signal quantity** checkbox in your strategy subscription.

![Use signal quantity checkbox.](<../.gitbook/assets/Use Signal Quantity Checkbox>)

### Entries

For entries, if you send a signal quantity and enable **Use signal quantity** in your strategy subscription, then the quantity from the signal will be used for your entry order.

```json
{
    "ticker": "TSLA",
    "action": "buy",
    "price": 600.00,
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

You can't specify a quantity using **take profit** or **stop loss** so instead you can partially exit a position like demonstrated on the example below. The first code block would be the entry, the second code block would be the partial exit.\
\
Entry:

```
{
    "ticker": "TSLA",
    "action": "buy",
    "quantity": 5
}
```

Partial Exit:

```
{
    "ticker": "TSLA",
    "action": "sell",
    "quantity": 3
}
```

## Sentiment

The JSON sentiment field in TradersPost allows you to specify what the sentiment of the position should be after executing the trade. When sending a webhook, you can include the `sentiment` field with a value of `flat` to exit a bullish or bearish position without entering the opposite position. This means that it will always exit the full quantity of the open position without entering a new position on the other side.

For example, if you send a JSON payload with `action` set to `sell` and `sentiment` set to `flat`, it will exit a bullish position without entering a bearish position. Similarly, if you send `action` as `buy` and `sentiment` as `flat`, it will exit a bearish position without entering a bullish position.

You are also able to have a `sentiment` of `bullish` or `bearish`. This is useful whenever you are partially exiting a position and you aren't fully exiting the position and you aren't changing sides. For example, if you are in a `bearish` short position with a quantity of 10 and you send a JSON payload with `action` set to `buy`, `quantity` set to `5` and sentiment set to `bearish`, this means that after executing the buy, you will still be in a `bearish` position with a quantity of 5.

## Add to position

You can add to existing open positions by enabling the **Allow add to position** checkbox in your strategy subscription.

![Allow add to position checkbox.](<../.gitbook/assets/Allow Add To Position Checkbox>)

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

**When trading both sides of a strategy, TradersPost requires that the exit be a market order. We will wait for 2 minutes for the market exit order to fill before submitting the entry order. If the exit order takes longer than 2 minutes to fill, the trade will fail and you will be notified via email and you will need to take manual action.**

### Manually Manage Both Sides

You can accomplish the both sides functionality by manually managing the entries and exits on both sides yourself instead of relying on the TradersPost both sides functionality. Keep in mind you are responsible for waiting long enough inbetween exits and entries, otherwise your entry could get rejected due to the exit order not being filled yet.

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

* Alpaca
* TradeStation
* TDAmeritrade
* Tradier

### How are take profit & stop loss orders calculated?

TradersPost supports the ability for you to send pre-calculated prices for your take profit & stop loss or you can send relative values to us like a dollar amount or percentage and we will calculate the price to send to the broker. For example, if you use a $10 stop loss amount and you enter at $100, then your stop loss stop price will be calculated at $90. If you buy 10 shares of a stock with an entry at $100 and a stop loss stop price at $90, then the most you can theoretically lose on the trade will be $100.

You can configure your strategy subscription to include your take profit & stop loss settings, or you can send your take profit & stop losses with your webhook signal. Take a look at the [Webhooks](webhooks.md#signal-take-profit) documentation learn more about how to send your take profit & stop losses with your webhook signal.
