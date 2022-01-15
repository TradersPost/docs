---
description: >-
  Order queueing is used when an order cannot be sent to the broker when the
  market is closed and TradersPost will queue these orders to be sent at the
  next market open.
---

# Order Queuing

## Both Sides

If the trade plan has both an exit and entry order. We do this because we have to wait for the exit order to fill before being able to submit the entry order. If we submit the market exit order when the market is closed, the order will never fill or may be rejected by the broker.

## Regular Orders in Extended Hours

If the trade plan has an exit or entry order, they are regular non extended hours orders and the broker does not support sending regular orders in extended hours. These are the brokers which do not support sending non extended hours orders after close.

### Alpaca

Alpaca doesn’t directly enforce any timing rules. They simply accept all orders and then route them to one of several execution partners. Each partner has slightly different rules. Some of these partners may reject non extended hours orders in extended hours after Alpaca accepts the order and sends it to the partner. This means that non extended hours orders sent in extended hours may get rejected but not always. Because of this, we will queue these trade orders and send them to Alpaca at the start of the next market open.
