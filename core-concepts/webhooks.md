---
description: >-
  TradersPost allows third party applications like TradingView and TrendSpider
  to integrate with your connected brokers via webhooks.
---

# Webhooks

## What is a webhook?

Webhooks are automated messages sent from applications when something happens. They have a [JSON message](json-messages.md) that can contain a payload of data and are sent to a unique URL.

In the context of automated trading, the webhook JSON message contains all the information about the trade signal like what ticker to buy and at what price. Here is an example simple webhook and JSON message.

<mark style="color:green;">POST</mark> `https://webhooks.traderspost.io/trading/webhook/{uuid}/{password}`

```json5
{
    "ticker": "AMD",
    "action": "buy",
    "signalPrice": 143.12,
    "quantity": 1,
    "takeProfit": {
        "percent": 10
    },
    "stopLoss": {
        "type": "stop",
        "percent": 5
    }
}
```

This example would route to a TradersPost [strategy](strategies.md), and then to one or more [strategy subscriptions](subscriptions.md) where the trade for AMD would be executed to buy 1 share of AMD with a take profit order at 10 percent above the potential entry price of 143.12 (assuming no slippage) and a stop market order 5 percent below the entry price of 143.12.

## Webhook Reference Documentation

A full, technical reference document is [available here](../developer-resources/webhook-reference.md) and covers every available request body property and possible response bodies.

## Webhook Field Reference

Here is a quick reference list of all the supported fields and values for the TradersPost webhook JSON message. These fields are case-sensitive and should be used in the way they are presented here. Fields other than the ones listed here can be sent, but will be ignored by TradersPost. This means you can send extra fields for debugging purposes, but we do recommend using the "extras" field for this purpose.

### ticker

{% hint style="warning" %}
REQUIRED FIELD: ticker is required with all JSON messages.
{% endhint %}

The ticker symbol of the financial instrument (e.g., `AAPL`, `SPY 250624C596`, `MNQU2025`, `BTCUSD`).

{% hint style="info" %}
**Note:** For futures contracts, continuous symbols like NQ1! are automatically mapped to the front-month contract according to our rollover schedule. Since this schedule may differ from other platforms like TradingView, we strongly recommend using explicit futures contract symbols rather than continuous symbols.
{% endhint %}

### action

{% hint style="warning" %}
REQUIRED FIELD: action is required with all JSON messages.
{% endhint %}

The action or signal type used to determine what type of order to execute.

{% hint style="info" %}
Possible values: `buy`, `sell`, `exit`, `cancel`, `add`
{% endhint %}

{% hint style="info" %}
**Note:** when you are trading put options, the action is inverted. So this means `action=buy` will sell to open short puts and `action=sell` will buy to open long puts. This is necessary when you are running a strategy on the underlying chart but you are buying and selling puts instead of shares.
{% endhint %}

{% code title="Example for ticker and action" %}
```json5
{
    "ticker": "MSFT",
    "action": "buy"
}
```
{% endcode %}

You can add to an existing open position by using the **add** action. This will add to the existing open position regardless of if **Allow add to position** is checked in your strategy subscription settings.

```json
{
    "ticker": "SQ",
    "action": "add"
}
```

#### Cancelling Open Orders

Cancel all the open orders for the given ticker.

```json
{
    "ticker": "SQ",
    "action": "cancel"
}
```

You can also control the open order canceling functionality with the `cancel` property so you can combine it with other actions. For example, if you want to exit the open position and cancel open orders first, you can use the following.

```json5
{
    "ticker": "SQ",
    "action": "exit",
    "cancel": true
}
```

If you have order canceling enabled in your strategy subscription settings and you want to disable the order canceling for a signal, you can send `cancel: false` as well.

```json5
{
    "ticker": "SQ",
    "action": "exit",
    "cancel": false
}
```

### sentiment

The sentiment field allows you to specify what the sentiment of the position should be _after_ executing the trade.&#x20;

{% hint style="info" %}
Supported values: `bullish`, `long` `bearish`, `short`, and`flat`
{% endhint %}

