---
title: Example Prompts
parent: MCP Connector
nav_order: 4
---

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
