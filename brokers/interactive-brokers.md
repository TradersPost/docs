---
description: >-
  Interactive Brokers is a popular stocks trading broker for international
  traders. Build automated trading strategies using TradersPost on top of your
  Interactive Brokers account.
---

# Interactive Brokers

{% hint style="warning" %}
The Interactive Brokers integration is generally available for all TradersPost customers. Please remember that this integration is in <mark style="color:orange;">**BETA**</mark> and you may experience issues that we have not discovered yet. It is recommended to test with a paper account first. If you have any issues or questions, please email us at [support@traderspost.io](mailto:support@traderspost.io)
{% endhint %}

## Contact Information

Email: [help@interactivebrokers.com](mailto:help@interactivebrokers.com)

Phone: [+1 (877) 442-2757](tel:18774422757)

## Reliability

The Interactive Brokers API is generally pretty reliable. You may occasionally receive errors from IBKR that may look like this with a message like "**Idle timeout reached**". This means we sent a request to the IBKR API and it timed out after waiting 10 seconds for a response.

<figure><img src="../.gitbook/assets/Screenshot 2023-08-21 at 5.42.06 PM.png" alt=""><figcaption></figcaption></figure>

On average, the IBKR API responds to our requests in **229 milliseconds**.

## Supported Asset Classes

<table><thead><tr><th width="363">Asset Class</th><th data-type="checkbox">Supported</th></tr></thead><tbody><tr><td>Stocks</td><td>true</td></tr><tr><td>Options</td><td>false</td></tr><tr><td>Futures</td><td>false</td></tr><tr><td>Crypto</td><td>false</td></tr><tr><td>Forex</td><td>false</td></tr></tbody></table>

## Daily Reset

The IBKR API has a daily "reset" window that occurs between 23:45 and 00:45 ET for the North America region. You can read more about the Interactive Brokers system status [here](https://www.interactivebrokers.com/en/software/systemStatus.php).

Since the Interactive Brokers API is basically unavailable during these windows and cannot be relied upon to execute automated trades, it is recommended to program your strategy to not send signals during these windows. If you send orders during these windows, it is possible that the trades will fail to execute, even with retries enabled.

## Market Data Quotes

The Interactive Brokers API does not have a 100% reliable API for retrieving market data quotes for use with automated trading. In the scenarios where we cannot retrieve a quote from IBKR, we fallback to our Polygon market data provider. We will fallback to Polygon in the following scenarios.

* If you are logged in to another IBKR session, then we will fallback to Polygon. For example, logging in to the IBKR mobile app or TWS will cause TradersPost to not be able to use your market data. IBKR market data can only be used in one active session at a time.
* If you don't have market data in IBKR for the exchange being requested.
* If the IBKR API fails when fetching a quote from it.
* If it is the first request for a quote from IBKR for that symbol during the current session. Sessions are active for 24 hours and are restarted every night due to the IBKR [Daily Reset](interactive-brokers.md#daily-reset). Subsequent requests for the same symbol in the same session will return data from IBKR and we will use that data if it exists, otherwise it will fallback to Polygon.
* If IBKR returns a quote but the data is delayed, we will fallback to Polygon.

## Paper Account

Some paper IBKR accounts have trouble connecting to TradersPost and may receive the message "This username is not associated with a paper trading account" when trying to connect with TradersPost.

You will need to follow these steps to fix your IBKR paper account:

* Login to your live client portal and go to Settings.
* Under settings go to Paper Trading Account.
* Find your paper trading username and complete a password reset for a new paper trading password.

Then you will be able to connect your IBKR paper account to TradersPost.

## TWS Precautionary Settings

Interactive Brokers by default requires order confirmations under certain conditions. For example, if the order total value is greater than $100000, the order will require a confirmation before being able to submit the order. These confirmations can slow down trade execution and can increase the likelihood that something fails. IBKR recommends turning off these precautionary settings.

You can do this by logging into TWS and going to **Global Config > Presets > Stocks (or whatever other asset class).**

You can put 0s in all fields to disable them, and then those precautionary confirmation messages won't be required when submitting orders through the IBKR API via TradersPost.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

## User Login Sessions

Interactive Brokers only allows a login username to have one session active at a time. Once you connect your IBKR account to TradersPost, we will ping the session every 1 minute to make sure our session remains active and is ready to execute automated trades if an automated trade signal comes in. If you login to another client, like the TWS application with the same username, it will steal the session from TradersPost and when our process runs every minute it will steal the session back from TWS.

{% hint style="danger" %}
If you login to another IBKR client with the same username that TradersPost uses, it is possible it can cause automated trades to fail as the session may not be active and available when we go to execute the trade. We will make an attempt to start the session and wait for the session to become active before retrying the trade, but it is possible IBKR may be delayed in starting the session and the trade won't be able to be executed.
{% endhint %}

The only workaround for this is to create a 2nd username that is dedicated for use with TradersPost. Read about [adding a user](https://www.ibkrguides.com/clientportal/uar/addingauser.htm) in the IBKR documentation to get your 2nd user setup. Make sure that the dedicated user you create in IBKR only has access to the one account you want to trade within TradersPost. TradersPost and IBKR does not support executing trades across multiple different accounts from one user login session.

## Historical Orders

The Interactive Brokers API only has the ability to view todays orders so we are not able to show historical orders within TradersPost. This means you may have issues viewing historical trades as well, since we are unable to pull order data for older order ids. You will get an error when viewing old order ids that says something like this.

> Idle timeout reached for "https://api.ibkr.com/v1/api/iserver/account/order/status/519256816".
