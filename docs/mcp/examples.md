# Example Prompts

Ready-to-use prompts you can try after connecting Anny to your AI client.

---

## Market Analysis

> **What's the CFO Line reading for BTC?**

Returns the current indicator state, recent transitions, and context.

> **Compare the CFO Line state for ETH across all timeframes**

Anny will check the 1d, 4h, and 1h intervals and summarize alignment or divergence.

> **Which of these coins is showing strength right now: SOL, AVAX, LINK?**

Anny checks each asset and reports which are in Accumulate, Wait, or Distribute.

---

## Portfolio Review

> **How is my portfolio doing?**

Returns a full portfolio table with prices, P&L, and indicator states for every position.

> **Show me just my Binance positions**

Filters to a single exchange.

> **Which of my holdings are in a Distribute state?**

Anny reads your portfolio and highlights assets showing weakness.

---

## Historical Scenario Analysis

> **Run a scenario analysis for BTC over the last year**

Returns performance metrics and the top 5 notable entries/exits.

> **How would the CFO Line have performed on ETH using the 4h chart over 6 months?**

Runs the analysis with custom interval and period settings.

> **Compare scenario analysis results for SOL on daily vs 4-hour**

Anny runs both analyses and compares the results.

---

## Custom Strategy Builder

> **Backtest buying BTC when RSI(14) crosses below 30, with price above EMA(200), 3% stop-loss, and 2:1 risk-reward over the last year**

Runs a full backtest with performance metrics, trade history, equity curve, and current signal status.

> **Is RSI below 30 on BTC right now?**

Scans live market data and returns current indicator values plus signal status.

> **Try the same strategy but with RSI 25 instead of 30, and add an ADX > 25 confirmation**

Iterate on your strategy — adjust thresholds, add/remove indicators, change timeframes.

> **Backtest a strategy on ETH 4h where EMA(9) crosses above EMA(21), but only when the daily RSI is above 50**

Multi-timeframe strategy: 4-hour trigger with a daily confirmation.

> **Deploy this strategy as a bot on Binance SPOT with $200 USDT**

Creates a paused bot on your exchange. Activate it from the dashboard when ready.

> **What's the strategy on bot abc123? Change the stop-loss to 4%**

Retrieve and update strategy rules on an existing bot.

---

## Multi-Turn Conversations

> **What's the CFO Line reading for BTC?**
>
> *[Anny responds with the current state]*
>
> **What about on the 4-hour chart?**
>
> *[Anny uses conversation context to check BTC on 4h]*
>
> **Run a scenario analysis for it**
>
> *[Anny runs the analysis for BTC]*

The `ask_anny` tool supports multi-turn context via conversation IDs.

---

## Feedback

> **The portfolio tool is showing stale prices for my Bybit positions — they haven't updated in over an hour**

Sends a detailed bug report directly to the Anny development team.