You can include the `sentiment` field with a value of `flat` to exit a bullish or bearish position without entering the opposite position. This means that it will always exit the full quantity of the open position without entering a new position on the other side.

If you send a JSON message with `action` set to `sell` and `sentiment` set to `flat`, it will exit a bullish position without entering a bearish position. Similarly, if you send `action` as `buy` and `sentiment` as `flat`, it will exit a bearish position without entering a bullish position.

You are also able to have a `sentiment` of `bullish` or `bearish`. This is useful whenever you are partially exiting a position and you aren't fully exiting the position and you aren't changing sides. For example, if you are in a `bearish` short position with a quantity of 10 and you send a JSON message with `action` set to `buy`, `quantity` set to `5` and sentiment set to `bearish`, this means that after executing the buy, you will still be in a `bearish` position with a quantity of 5.

### signalPrice (price)

{% hint style="info" %}
Note: `signalPrice` is optional. `price` is an alias for `signalPrice`.
{% endhint %}

This is the market price at the time your TradingView (or other platform) alert is triggered. You can pass it using the `{{close}}` placeholder in your alert message. TradersPost uses this value to estimate slippage (the difference between the alert price and the actual fill price) so you can see how much delay or movement occurred between your signal and the trade execution.

You can also send `price` which is an alias for `signalPrice`.

It is only necessary when you are using relative take profit or stop losses and the broker does not support fetching quotes to be able to perform the calculation. It is also used to determine the P\&L on your trade if the quote or fill price isn't available from your connection.

Here is an example where the price at the time of the signal was `$18500` and we specify that we want a `$100` take profit. So a take profit order with a limit price of `$18600` will be calculated and sent to your broker along with your market entry order.

```json
{
    "ticker": "MNQ",
    "action": "buy",
    "orderType": "market",
    "signalPrice": 18500,
    "takeProfit": {
        "amount": 100
    }
}
```

If you are using limit orders, then the `limitPrice` you send will be used to calculate your take profit.

```json
{
    "ticker": "MNQ",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": 18500,
    "takeProfit": {
        "amount": 100
    }
}
```

### limitPrice

The limit price of the buy or sell action if `limit` orders are used. If you omit this value and `limit` orders are used, the current market price will be used when the trade is executed.

### stopPrice

The stop price of the buy or sell action if `stop_limit` orders are used. If you omit this value and `stop` or `stop_limit` orders are used, the current market price will be used when the trade is executed.

### quantity

The quantity to enter. If you omit this value, the quantity will be dynamically calculated or defaulted to 1. Check **Use signal quantity** in your strategy subscription settings to use this quantity.

The signal `quantity` will only be used if you check **Use signal quantity** in the strategy subscription settings in TradersPost.

```json
{
    "ticker": "SQ",
    "action": "buy",
    "quantity": 5
}
```

{% hint style="danger" %}
The full quantity of the open position in the broker will be exited if you do not send a quantity in the exit signal. TradersPost is only able to partially exit open positions by sending the explicit quantity to exit in the webhook JSON.
{% endhint %}

### quantityType

{% hint style="info" %}
Supported values: `fixed_quantity`, `dollar_amount`, `risk_dollar_amount`, `percent_of_equity`, `percent_of_position`
{% endhint %}

The type of the value sent in the `quantity` field documented below. The default value is `fixed_quantity` when you send a `quantity` without a `quantityType`.

You can optionally send a value in the `quantityType` field to control how the value in the `quantity` field should be handled. By default the value in the `quantity` field is used as the quantity for the order directly.

This field is only used if you have **Use signal quantity** checked in the strategy subscription settings in TradersPost.

The supported values for `quantityType` are the following:

* `fixed_quantity` - A fixed quantity number that is used for the order. This is the default when you send a `quantity` without a `quantityType`.
* `dollar_amount` - Dynamically calculates a quantity for the given dollar amount.
* `risk_dollar_amount` - Dynamically calculates a quantity for the given risk dollar amount. This type requires a stop loss.
* `percent_of_equity` - Dynamically calculates a quantity for the given percent of equity.
* `percent_of_position` - Dynamically calculates a quantity for the given percent of position.

