---
title: Add DCA
parent: "Signal API (Partner)"
nav_order: 7
---

# Add DCA

```
POST /v1/signal/:parent_signal_id/call/dca
```

Add a Dollar-Cost Averaging (DCA) level to an existing signal.

## Path Parameters

| Parameter | Description |
|-----------|-------------|
| `parent_signal_id` | Signal ID returned from create signal |

## Request Body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `parent_signal_id` | string | Yes | Signal ID (also in path) |
| `buy_price` | string | Yes | DCA entry price |
| `multiplier` | number | Yes | Position size multiplier relative to original investment |

## Example

```bash
curl -X POST https://api.anny.trade/v1/signal/abc123/call/dca \
  -H "Content-Type: application/json" \
  -H "anny-api-key: YOUR_API_KEY" \
  -H "anny-api-secret: YOUR_API_SECRET" \
  -d '{
    "parent_signal_id": "abc123",
    "buy_price": "58000",
    "multiplier": 1.5
  }'
```

## How It Works

When the market drops to the `buy_price`, a new buy order is placed with a size of `original_investment * multiplier`. This averages down the entry price of the overall position.

For example, if the original signal invested 10% of the user's portfolio and the multiplier is 1.5, the DCA order invests 15%.
