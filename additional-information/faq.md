---
description: Get answers to the most frequently asked questions about TradersPost.
---

# Frequently Asked Questions

### Do you support paper trading?

Yes, TradersPost supports paper trading with multiple different brokers. Read more [here](../paper-trading.md).

### Can I paper trade with TD Ameritrade?

TD Ameritrade does not support paper trading. Only the ThinkOrSwim platform supports paper trading and ThinkOrSwim does not provide an API for TradersPost to integrate with. If you would like to get started paper trading, you can register a free account with [Alpaca](../paper-trading.md#alpaca) or [TradeStation](../paper-trading.md#tradestation) or use the [TradersPost Paper Trading](../paper-trading.md#traderspost-paper) functionality.

### Does TradersPost require coding?

No. TradersPost does not require coding. You can easily connect strategies to TradersPost that other traders have created and published on [TradingView](https://cdn.traderspost.io/images/TradingView.png). Or you can use a platform like [TrendSpider](https://trendspider.com/?\_go=traderspost) which allows you to build strategies without code.

### Can I trade both long and short?

Yes, TradersPost supports trading both the long and short sides of a strategy.

### Do you support crypto?

Not yet, but it is on the roadmap for 2023.

### Do you support futures?

Yes, futures support is available and can be enabled in your account settings.

### Do you support options?

Yes, options support is in beta and can be enabled in your account settings.

### What brokers do you support?

TradersPost currently integrates with TD Ameritrade, Alpaca, TradeStation and Robinhood.

### Can I trade my IRA?

Yes, TD Ameritrade and TradeStation both support specialty account types like IRA (retirement), business and other specialty account types.

### What happens to existing positions when I connect my broker

If you connect an account with existing open positions, TradersPost will not do anything to those positions unless your strategy subscription has those tickers selected. It is up to you to be sure your manual trading does not conflict with the tickers being managed by TradersPost. It is recommended that you use an account dedicated to TradersPost but we do not strictly disallow you from trading manually in the same account.

### How old is TradersPost?

TradersPost was founded by [Jonathan Wage](https://www.linkedin.com/in/jwage/) on January 1st 2021.

### Is TradersPost free?

TradersPost is free to get started. You can paper trade for free for 90 days. Once you are ready to trade live with real money, a paid subscription is required.

### I don't have a supported broker, how can I get started?

TradersPost comes with a free paper account that lets you test strategies and get familiar with the platform.

### Does TradersPost support ThinkOrSwim?

Yes, we support TD Ameritrade accounts with ThinkOrSwim advanced features disabled. If you have ThinkOrSwim advanced features enabled, you may experience unexpected behavior and you will not have the ability to use OCO take profit and stop loss orders. It is recommended to use TradersPost with accounts that have ThinkOrSwim advanced features disabled.

### Do you have an API?

No, but it is on our 2023 roadmap. The only way currently to integrate strategies with TradersPost is via [Webhooks](../webhooks.md).

### Are trades executed on my own dedicated server?

No, TradersPost is a software as a service and is hosted in a cloud environment. If you'd like to discuss dedicated automated trading systems, please email [support@traderspost.io](mailto:support@traderspost.io).

### What happens if a signal is received when the market is closed

The resulting orders will be either queued for the next market open on the TradersPost side or on the broker side. You can read more about [Order Queueing](../order-queueing.md) here.

### Why was my order rejected by my broker?

Unfortunately, TradersPost does not have much visibility in to the backend of the brokers we integrate with and they and the parties that execute orders may choose to reject orders for a variety of different reasons. If you are unsure why something was rejected, please contact your brokers support team. If you are still unsure, email us at [support@traderspost.io](mailto:support@traderspost.io).

### Why is my fill price different than my signal price?

This is caused by slippage. Slippage is caused by the spread between the bid and the ask and the price movement that occurs between when a strategy signal is generated and an order is filled. Make sure you account for enough slippage in your strategy backtests. The amount of slippage depends on the ticker and the amount of volume it has. Here is some more general information about slippage [https://www.investopedia.com/terms/s/slippage.asp](https://www.investopedia.com/terms/s/slippage.asp)

### Why are my TradeStation simulated orders not filling?

TradeStation simulated paper trading environment often has delays with filling simulated orders. Especially with options. When you experience these issues, you can report the problem to [clientservice@tradestation.com](<mailto:clientservice@tradestation.com >).

### Do you support Two-Factor (2FA) Authentication?

Yes, we support Two-Factor (2FA) authentication with popular authenticator apps like Google Authenticator and Authy.

### What is the Pattern Day Trading (PDT) rule?

A pattern day trader (PDT) is a regulatory designation for those traders or investors that execute four or more day trades over the span of five business days. Once your account is labeled as a pattern day trader then you have to maintain at least $25,000 in equity in your account. This means that in order to execute automated trading strategies that frequently buy and sell in the same day, you need at least $25,000 equity in your account.

### Are there limits on how many webhook signals you can send?

There are no technical limits enforced today but TradersPost is **NOT** designed to be a high frequency trading platform. While we do not currently rate limit traffic to webhooks, we may contact you and disable your webhooks and strategies if we determine that your account is sending too many requests.

For example, strategies running on a timeframe lower than 1 minute which are getting in and out of a trade every minute or less than every minute are not supported. TradingView alerts can be delayed by 30 to 60 seconds in some rare cases so your strategy needs to run on a timeframe that is higher than the possible delay.

### Can you trade extended hours with futures?

Futures don’t have a concept of extended hours. The extended hours checkboxes are for stocks only. You can’t use extended hours orders with futures. Futures have one single 23 hour session 6 days a week and there is no pre/post market hours. You can leave the extended hours checkboxes unchecked when you are setting up a futures strategy subscription.

