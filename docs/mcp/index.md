# MCP Connector

The Anny Trade MCP Connector lets you access Anny's portfolio intelligence tools directly from Claude, ChatGPT, or any [MCP-compatible](https://modelcontextprotocol.io) AI client.

## What You Can Do

| Tool | Description | Auth Required |
|------|-------------|---------------|
| `ask_anny` | Ask Anny anything about crypto or your portfolio | No (limited without auth) |
| `get_market_analysis` | Get CFO Anny Line indicator reading for any asset | No |
| `get_portfolio_status` | View your portfolio with indicator states | Yes |
| `run_scenario_analysis` | Run historical scenario analysis on any asset | Yes |
| `backtest_custom_strategy` | Backtest your own indicator strategy | Yes |
| `scan_custom_signals` | Check if your strategy conditions are met now | Yes |
| `deploy_strategy_as_bot` | Deploy a strategy as a live trading bot | Yes |
| `get_bot_strategy` | View strategy rules on an existing bot | Yes |
| `update_strategy_config` | Modify strategy rules on a bot | Yes |
| `feedback_to_anny` | Send feedback or report a bug | No |

## Server URL

```
https://mcp.anny.trade/mcp
```

## Transport

Streamable HTTP (stateless). Each request creates a fresh transport — no session management required.

## Quick Start

1. Open your MCP client settings (e.g., Claude Desktop → Settings → Connectors)
2. Add a custom connector with URL: `https://mcp.anny.trade/mcp`
3. Sign in with your Anny Trade account when prompted
4. Start asking questions: *"What's the CFO Line reading for BTC?"*

See [Getting Started](getting-started.md) for detailed setup instructions per client.
