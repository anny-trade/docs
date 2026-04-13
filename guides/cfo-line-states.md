# Understanding CFO Line States

The CFO Anny Line is a proprietary trend indicator that classifies market conditions into three distinct states based on price structure.

## The Three States

### Accumulate — Strength

**Color:** Teal green (`#3ca691`)

The asset is showing structural strength. Price structure is aligned in a way that indicates positive momentum and favorable conditions.

**What it means:** The underlying price dynamics are strong. Accumulate doesn't mean "buy" — it means the structural conditions are favorable.

### Wait — Neutral

**Color:** Muted purple-gray (`#6B6588`)

No clear directional bias. The asset is in a transitional or consolidating phase.

**What it means:** The indicator doesn't have a strong read. Wait periods often occur between state changes as the market structure reorganizes.

### Distribute — Weakness

**Color:** Violet purple (`#B767DE`)

The asset is showing structural weakness. Price structure indicates deteriorating conditions.

**What it means:** The underlying dynamics are weak. Distribute doesn't mean "sell" — it means the structural conditions are unfavorable.

## State Transitions

When the indicator changes state (e.g., Wait → Accumulate), this is called a **flip**. The `get_market_analysis` tool shows recent flips with dates and context explaining what changed in the price structure.

## Reading Across Timeframes

The CFO Line is available on three intervals:

| Interval | Best for |
|----------|----------|
| **1d** (Daily) | Macro trend. The primary timeframe. |
| **4h** (4-hour) | Medium-term momentum shifts. |
| **1h** (Hourly) | Short-term conditions. |

**Alignment** occurs when all timeframes show the same state (e.g., all Accumulate). This typically indicates a stronger, more reliable reading.

**Divergence** occurs when timeframes disagree (e.g., 1d Accumulate but 1h Distribute). This can indicate a pullback within an otherwise strong trend, or an early signal of a trend change.

## Important Notes

- The CFO Line is an **indicator**, not a recommendation. It describes market structure — it does not tell you what to do.
- Past indicator states do not predict future states.
- Always combine indicator readings with your own research and risk management.
