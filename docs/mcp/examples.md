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

## Daily Briefing & Market State

> **Give me a morning briefing**

Returns an AI-generated summary of market conditions and portfolio-relevant observations.

> **What's the current market sentiment?**

Pulls the Fear & Greed Index, BTC technicals, ETF flows, funding rates, and on-chain metrics.

> **Are funding rates elevated right now?**

Anny checks derivatives data and reports funding rates alongside liquidation activity.

---

## Price Checks

> **What's the current price of SOL?**

Returns the live price, 24h change, range, and volume.

> **How much is ETH right now?**

Quick price lookup without a full analysis — fast and lightweight.

---

## Macro Analysis

> **How is Bitcoin correlating with gold right now?**

Returns the BTC vs Gold ratio, current values, and an AI-generated analysis of the store-of-value narrative.

> **What's the relationship between BTC and the dollar index?**

Pulls the BTC vs DXY comparison with inverse correlation context and dollar strength impact.

---

## Portfolio Review

> **How is my portfolio doing?**

Returns a full portfolio table with prices, P&L, and indicator states for every position.

> **Show me just my Binance positions**

Filters to a single exchange.

> **Which of my holdings are in a Distribute state?**

Anny reads your portfolio and highlights assets showing weakness.

---

## Risk Assessment

> **How risky is my portfolio right now?**

Returns a composite risk score (0-100) broken down by portfolio, market, on-chain, and macro factors.

> **Should I be worried about my positions?**

Anny evaluates your risk exposure and lists the top contributing factors in plain language.

> **Is it a good time to go long on ETH?**

Runs a technical risk assessment with RSI, ADX, MACD, and volume analysis for the specified direction.

> **What's the risk of shorting SOL on futures?**

Assesses short-side technical conditions on the FUTURES account.

---

## Portfolio Scenarios

> **What happens to my portfolio if BTC drops 30%?**

Projects the impact of a BTC crash on every asset you hold.

> **Simulate a full market crash like 2022**

Anny parses the scenario into price movements and applies them across your portfolio.

> **What if ETH doubles from here?**

Models the upside impact on your positions and total portfolio value.

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

## Strategy Optimization

> **Optimize the CFO Line on BTC daily over the last year**

Diagnoses losing trade patterns and recommends filter settings to eliminate them. Costs 8 credits.

> **Why is my strategy losing money on ETH?**

Runs the optimizer to identify whipsaw, weak conviction, counter-trend, or revenge trade patterns.

> **Find better settings for SOL on the 4-hour chart**

Tests 15-20 filter configurations and compares baseline vs optimized performance.

---

## Stop-Loss & Position Sizing

> **Where should I put my stop-loss if I'm going long on BTC at $65,000?**

Calculates stop-loss levels using three models (ATR volatility, swing structure, and adaptive regime detection) plus take-profit targets at multiple risk-reward ratios.

> **Calculate my position size with a $10,000 account, entry at $65,000, and stop at $62,000**

Returns the position size in USD and units, risk amount, and portfolio allocation percentage.

> **Use Kelly criterion with a 55% win rate and 2:1 win-loss ratio**

Applies Half-Kelly sizing with expected value analysis and cap warnings.

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
