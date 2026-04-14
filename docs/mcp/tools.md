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

## get\_price

Get the current price of any crypto asset. Lightweight and fast — use this when you just need a quick price check, not a full market analysis.

**Auth required:** No

### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `asset` | string | Yes | — | Crypto symbol: `BTC`, `ETH`, `SOL`, etc. (1–10 characters) |
| `trade_market` | string | No | `USDT` | Quote currency |

### Example

> "What's the price of ETH right now?"

### Response

Returns:

- Current price in the specified quote currency
- 24h price change (percentage)
- 24h range (low – high)
- 24h trading volume

```
BTC/USDT: $67,432.10 (+2.35%)
24h Range: $65,800.00 – $68,100.00
24h Volume: $1,234,567,890.00
```

---

## get\_market\_state

Get a comprehensive snapshot of current crypto market conditions, covering sentiment, technicals, derivatives, ETF flows, and on-chain metrics.

**Auth required:** Yes

### Parameters

None.

### Example

> "How is the market doing right now?"

### Response

Returns a multi-section overview:

- **Fear & Greed Index** — 0–100 scale with classification (Extreme Fear / Fear / Neutral / Greed / Extreme Greed)
- **Risk Summary** — market, on-chain, and macro risk scores (0–100) with zone labels
- **BTC Overview** — price, RSI(14) with interpretation, EMA 20/50/200 levels, distance from EMA 200, dominance, golden/death cross signals
- **Derivatives** — BTC and ETH funding rates (8h + annualised), 24h liquidations
- **Bitcoin ETF Flows** — daily flow, 7-day net flow, flow streak
- **On-Chain Metrics** — MVRV Z-Score, NUPL, Coinbase Premium, and 7-day exchange netflow, each with interpretation zones

---

## get\_daily\_briefing

Get an AI-generated daily briefing about market conditions and your portfolio. The briefing is personalised to your holdings and generated fresh each day.

**Auth required:** Yes

### Parameters

None.

### Example

> "Give me my morning briefing"

### Response

Returns a concise 60–100 word summary combining:

- Current market state and sentiment
- Key market events and shifts
- Portfolio-relevant observations

---

## get\_risk\_score

Get a composite risk score (0–100) for your portfolio, calculated from four weighted components.

**Auth required:** Yes

### Parameters

None.

### Example

> "How risky is my portfolio right now?"

### Response

Returns:

- **Overall score** — 0–100 with label: Low Risk, Moderate Risk, High Risk, or Very High Risk
- **Score change** — delta since last reading
- **Breakdown** — sub-scores for each component:
    - Portfolio (30%) — concentration, diversification, allocation by tier
    - Market (30%) — BTC technicals, Fear & Greed, ETF flows, funding rates
    - On-Chain (25%) — MVRV valuation, NUPL sentiment, exchange flows
    - Macro (15%) — Fed posture, macro shocks, meeting timing
- **Key Factors** — top risk factors explained in plain language
- **Portfolio Breakdown** — each asset with allocation percentage and tier (blue-chip, large-cap, mid-cap, small-cap)

---

## get\_macro\_analysis

Get an AI-generated analysis comparing Bitcoin against a macro indicator. Each analysis includes current values, ratio, and a multi-paragraph interpretation.

**Auth required:** No

### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `pair` | string | Yes | — | Macro comparison pair: `btc-xau`, `btc-dxy`, or `btc-pmi` |

Available pairs:

- **btc-xau** — BTC vs Gold: correlation, divergence, store-of-value narrative
- **btc-dxy** — BTC vs US Dollar Index: inverse correlation, dollar strength impact
- **btc-pmi** — BTC vs Manufacturing PMI: economic activity correlation

### Example

> "How does Bitcoin correlate with gold right now?"

### Response

Returns:

- **Data snapshot** — BTC price, indicator value, ratio, and data source
- **Analysis** — AI-generated multi-paragraph interpretation of the current relationship

---

## Custom Strategy Tools

For full documentation on custom strategies, see [Custom Strategy Builder](custom-strategies.md).

### backtest\_custom\_strategy

