# Tools Reference

All available MCP tools organized by category, with parameters and response formats.

The source of truth for tool definitions is `anny-backend/src/askanny/tools/ToolDefinitions.js` (54 tools). This document covers every implemented tool.

---

## Technical Analysis

### get\_technical\_analysis

Get technical analysis indicators (RSI, MACD, EMA, ADX, OBV, VWAP, VROC, ADL, volume trend) for a cryptocurrency.

**Auth required:** No | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `symbol` | string | Yes | Trading pair with USDT quote, e.g. `BTCUSDT`, `ETHUSDT` |
| `timeframe` | string | Yes | Candlestick timeframe: `5m`, `15m`, `30m`, `1h`, `4h`, `1d`, `1w` |

#### Example

```
"Show me the RSI and MACD for ETH on the 4h chart"
```

#### Response

Returns momentum indicators (RSI, MACD, ADX), trend indicators (EMA 20/50/200), and volume indicators (OBV, VWAP, VROC, ADL, volume trend analysis).

---

### get\_anny\_line\_status

Get the CFO Anny Line indicator status for a specific cryptocurrency.

**Auth required:** No | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `symbol` | string | Yes | Asset symbol: `BTC`, `ETH`, `SOL`, etc. |

#### Example

```
"What's the CFO Line reading for BTC?"
"Show me the chart for SOL"
```

#### Response

Returns:

- Current CFO Anny Line state: **Accumulate** (strength), **Wait** (neutral), or **Distribute** (weakness)
- Date since current state has been active
- Recent state transitions (last 5 flips with dates)
- Band values (fast/slow)

---

### get\_flip\_intelligence

Get confidence scoring for a recent CFO Line state flip on a specific asset.

**Auth required:** No | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `asset` | string | Yes | Asset symbol: `BTC`, `ETH`, `SOL`, etc. |
| `timeframe` | string | No | Timeframe: `1h`, `1d`, `1w` (default: `1d`) |

#### Example

```
"Why did BTC flip to Accumulate? Should I trust it?"
```

#### Response

Returns:

- **Confidence score** (0–100) with label (Low / Medium / High / Very High)
- **Sub-scores**: band gap score, duration score, historical score
- **Contrarian flag**: whether the flip goes against the broader market
- **Market context**: percentage of all tracked assets in Accumulate / Wait / Distribute
- Detection timestamp

Returns `null` if no recent flip was detected for the asset.

---

### compare\_assets

Compare two cryptocurrencies head to head.

**Auth required:** No | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `base` | string | Yes | First asset symbol (e.g. `BTC`, `SOL`) |
| `quote` | string | Yes | Second asset symbol (e.g. `ETH`, `ADA`) |

#### Example

```
"Compare SOL vs ETH"
"Which is better, AVAX or LINK?"
```

#### Response

Returns:

- CFO Anny Line state for each asset
- Synthetic ratio CFO Line showing relative strength
- Performance spread (1d / 7d / 30d / 90d / 1y)
- Technical indicators (RSI, MACD, ADX, EMA) for both
- Fundamentals (ETF status, tokenomics, on-chain TVL/fees/dev activity) when available

---

### get\_institutional\_intelligence

Get institutional adoption data: ETF flows, corporate treasury holdings, whale activity.

**Auth required:** No | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `coin` | string | No | Focus on a specific coin (`BTC`, `ETH`, `SOL`, `XRP`). Default: BTC overview. |

#### Example

```
"What are the latest ETF flows?"
"How much Bitcoin does MicroStrategy hold?"
```

#### Response

Returns:

- **ETF flows**: BTC/ETH daily, 7d, 30d, YTD, per-issuer breakdown (BlackRock IBIT, Fidelity FBTC, etc.)
- **Corporate treasury**: MicroStrategy, MARA, Metaplanet — 154+ companies
- **On-chain**: whale activity, stablecoin supply, bitcoin mined vs bought ratio
- **ETF approval status** per coin
- **International ETFs**

---

## Market Intelligence

### get\_market\_state

