# Resource Report: Finnhub MCP

**URL (primary):** https://github.com/cfdude/mcp-finnhub
**Alternatives found:** https://github.com/NimbleBrainInc/mcp-finnhub | https://github.com/SalZaki/finnhub-mcp (C#)
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
A Python MCP server providing access to Finnhub's financial market data API — news, sentiment, real-time quotes, technical indicators, and fundamentals. Multiple community implementations exist; none has strong adoption yet.

## What It Does
- 100+ Finnhub API endpoints exposed as 15 MCP tools
- Real-time market quotes, 50+ technical indicators
- Financial fundamentals and alternative data
- News and sentiment layer: understand strategy underperformance via news events, earnings releases, economic reports
- Project-based data storage with automatic exports
- Requires free Finnhub API key (finnhub.io)

## MCP Tool Manifest

- **Tool count:** 15 tools (100+ Finnhub API endpoints mapped into 15 categorized tools)
- **Tools:**
  - `finnhub_stock_market_data` — Real-time quotes, intraday/historical candles, tick data, BBO, market status
  - `finnhub_technical_analysis` — 50+ technical indicators (RSI, MACD, SMA, EMA), pattern recognition, trading signals
  - `finnhub_news_sentiment` — Company news, market news, AI-scored sentiment analysis
  - `finnhub_stock_fundamentals` — Financial statements, earnings history, dividends, key metrics
  - `finnhub_stock_estimates` — Revenue/EPS analyst estimates, price targets, recommendation trends
  - `finnhub_stock_ownership` — Insider trades, institutional holdings, fund ownership data
  - `finnhub_alternative_data` — ESG scores, social sentiment, supply chain intelligence
  - `finnhub_sec_filings` — SEC filing documents, earnings call transcripts
  - `finnhub_crypto_data` — Crypto exchange listings, symbol metadata, profiles, candle history
  - `finnhub_forex_data` — Forex exchange rates, currency candles, exchange metadata
  - `finnhub_calendar_data` — IPO calendar, earnings release calendar, economic event calendar
  - `finnhub_project_create` — Create a project workspace with .project.json metadata for data organization
  - `finnhub_project_list` — List all projects with file counts and statistics
  - `finnhub_job_status` — Check background job status and retrieve results
  - `finnhub_symbol_lookup` — Search for stock, ETF, or crypto symbols by name or keyword
- **Transport type:** stdio
- **settings.json registration:**
```json
{
  "mcpServers": {
    "finnhub": {
      "command": "mcp-finnhub",
      "env": {
        "FINNHUB_API_KEY": "your_finnhub_api_key",
        "FINNHUB_STORAGE_DIR": "/path/to/finnhub-data"
      }
    }
  }
}
```
- **Recommended serverInstructions:** "Finnhub MCP provides financial market data including quotes, candles, 50+ indicators, news/sentiment, fundamentals, insider trades, and earnings/IPO calendars. Free API key required (finnhub.io). Community-built (cfdude) with low star count — validate against higher-adoption alternatives."

## Relevance to This Project
News and sentiment context on top of market data. Helps build smarter time filters around high-impact events. Secondary to core trading stack — most useful when strategy research and refinement phase begins.

## Master Library Assessment
- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** Phase 2, secondary data layer. Functional but low community validation — monitor for a more mature implementation.

## Soren Security Pre-check
- **Verdict:** FLAG — Low community validation + stagnation risk (elevated)
- **Checked:** Primary repo (cfdude/mcp-finnhub): 9 stars (was 3), 4 forks, MIT license, Python. No malicious patterns detected.
- **Notes:** 9 stars is still minimal community validation. Alternatives exist (NimbleBrainInc, SalZaki) but none significantly better validated. Last push 2026-03-17 — no commits in nearly 3 months as of 2026-06-08; low activity risk. Recommend operator acknowledge low adoption before install. Revisit when a higher-adoption option emerges.
- **Re-reviewed 2026-06-08 — FLAG confirmed, stagnation risk elevated.** Stars now 9 (was 5 at April freshness review, 3 at original research) — negligible growth over 3 months. Last push remains 2026-03-17 — no commits in ~83 days as of today. The stagnation concern flagged by Rose is real and confirmed: this repo shows all signs of low-priority maintenance or soft abandonment. The original FLAG stood on low community validation; the stagnation data adds a second independent reason to hold. **Recommendation: do not install. Flag to Sage for a direction decision — either wait for this repo to show renewed activity, or select a higher-adoption alternative (Lambda Finance MCP, Alpha Vantage official MCP) before committing to a Finnhub-specific implementation.**

## Recommendation
Add to Section 4, Tier 2 with FLAG. Primary source: cfdude/mcp-finnhub. Operator aware of low community adoption. Monitor for a more widely-adopted Finnhub MCP to replace this entry.

---

## Rose's Freshness Review

**Date reviewed:** 2026-04-14 | **Reviewed by:** Rose

**What changed (2026-04-14):** Stars ticked up from 3 to 5 — still very low. Two notable competing alternatives have emerged: `SalZaki/finnhub-mcp` (C# SDK with real-time SSE streaming) and `catherinedparnell/mcp-finnhub` (simpler, more accessible). More importantly, the financial MCP space has matured — Lambda Finance MCP has emerged as a strong broader-coverage alternative to Finnhub-specific tools. Alpha Vantage now has an official vendor-maintained MCP server as well.

**C&P Summary:** This MCP server connects Claude directly to Finnhub's financial data API. Once it's set up, you can ask Claude for live stock quotes, technical indicators (RSI, MACD, 50+ others), earnings reports, insider trading activity, ESG scores, crypto exchange data, and forex rates — all without leaving your chat window. It covers 100+ Finnhub API endpoints wrapped into 15 MCP tools, with automatic CSV and JSON export. The catch: Finnhub requires a free API key for basic access and a paid plan for real-time data — you configure that key separately before the tool works. Community validation is still low (5 stars) and better-validated alternatives now exist.

**Updated recommendation:** If Finnhub data specifically is the requirement, this remains functional. If broader financial data coverage is the actual goal, Lambda Finance MCP is the stronger 2026 option and worth comparing before committing to Finnhub. Decision still belongs to Jay — hold until trading data source architecture is decided.

---
*Report by Sophia | Session 31 | 2026-03-29*
*Rose Freshness Review — Session 42 | 2026-04-14*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---

## C&P Summary

This MCP server connects Claude directly to Finnhub's financial data API. Once it's set up, you can ask Claude for live stock quotes, technical indicators (RSI, MACD, 50+ others), earnings reports, insider trading activity, ESG scores, crypto exchange data, and forex rates — all without leaving your chat window. It covers 100+ Finnhub API endpoints wrapped into 15 MCP tools, with automatic CSV and JSON export. The catch: Finnhub requires a free API key for basic access and a paid plan for real-time data — you configure that key separately before the tool works. Community validation is still low (5 stars) and better-validated alternatives now exist — Lambda Finance MCP is the stronger 2026 option if broader financial data coverage is the actual goal.
