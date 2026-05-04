# Strategy Optimization

Anny offers two optimization tools for refining your CFO Line settings. Use them together: first **optimize** to find better filter settings, then **stress test** to validate.

Both tools work on Anny's proprietary CFO Line indicator — they tune the filters that decide when to enter and exit trades.

---

## run\_optimizer

Diagnose why the CFO Line is losing money on a specific asset and find filter settings that eliminate those losses. The optimizer runs 15–20 filter configurations, categorizes every losing trade by root cause, and prescribes filter adjustments.

!!! note "Beta"
    This feature is in beta. Results are experimental and should be validated before applying filter settings to a live bot.

- **Auth required:** Yes
- **Cost:** 900 credits
- **Minimum tier:** PRO or Pro Max

### Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `asset` | string | Yes | — | Crypto asset symbol (e.g. `BTC`, `ETH`, `SOL`) |
| `period` | string | No | `1y` | Lookback period: `3m`, `6m`, `9m`, or `1y` |
| `interval` | string | No | `1d` | Candle interval: `1h`, `4h`, `1d`, or `1w` |
| `mode` | string | No | `long` | Trading mode: `long`, `long_short`, or `short` |

### Examples

- *"Optimize BTC on the daily chart"*
- *"Why is my ETH strategy losing? Diagnose it over 6 months"*
- *"Find better CFO Line settings for SOL on the 1-hour chart, long and short"*

### Response

Returns four sections:

**Performance Comparison** — baseline (raw CFO Line) vs optimized:

| Metric | Baseline | Optimized |
|--------|----------|-----------|
| Total Return | +12.45% | +31.20% |
| Win Rate | +42.00% | +61.50% |
| Sharpe Ratio | 0.85 | 1.42 |
| Max Drawdown | -18.30% | -9.70% |

**Loss Diagnosis** — categorizes every losing trade:

- **Whipsaw**: filter → Confirmation Candles
- **Weak Conviction**: filter → Spread Threshold %
- **Counter Trend**: filter → Trend SMA
- **Revenge Trade**: filter → Cooldown Candles

**Recommended Filters** — the specific settings to apply.

**Strategy label** — summary name for the winning configuration.

---

## Stress Test (Coming Soon)

Walk-forward analysis to validate whether optimized settings hold up on unseen data. Detects overfitting by splitting data into rolling windows and testing out-of-sample performance.

- **Cost:** 1,800 credits
- **Minimum tier:** PRO or Pro Max

This tool is under development. Use `run_optimizer` in the meantime.

---

## Recommended Workflow

```
1. Backtest  → "Backtest the CFO Line on BTC daily"
2. Optimize  → "Optimize BTC on the daily chart"
3. Review    → Check loss diagnosis and recommended filters
4. Validate  → "Stress test my BTC strategy"       (coming soon)
5. Apply     → Set recommended filters on your bot
6. Monitor   → Re-run periodically for regime shifts
```

!!! warning "Important"
    Results are hypothetical and simulated. Past performance does not indicate future results. Filter recommendations are based on historical data and may not perform the same way in live markets. This is not financial advice.