Backtest a custom trading strategy against historical data using technical indicators.

**Auth required:** Yes | **Cost:** 5 credits

#### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `name` | string | No | `Custom Strategy` | Strategy name |
| `asset` | string | Yes | — | Crypto symbol: `BTC`, `ETH`, `SOL`, etc. |
| `interval` | string | No | `1d` | Primary interval: `1d`, `4h`, `1h` |
| `direction` | string | No | `long` | Trade direction: `long` or `short` |
| `lookback_period` | string | No | `6M` | Lookback: `3M`, `6M`, `1y` |
| `trigger` | object | Yes | — | Entry signal condition (see [condition format](#condition-format)) |
| `confirmations` | array | No | `[]` | Additional conditions that must all be true |
| `stop_loss` | object | No | `3%` | Stop-loss config: `{type, value}` |
| `take_profit` | object | No | `6%` | Take-profit config: `{type, value}` |

#### Example

```
"Backtest a strategy on BTC where RSI(14) crosses below 30,
with price above EMA(200), 3% stop-loss, and 2:1 risk-reward"
```

#### Response

Returns performance metrics (return, win rate, Sharpe, drawdown), trade history, equity curve, train/test split, price/volume context, and current signal status.

---

### scan\_custom\_signals

Check if your strategy conditions are met right now.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `asset` | string | Yes | — | Crypto symbol |
| `interval` | string | No | `1d` | Primary interval |
| `trigger` | object | Yes | — | Trigger condition |
| `confirmations` | array | No | `[]` | Confirmation conditions |

#### Example

```
"Is RSI below 30 on BTC right now?"
```

#### Response

Returns current value of each indicator, whether each condition is met, and overall signal status: **ACTIVE** (all conditions met, trigger just fired), **APPROACHING** (getting close), or **INACTIVE**.

---

### deploy\_strategy\_as\_bot

Deploy a strategy as a live bot on your connected exchange.

**Auth required:** Yes

#### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `exchange` | string | Yes | — | Exchange: `binance`, `bybit`, `okx`, etc. |
| `account` | string | No | `SPOT` | Account type: `SPOT` or `FUTURES` |
| `investment` | number | No | `100` | Investment in quote asset |
| `quote_asset` | string | No | `USDT` | Quote asset |
| *+ all strategy params* | | | | Same as `backtest_custom_strategy` |

The bot is created in **paused** mode. Activate it from the Anny Trade dashboard when ready.

---

### get\_bot\_strategy

Retrieve the strategy definition for a custom strategy bot.

**Auth required:** Yes

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `bot_id` | string | Yes | Bot ID |

---

### update\_strategy\_config

Update the strategy rules on an existing bot.

**Auth required:** Yes

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `bot_id` | string | Yes | Bot ID |
| `strategy` | object | Yes | Updated strategy definition |

---

## Condition Format

Each condition (trigger or confirmation) uses this format:

| Field | Type | Description |
|-------|------|-------------|
| `indicator` | string | `RSI`, `EMA`, `SMA`, `MACD`, `ADX`, `ATR`, `BBANDS`, `STOCHRSI`, or `PRICE` |
| `params` | object | Indicator parameters (e.g., `{"period": 14}`) |
| `field` | string | Output field (e.g., `value`, `histogram`, `upper`) |
| `operator` | string | `crosses_above`, `crosses_below`, `above`, `below` |
| `compare_to` | number or object | Threshold value (e.g., `30`) or another indicator reference |
| `interval` | string | Optional: override interval for multi-timeframe (e.g., `1d` on a `4h` strategy) |

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
| get_price | true | false | true |
| get_market_state | true | false | true |
| get_daily_briefing | true | false | false |
| get_risk_score | true | false | true |
| get_macro_analysis | true | false | true |
| backtest_custom_strategy | true | false | true |
| scan_custom_signals | true | false | true |
| deploy_strategy_as_bot | false | false | false |
| get_bot_strategy | true | false | true |
| update_strategy_config | false | false | true |

Read-only tools never modify your account. `deploy_strategy_as_bot` creates a new bot (always paused). `update_strategy_config` modifies an existing bot's rules.