Here are some examples:

```json
{
    "ticker": "SQ",
    "action": "buy",
    "quantityType": "fixed_quantity",
    "quantity": 100
}
```

This will buy 100 shares of $SQ.

<pre class="language-json"><code class="lang-json"><strong>{
</strong>    "ticker": "SQ",
    "action": "buy",
    "quantityType": "dollar_amount",
    "quantity": 1000
}
</code></pre>

If the price of $SQ at the time of executing the trade was $100, then TradersPost would calculate a quantity of 10.

```json
{
    "ticker": "SQ",
    "action": "buy",
    "signalPrice": 100,
    "quantityType": "risk_dollar_amount",
    "quantity": 100,
    "stopLoss": {
        "type": "stop",
        "stopPrice": 90
    }
}
```

The `risk_dollar_amount` quantity in this example means you want to calculate a quantity that would only allow you to lose roughly $100 when the stop loss is hit. In this example, TradersPost would calculate a quantity of 10. If you enter at $100 and get stopped out at $90 and the most you want to lose is $100, then you can only buy a quantity of 10.

### orderType

{% hint style="info" %}
Supported values: `market`, `limit`, `stop`, `stop_limit`, and `trailing_stop`
{% endhint %}

The type of order to create.  If you send an order type not supported by your broker, it will fallback to the default order type configured in the strategy subscription settings. If that order type is still not supported, the order will be rejected by the broker.

The signal `orderType` will only be used if you check **Use signal order type for entries** or **Use signal order type for exits**.

```json
{
    "ticker": "SQ",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": 50.50
}
```

Or if you want to use a stop limit order:

```json
{
    "ticker": "SQ",
    "action": "buy",
    "orderType": "stop_limit",
    "stopPrice": 60,
    "limitPrice": 50.50
}
```

### trailAmount

When `orderType=trailing_stop`, you can send a dollar amount  in the `trailAmount` field to create a trailing stop order.

### trailPercent

When `orderType=trailing_stop`, you can send a percentage in the `trailPercent` field to create a trailing stop order.

### timeInForce

{% hint style="info" %}
Supported values: `day`, `gtc`, `opg`, `cls`, `ioc` and `fok`
{% endhint %}

The time in force for your order. If you send a time in force not supported by your broker, it will fallback to the default time in force or the time in force configured in the strategy subscription settings.

This time in force will only be used if you have **Use signal time in force for entries** or **Use signal time in force for exits** checked.

Example:

```json5
{
    "ticker": "SQ",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": 50.50,
    "timeInForce": "gtc"
}
```

Or if want to send the order with extended hours enabled so that the order can be filled in extended hours, you can use the `extendedHours` field to send a `true` or `false` value.

```json
{
    "ticker": "SQ",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": 50.50,
    "timeInForce": "gtc",
    "extendedHours": true
}
```

### time

The time property is used to keep track of the time the signal was generated and the request to TradersPost was started. It can also be used to calculate the time it takes between the signal source and getting to TradersPost.

### extendedHours

Whether or not to send the order as an extended hours order. This is only applicable for stocks and the supported values are true or false.

### ignoreTradingWindows

You can use the `ignoreTradingWindows` property in your JSON to ignore the defined trading windows in the strategy subscription settings and allow the trade to execute even if it is outside of the defined trading windows.

Here is an example where maybe you entered a `SPY` position while the trading window was open, and you now you want to exit the position but the trading window is closed. Simply send the `ignoreTradingWindows` property with a value of `true` and the trade will be allowed to execute.

```json5
{
    "ticker": "SPY",
    "action": "exit",
    "ignoreTradingWindows": true
}
```

### cancel

Explicitly control whether or not to cancel open orders before submitting new orders to your broker.

### extras

