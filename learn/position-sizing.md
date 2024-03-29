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
The position sizing features documented here are only for dynamically calculating quantities for entry orders and the **FULL** quantity of the open position is used for exit orders unless a quantity is explicitly sent in the signal and **Use signal quantity** is checked in the strategy subscription settings. You can read more about what can be sent in signals in the [Webhooks](../core-concepts/webhooks.md) page.
{% endhint %}

## Amount per position

The **Amount per position** field allows you to configure a fixed dollar amount to be used to calculate the quantity for your entry order.

```
quantity = amountPerPosition / entryPrice
```

## Risk per position

The **Risk per position** field allows you to configure a fixed risk dollar amount to be used to calculate the quantity for your entry order. This setting requires a stop loss to be configured.

```
difference = entryPrice > stopLossPrice
    ? entryPrice - stopLossPrice : stopLossPrice - entryPrice

quantity = riskPerPosition / difference 
```

## Percent of portfolio value

The **Percent of portfolio value** allows you to dynamically calculate an amount per position to use based on your portfolio value. This calculation does not use your total buying power/margin. It is only your total portfolio value minus any unrealized profits or losses.

```
portfolioValue = portfolioValue - unrealized

amountPerPosition = portfolioValue * percentOfPortfolioValue

quantity = amountPerPosition / entryPrice
```

If you want to use margin, you can use percentages that add up to greater than 100%. If you are trading 5 tickers, each with 25%, then you will use 125% of your total portfolio value which will require some margin.

{% hint style="info" %}
The **`entryPrice`** variable in the above examples use the price from the signal if limit orders are configured and uses the latest quote price when using market orders.\
\
If the signal does not have a price and limit orders are configured, then the latest quote price is used.
{% endhint %}

## Quantity

If you don't want to dynamically calculate a quantity, you can input a hardcoded fixed quantity to buy per signal in the **Quantity** field. TradersPost will pass this quantity directly to your broker.

## Use signal quantity

In addition to being able to dynamically calculate quantity. You can simply pass your quantity to use in the signal. You must check the **Use signal quantity** checkbox in order to tell TradersPost you want to use the quantity from the signal.\
\
If you have **Use signal quantity** unchecked then it will completely ignore the `quantity` field in the signal, even if it is hardcoded into a TradingView strategy for example.

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

## Screenshot

![Position Size Configuration](<../.gitbook/assets/Screen Shot 2022-08-17 at 10.06.27 PM.png>)

