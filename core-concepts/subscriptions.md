---
description: >-
  Subscriptions are what allow you to connect a strategy to a broker and to
  control what kind of orders get sent to the broker.
---

# Subscriptions

Once you have connected your broker and created a webhook and strategy, now you are ready to subscribe to the strategy to connect it to your broker.

1. Navigate to **Strategies > Subscriptions** and click the **New Subscription** button at the top right.
2. Then, choose the strategy from the list that you want to subscribe to and click the **Subscribe** button.
3. Next, choose the broker from the list that you want to connect your strategy to and click it. A confirmation modal will pop up, check the **Confirm** checkbox and click the **Confirm** button.
4. Now your strategy subscription is created, but has not been enabled yet. Review the settings for your strategy subscription and click Save if you make any changes.
5. Once you are ready, click the green **Enable** button at the top right to enable your strategy subscription. Now, when TradersPost receives a request to your webhook, a trade will be executed and orders sent to your broker.

## Architecture

We separate the Brokers, Webhooks, Strategies and Subscriptions at an architecture level to give more flexibility. Some of the benefits are:

* You can easily change the webhook that powers a strategy with zero disruption to the strategy subscribers.
* You can connect a strategy to multiple different brokers with different settings.
* You can connect a strategy to both a paper and live account at the same time and run them in parallel.
* Other customers can subscribe to your strategies.
