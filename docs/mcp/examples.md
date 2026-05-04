# Example Prompts

Ready-to-use prompts you can try after connecting Anny to your AI client.

---

## Market Analysis

> **What's the CFO Line reading for BTC?**

Returns the current indicator state, recent transitions, and context.

> **Compare the CFO Line state for ETH across all timeframes**

Anny checks the 1d, 4h, and 1h intervals and summarizes alignment or divergence.

> **Which of these coins is showing strength right now: SOL, AVAX, LINK?**

Anny checks each asset and reports which are in Accumulate, Wait, or Distribute.

> **Compare SOL vs ETH**

Head-to-head comparison with CFO Line states, performance spread, technicals, and fundamentals.

---

## Market State & Sentiment

> **What's the current market sentiment?**

Pulls the Fear & Greed Index, BTC technicals, ETF flows, funding rates, and on-chain metrics.

> **Are funding rates elevated right now?**

Anny checks derivatives data and reports funding rates alongside liquidation activity.

> **Give me a full market overview**

Cross-market analysis: BTC regime, correlations with S&P 500 and Gold, market cap data.

---

## Institutional Intelligence

> **What are the latest ETF flows?**

Returns daily, weekly, and monthly ETF flow data with per-issuer breakdown.

> **How much Bitcoin does MicroStrategy hold?**

Corporate treasury data across 154+ companies.

> **Is there smart money accumulation happening?**

Whale on-chain activity, stablecoin supply, and mined vs bought ratios.

---

## Flip Intelligence

> **BTC just flipped to Accumulate — should I trust it?**

Returns a confidence score (0–100) with sub-scores explaining why the flip may or may not hold.

> **Is this flip contrarian or consensus?**

Anny checks what percentage of all assets are in each state and flags if the flip goes against the crowd.

---

## Technical Analysis

> **Show me RSI and MACD for ETH on the daily chart**

Returns momentum, trend, and volume indicators via `get_technical_analysis`.

> **Is BTC overbought on the 4h chart?**

Anny checks RSI, ADX, and EMA alignment for the specified timeframe.

---

## Portfolio Scenarios

> **What happens to my portfolio if BTC drops 30%?**

Projects the impact of a BTC crash on every asset you hold.

> **Simulate a full market crash like 2022**

Anny parses the scenario into price movements and applies them across your portfolio.

> **What if ETH doubles from here?**

Models the upside impact on your positions and total portfolio value.

---

## Tax & Holdings

> **Do I need to pay DARF this month?**

Returns monthly disposals, gains/losses, thresholds, and DARF estimate.

> **What's my cost basis?**

Shows per-asset holdings with weighted average cost and unrealized gain/loss.

---

## Signal Management

> **What signals do I have?**

Lists all active trading signals with asset, direction, entry price, P&L, and automation state.

> **Show me signal #12345**

Detailed view of a specific signal including targets, stop-loss, and CFO Line state.

> **Enable auto-buy for signal #12345**

Toggles the auto-invest flag. DB-only — no exchange side-effect.

> **Change my target to $70,000 for signal #12345**

Updates the target price in the database.

> **Cancel my pending order on signal #12345**

Cancels the exchange order. Anny confirms before executing.

---

## Bot Management

> **List my bots**

Shows all bots with type, status, exchange, and asset.

> **How is my bot abc123 performing?**

Returns recent trigger events — entries, take-profits, stops fired.

> **Pause my bot abc123**

Pauses the bot. Anny confirms before executing.

---

## Portfolio Management

> **How much USDT do I have?**

Checks your exchange balance for a specific asset.

> **Can I trade DOGE on my exchange?**

Checks symbol availability across your connected exchanges.

> **Buy $200 worth of ETH**

Anny shows a preview first, then asks for confirmation before placing the real order.

> **Do I have any open orders?**

Lists all pending orders across connected exchanges.

> **Cancel order 12345678 for BTC/USDT**

Cancels the specific order after confirmation.

---

## CFO Line Backtest

> **Backtest the CFO Line on BTC daily over the last year**

Returns performance metrics: total return, win rate, Sharpe, max drawdown, profit factor.

> **How does the CFO Line perform on ETH 4h over 6 months?**

Runs the analysis with custom interval and period settings.

---

## Custom Strategy Builder

> **Backtest buying BTC when RSI(14) crosses below 30, with price above EMA(200), 3% stop-loss, and 2:1 risk-reward over the last year**

Runs a full backtest with metrics, trade history, and current signal status.

> **Is RSI below 30 on BTC right now?**

Scans live data for your strategy conditions.

> **Try the same strategy but with RSI 25 instead of 30, and add an ADX > 25 confirmation**

Iterate on your strategy — adjust thresholds, add/remove indicators, change timeframes.

> **Deploy this strategy as a bot on Binance SPOT with $200 USDT**

Creates a paused bot. Activate from the dashboard when ready.

---

## Strategy Optimization

> **Optimize the CFO Line on BTC daily over the last year**

Diagnoses losing patterns and recommends filter settings. Costs 900 credits.

> **Why is my strategy losing money on ETH?**

Identifies whipsaw, weak conviction, counter-trend, or revenge trade patterns.

---

## Trading Ideas

> **Tell me about the BTC EMA crossover strategy**

Returns full analysis of a published strategy: rules, metrics, regime breakdown, OOS validation.

> **Deploy the btc-ema-crossover-1d strategy on Binance with $500**

Creates a bot from a published strategy.

---

## Support & Knowledge

> **How do I connect my Binance account?**

Routes to the Knowledge Agent for platform how-to questions.

> **My portfolio isn't syncing**

Routes to the Support Agent with automatic diagnostics.

> **How do I get my Bybit API key?**

Step-by-step exchange setup guide.

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
> **Run a backtest for it**
>
> *[Anny runs the analysis for BTC]*

The `ask_anny` MCP tool supports multi-turn context via conversation IDs.
