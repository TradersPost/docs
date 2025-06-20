# Brokers (Connections)

TradersPost centers around connections with brokers, exchanges, and prop firms. Each connection represents an individual account with your broker or exchange. For instance, if you link two accounts with TradeStation, both would count under your live plan.

You can connect any of these to TradersPost and authorize our software to read your balances, open positions, open orders, order history, place trades and cancel orders.

## Connect Your Broker

To connect your broker to TradersPost, follow these steps:

1. Navigate to your [dashboard](https://app.traderspost.io/app/dashboard) in the application and click [**Connect Broker**](https://app.traderspost.io/app/trading/brokers/choose) in the top right. If you are just getting started, we recommend using the already connected built in TradersPost paper broker to run your first tests against.
2. Next, choose the broker you want to connect and follow the prompts.
3. You will be redirected to the chosen broker and asked login and authorize TradersPost to access your account.
4. After you agree, you will be redirected back to TradersPost and your broker account will be connected to TradersPost.

{% hint style="warning" %}
TradersPost does not have access to your banking information and does not have the ability to transfer money in or out of your accounts. We only have access to the functionality to control trading activities.
{% endhint %}

## Broker Settings

#### **Name**

Assign a unique and descriptive name to each of your broker connections on TradersPost to easily differentiate between them, especially if you have multiple accounts with the same broker. Note that only one live and one paper account are allowed per connection, and the number of connections available depends on your payment plan. For example, you could name a futures account with TradeStation as "TradeStation Futures" and a margin account as "TradeStation Stocks," each set up as separate broker connections.

#### **Choose Paper Account / Choose Live Account**

Here you will decide which account to use for your live trading for this broker, and which account to use for paper trading. We sometimes see that customers choose their margin account here, when they meant to choose their futures account and they see errors indicating that futures aren't supported. Make sure you've selected the right live account for your broker connection.

#### **Max strategy positions**

{% hint style="warning" %}
WARNING: this feature has been deprecated and will be removed in a future version of TradersPost.
{% endhint %}

Enter the max number of positions you want allow with this broker when using it with automated strategy subscriptions. Any existing positions opened prior to using TradersPost will still count as a position, and crypto dust is often seen as a position if worth roughly more than $1.50 USD.
