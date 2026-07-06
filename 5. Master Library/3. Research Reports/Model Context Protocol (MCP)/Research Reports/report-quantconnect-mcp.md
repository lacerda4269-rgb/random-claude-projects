# Resource Report: QuantConnect MCP

**URL:** https://github.com/QuantConnect/mcp-server
**Docs:** https://www.quantconnect.com/mcp
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
Official Python MCP server from QuantConnect — bridges AI agents to QuantConnect's quantitative trading platform for full algorithmic strategy lifecycle management.

## What It Does
- 60+ fully implemented and tested API endpoints
- Project management: create, edit, compile
- Documentation reference with vector search across docs and API examples
- Static code analysis and syntax checking
- Backtesting: autonomous strategy testing
- Parameter optimization: sensitivity testing
- Live trading: deploy and manage strategies
- Install via Docker (`docker pull quantconnect/mcp-server`) or PyPI (`uvx quantconnect-mcp`)
- Requires QuantConnect account credentials (free tier available)

## MCP Tool Manifest

- **Tool count:** 60+ tools (full QuantConnect API coverage; organized by lifecycle phase)
- **Tools (representative by phase):**
  - `create_project` — Create a new strategy project in the default organization
  - `read_file` — Read a file from a QuantConnect project
  - `update_file_contents` — Write or update code in a project file
  - `compile_project` — Compile a strategy project and get error/warning output
  - `create_backtest` — Submit a new backtest request and return the backtest ID
  - `read_backtest` — Retrieve full backtest results including metrics
  - `list_backtests` — List all backtests for a given project
  - `read_backtest_chart` — Retrieve equity curve or chart data from a backtest
  - `read_backtest_orders` — Retrieve order history from a backtest
  - `read_backtest_insights` — Retrieve alpha insights from a backtest
  - `optimize_parameters` — Run parameter sensitivity and optimization sweep
  - `search_documentation` — Vector search across QuantConnect docs and API examples
  - `deploy_live` — Deploy a compiled strategy to live trading
  - `list_live_algorithms` — List all currently live-deployed strategies
  - `stop_live_algorithm` — Stop a live-running strategy
  - `get_project` — Retrieve project metadata and file structure
  - `list_projects` — List all projects in the organization
  - *(additional tools covering data downloads, portfolio management, and notifications)*
- **Transport type:** stdio (Docker: `docker pull quantconnect/mcp-server`) or PyPI (`uvx quantconnect-mcp`)
- **settings.json registration:**
```json
{
  "mcpServers": {
    "quantconnect": {
      "command": "uvx",
      "args": ["quantconnect-mcp"],
      "env": {
        "QUANTCONNECT_USER_ID": "your_user_id",
        "QUANTCONNECT_API_TOKEN": "your_api_token"
      }
    }
  }
}
```
- **Recommended serverInstructions:** "QuantConnect MCP provides the full algorithmic trading strategy lifecycle — project management, code editing, compilation, backtesting, parameter optimization, and live deployment. Requires a QuantConnect account (free tier available). Live deployment tools require validated strategy + appropriate API permissions."

## Relevance to This Project
Optional expansion platform. If the build ever expands beyond NinjaTrader to a second trading platform or requires Python-native backtesting with cloud execution, QuantConnect has one of the more mature AI integrations in the trading space. Not needed for the current NinjaTrader-first stack.

## Master Library Assessment
- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** Phase 3, optional expansion only. Current focus is NinjaTrader. Add now for awareness; activate only if platform expansion is decided.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** Official QuantConnect organization repo, active maintenance (last push 2026-05-07), 74 stars, 31 forks, 16 open issues, 60+ tested API endpoints documented, credential-based authentication, Docker and PyPI install paths, open-source. Latest release: 0.0.10 (2025-08-22). No malicious patterns detected.
- **Notes:** Live trading features require API credentials with appropriate permissions — scope carefully at setup.
- *Re-reviewed 2026-06-08 — verdict confirmed. Rose freshness sweep confirms active maintenance (last push 2026-05-07, current as of sweep date). Official QuantConnect organization. Security posture unchanged.*

## Recommendation
Add to Section 4, Tier 2. Phase 3 optional. Install only if expanding beyond NinjaTrader.

---
*Report by Sophia | Session 31 | 2026-03-29*

---

## C&P Summary

QuantConnect MCP is the official Python MCP server from QuantConnect, a quantitative trading platform with a free tier. It bridges AI agents to the full QuantConnect strategy lifecycle — project management, documentation reference with vector search, static code analysis, autonomous backtesting, parameter optimization, and live strategy deployment — across 60+ fully implemented and tested API endpoints. For this project, it is an optional expansion platform: relevant only if the build ever grows beyond NinjaTrader to a second trading platform or needs Python-native backtesting with cloud execution. Phase 3 and conditional — do not install unless platform expansion is decided. Official QuantConnect source, 74 stars, 31 forks, v0.0.10 (Aug 2025), active as of May 2026, cleared with no concerns.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
