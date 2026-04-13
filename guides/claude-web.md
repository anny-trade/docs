---
title: Connect to Claude.ai
parent: Guides
nav_order: 2
---

# Connect to Claude.ai

Step-by-step guide to connecting Anny Trade to Claude on the web.

## Requirements

- A [Claude.ai](https://claude.ai) account with Pro, Team, or Enterprise subscription
- An Anny Trade account

## Steps

### 1. Open Connector Settings

Go to [claude.ai](https://claude.ai), click your **profile icon** in the bottom-left → **Settings** → **Connectors**.

### 2. Add Custom Connector

Click **Add custom connector** and fill in:

| Field | Value |
|-------|-------|
| Name | `Anny Trade` |
| URL | `https://mcp.anny.trade/mcp` |

Click **Add**.

### 3. Authorize

You'll be redirected to the Anny Trade login page. Sign in with your email and password.

After authorization, you'll be redirected back to Claude. The connector should show as connected.

### 4. Start Using

Open a new conversation and try:

> How is my portfolio doing?

Claude will call Anny's `get_portfolio_status` tool and return a table of your positions with CFO Line states.

## Tips

- You can use Anny tools alongside other connectors — Claude will pick the right tool based on your question
- For best results, be specific about what you want: "CFO Line reading for SOL on the 4-hour chart" works better than "tell me about SOL"
- Use follow-up questions — Anny supports multi-turn conversations with context
