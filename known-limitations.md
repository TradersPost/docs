---
description: >-
  TradersPost is an actively developed and maintained platform and while we
  strive to continue improving the platform, there are known limitations that
  this page aims to document.
---

# Known Limitations

### High Frequency Trading

TradersPost is not designed to be a high frequency trading platform and sending multiple signals within less than a minute are not guaranteed to behave correctly.

While we do not currently rate limit traffic to webhooks, we may decide to disable your strategies if we determine that your strategies are sending too many requests.

### Order Retrying

Failed orders will never be retried. If communication with a broker fails for any reason, we will never retry a failed operation. We will do our best to detect when something fails or something unexpected happens and notify you via email. However, there are scenarios where an order could be accepted by a broker and then rejected later and in those scenarios, you may not receive a trade failed email notification.

### Alert Delays

Alert webhooks from third parties like [TradingView](tradingview.md) and [TrendSpider](trend-spider.md) can be delayed for an undetermined amount of time or may not be sent at all. You are responsible for monitoring your automated trading strategy and taking manual action when necessary.&#x20;
