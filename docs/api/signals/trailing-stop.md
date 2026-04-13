# Add Trailing Stop

```
POST /v1/signal/:parent_signal_id/call/trailingstop
```

Add a trailing stop-loss to an existing signal.

## Path Parameters

| Parameter | Description |
|-----------|-------------|
| `parent_signal_id` | Signal ID returned from create signal |

## Request Body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `parent_signal_id` | string | Yes | Signal ID (also in path) |
| `trailing_stop_price` | string | Yes | Stop trigger price (must be > 0) |
| `trailing_stop_limit_price` | string | Yes | Limit price for the stop order (must be > 0) |

## Example

```bash
curl -X POST https://api.anny.trade/v1/signal/abc123/call/trailingstop \
  -H "Content-Type: application/json" \
  -H "anny-api-key: YOUR_API_KEY" \
  -H "anny-api-secret: YOUR_API_SECRET" \
  -d '{
    "parent_signal_id": "abc123",
    "trailing_stop_price": "64000",
    "trailing_stop_limit_price": "63500"
  }'
```

## How It Works

- **Stop price:** When the market drops to this level, the stop order is triggered
- **Limit price:** The minimum price at which the stop order will execute
- The stop trails upward as price rises — it only moves up, never down
