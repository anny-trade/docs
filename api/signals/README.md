---
title: "Signal API (Partner)"
nav_order: 4
has_children: true
---

# Signal API (Partner)

The Signal API allows partner channels to create and manage trading signals programmatically. Signals are distributed to subscribed users who can auto-execute them on connected exchanges.

## Base URL

```
https://api.anny.trade
```

## Versions

| Version | Path | Notes |
|---------|------|-------|
| **V1** | `/v1/signal` | Original. Range entry, up to 6 take-profit targets. |
| **V2** | `/v2/signal` | Extended. Adds leverage, margin type, split entry allocation, mid entry price. |

Both versions are active. V2 is recommended for new integrations.

## Signal Lifecycle

```
Create Signal ──► Signal enters bot queue
                     │
                     ├──► Entry price hit → Auto-invest executes buy order
                     │
                     ├──► Take Profit added → Sell target(s) set
                     │
                     ├──► Trailing Stop added → Dynamic stop-loss activated
                     │
                     ├──► Rebuy added → Additional entry zone created
                     │
                     ├──► DCA added → Dollar-cost averaging level added
                     │
                     ├──► Update Prices → Modify entry/exit/stop levels
                     │
                     └──► Cancel → Signal removed, positions closed
```

## Endpoints Summary

| Method | Path | Description |
|--------|------|-------------|
| POST | `/v1/signal` | Create signal (V1) |
| POST | `/v2/signal` | Create signal (V2) |
| POST | `/v1/signal/:parent_signal_id/call/takeprofit` | Add take profit target |
| POST | `/v1/signal/:parent_signal_id/call/trailingstop` | Add trailing stop |
| POST | `/v1/signal/:parent_signal_id/call/rebuy` | Add rebuy zone |
| POST | `/v1/signal/:parent_signal_id/call/dca` | Add DCA level |
| PUT | `/v1/signal/:parent_signal_id/updateprice` | Update signal prices |
| DELETE | `/v1/signal/:parent_signal_id/cancel` | Cancel signal |

All endpoints require partner authentication. See [Authentication](authentication.md).

## Response Format

All endpoints return the standard Anny response envelope:

```json
{
  "result": {
    "type": "OPERATION_PERFORMED"
  },
  "payload": {
    "parent_signal_id": "abc123",
    "result": "success"
  }
}
```

### Error Responses

| HTTP | Result Type | Meaning |
|------|------------|---------|
| 200 | `OPERATION_PERFORMED` | Success (check `payload.result`) |
| 400 | `INVALID_INPUT_MISSING` | Required fields missing |
| 400 | `INVALID_INPUT_CONTENT` | Invalid field values |
| 403 | `UNAUTHORIZED` | Invalid API credentials |
| 500 | `CRITICAL` | Internal server error |
