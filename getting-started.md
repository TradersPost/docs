---
description: >-
  Quick tutorial for getting setup on TradersPost with an automated trading
  strategy in less than 10 minutes.
---

# Getting Started

## Create TradersPost Account

First, go to [TradersPost.io](https://traderspost.io) and click [Register](https://app.traderspost.io/register) at the top right of the page.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.17.28 PM.png" alt=""><figcaption><p>TradersPost Home Page</p></figcaption></figure>

Enter your email and click the **I agree, Register** button. Alternatively, you can login with your Google account if you have a Google account.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.21.10 PM.png" alt=""><figcaption><p>TradersPost Register Page</p></figcaption></figure>

After creating your account, you will be redirected to a form to setup your account. Fill out the setup your account form with your information and click **I agree, Continue**.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.25.18 PM.png" alt=""><figcaption><p>Setup Your Account Page</p></figcaption></figure>

## Connect Your Broker

After you setup your account, navigate to **Brokers** in the top menu bar.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.36.43 PM (1).png" alt=""><figcaption><p>TradersPost Dashboard</p></figcaption></figure>

On the next page, click **Connect Live Broker** or **Connect Paper Broker**.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.35.08 PM.png" alt=""><figcaption><p>TradersPost Connected Brokers Page</p></figcaption></figure>

Next, choose what broker you want to connect to TradersPost. In this example, we will use [Alpaca](https://app.alpaca.markets/signup?utm\_source=traderspost).&#x20;

If you don't already have an Alpaca account, [click here](https://app.alpaca.markets/signup?utm\_source=traderspost) to create one. Create your account and then make sure you are logged in.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.48.38 PM.png" alt=""><figcaption><p>Create Alpaca Account Page</p></figcaption></figure>

Now, back in TradersPost click the **Alpaca** button to connect your Alpaca account to TradersPost.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.35.14 PM (1).png" alt=""><figcaption><p>Connect Live Broker Page</p></figcaption></figure>

Read the Disclosure, Terms of Service and Privacy Policy then click the green **I agree** button to continue.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.35.17 PM.png" alt=""><figcaption><p>Connect Broker Disclosure Page</p></figcaption></figure>

Click the yellow **Allow** button to authorize TradersPost to access your Alpaca account.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.35.22 PM.png" alt=""><figcaption><p>Alpaca Authorize TradersPost Page</p></figcaption></figure>

You will be redirected back to TradersPost after your Alpaca account is connected successfully.



<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.35.26 PM.png" alt=""><figcaption><p>TradersPost Edit Broker Page</p></figcaption></figure>

Congratulations! You successfully connected your broker to TradersPost. Continue reading to learn how start sending signals to TradersPost from your strategy.

## Create a Webhook

Webhooks are how signals get sent to TradersPost from external third-party platforms like [TradingView](https://tradingview.com) or [TrendSpider](https://trendspider.com).

Start by hovering over **Strategies** in the top menu bar and click **Webhooks**.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.57.15 PM.png" alt=""><figcaption><p>TradersPost Webhooks Menu</p></figcaption></figure>

Click the black **New Webhook** button at the top right of the page.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.57.23 PM (1).png" alt=""><figcaption><p>TradersPost New Webhook Button</p></figcaption></figure>

Give your webhook a name like **Stocks Webhook** and click **Save** at the top right of the page.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.57.41 PM.png" alt=""><figcaption><p>TradersPost Webhook Form</p></figcaption></figure>

## Create a Strategy

Now that you have a webhook created, you are ready to create a strategy. Click the **Create a new strategy** link after saving your webhook.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.57.47 PM.png" alt=""><figcaption><p>TradersPost Webhook Edit Page</p></figcaption></figure>

Give your strategy a name like **Stocks Strategy** and associate your **Stocks Webhook** with the strategy by checking the checkbox next to your webhook, then click the **Save** button at the top right of the page.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.58.09 PM (1).png" alt=""><figcaption><p>TradersPost New Strategy Page</p></figcaption></figure>

## Subscribe to your Strategy

Now that your strategy is created, you are ready to connect it to your Alpaca broker by subscribing to the strategy. Click the **Create a subscription** button to connect your subscription to your broker.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.58.14 PM.png" alt=""><figcaption><p>TradersPost Strategy Edit Page</p></figcaption></figure>

Choose which broker you want to connect the strategy to. Lets choose the **Live Alpaca** broker here.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.58.43 PM.png" alt=""><figcaption><p>Subscribe to Strategy Page</p></figcaption></figure>

Check the **Confirm** checkbox and then click the **Confirm** button to continue.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.58.49 PM.png" alt=""><figcaption><p>Subscribe to Strategy Confirmation</p></figcaption></figure>

Your new strategy subscription has been created, but it is not enabled yet. Lets customize some of the settings before we enable it.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.58.53 PM.png" alt=""><figcaption><p>Strategy Subscription Edit Page</p></figcaption></figure>

Check the **Auto submit** checkbox because we want the trades to submit to the broker automatically, without us having to manually approve or reject each trade. If you leave this unchecked, you will be able to approve or reject the trade before it submits to the broker.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.59.12 PM.png" alt=""><figcaption><p>Check auto submit checkbox</p></figcaption></figure>

Scroll down a little bit to the **Tickers** section and check **SQ** under the list of available **Tickers** or check **Allow any ticker** if you want to allow any ticker on this strategy subscription.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.59.28 PM.png" alt=""><figcaption><p>Strategy Subscription Tickers Section</p></figcaption></figure>

Scroll down a little more to the **Advanced Options** section and check **Entry market** and **Exit market** and then click the **Save** button. Lets keep it simple to start, normal market hours only with market orders.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.59.38 PM.png" alt=""><figcaption><p>TradersPost Strategy Subscription Advanced Options</p></figcaption></figure>

You are ready to enable your first strategy subscription. Click the green **Enable** button at the top right to enable your strategy.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.59.44 PM.png" alt=""><figcaption><p>Strategy Subscription Enable Button</p></figcaption></figure>

Confirm you have read the TradersPost Terms of Service and Privacy Policy and check the checkbox then click the green **Enable** button.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.59.51 PM.png" alt=""><figcaption><p>Eable Strategy Subscription Confirmation</p></figcaption></figure>

Your strategy subscription is now enabled! You are ready to start sending signals to TradersPost from your strategy.

## Copy Webhook URL

In the top menu bar, hover over **Strategies** and click **Webhooks**. We're going to go back to the webhook we created in the beginning to copy the webhook URL so that we can use it in TradingView alerts.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 9.28.24 PM.png" alt=""><figcaption><p>Webhooks Menu</p></figcaption></figure>

Click the **View** button next to the webhook that we created in the beginning of this tutorial.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 9.29.13 PM.png" alt=""><figcaption><p>Webhook View Button</p></figcaption></figure>

Click the **Copy** button next to the masked **Webhook URL** to copy the URL in to your computers clipboard.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 9.29.22 PM.png" alt=""><figcaption><p>TradersPost Webhook URL Copy Button</p></figcaption></figure>

## Setup TradingView Alerts

Now you have your TradersPost Webhook URL in your computers clipboard so you are ready to head over to TradingView and create an alert for your strategy or indicator.

First, load your strategy or indicator on your chart. If you don't have your own strategy or indicator, you can use this example [Trend Following MOMO](https://www.tradingview.com/script/Jrw5Qegy-Trend-Following-MOMO/) strategy by Matt DeLong.

Next, load the **SQ** ticker on your chart and click the **Create Alert** button at the top right of TradingView.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 9.34.55 PM.png" alt=""><figcaption><p>TradingView Create Alert Button</p></figcaption></figure>

Fill out the **Settings** tab in the **Create Alert on SQ** form. Enter the following settings.

* Choose **Trend Following MOMO** from the **Condition** dropdown
* Choose **ProjectX Buy Alert** from the 2nd dropdown under Condition
* Click **Once Per Bar Close** next to the **Trigger** section.
* Give the alert a name like **TradersPost SQ Buy Alert**.
* Paste the following JSON in to the alert message textarea.

```json
{
    "ticker": "{{ticker}}",
    "action": "buy"
}
```

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 9.37.15 PM.png" alt=""><figcaption><p>TradingView Create Buy Alert</p></figcaption></figure>

Click the **Notifications** tab and paste the TradersPost Webhook URL in the Webhook URL field and then click the blue **Create** button.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 9.54.33 PM (1).png" alt=""><figcaption><p>TradingView Create Alert Notifications Tab</p></figcaption></figure>

Now do the same thing for the sell side. Except choose **ProjectX Sell Alert** this time and paste the JSON for a sell in to the alert message textarea and then click the blue **Create** button.

```json
{
    "ticker": "{{ticker}}",
    "action": "sell"
}
```

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 9.54.35 PM.png" alt=""><figcaption><p>TradingView Create Sell Alert</p></figcaption></figure>

**Congratulations!** You are all set. You are live with your first automated trading strategy connected to your Alpaca broker. If you have any questions, join us in our [Discord](https://traderspost.io/discord) chat. Looking forward to seeing you there!
