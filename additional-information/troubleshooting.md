---
description: >-
  Find the solutions for common issues and learn how to troubleshoot issues on
  your own using TradersPost logs and trade execution information.
---

# Troubleshooting

### **My strategy is only sending limit orders, how do I send market orders?**

In your Strategy Subscription settings, scroll down to the `Entry` and `Exit` sections and change the `Entry order type` and `Exit order type` from `Limit` to `Market`.

### Why is my strategy not trading in extended hours?

If you would like your strategy to trade in extended hours, you will need to setup the alert in TradingView or TrendSpider with extended hours enabled on the chart. Then, in TradersPost, make sure you have the **Allow entry extended hours** and **Allow exit extended hours** checkboxes checked so that TradersPost knows to send orders with extended hours enabled. This tells the broker that the order is allowed to be filled in extended hours. Note that in extended hours, you can only use limit orders and market orders are not allowed.

### Why is my strategy trading manually rather than automatically?

To make your strategy submit orders to the broker automatically, make sure you have the **Auto submit** checkbox checked in your strategy subscription settings.

### Why can I not see any example orders on my subscription settings page?

This is likely due to you selecting a contract that you can't afford based on the Position Size settings you set. Check your Position Size settings and try removing your settings until you get an entry order generated.&#x20;

### My trade did not execute. How can I troubleshoot?

You can troubleshoot your traded by examining the TradingView and TradersPost logs.

First, make sure that TradingView actually triggered an alert by checking the **Alerts log** in TradingView right column pane. The alert must show up here. If it shows on the chart or shows in the backtester, but it does not show in the **Alerts log** then it is likely that your Pine Script code suffers from [repainting](../learn/signal-sources/tradingview.md#pine-script-repainting).

<figure><img src="../.gitbook/assets/Screenshot 2025-09-12 at 1.13.09 PM.png" alt=""><figcaption><p>TradingView Alerts log column pane and tab</p></figcaption></figure>

Second, in TradersPost navigate to your [strategies](https://app.traderspost.io/app/trading/strategies) page then click Signals.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-12 at 1.15.13 PM.png" alt=""><figcaption><p>TradersPost Strategies List</p></figcaption></figure>

After you click **Signals**, you will see a list of all the requests that have been sent to your strategy webhook URL.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2025-09-12 at 1.16.47 PM.png" alt=""><figcaption><p>TradersPost Webhook Logs</p></figcaption></figure>

You can then click in to each signal to see information about the signal, where it came from, what time it was received and any trades that were executed as a result of the signal.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-12 at 1.19.07 PM.png" alt=""><figcaption><p>TradersPost View Webhook Request Page</p></figcaption></figure>

Next, click the individual trade to view the executed trade and all the associated information about the trade. On this pop up you can see information about the trade. If a trade was rejected, these messages can tell you information about why the trade was rejected.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-12 at 1.18.25 PM.png" alt=""><figcaption><p>TradersPost View Trade Pop Up</p></figcaption></figure>
