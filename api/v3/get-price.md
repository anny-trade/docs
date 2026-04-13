# Get Price

```
GET /v3/ai/get_price
POST /v3/ai/get_price
```

Retrieves the latest spot price for a cryptocurrency trading pair.

**Rate limit:** 100 requests/minute per IP

## Authentication

Same as [Assess Risk](assess-risk.md) — HMAC-SHA256 or ChatGPT User-Agent bypass.

## Parameters

| Name | In | Type | Required | Default | Description |
|------|----|------|----------|---------|-------------|
| `base_asset` | query | string | Yes | — | Base asset symbol: `BTC`, `ETH`, `SOL` |
| `quote_asset` | query | string | No | `USDT` | Quote asset symbol |

## Example

```bash
curl "https://api.anny.trade/v3/ai/get_price?base_asset=ETH&quote_asset=USDT"
```

## Response

```json
{
  "base_asset": "ETH",
  "quote_asset": "USDT",
  "symbol": "ETH/USDT",
  "price": "3850.42",
  "timestamp": "2026-04-13T12:30:00.000Z"
}
```

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `base_asset` | string | The base cryptocurrency symbol |
| `quote_asset` | string | The quote asset symbol |
| `symbol` | string | Full trading pair (e.g., `ETH/USDT`) |
| `price` | string | Spot price (string for decimal precision) |
| `timestamp` | string | ISO 8601 UTC timestamp |
