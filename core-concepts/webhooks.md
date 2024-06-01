---
description: >-
  TradersPost allows third party applications like TradingView and TrendSpider
  to integrate with your connected brokers via webhooks.
---

# Webhooks

## What is a webhook?

Webhooks are automated messages sent from applications when something happens. They have a message that can contain a payload of data and are sent to a unique URL.

In the context of automated trading, the webhook message contains all the information about the trade signal like what ticker to buy and at what price. Here is an example simple webhook.

```json
{
    "ticker": "AMD",
    "action": "buy"
}
```

## Create a Webhook

Once you have [connected your broker](brokers/#connect-your-broker), you will be ready to create a webhook. To create your first webhook, follow these steps.

1. Navigate to **Webhooks** and click the **New Webhook** button at the top right. Give it a name and choose which asset class this webhook should work for.
2. Review the other optional available settings. These settings are optional and can be ignored if you are just getting started.
3. Finally, click the **Save** button and your webhook will be created.
4. Now you will see a **Webhook URL** and a **Copy** button. You can use the copy button to copy the webhook URL to your clipboard for pasting it in TradingView later.

Next, you are ready to create a [strategy](strategies.md).

{% hint style="info" %}
You can continue reading and learning about webhooks below. You can always come back to this page later to learn about the functionality that you can control with the webhook JSON payload.
{% endhint %}

## Webhook API Documentation

Here is a quick reference list of all the supported fields and values for the TradersPost webhook JSON.

* **ticker** - The ticker symbol name. Example **AMD.**
* **action** - The signal action. The supported values are `buy`, `sell`,  `exit`, `cancel` or `add`.
* **sentiment** - The signal sentiment. The supported values are `bullish`, `long`, `bearish`, `short` and `flat`.
* **optionType** - The type of option contract to trade. The supported values are `both`, `call` and `put`.
* **intrinsicValue** - The intrinsic value of the option contract to trade. The supported values are `itm` (in the money) and `otm` (out of the money).
* **expiration** - The expiration of the option contract to trade. The value can be a specific date like `2024-05-06` or a relative date expression like `+6 months`.
* **strikeCount** - How many strikes to ask for from the broker when executing options trades and scanning the option chain to find a contract to trade.
* **strikesAway** - How many strikes away from at the money to select.
* **orderType** - The type of order to create. Supported values are `market`, `limit`, `stop`, `stop_limit`, and `trailing_stop`.
* **limitPrice** - The limit price of the buy or sell action if `limit` orders are used. If you omit this value and `limit` orders are used, the current market price will be used when the trade is executed.
* **stopPrice** - The stop price of the buy or sell action if `stop_limit` orders are used. If you omit this value and `stop` or `stop_limit` orders are used, the current market price will be used when the trade is executed.
* **trailAmount** - When `orderType=trailing_stop`, you can send a dollar amount  in the `trailAmount` field to create a trailing stop order.
* **trailPercent** - When `orderType=trailing_stop`, you can send a percentage in the `trailPercent` field to create a trailing stop order.
* **quantityType** - The type of the value sent in the `quantity` field documented below. The only supported values are `fixed_quantity`, `dollar_amount`, `risk_dollar_amount`, `percent_of_equity`, `percent_of_position`. Default is `fixed_quantity` when you send a `quantity` without a `quantityType`.
* **quantity** - The quantity to enter. If you omit this value, the quantity will be dynamically calculated or defaulted to 1. Check **Use signal quantity** in your strategy subscription settings to use this quantity.
* **takeProfit** - The take profit to attach to your entry order. This objects supported fields are `limitPrice`, `price`, `percent`. Check **Use signal take profit** in your strategy subscription settings to use this take profit.
* **stopLoss** - The stop loss to attach to your entry order. This objects supported fields are `type`, `percent`, `amount`, `stopPrice`,  `limitPrice`, `trailAmount` and `trailPercent`. Check **Use signal stop loss** in your strategy subscription settings to use this stop loss.
* **timeInForce** - The time in force for your order. The supported values are `day`, `gtc`, `gtd`, `opg`, `cls`, `ioc` and `fok`.
* **extendedHours** - Whether or not to send the order as an extended hours order. This is only applicable for stocks and the supported values are `true` or `false`.

Properties other than the ones listed above can be sent, but will be ignored by TradersPost. This means you can send extra properties for debugging purposes.

Here is the full reference documentation for the TradersPost webhook JSON.

## TradersPost Webhook Request API documentation.

<mark style="color:green;">`POST`</mark> `https://webhooks.traderspost.io/trading/webhook/{uuid}/{password}`

#### Query Parameters

| Name                                       | Type   | Description                                                                                                                                        |
| ------------------------------------------ | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| uuid<mark style="color:red;">\*</mark>     | String | Unique webhook UUID string used to identify a webhook. This never changes.                                                                         |
| password<mark style="color:red;">\*</mark> | String | Password string used to protect access to your webhook. You can change this by clicking Generate New URL in TradersPost when editing your webhook. |

#### Request Body

| Name                                     | Type    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ---------------------------------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ticker<mark style="color:red;">\*</mark> | String  | The ticker symbol name. Example **AMD**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| action<mark style="color:red;">\*</mark> | String  | <p>The signal action. Supported values are the following:</p><p></p><p><code>buy</code> - Exit bearish position and optionally open bullish position</p><p></p><p><code>sell</code> - Exit bullish position and optionally open bearish position</p><p></p><p><code>exit</code> - Exit open position without entering a new position on the other side.</p><p></p><p><code>cancel</code> - Cancel open orders</p><p></p><p><code>add</code> - Add to existing open position</p>                                                                                                                                                                                                                                                                                                                                                                            |
| sentiment                                | String  | <p><code>bullish</code> - Open position after trade is executed should be bullish or flat.</p><p></p><p><code>bearish</code> - Open position after trade is executed should be bearish or flat.</p><p></p><p><code>flat</code> - No position should be open after trade is executed.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| optionType                               | String  | The type of option contract to trade. The supported values are `both`, `call` and `put`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| intrinsicValue                           | String  | The intrinsic value of the option contract to trade. The supported values are `itm` (in the money) and `otm` (out of the money).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| expiration                               | String  | The expiration of the option contract to trade. The value can be a specific date like `2024-05-06` or a relative date expression like `+6 months`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| strikeCount                              | Integer | How many strikes to ask for from the broker when executing options trades and scanning the option chain to find a contract to trade.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| strikesAway                              | Integer | How many strikes away from at the money to select.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| orderType                                | String  | The type of order to create. Supported values are `market`, `limit`, `stop`, `stop_limit`, and `trailing_stop`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| limitPrice                               | Number  | The price of the buy or sell action. If you omit this value, the current market price will be used when the trade is executed.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| stopPrice                                | Number  | The stop price of the buy or sell action if `stop_limit` orders are used. If you omit this value and `stop` or `stop_limit` orders are used, the current market price will be used when the trade is executed.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| trailAmount                              | Number  | When `orderType=trailing_stop`, you can send a dollar amount  in the `trailAmount` field to create a trailing stop order.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| trailPercent                             | Number  | When `orderType=trailing_stop`, you can send a percentage in the `trailPercent` field to create a trailing stop order.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| quantityType                             | Number  | <p>The type of the value sent in the <code>quantity</code> field documented below. Supported values are the following:</p><p></p><p><code>fixed_quantity</code> - A fixed quantity number that is used for the order.</p><p></p><p><code>dollar_amount</code> - Dynamically calculates a quantity for the given dollar amount.</p><p></p><p><code>risk_dollar_amount</code> - Dynamically calculates a quantity for the given risk dollar amount. This type requires a stop loss.</p><p></p><p><code>percent_of_equity</code> - Dynamically calculates a quantity for the given percent of equity.</p><p></p><p><code>percent_of_position</code> - Dynamically calculates a quantity for the given percent of position.</p><p></p><p>Default is <code>fixed_quantity</code> when you send a <code>quantity</code> without a <code>quantityType</code>.</p> |
| quantity                                 | Number  | The quantity to enter. If you omit this value, the quantity will be dynamically calculated or defaulted to 1.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| stopLoss                                 | Object  | [Read more](webhooks.md#signal-stop-loss)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| takeProfit                               | Object  | [Read more](webhooks.md#signal-take-profit)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| timeInForce                              | String  | <p>The time in force for your order. The supported values are <code>day</code>, <code>gtc</code>, <code>gtd</code>, <code>opg</code>, <code>cls</code>, <code>ioc</code> and <code>fok</code>.<br><br><code>day</code> - Good For Day<br><br><code>gtc</code> - Good Until Canceled<br><br><code>gtd</code> - Good Until Date<br><br><code>opg</code> - Market on Open / Limit on Open<br><br><code>cls</code> - Market on Close / Limit on Close<br><br><code>ioc</code> - Immediate or Cancel<br><br><code>fok</code> - Fill or Kill</p>                                                                                                                                                                                                                                                                                                                 |
| extendedHours                            | Boolean | Whether or not to send the order as an extended hours order. This is only applicable for stocks and the supported values are either `true` or `false`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

{% tabs %}
{% tab title="200: OK Successful webhook response." %}
```javascript
{
    "success":true,
    "id":"47462f2d-378c-4bf5-a016-1c1221aa0e62",
    "logId":"a036eff1-b7db-4f15-b5b6-f5e51995ad29",
    "payload": {
        "ticker":"NQ",
        "action":"buy",
        "sentiment": "bullish",
        "price":12663.5,
        "quantity": 1
    }
}
```
{% endtab %}

{% tab title="400: Bad Request Rejected webhook response." %}
When a webhook request is sent to TradersPost, we run it through several different validation checks. If any of these validation rules fail, the webhook will respond like the following with a status code of 400.

Here is an example invalid JSON payload.

```json
{
    "ticker": "NQ",
    "action": "bu"
}
```

Here is the response you would get for that payload.

```json
{
    "success":false,
    "logId":"bf3b4869-bf85-48cc-a1b3-8e49c77215ae",
    "messageCode":"invalid-action",
    "message":"Invalid action provided. Action must be one of: buy, sell, exit, cancel, add."
}
```

You can read more about 400 Bad Requests here.
{% endtab %}

{% tab title="404: Not Found Webhook not found." %}
```javascript
{
    "success": false,
    "messageCode": "not-found",
    "message": "Webhook not found."
}
```
{% endtab %}

{% tab title="500: Internal Server Error Something went wrong" %}

{% endtab %}
{% endtabs %}

## Rate Limiting

TradersPost is **NOT** designed to be a high frequency trading platform. While we do not currently rate limit traffic to webhooks, we may contact you and disable your webhooks and strategies if we determine that your account is sending too many requests.

## Examples

Here are some example webhook JSON payloads to demonstrate the different use cases.

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

### Cancel Open Orders

Cancel all the open orders for the given ticker.

```json
{
    "ticker": "SQ",
    "action": "cancel"
}
```

### Add to Open Position

You can add to an existing open position by using the **add** action. This will add to the existing open position regardless of if **Allow add to position** is checked in your strategy subscription settings.

```json
{
    "ticker": "SQ",
    "action": "add"
}
```

### Order Type

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
    "stopPrice" 60,
    "limitPrice": 50.50
}
```

### Trailing Stop

You can easily create trailing stop orders by sending `trailing_stop` in the `orderType` field. The following JSON will create a $1 trailing stop order for the open SQ position.

```json
{
    "ticker": "SQ",
    "action": "exit",
    "orderType": "trailing_stop",
    "price": 71,
    "trailAmount": "1"
}
```

{% hint style="info" %}
Note that if the broker you are using does not support fetching quotes, you will need to be sure to send the current price in the `price` field so that we can use that price to calculate your trailing stop price. In the above example, the starting trailing stop price would be $70. If the price moves up to $72, then the trailing stop price would update to $71.
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

### Quantity

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

### Quantity Type

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
    "price": 100,
    "quantityType": "risk_dollar_amount",
    "quantity": 100,
    "stopLoss": {
        "type": "stop",
        "stopPrice": 90
    }
}
```

The `risk_dollar_amount` quantity in this example means you want to calculate a quantity that would only allow you to lose roughly $100 when the stop loss is hit. In this example, TradersPost would calculate a quantity of 10. If you enter at $100 and get stopped out at $90 and the most you want to lose is $100, then you can only buy a quantity of 10.

### Signal Price

The signal price is optional. It is only necessary when you are using relative take profit or stop losses and the broker does not support fetching quotes to be able to perform the calculation. Here is an example where the price at the time of the signal was `$18500` and we specify that we want a `$100` take profit. So a take profit order with a limit price of `$18600` will be calculated and sent to your broker along with your market entry order.

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

### Take Profit

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

### Stop Loss

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

### Time In Force

If you want to control the order time in force from the webhook, you can optionally send a value in the `timeInForce` field. This time in force will only be used if you have **Use signal time in force for entries** or **Use signal time in force for exits** checked.

```json
{
    "ticker": "SQ",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": 50.50
    "timeInForce": "gtc"
}
```

Or if want to send the order with extended hours enabled so that the order can be filled in extended hours, you can use the `extendedHours` field to send a boolean `true` or `false` value.

```json
{
    "ticker": "SQ",
    "action": "buy",
    "orderType": "limit",
    "limitPrice": 50.50,
    "timeInForce": "gtc",
    "extendedHours" true
}
```

### Options

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

## 400 Bad Request

The JSON that gets sent to TradersPost has to be precisely accurate in order for us to accept it. It is important to pay attention all the details, all the little characters have meaning and are important. Here are the types of errors you may encounter when sending JSON to TradersPost webhooks.

**post-required** - HTTP POST method is required.

All webhook HTTP requests must be sent with a request method of POST. All other request methods will not be accepted.

**malformed-json** - Could not parse JSON payload.

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

**invalid-payload** - Invalid payload. action and ticker is required.

The minimum required fields are an action and ticker. All other fields are optional.

**invalid-action** - Invalid action provided.

Action must be one of: buy, sell, exit, cancel, add. The available actions available for webhooks are buy, sell, exit, cancel and add.

**invalid-sentiment** - Invalid sentiment provided.

Sentiment must be one of: bullish, bearish, flat. The available sentiments are bullish, bearish and flat. You can optionally exchange long for bullish and short for bearish. This is for compatibility with TradingView strategies out of the box.

**invalid-sentiment-action** - Invalid sentiment action provided.

Sentiment can only be used with action buy or sell. You can only pass a sentiment in a webhook request when using action=buy or action=sell.

For example, sending a payload with `"action": "exit"` and `"sentiment": "flat"` will produce an error since only the `"action": "exit"` is needed.

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

## Third Parties

Because TradersPost works using standard webhooks, this enables users to integrate with third party platforms that support sending alerts as webhooks.

Here are some popular platforms that enable you to build strategies and send alerts as webhooks.

* [TradingView](../learn/tradingview.md) - TradingView is a social network of 30 million traders and investors using the world's best charts and tools to spot trading opportunities across global markets.
* [TrendSpider](../learn/trend-spider.md) - TrendSpider provides technical analysis software for retail traders and investors focused on the US equity and foreign exchange markets.

## Custom Code

In addition to sending webhooks from third parties, you can send webhooks to TradersPost from custom code using programming languages like [PHP](https://php.net) or [Python](https://www.python.org). Here is an example using [PHP](https://php.net) and the [Symfony HTTP Client](https://symfony.com/doc/current/http\_client.html).

This example uses [PHP](https://www.php.net/) and the [Composer](https://getcomposer.org/) package manager. First create a new directory to work inside of.

```bash
mkdir traderspost
cd traderspost
```

Now require the `symfony/http-client` package using composer.

```
composer require symfony/http-client
```

Now you are ready to create a file named `traderspost-test.php` and paste the following code inside of the file.

```php
<?php
// traderspost-test.php

require 'vendor/autoload.php';

use Symfony\Component\HttpClient\HttpClient;

$webhookUrl = 'https://traderspost.io/trading/webhook/9d9f8620-d60d-416e-827e-0ec01ef93532/9b5b8c4264421f5515fd4fcb6571af50';

$client = HttpClient::create();

$response = $client->request('POST', $webhookUrl, [
    'json' => [
        'ticker' => 'AMD',
        'action' => 'buy',
        'price' => 85.50,
    ]
]);

echo $response->getContent();
```

Now you are ready to send the webhook to TradersPost!

```bash
php traderspost-test.php
{"success":true,"id":"cd481b19-9bb7-4845-8227-523203971d47","payload":{"ticker":"AMD","action":"buy","price":85.50}}
```

This is a simple example, but you can combine this with a service like [Polygon.io](https://polygon.io) to get live real-time market data and build your own completely custom trading strategies and TradersPost can handle the integrations with your broker.

You can read more about [custom code examples here.](../learn/custom-code-examples.md)
