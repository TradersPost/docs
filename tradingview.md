---
description: >-
  TradingView is a tool that lets you perform technical analysis on charts in
  addition to building and backtesting strategies in their custom scripting
  language PineScript.
---

# TradingView

## Alert Message JSON

The TradersPost webhook system lets you easily integrate alerts from platforms like [TradingView](https://www.tradingview.com/?offer\_id=10\&aff\_id=26514) with TradersPost. Webhooks can receive [JSON](https://en.wikipedia.org/wiki/JSON) like the following.

```json
{
    "ticker": "TSLA",
    "action": "buy",
    "price": "420.69"
}
```

This JSON data structure is very important and it must be 100% correct otherwise TradersPost will not be able to parse the data out of the JSON in order to use the information correctly.

You can dynamically send the values in the above JSON using TradingView variables. You can read more about TradingView variables [here](https://www.tradingview.com/support/solutions/43000531021-how-to-use-a-variable-value-in-alert/?offer\_id=10\&aff\_id=26514).

```json
{
    "ticker": "{{ticker}}",
    "action": "buy",
    "price": "{{close}}"
}
```

The values inside of the **{{** and **}}** will be dynamically replaced by TradingView when the alert triggers.

When you create an alert in TradingView, you only need to enter the above JSON in the **Message** field and the URL of your webhook in the **Webhook URL** field. Here is a screenshot of a simple example that would send a signal to buy **SQ** when the price crosses above **241.94**.

![](https://traderspost.io/images/docs/trading-view/alert-window.png)

This is a simple example to demonstrate the basics of how you can integrate TradingView alerts with TradersPost but the same principals apply if you are doing something more advanced with a Pinescript indicator. Continue reading to learn how you can integrate your Pinescript indicators and alerts with TradersPost.

## Pinescript Study alertcondition()

Here is a simple trend following momentum based indicator called MOMO that was created by [Matt DeLong](https://www.tradingview.com/u/MattDeLong/?offer\_id=10\&aff\_id=26514) from [RealLifeTrading.com](https://lddy.no/u5jf). It uses the **EMA8** and **EMA21** and the signal is when those two values cross each other.

```javascript
//@version=4
//author = https://www.tradingview.com/u/MattDeLong/

study("Trend Following MOMO", overlay=true)

ema8 = ema(close, 8)
ema21 = ema(close, 21)

isUptrend = ema8 >= ema21
isDowntrend = ema8 <= ema21
trendChanging = cross(ema8, ema21)

tradersPostBuy = trendChanging and isUptrend
tradersPostSell = trendChanging and isDowntrend

plotshape(tradersPostBuy, style=shape.triangleup, location=location.belowbar, color=color.green, size=size.small, text='Buy')
plotshape(tradersPostSell, style=shape.triangledown, location=location.abovebar, color=color.red, size=size.small, text='Sell')

aa = plot(ema8, linewidth=3, color=color.green, editable=true, title="ema8")
bb = plot(ema21,linewidth=3, color=color.red, editable=true, title="ema21")
fill(aa, bb, color=isUptrend ? color.green : color.red)

alertcondition(tradersPostBuy, title="TradersPost Buy Alert", message="{\"time\": \"{{timenow}}\", \"interval\": \"{{interval}}\", \"ticker\": \"{{ticker}}\", \"action\": \"buy\", \"open\": {{open}}, \"high\": {{high}}, \"low\": {{low}}, \"close\": {{close}}}")
alertcondition(tradersPostSell, title="TradersPost Sell Alert", message="{\"time\": \"{{timenow}}\", \"interval\": \"{{interval}}\", \"ticker\": \"{{ticker}}\", \"action\": \"sell\", \"open\": {{open}}, \"high\": {{high}}, \"low\": {{low}}, \"close\": {{close}}}")
```

Once you have the **Trend Following MOMO** indicator in your TradingView you can add it to your charts and it will look like the following with visual buy and sell indicators overlayed on top of your chart.

![](https://traderspost.io/images/docs/trading-view/momo-home-depot.png)

Next, you can create alerts for the buy and sell signals and send them to TradersPost via webhooks. Follow these steps to setup the alerts as webhooks.

1. Open the **Alerts** pane in TradingView
2. Click **Create Alert** at the top right of the Alerts pane
3. Select **Trend Following MOMO** from the **Condition** dropdown
4. Select **TradersPost Buy Alert** or **TradersPost Sell Alert** under the **Condition** dropdown.
5. Click **Once Per Bar Close** next to **Options**
6. Paste your TradersPost webhook URL in the **Webhook URL** field.
7. Give your alert a name like **HD MOMO 1D Buy**

Here is what your alert should look like.

![](https://traderspost.io/images/docs/trading-view/momo-home-depot-alert.png)

Notice how the **Message** field in the alert was automatically filled in with the JSON that is required for TradersPost? This is made available to us by these two lines of code in the Pinescript.

```javascript
alertcondition(tradersPostBuy, title="TradersPost Buy Alert", message="{\"time\": \"{{timenow}}\", \"interval\": \"{{interval}}\", \"ticker\": \"{{ticker}}\", \"action\": \"buy\", \"open\": {{open}}, \"high\": {{high}}, \"low\": {{low}}, \"close\": {{close}}}")
alertcondition(tradersPostSell, title="TradersPost Sell Alert", message="{\"time\": \"{{timenow}}\", \"interval\": \"{{interval}}\", \"ticker\": \"{{ticker}}\", \"action\": \"sell\", \"open\": {{open}}, \"high\": {{high}}, \"low\": {{low}}, \"close\": {{close}}}")
```

## Pinescript Strategy Alert Message

There are several different ways that you can build strategies in TradingView from studies that are purely visual indicators to strategies that are back testable. Here is an example where the JSON for the alert message is defined in the Pinescript strategy itself and passed to the `alert_message` parameter in functions like `strategy.entry()`.

```javascript
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © TradersPostInc

//@version=5
strategy('TradersPost Example MOMO Strategy', overlay=true)

ema8 = ta.ema(close, 8)
ema21 = ta.ema(close, 21)

isUptrend = ema8 >= ema21
isDowntrend = ema8 <= ema21
trendChanging = ta.cross(ema8, ema21)

tradersPostBuy = trendChanging and isUptrend
tradersPostSell = trendChanging and isDowntrend

buyAlertMessage = '{"ticker": "' + syminfo.ticker + '", "action": "buy", "price": ' + str.tostring(close) + '}'
sellAlertMessage = '{"ticker": "' + syminfo.ticker + '", "action": "sell", "price": ' + str.tostring(close) + '}'

if tradersPostBuy
    strategy.entry("Long", strategy.long, alert_message = buyAlertMessage)

if tradersPostSell
    strategy.close("Long", when = open[0], alert_message = sellAlertMessage)
```

Then when you are setting up the alert for your strategy you can put the following code in the `Alert Message` text area.

```
{{strategy.order.alert_message}} 
```

&#x20;

If you are interested automating your TradingView strategies, give TradersPost a try and [Register](https://traderspost.io/register) your free account today! If you have any questions, join our [Community](https://traderspost.io/community) or email us at [support@traderspost.io](mailto:support@traderspost.io).
