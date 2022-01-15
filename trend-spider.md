# Trend Spider

TrendSpider is an automated technical analysis software for day and swing traders. It is similar to [TradingView](https://traderspost.io/docs/trading-view) and integrates with TradersPost in the same way. Just with a few small differences in how you send data to TradersPost in the webhook.

TrendSpider webhook alerts can utilize the following variables in alert descriptions.

* **%alert\_name%** - returns the name of the alert.
* **%alert\_symbol%** - returns the symbol.
* **%alert\_note%** - returns the notes for the alert.
* **%price\_action\_event%** - returns one of: touch, break\_through, bounce, script\_returned\_true.
* **%last\_price%** - returns the price of an asset for the moment when the alert has fired.

Now when you setup an alert in TrendSpider, you can configure the alert in TrendSpider with a TradersPost webhook URL and send it JSON like the following.

```json
{
    "ticker": "%alert_symbol%",
    "action": "buy",
    "price": "%last_price%"
}
```

This is the minimum amount of information you need to send TradersPost in a signal. If you omit the **price** variable, then the signal will only be able to create market orders.

You can include additional information in the webhook payload if you want, it won't affect the signal and it will just be stored and displayed in TradersPost. This can be useful for troubleshooting where a webhook came from.

```json
{
    "ticker": "%alert_symbol%",
    "action": "buy",
    "price": "%last_price%",
    "alertName": "%alert_name%",
    "alertNote": "%alert_note%",
    "priceActionEvent": "%price_action_event%"
}
```

If you are interested automating your TrendSpider strategies, give TradersPost a try and [Register](https://traderspost.io/register) your free account today! If you have any questions, join our [Community](https://traderspost.io/community) or email us at [support@traderspost.io](mailto:support@traderspost.io).
