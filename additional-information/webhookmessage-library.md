---
description: >-
  The WebhookMessage Library was built to make it easier to create JSON messages
  for TradingView strategies and indicators.
---

# WebhookMessage Library

{% embed url="https://www.tradingview.com/script/Dfo3ErmN-TradersPost-WebhookMessage-Library-Automatically-Build-JSON/" %}
Add this library to your favorites.
{% endembed %}

```
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © TradersPostInc (https://traderspost.io). Visit TradersPost to automate your TradingView strategies and indicators.

//@version=5

// @description The webhook message library provides several functions for building JSON payloads 
// used as instructions to manage automated orders and positions with TradersPost.io. See:
// https://docs.traderspost.io/docs/learn/webhooks
library("WebhookMessage", overlay = false)

// Example: Go long, 1 contract, with a 0.75% trailing stop
// import TradersPostInc/WebhookMessage/1 as wm
// cnst = wm.CONSTANTS.new()
// msg = wm.webhookMessage.new(
//   ticker = syminfo.ticker,
//   action = cnst.ACTION_BUY,
//   sentiment = cnst.SENTIMENT_BULLISH,
//   quantity = 1,
//   stopLoss = wm.stopLossMessage.new(type = cnst.STOP_LOSS_TYPE_TRAILING_STOP, trailPercent = 0.75).buildStopLossJson()
//   ).buildWebhookJson()
// alert(msg, freq = alert.freq_once_per_bar_close)

// @type Constants for payload values.
// @field <string> ACTION_BUY buy - Exit bearish position and optionally open bullish position. Used in webhookMessage.action.
// @field <string> ACTION_SELL sell - Exit bullish position and optionally open bearish position. Used in webhookMessage.action.
// @field <string> ACTION_EXIT exit - Exit open position without entering a new position on the other side. Used in webhookMessage.action.
// @field <string> ACTION_CANCEL cancel - Cancel open orders. Used in webhookMessage.action.
// @field <string> ACTION_ADD add - Add to existing open position. Used in webhookMessage.action.
// @field <string> SENTIMENT_BULLISH bullish - Open position after trade is executed should be bullish or flat. Used in webhookMessage.sentiment.
// @field <string> SENTIMENT_BEARISH bearish - Open position after trade is executed should be bearish or flat. Used in webhookMessage.sentiment.
// @field <string> SENTIMENT_FLAT flat - No position should be open after trade is executed. Used in webhookMessage.sentiment.
// @field <string> Stop loss type of market stop. Used in stopLossMessage.type.
// @field <string> Stop loss type of limit stop. Used in stopLossMessage.type.
// @field <string> Stop loss type of trailing stop. Used in stopLossMessage.type.
export type CONSTANTS
	ACTION_BUY                   = "buy"
	ACTION_SELL                  = "sell"
	ACTION_EXIT                  = "exit"
	ACTION_CANCEL                = "cancel"
	ACTION_ADD                   = "add"
	SENTIMENT_BULLISH            = "bullish"
	SENTIMENT_BEARISH            = "bearish"
	SENTIMENT_LONG               = "long"
	SENTIMENT_SHORT              = "short"
	SENTIMENT_FLAT               = "flat"
	STOP_LOSS_TYPE_STOP          = "stop"
	STOP_LOSS_TYPE_STOP_LIMIT    = "stop_limit"
	STOP_LOSS_TYPE_TRAILING_STOP = "trailing_stop"

cnst = CONSTANTS.new()

// @type Final webhook message. See: https://docs.traderspost.io/docs/learn/webhooks#what-is-a-webhook
// @field <string> ticker The ticker symbol name. Example: SPY.
// @field <string> action The signal action. Supported values are buy, sell, exit, cancel or add.
// @field <string> sentiment bullish, bearish, or flat.
// @field <float> price The price of the buy or sell action. If you omit this value, the current market price will be used when the trade is executed.
// @field <int> quantity The quantity to enter. If you omit this value, the quantity will be dynamically calculated or defaulted to 1.
// @field <takeProfitMessage> takeProfit. See takeProfitMessage.
// @field <stopLossMessage> stopLoss. See stopLossMessage.
export type webhookMessage
	string ticker
	string action
	string sentiment
	float price
	int quantity
	string takeProfit = ""
	string stopLoss = ""

// @type Take profit message. See: https://docs.traderspost.io/docs/learn/webhooks#signal-take-profit
// @field <string> limitPrice Absolute limit price calculated on the webhook sender side.
// @field <float> percent Relative percentage take profit to calculate relative to entry price. The entry price for market orders is estimated based on the mid point between the bid and ask on the most recent quote.
// @field <float> amount Relative dollar amount take profit to calculate relative to entry price. The entry price for market orders is estimated based on the mid point between the bid and ask on the most recent quote.
export type takeProfitMessage
	float limitPrice
	float percent
	float amount

// @type Stop loss message. See: https://docs.traderspost.io/docs/learn/webhooks#signal-stop-loss
// @field <string> type Type of stop loss. If a value is provided, it overrides the stop loss type configured in strategy subscription settings. Allowed values are: stop, stop_limit, trailing_stop.
// @field <float> percent Relative percentage stop loss to calculate relative to entry price.
// @field <float> amount Relative dollar amount stop loss to calculate relative to entry price.
// @field <float> stopPrice Absolute stop price calculated on the webhook sender side.
// @field <float> limitPrice Absolute limit price calculated on the webhook sender side. type must be set to stop_limit to use this field.
// @field <float> trailPrice A dollar value away from the highest water mark. If you set this to 2.00 for a sell trailing stop, the stop price is always hwm - 2.00. type must be set to trailing_stop to use this field.
// @field <float> trailPercent A percent value away from the highest water mark. If you set this to 1.0 for a sell trailing stop, the stop price is always hwm * 0.99. type must be set to trailing_stop to use this field.
export type stopLossMessage
	string type
	float percent
	float amount
	float stopPrice
	float limitPrice
	float trailPrice
	float trailPercent

// @function Builds the final JSON payload from a webhookMessage type.
// @param <webhookMessage> msg A prepared webhookMessage.
// @returns <string> A JSON Payload.
export method buildWebhookJson(webhookMessage msg) =>
	json = "{"
	json += '"library": "WebhookMessage"'
	json += ',"timestamp": "' + str.tostring(time) + '"'
	//ticker
	json += ',"ticker": "' + (msg.ticker == "" ? syminfo.ticker : msg.ticker) + '"'
	// action
	json += ',"action": "' + msg.action + '"'
	// sentiment
	if (msg.sentiment == cnst.SENTIMENT_BULLISH or msg.sentiment == cnst.SENTIMENT_BEARISH or msg.sentiment == cnst.SENTIMENT_LONG or msg.sentiment == cnst.SENTIMENT_SHORT or msg.sentiment == cnst.SENTIMENT_FLAT)
		json += ',"sentiment": "' + msg.sentiment + '"'
	// price
	json += msg.price > 0 ? ',"price": ' + str.tostring(msg.price) : ""
	// quantity
	json += msg.quantity > 0 ? ',"quantity": ' + str.tostring(msg.quantity) : ""
	// takeProfit
	if (msg.takeProfit != "")
		json += ',"takeProfit":' + msg.takeProfit
	// stopLoss
	if (msg.stopLoss != "")
		json += ',"stopLoss":' + msg.stopLoss
	json += "}"
	json

// @function Builds the takeProfit JSON message to be used in a webhook message.
// @param <takeProfitMessage> msg
// @returns <string> A JSON takeProfit payload.
export method buildTakeProfitJson(takeProfitMessage msg) =>
	json = '{'
	json += na(msg.limitPrice) ? "" : '"limitPrice": ' + str.tostring(msg.limitPrice)
	json += na(msg.percent) ? "" : '"percent": ' + str.tostring(msg.percent)
	json += na(msg.amount) ? "" : '"amount": ' + str.tostring(msg.amount)
	json += "}"
	json

// @function Builds the stopLoss JSON message to be used in a webhook message.
// @param <stopLossMessage> msg
// @returns <string> A JSON stopLoss payload.
export method buildStopLossJson(stopLossMessage msg) =>
	//overload type message if not configured properly
	if (not na(msg.limitPrice) and msg.type != cnst.STOP_LOSS_TYPE_STOP_LIMIT)
		msg.type := cnst.STOP_LOSS_TYPE_STOP_LIMIT
	if (not na(msg.trailPrice) or not na(msg.trailPercent) and msg.type != cnst.STOP_LOSS_TYPE_TRAILING_STOP)
		msg.type := cnst.STOP_LOSS_TYPE_TRAILING_STOP

	json = '{'
	messages = array.new_string(0)
	if (na(msg.type) == false)
		array.push(messages, '"type": "' + msg.type + '"')
	if (na(msg.percent) == false)
		array.push(messages, '"percent": ' + str.tostring(msg.percent))
	if (na(msg.amount) == false)
		array.push(messages, '"amount": ' + str.tostring(msg.amount))
	if (na(msg.stopPrice) == false)
		array.push(messages, '"stopPrice": ' + str.tostring(msg.stopPrice))
	if (na(msg.limitPrice) == false)
		array.push(messages, '"limitPrice": ' + str.tostring(msg.limitPrice))
	if (na(msg.trailPrice) == false)
		array.push(messages, '"trailPrice": ' + str.tostring(msg.trailPrice))
	if (na(msg.trailPercent) == false)
		array.push(messages, '"trailPercent": ' + str.tostring(msg.trailPercent))
	json += array.join(messages, ",")
	json += "}"
	json

//plot nothing to pass publishing rules
plot(0)
```
