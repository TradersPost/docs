# Paper Trading

Paper trading is a useful tool for being able to forward test your automated trading strategies without having to risk real money. TradersPost provides basic paper trading functionality in addition to working with paper trading provided by the brokers. However, not all brokers provide simulated paper trading environments.

**Please note that trading with paper money is only a simulation. It provides an approximation for what to expect in real live trading, but it is not a substitute for real live trading and your performance may differ.**

Below you will find information about the brokers that do provide paper trading in addition to the paper trading functionality provided by TradersPost.

## Alpaca

Alpaca offers paper trading for free to all Alpaca users.

> Paper trading is a real-time simulation environment where you can test your code. You can reset and test your algorithm as much as you want using free, real-time market data. Everything on the broker side behaves the same way as the live account except the orders aren’t routed to the real exchanges. Instead, the system simulates the order filling based on the real-time quotes.

You can read more about Alpaca paper trading [here](https://alpaca.markets/docs/trading-on-alpaca/paper-trading/). If you have questions about Alpaca paper trading, you can email [support@alpaca.markets](mailto:support@alpaca.markets).

## TradeStation

TradeStation offers paper trading for free to all TradeStation users.

> Test your trading strategies before you trade. Our simulated trading account allows you to test your strategies in real-time – without risking your capital. You also have access to one of the industry’s largest historical market databases, allowing you to back-test your stock, options, and futures trading strategies on decades of historical market data.

You can read more about TradeStation paper trading [here](https://www.tradestation.com/platforms-and-tools/simulated-trading/). If you have questions about TradeStation paper trading, you can email [ClientService@tradestation.com](mailto:ClientService@tradestation.com).

## TradersPost Paper

TradersPost offers a very basic paper trading functionality for testing your webhooks and strategies. Please note the following about TradersPost paper accounts:

* Market hours are not respected and orders will fill 24/7
* Limit orders will fill at any price specified
* Market orders will fill at the current market price

It is recommended that you use one of the above simulated paper trading environments provided by a broker if you want a more real simulated environment. The TradersPost paper trading functionality is only useful for testing that your webhooks and strategies are configured correctly but should not be used to measure the performance of your strategy.

If you have any other questions about paper trading on TradersPost, you can email [support@traderspost.io](mailto:support@traderspost.io).

## Other Brokers

Unfortunately, not all brokers support simulated paper trading environments. The following brokers that TradersPost supports do not offer paper trading functionality:

* Robinhood
* TDAmeritrade
