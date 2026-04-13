# Signal API Authentication

Partner authentication uses an API key + HMAC secret pair issued per partner channel.

## Headers

Every request must include:

| Header | Description |
|--------|-------------|
| `anny-api-key` | Your partner API key |
| `anny-api-secret` | HMAC-SHA512 signature |

## How the Secret Works

The secret is computed as:

```
HMAC-SHA512(api_key, JWT_SECRET + partner_salt) → Base64
```

Where:
- `api_key` is the key used as HMAC input
- `JWT_SECRET` is Anny's server-side secret
- `partner_salt` is a unique salt assigned to your partner channel

You receive both the `api_key` and pre-computed `api_secret` when your partner channel is provisioned. You don't compute the HMAC yourself — just send both values as headers.

## Example Request

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
    "entry_price_max": "68000",
    "exit_price_1": "72000"
  }'
```

## Obtaining Credentials

Partner API credentials are provisioned by the Anny Trade team. Contact support@anny.trade to set up a partner channel.

## Security Notes

- API secrets are validated using constant-time comparison to prevent timing attacks
- Each partner channel has a unique salt — compromising one key does not affect others
- All requests must be sent over HTTPS
