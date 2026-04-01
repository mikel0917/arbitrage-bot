# Kalshi / Polymarket Arbitrage Bot 📊

> Real-time arbitrage detection across prediction markets — find the spread, surface the edge.

## Overview

This bot monitors Kalshi and Polymarket simultaneously for price discrepancies on matching markets. When a profitable arbitrage spread is detected, it surfaces the opportunity with calculated return, confidence, and sizing suggestions.

Built for speed — uses async polling and WebSocket connections to minimize latency between market reads.

---

## How It Works

```
Kalshi API  ──┐
               ├──→ [Market Matcher] ──→ [Spread Calculator] ──→ [Alert / Feed]
Polymarket ───┘
```

1. **Market matching** — maps equivalent contracts across both platforms by event/outcome
2. **Spread detection** — calculates implied probability gaps accounting for platform fees
3. **Opportunity scoring** — ranks by expected value, liquidity, and time to resolution
4. **Output** — real-time alerts and data feed

---

## Features

- Real-time price polling via REST APIs and WebSockets
- Cross-platform contract matching by event title and outcome keywords
- Fee-adjusted spread calculation (Kalshi ~2%, Polymarket variable)
- Configurable minimum EV threshold for alerts
- Historical spread logging for backtesting
- Clean data feed output for distribution

---

## Tech Stack

```
Python       → Core bot logic
REST APIs    → Kalshi API, Polymarket Gamma API
WebSockets   → Real-time price streaming
PostgreSQL   → Spread history and logging
Docker       → Containerized deployment
```

---

## Configuration

```env
KALSHI_API_KEY=your_key
MIN_SPREAD_PCT=0.03        # Minimum spread to surface (3%)
POLL_INTERVAL_SEC=5
ALERT_WEBHOOK=your_url     # Optional webhook for alerts
```

---

## Sample Output

```
[ARBIT] YES — "Fed raises rates Sep 2025"
  Kalshi:     62¢  (implied 62%)
  Polymarket: 57¢  (implied 57%)
  Spread:     5.0% after fees
  EV:         +$4.80 per $100 deployed
  Liquidity:  $12,400 available
  Time:       2025-09-17 (87 days)
```

---

## Setup

```bash
git clone https://github.com/mikel0917/arbitrage-bot
cd arbitrage-bot
pip install -r requirements.txt
cp .env.example .env
# Add your Kalshi API key
python main.py
```

---

> ⚠️ This bot is for data and research purposes. Always review platform terms before deploying capital.
