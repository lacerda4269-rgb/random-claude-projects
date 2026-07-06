# Resource Report: TradingView MCP

**URL:** https://github.com/atilaahmettaner/tradingview-mcp
**Date Researched:** 2026-03-29 | **Updated:** 2026-06-08
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia (v1.0) / Rose (v1.1)
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
A community-built Python MCP server providing AI-powered market analysis through TradingView data — the most active and complete TradingView MCP found in current research.

## What It Does
- Real-time crypto and stock screening across exchanges
- 30+ technical indicators (multi-timeframe)
- Backtesting across six built-in strategies
- Multi-exchange support: Binance, KuCoin, Bybit, US equity markets (Bybit added since original report)
- Reddit sentiment analysis integration
- Live financial news feeds (Yahoo Finance)
- No API keys required for core functionality
- Last commit: March 29, 2026 (day of research — extremely active)

## MCP Tool Manifest

- **Tool count:** ~10 tools (community-built; no official tool registry document; based on README capabilities)
- **Tools:**
  - `top_gainers` — Screen for top gaining stocks or crypto across configured exchanges
  - `top_losers` — Screen for top losing stocks or crypto
  - `bollinger_scan` — Scan for assets matching Bollinger Band criteria (squeeze, breakout, etc.)
  - `coin_analysis` — Full technical analysis of a crypto coin including 30+ indicators
  - `consecutive_candles_scan` — Find assets with a specified number of consecutive up/down candles
  - `get_technical_indicators` — Retrieve 30+ technical indicators for a symbol on a given timeframe
  - `run_backtest` — Run one of six built-in backtesting strategies on historical data
  - `get_news_sentiment` — Fetch Reddit sentiment analysis for a symbol
  - `get_financial_news` — Fetch live financial news via Yahoo Finance feed
  - `get_webhook_data` — Read incoming TradingView webhook alert data
- **Transport type:** stdio (Python MCP server, install via uv or pip)
- **settings.json registration:**
```json
{
  "mcpServers": {
    "tradingview-mcp": {
      "command": "uv",
      "args": [
        "run",
        "--with", "mcp[cli]",
        "--with", "tradingview-ta",
        "python", "-m", "tradingview_mcp"
      ]
    }
  }
}
```
- **Recommended serverInstructions:** "TradingView MCP provides real-time market screening, 30+ technical indicators, backtesting across six strategies, Reddit sentiment, and news feeds. No API key required for core functionality. Community-built — monitor for maintenance continuity."

## Relevance to This Project
Cross-platform signal validation (NT ↔ TradingView ↔ Python). Multi-instrument screening. Pine Script strategy development support. Webhook listener for routing TradingView alerts to other systems. Note: this is a community implementation, not an official TradingView product — no official TradingView MCP exists as of research date.

## Master Library Assessment
- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** Phase 2 — needed when TradingView workflow begins. Best available option; community-built but highly active.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked (updated 2026-06-08):** Stars (3,028 — up from 482 at original clearance; 6x growth in ~10 weeks), forks (651 — up from 131), MIT license (permissive, confirmed), last pushed (2026-06-05 — 3 days before update, still active), open issues (10 — low), Python codebase, maintainer (atilaahmettaner — individual developer, active public GitHub, consistent commit history), no API keys required for core functionality, Bybit integration added since original clearance, new tool additions reviewed (candlestick patterns, Bybit exchange — no unexpected network endpoints or security concerns introduced), no malicious patterns detected in expanded codebase review
- **Notes:**
  1. Significant growth (482 → 3,028 stars in 10 weeks) prompted this re-check. Expanded community scrutiny is a net positive security signal — no new security issues surfaced at scale.
  2. Bybit exchange integration: adds one new data source connection; same architecture as existing integrations (no API key required for read-only market data). No elevated risk.
  3. Still a single-developer project — watch for maintainer burnout or abandonment as community expectations scale. Not a current concern (10 open issues, active commits) but flagged for the next review cycle.
  4. Community implementation, not official TradingView. No official TradingView MCP exists — this remains the best available option.
  5. Original CLEARED verdict confirmed. No conditions added.

*Reviewed by Soren | 2026-06-08*

## Recommendation
Add to Section 4, Tier 2. Note it is community-built. Phase 2 install alongside PineScript MCP.

---
*Report by Sophia | Session 31 | 2026-03-29*

---

---

## Report Version Log

| Version | Date | What Changed |
|---------|------|--------------|


## C&P Summary

TradingView MCP is a community-built Python MCP server providing AI-powered market analysis through TradingView data — real-time crypto and stock screening, 30+ multi-timeframe technical indicators, backtesting across six built-in strategies, Reddit sentiment analysis, and live financial news feeds. No API keys required for core functionality. For this project, it enables cross-platform signal validation between NinjaTrader, TradingView, and Python — plus multi-instrument screening and a webhook listener for routing TradingView alerts to other systems. Note: this is not an official TradingView product; no official TradingView MCP existed as of the research date. Phase 2 install alongside PineScript MCP. MIT license, community-built, individual developer. Stars grew from 482 to 3,028 in 10 weeks (updated 2026-06-08) — strong community uptake. Still single-developer; monitor for continued maintenance at scale. Bybit now supported in addition to Binance and KuCoin.

*Updated by Rose | Session 230 | 2026-06-08*