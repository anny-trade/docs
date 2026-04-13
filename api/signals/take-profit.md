# Add Take Profit

```
POST /v1/signal/:parent_signal_id/call/takeprofit
```

Add a take-profit target to an existing signal. If selling less than 100% of the position, a trailing stop is required for the remaining portion.

## Path Parameters

| Parameter | Description |
|-----------|-------------|
| `parent_signal_id` | Signal ID returned from create signal |

## Request Body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `parent_signal_id` | string | Yes | Signal ID (also in path) |
| `order_type` | string | Yes | `limit` or `market` |
| `sell_price` | string | Conditional | Required if `order_type` is `limit` |
| `sell_amount_relative` | number | Yes | Percentage of position to sell (1–100) |
| `symbol` | string | No | Trading pair symbol |
| `trailing_stop_price` | string | Conditional | Required if `sell_amount_relative` < 100 |
| `trailing_stop_limit_price` | string | Conditional | Required if `sell_amount_relative` < 100 |

## Example — Sell 50% at Limit

```bash
curl -X POST https://api.anny.trade/v1/signal/abc123/call/takeprofit \
  -H "Content-Type: application/json" \
  -H "anny-api-key: YOUR_API_KEY" \
  -H "anny-api-secret: YOUR_API_SECRET" \
  -d '{
    "parent_signal_id": "abc123",
    "order_type": "limit",
    "sell_price": "72000",
    "sell_amount_relative": 50,
    "trailing_stop_price": "68000",
    "trailing_stop_limit_price": "67500"
  }'
```

## Example — Sell 100% at Market

```bash
curl -X POST https://api.anny.trade/v1/signal/abc123/call/takeprofit \
  -H "Content-Type: application/json" \
  -H "anny-api-key: YOUR_API_KEY" \
  -H "anny-api-secret: YOUR_API_SECRET" \
  -d '{
    "parent_signal_id": "abc123",
    "order_type": "market",
    "sell_amount_relative": 100
  }'
```
