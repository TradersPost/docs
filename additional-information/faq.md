---
description: Get answers to the most frequently asked questions about TradersPost.
---

# Frequently Asked Questions

### Do you support paper trading?

Yes, TradersPost supports paper trading with multiple different brokers. Read more [here](../learn/paper-trading.md).

### Does TradersPost require coding?

No. TradersPost does not require coding. You can easily connect strategies to TradersPost that other traders have created and published on [TradingView](https://cdn.traderspost.io/images/TradingView.png). Or you can use a platform like [TrendSpider](https://trendspider.com/?\_go=traderspost) which allows you to build strategies without code.

### Can I trade both long and short?

Yes, TradersPost supports trading both the long and short sides of a strategy.

### Do you support crypto?

Yes, we support crypto with several different popular crypto exchanges like [Coinbase](../core-concepts/brokers/coinbase.md) and [Kraken](../core-concepts/brokers/kraken.md).

### Do you support futures?

Yes, futures support is available and can be enabled in your account settings. We support futures with popular brokers like [Tradovate](../core-concepts/brokers/broker-roadmap/tradovate.md) and [TradeStation](../core-concepts/brokers/tradestation.md).

### Do you support options?

Yes, options support is in beta and can be enabled in your account settings. We support options with popular brokers like [TradeStation](../core-concepts/brokers/tradestation.md) and [Tradier](../core-concepts/brokers/tradier.md).

### Do you support spreads or other complex options strategies?

No, currently we only support directional options trades. This means we only support buying or selling calls in the same way you would buy shares of the underlying. Just instead of buying shares, you are buying calls. Or instead of shorting a underlying, you are buying puts.

### Do you support index options on indexes like SPX?

No, we don't yet support index options. We only support Stock & ETF options. So in the case of SPX, you can trade SPY ETF options instead.

### Does TradersPost manage margin or offer margin rules for my account?

No. TradersPost does not currently track margin availability in your margin accounts. We also do not have settings in place to prevent the use of margin if it is available in your account. If your account does not have margin available and you send a trade that exceeds your purchasing power, the trade will be rejected by the broker.

### What brokers do you support?

TradersPost currently integrates with brokers like [TradeStation](../core-concepts/brokers/tradestation.md) and [Tradovate](../core-concepts/brokers/broker-roadmap/tradovate.md). You can see our full list of brokers on our website [here](https://traderspost.io/connections).

### Can I trade my IRA?

Yes, TradeStation and other brokers supports specialty account types like IRA (retirement), business and other specialty account types. Note that with Robinhood we don't currently support trading in IRA accounts.

### What happens to existing positions when I connect my broker?

If you connect an account with existing open positions, TradersPost will not do anything to those positions unless your strategy subscription has those tickers selected. It is up to you to be sure your manual trading does not conflict with the tickers being managed by TradersPost. It is recommended that you use an account dedicated to TradersPost but we do not strictly disallow you from trading manually in the same account.

### How old is TradersPost?

TradersPost was founded by the CEO & Founder, [Jonathan Wage](https://www.linkedin.com/in/jwage/), on January 1st 2021. You can learn more about TradersPost [here](https://traderspost.io/about).

### Is TradersPost free?

TradersPost is free to get started. You can paper trade for free for 7 days. Once you are ready to trade live with real money, a paid subscription is required.

### What happens after my free 7 day trial is up?

Your strategy subscriptions will be disabled and your account will be disabled. To reactivate your account, you can upgrade to the paid Starter plan for $49 per month to get access to paper and live trading.

### I don't have a supported broker, how can I get started?

TradersPost comes with a free paper account that lets you test strategies and get familiar with the platform.

### Do you have an API?

No, but it is on our future roadmap. The only way currently to integrate strategies with TradersPost is via [Webhooks](../core-concepts/webhooks.md).

### Are trades executed on my own dedicated server?

No, TradersPost is a software as a service and is hosted in a shared cloud environment.

### What happens if a signal is received when the market is closed

The resulting orders will be either queued for the next market open on the TradersPost side or on the broker side. You can read more about [Order Queueing](../learn/order-queueing.md) here.

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

### How does trading in extended hours work?

For Stocks and Stock Options you can place market orders in regular trading hours but only limit orders in extended hours.&#x20;

Futures don’t have a concept of extended hours as the extended hours checkboxes are for stocks only. You can’t use extended hours orders with futures. Futures have one single 23 hour session 6 days a week and there is no pre/post market hours. You can leave the extended hours checkboxes unchecked when you are setting up a futures strategy subscription.

### Can I manually exit a position before my strategy exits?

If the quantity is hardcoded to a fixed number and you aren’t using a position aware quantity from your strategy then it is ok to manually exit a position early. If you ARE using a position aware quantity from your strategy then it could cause an issue because the strategy will send a signal with enough quantity to close the open position and enter a new position on the other side. Since the open position is already closed, the full quantity sent would be used to enter a new position. Essentially if your strategy is position aware and your broker is not in sync with the quantity your strategy thinks you have, you will have issues.

### Do you charge a fee per trade?

No, TradersPost does not charge a fee per trade. Our service is a monthly or yearly Software as a Service (SaaS) fee. Take a look at our [pricing](https://traderspost.io/pricing) to learn more.

### How can I see my profit and loss per trade?

We don't currently have strategy or trade level analytics or reports. You will need to use your broker data to do analysis or use a third-party [Trade Journaling](trade-journaling.md) tool.

### How come I see trades on my chart that didn't alert in realtime?

Your strategy may suffer from [repainting](../learn/tradingview.md#pine-script-repainting). Make sure you study up on repainting to avoid any potential issues with your strategy being coded in a way where it executes in a backtest but does not execute in the same way with live data.

### Can I export my traders from TradersPost?

No, we don't yet support exporting data from TradersPost.

### What payment options do you accept? Do you accept crypto payments?

We support payments from Visa, Mastercard, American Express and Discover. We don't accept crypto payments.

### Can I combine multiple indicator alerts before triggering a trade?

Yes, you can perform logic in TradingView to combine multiple indicators in to one alert. Read this [blog post](https://blog.traderspost.io/article/new-indicator-confluence-of-alerts) to learn more about our Confluence of Alerts indicator.&#x20;

{% embed url="https://www.youtube.com/watch?v=nKVavKVFV60" %}

### Are TradingView alert webhooks delayed?

TradingView webhooks can be delayed by anywhere from 2-3 seconds to upwards of 60 or more. TradingView considers a 25 to 45 second delay to be normal.

### How much does TradersPost cost?

TradersPost is a Software as a Service. We charge a monthly or yearly software subscription fee. The base Starter plan costs $49 per month or $499.80 per year if paid annually. You can learn more about our available pricing [here](https://traderspost.io/pricing).

### Does TradersPost require a computer to be online and on at all times? Or does the TradingView window have to be open for TradersPost to work?

No, TradingView alerts and TradersPost both work in the cloud and independently of your computer. Unlike other services that might use a chrome extension to pass along the alert to your broker, TradersPost receives webhook requests behind-the-scenes from the cloud so you don't have to worry about losing internet or keeping your computer on.

### Do I have to be logged in to TradersPost for my strategies to work?

No, TradersPost, TradingView and TrendSpider all live in the cloud so they are always online. Your computer does not have to be running for your automated trading strategies to work.

### How can I contact TradersPost?

There are several contact options on the [Contact Us Page](https://traderspost.io/contact).  We are also available in [Discord](https://traderspost.io/discord) with the rest of the TradersPost community.

### Does TradersPost support advanced order types like Fill or Kill?

Yes, if the broker supports that order type, then you can send orders with the fill or kill time in force.

### If I want to upgrade my plan how will the billing be handled?

The used time on your current month and current plan will be billed at the current plan rate and the rest of the month will be billed at the new plan rate. This amount isn't billed immediately, it is added to your next invoice.\
\
Here is a simple example with fake numbers to make the math easy. If you are on the $100 per month plan and you upgrade to the $200 per month plan in the middle of the month, your next invoice would be $250. This would be $200 for the next month, $100 for half of the month and then $50 reduced from half of the original month.\
\
If you are upgrading on an already existing yearly plan, the billing cost will take into account your unused days on your current plan.

### Why can't I connect my Robinhood account?

Robinhood accounts are required to have 2fa (two-factor authentication) enabled in order to connect to TradersPost. Go to your Robinhood security settings and make sure 2fa is enabled. If you are still have issues connecting, try turning 2fa off and on again.

### Can I update take profit or stop losses or send take profit or stop losses after the entry?

You can't update stop losses that are in the broker that get established at entry time, but if you control all your take profit and stop loss logic in the strategy, then you can move it and change it dynamically and when the price is reached in your strategy, an exit signal can be generated and sent to TradersPost.

### Can I receive email notifications for signals?

Yes, you can navigate to **My Account > Settings** and then scroll down to the section named **Account Notification Settings** and enter the email address you wish to use. You can be notified of new webhooks, failed webhooks, new trades and failed trades. Check the **Notify failures only**  checkbox if you only wish to be notified of failures.

### How long do promotional discounts last for?

Promotional discounts typically only last for 12 months. If it appears that you have been charged slightly higher than usual then it is likely due to your promotional discount code expiring.
