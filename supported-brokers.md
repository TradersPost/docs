---
description: >-
  TradersPost supports several different brokers and we plan to continue adding
  more in the future.
---

# Brokers

## Supported Brokers

Here is a list of brokers that TradersPost currently integrates with and supports.

### Alpaca

![](.gitbook/assets/Alpaca-Full.png)

API for Stock Trading - Trade with algorithms, connect with apps, build services — all with commission-free stock trading API.

#### Supported Asset Classes

<table><thead><tr><th>Asset Class</th><th data-type="checkbox">Supported</th></tr></thead><tbody><tr><td>Stocks</td><td>true</td></tr><tr><td>Options</td><td>false</td></tr><tr><td>Futures</td><td>false</td></tr><tr><td>Crypto</td><td>false</td></tr><tr><td>Forex</td><td>false</td></tr></tbody></table>

### Robinhood

![](.gitbook/assets/Robinhood-Full.png)

Robinhood is a free-trading app that lets investors trade stocks, options, exchange-traded funds and cryptocurrency without paying commissions or fees.

#### Supported Asset Classes

<table><thead><tr><th>Asset Class</th><th data-type="checkbox">Supported</th></tr></thead><tbody><tr><td>Stocks</td><td>true</td></tr><tr><td>Options</td><td>false</td></tr><tr><td>Futures</td><td>false</td></tr><tr><td>Crypto</td><td>false</td></tr><tr><td>Forex</td><td>false</td></tr></tbody></table>

### TDAmeritrade

![](.gitbook/assets/TDAmeritrade-Full.png)

TD Ameritrade is a broker that offers an electronic trading platform for the trade of financial assets.

#### Supported Asset Classes

<table><thead><tr><th>Asset Class</th><th data-type="checkbox">Supported</th></tr></thead><tbody><tr><td>Stocks</td><td>true</td></tr><tr><td>Options</td><td>true</td></tr><tr><td>Futures</td><td>false</td></tr><tr><td>Crypto</td><td>false</td></tr><tr><td>Forex</td><td>false</td></tr></tbody></table>

#### Wash Sale Rule

TDAmeritrade will automatically adjust the cost basis of your positions if a previous loss on the same security has occurred in the last 30 days. This adjustment happens the night after you enter a position. The wash rule will run and the next day, the cost basis of your position will be adjusted and your avgerage entry price will not match the average fill price of the order that entered you in the position.

You can read more about how TDAmeritrade applies the wash sale rule [here](https://www.tdameritrade.com/investment-guidance/investment-management-services/tax-loss-harvesting/tax-loss-harvesting-wash-sales.html).

### TradeStation

![](.gitbook/assets/TradeStation-Full.png)

TradeStation offers state-of-the-art trading technology and online electronic brokerage services to active individual and institutional traders in the U.S. and worldwide.

<table><thead><tr><th>Asset Class</th><th data-type="checkbox">Supported</th></tr></thead><tbody><tr><td>Stocks</td><td>true</td></tr><tr><td>Options</td><td>true</td></tr><tr><td>Futures</td><td>true</td></tr><tr><td>Crypto</td><td>false</td></tr><tr><td>Forex</td><td>false</td></tr></tbody></table>

## Broker Roadmap

We plan to continually add more broker integrations to our system over time. Here are the brokers most immediately on our roadmap.

* [Interactive Brokers](https://www.interactivebrokers.com)
* [Coinbase Pro](https://pro.coinbase.com)
* [Fidelity](https://www.fidelity.com)
* [E-Trade](https://etrade.com)

If you would like to see your broker supported within TradersPost, please email us at [support@traderspost.io](mailto:support@traderspost.io) and let us know what you use.