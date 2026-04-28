# Getting Started

TradersPost is a cloud-based, no-code, event-driven trading automation platform that allows you to turn your [trade signals](core-concepts/signals.md) into executed orders across one or multiple broker, exchange, or prop firm accounts.

* It's **cloud-based**, meaning that your trades execute even when you're offline. No need to keep your computer running or your browser open. Our servers process your signals 24/7, securely routing orders to your connected brokers or exchanges.
* It's **no-code**, meaning that you don't need to write any software or have any programming knowledge to automate your trading. You can connect signals from platforms like TradingView, TrendSpider, and others directly to your broker accounts using simple configuration tools.
* It's **event-driven**, meaning that your trades are executed automatically in real-time the moment your signal is triggered. Instead of monitoring charts or waiting for price levels manually, you define the conditions once, and TradersPost handles the execution based on live incoming alerts.

_**Our mission is simple: to help you transform trade ideas into executed orders, effortlessly.**_

With powerful tools like dynamic take profit and stop loss management, automated position size adjustments, and an options contract screener, TradersPost simplifies and optimizes your trading workflow.

Whether you're a discretionary trader who wants help managing trade execution or a systematic trader running fully automated strategies, TradersPost gives you full control over how signals are processed and routed to your connected accounts.

We empower traders to automate strategies and scale accounts from platforms like [TradingView](learn/signal-sources/tradingview.md), [TrendSpider](learn/signal-sources/trend-spider.md), our own [Command Pad](core-concepts/command-pad.md), and custom programmatic and agentic approaches. With seamless integrations to brokers such as [TradeStation](all-supported-connections/tradestation.md), [Tradier](all-supported-connections/tradier.md), [Robinhood](all-supported-connections/robinhood.md), [Alpaca](all-supported-connections/alpaca.md), and [many more](https://traderspost.io/connections), TradersPost supports trading across Futures, Futures Prop Firms, Stocks, Options, and Crypto.

## How It Works: The Basics

{% embed url="https://youtu.be/kLJqB4Qpbvo" %}

It's important to understand a few core concepts in TradersPost. Terms like strategies, subscriptions, JSON messages, webhooks, connections, and signals might sound unfamiliar at first, but once you start using the platform, these building blocks will quickly become second nature.

{% stepper %}
{% step %}
[**Brokers (Connections)**](core-concepts/brokers-connections.md)**: Connect a Broker, Exchange, or Prop Firm Account**

Link your live, paper, or prop firm accounts directly to TradersPost through our [supported connections](https://traderspost.io/connections).
{% endstep %}

{% step %}
**Create a** [**Strategy**](core-concepts/strategies.md)

Your strategy defines your asset class, trading style, allowed tickers, security settings, and provides you with a unique webhook URL.
{% endstep %}

{% step %}
**Create a** [**Subscription**](core-concepts/subscriptions.md)

Each subscription connects one broker account to your strategy, applying account-specific settings like position size, overrides, and auto submit preferences.
{% endstep %}

{% step %}
**Send** [**Trading Signals**](core-concepts/signals.md) **via** [**Webhook**](core-concepts/webhooks.md)

From your external platform (like TradingView or TrendSpider), send a [JSON message](core-concepts/signals/signal-template-creator.md) to your strategy’s [webhook URL](core-concepts/webhooks.md). TradersPost parses this message and routes the trade to your connected broker or exchange using the settings defined in your subscription.

You can also send signals directly from [Command Pad](core-concepts/command-pad.md), a trading tool we built to help discretionary traders, but also give you an interface to test signals before using them in your automated approach.
{% endstep %}
{% endstepper %}

That’s the foundation. From here, you can explore how to customize risk management and build multi-account setups. Head to the core concepts on the left to get a better understanding of these main components of the platform.

## Why Automation?

Automation allows you to remove emotion, improve consistency, and scale your trading across multiple accounts at once. You can use TradersPost to:

* Run fully automated trading systems that execute signals as soon as they fire.
* Mirror your trades across multiple live, paper, or prop firm accounts simultaneously.
* Reduce manual errors, delayed entries, and inefficient order routing.

## Who TradersPost Is For?

* **Systematic Traders**: Automate strategies using TradingView, TrendSpider, or other signal providers.
* **Discretionary Traders**: Set up guardrails, semi-automation, and manage trade approval while preserving full control.
* **Prop Firm Traders**: Connect and automate evaluation or funded accounts across supported prop firms.

TradersPost is designed exclusively for independent traders, meaning each user maintains full control over their own accounts, signal sources, strategy settings, risk management, and trade automation. Even when using third-party indicators or strategies, you are responsible for configuring your own broker connections, subscriptions, and automation preferences.

## Key Limitations

* **Not Designed for High-Frequency or Sub-Minute Trading**\
  TradersPost is not intended for ultra-short-term scalping or high-frequency trading strategies operating below the 1-minute timeframe. We have rate limits in place to prevent abuse to our webhook system. Read more about our [rate limiting behavior](learn/platform-concepts/rate-limits.md). Signal speed is largely contingent on where your signal comes from and how quickly it can send the request to the TradersPost webhook server. The average webhook response is delivered in 80 milliseconds. Please read our article on [Signal Speed](learn/signal-speed.md) to learn more about how fast trades can be sent to one or many accounts.
* **Signal Conflicts (Race Conditions)**\
  Since TradersPost operates as an event-driven system, it's the trader’s responsibility to ensure that multiple signals do not conflict with one another. Overlapping signals may lead to unintended trade behavior if strategy logic doesn't account for open positions, pending orders, or rapidly changing market conditions.
* **No Broker State or Order Feedback Loop**\
  TradersPost does not currently provide broker or exchange order IDs, position state, or account-level information for use in strategy logic. We strongly encourage users to maintain strategy state and trade logic externally on platforms like TradingView, or via direct broker APIs in their own environment. TradersPost focuses strictly on signal routing and execution based on externally provided webhook signals.
* **Not a "Set-It-and-Forget-It" Platform**\
  TradersPost is designed to automate the execution of trading strategies, but it is not a fully autonomous, self-healing system. Things can and will go wrong. Users are responsible for actively monitoring their signals, trading rules, open positions, and broker connections. Signal misfires, failed payments, or broker-side issues can disrupt execution. We strongly recommend checking your account regularly, especially after configuration changes or while away from active trading, to ensure everything is operating as intended.
