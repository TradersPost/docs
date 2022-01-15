---
description: >-
  TradersPost supports trading in fractional share quantities with brokers that
  support it. The following brokers support fractional trading:
---

# Fractional Shares

## Support Brokers

* **Alpaca** - supports 6 decimal places. You can read more about Alpaca fractional trading [here](https://alpaca.markets/docs/trading-on-alpaca/fractional-trading/).
* **Robinhood** - supports 9 decimal places. You can read more about Robinhood fractional trading [here](https://robinhood.com/us/en/support/articles/fractional-shares/).
* **TradersPost Paper** - supports 9 decimal places

You can trade fractional shares by entering a fractional quantity with a decimal or by entering a dollar amount to buy and the fractional quantity will be calculated for you.

## Behavior

Here are some notes on fractional trading behavior to consider when trading fractional shares:

* Fractional buy and sell orders must be simple good for day market orders
* Fractional orders cannot have stop loss or take profits.
* Fractional orders cannot be short.
* Fractional quantities will be rounded down to the number of decimal places the broker supports.

## Strategy Subscriptions

If you want to use fractional shares in your automated strategy subscriptions, you just need to check the `Use fractional quantity` checkbox in your strategy subscription.

![Use fractional quantities in your strategy subscriptions.](<.gitbook/assets/Use Fractional Quantity Checkbox>)