Users can send additional custom JSON properties within an "extras" field, allowing for more detailed information or contextual data to be included with each request. By keeping the properties inside an "extras" property, you avoid conflicting with TradersPost properties defined on this page. This is useful for tracking specific conditions or notes related to a trade. For example:

```json5
{
    "ticker": "SQ",
    "action": "buy",
    "extras": {
        "message": "RSI Below 30",
        "rsi": 23
    }
}
```

## Webhook Field Reference - Take Profit and Stop Loss

### takeProfit

{% hint style="info" %}
Supported values: `limitPrice`, `price`, `percent`
{% endhint %}

You can optionally send take profit information with your entry signals.

{% hint style="info" %}
The signal take profit will only be used if you check **Use signal take profit** in the strategy subscription settings in TradersPost.
{% endhint %}

The following fields are allowed on the **takeProfit** object, but never together. You can only choose one of the three types of take profit types (limitPrice, percent, or amount).

* **limitPrice** - Absolute limit price calculated on the webhook sender side.
* **percent**: Relative percentage take profit to calculate relative to entry price. The entry price for market orders is estimated based on the mid point between the bid and ask on the most recent quote.
* **amount** - Relative dollar amount take profit to calculate relative to entry price. The entry price for market orders is estimated based on the mid point between the bid and ask on the most recent quote.

#### **Percentage take profit calculated relative to entry price.**

{% hint style="info" %}
When using market orders and you are calculating a relative take profit price, TradersPost will fetch a quote from your broker and use the price from the quote as the entry price in order to calculate the take profit limit price since with markets orders, we don't know the price you will be filled at so we have to use the quote price.
{% endhint %}

```json
{
    "ticker": "SQ",
    "action": "buy",
    "takeProfit": {
        "percent": 10
    }
}
```

#### **Dollar amount take profit calculated relative to entry price.**

```json
{
    "ticker": "SQ",
    "action": "buy",
    "takeProfit": {
        "amount": 10
    }
}
```

#### **Absolute take profit calculated on the webhook sender side.**

```json
{
    "ticker": "SQ",
    "action": "buy",
    "takeProfit": {
        "limitPrice": 19.99
    }
}
```

### stopLoss

{% hint style="info" %}
Supported values: `type`, `percent`, `amount`, `stopPrice`,  `limitPrice`, `trailAmount` and `trailPercent`
{% endhint %}

You can optionally send stop loss information with your entry signals.

{% hint style="info" %}
The signal stop loss will only be used if you check **Use signal stop loss** in the strategy subscription settings in TradersPost.
{% endhint %}

The following fields are allowed on the **stopLoss** object.

* **type** - Type of stop loss. If a value is provided, it overrides the stop loss type configured in strategy subscription settings. Allowed values are: stop, stop\__limit, trailing\_stop._
* **percent**: Relative percentage stop loss to calculate relative to entry price.
* **amount** - Relative dollar amount stop loss to calculate relative to entry price.
* **stopPrice** - Absolute stop price calculated on the webhook sender side.
* **limitPrice** - Absolute limit price calculated on the webhook sender side. **type** must be set to **stop\_limit** to use this field.
* **trailAmount** - A dollar value away from the highest water mark. If you set this to 2.00 for a sell trailing stop, the stop price is always hwm - 2.00. **type** must be set to **trailing\_stop** to use this field.
* **trailPercent** - A percent value away from the highest water mark. If you set this to 1.0 for a sell trailing stop, the stop price is always hwm \* 0.99. **type** must be set to **trailing\_stop** to use this field.

**Percentage stop loss calculated relative to entry price.**

{% hint style="info" %}
When using market orders and you are calculating a relative stop loss price, TradersPost will fetch a quote from your broker and use the price from the quote as the entry price in order to calculate the stop loss stop price since with markets orders, we don't know the price you will be filled at so we have to use the quote price.
{% endhint %}

```json
{
    "ticker": "SQ",
    "action": "buy",
    "stopLoss": {
        "type": "stop",
        "percent": 5
    }
}
```

