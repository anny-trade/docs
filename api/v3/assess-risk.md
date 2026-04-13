---
title: Assess Risk
parent: "AI Endpoints (V3)"
nav_order: 1
---

# Assess Risk

```
GET /v3/ai/assess_risk
POST /v3/ai/assess_risk
```

Performs a technical analysis risk assessment for a cryptocurrency. Returns indicators including ADX, PSAR, RSI, MACD, EMA, volume analysis, and candlestick patterns.

**Rate limit:** 100 requests/minute per IP

## Authentication

V3 uses HMAC-SHA256 signature authentication:

| Header | Description |
|--------|-------------|
| `x-signature` | HMAC-SHA256 signature |
| `x-timestamp` | Unix timestamp of the request |

ChatGPT requests (identified by `User-Agent: ChatGPT-User`) bypass authentication.

## Parameters

| Name | In | Type | Required | Default | Description |
|------|----|------|----------|---------|-------------|
| `coin` | query | string | Yes | — | Crypto symbol: `BTC`, `ETH`, `XRP` |
| `trade_market` | query | string | No | `USDT` | Quote currency |
| `trade_side` | query | string | No | `long` | Direction: `long` or `short` |

## Example

```bash
curl "https://api.anny.trade/v3/ai/assess_risk?coin=BTC&trade_market=USDT&trade_side=long"
```

## Response

```json
{
  "riskProfile": "moderate",
  "adx": {
    "value": 25,
    "pdi": 28.5,
    "mdi": 18.2,
    "strength": 65,
    "trendStrength": "strong",
    "trendDirection": "up"
  },
  "psar": {
    "value": "up",
    "psarValue": "66500.00"
  },
  "btc": {
    "psar": {
      "value": "up",
      "psarValue": "67000.00"
    }
  },
  "marketTrend": {
    "value": "up"
  },
  "rsiCross": {
    "value": "bullish",
    "labels": { "trend": "up", "signal": "buy", "momentum": "increasing" },
    "results": { "rsi": 58.3, "rsiMovingAvg": 52.1 }
  },
  "macdCross": {
    "value": "bullish",
    "labels": { "trend": "up", "signal": "buy", "momentum": "increasing" },
    "results": { "MACD": 150.5, "histogram": 45.2, "signalValue": 105.3 }
  },
  "emaCross": {
    "value": "bullish",
    "labels": { "trend": "up", "signal": "buy", "momentum": "increasing" },
    "results": { "emaFast": 67200.0, "emaSlow": 66800.0 }
  },
  "volume": {
    "value": "+15%",
    "currentVolume": 1250000000,
    "previousVolume": 1086956522
  },
  "volumeAverage": {
    "label": "above average",
    "value": "high",
    "currentVolume": 1250000000,
    "averageVolume": 980000000,
    "medianVolume": 920000000,
    "maxVolume": 2100000000,
    "relativeVolume": "1.28"
  },
  "volumeSpread": {
    "momentum": "bullish",
    "spreadValue": "narrow",
    "volumeValue": "high",
    "currentVolume": 1250000000
  },
  "candlestick": {
    "value": "bullish",
    "pattern": "hammer",
    "sentiment": "bullish"
  },
  "dayOfWeek": "Weekday",
  "marketSession": "US"
}
```

## Response Fields

| Field | Description |
|-------|-------------|
| `riskProfile` | Overall risk assessment: `tooRisky`, `moderate`, `low` |
| `adx` | Average Directional Index — trend strength and direction |
| `psar` | Parabolic SAR — trend direction for the asset |
| `btc` | BTC market trend (PSAR-based) |
| `marketTrend` | Overall market direction based on BTC |
| `rsiCross` | RSI crossover signal with trend/momentum labels |
| `macdCross` | MACD crossover signal with histogram |
| `emaCross` | EMA crossover signal (fast vs slow) |
| `volume` | Volume change vs previous period |
| `volumeAverage` | Current volume relative to historical average |
| `volumeSpread` | Volume-spread analysis for momentum |
| `candlestick` | Detected candlestick pattern and sentiment |
| `dayOfWeek` | Weekday or Weekend |
| `marketSession` | Active trading session: Asian, US, Europe |
