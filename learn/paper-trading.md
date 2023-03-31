---
description: >-
  Paper trading is a useful tool for being able to forward test your automated
  trading strategies without having to risk real money.
---

# Paper Trading

TradersPost provides basic paper trading functionality in addition to working with paper trading provided by third-party brokers. However, not all brokers provide simulated paper trading environments.

**Please note that trading with paper money is only a simulation. It provides an approximation for what to expect in real live trading, but it is not a substitute for real live trading and your performance may differ.**

Below you will find information about the brokers that do provide paper trading in addition to the paper trading functionality provided by TradersPost.

## Alpaca

Alpaca offers paper trading for free to all Alpaca users.

> Paper trading is a real-time simulation environment where you can test your code. You can reset and test your algorithm as much as you want using free, real-time market data. Everything on the broker side behaves the same way as the live account except the orders aren’t routed to the real exchanges. Instead, the system simulates the order filling based on the real-time quotes.

You can read more about Alpaca paper trading [here](https://alpaca.markets/docs/trading-on-alpaca/paper-trading/). If you have questions about Alpaca paper trading, you can email [support@alpaca.markets](mailto:support@alpaca.markets).

[**Open Alpaca Account**](https://app.alpaca.markets/signup)****

## TradeStation

TradeStation offers paper trading for free to all TradeStation users.

> Test your trading strategies before you trade. Our simulated trading account allows you to test your strategies in real-time – without risking your capital. You also have access to one of the industry’s largest historical market databases, allowing you to back-test your stock, options, and futures trading strategies on decades of historical market data.

You can read more about TradeStation paper trading [here](https://www.tradestation.com/platforms-and-tools/simulated-trading/). If you have questions about TradeStation paper trading, you can email [ClientService@tradestation.com](mailto:ClientService@tradestation.com).

[**Open TradeStation Account**](https://getstarted2.tradestation.com/intro?offer=0147AFWX\&sales\_rep=AHayes)****

## TradersPost Paper

TradersPost offers a very basic paper trading functionality for testing your strategies. Please note the following about TradersPost paper accounts:

* Market hours are not respected and orders will fill 24/7.
* Limit orders will fill at any price specified.
* Market orders will fill at the middle point between the bid and the ask.

It is recommended that you use one of the above simulated paper trading environments provided by a broker if you want a more real simulated environment. The TradersPost paper trading functionality is only useful for testing that your strategies are configured correctly but should not be used to measure the performance of your strategy.

### Market Data Source

By default, TradersPost paper data is delayed and only supports stocks and futures. Additionally, the futures data can be delayed by over an hour and does not update in real-time. If you want the TradersPost paper broker to support options and have real-time data, you will need to connect a broker that supports options and has live data, like TDAmeritrade or TradeStation.

1. Go to **Brokers** and click **Connect Broker** and connect your TDAmeritrade account.
2. Once your TDAmeritrade account is connected, go back to **Brokers** and click **Edit** next to your TradersPost paper broker.
3. Choose your connected TDAmeritrade account in the **Market Data Source** dropdown and click **Save**. Now your TradersPost paper broker will use your TDAmeritrade account for live market data and will support the options asset class.

Here is a quick video showing you how to set this up.

{% embed url="https://www.youtube.com/watch?v=NK_AE2aTDrU" %}
How to Connect A Live Market Data Source To Your TradersPost Paper Broker
{% endembed %}

### Market Price Type

The TradersPost paper broker allows you to configure a `Market Price Type` so you can control which price to use as the current market price for market orders and open positions. By default TradersPost will use the `Bid-ask midpoint` price from the quote. The available options are as follows.

* **Bid-ask midpoint (default)** - This option will use the midpoint between the bid price and ask price.
* **Use ask for buys and bid for sells** - This option will use the quote ask price for buys and bid price for sells.
* **Always use ask** - This option will always use the quote ask price.
* **Always use bid** - This option will always use the quote bid price.
* **Use last price** - This option will always use the quote last price.

## Other Brokers

Unfortunately, not all brokers support simulated paper trading environments. The following brokers that TradersPost supports do not offer paper trading functionality.

* [Robinhood](https://robinhood.com/?utm\_source=traderspost)
* [TDAmeritrade](https://www.tdameritrade.com/?utm\_source=traderspost)

If you have any other questions about paper trading on TradersPost, you can email [support@traderspost.io](mailto:support@traderspost.io).
