---
description: >-
  TradersPost offers several different features for dynamically and manually
  managing your position size.
---

# Position Sizing

{% hint style="info" %}
TradersPost does not verify you have the buying power for an order and we depend on the broker accepting or rejecting the order based on your available buying power and the rules each broker implements surrounding buying power.
{% endhint %}

{% hint style="danger" %}
The position sizing features documented here are only for dynamically calculating quantities for entry orders and the **FULL** quantity of the open position is used for exit orders unless a quantity is explicitly sent in the signal and **Use signal quantity** is checked in the strategy subscription settings. You can read more about what can be sent in signals in the [Webhooks](../../core-concepts/signals/webhooks.md) page.
{% endhint %}

## Amount per position

The **Amount per position** feature allows you to configure a fixed dollar amount to be used to calculate the quantity for your entry order.

```
quantity = amountPerPosition / entryPrice
```

Here is an example of how you can control this feature from the webhook JSON. This example would calculate a quantity of `10` with an entry limit price of `$100` and an amount per position of `$1000`.

```json
{
    "ticker": "TSLA",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": 100,
    "quantityType": "amount_per_position",
    "quantity": 1000
}
```

## Risk per position

The **Risk per position** feature allows you to configure a fixed risk dollar amount to be used to calculate the quantity for your entry order. This setting requires a stop loss to be configured.

```
difference = entryPrice - stopLossPrice

quantity = riskPerPosition / difference 
```

Here is an example of how you can control this feature from the webhook JSON. This example would calculate a quantity of `10` with an entry limit price of `$100` and a stop loss stop price of `$90` and a risk per position of `$100`. Since the most we want to lose is $100, then we can afford to buy `10` shares.

```json
{
    "ticker": "TSLA",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": 100,
    "stopLoss": {
        "type": "stop",
        "stopPrice": 90
    },
    "quantityType": "risk_per_position",
    "quantity": 100
}
```

## Percent of equity

The **Percent of equity** feature allows you to dynamically calculate an amount per position to use based on your total portfolio equity. This calculation does not use your total buying power/margin. It is only your total portfolio value minus any unrealized profits or losses.

```
portfolioValue = portfolioValue - unrealized

amountPerPosition = portfolioValue * percentOfPortfolioValue

quantity = amountPerPosition / entryPrice
```

If you want to use margin, you can use percentages that add up to greater than 100%. If you are trading 5 tickers, each with 25%, then you will use 125% of your total equity which will require some margin.

Here is an example of how you can control this feature from the webhook JSON. Assuming you have a `$100000` account, this example would calculate a quantity of `10` with an entry limit price of `$100` and a percent of equity `1%`. If you have a `$100000` account and you want to use `1%` of it, then you have `$1000` to spend which means at a entry limit price of `$100`, we will calculate a quantity of `10`.

```json
{
    "ticker": "TSLA",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": 100,
    "quantityType": "percent_of_equity",
    "quantity": 1
}
```

{% hint style="info" %}
The **`entryPrice`** variable in the above examples use the price from the signal if limit orders are configured and uses the latest quote price when using market orders.\
\
If the signal does not have a price and limit orders are configured, then the latest quote price is used.
{% endhint %}

## Fixed Quantity

If you don't want to dynamically calculate a quantity, you can used the fixed quantity feature. You can configure a fixed quantity in your strategy subscription settings or send it a long in your webhook JSON. Here is an example that will buy 5 shares of TSLA.

```json
{
    "ticker": "TSLA",
    "action": "buy",
    "orderType": "market",
    "quantity": 5
}
```

{% hint style="info" %}
For entries, TradersPost will buy a quantity of **1** if no quantity is provided in the signal and no dynamic quantity calculation is configured in your strategy subscription settings.

For exits, TradersPost will exit the **FULL** quantity of the open position in the broker if you do not provide a quantity to exit in the signal.
{% endhint %}

## Subtract exit quantity from signal quantity

Sometimes when you are flipping from one side to the other, for example long to short, you need to send the full quantity to exit the current open position and use the remaining quantity to enter a new position on the other side. Check the **Subtract exit quantity from signal quantity** checkbox to enable this behavior.

Now if you were long a quantity of 5, you can send a signal like the following to exit the 5 long and enter 3 short.

```json
{
    "ticker": "TSLA",
    "action": "sell",
    "sentiment": "bearish",
    "quantity": 8
}
```

## Use fractional quantity

By default TradersPost will round decimal quantity to a whole number. If you check the **Use fractional quantity** checkbox then we will pass the fractional quantity to the broker if the broker supports it. We will round the decimal to the number of decimal places the broker supports. You can read more about fractional shares [here](fractional-shares.md).
