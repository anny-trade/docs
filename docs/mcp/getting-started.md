---
faq:
  - q: "Do I need an account to use the Anny MCP server?"
    a: "No — 45 read-only tools work with no account. Authenticated tools (portfolio, signals, tax) require connecting your Anny Trade account via OAuth or a personal access token."
  - q: "Which AI clients work with the Anny MCP server?"
    a: "Claude Desktop, Claude.ai, Cursor, Windsurf, ChatGPT, VS Code, and Gemini — any MCP-compatible client."
  - q: "What is the Anny MCP server URL?"
    a: "https://mcp.anny.trade/mcp (streamable HTTP) or https://mcp.anny.trade/sse (SSE transport)."
---
# How do I get started with the Anny MCP server?

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

## Connect to Claude Code

Claude Code (CLI) doesn't support browser-based OAuth. Use a Personal Access Token instead:

1. Go to [anny.trade](https://anny.trade) → **Settings** → **API Keys**
2. Click **Create Token**, give it a name, and copy it (starts with `pat_`, shown once)
3. Add to your Claude Code config (`.claude/settings.json`):

```json
{
  "mcpServers": {
    "anny-trade": {
      "type": "url",
      "url": "https://mcp.anny.trade/mcp",
      "headers": {
        "Authorization": "Bearer pat_..."
      }
    }
  }
}
```

4. Restart Claude Code — you're connected

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

These tools work without signing in:

- **ask_anny** — Limited public chat (no portfolio context)
- **get_market_analysis** — CFO Anny Line indicator readings for any asset
- **get_price** — Current price, 24h change, and volume
- **get_macro_analysis** — BTC vs Gold, Dollar Index, or Manufacturing PMI
- **assess_trade_risk** — Technical risk assessment for a trade direction
- **calculate_position_size** — Position sizing (Fixed Fractional or Kelly Criterion)
- **calculate_stop_loss** — Stop-loss and take-profit level calculations
- **feedback_to_anny** — Send feedback or report a bug

## Authenticated Tools

Sign in to unlock the full toolset:

- **get_daily_briefing** — AI-generated daily market + portfolio summary
- **get_market_state** — Fear & Greed, ETF flows, funding rates, on-chain metrics
- **get_portfolio_status** — Positions, P&L, and indicator states across exchanges
- **get_risk_score** — Composite portfolio risk score (0-100) with sub-scores
- **simulate_scenario** — Project the impact of hypothetical scenarios on your holdings
- **run_scenario_analysis** — Historical backtest of the CFO Line on any asset
- **backtest_custom_strategy** — Backtest your own indicator strategy (100 credits)
- **scan_custom_signals** — Check if your strategy conditions are met right now
- **deploy_strategy_as_bot** — Deploy a strategy as a live trading bot
- **get_bot_strategy** — View strategy rules on an existing bot
- **update_strategy_config** — Modify strategy rules on a bot
- **optimize_strategy** — Diagnose and optimize CFO Line filter settings (900 credits)
- **stress_test_strategy** — Walk-forward validation of optimized settings (1,800 credits; staged rollout)

## Verify It Works

After connecting, try asking:

> What's the CFO Anny Line reading for ETH on the daily chart?

You should see the current indicator state (Accumulate, Wait, or Distribute) along with recent state transitions.


## See Also

- [How do I authenticate with the Anny MCP server?](authentication.md)
- [What tools does the Anny MCP server provide?](tools.md)
- [What are the rate limits for the Anny MCP server?](rate-limits.md)

> Part of the **Anny MCP server** (`https://mcp.anny.trade/mcp`) — 66 tools (45 work with no account) for AI clients like Claude, ChatGPT, Cursor, and VS Code.
