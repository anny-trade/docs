# Update Prices

```
PUT /v1/signal/:parent_signal_id/updateprice
```

Update entry prices, take-profit targets, or stop-loss on an existing signal.

## Path Parameters

| Parameter | Description |
|-----------|-------------|
| `parent_signal_id` | Signal ID returned from create signal |

## Request Body

All fields are optional — include only the prices you want to update.

| Field | Type | Description |
|-------|------|-------------|
| `parent_signal_id` | string | Signal ID (also in path) |
| `entry_price_min` | string | New entry range lower bound |
| `entry_price_max` | string | New entry range upper bound |
| `exit_price_1` | string | New take profit target 1 |
| `exit_price_2` | string | New take profit target 2 |
| `exit_price_3` | string | New take profit target 3 |
| `exit_price_4` | string | New take profit target 4 |
| `exit_price_5` | string | New take profit target 5 |
| `exit_price_6` | string | New take profit target 6 |
| `stop_loss` | string | New stop-loss price |

## Example

```bash
curl -X PUT https://api.anny.trade/v1/signal/abc123/updateprice \
  -H "Content-Type: application/json" \
  -H "anny-api-key: YOUR_API_KEY" \
  -H "anny-api-secret: YOUR_API_SECRET" \
  -d '{
    "parent_signal_id": "abc123",
    "exit_price_1": "73000",
    "stop_loss": "63000"
  }'
```
