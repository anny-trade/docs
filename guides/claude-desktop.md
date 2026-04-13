# Connect to Claude Desktop

Step-by-step guide to connecting Anny Trade to the Claude Desktop app.

## Requirements

- [Claude Desktop](https://claude.com/download) installed
- A Claude Pro, Team, or Enterprise subscription
- An Anny Trade account

## Steps

### 1. Open Connector Settings

Open Claude Desktop and click the **hamburger menu** (☰) → **Settings** → **Connectors**.

### 2. Add Custom Connector

Click **Add custom connector** and fill in:

| Field | Value |
|-------|-------|
| Name | `Anny Trade` |
| URL | `https://mcp.anny.trade/mcp` |

Click **Add**.

### 3. Authorize

Claude will open a browser window showing the Anny Trade login page. Enter your email and password, then click **Sign in**.

After signing in, the browser will redirect back to Claude. You should see "Anny Trade" listed under your connectors with a green status indicator.

### 4. Start Using

Go back to any Claude conversation and try:

> What's the CFO Line reading for BTC?

Claude will use Anny's `get_market_analysis` tool and return the current indicator state.

## Troubleshooting

**"Connection failed" error:**
- Check that `https://mcp.anny.trade/health` returns `{"status":"ok"}` in your browser
- Make sure you're on a paid Claude plan (connectors require Pro or higher)

**"Authentication required" on portfolio tools:**
- Your session may have expired. Go to Settings → Connectors → Anny Trade → Reconnect

**Tools not appearing:**
- Try disconnecting and reconnecting the connector
- Restart Claude Desktop
