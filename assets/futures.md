---
description: >-
  TradersPost supports buying, selling and shorting futures contracts with
  support for over 100 tickers.
---

# Futures

{% embed url="https://www.youtube.com/watch?v=g0dB64iWTpA" %}
TradersPost Automated Futures Trading Setup
{% endembed %}

## Supported Brokers

* [TradeStation](../core-concepts/brokers/tradestation.md)
* [Tradovate](../core-concepts/brokers/broker-roadmap/tradovate.md) (coming soon)

## Supported Tickers

TradersPost currently supports trading with the following futures tickers through TradeStation.

{% hint style="info" %}
The ticker names are not always the same from TradingView to TradersPost. Because of this, it's recommended that you hard code your ticker symbol into your alerts instead of using the **\{{ticker\}}** TradingView variable. For example, Lumber with TradeStation is **LB** and on TradingView it's **LBS**. To ensure you end up in the front contract for Lumber, use the TradersPost Symbol Root LB1!
{% endhint %}

```json
{
    "ticker": "LB1!",
    "action": "buy"
}
```

[View our TradingView Watchlist with all available symbols.](https://www.tradingview.com/watchlists/109951165/)

| Description                                      | TradersPost Symbol Root | TradingView Symbol |
| ------------------------------------------------ | ----------------------- | ------------------ |
| **INDEXES**                                      |                         |                    |
| E-MINI S\&P 500                                  | ES                      | ES1!               |
| E-MINI MIDCAP 400                                | EMD                     | EMD1!              |
| E-MINI NASDAQ 100                                | NQ                      | NQ1!               |
| MINI RUSSELL 2000 (CME)                          | RTY                     | RTY1!              |
| MINI DOW JONES ($5)                              | YM                      | YM1!               |
| MICRO ES                                         | MES                     | MES1!              |
| MICRO NQ                                         | MNQ                     | MNQ1!              |
| MICRO RUSSELL                                    | M2K                     | M2K1!              |
| MICRO YM                                         | MYM                     | MYM1!              |
| NIKKEI ($ BASED) (CME)                           | NK                      | NKD1!              |
| VIX                                              | VX                      | VX1!               |
| MINI VOLATILITY INDEX                            | VXM                     |                    |
| ICE Bitcoin                                      | BTM                     | BTM1!              |
| CME BITCOIN FUTURES                              | BTC                     | BTC1!              |
| CME MICRO BITCOIN FUTURES                        | MBT                     | MBT1!              |
| CME ETHEREUM FUTURES                             | ETH                     | ETH1!              |
| CME MICRO ETHEREUM FUTURES                       | MET                     | MET1!              |
| **EUREX**                                        |                         |                    |
| DAX                                              | FDAX                    | FDAX1!             |
| MINI-DAX                                         | FDXM                    | FDXM1!             |
| MICRO-DAX                                        | FDXS                    | FDXS1!             |
| DJ STOXX 50 INDEX                                | FESX                    | FESX1!             |
| MICRO-DJ EURO STOXX 50 INDEX FUTURES             | FSXE                    | FSXE1!             |
| DJ STOXX 600 BANKS                               | FSTB                    | FSTB1!             |
| DJ STOXX 600 INDST G\&S                          | FSTG                    | FSTG1!             |
| EURO-SCHATZ                                      | FGBS                    | FGBS1!             |
| EURO-BOBL                                        | FGBM                    | FGBM1!             |
| EURO-BUND                                        | FGBL                    | FGBL1!             |
| EURO-OAT                                         | FOAT                    | FOAT1!             |
| EURO-BUXL                                        | FGBX                    | FGBX1!             |
| DJ STOXX 600 UTILITY                             | FSTU                    | FSTU1!             |
| **EURONEXT LIFFE**                               |                         |                    |
| FTSE 100 INDEX FUTURES                           | LZ                      | Z1!                |
| THREE MONTH EURO (EURIBOR) INTEREST RATE FUTURES | LT2                     | FEU31!             |
| LONG GILT FUTURES                                | LJ                      | R1!                |
| MEDIUM GILT FUTURES                              | H                       | H1!                |
| SHORT GILT FUTURES                               | G                       | G1!                |
| LONDON COCOA FUTURES                             | CC3                     | C1!                |
| LONDON ROBUSTA COFFEE FUTURES                    | RC                      | RC1!               |
| **CURRENCIES (CME)**                             |                         |                    |
| AUSTRALIAN DLR.                                  | AD                      | 6A1!               |
| BRITISH POUND                                    | BP                      | 6B1!               |
| CANADIAN DLR.                                    | CD                      | 6C1!               |
| EURO CURRENCY                                    | EC                      | 6E1!               |
| JAPANESE YEN                                     | JY                      | 6J1!               |
| MEXICAN PESO                                     | MP1                     | 6M1!               |
| NEW ZEALAND DLR.                                 | NE1                     | 6N1!               |
| SWISS FRANC                                      | SF                      | 6S1!               |
| DOLLAR INDEX (ICE)                               | DX                      | DX1!               |
| MINI EURO                                        | E7                      | E71!               |
| MINI YEN                                         | J7                      | J71!               |
| E-MICRO AUD/USD                                  | M6A                     | M6A1!              |
| E-MICRO GBP/USD                                  | M6B                     | M6B1!              |
| E-MICRO EUR/USD                                  | M6E                     | M6E1!              |
| **INTEREST RATES (CBOT)**                        |                         |                    |
| 30-YR T-BOND                                     | US                      | ZB1!               |
| Ultra 30-YR T-BOND                               | UB                      | UB1!               |
| 20-YR T-BOND                                     | TWE                     | TWE1!              |
| 10-YR T-NOTE                                     | TY                      | ZN1!               |
| Ultra 10-YR NOTE                                 | TEN                     | TN1!               |
| 5-YR T-NOTE                                      | FV                      | ZF1!               |
| 2-YR T-NOTE                                      | TU                      | ZT1!               |
| EURODOLLAR (CME)                                 | ED                      | GE1!               |
| ONE-MONTH SOFR                                   | SR1                     | SR11!              |
| THREE-MONTH SOFR                                 | SR3                     | SR31!              |
| MICRO 2-YEAR YIELD FUTURES                       | 2YY                     | 2YY1!              |
| MICRO 5-YEAR YIELD FUTURES                       | 5YY                     | 5YY1!              |
| MICRO 10-YEAR YIELD FUTURES                      | 10Y                     | 10Y1!              |
| MICRO 30-YEAR YIELD FUTURES                      | 30Y                     | 30Y1!              |
| **METALS**                                       |                         |                    |
| GOLD (COMEX)                                     | GC                      | GC1!               |
| SILVER (COMEX)                                   | SI                      | SI1!               |
| COPPER (COMEX)                                   | HG                      | HG1!               |
| PALLADIUM (NYMEX)                                | PA                      | PA1!               |
| PLATINUM (NYMEX)                                 | PL                      | PL1!               |
| ALUMINUM (COMEX)                                 | ALI                     | ALI1!              |
| MICRO GOLD (COMEX)                               | MGC                     | MGC1!              |
| E-MICRO SILVER (COMEX)                           | SIL                     | SIL1!              |
| MICRO COPPER (COMEX)                             | MHG                     | MHG1!              |
| **ENERGIES**                                     |                         |                    |
| CRUDE OIL (NYMEX)                                | CL                      | CL1!               |
| NATURAL GAS (NYMEX)                              | NG                      | NG1!               |
| HEATING OIL (NYMEX)                              | HO                      | HO1!               |
| RBOB GASOLINE (NYMEX)                            | RB                      | RB1!               |
| BRENT CRUDE OIL (ICE)                            | BRN                     | BRN1!              |
| LOW SULPHUR GASOIL (ICE)                         | ULS                     | GAS1!              |
| E-MINY CRUDE OIL (NYMEX)                         | QM                      | QM1!               |
| E-MINY NATURAL GAS (NYMEX)                       | QN                      | QG1!               |
| E-MINY HEATING OIL (NYMEX)                       | QH                      | QH1!               |
| E-MINY RBOB GASOLINE (NYMEX)                     | QU                      | QU1!               |
| MICRO CRUDE OIL (NYMEX)                          | MCL                     | MCL1!              |
| MICRO HEATING OIL                                | MHO                     | MHO1!              |
| MICRO RBOB GASOLINE                              | MRB                     | MRB1!              |
| **AGRICULTURE (CBOT)**                           |                         |                    |
| WHEAT                                            | W                       | ZW1!               |
| HARD RD WINTER WHEAT                             | KW                      | KE1!               |
| CORN                                             | C                       | ZC1!               |
| OATS                                             | O                       | ZO1!               |
| SOYBEANS                                         | S                       | ZO1!               |
| SOYBEAN OIL                                      | BO                      | ZL1!               |
| SOYBEAN MEAL                                     | SM                      | ZM1!               |
| ROUGH RICE                                       | RR                      | ZR1!               |
| MILK (CME)                                       | DA                      | DC1!               |
| BUTTER (CME)                                     | CB                      | CB1!               |
| MINI WHEAT                                       | YW                      | XW1!               |
| MINI CORN                                        | YC                      | XC1!               |
| MINI SOYBEANS                                    | YK                      | XK1!               |
| **MEATS (CME)**                                  |                         |                    |
| LEAN HOGS                                        | LH                      | HE1!               |
| LIVE CATTLE                                      | LC                      | LE1!               |
| FEEDER CATTLE                                    | FC                      | GF1!               |
| **SOFTS (ICE)**                                  |                         |                    |
| COFFEE                                           | KC                      | KC1!               |
| COTTON                                           | CT                      | CT1!               |
| FROZEN OJ                                        | OJ                      | OJ1!               |
| COCOA                                            | CC                      | CC1!               |
| SUGAR #11                                        | SB                      | SB1!               |
| **OTHER**                                        |                         |                    |
| LUMBER (CME)                                     | LB                      | LBR1!              |
| One-Month SOFR Futures                           | SR1                     | SR1!               |
| Three-Month SOFR Futures                         | SR3                     | SR3!               |

## Symbol Format

TradersPost standardizes the futures symbol format to have a 4 digit year. We convert this symbol format back and fourth when communicating with each broker so you don't have to worry about the differences between brokers.

| Symbol  | Type                         |
| ------- | ---------------------------- |
| NQZ2021 | 4 digit year (TradersPost)   |
| NQ1!    | TradingView current contract |
| NQ2!    | TradingView next contract    |
| NQ\*0   | TrendSpider current contract |
| NQ\*1   | TrendSpider next contract    |

## Signals

It's easy to send signals to TradersPost using [Webhooks](../core-concepts/webhooks.md) from platforms like [TradingView](../learn/tradingview.md) or [TrendSpider](../learn/trend-spider.md). You just need to send JSON like the following to the webhook URL you create within TradersPost.

### Enter Bullish

The **buy** action is a bullish signal. When TradersPost receives a buy signal, we will **Buy To Cover** any bearish (short) position for the ticker and **Buy To Open** a bullish (long).

```json
{
    "ticker": "NQH2022",
    "action": "buy"
}
```

### Exit Bullish

The **exit** action will exit any open position. So for example if you have a long shares position open, then TradersPost will **Sell To Close** those long contracts.

```json
{
    "ticker": "NQH2022",
    "action": "exit"
}
```

### Enter Bearish

The **sell** action is a bearish signal. When TradersPost receives a sell signal, we will **Sell To Close** any bullish (long) position for the ticker and **Sell To Open** a bearish (short) position.

```json
{
    "ticker": "NQH2022",
    "action": "sell"
}
```

### Exit Bearish

The **exit** action will exit any open position. So for example if you have a short contracts position open, then TradersPost will **Buy to Cover** those short contracts.

```json
{
    "ticker": "NQH2022",
    "action": "exit"
}
```

### Full Signal Example

You can optionally include a **price** and **quantity** in the signal that can then be used in the calculated orders that we send to your broker. Here is a full example signal.

```json
{
    "ticker": "NQH2022",
    "action": "buy",
    "price": 1420.50,
    "quantity": 2
}
```

If you configure your strategy subscription to use limit orders and to use the signal quantity, then you will get a **Buy Limit** order for 2 contracts at a price of **$1420.50**.

## Market Orders

{% hint style="danger" %}
While futures trading generally supports market orders, under certain conditions market orders may be <mark style="color:red;">**REJECTED**</mark> by your broker or exchange. For example, during major news announcements like unemployment or inflation numbers, the exchange can go into reserve and during this time market orders are not accepted.
{% endhint %}

During these market conditions, you may receive rejected orders with a reject reason of the following:

![Order type not permitted while the market is reserved](<../.gitbook/assets/Screen Shot 2022-07-13 at 9.17.30 AM (1).png>)

Whenever trading futures and you are facing upcoming volatile market conditions, you have two options:

1. Don't hold positions over upcoming major news announcements (CPI, FOMC announcements, etc)
2. Watch your positions and be ready to take manual action with limit orders if your market orders are rejected.

To keep track of the different news events that may cause the market to move in one direction or another you can use the following calendars.

* [https://www.federalreserve.gov/newsevents/calendar.htm](https://www.federalreserve.gov/newsevents/calendar.htm)
* [https://www.marketwatch.com/economy-politics/calendar](https://www.marketwatch.com/economy-politics/calendar)

## Contract Rollover

{% hint style="danger" %}
You are responsible for ensuring futures contract positions are exited before expiration or are rolled over manually. TradersPost does not automatically do anything special for futures contract positions based on expiration date.
{% endhint %}

The TradersPost continuous contract symbols like **NQ1!** rollover on the exact expiration date. We do not rollover automatically early or based on volume.

This means if your strategy gets in a trade before the current contract expires, TradersPost will NOT automatically exit the position for you.\
\
If you want to trade a specific contract, then you can send **NQH2023** or **NQM2023** instead of **NQ1!** for example. Here is an example JSON.

```json
{
    "ticker": "NQH2023",
    "action": "buy"
}
```
