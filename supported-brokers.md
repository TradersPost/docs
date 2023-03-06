---
description: >-
  TradersPost supports several different brokers and we plan to continue adding
  more in the future.
---

# Supported Brokers

{% hint style="info" %}
If you do not see your broker listed here, please visit [this page](https://traderspost.io/brokers) and join the wait list for the broker that you want to use with TradersPost. If you do not see your broker listed, email us at [support@traderspost.io](mailto:support@traderspost.io).
{% endhint %}

## Supported Brokers

Here is a list of brokers that TradersPost currently integrates with and supports.

### Alpaca

API for Stock Trading - Trade with algorithms, connect with apps, build services — all with commission-free stock trading API.

[Countries supported by Alpaca](https://alpaca.markets/support/countries-alpaca-is-available)

{% hint style="danger" %}
While Alpaca does support crypto, TradersPost has not integrated it with our platform yet but we plan to in the future.\
\
<mark style="color:red;">Be aware that TradersPost will hide crypto orders and positions from the TradersPost UI but the</mark> <mark style="color:red;"></mark><mark style="color:red;">**Close All Positions**</mark> <mark style="color:red;"></mark><mark style="color:red;">and</mark> <mark style="color:red;"></mark><mark style="color:red;">**Cancel All Orders**</mark> <mark style="color:red;"></mark><mark style="color:red;">buttons in the TradersPost user interface will still close your crypto positions and cancel your crypto orders even though they are not visible in the TradersPost user interface.</mark>

\
It is recommended that you use a broker account that does not have other positions in it that were not created by TradersPost.
{% endhint %}

#### Supported Asset Classes

<table><thead><tr><th>Asset Class</th><th data-type="checkbox">Supported</th></tr></thead><tbody><tr><td>Stocks</td><td>true</td></tr><tr><td>Options</td><td>false</td></tr><tr><td>Futures</td><td>false</td></tr><tr><td>Crypto</td><td>false</td></tr><tr><td>Forex</td><td>false</td></tr></tbody></table>

### Robinhood

Robinhood is a free-trading app that lets investors trade stocks, options, exchange-traded funds and cryptocurrency without paying commissions or fees.

#### Supported Asset Classes

<table><thead><tr><th>Asset Class</th><th data-type="checkbox">Supported</th></tr></thead><tbody><tr><td>Stocks</td><td>true</td></tr><tr><td>Options</td><td>false</td></tr><tr><td>Futures</td><td>false</td></tr><tr><td>Crypto</td><td>false</td></tr><tr><td>Forex</td><td>false</td></tr></tbody></table>

#### Crypto & Options Support

{% hint style="info" %}
While Robinhood does support crypto and options, TradersPost has not integrated it with our platform yet but we plan to in the future.
{% endhint %}

### TDAmeritrade

TD Ameritrade is a broker that offers an electronic trading platform for the trade of financial assets.

#### Supported Asset Classes

<table><thead><tr><th>Asset Class</th><th data-type="checkbox">Supported</th></tr></thead><tbody><tr><td>Stocks</td><td>true</td></tr><tr><td>Options</td><td>true</td></tr><tr><td>Futures</td><td>false</td></tr><tr><td>Crypto</td><td>false</td></tr><tr><td>Forex</td><td>false</td></tr></tbody></table>

#### Wash Sale Rule

{% hint style="info" %}
TDAmeritrade will automatically adjust the cost basis of your positions if a previous loss on the same security has occurred in the last 30 days. This adjustment happens the night after you enter a position. The wash rule will run and the next day, the cost basis of your position will be adjusted and your avgerage entry price will not match the average fill price of the order that entered you in the position.

You can read more about how TDAmeritrade applies the wash sale rule [here](https://www.tdameritrade.com/investment-guidance/investment-management-services/tax-loss-harvesting/tax-loss-harvesting-wash-sales.html).
{% endhint %}

#### Futures Support

{% hint style="info" %}
While TDAmeritrade supports futures via the [ThinkOrSwim](https://www.tdameritrade.com/tools-and-platforms/thinkorswim.html) platform, they unfortunately do not allow futures trading through their API. If you would like to see TD Ameritrade support futures trading through their api, please email their support team at [api@tdameritrade.com](<mailto:api@tdameritrade.com >).
{% endhint %}

### TradeStation

TradeStation offers state-of-the-art trading technology and online electronic brokerage services to active individual and institutional traders in the U.S. and worldwide.

<table><thead><tr><th>Asset Class</th><th data-type="checkbox">Supported</th></tr></thead><tbody><tr><td>Stocks</td><td>true</td></tr><tr><td>Options</td><td>true</td></tr><tr><td>Futures</td><td>true</td></tr><tr><td>Crypto</td><td>false</td></tr><tr><td>Forex</td><td>false</td></tr></tbody></table>

{% hint style="info" %}
While TradeStation does support crypto and forex, TradersPost has not integrated it with our platform yet but we plan to in the future.
{% endhint %}

### Tradier

Tradier provides a full range of services in a scalable, secure, and easy-to-use REST-based API for businesses and individual developers. It’s unlike anything you’ve seen before.

<table><thead><tr><th>Asset Class</th><th data-type="checkbox">Supported</th></tr></thead><tbody><tr><td>Stocks</td><td>true</td></tr><tr><td>Options</td><td>true</td></tr><tr><td>Futures</td><td>false</td></tr><tr><td>Crypto</td><td>false</td></tr><tr><td>Forex</td><td>false</td></tr></tbody></table>

## Broker Roadmap

We plan to continually add more broker integrations to our system over time. Here are the brokers most immediately on our roadmap.

* [Interactive Brokers](https://traderspost.io/broker/ibkr)
* [Coinbase Pro](https://traderspost.io/broker/coinbasepro)
* [Fidelity](https://traderspost.io/broker/fidelity)

You can find the full list of supported brokers and broker wait lists [here](https://traderspost.io/brokers).

If you would like to see your broker supported within TradersPost, please email us at [support@traderspost.io](mailto:support@traderspost.io) and let us know what you use.
