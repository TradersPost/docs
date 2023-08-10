---
description: >-
  TDAmeritrade is a well known popular broker that supports both stocks and
  stock options. Build automated trading strategies using TradersPost on top of
  your TDAmeritrade account.
---

# TDAmeritrade

## Contact Information

Email: [api@tdameritrade.com](mailto:api@tdameritrade.com)

Phone: [+1 (800) 669-3900](tel:18006693900)

## Supported Asset Classes

<table><thead><tr><th>Asset Class</th><th data-type="checkbox">Supported</th></tr></thead><tbody><tr><td>Stocks</td><td>true</td></tr><tr><td>Options</td><td>true</td></tr><tr><td>Futures</td><td>false</td></tr><tr><td>Crypto</td><td>false</td></tr><tr><td>Forex</td><td>false</td></tr></tbody></table>

## Wash Sale Rule

TDAmeritrade will automatically adjust the cost basis of your positions if a previous loss on the same security has occurred in the last 30 days. This adjustment happens the night after you enter a position. The wash rule will run and the next day, the cost basis of your position will be adjusted and your avgerage entry price will not match the average fill price of the order that entered you in the position.

You can read more about how TDAmeritrade applies the wash sale rule [here](https://www.tdameritrade.com/investment-guidance/investment-management-services/tax-loss-harvesting/tax-loss-harvesting-wash-sales.html).

## Futures Support

While TDAmeritrade supports futures via the [ThinkOrSwim](https://www.tdameritrade.com/tools-and-platforms/thinkorswim.html) platform, they unfortunately do not allow futures trading through their API. If you would like to see TDAmeritrade support futures trading through their API, please email their support team at [api@tdameritrade.com](<mailto:api@tdameritrade.com >).

## Schwab Migration
