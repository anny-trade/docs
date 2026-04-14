# Getting Started

## Prerequisites

- An Anny Trade account ([anny.trade](https://anny.trade))
- A supported MCP client (Claude Desktop, Claude.ai, or any MCP-compatible app)

## Connect to Claude Desktop

1. Open Claude Desktop
2. Go to **Settings** → **Connectors**
3. Click **Add custom connector**
4. Enter:
   - **Name:** Anny Trade
   - **URL:** `https://mcp.anny.trade/mcp`
5. Click **Connect**
6. You'll be redirected to sign in with your Anny Trade credentials
7. After signing in, you're connected — start chatting

## Connect to Claude.ai

1. Go to [claude.ai](https://claude.ai)
2. Click your profile → **Settings** → **Connectors**
3. Click **Add custom connector**
4. Enter:
   - **Name:** Anny Trade
   - **URL:** `https://mcp.anny.trade/mcp`
5. Click **Connect** and sign in when prompted

## Connect to Other MCP Clients

Any client that supports the MCP Streamable HTTP transport can connect. Point it at:

```
https://mcp.anny.trade/mcp
```

OAuth discovery is available at:

```
https://mcp.anny.trade/.well-known/oauth-authorization-server
```

## Guest Access

Some tools work without signing in:

- **ask_anny** — Limited public chat (no portfolio context)
- **get_market_analysis** — Full indicator readings for any asset
- **feedback_to_anny** — Send feedback

To use portfolio tools (`get_portfolio_status`, `run_scenario_analysis`) and custom strategy tools (`backtest_custom_strategy`, `scan_custom_signals`, `deploy_strategy_as_bot`), you need to sign in.

## Verify It Works

After connecting, try asking:

> What's the CFO Anny Line reading for ETH on the daily chart?

You should see the current indicator state (Accumulate, Wait, or Distribute) along with recent state transitions.
