---
title: askAnny
parent: API Reference
nav_order: 5
---

# askAnny

Chat with Anny, the AI portfolio intelligence assistant. Anny has access to indicator readings, market data, and (for authenticated users) your portfolio context.

## Authenticated Chat

```
POST /backend/askanny/chat
```

**Auth required:** Yes

Full-context chat with access to your portfolio, positions, and account data.

### Request Body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `message` | string | Yes | Your question (max 2000 characters) |
| `conversationId` | string | No | Continue a previous conversation |

### Example

```bash
curl -X POST https://api.anny.trade/backend/askanny/chat \
  -H "Content-Type: application/json" \
  -H "session-token: <your-token>" \
  -d '{"message": "How is my portfolio doing?"}'
```

### Response

```json
{
  "result": { "type": "OPERATION_PERFORMED" },
  "payload": {
    "response": "Your portfolio is looking strong today...",
    "conversationId": "conv_abc123"
  }
}
```

---

## Guest Chat

```
POST /backend/askanny/guest-chat
```

**Auth required:** No

Limited chat with access to public market data and general crypto knowledge. No portfolio context.

### Request Body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `message` | string | Yes | Your question (max 2000 characters) |
| `conversationId` | string | No | Continue a previous conversation |

### Example

```bash
curl -X POST https://api.anny.trade/backend/askanny/guest-chat \
  -H "Content-Type: application/json" \
  -d '{"message": "What is the CFO Anny Line?"}'
```

---

## Multi-Turn Conversations

Pass the `conversationId` from a previous response to continue the conversation with context:

```bash
# First message
curl -X POST https://api.anny.trade/backend/askanny/chat \
  -H "Content-Type: application/json" \
  -H "session-token: <your-token>" \
  -d '{"message": "What is the CFO Line reading for BTC?"}'

# Follow-up (using conversationId from previous response)
curl -X POST https://api.anny.trade/backend/askanny/chat \
  -H "Content-Type: application/json" \
  -H "session-token: <your-token>" \
  -d '{
    "message": "What about on the 4-hour chart?",
    "conversationId": "conv_abc123"
  }'
```
