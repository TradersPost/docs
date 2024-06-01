---
description: >-
  TDAmeritrade is a well known popular broker that supports both stocks and
  stock options. Build automated trading strategies using TradersPost on top of
  your TDAmeritrade account.
---

# TDAmeritrade

{% hint style="danger" %}
The TDAmeritrade integration is no longer active and available and unfortunately, Schwab has thus far rejected our application to integrate TradersPost with them. We hope this changes in the future but right now Schwab is not available. Please email [traderapi@schwab.com](<mailto:traderapi@schwab.com >) to let them know you would like to use your Schwab accounts with TradersPost.
{% endhint %}

## Contact Information

Email: [api@tdameritrade.com](mailto:api@tdameritrade.com)

Phone: [+1 (800) 669-3900](tel:18006693900)

## Supported Asset Classes

* Stocks
* Options

## Wash Sale Rule

TDAmeritrade will automatically adjust the cost basis of your positions if a previous loss on the same security has occurred in the last 30 days. This adjustment happens the night after you enter a position. The wash rule will run and the next day, the cost basis of your position will be adjusted and your avgerage entry price will not match the average fill price of the order that entered you in the position.

You can read more about how TDAmeritrade applies the wash sale rule [here](https://www.tdameritrade.com/investment-guidance/investment-management-services/tax-loss-harvesting/tax-loss-harvesting-wash-sales.html).

## Futures Support

While TDAmeritrade supports futures via the [ThinkOrSwim](https://www.tdameritrade.com/tools-and-platforms/thinkorswim.html) platform, they unfortunately do not allow futures trading through their API. If you would like to see TDAmeritrade support futures trading through their API, please email their support team at [api@tdameritrade.com](<mailto:api@tdameritrade.com >).

## Schwab Migration

Once your account has been migrated to Schwab from TDAmeritrade, you will unfortunately no longer be able to use TradersPost with TDAmeritrade or Schwab. TDAmeritrade has started migrating accounts to Schwab before the new Schwab API is ready and available for TradersPost to integrate with and they don't have a concrete date on when the Schwab API will be available for us to integrate.

The only solution at this time is to migrate your trading to a different broker such as Alpaca, TradeStation, Tradier or Robinhood.

If you have questions about the transition from TDAmeritrade to Schwab, you can call the TDAmeritrade to Schwab transition team at [+1 800-780-8614](tel:18007808614).
