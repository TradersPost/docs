---
description: >-
  Interactive Brokers is a popular broker for international traders and they
  support stocks and futures. Build automated trading strategies using
  TradersPost on top of your Interactive Brokers account.
---

# Interactive Brokers

{% hint style="info" %}
COMING SOON. Join the [wait list](https://traderspost.io/broker/ibkr) to be notified once Interactive Brokers is available.
{% endhint %}

## Contact Information

Email: [help@interactivebrokers.com](mailto:help@interactivebrokers.com)

Phone: [+1 (877) 442-2757](tel:18774422757)

## Reliability

The Interactive Brokers API is unfortunately quite unreliable relative to other broker integrations. This means that trade execution can fail more often when using Interactive Brokers due to Interactive Brokers server errors and request timeouts. These issues have been reported to the IBKR support team but they have not given any indication as to if they plan to resolve these issues. Errors from IBKR may look like this with a message like "**Idle timeout reached**". This means we sent a request to the IBKR API and it timed out after waiting 10 seconds for a response.

<figure><img src="../../.gitbook/assets/Screenshot 2023-08-21 at 5.42.06 PM.png" alt=""><figcaption></figcaption></figure>

On average, the IBKR API responds to our requests in **252 milliseconds**. This is around 5x slower than [Alpaca](../alpaca.md) and [Robinhood](../robinhood.md) for example.

## Supported Asset Classes

<table><thead><tr><th width="363">Asset Class</th><th data-type="checkbox">Supported</th></tr></thead><tbody><tr><td>Stocks</td><td>true</td></tr><tr><td>Options</td><td>false</td></tr><tr><td>Futures</td><td>false</td></tr><tr><td>Crypto</td><td>false</td></tr><tr><td>Forex</td><td>false</td></tr></tbody></table>

## Daily Reset

The IBKR API has a daily "reset" window that occurs between 23:45 and 00:45 ET for the North America region. You can read more about the Interactive Brokers system status [here](https://www.interactivebrokers.com/en/software/systemStatus.php).

Since the Interactive Brokers API is basically unavailable during these windows and cannot be relied upon to execute automated trades, it is recommended to program your strategy to not send signals during these windows. If you send orders during these windows, it is possible that the trades will fail to execute, even with retries enabled.

## Quotes

The IBKR API does not have a reliable way to retrieve quotes for symbols, so prices are always required to be sent in the webhook signal when you want to submit limit orders. We are unable to fetch quotes to use the midpoint price as the limit price for limit orders. See example below.

```json5
{
    "ticker": "SPY",
    "action": "buy",
    "price": 447.31
}
```

If the `price` field is omitted and you have a feature enabled in your strategy subscription settings that requires a price, like limit orders, then the trade will be rejected.

## Paper Account

Some paper IBKR accounts have trouble connecting to TradersPost and may receive the message "This username is not associated with a paper trading account" when trying to connect with TradersPost.

You will need to follow these steps to fix your IBKR paper account:

* Login to your live client portal and go to Settings.
* Under settings go to Paper Trading Account.
* Find your paper trading username and complete a password reset for a new paper trading password.

Then you will be able to connect your IBKR paper account to TradersPost.

## TWS Precautionary Settings

Interactive Brokers by default requires order confirmations under certain conditions. For example, if the order total value is greater than $100000, the order will require a confirmation before being able to submit the order. These confirmations can slow down trade execution and can increase the likelihood that something fails. IBKR recommends turning off these precautionary settings.

You can do this by logging into TWS and going to **Global Config > Presets > Futures (or whatever other asset class).**

You can put 0s in all fields to disable them, and then those precautionary confirmation messages won't be required when submitting orders through the IBKR API via TradersPost.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

## User Sessions

Interactive Brokers only allows a login username to have one session active at a time. Once you connect your IBKR account to TradersPost, we will ping the session every 1 minute to make sure our session remains active and is ready to execute automated trades if an automated trade signal comes in. If you login to another client, like the TWS application with the same username, it will steal the session from TradersPost and when our process runs every minute it will steal the session back from TWS.

{% hint style="danger" %}
If you login to another IBKR client with the same username that TradersPost uses, it is possible it can cause automated trades to fail as the session may not be active and available when we go to execute the trade. We will make an attempt to start the session and wait for the session to become active before retrying the trade, but it is possible IBKR may be delayed in starting the session and the trade won't be able to be executed.
{% endhint %}

The only workaround for this is to create a 2nd username that is dedicated for use with TradersPost. Read about [adding a user](https://www.ibkrguides.com/clientportal/uar/addingauser.htm) in the IBKR documentation to get your 2nd user setup.

