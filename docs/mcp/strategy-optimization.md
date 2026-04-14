# Strategy Optimization

Anny offers two optimization tools that help you refine your CFO Line settings and stress-test strategies against unseen market conditions. Use them together: first **optimize** to find better filter settings, then **stress test** to validate those settings aren't overfit.

Both tools work on Anny's proprietary CFO Line indicator — they tune the filters that decide when to enter and exit trades based on CFO Line signals.

---

## optimize\_strategy

Diagnose why the CFO Line is losing money on a specific asset and find filter settings that eliminate those losses. The optimizer runs 15-20 filter configurations against historical CFO Line signals, categorizes every losing trade by root cause (whipsaw, weak conviction, counter-trend, revenge trade), and prescribes filter adjustments to fix each one.

!!! note "Beta"
    This feature is in beta. Results are experimental and should be validated before applying filter settings to a live bot.

- **Auth required:** Yes
- **Cost:** 900 credits
- **Minimum tier:** PRO or Pro Max

### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `asset` | string | Yes | — | Crypto asset symbol (e.g. `BTC`, `ETH`, `SOL`) |
| `period` | string | No | `1y` | Lookback period: `3M`, `6M`, or `1y` |
| `interval` | string | No | `1d` | Candle interval: `1h`, `1d`, or `1w` |
| `mode` | string | No | `long` | Trading mode: `long`, `long_short`, or `short` |

### Examples

Try prompts like:

- *"Optimize BTC on the daily chart"*
- *"Why is my ETH strategy losing? Diagnose it over 6 months"*
- *"Find better CFO Line settings for SOL on the 1-hour chart, long and short"*

### Response

The optimizer returns four sections:

**Performance Comparison** — side-by-side metrics for the baseline (raw CFO Line, no filters) vs the optimized configuration:

| Metric | Baseline | Optimized |
|--------|----------|-----------|
| Total Return | +12.45% | +31.20% |
| Win Rate | +42.00% | +61.50% |
| Sharpe Ratio | 0.85 | 1.42 |
| Max Drawdown | -18.30% | -9.70% |
| Total Trades | 47 | 28 |
| Profit Factor | 1.15 | 2.10 |
| Avg Hold Days | 3.20 | 5.80 |

**Loss Diagnosis** — categorizes every losing trade by root cause:

- **Whipsaw**: 8 trades (filter: Confirmation Candles)
- **Weak Conviction**: 5 trades (filter: Spread Threshold %)
- **Counter Trend**: 4 trades (filter: Trend SMA)
- **Revenge Trade**: 3 trades (filter: Cooldown Candles)

**Recommended Filters** — the specific settings to apply:

| Filter | Value |
|--------|-------|
| Confirmation Candles | 3 |
| Spread Threshold % | 1.5 |
| Trend SMA | 200 |
| Cooldown Candles | 4 |
| ATR Period | 14 |
| ATR Multiplier | 2.5 |
| Equity Curve SMA | 20 |

**Strategy label** — a summary name for the winning configuration.

### How to Interpret Results

- **Total Return improvement** shows how much the filters helped overall. Look for meaningful gains, not marginal ones.
- **Win Rate going up + Total Trades going down** is normal — filters remove bad trades, which raises the win rate but reduces trade count.
- **Profit Factor** above 1.5 is solid; above 2.0 is strong. Below 1.0 means the strategy is losing money.
- **Sharpe Ratio** measures risk-adjusted return. Above 1.0 is acceptable; above 1.5 is good.
- **Max Drawdown** getting smaller means the filters are protecting capital during adverse moves.
- **Loss Diagnosis** tells you *why* you were losing — use this to understand the market behavior, not just to apply the fix blindly.
- Apply the recommended filters when creating or updating a trading bot in the Anny Trade app.

---

## stress\_test\_strategy

Validate whether optimized CFO Line settings hold up on unseen data using walk-forward analysis. This detects overfitting — if the optimizer found settings that only work on the data they were tuned to, the stress test will expose it.

Walk-forward analysis splits historical data into rolling windows (4+ minimum). For each window, it optimizes filters on the in-sample portion and then tests them on unseen out-of-sample data. A robust strategy shows consistent performance across all windows.

!!! warning "Coming Soon"
    This tool is currently under development. The endpoint is registered but returns a "coming soon" message. Use `optimize_strategy` in the meantime.

- **Auth required:** Yes
- **Cost:** 1,800 credits
- **Minimum tier:** PRO or Pro Max

### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `asset` | string | Yes | — | Crypto asset symbol (e.g. `BTC`, `ETH`, `SOL`) |
| `period` | string | No | `1y` | Lookback period: `3M`, `6M`, or `1y` |
| `interval` | string | No | `1d` | Candle interval: `1h`, `1d`, or `1w` |

### Examples

Try prompts like:

- *"Stress test my BTC strategy"*
- *"Run walk-forward analysis on ETH over 1 year"*
- *"Are my SOL optimization results overfit?"*

### Response

The stress test returns four sections:

**Confidence Score** — a single number from 0 to 100 summarizing how robust the strategy is. Higher is better.

**Out-of-Sample Performance** — aggregate metrics across all out-of-sample windows:

| Metric | Value |
|--------|-------|
| Total Return | +18.50% |
| Win Rate | +55.00% |
| Sharpe Ratio | 1.10 |
| Max Drawdown | -12.40% |
| Total Trades | 34 |
| Profit Factor | 1.65 |

**Rolling Windows** — per-window breakdown showing in-sample vs out-of-sample performance:

| Window | IS Return | OOS Return | Decay | Status |
|--------|-----------|------------|-------|--------|
| Q1 2025 | +14.20% | +11.30% | 0.80 | Pass |
| Q2 2025 | +9.80% | +6.10% | 0.62 | Pass |
| Q3 2025 | +18.50% | +3.20% | 0.17 | Fail |
| Q4 2025 | +11.00% | +8.90% | 0.81 | Pass |

**Regime Analysis** — detects whether market conditions have shifted since the optimization:

- **Current regime:** e.g. "Trending bullish" or "Range-bound"
- **Regime shift detected:** whether conditions changed between windows
- **Recommended adaptation:** what to adjust if the regime has changed

### How to Interpret Results

- **Confidence Score** above 70 means the strategy is likely robust. Below 50 suggests overfitting.
- **Decay ratio** (OOS Return / IS Return) measures how well each window's optimized settings transferred to unseen data. Values near 1.0 are ideal — the settings worked almost as well on new data. Below 0.3 is a fail.
- **Pass/Fail** per window: OOS must retain at least 30% of the IS return to pass. Negative OOS always fails. A single failed window is a warning; multiple failures mean the optimization is not reliable.
- **Regime Analysis** helps explain *why* a window failed — if the market shifted from trending to ranging mid-test, poor OOS performance may reflect regime change rather than overfitting.
- If most windows fail, do not trust the optimizer's filter recommendations. Consider using a different lookback period or interval.

---

## Recommended Workflow

```
1. Optimize  → "Optimize BTC on the daily chart"
2. Review    → Check the loss diagnosis and recommended filters
3. Validate  → "Stress test my BTC strategy"       (coming soon)
4. Apply     → Set the recommended filters on your bot
5. Monitor   → Re-run periodically to check for regime shifts
```

!!! warning "Important"
    Results are hypothetical and simulated. Past performance does not indicate future results. Filter recommendations are based on historical data and may not perform the same way in live markets. This is not financial advice.
