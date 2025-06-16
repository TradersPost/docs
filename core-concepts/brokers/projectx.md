# ProjectX

{% hint style="warning" %}
The ProjectX integration is generally available for all TradersPost customers. Please remember that this integration is in <mark style="color:orange;">**BETA**</mark> and you may experience issues that we have not discovered yet. It is recommended to test with small position size first. If you have any issues or questions, please email us at [support@traderspost.io](mailto:support@traderspost.io)
{% endhint %}

## Contact Information

Email: [info@projectx.com](mailto:info@projectx.com)

## Setup

Please follow the guide from your prop firm on how to set up API access. In all cases, you will be required to purchase API access on ProjectX. For example, TopstepX has this guide: [https://help.topstep.com/en/articles/11187768-topstepx-api-access](https://help.topstep.com/en/articles/11187768-topstepx-api-access)

You can register for a ProjectX account here: [https://dashboard.projectx.com/](https://dashboard.projectx.com/)

## Supported Asset Classes

* Futures

## Supported Prop Firms

A list of supported prop firms is available on [our Connections page](https://traderspost.io/connections).

## Known Limitations

* No market data provided by ProjectX.
* No P\&L data for positions or account provided by ProjectX.
* Account balances do not update in real-time. It only updates after you close a position.
* No bracket orders supported. This means you cannot send a take profit or stop loss with your entry order.
* Submitting a limit order with a price greater then current market price will convert the order to a market order and will show as a market order in your order history instead of a limit order.
