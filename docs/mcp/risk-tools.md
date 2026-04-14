# Risk & Position Management

Tools for sizing positions, setting stops, assessing trade risk, and stress-testing your portfolio against hypothetical scenarios.

---

## calculate\_position\_size

Calculate the optimal position size for a trade based on risk management rules.

**Auth required:** No

Supports two sizing methods:

- **Fixed Fractional** -- risk a fixed percentage of your account per trade (default 2%).
- **Kelly Criterion** -- mathematically optimal sizing based on your historical edge. Uses Half-Kelly (industry standard) to reduce volatility.

### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `account_balance` | number | Yes | — | Total account balance in USD |
| `entry_price` | number | Yes | — | Planned entry price |
| `stop_loss_price` | number | Yes | — | Stop-loss price level |
| `risk_percent` | number | No | `2` | Max percentage of account to risk per trade (0.1–100) |
| `method` | string | No | `fixed_fractional` | Sizing method: `fixed_fractional` or `kelly` |
| `win_rate` | number | No | — | Historical win rate as a percentage (required for Kelly) |
| `avg_win_loss_ratio` | number | No | — | Average win / average loss ratio (required for Kelly) |
| `leverage` | number | No | `1` | Leverage multiplier (1–125, where 1 = no leverage) |

### Example

```
"I have $10,000 and want to buy BTC at $65,000 with a stop at $62,000.
How much should I buy?"
```

### Response

Returns a formatted breakdown including:

- **Trade Parameters** -- account balance, entry price, stop-loss, risk per unit, risk budget
- **Position Size** -- risk amount in USD, position size in units and USD, portfolio allocation percentage
- **Leverage details** (when leverage > 1) -- leveraged exposure, margin required, estimated liquidation distance
- **Kelly Analysis** (when method is `kelly`) -- full Kelly fraction, Half-Kelly used, expected value per dollar risked

Example output:

```
## Position Size Calculator

**Direction:** Long
**Method:** Fixed Fractional

### Trade Parameters

| Parameter | Value |
|-----------|-------|
| Account Balance | $10,000.00 |
| Entry Price | $65,000.00 |
| Stop-Loss | $62,000.00 |
| Risk per Unit | $3,000.00 (4.62%) |
| Risk Budget | 2.00% of account |

### Position Size

| Metric | Value |
|--------|-------|
| Risk Amount | $200.00 |
| Position Size | 0.066667 units |
| Position Value | $4,333.33 |
| Portfolio Allocation | 43.3% |
```

---

## calculate\_stop\_loss

Calculate optimal stop-loss and take-profit levels for a crypto trade using three independent models.

**Auth required:** No

The tool fetches OHLC data automatically from the exchange and runs the calculation through three models:

1. **Volatility (ATR)** -- stop based on Average True Range multiplied by a configurable factor
2. **Structure** -- stop based on recent swing highs/lows with a buffer
3. **Regime (Adaptive)** -- selects the best model based on trend vs. range detection

### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `asset` | string | Yes | — | Crypto asset symbol (e.g. `BTC`, `ETH`, `SOL`) |
| `entry_price` | number | Yes | — | Your entry price for the trade |
| `direction` | string | No | `long` | Trade direction: `long` or `short` |
| `interval` | string | No | `1d` | Candle interval: `1h`, `4h`, or `1d` |
| `atr_multiplier` | number | No | `1.5` | ATR multiplier for the volatility-based stop (0.5–5) |

### Example

```
"Where should I set my stop-loss if I buy ETH at $3,200?"
```

### Response

Returns:

- **Market Context** -- market state (trending/ranging/volatile), ADX trend strength and direction, ATR value
- **Stop-Loss Levels** -- one level per model (Volatility, Structure, Regime) with a recommended stop-loss and risk percentage
- **Take-Profit Targets** -- levels at 1.5:1, 2:1, and 3:1 risk-reward ratios, plus a structure-based target from swing levels, with a recommended take-profit

If risk exceeds 5%, the response includes a warning to consider reducing position size.

Example output:

