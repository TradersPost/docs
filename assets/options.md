# Options

{% hint style="info" %}
**Coming Soon!** Options trading is currently only available for paper trading. If you would like to apply to be a part of the options beta, email [support@traderspost.io](mailto:support@traderspost.io).
{% endhint %}

## Symbol Format

TradersPost understands many different stock options symbol formats. Since every broker and trading platform has subtle differences in the format we try to be as flexible as possible.

| Symbol           | Type                      |
| ---------------- | ------------------------- |
| TSLA 210121C325  | TradeStation, TradersPost |
| TSLA\_210121C325 | TD Ameritrade             |

## Supported Brokers

Currently we support stock options trading through the following brokers.

| Broker        | Live | Paper |
| ------------- | ---- | ----- |
| TD Ameritrade | Yes  | No    |
| TradeStation  | Yes  | Yes   |

## Supported Option Types

When setting up a strategy within TradersPost you will have the ability to choose what kind of option to buy or sell when signals are received.

* **Both** - Buy calls when bullish (action=buy) and buy puts when bearish (action=sell).
* **Call** - Buy calls when bullish (action=buy) and sell calls when bearish (action=sell).
* **Put** - Buy puts when bearish (action=sell) and sell puts when bullish (action=buy.

{% hint style="info" %}
It can be a little confusing that when you configure a strategy to use puts, an action of sell will actually buy puts and an action of buy will sell puts. Essentially, a buy action indicates a bullish sentiment and a sell signal indicates a bearish sentiment.
{% endhint %}

