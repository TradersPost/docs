---
description: >-
  Paper trading is a useful tool for being able to forward test your automated
  trading strategies without having to risk real money.
---

# Paper Trading

TradersPost provides basic paper trading functionality in addition to working with paper trading provided by third-party brokers. However, not all brokers provide simulated paper trading environments.

{% hint style="info" %}
Please note that trading with paper money is only a simulation. It provides an approximation for what to expect in real live trading, but it is not a substitute for real live trading and your performance may differ.
{% endhint %}

The following brokers supported by TradersPost currently support paper trading.

* **TradeStation** - has delayed fills and market data sometimes
* **Alpaca** - realtime fills and realtime market data
* **Tradier** - 15 minutes delayed
* **Tradovate** - realtime fills and no market data
* **Interactive Brokers** - realtime fills and market data
* **Bybit** - realtime fills and market data

## TradersPost Paper

TradersPost offers a very basic paper trading functionality for testing your strategies. Please note the following about TradersPost paper accounts:

* Market hours are not respected and orders will fill 24/7.
* Limit orders will fill at any price specified.
* Market orders will fill at the middle point between the bid and the ask.
* Options and futures contract positions will not expire and be removed from your open positions. Open positions for expired contracts will remain open until they are closed.

It is recommended that you use one of the above simulated paper trading environments provided by a broker if you want a more real simulated environment. The TradersPost paper trading functionality is only useful for testing that your strategies are configured correctly but should not be used to measure the performance of your strategy.

### Market Data Source

The TradersPost paper broker supports all asset classes, but the futures asset class does not come with data by default. If you want the TradersPost paper broker to have real-time futures data, you will need to connect a broker such as TradeStation that supports futures and has live data and set is as the market data source for your TradersPost paper broker.

{% hint style="info" %}
You must have live market data available with your broker before this feature will work. If you connect a broker that doesn't provide you with live market data (typically that you have paid for), then the data and pricing will still be delayed.
{% endhint %}

#### Using a Supported Broker for Market Data

1. Once your TradeStation account is connected, go back to **Brokers** and click **Edit** next to your TradersPost paper broker.
2. Choose your connected TradeStation account in the **Market Data Source** dropdown and click **Save**. Now your TradersPost paper broker will use your TradeStation account for live market data and will fully support the futures asset class.

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

When market orders are filled, the configured option will be used to fill the paper orders and open positions will use that price as the position current price.

### Reset Paper Broker

You can reset the TradersPost paper broker account balances, orders and positions by navigating to **Connected Brokers** and then click the **Reset** button next to the TradersPost paper broker you want to reset.

## Brokers

Unfortunately, not all brokers support simulated paper trading environments. If your current broker does not support paper trading, try another one of our supported brokers.

If you have any other questions about paper trading on TradersPost, you can email [support@traderspost.io](mailto:support@traderspost.io).
