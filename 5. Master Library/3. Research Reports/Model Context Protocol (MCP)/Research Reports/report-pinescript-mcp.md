# Resource Report: PineScript MCP

**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
The old source listed two PineScript MCP options. Status has changed since the list was written — one option is gone, one remains with a significant license concern.

---

## Option A: PineScript Syntax Checker (erevus-cn)
**URL:** https://github.com/erevus-cn/pinescript-syntax-checker
**Status:** REPO REMOVED (404) — no longer available. Cannot be researched, installed, or used. Do not add to index.

---

## Option B: PineScript Strategy MCP (cklose2000)
**URL:** https://github.com/cklose2000/pinescript-mcp-server
**Stars:** 101 | **Forks:** 29 | **License:** PROPRIETARY — All Rights Reserved (Copyright © 2025)
**Status:** Low activity — 19 commits, last push 2025-07-30 (no updates in ~10 months as of June 2026), TypeScript/HTML/Python stack. No formal releases.

### What It Does
Full PineScript strategy development workflow: create, test, optimize, export. Backtest integration, performance analysis, parameter optimization, Claude integration for conversational development, web UI and desktop app options. Install via: `npx pinescript-mcp-server`.

### MCP Tool Manifest

- **Tool count:** ~8 tools (based on documented capabilities; proprietary license limits full tool schema visibility)
- **Tools:**
  - `validate_pinescript` — Validate PineScript code for syntax errors and warnings
  - `fix_pinescript_errors` — Automatically fix common PineScript syntax errors
  - `generate_strategy_template` — Generate a validated strategy template for a given pattern type
  - `generate_indicator_template` — Generate a validated indicator template
  - `create_backtest` — Create and run a backtest for a PineScript strategy
  - `get_backtest_results` — Retrieve performance metrics and trade log from a backtest
  - `optimize_parameters` — Run parameter sensitivity analysis on a strategy
  - `export_strategy` — Export a finalized PineScript strategy to file
- **Transport type:** stdio
- **settings.json registration:**
```json
{
  "mcpServers": {
    "pinescript_mcp": {
      "command": "npx",
      "args": ["pinescript-mcp-server"]
    }
  }
}
```
- **Recommended serverInstructions:** "PineScript MCP supports creating, validating, optimizing, and exporting PineScript trading strategies. Note: proprietary license (all rights reserved) — confirm terms before use. Backtest integration is built-in."

### Relevance to This Project
Todd's TradingView workflow. Would enable Claude to help create and optimize Pine Script strategies directly, with built-in backtest integration. Most complete PineScript development toolchain found.

### Soren Security Pre-check
- **Verdict:** FLAG — Proprietary License + Extended Inactivity
- **Checked:** 101 stars, 29 forks, 19 commits, last push 2025-07-30 (stalled — no updates in ~10 months as of June 2026). No malicious patterns detected in repository description.
- **Notes:** "Proprietary and confidential. All rights reserved." means no redistribution, no modification rights, no guaranteed long-term access. Use is at operator's discretion. Cannot be freely adopted without risk of access being revoked or terms changing.
- **Extended inactivity reinforcement (2026-06-08):** Last commit is now confirmed at July 2025 — over 10 months without a single update. For a proprietary-licensed tool with no redistribution rights, abandonment risk is not academic: if the repo goes dark, the team has no ability to fork, patch, or maintain it. The combination of proprietary license and stalled development means the operator is fully dependent on an author who has shown no activity for almost a year. This flag is stronger now than at original review. Operator decision required before install — and if an open-source alternative emerges at any point, it immediately displaces this entry.
- *Re-reviewed 2026-06-08 — FLAG verdict confirmed and reinforced. Extended inactivity (10+ months) added to flag conditions. Original proprietary license flag unchanged and still in force.*

## Master Library Assessment
- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** Only remaining PineScript MCP option. Proprietary license is a real concern — operator decision required before install. If accepted, Phase 2 alongside TradingView MCP.

## Recommendation
Add to Section 4, Tier 2 with FLAG. Operator must acknowledge proprietary license before installation. If a suitable open-source alternative emerges, replace this entry.

---
*Report by Sophia | Session 31 | 2026-03-29*

---

## C&P Summary

PineScript MCP is a community-built MCP server for full PineScript strategy development within Claude — covering creation, testing, optimization, export, backtest integration, and parameter sensitivity analysis, with both a web UI and desktop app option. It is the only remaining PineScript MCP option: the other candidate (erevus-cn/pinescript-syntax-checker) was removed (404) before the report was filed. The significant concerns are (1) the proprietary "All Rights Reserved" license — no redistribution rights, no modification rights, no guaranteed long-term access — and (2) low activity: last commit was July 2025, ~10 months before this sweep. Operator decision required before installation. If an open-source alternative emerges, this entry should be replaced. Section 4, Tier 2 with FLAG.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
