# Cancel Signal

```
DELETE /v1/signal/:parent_signal_id/cancel
```

Cancel an existing signal. If the signal has open positions, they will be closed.

## Path Parameters

| Parameter | Description |
|-----------|-------------|
| `parent_signal_id` | Signal ID returned from create signal |

## Request Body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `parent_signal_id` | string | Yes | Signal ID (also in path) |

## Example

```bash
curl -X DELETE https://api.anny.trade/v1/signal/abc123/cancel \
  -H "Content-Type: application/json" \
  -H "anny-api-key: YOUR_API_KEY" \
  -H "anny-api-secret: YOUR_API_SECRET" \
  -d '{"parent_signal_id": "abc123"}'
```

## Response

```json
{
  "result": { "type": "OPERATION_PERFORMED" },
  "payload": {
    "result": "success"
  }
}
```
