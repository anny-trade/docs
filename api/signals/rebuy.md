# Add Rebuy

```
POST /v1/signal/:parent_signal_id/call/rebuy
```

Add a rebuy zone to an existing signal — an additional entry point at a lower price to average down the position.

## Path Parameters

| Parameter | Description |
|-----------|-------------|
| `parent_signal_id` | Signal ID returned from create signal |

## Request Body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `parent_signal_id` | string | Yes | Signal ID (also in path) |
| `buy_price_min` | string | Yes | Rebuy zone lower bound |
| `buy_price_max` | string | Yes | Rebuy zone upper bound |
| `invest` | number | No | Investment percentage for the rebuy |
| `trailing_stop_price` | string | No | Optional trailing stop for the combined position |
| `trailing_stop_limit_price` | string | Conditional | Required if `trailing_stop_price` is set |

## Example

```bash
curl -X POST https://api.anny.trade/v1/signal/abc123/call/rebuy \
  -H "Content-Type: application/json" \
  -H "anny-api-key: YOUR_API_KEY" \
  -H "anny-api-secret: YOUR_API_SECRET" \
  -d '{
    "parent_signal_id": "abc123",
    "buy_price_min": "60000",
    "buy_price_max": "61000",
    "invest": 5,
    "trailing_stop_price": "58000",
    "trailing_stop_limit_price": "57500"
  }'
```