Get a comprehensive snapshot of current crypto market conditions.

**Auth required:** Yes | **Cost:** Free

#### Parameters

None.

#### Example

```
"How is the market doing right now?"
"What's the current Fear & Greed?"
```

#### Response

Returns:

- **Fear & Greed Index** — 0–100 scale with classification
- **Risk Summary** — market, on-chain, and macro risk scores
- **BTC Overview** — price, RSI(14), EMA 20/50/200, dominance, golden/death cross signals
- **Derivatives** — BTC and ETH funding rates (8h + annualised), 24h liquidations
- **Bitcoin ETF Flows** — daily flow, 7-day net flow, flow streak
- **On-Chain Metrics** — MVRV Z-Score, NUPL, Coinbase Premium, exchange netflow

---

### get\_market\_analysis

Get cross-market analysis: BTC regime, correlations with traditional markets, market cap data.

**Auth required:** No | **Cost:** Free

#### Parameters

None.

#### Example

```
"Give me a full market overview"
"How is BTC correlating with equities?"
```

#### Response

Returns:

- BTC regime detection (SMA20/SMA50 crossover)
- 30-day correlations between BTC and S&P 500 / Gold (Pearson)
- S&P 500 and Gold prices with 7-day changes
- BTC 30-day range, total crypto market cap, ETH price
- Fear & Greed streak

---

### run\_scenario

Run a portfolio stress-test scenario against your holdings.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `scenario` | string | Yes | Free-text scenario: `"BTC drops 30%"`, `"2022-style crash"`, `"everything drops 20%"` |
| `assets` | array | No | Structured input: `[{asset: "BTC", changePct: -30}]`. Takes precedence over scenario string. |

#### Example

```
"What happens to my portfolio if BTC crashes 40%?"
"Simulate ETH doubling while BTC drops 10%"
```

#### Response

Returns before/after portfolio values, per-asset impact, allocation shifts, and risk score changes.

---

### find\_historical\_pattern

Find historical market conditions similar to current ones using cosine similarity matching.

**Auth required:** No | **Cost:** Free

#### Parameters

None.

#### Example

```
"Has this happened before?"
"Find historical parallels to current market conditions"
```

#### Response

Returns past periods with similar Fear & Greed, RSI, EMA position, and on-chain metrics, along with what happened next (7d, 30d, 90d BTC price changes).

!!! note "Coming Soon"
    This tool is registered but returns a "coming soon" message while data accumulation is in progress.

---

## Tax & Holdings

### get\_tax\_status

Get the user's current tax status including monthly disposals, gains/losses, DARF estimate, and transaction details.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `year` | integer | No | Year (e.g. 2026). Default: current year. |
| `month` | integer | No | Month 1–12. Default: current month. |

#### Example

```
"Do I need to pay DARF this month?"
"Show my crypto tax status for March"
```

---

### get\_tax\_holdings

Get the user's portfolio position with cost basis, weighted average cost, and unrealized gain/loss per asset.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `year` | integer | No | Year (e.g. 2026). Omit for current holdings. |
| `month` | integer | No | Month 1–12. Omit for current holdings. |

#### Example

```
"What's my cost basis?"
"Show my holdings and unrealized gains"
```

---

## Signal Management

### get\_signal

Get detailed information about a specific trading signal.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID to retrieve |

---

### list\_active\_signals

List all active trading signals and positions.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `exchange` | string | No | Filter to a specific exchange: `BINANCE`, `BYBIT`, etc. |
| `limit` | integer | No | Max signals to return (default: 20, max: 50) |

---

### get\_signal\_automation\_config

Get the full automation configuration for a specific signal.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID |

---

### analyze\_signal\_with\_cfo

Analyze a signal's asset using the CFO Anny Line indicator, respecting the signal's timeframe.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID to analyze |

---

### toggle\_auto\_invest

Enable or disable auto-invest (auto-buy) for a specific signal. DB-only toggle — no exchange side-effect.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID |
| `enabled` | boolean | Yes | `true` to enable, `false` to disable |

---