#### **Dollar amount stop loss calculated relative to entry price.**

```json
{
    "ticker": "SQ",
    "action": "buy",
    "stopLoss": {
        "type": "stop",
        "amount": 5
    }
}
```

#### **Absolute stop price calculated on the webhook sender side.**

```json
{
    "ticker": "SQ",
    "action": "buy",
    "stopLoss": {
        "type": "stop",
        "stopPrice": 10.71
    }
}
```

#### **Or with a stop limit instead of stop market.**

```json
{
    "ticker": "SQ",
    "action": "buy",
    "stopLoss": {
        "type": "stop_limit",
        "stopPrice": 10.71,
        "limitPrice": 10.75
    }
}
```

#### **Use a 1% trailing stop trail percent.**

```json
{
    "ticker": "SQ",
    "action": "buy",
    "stopLoss": {
        "type": "trailing_stop",
        "trailPercent": 1
    }
}
```

#### **Use a $1 trailing stop trail price.**

```json
{
    "ticker": "SQ",
    "action": "buy",
    "stopLoss": {
        "type": "trailing_stop",
        "trailAmount": 1
    }
}
```

## Webhook Field Reference - Options Contracts and Screening

{% hint style="warning" %}
When you are trading put options, the action is inverted. So this means action=buy will sell to open short puts and action=sell will buy to open long puts. This is necessary when you are running a strategy on the underlying chart but you are buying and selling puts instead of shares.
{% endhint %}

You have the ability to control the option chain scanning from the webhook or you can even send a specific contract to trade instead of scanning the option chain dynamically to find a contract to trade. Here is an example that will buy long calls using the contract in the `ticker` field.

```json
{
    "ticker": "SQ 240510C68",
    "action": "buy"
}
```

Or if you want to instead scan the option chain dynamically to find a contract to trade, you can do so like this. This example will scan the option chain and look for an in the money call that is expiring 6 months from now and is 2 strikes away from at the money.

```json
{
    "ticker": "SQ",
    "action": "buy",
    "optionType": "call",
    "expiration": "+6 months",
    "intrinsicValue": "itm",
    "strikesAway": 2
}
```

You can also specify the specific contract to trade with individual values instead of using the contract symbol in the `ticker` field. The following is equivalent to sending `SQ 240510C68` in the `ticker` field.

```json
{
    "ticker": "SQ",
    "action": "buy",
    "optionType": "call",
    "expiration": "2024-05-10",
    "strikePrice": 68
}
```

### optionType

{% hint style="info" %}
Supported values: `both`, `call` and `put`
{% endhint %}

Specify the type of option contract for trading: `call`, `put`, or `both`.

### intrinsicValue

{% hint style="info" %}
Supported values: `itm`, `otm`
{% endhint %}

The intrinsic value of the option contract to trade. The only values allowed are `itm` for in-the-money and `otm` for out-of-the-money.

### expiration

The expiration of the option contract to trade. The value can be a specific date like `2024-05-06` or a relative date expression like `+6 months`. This should be used to filter the nearest contract _after_ the specified date or date expression. For example, for 0DTE options, you can use `+0 days`, or omit this field. For options a year out, use `+12 months`.

### strikeCount

How many strikes to ask for from the broker when executing options trades and scanning the option chain to find a contract to trade.

### strikesAway

How many strikes away from at the money to select.

### strikePrice

Specifies the strike price of the option contract to trade.

## JSON Message Examples

Here are some example webhook JSON messages to demonstrate the different use cases.

### Enter Bullish

```json
{
    "ticker": "SQ",
    "action": "buy"
}
```

### Exit Bullish

```json
{
    "ticker": "SQ",
    "action": "exit"
}
```

You can also use the sentiment field to exit a bullish position without entering a bearish position on the other side. When you send sentiment=flat, it will always exit the full quantity of the open position.

```json
{
    "ticker": "SQ",
    "action": "sell",
    "sentiment": "flat"
}
```

