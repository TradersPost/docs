---
description: >-
  This page documents the behavior of TradersPost when receiving different types
  of strategy signals.
---

# Order Behavior

## Buy TSLA

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

## Sell TSLA

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

![Use signal quantity checkbox.](<.gitbook/assets/Use Signal Quantity Checkbox>)

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

## Add to Position

You can add to existing open positions by enabling the **Allow add to position** checkbox in your strategy subscription.

![Allow add to position checkbox.](<.gitbook/assets/Allow Add To Position Checkbox>)

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

The ability to take both the **long** and **short** side of a strategy in one strategy subscription is only available in paper accounts at the moment. If you would like to have both sides enabled in live accounts, please email [support@traderspost.io](mailto:support@traderspost.io).

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

#### **LONG**

To open a long position, send a **buy** action to the webhook.

```
{
    "ticker": "TSLA",
    "action": "buy"
}
```

To exit a long position, send an **exit** action to the webhook.

```
{
    "ticker": "TSLA",
    "action": "exit"
}
```

#### **SHORT**

To open a short position, send a **sell** action to the webhook.

```
{
    "ticker": "TSLA",
    "action": "sell"
}
```

To exit a short position, send an **exit** action to the webhook.

```
{
    "ticker": "TSLA",
    "action": "exit"
}
```