```
## ETH — Stop-Loss & Take-Profit Levels

### Market Context

| Metric | Value |
|--------|-------|
| Market State | Trending |
| Trending | Yes |
| Trend Strength | Strong |
| Trend Direction | Up |
| ADX (14) | 32.5 |
| ATR (14) | $125.40 |

### Stop-Loss Levels

| Model | Level | Method |
|-------|-------|--------|
| Volatility (ATR) | $3,011.90 | ATR x multiplier |
| Structure | $2,980.00 | Swing high/low + buffer |
| Regime (Adaptive) | $3,011.90 | Trend-aware selection |

**Recommended Stop-Loss:** $3,011.90 (5.88% risk)

### Take-Profit Targets

| R:R | Level |
|-----|-------|
| 1.5:1 | $3,482.15 |
| 2:1 | $3,576.20 |
| 3:1 | $3,764.30 |
| Structure | $3,650.00 |

**Recommended Take-Profit:** $3,576.20
```

---

## assess\_trade\_risk

Assess the technical risk of entering a trade on a specific crypto asset.

**Auth required:** No (authenticated users may receive enhanced context)

Runs technical analysis including RSI, ADX, MACD, volume analysis, and trend detection to evaluate whether current conditions favor the intended trade direction.

### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `asset` | string | Yes | — | Crypto asset symbol (e.g. `BTC`, `ETH`, `SOL`) |
| `direction` | string | No | `long` | Trade direction: `long` or `short` |
| `trade_market` | string | No | `USDT` | Quote currency |
| `exchange` | string | No | `BINANCE` | Exchange for price data |
| `account` | string | No | `SPOT` | Account type: `SPOT` or `FUTURES` |

### Example

```
"Should I go long on SOL right now?"
"What's the risk of shorting BTC?"
```

### Response

Returns:

- **Indicator table** -- RSI (with oversold/overbought signal), ADX (trend strength), MACD, volume, and trend direction
- **Overall assessment** -- a recommendation based on the combined indicators

Example output:

```
## SOL — Trade Risk Assessment (LONG)

| Indicator | Value | Signal |
|-----------|-------|--------|
| RSI (14) | 42.3 | Neutral |
| ADX | 28.7 | Strong trend |
| MACD | 0.0245 | Bullish crossover |
| Volume | Above average | Confirming |
| Trend | Up | Moderate |

**Assessment:** Conditions moderately favor a long entry.
RSI is neutral with room to run, trend is intact, and volume confirms.
```

---

## simulate\_scenario

Simulate how your portfolio would be affected by a hypothetical market scenario.

**Auth required:** Yes

Accepts natural language scenario descriptions and projects the impact on your current holdings. The engine parses the scenario into price movements and applies them to your portfolio.

### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `scenario` | string | Yes | — | Free-text scenario description (3–500 characters) |

Valid scenario examples:

- `"BTC drops 30%"`
- `"ETH doubles in price"`
- `"Full market crash like 2022"`
- `"Bitcoin hits $100,000"`
- `"All altcoins drop 50%"`

### Example

```
"What happens to my portfolio if BTC crashes 40%?"
```

### Response

Returns:

- **Portfolio Impact** -- current value, projected value, total impact in USD and percentage
- **Per-Asset Impact** -- table showing each holding with current value, projected value, and percentage change
- **Analysis** -- narrative summary of how the scenario would affect your overall portfolio

Example output:

```
## Scenario Simulation

**Scenario:** BTC drops 40%

### Portfolio Impact

| Metric | Value |
|--------|-------|
| Current Value | $25,400.00 |
| Projected Value | $18,120.00 |
| Impact | -28.66% |
| Impact (USD) | -$7,280.00 |

### Per-Asset Impact

| Asset | Current | Projected | Change |
|-------|---------|-----------|--------|
| BTC | $15,000.00 | $9,000.00 | -40.00% |
| ETH | $6,400.00 | $5,440.00 | -15.00% |
| SOL | $2,800.00 | $2,520.00 | -10.00% |
| USDT | $1,200.00 | $1,200.00 | +0.00% |

### Analysis

Your portfolio is heavily weighted toward BTC (59%), making it
highly sensitive to this scenario. Consider diversifying or
hedging your BTC exposure.
```

---

## Safety Annotations

| Tool | readOnlyHint | destructiveHint | idempotentHint |
|------|-------------|-----------------|----------------|
| calculate_position_size | true | false | true |
| calculate_stop_loss | true | false | true |
| assess_trade_risk | true | false | true |
| simulate_scenario | true | false | true |

All four tools are read-only and never modify your account. `calculate_position_size` is a pure calculation that runs entirely client-side. The other three fetch live market data but make no changes.