When you use `sentiment: flat` feature, TradersPost will always exit the full quantity of the open position no matter what quantity is sent in the signal. This is because the sentiment is indicating that the position should be flattened.

### Enter Bearish

```json
{
    "ticker": "SQ",
    "action": "sell"
}
```

### Exit Bearish

```json
{
    "ticker": "SQ",
    "action": "exit"
}
```

You can also use the sentiment field to exit a bearish position without entering a bullish position on the other side. When you send sentiment=flat, it will always exit the full quantity of the open position.

```json
{
    "ticker": "SQ",
    "action": "buy",
    "sentiment": "flat"
}
```

When you use `sentiment: flat` feature, TradersPost will always exit the full quantity of the open position no matter what quantity is sent in the signal. This is because the sentiment is indicating that the position should be flattened.

### Partial Exits

You can partially exit an open position by using `action: exit` and sending a `quantity` in the signal with a value less than the quantity of the open position. So imagine you are long 5 shares and you want to exit 2 of them, you would send a JSON message like this.

```json5
{
    "ticker": "SQ",
    "action": "exit",
    "quantity": 2
}
```

The above JSON would partially exit the open position and exit 2 of the 5 total shares. If you send a quantity that is greater than the quantity of the open position, the full position will be exited.

### Trailing Stop

You can easily create trailing stop orders by sending `trailing_stop` in the `orderType` field. The following JSON will create a $1 trailing stop order for the open SQ position.

```json
{
    "ticker": "SQ",
    "action": "exit",
    "orderType": "trailing_stop",
    "signalPrice": 71,
    "trailAmount": "1"
}
```

{% hint style="info" %}
Note that if the broker you are using does not support fetching quotes, you will need to be sure to send the current price in the `signalPrice`field so that we can use that price to calculate your trailing stop price. In the above example, the starting trailing stop price would be $70. If the price moves up to $72, then the trailing stop price would update to $71.
{% endhint %}

If you want to send a trailing stop with your entry order so that the trailing stop order is active immediately after your entry order fills and your position is open, you can do so by using the `stopLoss` object. The following example will create a buy limit order with a limit price of $71 and a trailing stop loss order with an initial trailing stop price of $70.

```json
{
    "ticker": "SQ",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": 71,
    "stopLoss": {
        "type": "trailing_stop",
        "trailAmount": 1
    }
}
```

### Take Profit & Stop Loss

You can use the take profit and stop loss functionality together. Just send us both the `takeProfit` and `stopLoss` with your entry signal. Here is an example.

```json
{
    "ticker": "SQ",
    "action": "buy",
    "takeProfit": {
        "limitPrice": 19.99
    },
    "stopLoss": {
        "type": "stop",
        "stopPrice": 10.71
    }
}
```

## 400 Bad Request

The JSON that gets sent to TradersPost has to be precisely accurate in order for us to accept it. It is important to pay attention all the details, all the little characters have meaning and are important. Here are the types of errors you may encounter when sending JSON to TradersPost webhooks.

**post-required** - HTTP POST method is required.

All webhook HTTP requests must be sent with a request method of POST. All other request methods will not be accepted.

**malformed-json** - Could not parse JSON message.

If you have a parse error in your JSON code, TradersPost will not be able to extract the instructions from the signal. Here are some common mistakes people make.

**No trailing comma**

Notice the trailing comma on line 3, the JSON specification requires that there be no final trailing comma on the last item in a JSON object.

```json
{
    "ticker": "TSLA",
    "action": "buy",
}
```

Here is the corrected JSON.

```json
{
    "ticker": "TSLA",
    "action": "buy"
}
```

**Invalid double quote character**

Some applications will convert a double quote like `"quote"` to a left and right side double quote like `“quote”`. Notice the difference between `"` and `“` . JSON parsers don't like it when you use the latter. Here is an example invalid signal.

```
{
    “ticker”: “TSLA”,
    “action”: “buy”
}
```

Here is the corrected JSON.

```json
{
    "ticker": "TSLA",
    "action": "buy"
}
```

