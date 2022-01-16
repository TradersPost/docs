---
description: >-
  TradingView is a social network of 30 million traders and investors using the
  world's best charts and tools to spot trading opportunities across global
  markets.
---

# TradingView

![](.gitbook/assets/TradingView.png)

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

![TradingView plain manually configured alert webhook.](https://traderspost.io/images/docs/trading-view/alert-window.png)

This is a simple example to demonstrate the basics of how you can integrate TradingView alerts with TradersPost but the same principals apply if you are doing something more advanced with a Pinescript indicator. Continue reading to learn how you can integrate your Pinescript indicators and alerts with TradersPost.

## Pinescript Studies

Here is a simple trend following momentum based indicator called MOMO that was created by [Matt DeLong](https://www.tradingview.com/u/MattDeLong/?offer\_id=10\&aff\_id=26514) from [RealLifeTrading.com](https://lddy.no/u5jf). It uses the **EMA8** and **EMA21** and the signal is when those two values cross each other.

The `message` parameter of the `alertcondition()` function is pre-populated with the JSON alert message required by TradersPost.

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

alertcondition(tradersPostBuy, title="TradersPost Buy Alert", message="{\"ticker\": \"{{ticker}}\", \"action\": \"buy\", \"price\": {{close}}}")
alertcondition(tradersPostSell, title="TradersPost Sell Alert", message="{\"ticker\": \"{{ticker}}\", \"action\": \"sell\", \"price\": {{close}}}")
```

Once you have the **Trend Following MOMO** indicator in your TradingView you can add it to your charts and it will look like the following with visual buy and sell indicators overlayed on top of your chart.

![MOMO Trend Following Indicator](https://traderspost.io/images/docs/trading-view/momo-home-depot.png)

Next, you can create alerts for the buy and sell signals and send them to TradersPost via webhooks. Follow these steps to setup the alerts as webhooks.

1. Open the **Alerts** pane in TradingView
2. Click **Create Alert** at the top right of the Alerts pane
3. Select **Trend Following MOMO** from the **Condition** dropdown
4. Select **TradersPost Buy Alert** or **TradersPost Sell Alert** under the **Condition** dropdown.
5. Click **Once Per Bar Close** next to **Options**
6. Paste your TradersPost webhook URL in the **Webhook URL** field.
7. Give your alert a name like **HD MOMO 1D Buy**

Here is what your alert should look like.

![MOMO Trend Following Indicator Alert Webhook](https://traderspost.io/images/docs/trading-view/momo-home-depot-alert.png)

Notice how the **Message** field in the alert was automatically filled in with the JSON that is required for TradersPost? This is made available to us by these two lines of code in the Pinescript.

```javascript
alertcondition(tradersPostBuy, title="TradersPost Buy Alert", message="{\"ticker\": \"{{ticker}}\", \"action\": \"buy\", \"price\": {{close}}}")
alertcondition(tradersPostSell, title="TradersPost Sell Alert", message="{\"ticker\": \"{{ticker}}\", \"action\": \"sell\", \"price\": {{close}}}")
```

## Pinescript Strategies

There are several different ways that you can build strategies in TradingView from studies that are purely visual indicators to strategies that are back testable.

### Custom Strategies

Here is an example where the JSON for the alert message is defined in the Pinescript strategy itself and passed to the `alert_message` parameter in functions like `strategy.entry()`.

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

### Complex Strategy&#x20;

Here is a much more complex version of the above strategy with many more features implemented.  It has the following additional features implemented.

* Both long and short trades
* Long and short take profit and stop losses
* Configure EMA length
* Configure backtest time window

```javascript
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © TradersPostInc

//@version=5
strategy('TradersPost Example MOMO Strategy', overlay=true, default_qty_value=100, initial_capital=100000, default_qty_type=strategy.percent_of_equity, pyramiding=0)

startTime = input.time(defval = timestamp('01 Jan 2021 00:00 +0000'), title = 'Start Time', group = 'Date Range')
endTime = input.time(defval = timestamp('31 Dec 2023 23:59 +0000'), title = 'End Time', group = 'Date Range')
timeCondition = time >= startTime and time < endTime
timeConditionEnd = timeCondition[1] and not timeCondition

fastEmaLength = input.int(defval = 8, title = 'Fast EMA Length')
slowEmaLength = input.int(defval = 21, title = 'Slow EMA Length')
sides = input.string(defval = 'Long', title = 'Sides', options = ['Long', 'Short', 'Both', 'None'])

fastEma = ta.ema(close, fastEmaLength)
slowEma = ta.ema(close, slowEmaLength)

isUptrend = fastEma >= slowEma
isDowntrend = fastEma <= slowEma
trendChanging = ta.cross(fastEma, slowEma)

ema105 = request.security(syminfo.tickerid, '30', ta.ema(close, 105)[1], barmerge.gaps_off, barmerge.lookahead_on)
ema205 = request.security(syminfo.tickerid, '30', ta.ema(close, 20)[1], barmerge.gaps_off, barmerge.lookahead_on)
plot(ema105, linewidth=4, color=color.new(color.purple, 0), editable=true)
plot(ema205, linewidth=2, color=color.new(color.purple, 0), editable=true)

aa = plot(fastEma, linewidth=3, color=color.new(color.green, 0), editable=true)
bb = plot(slowEma, linewidth=3, color=color.new(color.red, 0), editable=true)
fill(aa, bb, color=isUptrend ? color.green : color.red, transp=90)

tradersPostBuy = trendChanging and isUptrend and timeCondition
tradersPostSell = trendChanging and isDowntrend and timeCondition

pips = syminfo.pointvalue / syminfo.mintick

percentOrPipsInput = input.string('Percent', title='Percent or Pips', options=['Percent', 'Pips'])

stopLossLongInput = input.float(defval=0, step=0.01, title='Stop Loss Long', minval=0)
stopLossShortInput = input.float(defval=0, step=0.01, title='Stop Loss Short', minval=0)

takeProfitLongInput = input.float(defval=0, step=0.01, title='Target Profit Long', minval=0)
takeProfitShortInput = input.float(defval=0, step=0.01, title='Target Profit Short', minval=0)

stopLossPriceLong = ta.valuewhen(tradersPostBuy, close, 0) * (stopLossLongInput / 100) * pips
stopLossPriceShort = ta.valuewhen(tradersPostSell, close, 0) * (stopLossShortInput / 100) * pips

takeProfitPriceLong = ta.valuewhen(tradersPostBuy, close, 0) * (takeProfitLongInput / 100) * pips
takeProfitPriceShort = ta.valuewhen(tradersPostSell, close, 0) * (takeProfitShortInput / 100) * pips

takeProfitALong = takeProfitLongInput > 0 ? takeProfitLongInput : na
takeProfitBLong = takeProfitPriceLong > 0 ? takeProfitPriceLong : na

takeProfitAShort = takeProfitShortInput > 0 ? takeProfitShortInput : na
takeProfitBShort = takeProfitPriceShort > 0 ? takeProfitPriceShort : na

stopLossALong = stopLossLongInput > 0 ? stopLossLongInput : na
stopLossBLong = stopLossPriceLong > 0 ? stopLossPriceLong : na

stopLossAShort = stopLossShortInput > 0 ? stopLossShortInput : na
stopLossBShort = stopLossPriceShort > 0 ? stopLossPriceShort : na

takeProfitLong = percentOrPipsInput == 'Pips' ? takeProfitALong : takeProfitBLong
stopLossLong = percentOrPipsInput == 'Pips' ? stopLossALong : stopLossBLong
takeProfitShort = percentOrPipsInput == 'Pips' ? takeProfitAShort : takeProfitBShort
stopLossShort = percentOrPipsInput == 'Pips' ? stopLossAShort : stopLossBShort

buyAlertMessage = '{"ticker": "' + syminfo.ticker + '", "action": "buy", "price": ' + str.tostring(close) + '}'
sellAlertMessage = '{"ticker": "' + syminfo.ticker + '", "action": "sell", "price": ' + str.tostring(close) + '}'

if (sides != "None")
    if tradersPostBuy
        strategy.entry('Long', strategy.long, when = sides != 'Short', alert_message = buyAlertMessage)
        strategy.close('Short', when = sides == "Short" and timeCondition, alert_message = buyAlertMessage)

    if tradersPostSell
        strategy.entry('Short', strategy.short, when = sides != 'Long', alert_message = sellAlertMessage)
        strategy.close('Long', when = sides == 'Long', alert_message = sellAlertMessage)

longTakeProfitExitAlertMessage = '{"ticker": "' + syminfo.ticker + '", "action": "exit", "price": ' + str.tostring(close + (takeProfitLong / 100)) + '}'
longStopLossExitAlertMessage = '{"ticker": "' + syminfo.ticker + '", "action": "exit", "price": ' + str.tostring(close - (stopLossLong / 100)) + '}'

strategy.exit('Long Take Profit', from_entry = "Long", profit = takeProfitLong, alert_message = longTakeProfitExitAlertMessage)
strategy.exit('Long Stop Loss', from_entry = "Long", loss = stopLossLong, alert_message = longStopLossExitAlertMessage)

shortTakeProfitExitAlertMessage = '{"ticker": "' + syminfo.ticker + '", "action": "exit", "price": ' + str.tostring(close - (takeProfitShort / 100)) + '}'
shortStopLossExitAlertMessage = '{"ticker": "' + syminfo.ticker + '", "action": "exit", "price": ' + str.tostring(close + (stopLossShort / 100)) + '}'

strategy.exit('Short Take Profit', from_entry = "Short", profit = takeProfitShort, alert_message = shortTakeProfitExitAlertMessage)
strategy.exit('Short Stop Loss', from_entry = "Short", loss = stopLossShort, alert_message = shortStopLossExitAlertMessage)

strategy.close_all(when = timeConditionEnd)
```

### Shared Strategies

Sometimes you may want to hook up a strategy to TradersPost that was built by someone else and you do not have the ability to modify the Pinescript. You can easily send alerts from existing strategies and send the alerts as webhooks to TradersPost.

Just send the following JSON in the alert message to TradersPost.

```json
{
    "ticker": "{{ticker}}",
    "action": "{{strategy.order.action}}",
    "price": "{{close}}"
}
```

The `{{strategy.order.action}}` code will be dynamically replaced with a value of `buy` or `sell` when the strategy triggers an order.

If you are interested automating your TradingView strategies, give TradersPost a try and [Register](https://traderspost.io/register) your free account today! If you have any questions, join our [Community](https://traderspost.io/community) or email us at [support@traderspost.io](mailto:support@traderspost.io).
