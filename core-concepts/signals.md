# Signals

A signal (or trade signal) is an event that tells TradersPost to execute a trade. Signals are created outside of TradersPost, typically by a charting platform, indicator, or strategy like TradingView or TrendSpider, and sent to TradersPost via a [webhook URL](webhooks.md). Each signal includes a [JSON message](json-messages.md) containing all the details needed to place an order: ticker, action (buy/sell/add/exit), quantity, and any optional instructions.

Once TradersPost receives a signal, it processes the message according to your configured strategy and subscriptions, then submits the trade to your connected broker or exchange. This event-driven approach gives you full control over where your signals come from, how they are formatted, and how they are executed across multiple accounts.

## How Inheritance Works Between Signals and Subscription Settings

TradersPost allows you to control how much of the incoming **signal** data (contained in the **JSON message**) is used directly versus how much is overridden by your **subscription** settings.

By default, most subscription settings have a **“Use signal”** toggle enabled. This means the subscription will inherit and apply the values sent in the JSON message for properties like quantity (position size), order type, stop loss, and take profit instructions, among others. However, you can disable this inheritance on a per-subscription basis to override specific fields and apply fixed settings instead.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-05 at 12.34.50 PM.png" alt=""><figcaption><p>Example of toggling off "Use signal quantity" to trade 1 contract of NQ</p></figcaption></figure>

For example, imagine you are trading futures and your signal sends an instruction to buy `NQ1!` with a quantity of 3 contracts. The JSON message would look like this:

```json5
{
  "ticker": "MNQ1!",
  "action": "buy",
  "quantity": 3
}
```

If you have a subscription where you want to always trade just 1 contract regardless of the signal, you can disable **“Use signal quantity”** for that subscription and enter a fixed quantity of 1. The subscription will then ignore the quantity provided in the signal and always submit trades using your defined position size.

This inheritance model allows you to send one universal signal to your **strategy**, while maintaining granular control over execution behavior for each **subscription** (broker account). It’s a flexible way to scale your strategy across multiple accounts with varying trade sizes, risk profiles, or broker constraints, all from a single signal source.
