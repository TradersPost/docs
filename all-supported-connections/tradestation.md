---
description: >-
  TradeStation is a well known popular broker that supports stocks, stock
  options and futures. Build automated trading strategies using TradersPost on
  top of your TradeStation account.
---

# TradeStation

## Contact Information

Email: [clientservice@tradestation.com](mailto:clientservice@tradestation.com)

Phone: [+1 (800) 822-0512](tel:18008220512)

## Supported Asset Classes

* Stocks
* Options
* Futures

## Crypto Support

While TradeStation does support crypto, TradersPost has not integrated it with our platform yet but we plan to in the future. If you wish to see crypto support with TradeStation, please email us at [support@traderspost.io](mailto:support@traderspost.io) and let us know.

## MinMove/TickSize Data Discrepancy

If you encounter an order that gets rejected with a message like **Price = 1.19500000 not rounded to a valid price increment \[0.01]**, it is usually caused by a discrepancy with the data provided by TradeStation, which we use to ensure prices are rounded to the nearest valid increment.

You can check the `minMove` value used for price rounding by clicking the **Quote** button while viewing a trade.

```json5
{
    "source": "ts",
    "symbol": "RNAZ",
    "expirationDate": null,
    "ask": "1.2",
    "bid": "1.19",
    "last": "1.1912",
    "mark": "1.195",
    "minMove": {
        "threshold": 0,
        "below": "0.0001",
        "above": "0.0001"
    },
    "baseMinMove": null,
    "pointValue": "1",
    "updatedAt": "2025-03-21T14:05:01.000000+00:00",
    "status": "realtime"
}
```

In this example, TradeStation reports that the `minMove` is 4 decimal places (0.0001). However, when the order was placed, it was rejected with the message **"Price = 1.19500000 not rounded to a valid price increment \[0.01]"**. This is due to a data discrepancy for the ticker in question.

To resolve this issue, you need to call TradeStation at 1-800-822-0512 and report the problem so it can be escalated to their data integrity team to fix the issue.
