# MCP Connector

The Anny Trade MCP Connector lets you access Anny's portfolio intelligence tools directly from Claude, ChatGPT, or any [MCP-compatible](https://modelcontextprotocol.io) AI client.

## What You Can Do

Anny exposes 21 tools across six categories. Some work without signing in; others require authentication and may cost credits.

### Market Intelligence

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `get_market_analysis` | CFO Anny Line indicator reading for any asset | No | 0 |
| `get_price` | Current price, 24h change, and volume | No | 0 |
| `get_macro_analysis` | BTC vs Gold, Dollar Index, or Manufacturing PMI | No | 0 |
| `get_daily_briefing` | AI-generated daily market + portfolio summary | Yes | 0 |
| `get_market_state` | Fear & Greed, ETF flows, funding rates, on-chain metrics | Yes | 0 |

### Portfolio

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `get_portfolio_status` | Positions, P&L, and indicator states across exchanges | Yes | 0 |
| `get_risk_score` | Composite risk score (0-100) with sub-scores and top factors | Yes | 0 |
| `simulate_scenario` | "What if BTC drops 30%?" — project impact on your holdings | Yes | 0 |

### Analysis

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `run_scenario_analysis` | Historical backtest of the CFO Line on any asset | Yes | 0 |
| `assess_trade_risk` | Technical risk assessment (RSI, ADX, MACD, volume) for a trade | No | 0 |

### Custom Strategies

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `backtest_custom_strategy` | Backtest your own indicator strategy on historical data | Yes | 100 |
| `scan_custom_signals` | Check if your strategy conditions are met right now | Yes | 0 |
| `deploy_strategy_as_bot` | Deploy a strategy as a live trading bot (created paused) | Yes | 0 |
| `get_bot_strategy` | View strategy rules on an existing bot | Yes | 0 |
| `update_strategy_config` | Modify strategy rules on a bot | Yes | 0 |

### Strategy Optimization

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `optimize_strategy` | Diagnose and optimize CFO Line filter settings (Beta) | Yes | 900 |
| `stress_test_strategy` | Walk-forward analysis to validate optimized settings (Coming soon) | Yes | 1,800 |

### Risk Management

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `calculate_position_size` | Position sizing via Fixed Fractional or Kelly Criterion | No | 0 |
| `calculate_stop_loss` | Stop-loss and take-profit levels using ATR, structure, and regime models | No | 0 |

### General

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `ask_anny` | Ask Anny anything about crypto or your portfolio | No* | Varies |
| `feedback_to_anny` | Send feedback or report a bug | No | 0 |

*`ask_anny` works without auth (limited public chat) but provides full portfolio context when signed in.

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
