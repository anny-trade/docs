# Create Signal (V2)

```
POST /v2/signal
```

Extended signal creation with support for leverage, margin type, split entry allocation, and mid-range entry price. Recommended for new integrations.

## Request Body

### Structured Fields

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `coin` | string | Yes | — | Asset symbol: `BTC`, `ETH`, `SOL` |
| `trade_market` | string | Yes | — | Quote currency: `USDT`, `BTC` |
| `exchange` | string | Yes | — | Exchange: `BINANCE`, `BYBIT`, `OKX` |
| `invest` | number | Yes | — | Investment percentage per user |
| `entry_price_max` | string | Yes | — | Entry price range — upper bound |
| `entry_price_min` | string | No | — | Entry price range — lower bound |
| `entry_price_mid` | string | No | — | Mid-range entry price |
| `exit_price_1` | string | Yes | — | Take profit target 1 |
| `exit_price_2` | string | No | — | Take profit target 2 |
| `exit_price_3` | string | No | — | Take profit target 3 |
| `exit_price_4` | string | No | — | Take profit target 4 |
| `exit_price_5` | string | No | — | Take profit target 5 |
| `stop_loss` | string | No | — | Stop-loss price |
| `type` | string | No | `long` | `long` or `short` |
| `account` | string | No | `SPOT` | `SPOT`, `MARGIN`, or `FUTURES` |
| `leverage` | number | No | `1` | Leverage multiplier (futures/margin) |
| `margin_type` | string | No | `ISOLATED` | `ISOLATED` or `CROSS` |
| `entry_mode` | string | No | `range` | Entry mode |
| `invest_entry_min` | number | No | — | Allocation % for min entry |
| `invest_entry_mid` | number | No | — | Allocation % for mid entry |
| `invest_entry_max` | number | No | — | Allocation % for max entry |
| `ttl_buy_order` | number | No | — | Time-to-live for buy order (ms) |
| `attachment_image1_url` | string | No | — | Chart image URL |
| `attachment_image2_url` | string | No | — | Secondary image URL |
| `attachment_description` | string | No | — | Signal description (max 1000 chars) |

### Split Entry Allocation

V2 supports splitting the investment across multiple entry levels. Use `invest_entry_min`, `invest_entry_mid`, and `invest_entry_max` to control what percentage of the total investment goes to each entry price.

## Example — Spot Signal

```bash
curl -X POST https://api.anny.trade/v2/signal \
  -H "Content-Type: application/json" \
  -H "anny-api-key: YOUR_API_KEY" \
  -H "anny-api-secret: YOUR_API_SECRET" \
  -d '{
    "coin": "BTC",
    "trade_market": "USDT",
    "exchange": "BINANCE",
    "invest": 10,
    "entry_price_min": "65000",
    "entry_price_max": "66000",
    "exit_price_1": "70000",
    "exit_price_2": "75000",
    "stop_loss": "62000",
    "type": "long"
  }'
```

## Example — Futures Signal with Leverage

```bash
curl -X POST https://api.anny.trade/v2/signal \
  -H "Content-Type: application/json" \
  -H "anny-api-key: YOUR_API_KEY" \
  -H "anny-api-secret: YOUR_API_SECRET" \
  -d '{
    "coin": "ETH",
    "trade_market": "USDT",
    "exchange": "BYBIT",
    "invest": 5,
    "account": "FUTURES",
    "leverage": 10,
    "margin_type": "ISOLATED",
    "entry_price_max": "3800",
    "exit_price_1": "4000",
    "stop_loss": "3650",
    "type": "long"
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
