# Reading Your Portfolio

The `get_portfolio_status` tool gives you a complete view of your holdings across all connected exchanges, enriched with CFO Anny Line indicator states.

## What You Get

When you ask "How is my portfolio doing?", Anny returns a table like this:

| Asset | CFO Line | Price | 24h | Qty | P&L |
|-------|----------|-------|-----|-----|-----|
| BTC | Accumulate | $68,500 | +2.30% | 0.5 | $1,250 |
| ETH | Wait | $3,850 | -0.80% | 10 | -$320 |
| SOL | Distribute | $145 | -3.20% | 100 | -$890 |

**Summary:** 1 Accumulate, 1 Wait, 1 Distribute | Total P&L: $40

## Understanding the Columns

| Column | Description |
|--------|-------------|
| **Asset** | The crypto symbol |
| **CFO Line** | Current Anny Line state — Accumulate (strength), Wait (neutral), Distribute (weakness) |
| **Price** | Current market price |
| **24h** | Price change in the last 24 hours |
| **Qty** | Your position size |
| **P&L** | Unrealised profit or loss |

## Filtering by Exchange

If you have positions on multiple exchanges, you can filter:

> Show me just my Binance positions

This passes the `exchange` parameter to only show positions from that exchange.

## Using the Summary

The summary line gives you a quick health check:

- **Mostly Accumulate** — Your portfolio is in structurally strong assets
- **Mostly Wait** — Neutral phase, no strong directional bias
- **Mostly Distribute** — Your portfolio is in structurally weak assets

This is not advice on what to do — it's a snapshot of where your holdings sit relative to the CFO Line indicator.

## Prerequisites

To see portfolio data, you need:

1. An Anny Trade account (signed in via the MCP connector)
2. At least one exchange connected in your [Anny Trade settings](https://anny.trade/settings)
3. Active positions on the connected exchange

If you see "I don't see any positions", check that your exchange API keys are connected and that you have open positions.
