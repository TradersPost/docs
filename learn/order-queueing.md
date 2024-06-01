---
description: >-
  Order queueing is used when an order cannot be sent to the broker when the
  market is closed and TradersPost will queue these orders to be sent at the
  next market open.
---

# Order Queueing

TradersPost will queue trades and execute them at the next market open in certain scenarios. We do this in scenarios where the broker would otherwise reject the order and it is better to queue it on the TradersPost side and send it to the broker for execution at the next market open.

![Queued trade for the next market open.](<../.gitbook/assets/Trade Queueing.png>)

{% hint style="warning" %}
You are only allowed one queued trade per strategy subscription and ticker. If you send multiple trades for the same strategy subscription and ticker, previous older trades will be replaced with newer trades.
{% endhint %}
