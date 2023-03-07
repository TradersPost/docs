---
description: >-
  TradersPost is an actively developed and maintained platform and while we
  strive to continue improving the platform, there are known limitations that
  this page aims to document.
---

# Known Limitations

### Rate Limiting

TradersPost is **NOT** designed to be a high frequency trading platform. While we do not currently rate limit traffic to webhooks, we may contact you and disable your webhooks and strategies if we determine that your account is sending too many requests.

### Order Retrying

Failed or rejected orders will never be retried. If communication with a broker fails for any reason, we will never retry a failed operation. We will do our best to detect when something fails or something unexpected happens and notify you via email if you have your notifications enabled on your strategy subscription. However, there are scenarios where an order could be accepted by a broker and then rejected later and in those scenarios, you may not receive a trade failed email notification.

### Alert Webhook Delays

Alert webhooks from third parties like [TradingView](../learn/tradingview.md) and [TrendSpider](../learn/trend-spider.md) can be delayed for an undetermined amount of time or may not be sent at all. You are responsible for monitoring your automated trading strategy and taking manual action when necessary.&#x20;

### Race Conditions

You are responsible for ensuring that signals do not conflict with each other. We do not currently guarantee that signals won't conflict with each other. For example, if you send a buy and sell signal in the exact same second with only milliseconds in between them, there is no guarantee that the buy order will be sent to the broker and filled by the time the sell order is received and sent to the broker. It is recommended that you leave at least 1 to 5 minutes between signals. As mentioned above, TradersPost is not a high frequency trading platform and should only be used to trade on higher timeframes.

### Signal Timing

TradersPost does not support sending back to back signals at the same time. For example, if you want to exit an open position and immediately enter a new position on the other side, you cannot send an exit signal and entry signal at the same time. You would need to either send the exit signal and wait to send the new entry signal later, or if you need to exit and enter at the same time, then only send one signal and TradersPost will make sure that the exit order is sent first and will wait to send the entry order until the exit order is filled.
