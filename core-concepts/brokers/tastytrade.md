# tastytrade

## Contact Information

Email: [support@tastytrade.com](mailto:support@tastytrade.com)

Phone: [+1 (888) 247-1963](tel:18882471963)

## Supported Asset Classes

* Stocks
* Options
* Futures
* Crypto

## Market Data

tastytrade does not provide access to market data through their API, so the we use market data from [Polygon](https://polygon.io/) at no additional charge to you for stocks and crypto only.

{% hint style="warning" %}
The futures asset class within tastytrade does not support market data, so you cannot fetch quotes for futures symbols or view the P\&L for futures positions.
{% endhint %}

## Fractional Shares

tastytrade supports fractional shares for both **crypto** and **stocks**, but there are important limitations—especially when it comes to **automated trading** of stocks.

### **Stocks**

While tastytrade technically allows holding fractional stock shares, **fractional shares are not fully supported for automated trading**. This functionality is primarily intended to handle small fractional amounts received from **dividends or account adjustments**, not for executing full or partial trades.

For example:

* If you own **4.99 shares** of a stock:
  * You **cannot** submit a single order to sell all 4.99 shares.
  * You must **first sell the 0.99 fractional shares**, then submit a separate order to sell the remaining 4 whole shares.

Because of this limitation, we **strongly recommend disabling fractional shares** when using tastytrade with TradersPost.

### **Crypto**

Fractional trading is **fully supported** for cryptocurrencies on tastytrade. You can buy and sell fractional crypto positions in a single order without any special handling.
