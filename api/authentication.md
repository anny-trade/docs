---
title: Authentication
parent: API Reference
nav_order: 1
---

# API Authentication

## Session Token

Authenticate by including your session token in the `session-token` header:

```bash
curl -X POST https://api.anny.trade/backend/anny-line/chart \
  -H "Content-Type: application/json" \
  -H "session-token: <your-session-token>" \
  -d '{"asset": "BTC", "interval": "1d", "tradeMarket": "USDT"}'
```

## Obtaining a Session Token

### Email + Password

```bash
curl -X POST https://api.anny.trade/backend/login \
  -H "Content-Type: application/json" \
  -d '{"email": "you@example.com", "password": "your-password"}'
```

Response:

```json
{
  "result": { "type": "OPERATION_PERFORMED" },
  "payload": {
    "token": "eyJhbG...",
    "user": {
      "userid": "12345",
      "email": "you@example.com",
      "subscriptionplan": "PRO"
    }
  }
}
```

### Firebase Authentication

If your account was created via Google, Facebook, Apple, or Twitter sign-in:

```bash
curl -X POST https://api.anny.trade/backend/login/firebase \
  -H "Content-Type: application/json" \
  -d '{"idToken": "<firebase-id-token>"}'
```

## Token Lifetime

Session tokens are valid for 7 days (30 days for mobile clients). After expiry, authenticate again to obtain a new token.

## Guest Endpoints

Some endpoints work without authentication:

- `POST /backend/anny-line/chart` — Indicator readings
- `POST /backend/anny-line/flip-intelligence` — Transition context
- `POST /backend/askanny/guest-chat` — Limited AI chat

These return data for any supported asset without requiring a session token.
