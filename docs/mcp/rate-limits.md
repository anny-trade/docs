# Rate Limits

Rate limits are applied per user (authenticated) or per IP (guest) using a sliding window.

## Limits by Tier

| Tier | Per Minute | Per Day |
|------|-----------|---------|
| Guest (no auth) | 5 | 50 |
| FREE | 10 | 200 |
| PRO | 30 | 1,000 |
| Pro Max | 60 | 5,000 |

## Credit Costs

Most tools are free to use. The following tools consume credits from your subscription balance:

| Tool | Credits | Min Tier |
|------|---------|----------|
| `ask_anny` | Varies (80–2,900) | FREE |
| `backtest_custom_strategy` | 100 | PRO |
| `optimize_strategy` | 900 | PRO |
| `stress_test_strategy` | 1,800 | Pro Max |

AI-powered tools (`ask_anny`) are billed dynamically based on actual token usage. Simple questions cost ~80–150 credits; deep portfolio analysis with multiple tool rounds costs more. You can see the exact cost of each response via the info icon next to it.

All other tools cost 0 credits:

`get_market_analysis`, `get_price`, `get_macro_analysis`, `get_daily_briefing`, `get_market_state`, `get_portfolio_status`, `get_risk_score`, `simulate_scenario`, `run_scenario_analysis`, `assess_trade_risk`, `scan_custom_signals`, `deploy_strategy_as_bot`, `get_bot_strategy`, `update_strategy_config`, `calculate_position_size`, `calculate_stop_loss`, `feedback_to_anny`

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
