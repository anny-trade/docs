# MCP Connector

The Anny Trade MCP Connector lets you access Anny's portfolio intelligence tools directly from Claude, ChatGPT, or any [MCP-compatible](https://modelcontextprotocol.io) AI client.

## What You Can Do

Anny exposes 54 tools across ten categories. Some work without signing in; others require authentication and may cost credits.

### Technical Analysis & Market Intelligence

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `get_technical_analysis` | RSI, MACD, EMA, ADX, OBV, VWAP, volume analysis | No | 0 |
| `get_anny_line_status` | CFO Anny Line indicator state for any asset | No | 0 |
| `get_flip_intelligence` | Confidence scoring for recent CFO Line state flips | No | 0 |
| `compare_assets` | Head-to-head comparison of two assets | No | 0 |
| `get_institutional_intelligence` | ETF flows, corporate treasuries, whale activity | No | 0 |
| `get_market_state` | Fear & Greed, ETF flows, funding rates, on-chain metrics | Yes | 0 |
| `get_market_analysis` | Cross-market dynamics: BTC regime, correlations, macro | No | 0 |
| `run_scenario` | Portfolio stress-test: "what if BTC drops 30%?" | Yes | 0 |
| `find_historical_pattern` | Find similar past market conditions (coming soon) | No | 0 |

### Tax & Holdings

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `get_tax_status` | Monthly disposals, gains/losses, DARF estimate | Yes | 0 |
| `get_tax_holdings` | Cost basis, unrealized P&L per asset | Yes | 0 |

### Signal Management

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `get_signal` | Detailed info on a specific signal | Yes | 0 |
| `list_active_signals` | All active signals and positions | Yes | 0 |
| `get_signal_automation_config` | Automation settings for a signal | Yes | 0 |
| `analyze_signal_with_cfo` | CFO Line analysis for a signal's asset | Yes | 0 |
| `toggle_auto_invest` / `stop` / `sell` / `trailing` | Toggle automation flags | Yes | 0 |
| `update_signal_target` | Update target/stop prices (DB-only) | Yes | 0 |
| `cancel_pending_order` | Cancel exchange order for a signal | Yes | 0 |
| `place_take_profit` | Place sell order for a signal | Yes | 0 |
| `place_trailing_stop` | Place stop order for a signal | Yes | 0 |

### Bot Management

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `list_bots` | List all trading bots | Yes | 0 |
| `get_bot_config` | Bot configuration details | Yes | 0 |
| `get_bot_fires` | Bot trigger history | Yes | 0 |
| `pause_bot` / `restart_bot` | Pause or restart a bot | Yes | 0 |
| `create_bot_from_strategy` | Deploy strategy as a bot (created paused) | Yes | 0 |

### Community (Signal Groups)

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `list_communities` | List signal group memberships | Yes | 0 |
| `get_community_pnl` | Community performance report | Yes | 0 |
| `allocate_community_investment` | Set investment per signal | Yes | 0 |

### CFO Line Backtest & Optimizer

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `run_cfo_line_backtest` | Backtest CFO Line on any asset | Yes | 100 |
| `run_optimizer` | Diagnose and optimize CFO Line filters (PRO+) | Yes | 900 |

### Custom Strategies

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `backtest_custom_strategy` | Backtest custom indicator strategy | Yes | In msg |
| `scan_custom_signals` | Check if strategy conditions are met now | Yes | 0 |
| `prescan_custom_strategy` | Free loss pattern pre-scan | Yes | 0 |
| `optimize_custom_strategy` | Full custom strategy optimizer (PRO+) | Yes | 900 |

### Trading Ideas

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `get_trading_idea_analysis` | Analysis of published strategies | No | 0 |

### Portfolio Management

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `check_symbol_availability` | Check if asset is tradeable on your exchange | Yes | 0 |
| `execute_market_order` | Buy/sell at market price (2-step confirm) | Yes | 0 |
| `get_exchange_balance` | Check exchange balances | Yes | 0 |
| `get_open_orders` | List pending orders | Yes | 0 |
| `cancel_order` | Cancel a pending order | Yes | 0 |

### Support & Knowledge

| Tool | Description | Auth | Credits |
|------|-------------|------|---------|
| `ask_agent` | Knowledge base + support agent | No | 0 |
| `check_user_health` | Platform diagnostics | Yes | 0 |
| `create_support_ticket` | Escalate to human support | Yes | 0 |
| `get_ticket_status` | Check ticket status | Yes | 0 |
| `record_resolution_feedback` | Rate support quality | Yes | 0 |
| `claim_welcome_bonus` | Claim 500-credit welcome bonus | Yes | 0 |
| `get_exchange_setup_guide` | Exchange API key setup guide | No | 0 |
| `log_skill_gap` / `submit_skill_request` / `submit_bug_report` | Feature requests & bugs | Yes | 0 |

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
