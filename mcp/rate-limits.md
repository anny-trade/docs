---
title: Rate Limits
parent: MCP Connector
nav_order: 5
---

# Rate Limits

Rate limits are applied per user (authenticated) or per IP (guest) using a sliding window.

## Limits by Tier

| Tier | Per Minute | Per Day |
|------|-----------|---------|
| Guest (no auth) | 5 | 50 |
| FREE | 10 | 200 |
| PRO | 30 | 1,000 |
| PRO+ | 60 | 5,000 |

## Response Headers

When rate limited, the server returns HTTP `429` with:

```json
{
  "error": "Rate limit exceeded",
  "retryAfterMs": 45000
}
```

The `retryAfterMs` field tells you how many milliseconds until the window resets.

## How It Works

- **Per-minute window:** Resets every 60 seconds from first request
- **Per-day window:** Resets every 24 hours from first request
- Both windows must have capacity for a request to succeed
- Authenticated users are tracked by user ID; guests by IP address

## Tips

- Sign in to get higher limits (even FREE accounts get 2x guest limits)
- If you hit the per-minute limit, wait for the window to reset — it's usually under 60 seconds
- Scenario analysis is the heaviest operation (10–30 seconds compute time) but counts as a single request
