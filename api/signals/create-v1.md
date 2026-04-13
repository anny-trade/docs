---
title: "Create Signal (V1)"
parent: "Signal API (Partner)"
nav_order: 2
---

# Create Signal (V1)

```
POST /v1/signal
```

Create a new trading signal with entry range, up to 6 take-profit targets, and optional stop-loss.

## Request Body

You can send either a **structured object** or a **pre-formatted text** signal.

### Option A: Structured Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `coin` | string | Yes | Asset symbol: `BTC`, `ETH`, `SOL` |
| `trade_market` | string | Yes | Quote currency: `USDT`, `BTC` |
| `exchange` | string | Yes | Exchange: `BINANCE`, `BYBIT`, `OKX` |
| `buy_price_min` | string | Yes | Entry price range — lower bound |
| `buy_price_max` | string | Yes | Entry price range — upper bound |
| `sell_price_1` | string | Yes | Take profit target 1 |
| `sell_price_2` | string | No | Take profit target 2 |
| `sell_price_3` | string | No | Take profit target 3 |
| `sell_price_4` | string | No | Take profit target 4 |
| `sell_price_5` | string | No | Take profit target 5 |
| `sell_price_6` | string | No | Take profit target 6 |
| `stop_loss` | string | No | Stop-loss price |
| `type` | string | No | `long` (default) or `short` |
| `invest` | number | No | Investment percentage per user |
| `ttl_buy_order` | number | No | Time-to-live for the buy order (ms) |
| `attachment_image1_url` | string | No | Chart image URL |
| `attachment_image2_url` | string | No | Secondary image URL |
| `attachment_description` | string | No | Signal description (max 1000 chars) |

### Option B: Pre-Formatted Text

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `formatted_text` | object | Yes | Pre-parsed signal object matching Anny's internal signal schema |

If `formatted_text` is provided, structured fields are ignored.

## Example

```bash
curl -X POST https://api.anny.trade/v1/signal \
  -H "Content-Type: application/json" \
  -H "anny-api-key: YOUR_API_KEY" \
  -H "anny-api-secret: YOUR_API_SECRET" \
  -d '{
    "coin": "ETH",
    "trade_market": "USDT",
    "exchange": "BINANCE",
    "buy_price_min": "3800",
    "buy_price_max": "3850",
    "sell_price_1": "4000",
    "sell_price_2": "4200",
    "sell_price_3": "4500",
    "stop_loss": "3600",
    "type": "long",
    "invest": 10,
    "attachment_description": "ETH breaking out of resistance"
  }'
```

## Response

```json
{
  "result": { "type": "OPERATION_PERFORMED" },
  "payload": {
    "parent_signal_id": "abc123def456",
    "result": "success"
  }
}
```

The `parent_signal_id` is used in all subsequent operations (take profit, trailing stop, rebuy, DCA, cancel, update).
