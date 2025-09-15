# JSON Message Template Creator

TradersPost uses [JSON messages](https://en.wikipedia.org/wiki/JSON) to receive and process trading instructions sent to a webhook URL. If you're new to JSON, don't worry, it's simply a way to structure data in a format that's both machine-readable and easy for humans to understand.

Head to the [webhooks documentation](webhooks.md) to see all the different types of JSON messages you can send.

## What Is JSON?

**JSON** stands for _JavaScript Object Notation_. It’s a simple, text-based format for organizing data using key/value pairs. In TradersPost, JSON allows you to send your trading signals with clear instructions that define _what to trade_ and _how to trade it_.

Here’s a very simple example of a JSON message that TradersPost would use:

```json5
{
  "ticker": "NQ1!",
  "action": "buy",
  "signalPrice": 18250.5,
  "quantity": 2,
  "time": "2025-06-17T10:30:00Z"
}
```

## Required Fields

At minimum, every JSON message sent to TradersPost must include:

* **ticker** — The symbol you want to trade (e.g. `NQ1!` or `MSFT`)
* **action** — The trade action: `buy`, `sell`,  `exit`, `cancel` or `add`&#x20;

Without these two fields, TradersPost won’t know what trade to place.

## Recommended Fields

While not required, we strongly recommend also including:

* **signalPrice** — The price at the time your signal fired
* **time** — A timestamp for when the signal was generated

Providing these values helps you maintain a full record of your signal and enables TradersPost to better track execution slippage and timing.

## All Fields

See our entire [webhook documentation](webhooks.md) page for all the possible fields you can send in a JSON message.

## Creating and Saving JSON Message Templates

{% embed url="https://youtu.be/vBBt2rAkVwA" %}

We've made JSON message creation easy with our JSON message template creator tool. It can be found on the "Submit Signal" page that is located in your [strategy dashboard](https://app.traderspost.io/app/trading/strategies). Click the ••• icon next to Dashboard and navigate to "Submit Signal" and click it.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-05 at 12.09.28 PM.png" alt=""><figcaption></figcaption></figure>

The area highlighted in red is how you can build your own JSON to not only submit manual orders to your strategy subscriptions but also to create JSON Signal Templates to save and reuse later.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-05 at 12.13.39 PM (1).png" alt=""><figcaption></figcaption></figure>

Once you've selected how you want your trade to be formed, click Save Signal Template.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-05 at 12.17.56 PM.png" alt=""><figcaption></figcaption></figure>

Here is a sample JSON message created for a buy entry order with a take profit of 20 points and a stop loss of 10 points.

```
{
    "ticker": "{{ticker}}",
    "action": "buy",
    "takeProfit": {
        "amount": "20"
    },
    "stopLoss": {
        "type": "stop",
        "amount": "10"
    },
    "signalPrice": "{{close}}",
    "time": "{{timenow}}",
    "interval": "{{interval}}"
}
```

Once you are finished creating your JSON, you'll choose a template name, select the signal source, and you'll then see the custom JSON message that you'll then save. Once it's saved, you'll copy and paste the signal template JSON into your alert in Tradingview (or your signal source if different than Tradingview).

<figure><img src="../.gitbook/assets/Screenshot 2025-09-10 at 10.23.01 PM.png" alt="" width="563"><figcaption></figcaption></figure>

Saved signal templates will appear at the bottom of the Submit Signal page where you can easily copy, edit, and delete them.

## Using a Saved JSON Template In Your Alert

{% embed url="https://youtu.be/u3tPkFWN6xk" %}

Once you've saved your reusable JSON templates it's time to create your alerts. This example will be for a Tradingview indicator called [UT Bot Alerts](https://www.tradingview.com/v/n8ss8BID/). For this indicator we'll need both a **buy** and a **sell** alert.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-10 at 10.26.04 PM.png" alt=""><figcaption><p>Screenshot of the UT Bot Alerts indicator with Buys and Sells</p></figcaption></figure>

First, we'll need to add a new alert. Click the + icon in the "Alerts" area (in the clock tab on the right side of your Tradingview window)

<figure><img src="../.gitbook/assets/Screenshot 2025-09-10 at 10.27.09 PM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2025-09-10 at 10.29.07 PM.png" alt="" width="375"><figcaption><p>UT Bot Alerts "Buy" Signal Settings Screenshot</p></figcaption></figure>

This first alert will be for the <mark style="background-color:green;">**buy**</mark>. We'll choose the indicator in the condition dropdown (in this example: UT Bot Alerts), then the long (<mark style="background-color:green;">**buy**</mark>) condition, once per bar close, and make sure our expiration is open ended or as far out as we can choose if you don't have a plan which supports open ended alerts.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-10 at 10.33.04 PM (1).png" alt="" width="563"><figcaption></figcaption></figure>

We'll copy the previously made JSON template for the Indicator <mark style="background-color:green;">**Buy**</mark> w/ Take Profit and Stop Loss and paste it into the Message tab in our <mark style="background-color:green;">**buy**</mark> alert.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-10 at 10.31.31 PM.png" alt="" width="375"><figcaption><p>The JSON message pasted into the Message tab</p></figcaption></figure>

Finally, we'll go to our TradersPost strategy dashboard, click the Webhook button, and copy the webhook URL to paste into the third tab of our <mark style="background-color:green;">**buy**</mark> alert.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-10 at 10.36.33 PM.png" alt=""><figcaption></figcaption></figure>

We'll click Copy on the Strategy Webhook module that pops up.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-10 at 10.38.14 PM.png" alt=""><figcaption></figcaption></figure>

Finally, we'll paste that into the Notifications tab on our <mark style="background-color:green;">**buy**</mark> alert in the Webhook URL section.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-10 at 10.35.35 PM.png" alt="" width="375"><figcaption><p>The webhook URL is checked and pasted in</p></figcaption></figure>

Last step is to repeat this process for the <mark style="background-color:red;">**sell**</mark> alert. First, we click the + button again.

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2025-09-10 at 10.41.51 PM.png" alt="" width="375"><figcaption><p>UT Bot Alerts "Sell" Signal Settings Screenshot</p></figcaption></figure>

We'll choose the indicator in the condition dropdown (in this example: UT Bot Alerts), then the short (<mark style="background-color:red;">**sell**</mark>) condition, once per bar close, and make sure our expiration is open ended or as far out as we can choose if you don't have a plan which supports open ended alerts.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-10 at 10.44.16 PM.png" alt="" width="563"><figcaption></figcaption></figure>

We'll copy the previously made JSON template for the Indicator <mark style="background-color:red;">**Sell**</mark> w/ Take Profit and Stop Loss and paste it into the Message tab in our <mark style="background-color:red;">**sell**</mark> alert.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-10 at 10.45.37 PM.png" alt="" width="375"><figcaption><p>The JSON message pasted into the Message tab</p></figcaption></figure>

Finally, we'll paste that same webhook URL into the Notifications tab on our <mark style="background-color:red;">**sell**</mark> alert in the Webhook URL section.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-10 at 10.46.33 PM.png" alt="" width="375"><figcaption></figcaption></figure>

Once you've created both alerts, you'll start seeing the alerts populate your Tradingview Alert Log which can be accessed by clicking the "Log" tab on the top of the Tradingview Alert area.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-10 at 10.48.04 PM.png" alt="" width="375"><figcaption></figcaption></figure>

You'll also see your trades populate your signal list in the Strategy dashboard for your specific strategy in TradersPost.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-10 at 10.49.20 PM.png" alt=""><figcaption></figcaption></figure>

If you have questions or run into issues while creating alerts, JSON messages, or anything else related to TradersPost, you can contact us using the chat icon in the bottom right corner of your TradersPost Dashboard and we'll be glad to help!
