---
description: >-
  Subscriptions are what allow you to connect a strategy to a broker and to
  control what kind of orders get sent to the broker.
---

# Subscriptions

## Create a Subscription

Once you have connected your broker and created a webhook and strategy, now you are ready to subscribe to the strategy to connect it to your broker.

1. Navigate to **Strategies > Subscriptions** and click the **New Subscription** button at the top right.
2. Then, choose the strategy from the list that you want to subscribe to and click the **Subscribe** button.
3. Next, choose the broker from the list that you want to connect your strategy to and click it. A confirmation modal will pop up, check the **Confirm** checkbox and click the **Confirm** button.
4. Now your strategy subscription is created, but has not been enabled yet. Review the settings for your strategy subscription and click Save if you make any changes.
5. Once you are ready, click the green **Enable** button at the top right to enable your strategy subscription. Now, when TradersPost receives a request to your webhook, a trade will be executed and orders sent to your broker.

## What happens when  a trade is executed?

1. **Cancel Open Orders** - Open orders for the ticker will be canceled if one of the following is true
   * There is no open position for the ticker.
   * There is an open position and it is on the opposite side of the signal. For example you have an open long stocks position and you receive an `action=sell` signal. Any take profit or stop loss sell orders will be canceled before exiting the long stocks position.
   * The signal is an explicit cancel signal where `action=cancel`.
2. **Exit Current Position** - Any open position for the ticker in the signal will be exited based on the configuration details in your subscription. For example, if you have a long stocks position open for AMD and you get an `action=sell` signal, the long position will be closed with a sell order.
3. **Enter New Position** - A new position will be entered with an order based on the configuration details in your subscription.

## Architecture

We separate the Brokers, Webhooks, Strategies and Subscriptions at an architecture level to give more flexibility. Some of the benefits are:

* You can easily change the webhook that powers a strategy with zero disruption to the strategy subscribers.
* You can connect a strategy to multiple different brokers with different settings.
* You can connect a strategy to both a paper and live account at the same time and run them in parallel.
* Other customers can subscribe to your strategies.