### toggle\_auto\_stop

Enable or disable auto-stop (stop-loss automation) for a specific signal.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID |
| `enabled` | boolean | Yes | `true` to enable, `false` to disable |

---

### toggle\_auto\_sell

Enable or disable auto-sell (take-profit automation) for a specific signal.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID |
| `enabled` | boolean | Yes | `true` to enable, `false` to disable |

---

### toggle\_auto\_trailing

Enable or disable trailing stop for a specific signal.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID |
| `enabled` | boolean | Yes | `true` to enable, `false` to disable |

---

### update\_signal\_target

Update a target price, stop-loss price, or entry price for a signal. DB-only — does NOT place or modify exchange orders.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID |
| `target_field` | string | Yes | Field to update: `tradeExitPrice1`–`5`, `tradeStopLossPrice`, `tradeEntryPriceMin`/`Mid`/`Max` |
| `price` | number | Yes | New price value |

---

### cancel\_pending\_order

Cancel a pending (unfilled) order on the exchange for a specific signal.

**Auth required:** Yes | **Endpoint:** `/v1/full` only | **Cost:** Free

> **Warning:** This tool has exchange side-effects.

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID owning the order |
| `order_id` | string | Yes | The exchange order ID to cancel |
| `reason` | string | No | Reason for cancellation (default: `"user-request-via-chat"`) |

---

### place\_take\_profit

Place a take-profit (sell) order on the exchange for a signal's position.

**Auth required:** Yes | **Endpoint:** `/v1/full` only | **Cost:** Free

> **Warning:** This tool has exchange side-effects.

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID |
| `price` | number | No | Sell price |
| `amount_to_sell` | number | No | Exact coin amount to sell |
| `amount_relative` | number | No | Percentage to sell (0–100) |
| `order_type` | string | No | `LIMIT` or `MARKET` (default: `LIMIT`) |

---

### place\_trailing\_stop

Place a trailing stop (stop-loss) order on the exchange for a signal's position.

**Auth required:** Yes | **Endpoint:** `/v1/full` only | **Cost:** Free

> **Warning:** This tool has exchange side-effects.

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID |
| `stop_price` | number | Yes | Stop trigger price |
| `limit_price` | number | No | Limit price for STOP_LOSS_LIMIT orders |
| `amount_to_sell` | number | No | Quantity to liquidate |
| `order_type` | string | No | `STOP_LOSS_LIMIT` or `STOP_LOSS` (default: `STOP_LOSS_LIMIT`) |

---

## Bot Management

### list\_bots

List all trading bots owned by the user.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `status` | string | No | Filter: `active`, `paused`, or `all` (default: `all`) |

#### Example

```
"List my bots"
"Show my active bots"
```

#### Response

Returns bot ID, title, type (TradingView/CFO/DIY/Custom Strategy), status, exchange, coin, and interval per bot.

---

### get\_bot\_config

Get full configuration for a specific bot.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `bot_id` | string | Yes | The bot ID |

---

### get\_bot\_fires

Get recent trigger events for a bot — entries, take-profits, stop-losses fired.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `bot_id` | string | Yes | The bot ID |
| `limit` | integer | No | Max events to return (default: 10, max: 50) |

#### Example

```
"How is my bot performing?"
"What trades did my bot make?"
```

---

### pause\_bot

Pause a trading bot. The bot stops processing triggers until restarted.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `bot_id` | string | Yes | The bot ID |
| `mode` | string | No | `pause` (all), `pauseLong`, or `pauseShort` (default: `pause`) |

---

### restart\_bot

Restart a paused trading bot.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `bot_id` | string | Yes | The bot ID |

---

### create\_bot\_from\_strategy

Deploy a strategy as a trading bot. Created in **paused** status.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `strategy_slug` | string | No | Published strategy slug (mutually exclusive with `strategy_json`) |
| `strategy_json` | object | No | Inline custom strategy from conversation (mutually exclusive with `strategy_slug`) |
| `exchange` | string | Yes | Exchange: `binance`, `bybit`, `okx`, etc. |
| `account` | string | No | `SPOT` or `FUTURES` (default: `SPOT`) |
| `investment` | number | Yes | Investment per trade in USDT |
| `quote_asset` | string | No | Quote asset (default: `USDT`) |

