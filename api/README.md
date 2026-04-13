---
title: API Reference
nav_order: 3
has_children: true
---

# API Reference

The Anny Trade REST API provides programmatic access to the same intelligence layer that powers the MCP connector and the web platform.

## Base URL

```
https://api.anny.trade
```

## Authentication

All authenticated endpoints require a session token:

```
session-token: <your-session-token>
```

See [Authentication](authentication.md) for how to obtain a token.

## Response Format

All endpoints return a standard envelope:

```json
{
  "result": {
    "type": "OPERATION_PERFORMED",
    "ttl": 60000
  },
  "payload": {
    // ... endpoint-specific data
  }
}
```

### Result Types

| Type | Meaning |
|------|---------|
| `OPERATION_PERFORMED` | Success |
| `UNAUTHORIZED` | Invalid or missing session token |
| `INVALID_INPUT_*` | Validation error (suffix describes which field) |
| `CRITICAL` | Internal server error |

## Endpoints

| Method | Path | Description | Auth |
|--------|------|-------------|------|
| POST | `/backend/anny-line/chart` | CFO Anny Line indicator state | No |
| POST | `/backend/anny-line/flip-intelligence` | State transition context | No |
| POST | `/backend/anny-line/portfolio` | Portfolio-wide indicator states | Yes |
| POST | `/backend/anny-line/backtest` | Historical scenario analysis | Yes |
| GET | `/backend/activepositions` | Current portfolio positions | Yes |
| POST | `/backend/askanny/chat` | Chat with Anny (authenticated) | Yes |
| POST | `/backend/askanny/guest-chat` | Chat with Anny (guest) | No |

## Rate Limits

API requests are rate-limited per user. See [MCP Rate Limits](../mcp/rate-limits.md) for tier details — the same limits apply to direct API access.
