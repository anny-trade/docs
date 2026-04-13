---
title: Tools Reference
parent: MCP Connector
nav_order: 3
---

# Tools Reference

All available MCP tools, their parameters, and response formats.

---

## ask\_anny

Ask Anny anything about crypto, your portfolio, or market insights.

**Auth required:** No (guest mode available with limited context)

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `message` | string | Yes | Your question (1–2000 characters) |
| `conversation_id` | string | No | Pass this from a previous response to continue a multi-turn conversation |

### Example

```
"What's the CFO Line reading for ETH?"
```

### Response

Returns Anny's response text plus a `conversation_id` for follow-ups. Authenticated users get full portfolio context; guests get public market data only.

---

## get\_market\_analysis

Get the current CFO Anny Line indicator reading for any crypto asset.

**Auth required:** No

### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `asset` | string | Yes | — | Crypto symbol: `BTC`, `ETH`, `SOL`, etc. |
| `interval` | string | No | `1d` | Chart interval: `1d`, `4h`, or `1h` |
| `trade_market` | string | No | `USDT` | Quote currency |

### Example

```
"Show me the CFO Line reading for SOL on the 4h chart"
```

### Response

Returns:
- Current CFO Anny Line state: **Accumulate** (strength), **Wait** (neutral), or **Distribute** (weakness)
- Recent state transitions (last 5 changes with dates)
- Context on why the indicator state changed

---

## get\_portfolio\_status

Get your current crypto portfolio overview across all connected exchanges.

**Auth required:** Yes

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `exchange` | string | No | Filter to a specific exchange: `BINANCE`, `BYBIT`, etc. Omit to see all. |

### Example

```
"How is my portfolio doing?"
"Show me just my Binance positions"
```

### Response

Returns a table with:
- Each asset you hold
- Current price and 24h change
- Position size and unrealised P&L
- CFO Anny Line indicator state per asset
- Summary: count of Accumulate/Wait/Distribute assets and total P&L

---

## run\_scenario\_analysis

Run a historical scenario analysis for a crypto asset using Anny's CFO Line indicator.

**Auth required:** Yes

### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `asset` | string | Yes | — | Crypto symbol: `BTC`, `ETH`, `SOL`, etc. |
| `interval` | string | No | `1d` | Candle interval: `1d`, `4h`, or `1h` |
| `period` | string | No | `1y` | Lookback: `3M` (3 months), `6M`, or `1y` |

### Example

```
"Run a scenario analysis for BTC over the last year"
"How would the CFO Line have performed on ETH 4h over 6 months?"
```

### Response

Returns:
- Total return, win rate, Sharpe ratio, max drawdown
- Total entries and profit factor
- Top 5 notable entries with entry/exit prices and dates

Results are computed in real-time and may take 10–30 seconds depending on the period.

---

## feedback\_to\_anny

Send feedback, report a bug, or suggest an improvement.

**Auth required:** No

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `text` | string | Yes | Your feedback (1–5000 characters) |

### Example

```
"The portfolio tool doesn't show my Bybit positions"
```

### Response

Confirmation that your feedback was recorded.

---

## Safety Annotations

All tools include [MCP safety annotations](https://modelcontextprotocol.io/specification/draft/schema#toolannotations):

| Tool | readOnlyHint | destructiveHint | idempotentHint |
|------|-------------|-----------------|----------------|
| ask_anny | true | false | false |
| get_market_analysis | true | false | true |
| get_portfolio_status | true | false | true |
| run_scenario_analysis | true | false | true |
| feedback_to_anny | false | false | true |

All tools are read-only except `feedback_to_anny` (which writes feedback to our system but never modifies your account or positions).
