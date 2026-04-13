# Portfolio

Retrieve your current positions across all connected exchanges.

## Get Active Positions

```
GET /backend/activepositions
```

**Auth required:** Yes

### Example

```bash
curl https://api.anny.trade/backend/activepositions \
  -H "session-token: <your-token>"
```

### Response

```json
{
  "result": { "type": "OPERATION_PERFORMED" },
  "payload": {
    "positions": [
      {
        "coin": "BTC",
        "exchange": "BINANCE",
        "quantity": 0.5,
        "currentPrice": 68500.00,
        "change24h": 2.3,
        "pnl": 1250.00
      },
      {
        "coin": "ETH",
        "exchange": "BINANCE",
        "quantity": 10.0,
        "currentPrice": 3850.00,
        "change24h": -0.8,
        "pnl": -320.00
      }
    ]
  }
}
```

### Fields

| Field | Type | Description |
|-------|------|-------------|
| `coin` | string | Asset symbol |
| `exchange` | string | Exchange name |
| `quantity` | number | Position size |
| `currentPrice` | number | Current price in quote currency |
| `change24h` | number | 24-hour price change (%) |
| `pnl` | number | Unrealised profit/loss in quote currency |

## Combined Portfolio View

For a complete portfolio view with both positions and CFO Line states, call both endpoints:

```bash
# Positions
curl https://api.anny.trade/backend/activepositions \
  -H "session-token: <your-token>"

# CFO Line states
curl -X POST https://api.anny.trade/backend/anny-line/portfolio \
  -H "Content-Type: application/json" \
  -H "session-token: <your-token>" \
  -d '{}'
```

The MCP `get_portfolio_status` tool does this automatically and merges the results into a single table.
