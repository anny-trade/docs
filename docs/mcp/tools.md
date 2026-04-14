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
| backtest_custom_strategy | true | false | true |
| scan_custom_signals | true | false | true |
| deploy_strategy_as_bot | false | false | false |
| get_bot_strategy | true | false | true |
| update_strategy_config | false | false | true |

Read-only tools never modify your account. `deploy_strategy_as_bot` creates a new bot (always paused). `update_strategy_config` modifies an existing bot's rules.
