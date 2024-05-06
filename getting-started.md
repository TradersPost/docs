---
description: >-
  Quick tutorial for getting setup on TradersPost with an automated trading
  strategy in less than 30 minutes.
---

# Getting Started

## Create an Account

First, go to [TradersPost.io](https://traderspost.io) and click [Register](https://app.traderspost.io/register) at the top right of the page.

<figure><img src=".gitbook/assets/Screenshot 2024-05-06 at 12.55.13 PM.png" alt=""><figcaption></figcaption></figure>

Enter your email and click the **Register** button. Alternatively, you can login with your Google account if you have a Google account.

<figure><img src=".gitbook/assets/Screenshot 2024-05-06 at 1.41.33 PM.png" alt=""><figcaption></figcaption></figure>

After creating your account, you will be redirected to a form to setup your account. Fill out the setup your account form with your information and click **I agree, Continue**.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.25.18 PM.png" alt=""><figcaption></figcaption></figure>

## Connect Your Broker

After you setup your account, navigate to **Brokers** in the top menu bar.

<figure><img src=".gitbook/assets/Screenshot 2024-05-06 at 1.45.39 PM (1).png" alt=""><figcaption></figcaption></figure>

On the next page, click **Connect Live Broker** or **Connect Paper Broker**.

<figure><img src=".gitbook/assets/Screenshot 2024-05-06 at 1.47.20 PM.png" alt=""><figcaption></figcaption></figure>

Next, choose what broker you want to connect to TradersPost. In this example, we will use [Alpaca](https://app.alpaca.markets/signup?utm\_source=traderspost).&#x20;

If you don't already have an Alpaca account, [click here](https://app.alpaca.markets/signup?utm\_source=traderspost) to create one. Create your account and then make sure you are logged in.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.48.38 PM.png" alt=""><figcaption></figcaption></figure>

Now, back in TradersPost click the **Alpaca** button to connect your Alpaca account to TradersPost.

<figure><img src=".gitbook/assets/Screenshot 2024-05-06 at 1.53.08 PM (1).png" alt=""><figcaption></figcaption></figure>

Read the Disclosure, Terms of Service and Privacy Policy then click the green **I agree** button to continue.

<figure><img src=".gitbook/assets/Screenshot 2024-05-06 at 1.54.04 PM.png" alt=""><figcaption></figcaption></figure>

Click the yellow **Allow** button to authorize TradersPost to access your Alpaca account.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 8.35.22 PM (1).png" alt=""><figcaption></figcaption></figure>

You will be redirected back to TradersPost after your Alpaca account is connected successfully.

<figure><img src=".gitbook/assets/Screenshot 2024-05-06 at 1.55.34 PM (1).png" alt=""><figcaption></figcaption></figure>

Congratulations! You successfully connected your broker to TradersPost. Continue reading to learn how start sending signals to TradersPost from your strategy.

## Create a Strategy

Now that you have your broker connected, you are ready to create a strategy. Click the **Strategies** in the header and then click **New Strateg**y at the top right of the page.

<figure><img src=".gitbook/assets/Screenshot 2024-05-06 at 1.55.34 PM.png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/Screenshot 2024-05-06 at 1.59.40 PM (1).png" alt=""><figcaption></figcaption></figure>

Give your strategy a name like **Stocks Strategy** and then click the **Save** button at the bottom left of the page.

<figure><img src=".gitbook/assets/Screenshot 2024-05-06 at 2.01.52 PM (1).png" alt=""><figcaption></figcaption></figure>

## Subscribe to Strategy

Now that your strategy is created, you are ready to connect it to your Alpaca broker by subscribing to the strategy. Click the broker that you want to connect the strategy to. In this example, we'll connect it to the paper Alpaca broker.

<figure><img src=".gitbook/assets/Screenshot 2024-05-06 at 2.03.16 PM.png" alt=""><figcaption></figcaption></figure>

Check the **Confirm** checkbox and then click the **Confirm** button to continue.

<figure><img src=".gitbook/assets/Screenshot 2024-05-06 at 2.04.52 PM.png" alt=""><figcaption></figcaption></figure>

Your new strategy subscription has been created, but it is not enabled yet. Lets customize some of the settings before we enable it.

Check the **Auto submit** checkbox and click **Enable**. We want **Auto submit** enabled because we want the trades to submit to the broker automatically, without us having to manually approve or reject each trade. If you leave this unchecked, you will be able to approve or reject the trade before it submits to the broker.

<figure><img src=".gitbook/assets/Screenshot 2024-05-06 at 2.06.43 PM (1).png" alt=""><figcaption></figcaption></figure>

Your strategy subscription is now enabled! You are ready to start sending signals to TradersPost from your strategy.

## Copy Webhook URL

You can copy the webhook URL by clicking the **Copy** button above the example orders. This will put the webhook URL in your clipboard so you can paste it in to TradingView in the next steps.

<figure><img src=".gitbook/assets/Screenshot 2024-05-06 at 2.16.04 PM.png" alt=""><figcaption></figcaption></figure>

## Setup TradingView Alerts

Now you have your TradersPost Webhook URL in your computers clipboard so you are ready to head over to TradingView and create an alert for your strategy or indicator.

First, load your strategy or indicator on your chart. If you don't have your own strategy or indicator, you can use this example [Trend Following MOMO](https://www.tradingview.com/script/Jrw5Qegy-Trend-Following-MOMO/) strategy by Matt DeLong.

Next, load the **SQ** ticker on your chart and click the **Create Alert** button at the top right of TradingView.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 9.34.55 PM.png" alt=""><figcaption></figcaption></figure>

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

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 9.37.15 PM.png" alt=""><figcaption></figcaption></figure>

Click the **Notifications** tab and paste the TradersPost Webhook URL in the Webhook URL field and then click the blue **Create** button.

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 9.54.33 PM (1).png" alt=""><figcaption></figcaption></figure>

Now do the same thing for the sell side. Except choose **ProjectX Sell Alert** this time and paste the JSON for a sell in to the alert message textarea and then click the blue **Create** button.

```json
{
    "ticker": "{{ticker}}",
    "action": "sell"
}
```

<figure><img src=".gitbook/assets/Screen Shot 2023-03-02 at 9.54.35 PM (2).png" alt=""><figcaption></figcaption></figure>

**Congratulations!** You are all set. You are live with your first automated trading strategy connected to your Alpaca broker. If you have any questions, join us in our [Discord](https://traderspost.io/discord) chat. Looking forward to seeing you there!
