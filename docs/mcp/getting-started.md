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
- **stress_test_strategy** — Walk-forward validation of optimized settings (1,800 credits, coming soon)

## Verify It Works

After connecting, try asking:

> What's the CFO Anny Line reading for ETH on the daily chart?

You should see the current indicator state (Accumulate, Wait, or Distribute) along with recent state transitions.
