---
title: Scenario Analysis
parent: API Reference
nav_order: 4
---

# Scenario Analysis

Run a historical scenario analysis to see how the CFO Anny Line indicator readings corresponded with price movements over a given period.

## Run Analysis

```
POST /backend/anny-line/backtest
```

**Auth required:** Yes

### Request Body

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `asset` | string | Yes | — | Crypto symbol: `BTC`, `ETH`, `SOL` |
| `interval` | string | No | `1d` | Candle interval: `1d`, `4h`, `1h` |
| `period` | string | No | `1y` | Lookback: `3M`, `6M`, or `1y` |
| `tradeMarket` | string | No | `USDT` | Quote currency |

### Example

```bash
curl -X POST https://api.anny.trade/backend/anny-line/backtest \
  -H "Content-Type: application/json" \
  -H "session-token: <your-token>" \
  -d '{
    "asset": "BTC",
    "interval": "1d",
    "period": "1y",
    "tradeMarket": "USDT"
  }'
```

### Response

```json
{
  "result": { "type": "OPERATION_PERFORMED" },
  "payload": {
    "totalReturn": 45.2,
    "winRate": 62.5,
    "sharpe": 1.8,
    "maxDrawdown": -15.3,
    "tradeCount": 24,
    "profitFactor": 2.1,
    "trades": [
      {
        "entryPrice": 50000,
        "exitPrice": 55000,
        "entryDate": "2025-06-01",
        "exitDate": "2025-07-01",
        "return": 10.0
      }
    ]
  }
}
```

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `totalReturn` | number | Total return (%) |
| `winRate` | number | Percentage of positive entries |
| `sharpe` | number | Sharpe ratio |
| `maxDrawdown` | number | Maximum drawdown (%) |
| `tradeCount` | number | Total number of entries |
| `profitFactor` | number | Gross profit / gross loss |
| `trades` | array | Individual entries with prices, dates, and returns |

### Timing

Computation is done in real-time. Expect 10–30 seconds for longer periods (1y) on lower intervals (1h). The request will time out after 60 seconds.

### Disclaimer

Results are historical and informational. Past performance does not indicate future results.
