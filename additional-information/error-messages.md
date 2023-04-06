---
description: >-
  This page documents all the common error messages that you may receive in
  TradersPost and what they mean.
---

# Error Messages

### You are required to select at least one account.

When editing a connected broker, you are required to select at least one live or paper account.\
\
If you get this error message for a recently created TradeStation broker, you will have to wait 24 hours for TradeStation to fully provision your account before you will be able to connect it to TradersPost.

### Failed to save

If you get an error message when trying to save a form with a message like **Failed to save trading strategy subscription**. Scroll down on the form to look for the specific field that has the error on it so that you can correct the error.

### TradersPost broker does not support options.

If you get an error about the TradersPost paper broker not supporting options, this is because the TradersPost paper broker does not support options data by default out of the box. You will need to connect a broker that has live options data in order to trade options with the TradersPost paper broker. You can read more about this [here](../learn/paper-trading.md#market-data-source).

### Broker does not support asset class

Not all brokers support all asset classes, so you get errors like the following when trying to save a strategy subscription.

* Robinhood does not support options.
* TDAmeritrade does not support futures.

You will get this error when trying to connect a broker to a strategy where the broker does not support the asset class the strategy trades. This error cannot be fixed and you will have to connect a broker which supports the asset class you want to trade.

### You do not have access to trade stocks

* You do not have access to trade stocks. Go to your account settings to enable stocks trading.
* You do not have access to trade options. Go to your account settings to enable options trading.
* You do not have access to trade futures. Go to your account settings to enable futures trading.

If you get an error message like the above when editing a strategy subscription this is because you have not enabled the asset class in your account yet. Navigate to your dashboard by clicking the TradersPost logo at the top left and then clicking **Asset Classes** underneath **My Account** and then enable the asset class you want to trade.

### TradersPost does not currently support take profit orders

The TradersPost paper broker does not currently support take profit orders. This is a limitation only with the TradersPost paper broker. Other brokers like TDAmeritrade, Tradier, TradeStation and Alpaca support take profit orders.

### TradersPost does not currently support stop loss orders

The TradersPost paper broker does not currently support stop loss orders. This is a limitation only with the TradersPost paper broker. Other brokers like TDAmeritrade, Tradier, TradeStation and Alpaca support stop loss orders.

### Entry market orders cannot be submitted in extended hours

Extended hours require limit orders so you cannot use market orders for entries when trading with extended hours enabled.

### Exit market orders cannot be submitted in extended hours

Extended hours require limit orders so you cannot use market orders for exits when trading with extended hours enabled.

### Both sides cannot be used with exit extended hours

You cannot trade both sides with extended hours enabled because both sides requires that the exit order be a market order. Since we cannot enter a new position on the other side if the open position is not exited, we require a market order to exit so that we can have a high likelyhood that the open position will be exited before trying to send the order to enter a new position on the other side. TradersPost will wait for the market exit order to fully fill before we send the next order to enter a new position on the other side.

### Futures cannot be used with extended hours

Extended hours is for stocks only. Futures do not have an extended hours session so you don't need to check extended hours checkboxes when trading futures.
