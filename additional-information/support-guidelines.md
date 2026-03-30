---
description: >-
  When getting in touch with support, there are a couple of things you can
  provide to speed up and improve the quality of our help.
---

# Support Guidelines

## Signal or Signal ID Help

If you reach out to support, we can speed up the process of helping dramatically if you can isolate an exact signal or trade that failed, so we can look it up and investigate what happened for you. The simplest thing to provide is a Signal ID or Signal URL from your account.

A [Signal](../core-concepts/signals.md) is what you send to TradersPost for us to execute your trade with any [subscriptions](../core-concepts/subscriptions.md) you have tied to a [strategy](../core-concepts/strategies.md).

{% stepper %}
{% step %}
### Find the Signal ID

When you send a signal, we save all off them together on your [Signals dashboard](https://app.traderspost.io/app/account/signals). If you had a recent signal that didn't execute with your broker or exchange as expected, find that signal on this page and click the result.

Under the Details tab, you'll see a Signal ID. Copy that text and send it to us in your support ticket.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### **Find the Signal URL**

As an alternative, you can also share the entire Signal URL from the [Signals dashboard](https://app.traderspost.io/app/account/signals) by clicking on the signal that you want us to look at and share the URL from that page.

The URL should look like this:

```
https://app.traderspost.io/app/trading/strategies/<uuid characters/signals/<uuid characters/view
```

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

We can then quickly look up your account and the trade issue from this link.
{% endstep %}

{% step %}
### Provide Context about the Trade

Next, provide as much detail as possible about the trade, where it came from, how it should have fired and what you expected to happen.

With this information, our support team can quickly look up your trade and help you determine what happened and what can change.
{% endstep %}
{% endstepper %}

## JSON Guidance

You have a few options when it comes to JSON and what message to use.

1. Ask our AI bot for guidance on the proper message to send. It has been trained to correctly build JSON messages according to [our documentation](https://docs.traderspost.io/docs/core-concepts/webhooks). You can ask it to construct a JSON message for everything from the entry to the bracket take profit and stop loss.
2. Read through the [webhooks](https://docs.traderspost.io/docs/core-concepts/webhooks) section of the documentation for guidance on how to construct a message.
3. If you're still stuck, reach out to an agent and we'll help you.

All other questions and needs can be answered by the team through our support email or through the chat bubble on this page or from your [dashboard](https://app.traderspost.io/app/dashboard).