---

## Community (Signal Groups)

### list\_communities

List all signal communities the user is a member of.

**Auth required:** Yes | **Cost:** Free

#### Parameters

None.

#### Example

```
"Show my communities"
"What groups am I in?"
```

---

### get\_community\_pnl

Get profitability report for a specific signal community.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `community_id` | string | Yes | The partner channel ID |

---

### allocate\_community\_investment

Set the investment amount per signal for a community.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `community_id` | string | Yes | The partner channel ID |
| `investment` | number | Yes | Investment per signal in USDT |

---

## CFO Line Backtest & Optimizer

### run\_cfo\_line\_backtest

Run a CFO Line backtest for a specific asset.

**Auth required:** Yes | **Cost:** 100 credits

#### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `asset` | string | Yes | — | Crypto symbol: `BTC`, `ETH`, `SOL`, etc. |
| `interval` | string | No | `1d` | `1h`, `4h`, `1d`, `1w` |
| `period` | string | No | `1y` | `3m`, `6m`, `9m`, `1y` |
| `mode` | string | No | `long` | `long`, `long_short`, `short` |

#### Example

```
"Backtest the CFO Line on BTC daily over the last year"
"How does the CFO Line perform on ETH 4h?"
```

#### Response

Returns total return, buy & hold return, win rate, profit factor, Sharpe ratio, max drawdown, trade count, and filter rejection statistics.

---

### run\_optimizer

Run the CFO Line Optimizer (Anny Optimize) — diagnoses losing trades and prescribes optimized filter settings.

**Auth required:** Yes | **Cost:** 900 credits | **Minimum tier:** PRO

#### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `asset` | string | Yes | — | Crypto symbol |
| `interval` | string | No | `1d` | `1h`, `4h`, `1d`, `1w` |
| `period` | string | No | `1y` | `3m`, `6m`, `9m`, `1y` |
| `mode` | string | No | `long` | `long`, `long_short`, `short` |

#### Example

```
"Optimize BTC on the daily chart"
"Why is my ETH strategy losing? Diagnose it."
```

#### Response

Returns baseline vs optimized metrics, loss diagnosis by category (whipsaw, weak conviction, counter-trend, revenge trade), and recommended filter prescription.

---

## Custom Strategy Builder

For full documentation, see [Custom Strategy Builder](custom-strategies.md).

### backtest\_custom\_strategy

Backtest a custom trading strategy using technical indicators against historical data.

**Auth required:** Yes | **Cost:** Included in askAnny message cost

#### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `name` | string | No | `Custom Strategy` | Strategy name |
| `asset` | string | Yes | — | Crypto symbol |
| `interval` | string | No | `1d` | `1h`, `4h`, `1d`, `1w` |
| `direction` | string | No | `long` | `long` or `short` |
| `lookback_period` | string | No | `6M` | `3M`, `6M`, `1y` |
| `trigger` | object | Yes | — | Entry signal condition (see [Condition Format](#condition-format)) |
| `confirmations` | array | No | `[]` | Additional conditions (tier-gated: FREE=0, PRO=2, PRO+=4) |
| `stop_loss` | object | No | `3%` | `{type, value}` |
| `take_profit` | object | No | `6%` | `{type, value}` |

---

### scan\_custom\_signals

Check if your strategy conditions are met right now against live market data.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `asset` | string | Yes | Crypto symbol |
| `interval` | string | No | Primary interval (default: `1d`) |
| `trigger` | object | Yes | Trigger condition |
| `confirmations` | array | No | Confirmation conditions |

#### Response

Returns per-condition status (MET / NOT_MET / APPROACHING) and overall signal status: **ACTIVE**, **APPROACHING**, or **INACTIVE**.

---

### prescan\_custom\_strategy

Free pre-scan showing loss pattern breakdown without revealing the prescription. Use after a backtest shows poor results.

**Auth required:** Yes | **Cost:** Free

#### Parameters

Same as `backtest_custom_strategy`.

#### Response

Returns loss pattern categories (trend misalignment, overextended entry, high volatility, revenge entry, equity drawdown) with counts, and an improvement potential rating (LOW / MEDIUM / HIGH).

---

### optimize\_custom\_strategy

Run the Custom Strategy Optimizer — diagnoses losses and tests 10–15 meta-filter combinations to find optimal settings.

**Auth required:** Yes | **Cost:** 900 credits | **Minimum tier:** PRO

#### Parameters

Same as `backtest_custom_strategy`.

#### Response

Returns baseline vs optimized metrics, loss diagnosis with per-category rationales, and the winning prescription.

---

## Trading Ideas

### get\_trading\_idea\_analysis

Get detailed analysis of a published trading strategy from the Quant Search pipeline.

**Auth required:** No | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `strategy_slug` | string | No | Strategy slug (e.g. `btc-ema-crossover-1d`) |
| `idea_id` | integer | No | Trading idea ID (alternative to slug) |

#### Example

```
"Tell me about the BTC EMA crossover strategy"
```

#### Response

Returns strategy rules, backtest metrics, CFO regime breakdown, OOS validation, risk level, and description.

---

## Portfolio Management

### check\_symbol\_availability

Check if a crypto asset is available for trading on the user's connected exchanges.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `asset` | string | Yes | Crypto symbol: `BTC`, `ETH`, `SOL`, etc. |

#### Example

```
"Can I trade DOGE on my exchange?"
"Is PEPE available on Binance?"
```

#### Response

Returns whether the asset is available for SPOT trading, which exchange(s) support it, the full trading pair, and minimum order size.

---

### execute\_market\_order

Buy or sell a crypto asset at market price. Uses a **2-step confirmation flow**: preview first (`confirm=false`), then execute (`confirm=true`).

**Auth required:** Yes | **Endpoint:** `/v1/full` only | **Cost:** Free

#### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `asset` | string | Yes | — | Crypto symbol |
| `action` | string | Yes | — | `buy` or `sell` |
| `amount` | number | Yes | — | USDT amount (buy) or asset quantity (sell) |
| `confirm` | boolean | No | `false` | `true` to execute after preview |

#### Example

```
"Buy $200 worth of ETH"
"Sell 0.5 SOL"
```

!!! warning "Safety"
    Places **real orders** on your exchange. A `MAX_CHAT_ORDER_USDT` cap is enforced server-side. SPOT market only — no futures, no margin. Not available in guest mode.

---

### get\_exchange\_balance

Check available balance on connected exchanges.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `asset` | string | No | Filter to a specific asset (e.g. `USDT`, `BTC`). Omit for all. |
| `exchangeCode` | string | No | Filter to a specific exchange. Omit for all. |

#### Example

```
"How much USDT do I have?"
"Show my exchange balances"
```

---

### get\_open\_orders

List all pending (unfilled) orders across connected exchanges.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `symbol` | string | No | Filter by trading pair (e.g. `BTC/USDT`). Omit for all. |
| `exchangeCode` | string | No | Filter by exchange. Omit for all. |

#### Example

```
"Do I have any open orders?"
"Show my pending BTC orders"
```

---

### cancel\_order

Cancel a specific pending order on your exchange.

**Auth required:** Yes | **Endpoint:** `/v1/full` only | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `orderId` | string | Yes | The order ID (from `get_open_orders`) |
| `symbol` | string | Yes | Trading pair (e.g. `BTC/USDT`) |
| `exchangeCode` | string | No | Exchange code. Required if multiple exchanges connected. |
| `orderType` | string | No | `LIMIT`, `STOP_LOSS_LIMIT`, etc. (default: `LIMIT`) |

!!! warning "Safety"
    Cancels **real orders** on your exchange. Always use `get_open_orders` first to identify the correct order. Not available in guest mode.

---

## Support & Knowledge

### ask\_agent

Ask Anny's intelligent agent. Routes to Knowledge Agent (educational/how-to) or Support Agent (troubleshooting) automatically.

**Auth required:** No | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `question` | string | Yes | The question in natural language |
| `category` | string | No | Optional hint: `exchange`, `portfolio`, `billing`, `security`, `anny_line`, `tax`, `crypto_basics`, `trading_fundamentals`, `technical_analysis`, `anny_features`, `general` |

#### Example

```
"How do I connect my Binance account?"
"What is the CFO Line?"
```

---

### check\_user\_health

Diagnose the user's platform state — exchange connectivity, portfolio sync status, recent errors, known issues.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `component` | string | No | `exchange`, `portfolio`, `orders`, `anny_line`, or `all` (default: `all`) |

---

### create\_support\_ticket

Create a support ticket for an issue requiring human investigation. Auto-attaches diagnostics.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `category` | string | Yes | `incident`, `billing`, `security`, `exchange`, `data_issue`, `other` |
| `summary` | string | Yes | Brief summary (max 500 chars) |
| `userDescription` | string | No | User's own description |
| `priority` | string | No | `low`, `medium`, `high`, `critical` |
| `conversationContext` | string | No | Summary of conversation leading to ticket |

---

### get\_ticket\_status

Check status of support tickets. If no ticketId, returns user's recent open tickets.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `ticketId` | integer | No | Specific ticket ID. Omit for all recent tickets. |

---

### record\_resolution\_feedback

Record whether a support response resolved the user's issue. Trains the system to give better answers.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `helpful` | boolean | Yes | Whether the response resolved the issue |
| `resolutionId` | integer | No | ID of the referenced resolution |
| `feedbackNote` | string | No | Optional feedback text |

---

### claim\_welcome\_bonus

Grant a one-time 500-credit welcome bonus. Only call when user explicitly requests it.

**Auth required:** Yes | **Cost:** Free (grants credits)

#### Parameters

None.

---

### get\_exchange\_setup\_guide

Get step-by-step instructions for creating and configuring an API key on a specific exchange.

**Auth required:** No | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `exchange` | string | Yes | `binance`, `bybit`, `okx`, `gate_io`, `kraken`, `coinbase`, `kucoin` |
| `topic` | string | No | `create_api_key`, `permissions`, `ip_restrictions`, `troubleshooting`, `full_guide` |

---

## Skill System

### log\_skill\_gap

Log a capability gap when Anny cannot fulfill a request due to a missing feature.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `category` | string | Yes | `data_access`, `action`, `analysis`, `integration`, `alerts`, `trading`, `reporting`, `other` |
| `description` | string | Yes | Brief description of what the user wanted |

---

### submit\_skill\_request

Submit a structured skill request on behalf of the user (after explicit approval).

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `title` | string | Yes | Short title (max 200 chars) |
| `problem` | string | Yes | What problem does the user face? |
| `desiredCapability` | string | Yes | What capability would solve it? |
| `keyRequirements` | string | No | Must-have requirements |
| `niceToHave` | string | No | Nice-to-have additions |
| `categories` | array | No | Relevant categories |
| `gapCategory` | string | No | Gap category that triggered this |

---

### submit\_bug\_report

Submit a bug report on behalf of the user (after explicit approval). Auto-attaches diagnostics snapshot.

**Auth required:** Yes | **Cost:** Free

#### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `title` | string | Yes | Short title (max 200 chars) |
| `problem` | string | Yes | What is broken? |
| `stepsToReproduce` | string | No | Steps to reproduce |
| `expectedBehavior` | string | No | What was expected |
| `actualBehavior` | string | No | What actually happened |
| `severity` | string | No | `critical`, `major`, `minor`, `cosmetic` |

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
| `interval` | string | Optional: override interval for multi-timeframe |

---

## Safety Annotations

All tools include [MCP safety annotations](https://modelcontextprotocol.io/specification/draft/schema#toolannotations):

### Read-Only Tools

| Tool | readOnlyHint | destructiveHint | idempotentHint |
|------|:-----------:|:---------------:|:--------------:|
| get_technical_analysis | true | false | true |
| get_anny_line_status | true | false | true |
| get_flip_intelligence | true | false | true |
| compare_assets | true | false | true |
| get_institutional_intelligence | true | false | true |
| get_market_state | true | false | true |
| get_market_analysis | true | false | true |
| run_scenario | true | false | true |
| find_historical_pattern | true | false | true |
| get_tax_status | true | false | true |
| get_tax_holdings | true | false | true |
| get_signal | true | false | true |
| list_active_signals | true | false | true |
| get_signal_automation_config | true | false | true |
| analyze_signal_with_cfo | true | false | true |
| list_bots | true | false | true |
| get_bot_config | true | false | true |
| get_bot_fires | true | false | true |
| list_communities | true | false | true |
| get_community_pnl | true | false | true |
| run_cfo_line_backtest | true | false | true |
| run_optimizer | true | false | true |
| backtest_custom_strategy | true | false | true |
| scan_custom_signals | true | false | true |
| prescan_custom_strategy | true | false | true |
| optimize_custom_strategy | true | false | true |
| get_trading_idea_analysis | true | false | true |
| check_symbol_availability | true | false | true |
| get_exchange_balance | true | false | true |
| get_open_orders | true | false | true |
| ask_agent | true | false | false |
| check_user_health | true | false | true |
| get_ticket_status | true | false | true |
| get_exchange_setup_guide | true | false | true |

### Mutation Tools (DB-only)

| Tool | readOnlyHint | destructiveHint | idempotentHint |
|------|:-----------:|:---------------:|:--------------:|
| toggle_auto_invest | false | false | true |
| toggle_auto_stop | false | false | true |
| toggle_auto_sell | false | false | true |
| toggle_auto_trailing | false | false | true |
| update_signal_target | false | false | true |
| allocate_community_investment | false | false | true |
| create_bot_from_strategy | false | false | false |
| pause_bot | false | false | true |
| restart_bot | false | false | true |
| create_support_ticket | false | false | false |
| record_resolution_feedback | false | false | true |
| claim_welcome_bonus | false | false | true |
| log_skill_gap | false | false | true |
| submit_skill_request | false | false | false |
| submit_bug_report | false | false | false |

### Exchange-Mutation Tools (real exchange side-effects)

| Tool | readOnlyHint | destructiveHint | idempotentHint |
|------|:-----------:|:---------------:|:--------------:|
| cancel_pending_order | false | **true** | false |
| place_take_profit | false | **true** | false |
| place_trailing_stop | false | **true** | false |
| execute_market_order | false | **true** | false |
| cancel_order | false | **true** | false |

Exchange-mutation tools place or cancel **real orders** on your connected exchange. They are only available on the `/v1/full` endpoint (OAuth required) and are marked `destructiveHint: true`.

### Endpoint Split

| Endpoint | Tools | Auth Required | Directory Eligible |
|----------|-------|---------------|-------------------|
| `/v1` | Read-only + analysis + DB mutations | No (guest OK for public tools) | Yes |
| `/v1/full` | All tools incl. exchange mutations | OAuth required | No |
| `/mcp` | Alias for `/v1/full` | No (backward compat) | No |

Portfolio read tools (`check_symbol_availability`, `get_exchange_balance`, `get_open_orders`) require authentication but are available on both endpoints. Exchange mutation tools (`execute_market_order`, `cancel_order`, `cancel_pending_order`, `place_take_profit`, `place_trailing_stop`) are `/v1/full` only.

---

## Guest Tools

The following tools are available to unauthenticated (guest) visitors:

`get_technical_analysis`, `get_market_state`, `get_market_analysis`, `get_anny_line_status`, `get_flip_intelligence`, `get_exchange_setup_guide`, `ask_agent`, `get_trading_idea_analysis`, `compare_assets`, `get_institutional_intelligence`

All other tools require authentication.

For signal-specific tool documentation, see [Signal Tools](signals.md).
