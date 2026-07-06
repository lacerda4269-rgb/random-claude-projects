# Resource Report: Alpha Vantage MCP

**URL:** https://mcp.alphavantage.co/mcp
**Site:** https://www.alphavantage.co/
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
Official MCP server from Alpha Vantage — a Y Combinator-backed, NASDAQ-licensed US market data provider — giving AI assistants direct access to financial market data via natural language.

## What It Does
- Real-time and historical data: stocks, ETFs, mutual funds, forex, commodities, crypto
- 50+ technical indicators (RSI, MACD, SMA, and more)
- Economic calendar for smarter time filters
- Global market news API with AI sentiment analysis
- Fundamental data and multi-instrument research
- Free API key tier available (alphavantage.co registration)

## MCP Tool Manifest

- **Tool count:** ~15 tools (categories: stocks, forex, crypto, technical indicators, economic data, fundamentals, news/sentiment)
- **Tools (representative — full list via TOOL_LIST discovery):**
  - `get_stock_quote` — Real-time or intraday stock price, volume, and change data
  - `get_time_series_daily` — Daily OHLCV bar data for a given symbol
  - `get_time_series_weekly` — Weekly OHLCV bar data
  - `get_company_overview` — Fundamental company data (sector, market cap, P/E, etc.)
  - `get_technical_indicator` — Any of 50+ indicators (RSI, MACD, SMA, EMA, Bollinger, etc.) with configurable period
  - `get_forex_rate` — Real-time forex exchange rate between two currencies
  - `get_crypto_rate` — Real-time crypto exchange rate
  - `get_crypto_series` — Daily/weekly/monthly crypto price series
  - `get_options_chain` — Real-time options chain with Greeks and implied volatility
  - `get_historical_options` — Historical options chain data with filtering
  - `get_etf_profile` — ETF holdings, sector allocation, and performance data
  - `get_news_sentiment` — News articles with AI-scored sentiment for a symbol
  - `get_economic_indicator` — Macro economic indicators (CPI, unemployment, GDP, etc.)
  - `get_earnings_calendar` — Upcoming earnings release calendar
  - `get_ipo_calendar` — Upcoming IPO listings
- **Transport type:** Streamable HTTP (remote endpoint at `https://mcp.alphavantage.co/mcp`)
- **settings.json registration:**
```json
{
  "mcpServers": {
    "alpha-vantage": {
      "type": "http",
      "url": "https://mcp.alphavantage.co/mcp?apikey=YOUR_API_KEY"
    }
  }
}
```
- **Recommended serverInstructions:** "Alpha Vantage MCP provides financial market data including real-time and historical stock, forex, crypto, ETF data, 50+ technical indicators, economic calendar, and AI-powered news sentiment. Free API key available at alphavantage.co."

## Relevance to This Project
Market data layer for strategy research and backtesting context. Useful for understanding what was happening in the market on days when strategies over- or under-perform. Economic calendar integration helps build smarter time filters.

## Master Library Assessment
- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** Phase 2 — not needed until core trading loops are validated. High value once data research becomes part of the workflow.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** Established company (YC-backed, NASDAQ-licensed), dedicated MCP endpoint at mcp.alphavantage.co, API key authentication (scoped access), well-documented API. No malicious patterns detected.
- **Notes:** API endpoint requires authentication — 401 returned without key (expected behavior, not a red flag). Free tier available; paid tiers for higher rate limits.

## Recommendation
Add to Section 4, Tier 2. Phase 2 install after core trading loop is validated.

---
*Report by Sophia | Session 31 | 2026-03-29*

---

## C&P Summary

Alpha Vantage MCP is the official MCP server from Alpha Vantage, a Y Combinator-backed, NASDAQ-licensed US market data provider. It gives AI assistants direct natural language access to real-time and historical data across stocks, ETFs, forex, commodities, and crypto — plus 50+ technical indicators, an economic calendar, and AI-powered news sentiment analysis. For this project, it functions as the market data and research layer: understanding what was happening in the market on days when strategies over- or under-perform, and building smarter time filters using the economic calendar. Free API key available. Phase 2 install after core trading loops are validated.
