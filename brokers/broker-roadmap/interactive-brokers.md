---
description: >-
  Interactive Brokers is a popular broker for international traders and they
  support stocks and futures. Build automated trading strategies using
  TradersPost on top of your Interactive Brokers account.
---

# Interactive Brokers

{% hint style="info" %}
COMING SOON
{% endhint %}

## Supported Asset Classes

<table><thead><tr><th width="363">Asset Class</th><th data-type="checkbox">Supported</th></tr></thead><tbody><tr><td>Stocks</td><td>true</td></tr><tr><td>Options</td><td>false</td></tr><tr><td>Futures</td><td>true</td></tr><tr><td>Crypto</td><td>false</td></tr><tr><td>Forex</td><td>false</td></tr></tbody></table>

## Daily Reset

The Interactive Brokers API has a daily "reset" window that occurs between 23:45 and 00:45 ET for the North America region. You can read more about the Interactive Brokers system status [here](https://www.interactivebrokers.com/en/software/systemStatus.php).

Since the Interactive Brokers API is basically unavailable during these windows and cannot be relied upon to execute automated trades, it is recommended to program your strategy to not send signals during these windows. If you send orders during these windows, it is possible that the trades will fail to execute, even with retries enabled.

## Quotes

The Interactive Brokers API does not have a reliable way to retrieve quotes for symbols, so prices are always required to be sent in the webhook signal when you want to submit limit orders. We are unable to fetch quotes to use the midpoint price as the limit price for limit orders.

