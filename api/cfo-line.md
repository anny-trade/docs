---
title: CFO Anny Line
parent: API Reference
nav_order: 2
---

# CFO Anny Line

Get the current indicator state and recent transitions for any crypto asset.

## Get Indicator State

```
POST /backend/anny-line/chart
```

### Request Body

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `asset` | string | Yes | — | Crypto symbol: `BTC`, `ETH`, `SOL` |
| `interval` | string | No | `1d` | Chart interval: `1d`, `4h`, `1h` |
| `tradeMarket` | string | No | `USDT` | Quote currency |

### Example

```bash
curl -X POST https://api.anny.trade/backend/anny-line/chart \
  -H "Content-Type: application/json" \
  -d '{"asset": "BTC", "interval": "1d", "tradeMarket": "USDT"}'
```

### Response

Returns the current CFO Anny Line state and chart data. The state is one of:

| State | Meaning |
|-------|---------|
| `accumulate` | `#3ca691` (teal green) — the asset is showing structural strength |
| `wait` | `#6B6588` (muted purple-gray) — no clear directional bias |
| `distribute` | `#B767DE` (violet purple) — the asset is showing structural weakness |

---

## Get Transition Context (Flip Intelligence)

```
POST /backend/anny-line/flip-intelligence
```

Returns context on *why* the indicator changed state — what happened in the price structure that triggered the transition.

### Request Body

Same as `/backend/anny-line/chart`.

### Example

```bash
curl -X POST https://api.anny.trade/backend/anny-line/flip-intelligence \
  -H "Content-Type: application/json" \
  -d '{"asset": "ETH", "interval": "4h", "tradeMarket": "USDT"}'
```

### Response

Returns recent state transitions with dates and context explaining each change.

---

## Portfolio-Wide States

```
POST /backend/anny-line/portfolio
```

**Auth required:** Yes

Returns the CFO Anny Line state for all assets in your portfolio at once.

### Request Body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `exchange` | string | No | Filter to a specific exchange: `BINANCE`, `BYBIT` |

### Example

```bash
curl -X POST https://api.anny.trade/backend/anny-line/portfolio \
  -H "Content-Type: application/json" \
  -H "session-token: <your-token>" \
  -d '{}'
```

### Response

Returns an array of states for each asset in your portfolio:

```json
{
  "result": { "type": "OPERATION_PERFORMED" },
  "payload": {
    "states": [
      { "asset": "BTC", "state": "accumulate", "price": 68500.00 },
      { "asset": "ETH", "state": "wait", "price": 3850.00 },
      { "asset": "SOL", "state": "distribute", "price": 145.20 }
    ]
  }
}
```
