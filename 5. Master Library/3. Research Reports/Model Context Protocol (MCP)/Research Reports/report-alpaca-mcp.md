# Resource Report: Alpaca MCP

**URL:** https://alpaca.markets/mcp-server
**Site:** https://alpaca.markets/
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
Official MCP server from Alpaca Markets — an established commission-free trading API platform — enabling AI agents to execute trades and manage portfolios via natural language.

## What It Does
- Paper trading with simulated funds and real market data
- Live execution: fractional equities, crypto, ETFs, multi-leg options
- Switch paper → live by changing API keys only
- Forward-test validated Python strategies before live deployment
- Promoted prominently on Alpaca's homepage as their official AI trading integration

## MCP Tool Manifest

- **Tool count:** 43 tools (full Alpaca Trading API v2 coverage; organized into toolsets via ALPACA_TOOLSETS env var)
- **Tools (representative — full list in official docs):**
  - `get_account` — Get account details, buying power, and balance
  - `get_positions` — List all open positions
  - `get_position` — Get details of a specific position
  - `close_position` — Close a specific position
  - `close_all_positions` — Close all open positions
  - `get_orders` — List open or recent orders
  - `get_order` — Get details of a specific order
  - `create_order` — Place a new order (market, limit, stop, options, crypto)
  - `cancel_order` — Cancel an open order
  - `cancel_all_orders` — Cancel all open orders
  - `get_asset` — Get details of a specific tradeable asset
  - `search_assets` — Search for tradeable assets by symbol or keyword
  - `get_latest_quote` — Get latest bid/ask quote for an asset
  - `get_latest_trade` — Get the most recent trade for an asset
  - `get_bars` — Get historical OHLCV bar data for an asset
  - `get_snapshots` — Get snapshot data (quote + trade + bars) for multiple assets
  - `get_news` — Get financial news articles for specified symbols
  - `get_options_contracts` — Get options contracts chain for an underlying asset
  - `get_portfolio_history` — Get historical portfolio value and P&L data
  - `get_watchlists` — List all watchlists
  - `get_watchlist` — Get assets in a specific watchlist
  - *(plus ~22 additional tools covering crypto, fractional shares, corporate actions, and advanced order types)*
- **Transport type:** stdio
- **settings.json registration:**
```json
{
  "mcpServers": {
    "alpaca": {
      "command": "uvx",
      "args": ["alpaca-mcp-server"],
      "env": {
        "ALPACA_API_KEY": "your_alpaca_api_key",
        "ALPACA_SECRET_KEY": "your_alpaca_secret_key",
        "ALPACA_PAPER_TRADE": "true"
      }
    }
  }
}
```
- **Recommended serverInstructions:** "Alpaca MCP provides paper and live trading execution for stocks, ETFs, crypto, and options via Alpaca's API. Default to paper trading mode (ALPACA_PAPER_TRADE=true). Switch to live by swapping API keys — no code changes needed."

## Relevance to This Project
Forward-testing layer. Once a strategy is validated in NinjaTrader Market Replay and confirmed by Python backtesting, Alpaca provides the path to real forward-testing before live capital deployment. Paper trading with real data is the bridge between historical backtesting and live execution.

## Master Library Assessment
- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** Phase 2 — not needed until Python backtesting is validated. High value when ready to move from backtesting to forward-testing.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** Established trading platform (well-known in algo trading community), official MCP server promoted on their main site, API key-based authentication, paper/live switching is key-based only (no code changes). No malicious patterns detected.
- **Notes:** Live trading involves real capital — API key scoping is critical at setup. Use paper trading keys during development; live keys only when deploying validated strategies.

## Recommendation
Add to Section 4, Tier 2. Phase 2 install. Paper trading keys first; live keys only after full strategy validation.

---
*Report by Sophia | Session 31 | 2026-03-29*

---

## C&P Summary

Alpaca MCP is the official MCP server from Alpaca Markets, a well-established commission-free trading API platform. It allows AI agents to execute trades and manage portfolios via natural language, covering fractional equities, crypto, ETFs, and multi-leg options — with paper trading using real market data as the default mode and live execution available by swapping API keys. For this project, it serves as the forward-testing layer: the bridge between validated Python backtests and live capital deployment. Phase 2 install — not needed until backtesting is solid. Use paper trading keys throughout development; live keys only after full strategy validation.
