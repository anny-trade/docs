# Signal Tools

<!-- AUTO-GENERATED from anny-trade-mcp/src/definitions/signal-tools.ts -->
<!-- Do not edit manually. Run: cd anny-trade-mcp && node scripts/generate-docs.mjs -->

Tools for reading and managing trading signals via the MCP connector.

---

## get\_signal

Get detailed information about a specific trading signal.

**Auth required:** Yes

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID to retrieve details for |

### Annotations

| readOnlyHint | destructiveHint | idempotentHint |
|:---:|:---:|:---:|
| true | false | true |

---

## list\_active\_signals

List all active trading signals and positions for the authenticated user.

**Auth required:** Yes

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `exchange` | string | No | Filter to a specific exchange (e.g. "BINANCE", "BYBIT"). Omit for all. |
| `limit` | integer | No | Maximum number of signals to return (default: 20, max: 50) |

### Annotations

| readOnlyHint | destructiveHint | idempotentHint |
|:---:|:---:|:---:|
| true | false | true |

---

## get\_signal\_automation\_config

Get the full automation configuration for a specific signal.

**Auth required:** Yes

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID to get automation config for |

### Annotations

| readOnlyHint | destructiveHint | idempotentHint |
|:---:|:---:|:---:|
| true | false | true |

---

## analyze\_signal\_with\_cfo

Analyze a signal's asset using the CFO Anny Line indicator, respecting the signal's timeframe.

**Auth required:** Yes

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID to analyze with CFO Line |

### Annotations

| readOnlyHint | destructiveHint | idempotentHint |
|:---:|:---:|:---:|
| true | false | true |

---

## toggle\_auto\_invest

Enable or disable auto-invest (auto-buy) for a specific signal.

**Auth required:** Yes

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID |
| `enabled` | boolean | Yes | true to enable, false to disable |

### Annotations

| readOnlyHint | destructiveHint | idempotentHint |
|:---:|:---:|:---:|
| false | false | true |

---

## toggle\_auto\_stop

Enable or disable auto-stop (stop-loss automation) for a specific signal.

**Auth required:** Yes

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID |
| `enabled` | boolean | Yes | true to enable, false to disable |

### Annotations

| readOnlyHint | destructiveHint | idempotentHint |
|:---:|:---:|:---:|
| false | false | true |

---

## toggle\_auto\_sell

Enable or disable auto-sell (take-profit automation) for a specific signal.

**Auth required:** Yes

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID |
| `enabled` | boolean | Yes | true to enable, false to disable |

### Annotations

| readOnlyHint | destructiveHint | idempotentHint |
|:---:|:---:|:---:|
| false | false | true |

---

## toggle\_auto\_trailing

Enable or disable trailing stop for a specific signal.

**Auth required:** Yes

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID |
| `enabled` | boolean | Yes | true to enable, false to disable |

### Annotations

| readOnlyHint | destructiveHint | idempotentHint |
|:---:|:---:|:---:|
| false | false | true |

---

## update\_signal\_target

Update a target price, stop-loss price, or entry price for a signal.

**Auth required:** Yes

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The all_signals_id |
| `target_field` | string | Yes | Which price field to update |
| `price` | number | Yes | New price value |

### Annotations

| readOnlyHint | destructiveHint | idempotentHint |
|:---:|:---:|:---:|
| false | false | true |

---

## cancel\_pending\_order

Cancel a pending (unfilled) order on the exchange for a specific signal.

**Auth required:** Yes | **Endpoint:** `/v1/full` only

> **Warning:** This tool has exchange side-effects.

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID owning the order |
| `order_id` | string | Yes | The exchange order ID to cancel |
| `reason` | string | No | Reason for cancellation (default: "user-request-via-chat") |

### Annotations

| readOnlyHint | destructiveHint | idempotentHint |
|:---:|:---:|:---:|
| false | **true** | false |

---

## place\_take\_profit

Place a take-profit (sell) order on the exchange for a signal's position.

**Auth required:** Yes | **Endpoint:** `/v1/full` only

> **Warning:** This tool has exchange side-effects.

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID |
| `price` | number | No | Sell price |
| `amount_to_sell` | number | No | Exact coin amount to sell |
| `amount_relative` | number | No | Percentage to sell (0-100) |
| `order_type` | string | No | Order type (default: LIMIT) |

### Annotations

| readOnlyHint | destructiveHint | idempotentHint |
|:---:|:---:|:---:|
| false | **true** | false |

---

## place\_trailing\_stop

Place a trailing stop (stop-loss) order on the exchange for a signal's position.

**Auth required:** Yes | **Endpoint:** `/v1/full` only

> **Warning:** This tool has exchange side-effects.

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `signal_id` | string | Yes | The signal ID |
| `stop_price` | number | Yes | Stop trigger price |
| `limit_price` | number | No | Limit price for STOP_LOSS_LIMIT orders |
| `amount_to_sell` | number | No | Quantity to liquidate |
| `order_type` | string | No | Stop order type (default: STOP_LOSS_LIMIT) |

### Annotations

| readOnlyHint | destructiveHint | idempotentHint |
|:---:|:---:|:---:|
| false | **true** | false |

---

## Adding new signal tools

1. Add the definition to `anny-trade-mcp/src/definitions/signal-tools.ts`
2. Create the MCP tool in `src/tools/`
3. Add the handler in `anny-backend/src/askanny/tools/ToolExecutor.js`
4. Run `cd anny-trade-mcp && npm run build && node scripts/generate-docs.mjs`
5. Commit the updated `anny-docs/docs/mcp/signals.md`
