---
description: >-
  Every Friday, we dive into your questions and feedback to discuss the latest
  updates and offer guidance on developing automated trading algorithmic
  workflows.
---

# Office Hours

Subscribe to [Office Hours on our YouTube Channel](https://www.youtube.com/@TradersPost) to be notified when we go live.

#### Have a question?

* Post a comment on our blog at [traderspost.io/blog](https://traderspost.io/blog)
* Post as a comment on one of our [YouTube videos](https://www.youtube.com/@TradersPost)
* Post on Twitter or Discord using the #TPOfficeHours hashtag
* Send an email to support

***

## Can I automate FRACTIONAL SHARES trading on Interactive Brokers?

{% embed url="https://www.youtube.com/watch?index=1&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=5rTLVhR6O0w" %}

**Interactive Brokers:** Supports fractional shares on their platform but not via the API used for automation.&#x20;

**Alternatives:** Platforms like Alpaca and Robinhood support automated fractional trading through TradersPost.

**Crypto:** Most crypto exchanges inherently support fractional trading.

**Demand:** Low demand for automating fractional trades; whole share trading generally suffices for most algo traders.

**High-Value Stocks:** Fractional shares useful for high-priced stocks like Berkshire Hathaway.

***

## Resolving Broker Issues: When to Contact TradersPost vs. Your Broker

{% embed url="https://www.youtube.com/watch?index=2&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&v=t87UyLPttO4" %}

**General Policy:** TradersPost does not contact brokers on behalf of users for individual account issues. Users need to manage their own broker accounts.

**Error Investigation:** If the issue might be caused by TradersPost, they will investigate. If the error clearly comes from the broker, users will be directed to contact their broker.

**Broker Relationships:** TradersPost has close relationships with brokers and will follow up on issues affecting multiple users.

**Documentation:** Most common issues are covered in TradersPost documentation. Use Command/Control + K to search the documentation.

**AI Assistance:** The documentation is AI-powered to help answer user queries. If new issues arise, they are added to the documentation for future reference.

***

### How to Execute Only the First Buy Signal in TradersPost

{% embed url="https://www.youtube.com/watch?index=3&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&t=4s&v=wuNqb7R7UKk" %}

**Default Behavior:** By default, TradersPost executes only the first Buy trade and rejects subsequent Buy signals if the position is already open.

**Settings Check:** Ensure the “Allow Add to Position” setting is disabled.

**Steps to Disable:**

1. Go to your subscriptions or strategy settings.
2. Find “Subscription Defaults.”
3. Scroll down to “Allow Add to Position.”
4. Ensure it is set to “No.”\


Disabling this setting ensures only the first Buy trade is executed for a given ticker, and any additional Buy signals are rejected.

***

### TradersPost Affiliate Payouts: When to Expect Your Earnings

{% embed url="https://www.youtube.com/watch?index=4&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=XMDB58_uFps" %}

**Payout Frequency:** Payouts are processed monthly, typically at the end of each month.

**Minimum Payout:** Currently set at $100, though this is flexible and may change based on requests.

No Specific Payout Link: Payouts are managed automatically without needing a specific link.\


We’re refining the payout schedule to ensure consistency. For now, expect monthly payouts with a flexible minimum amount.

***

### Unlocking User Management on TradersPost: Pro and Premium Features Explained

{% embed url="https://www.youtube.com/watch?index=5&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=45UOjzSxan8" %}

**Not Monitored:** TradersPost doesn’t monitor for accounts connected under different names.

**Advisability:** Generally not advisable due to broker terms of service.

**Broker Requirements:** Typically, brokers expect the account owner to be the user. Confirm with your broker if you need to connect someone else’s account.

**Liability Concerns:** Connecting to an account not under your name can create liability and fiduciary responsibility issues.

#### Alternative Solution: User Accounts

**User Management:** Available on Pro and Premium plans.&#x20;

**Temporary Access:** Grant temporary access without sharing passwords.&#x20;

**User Accounts:**&#x20;

1. Create a user account for someone else to manage settings.
2. Revoke access anytime without changing your password.

**Pro and Premium Plans:** Necessary to use this feature.

**Interface:** Easy to switch and manage user accounts within the platform.

***

### Do You Recommend Trading to Others?

{% embed url="https://www.youtube.com/watch?index=6&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&t=30s&v=JTOtENO5qBY" %}

**General Recommendation:** Active trading is not recommended for most people. Passive investing is often more beneficial.

**Passive Investing:** Many people prefer passive strategies, such as dollar-cost averaging into low-cost ETFs or mutual funds.

**Active Trading:**

* Personal Enjoyment: If you love understanding markets, researching companies, and building strategies, active trading can be fulfilling.
* Educational Value: Trading teaches valuable lessons about risk management, personal psychology, and market dynamics.

**Risk and Performance:**

* Potential Underperformance: Many traders underperform compared to the market.
* Diversification Strategy: Consider putting most of your funds into passive investments and use a small portion for active trading to compare performance.

**Learning from Trading:**

* Self-Discovery: Trading helps you learn about your decision-making processes and resilience.
* Controlled Environment: Trading, like stand-up comedy, provides a controlled environment to learn from failure.

Trading can be a valuable learning experience, but be aware of the high risk and likelihood of underperformance. For most, passive investing is the safer, more reliable choice.

***

### Roth IRA and Futures: What Are Your Options?

{% embed url="https://www.youtube.com/watch?index=7&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=6-qWieNoh2Q" %}

**General Rule:** Roth IRAs in the U.S. do not support margin accounts, so direct futures trading is not allowed.

**Restrictions:**

* No margin accounts
* No short selling

**Alternative Options:**

* Use levered Futures ETFs or ETPs for exposure.
* Examples: Short the NASDAQ with SQQQ.

**Broker Requirements:**

* Ensure your broker supports these ETFs/ETPs.
* Check for associated expense ratios.

**Compatibility with** TradersPost**:** If your broker supports the ETFs/ETPs, TradersPost can manage the trades.

**Example Strategy:** TQQQ and SQQQ strategies in Roth IRAs are possible and have been implemented successfully.

For specific setups, confirm with your broker and then integrate with TradersPost as needed.

***

### Using Brokers in Beta: What You Need to Know

{% embed url="https://www.youtube.com/watch?index=8&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&t=5s&v=B-leFMBQtHA" %}

**Caution Advised:** Treat beta brokers with caution. Use paper trading initially to ensure reliability.

**Testing:** Rigorous testing is performed, but unexpected scenarios can arise.

**Beta Status:**

* Indicates a trial period.
* Use it to confirm that your trading activities work as expected.

**Transition from Beta:** Once sufficient successful trades are observed and no issues are detected, the broker will move out of beta.

**Potential Reversion:** It’s unlikely for a broker to move back into beta once it has transitioned out, as most issues are resolved before this point.

**Recommendation:** Start with paper trading for any broker in beta and proceed with real capital only after confirming stability and reliability.

***

### Mastering Multiple Trading Styles: Should You Diversify?

{% embed url="https://www.youtube.com/watch?index=10&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=SuwSpAeWN3Q" %}

**Start Simple:** Begin with one trading strategy, preferably in stocks. Focus on consistency and understanding the process.

**Avoid Complexity Early On:** Avoid derivatives and leverage products initially to reduce risk.

**Building a System:** Developing a single, well-understood system takes time and effort.

#### **Expanding Over Time**

**Market Regimes:** Different strategies suit different market conditions (e.g., high volatility vs. low volatility).

**Advanced Instruments:** Use options, futures, and other instruments to diversify and hedge.

**Portfolio of Strategies:** Over time, consider multiple strategies to capture various market opportunities.

#### Personal Preference

**Specialists:** Focus deeply on one style or market aspect, like non-farm payroll trading.

**Generalists:** Enjoy learning and applying multiple strategies across different markets.

#### Self-Discovery

**Know Yourself:** Determine if you thrive on depth (specialist) or variety (generalist).

**Test and Learn:** Experiment with different styles to see what fits your personality and goals.



Start with one simple strategy, then expand if desired. Your personal inclination—whether as a specialist or generalist—will guide your path in trading.

***

### Implementing Daily Profit and Loss Functions in TradersPost

{% embed url="https://www.youtube.com/watch?index=11&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=9WZL5EEDupE" %}

#### Daily Profit and Loss (P\&L) Function

**User Request**: Frequent inquiries about adding a daily P\&L function.

**Technical Challenges**:

* Brokers don’t provide direct support for P\&L calculation across all positions.
* Requires downloading all orders from users’ accounts to accurately determine P\&L.
* Uses the "Last In, Last Out" approach for pairing trades.

**Current Status**: Portfolio analytics (e.g., Sharpe ratio, max drawdown) are available, and work is ongoing to integrate detailed P\&L tracking.

#### **Managing Unexpected Open Positions**

**Race Conditions**: Situations where simultaneous signals lead to unexpected open positions.

**Fail-safes**:

* **TradingView Alerts**: Regular alerts to close any unexpected open positions.
* **Broker Level Safeguards**: Setting up stop-loss or conditional orders directly with the broker.

**Potential TradersPost Feature**:

* A rule to close all open positions at the start of the trading day if a clean slate is expected.
* Not currently available but could be developed based on user demand.

**Monitoring**: Emphasized the need for regular account monitoring, even with automated trading, to handle unexpected scenarios effectively.

While TradersPost is working on adding more robust P\&L tracking, users should implement their own safeguards and closely monitor their accounts to manage unexpected trades.

***

### Avoiding Race Conditions in Automated Trading

{% embed url="https://www.youtube.com/watch?index=12&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=OrZAXEf8rtQ" %}

**Recommended Buffer Time**: Allocate 10 to 15 seconds between sending trade signals to ensure all processes (order execution, broker response) complete successfully.

**Simultaneous Orders**:

* Attach take-profit and stop-loss orders with the entry order to ensure they are executed together.
* Avoid sending multiple buy/sell orders in quick succession to prevent execution errors.

**Trade on Higher Time Frames**: Consider using longer time frames (e.g., hourly charts) to reduce the impact of short-term market noise and minimize trade costs.

**Risk of Short Time Frames**:

* **High Volatility**: Short time frames can result in erratic price movements and increased risk.
* **Increased Costs**: More frequent trades lead to higher commission costs.
* **Noise vs. Signal**: Longer time frames provide clearer market trends, reducing the influence of random price fluctuations.

**Best Practices for Automated Trading**:

* **Regular Monitoring**: Even with automated systems, monitor your accounts regularly to handle unexpected scenarios.
* **Broker-Level Safeguards**: Set up stop-loss and conditional orders directly with your broker for additional safety.
* **Develop a Consistent System**: Start with a single, well-understood strategy and expand gradually.

**Skill vs. Luck in Trading**:

* **Skill Development**: Focus on developing and rigorously testing trading strategies over long periods.
* **Books and Learning**: Consider reading "Thinking in Bets" by Annie Duke to understand the difference between skill and luck in trading.
* **Consistent Performance**: Aim for consistent performance over years to distinguish skill from lucky trades.

Allocate sufficient buffer time between signals, focus on higher time frames, regularly monitor your trades, and continuously develop and test your trading strategies to ensure long-term success.

***

### Timing Trades in Pine Script: Closing and Reopening Trades

{% embed url="https://www.youtube.com/watch?index=14&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=HLOabAIOPY8" %}

**Objective**: Close open trades at 4:59 PM and reopen them at 6:01 PM.

**Key Points**:

* **Time-Based Signals**: Pine Script can generate trade signals based on specific times.
* **Execution Reliability**: Ensure signals are sent with enough lead time for reliable execution.

**Methods**:

1. **Time Variable**:
   * If using TradingView, use the time variable in Pine Script to detect specific times.
   * Example: `if (hour == 16 and minute == 59) close_trade()`
2. **Intraday Bars**:
   * Count intraday bars to determine the number of bars remaining.

```clike
// Will return an array close values from the 1-min timeframe.
count = request.security_lower_tf(syminfo.tickerid, '1', close)

// If the script is running on the 15-min timeframe, then when the array size is 10, we are 5 bars away from the bar closing.
if count.size() == 10
    strategy.close_all('End of Session', alert_message = close_trade_message)
```

**Testing**:

* **Thorough Testing**: Backtest the script to ensure trades close and open as intended.
* **Lead Time**: Consider potential delays and ensure signals are sent with adequate lead time.
* **No Trades:** If there is no activity on a particular bar, then events may not fire on that bar, even if the condition would be true.

It is possible to close and reopen trades at specific times using Pine Script. Choose the method that best fits your strategy and test thoroughly to ensure reliable execution.

***

### Using AI to Improve Automated Trading

{% embed url="https://www.youtube.com/watch?index=15&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=YosYsDM_6Os" %}

1. **Understanding AI in Trading**:
   * AI can assist in idea generation, strategy development, and decision-making processes.
   * Machine learning can help create and refine profitable strategies by analyzing large datasets and identifying patterns.
2. **AI Applications**:
   * **Thesis Development**: Use AI to clarify market hypotheses and develop entry and exit rules.
   * **Code Generation**: AI can help write and debug code in Pine Script for TradingView, although it requires iterative testing and refinement.
   * **Risk Management**: AI can act as an "AI Oracle" to evaluate the probability of success for trade signals using external data.
3. **Practical Use Cases**:
   * **Reasoning and Validation**: AI can help reason through strategies, identify potential pitfalls, and ensure comprehensive analysis.
   * **Automated Assistance**: Tools like ChatGPT can assist with articulating ideas, generating documentation, and creating prompts for execution.
   * **Creative Exploration**: AI enables creative exploration of new trading strategies without deep coding knowledge, making it accessible to more traders.
4. **Challenges and Limitations**:
   * **Prompt Engineering**: Success with AI requires clear, detailed prompts and iterative feedback.
   * **Human Oversight**: Continuous monitoring and validation by humans are essential to manage and correct AI outputs.
   * **Skill vs. Luck**: Distinguishing between skill and luck in AI-generated strategies is crucial for long-term success.
5. **Integration with Trading Platforms**:
   * **Traders Post**: AI can enhance platforms like Traders Post by automating strategy evaluation and execution.
   * **Future Potential**: While full AI integration in trading is still evolving, the potential for AI to streamline and improve trading processes is significant.

AI offers powerful tools for developing and refining trading strategies, assisting with market analysis, and managing trades. However, human oversight and iterative testing remain crucial for successful implementation. Use AI to enhance reasoning, validate ideas, and automate processes while being mindful of its limitations and the need for continuous refinement.

***

### Trading ETFs vs Single Stocks: Which is Better?

{% embed url="https://www.youtube.com/watch?index=16&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=cqJmH2FogTE" %}

**Risk Reduction**:

* **Diversification**: ETFs spread risk across multiple companies in a sector, reducing the impact of poor performance by any single stock.
* **Example**: Sector ETFs like XLE (Energy), XLF (Finance), and XLK (Technology) capture the overall performance of their respective sectors.

**Consistent Performance**:

* **Broad Exposure**: ETFs provide exposure to all winners in a sector while mitigating the damage from losers.
* **Stable Returns**: Less volatility compared to single stocks, leading to more stable returns over time.

**Passive Investing Flows**:

* **Regular Inflows**: ETFs benefit from consistent inflows from passive investment strategies like 401(k) contributions, which can drive prices upward.
* **Long-Only Bias**: These regular investments create a long-term upward bias in ETF prices.

**ETFs vs. Penny Stocks**:

* **Lower Risk**: ETFs offer a safer investment compared to the high risk associated with penny stocks or junior miners.
* **Predictable Returns**: While ETFs may offer lower upside potential than individual penny stocks, they provide more predictable and stable returns.

Trading ETFs is a prudent strategy for those looking to invest in sectors while minimizing risk and volatility. ETFs offer broad exposure, consistent performance, and benefit from passive investing flows, making them a suitable choice for most investors over speculative penny stocks.

***

### How to Trade SPX Futures with Continuous Contracts on TradeStation

{% embed url="https://www.youtube.com/watch?index=17&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=46xn4pZ722g" %}

Does TradeStation offer a fixed ticker for SPX futures that doesn't require changing based on contract expiration?

**Use Continuous Contracts**:

* **ES1!**: This ticker represents the front contract for S\&P 500 futures (e-minis or micro minis). It automatically rolls over to the next front-month contract upon expiration.
* **ES2!**: This ticker represents the second front contract, automatically updating to the subsequent contract following the front month.

**Benefits**:

* **No Manual Updates**: By using ES1!, you ensure that you're always trading the current front contract without needing to manually update the ticker.
* **Seamless Transition**: The continuous contract symbols handle rollovers automatically, maintaining your trading positions smoothly.

For continuous trading of S\&P 500 futures on TradeStation without the hassle of updating for contract expirations, use the ES1! ticker. It ensures you're always in the front contract, simplifying your trading process.

***

### Higher Time Frames vs Lower Time Frames in Trading Strategies

{% embed url="https://www.youtube.com/watch?index=18&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=5ufGmMTNhUM" %}

**Market Noise Reduction**:

* **Lower Time Frames**: Intraday strategies (e.g., 5-minute charts) experience significant market noise, random fluctuations, and short-term volatility.
* **Higher Time Frames**: Daily or hourly charts capture broader market movements and reduce the impact of short-term noise.

**Volatility and Stability**:

* **Consistency**: Higher time frames offer more stable data points, reflecting overall market trends rather than minute-to-minute fluctuations.
* **Seasonal and Regime Changes**: Strategies on higher time frames are less likely to be disrupted by sudden market regime changes or seasonal volatility.

**Data and Backtesting**:

* **Longer Data Periods**: Higher time frames allow for backtesting over longer periods, providing more reliable performance data.
* **TradingView Limitations**: Intraday strategies may be limited by the amount of historical data available on platforms like TradingView.

**Trade Frequency and Risk Management**:

* **Fewer Trades**: Higher time frames require fewer trades, reducing transaction costs and exposure to market risk.
* **Risk Per Trade**: While higher time frames might require larger stop losses, the overall risk is mitigated by fewer trades and less frequent market exposure.

**Market Participants and Volume**:

* **Institutional Influence**: Higher time frames align more with institutional trading patterns, providing a more stable trading environment.
* **Volume Weight**: Significant volume is needed to move prices on higher time frames, making them less susceptible to erratic movements.

**Transaction Costs**:

* **Commission Costs**: Fewer trades on higher time frames lead to lower overall commission costs, preserving more of your profits.
* **Efficiency**: Capturing trends on higher time frames can be more efficient, reducing the need for multiple intraday trades.

**Strategy Alignment**:

* **Fundamental Data**: Higher time frames are more appropriate for strategies based on fundamental data, which influences markets over longer periods.
* **Trend Following**: Strategies that follow market trends benefit from the clearer signals provided by higher time frames.

Strategies on higher time frames often perform better due to reduced market noise, greater stability, longer data periods for backtesting, lower transaction costs, and alignment with institutional trading patterns. Traders should consider these factors and the overall efficiency of their strategies when choosing time frames for trading.

***

### Updating TradingView Alerts: Avoid Common Mistakes

{% embed url="https://www.youtube.com/watch?index=19&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=31R7DDOup-w" %}

**Alert System Behavior**: When you create alerts on TradingView, it copies your script and conditions to run on its server.

**Impact of Strategy Changes**:

* **No Automatic Update**: Changes made to your indicator or strategy do not automatically update existing alerts.
* **Manual Update Required**: You need to delete the old alerts and create new ones to reflect the changes.

#### **Alternative Solution**

**Switch Alert Source**:

* Open your existing alert in TradingView.
* In the dropdown for the alert source, you will see two versions of your script.
* The first version is the old one copied by TradingView, and the second is the updated version.
* Select the updated version from the dropdown to update your alert without deleting it.

**Practical Tip**:

* **Monitor Alerts**: Ensure that your alerts are using the correct, updated version of your script to avoid unexpected triggers.

Changing strategy settings on TradingView charts does not automatically update existing alerts. Manually update your alerts or switch the alert source to the updated script version to ensure they reflect your latest strategy settings.

***

### Paper Trading vs Live Trading: Accuracy and Reliability

{% embed url="https://www.youtube.com/watch?index=20&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=satpjMbTL1E" %}

**Margin of Error**:

* **Slippage and Commissions**: Paper trading often doesn't account for slippage (price differences due to market orders) and commissions, leading to potentially misleading performance results.
* **Market Depth**: Real-time market depth and liquidity impact trades differently in live markets compared to paper trading.

**Factors Impacting Accuracy**:

* **Order Execution**: Paper trading assumes perfect order execution, which isn't always the case in live trading.
* **Data Feeds**: Ensure you have real-time data feeds in both paper and live trading. Delayed data can significantly impact strategy performance.
* **Market Conditions**: Paper trading can't perfectly simulate live market conditions, especially during high volatility or low liquidity periods.

**Best Practices for Transitioning to Live Trading**:

* **Walk Forward Testing**: Test your strategy with a small amount of capital in live markets to observe real-world performance.
* **Monitor Performance**: Regularly check your strategy's performance, even with automated trading. Treat it like managing an employee rather than a hands-off task.

**Common Issues**:

* **Delayed Information**: Running strategies on delayed data can lead to incorrect trade execution and poor performance.
* **Behavioral Differences**: Paper and live trading accounts might behave differently. Always verify with live data.

**Continuous Monitoring**:

* **Active Management**: Automated trading still requires regular oversight to ensure strategies are performing as expected and to address any issues promptly.
* **Daily Check-Ins**: Treat your trades like employees—check if they executed correctly and if the strategy remains profitable.

Paper trading can provide valuable insights but has limitations compared to live trading due to slippage, commissions, and real-time market conditions. Transitioning to live trading with a small amount of capital and regular monitoring can help ensure your strategy's real-world effectiveness. Automated trading requires active management to be truly successful.

***

### Using Private TradingView Indicators with TradersPost

{% embed url="https://www.youtube.com/watch?index=21&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=UpkpfEHE-jw" %}

**Alert Functionality**:

* The private indicator must be set up to provide alerts.
* If you can't access or modify the code, ensure the indicator supports alert creation through TradingView’s interface.

**Creating Alerts**:

* Use the “Create Alert” dialog panel in TradingView.
* Ensure the alert setup allows you to tie the necessary JSON message that needs to be sent to TradersPost.

**Integration**:

* Once alerts are set up correctly, they can be used to trigger signals through TradersPost to your broker.
* This turns your private indicator into a fully functional strategy for automated trading.

As long as your private TradingView indicator is capable of generating alerts, you can use it to send trading signals through TradersPost to your broker. Ensure that the alert setup includes the necessary JSON message integration for seamless operation.

***

### Generating Opposite Alerts in TradingView for TradersPost

{% embed url="https://www.youtube.com/watch?index=22&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&t=9s&v=QJxgxckdDMU" %}

**Alert Flexibility**:

* The signal generated by TradingView (long or short) is sent as a JSON payload to TradersPost.
* You can modify this payload to execute any action, regardless of the original signal.

**Custom Actions**:

* **Inverted Signals**: A long signal can trigger a short action and vice versa.
* **Cross-Instrument Strategies**: You can configure a signal from one asset (e.g., a stock) to trigger an action in another asset (e.g., an options order).

**Implementation**:

* Ensure your alert setup includes the desired action in the JSON message.
* Customize the payload to reflect the opposite or desired action.

**Caution**:

* Simply inverting your strategy (e.g., using a short signal instead of a long) is not guaranteed to yield better results.
* It's important to test and validate the effectiveness of any strategy changes.

You can generate and execute opposite alerts using TradingView and TradersPost by customizing the JSON payload. However, inverting signals does not inherently improve strategy performance, and thorough testing is recommended.

***

### Stop Loss and Take Profit Orders in TradersPost

{% embed url="https://www.youtube.com/watch?index=25&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=9NPW7PBa8rQ" %}

**Question**: Are stop loss and take profit orders placed immediately upon entering a position, or are they sent to the market as limit orders when the price reaches a certain level?

**Answer**: The behavior of these orders depends on the broker's capabilities and how the orders are set up.

**Bracket Orders**:

* **Supported Brokers**: If the broker supports bracket orders (e.g., TradeStation), you can send a limit entry order along with attached limit take profit and stop loss orders.
* **Immediate Execution**: These orders are executed simultaneously at the broker level upon entering the position.
* **Broker-Level Management**: The broker manages these orders, ensuring they are placed and monitored without needing further input from TradersPost.

**Separate Orders**:

* **Non-Supported Brokers**: If the broker does not support bracket orders, you must place the entry order first and then follow up with take profit and stop loss orders.
* **Race Conditions**: Sending entry and stop orders simultaneously can lead to race conditions. If the stop order is sent first and there's no open position, it will be rejected.

**Recommended Approach**:

* **Bracket Orders**: Use bracket orders if supported by your broker to ensure all orders are placed together.
* **Sequential Orders**: For brokers that do not support bracket orders, place the entry order first, then add take profit and stop loss orders after confirmation of the entry.

**Recent Improvements**:

* **Order Modification**: TradersPost now allows modifying orders after the fact, enabling you to set a limit entry order and then add take profit or stop loss orders afterward.
* **Future Enhancements**: Plans to improve the process by attaching additional orders to entries, ensuring trailing stops or stop losses are set after confirming the entry.

For the most reliable execution, use bracket orders if your broker supports them. Otherwise, sequentially place your entry and stop/limit orders to avoid race conditions. TradersPost continues to enhance its features to support these functionalities better.

***

### Managing Positions in TradersPost: Exit Signals Explained

{% embed url="https://www.youtube.com/watch?index=27&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=qvTC9msfdjs" %}

**Question:** If I have TradersPost add to a position every time it receives an entry signal, what happens when it receives an exit signal? Will it exit all positions or just one?

**Answer**: It will exit all positions for the ticker.

**Position Management**:

* **Single Ticker as a Position**: TradersPost treats a single ticker as a position. Regardless of how many entry signals have been received, the total position is considered collectively.
* **Example**: If you send a signal to buy one share of Microsoft and then another to buy an additional share, you now hold two shares of Microsoft as a single position.

**Exit Signal**:

* **Entire Position**: When an exit signal is received, TradersPost will exit the entire position for the specified ticker, not just one part of it.
* **Flatten to Zero**: The exit signal will flatten your position to zero. For example, if you hold two shares, an exit signal will sell both shares, reducing your position to zero.

**Consistency Across Platforms**:

* **Unified Management**: TradersPost manages the total number of shares or contracts you hold with your broker, ensuring that exit signals accurately reflect your entire position.
* **Avoid Manual Reconciliation**: This approach eliminates the need for manual reconciliation between different trading interfaces or platforms.

TradersPost will exit the entire position when it receives an exit signal, regardless of how many entry signals have been sent. This unified management approach simplifies position tracking and ensures accurate execution of trades.

***

### Subscriber Limits in Automated Trading Strategies

{% embed url="https://www.youtube.com/watch?index=28&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=DbeLqCtJ__M" %}

**Question**: Is there a limit to the number of subscribers that a strategy can have?

**Answer**: While there is no explicit upper limit on the number of subscribers a strategy can have, there are practical considerations and acceptable use limitations.

**Key Points**:

1. **Technical Limitations**:
   * **Theoretical Limits**: There is a theoretical limit to the number of subscribers, but it's not explicitly defined.
   * **Large Groups**: Some groups share strategies with hundreds of members, resulting in thousands of trades. This can cause strain on the broker’s infrastructure.
2. **Broker Considerations**:
   * **Broker Adjustments**: In cases of extremely high trade volumes, brokers may need to make hardware and software adjustments to handle the load.
   * **Commission Value**: Brokers generally aim to accommodate high trade volumes as they earn commissions from each trade.
3. **TradersPost System**:
   * **No Explicit Limit**: TradersPost does not have a specific limit on the number of subscribers, but system performance is monitored.
   * **Trade Volume**: The focus is more on the volume of trades rather than the number of subscribers. High trade volume can lead to race conditions and performance issues.
4. **Practical Implications**:
   * **Race Conditions**: Sending multiple signals simultaneously can lead to race conditions, affecting the performance and accuracy of the trading system.
   * **Scalability**: If a strategy has thousands of subscribers placing trades at the same time, it may cause performance bottlenecks.

**Custom Payload Limits**:

* **JSON Payload**: While there is no strict limit on the size of custom properties in the JSON payload, sending extremely large data sets can cause bandwidth issues.
* **Bandwidth Considerations**: Excessive data in signals can lead to delays and performance issues.

While there is no explicit limit on the number of subscribers a strategy can have on TradersPost, practical considerations such as trade volume and system performance need to be managed. High trade volumes can cause performance issues, and brokers may need to make adjustments to accommodate large groups. Monitoring trade volume and avoiding excessive data in JSON payloads are recommended for optimal performance.

***

### Can I close my position outside of my trading window?

{% embed url="https://www.youtube.com/watch?index=31&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=2Ft7VdwvhNM" %}

**Question**: Is there a way to set trading window hours to only open positions during that window but still close them outside of that window?

**Answer**: Currently, TradersPost allows you to set trading window hours, but there is a limitation regarding closing positions outside this window.

**Current Functionality**:

* **Trading Window**: You can specify a trading window (e.g., 10:00 AM to 12:00 PM Eastern Time) during which positions can be opened.
* **Stop Loss/Take Profit**: If you open a position within this window and attach a stop loss or take profit order, these will still execute outside the trading window as they are managed by the broker.

**Exit Signals**:

* **Restriction**: Currently, TradersPost rejects exit signals that are sent outside of the specified trading window.
* **Future Enhancement**: There is a potential enhancement under consideration to allow exit signals to be executed outside the trading window, possibly through an additional setting like a checkbox labeled “Allow exits outside of window.”

**Granularity and Flexibility**:

* **Strategy Implementation**: You can build and refine strategy logic on TradingView, within TradersPost, and at the broker level.
* **User Control**: Offering granular control provides users with flexibility, though it introduces complexity and potential challenges in debugging and managing the overall strategy.

**Balancing Simplicity and Flexibility**:

* **Tool Provision**: TradersPost aims to provide a versatile toolset, allowing users to decide how to best utilize these tools for their trading strategies.
* **Best Practices**: For consistency, try to keep as much logic within the strategy itself (e.g., in TradingView) and minimize separate logic layers on TradersPost and the broker.

While you can set trading windows for opening positions in TradersPost, currently, exit signals outside this window are not automatically allowed. Future enhancements may provide more flexibility in managing exit signals outside of trading windows. Balancing simplicity and flexibility in your trading strategy setup is crucial for effective management and troubleshooting.

***

### Difference between a market order and a stop market order

{% embed url="https://www.youtube.com/watch?index=32&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=njAPob5bKmM" %}

**Stop Market Order**: This order triggers a market or limit order when a specific price level is reached. It is not the same as a stop loss.

#### **Common Misunderstandings**

**Market Order Execution**:

* **Immediate Execution**: A market order is intended to execute immediately at the current market price, depending on the available volume and liquidity.
* **Not Guaranteed**: In rare cases, a market order might not fill if there is insufficient volume.

**Stop Market Order**:

* **Trigger Mechanism**: A stop market order activates a market order when the stop price is hit. It does not mean the order will fill at that exact stop price.
* **Gaps in Price**: If the market gaps below the stop price (e.g., during pre-market), the stop market order may not trigger until the market opens, potentially at a worse price.

**Example Scenario**:

* **Pre-market Gaps**: If you set a stop market order during pre-market and the market gaps below your stop price, the order might not trigger until the market reopens, potentially at a much lower price.

#### **Potential Issues**

**Order Rejection**:

* **Invalid Stop Price**: If the stop price is no longer valid by the time it reaches the broker, the order could be rejected.
* **Trading Window Rules**: Orders could be rejected if they fall outside of predefined trading windows or after market hours where only limit orders are allowed.

**Strategy Configuration**:

* **Incorrect Order Type**: Using a stop market order when a plain market order is needed can lead to execution issues.
* **Dynamic Stops**: When using dynamic stops (e.g., moving averages), ensure the exit signal sent to the broker is a market order, as the stop condition has already been met.

#### **Best Practices**

1. **Exit Signal**: Ensure your exit signal is a regular market order to avoid issues with invalid stop prices.
2. **Verify Strategy Settings**: Double-check your TradingView strategy and TradersPost settings to ensure compatibility and correct execution of orders.

Understanding the nuances between market orders and stop market orders is crucial for effective trading. Ensure that your strategy configuration aligns with your trading goals and market conditions to avoid order execution issues. If problems persist, review the specific conditions and settings to identify potential areas of improvement.

***

### Difference between action=exit and sentiment=flat

{% embed url="https://www.youtube.com/watch?index=33&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=-2I2bAaOXhw" %}

**Question**: What is the difference between using `"action": "exit"` versus `"sentiment": "flat"` if the goal is to exit a position?

**Answer**: There is no functional difference; they both serve to exit a position. However, their usage depends on the strategy and platform configurations.

**Action Exit**:

* **Definition**: This command is used to exit an existing position without initiating a new one.
* **Use Case**: Suitable for scenarios where you want to ensure that you only exit a position and do not enter a new position on the other side.

**Sentiment Flat**:

* **Definition**: This term is used in conjunction with TradingView's strategy variables to express the intention to exit a position.
* **Integration with TradingView**: TradingView uses sentiment (long, short, flat) along with action (buy, sell) to convey whether to exit a position or switch sides (e.g., from long to short).
* **Compatibility**: Ensures that signals from TradingView are accurately translated into actions on TradersPost.

**When to Use Each**:

* **If Using TradingView**:
  * **Action Buy with Sentiment Flat**: Means buying to exit a short position (flattening).
  * **Action Sell with Sentiment Flat**: Means selling to exit a long position (flattening).
* **If Not Using TradingView**:
  * **Action Exit**: You can rely solely on this command to exit positions without worrying about sentiment flat.

**Configuration Tips**:

* **One-Sided Strategies**: If your strategy only takes long positions, you can set the strategy to be bullish only on TradersPost, eliminating the need for sentiment flat.
* **Avoiding Unintended Positions**: If you want to avoid accidentally opening a new position when exiting, ensure your signals and broker configurations are clear and specific (e.g., using "sell to close" commands where applicable).

**Edge Cases and Best Practices**:

* **Race Conditions**: In scenarios where orders are processed simultaneously (e.g., stop loss triggers and exit signals), race conditions might occur. Ensure your strategy handles these appropriately to avoid unintended positions.
* **Broker API Specificity**: Some brokers differentiate between sell and sell short actions. Ensure your broker's API settings are configured to prevent accidental short positions when exiting long positions.

Both action exit and sentiment flat are used to exit positions. Action exit is a straightforward command to exit a position, while sentiment flat is used primarily for compatibility with TradingView's signaling. Proper configuration and understanding of these commands ensure accurate and intended trade executions.

***

### Webhook test signals when limiting IP addresses

{% embed url="https://www.youtube.com/watch?index=35&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=BrYU7y0Ysxc" %}



***

### Tips for Troubleshooting automated trading strategies

{% embed url="https://www.youtube.com/watch?index=36&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=LRoXWKd237k" %}

**Scenario**: When "Limit to TradingView" is selected, test signals sent from TradersPost to the webhook are blocked.

**Current Behavior**:

* Designed to only accept signals from TradingView for security.
* Blocking test signals from TradersPost when this option is enabled is intentional.

While the current system is working as intended, adding an option for test signals from TradersPost and improving documentation can reduce confusion and support tickets.

***

### How do I offset my price for automated strategies?

{% embed url="https://www.youtube.com/watch?index=38&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=o_fx2dNT6i4" %}

**Question**: Is there any update on when we can get into a position offset from the given price?

**Answer**: You can offset entry prices today by doing the necessary calculations on the strategy side.

While direct support within TradersPost is not available yet, you can achieve the desired offset by handling the calculations within your strategy script before sending the signals.

***

### Can I automate trade on indices with TradersPost?

{% embed url="https://www.youtube.com/watch?index=39&list=PLauFD1wHyS9GPrCq-jBXt_Gl-LAtoCI3Q&pp=gAQBiAQB&v=sjGwNSxAYOY" %}

**Question**: Can I trade indices?

**Answer**: TradersPost supports stock and ETF options, not index options.

**ETFs Tracking Indices**:

* **S\&P 500**: Tradeable via SPDR S\&P 500 ETF (SPY).
* **NASDAQ 100**: Tradeable via Invesco QQQ ETF (QQQ).
* **DAX**: Tradeable through DAX ETFs listed on NASDAQ.

**Technical Differences**:

* **Option Styles**: Index options (European style) have different rules compared to ETF options (American style).

While direct trading of index options is not supported on TradersPost, you can trade ETFs that track these indices. Future integration may expand support for index options.
