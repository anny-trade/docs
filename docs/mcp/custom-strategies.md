# Custom Strategy Builder

Build, test, and deploy your own trading strategies using technical indicators — all through natural conversation.

## How It Works

Define your strategy as a set of rules:

1. **Trigger** — the event that fires an entry signal (e.g., RSI crosses below 30)
2. **Confirmations** — conditions that must also be true (e.g., price above EMA 200)
3. **Stop-loss & take-profit** — risk management rules applied to every trade

Anny backtests your rules against real historical data, shows you the results, and can deploy the strategy as a live bot on your connected exchange.

## Supported Indicators

| Indicator | Fields | Key Parameters |
|-----------|--------|----------------|
| **RSI** | `value` | `period` (default: 14) |
| **EMA** | `value` | `period` (default: 20) |
| **SMA** | `value` | `period` (default: 20) |
| **MACD** | `macd`, `signal`, `histogram` | `fast` (12), `slow` (26), `signal` (9) |
| **ADX** | `value`, `plus_di`, `minus_di` | `period` (default: 14) |
| **ATR** | `value` | `period` (default: 14) |
| **BBANDS** | `upper`, `middle`, `lower` | `period` (20), `stddev` (2) |
| **STOCHRSI** | `k`, `d` | `period` (14), `k` (3), `d` (3) |

You can also use `PRICE` to reference raw candle data (`open`, `high`, `low`, `close`, `volume`).

## Operators

| Operator | Use As | Meaning |
|----------|--------|---------|
| `crosses_above` | Trigger | Value just crossed above threshold (state change) |
| `crosses_below` | Trigger | Value just crossed below threshold (state change) |
| `above` | Confirmation | Value is currently above threshold |
| `below` | Confirmation | Value is currently below threshold |

Triggers detect **transitions** — they fire once when the condition changes from false to true. Confirmations are **persistent** — they're checked continuously.

## Multi-Timeframe

Each condition can reference a different timeframe. For example, use a 4-hour trigger with a daily confirmation:

> "Backtest a strategy on ETH 4h where EMA(9) crosses above EMA(21), but only when the daily RSI is above 50"

Anny aligns the timeframes automatically using forward-fill mapping, so higher-timeframe conditions always reflect the most recent completed candle — no look-ahead bias.

## Risk Management

### Stop-Loss Types

| Type | Description |
|------|-------------|
| **Percent** | Fixed percentage from entry (e.g., 3%) |
| **ATR** | Multiplier of ATR(14) at entry (e.g., 2x ATR) |
| **Structure** | Based on recent support/resistance levels |
| **Regime** | Adapts to current market volatility regime |

### Take-Profit Types

| Type | Description |
|------|-------------|
| **Percent** | Fixed percentage target (e.g., 8%) |
| **Risk/Reward** | Multiple of stop-loss distance (e.g., 2:1 R:R) |

## Available Tools

### backtest\_custom\_strategy

Test your strategy against historical data. Returns performance metrics, trade history, equity curve, and current signal status.

- **Cost:** 5 credits
- **Lookback periods:** 3M, 6M, 1y

### scan\_custom\_signals

Check if your strategy conditions are met right now against live market data.

- **Cost:** Free (0 credits)
- **Returns:** Current indicator values, which conditions are met, signal status (ACTIVE / APPROACHING / INACTIVE)

### deploy\_strategy\_as\_bot

Deploy a tested strategy as a live trading bot on your connected exchange. The bot is created **paused** — you activate it manually from the dashboard.

- **Requires:** Connected exchange account
- **Creates:** A new bot with your strategy rules, stop-loss, and take-profit settings

### get\_bot\_strategy

Retrieve the strategy definition attached to an existing custom strategy bot.

### update\_strategy\_config

Modify the strategy rules on an existing bot (while paused).

## What the Backtest Shows

| Section | What It Contains |
|---------|------------------|
| **Strategy Rules** | Echo of your trigger, confirmations, direction, stop-loss, take-profit |
| **Performance** | Total return, win rate, profit factor, Sharpe ratio, max drawdown, avg hold |
| **Train/Test Split** | In-sample (80%) vs out-of-sample (20%) metrics with overfit detection |
| **Warnings** | Statistical significance flags (< 10 trades = meaningless, < 30 = low) |
| **Price Context** | Current price vs SMA(200), Bollinger Band position, ATR percentile, support/resistance |
| **Volume Context** | Relative volume, OBV direction, volume-confirmed win rates |
| **Trades** | Entry/exit prices, dates, hold duration, return, exit reason |
| **Signal Status** | Whether conditions are met right now (ACTIVE / APPROACHING / INACTIVE) |

## Transaction Costs

Backtests include realistic costs:

- **Fee:** 0.1% per side (taker)
- **Slippage:** 0.1% for major assets (BTC, ETH, SOL, BNB, XRP, ADA, DOGE, AVAX), 0.3% for alts
- **Entry:** at next bar's open (no look-ahead)
- **SL priority:** when both stop-loss and take-profit hit in the same bar, stop-loss wins (pessimistic)

## Typical Workflow

```
1. Scan     → "Check if RSI is below 30 on BTC right now"
2. Backtest → "Backtest buying BTC when RSI crosses below 30
               with price above EMA(200), 3% stop, 2:1 R:R"
3. Iterate  → "Try it with RSI 25 instead" / "Add ADX > 25 confirmation"
4. Deploy   → "Deploy this strategy as a bot on Binance SPOT with $200"
5. Monitor  → "What's the strategy on bot abc123?"
6. Update   → "Change the stop-loss to 4%"
```

!!! warning "Important"
    Results are hypothetical and simulated. Past performance does not indicate future results. Signal status of ACTIVE means your conditions are met — it is not a recommendation to trade. Bots are always created paused. This is not financial advice.
