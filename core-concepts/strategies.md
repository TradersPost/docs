# Strategies

A Strategy in TradersPost is the central place where the webhook URL is provided and all subscriptions (broker connections) are established. Within a strategy, users define the asset class (stocks, options, futures, or crypto), select the trading style (systematic or discretionary), set security controls and allowed tickers, and configure the default settings that apply to all future subscriptions (broker connections) created under that strategy. Each strategy includes a unique webhook URL, which external platforms use to deliver JSON messages containing trade signals. From the Strategy Dashboard, users can monitor and manage all active subscriptions linked to the strategy, ensuring full visibility and control over how signals are routed and executed.

## Create a Strategy

Lets get started by creating your first strategy in TradersPost!

1. Navigate to [**Strategies**](https://app.traderspost.io/app/trading/strategies) and click the [**New Strategy**](https://app.traderspost.io/app/trading/strategies/new) button at the top right.
2. Give your strategy a **Name** and choose which **Asset class** you want your strategy to trade.
3. Finally, click the **Save** button and your strategy will be created.
4. Next, define the Subscription Defaults that will be used when new subscriptions are created for this strategy.

Now you are ready to connect your strategy to your broker using a [subscription](subscriptions.md).

## Troubleshooting Signals

When sending signals to TradersPost, it's a recommended practice to head to your Strategies page and click on Signals for the strategy you want to inspect. This view shows a complete list of all incoming signals received for that strategy, along with the corresponding **ticker**, **action** (Buy, Sell, Exit, Add, Cancel), and the exact timestamp when each signal was processed.

Next to each signal, you'll see a quick status summary showing how many of your active **subscriptions** successfully processed the signal versus how many encountered issues. This allows you to easily verify that signals are being received correctly and that trades are executing as expected across all your connected broker and exchange accounts.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

When you click on any individual signal in the list, you'll be able to view the specific **trades** that were submitted to each of your subscribed broker connections. For each trade, you can see whether it was successfully submitted and executed, or if any issues occurred. Clicking into a specific trade provides detailed information about the execution, including order fills, broker responses, and, if applicable, any errors or reasons why the trade was rejected or failed. This allows you to fully audit how each signal was processed across all your accounts.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