**invalid-payload** - Invalid payload. action and ticker is required. Note: payload is another name used for JSON message.

The minimum required fields are an action and ticker. All other fields are optional.

**invalid-action** - Invalid action provided.

Action must be one of: buy, sell, exit, cancel, add. The available actions available for webhooks are buy, sell, exit, cancel and add.

**invalid-sentiment** - Invalid sentiment provided.

Sentiment must be one of: bullish, bearish, flat. The available sentiments are bullish, bearish and flat. You can optionally exchange long for bullish and short for bearish. This is for compatibility with TradingView strategies out of the box.

**invalid-sentiment-action** - Invalid sentiment action provided.

Sentiment can only be used with action buy or sell. You can only pass a sentiment in a webhook request when using action=buy or action=sell.

For example, sending a JSON message with `"action": "exit"` and `"sentiment": "flat"` will produce an error since only the `"action": "exit"` is needed.

```json5
// Invalid JSON
{
    "ticker": "GOOGL",
    "action": "exit",
    "sentiment": "flat"
}

// Valid JSON that will exit the entire GOOGL position
{
    "ticker": "GOOGL",
    "action": "exit"
}
```

**not-trading-view** - Request did not come from TradingView.

If you check Limit to TradingView in your webhook configuration, then the only IP addresses that will be allowed to send a request to it will be from TradingView.

**not-trend-spider** - Request did not come from TrendSpider.

If you check Limit to TrendSpider in your webhook configuration, then the only IP addresses that will be allowed to send a request to it will be from TrendSpider.

**invalid-ip-address** - Request did not come from configured IP addresses.

If you enter an ip address in Limit to IP Addresses in your webhook configuration, then the only IP addresses that will be allowed to send a request to it will be from the configure ip addresses.

**ticker-does-not-exist** - Ticker does not exist.

If the passed ticker does not exist in our ticker database then the webhook request will be rejected.

**invalid-password** - Password is invalid.

Every webhook has a password that can be regenerated by clicking the Generate New URL button when viewing a webhook

**empty-ticker-name** - Empty ticker name provided.

Sending an empty ticker name is not allowed.

```json
{
    "ticker": "",
    "action": "buy"
}
```

**unsupported-ticker** - Ticker is not allowed on this webhook.

If your webhook is restricted to a specific list of tickers and you send a ticker not in that list, then the webhook request will be rejected.

i**nvalid-quantity** - Invalid quantity.

Quantities must be a valid numeric value. Any other non numeric values will cause the webhook request to be rejected.

**invalid-asset-class** - Invalid asset class.

If you send a ticker for an asset class that the webhook does not support, then the webhook request will be rejected.

## Rate Limits

TradersPost is **NOT** designed to be a high frequency trading platform. The minimum allowed timeframe to trade on is the 1 minute chart. You are allowed to send 60 requests per minute and 500 requests per hour. If you setup a strategy on anything less than the 1 minute chart, your account may be temporarily suspended or permanently banned if the issue is not addressed. Read more about our rate limiting behavior [here](../learn/platform-concepts/rate-limits.md).

## Third Parties

Because TradersPost works using standard webhooks, this enables users to integrate with third party platforms that support sending alerts as webhooks.

Here are some popular platforms that enable you to build strategies and send alerts as webhooks.

* [TradingView](../learn/signal-sources/tradingview.md) - TradingView is a social network of 30 million traders and investors using the world's best charts and tools to spot trading opportunities across global markets.
* [TrendSpider](../learn/signal-sources/trend-spider.md) - TrendSpider provides technical analysis software for retail traders and investors focused on the US equity and foreign exchange markets.

## Custom Code

In addition to sending webhooks from third parties, you can send webhooks to TradersPost from custom code using programming languages like [PHP](https://php.net) or [Python](https://www.python.org).

{% content-ref url="../developer-resources/custom-code-examples.md" %}
[custom-code-examples.md](../developer-resources/custom-code-examples.md)
{% endcontent-ref %}
