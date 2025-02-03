---
description: >-
  This page provides an overview of the different order classes available in
  TradersPost and it explains the functionalities and use cases of these orders.
---

# Order Classes

### Simple

A simple order is a single order (entry or exit) that is submitted to the broker. It is the most basic order class. All brokers supported by TradersPost support this kind of order class.

### Bracket (OTOCO)

A bracket order is a chain of three orders that can be used to manage your position entry and exit. It is a common use case of an OTOCO (One Triggers OCO {One Cancels Other}) order.

#### Supported Brokers

* TradeStation
* Alpaca
* Tradier
* Tradovate
* NinjaTrader
* tastytrade
* Interactive Brokers

#### Unsupported Brokers

* Robinhood
* Coinbase
* E\*TRADE
* Bybit
* Kraken
* Binance

### One-Triggers-Other (OTO)

OTO (One-Triggers-Other) is a variant of bracket order. It takes one of the take-profit or stop-loss order in addition to the entry order. For example, if you want to set only a stop-loss order attached to the position, without a take-profit, you may want to consider OTO orders.

#### Supported Brokers

* TradeStation
* Alpaca
* Tradier
* Tradovate
* NinjaTrader
* Interactive Brokers

#### Unsupported Brokers

* Robinhood
* Coinbase
* E\*TRADE
* tastytrade
* Bybit
* Kraken
* Binance

{% hint style="info" %}
When using a broker that supports OTOCO (One-Triggers-One-Cancels-Other) but not OTO (One-Triggers-Other), you must submit both a take profit and a stop loss with your entry order. Submitting only a take profit or a stop loss is not permitted
{% endhint %}

### One-Cancels-Other (OCO)

OCO (One-Cancels-Other) is another type of advanced order type. This is a set of two orders with the same side (buy/buy or sell/sell). In other words, this is the second part of the bracket orders where the entry order is already filled, and you can submit the take-profit and stop-loss in one order submission.

{% hint style="warning" %}
TradersPost only supports this order class as a part of a bracket order. We do not support submitting an OCO order for an already open position. You can submit take profit and stop loss orders for existing open positions, but they will not be tied together as an OCO.
{% endhint %}

