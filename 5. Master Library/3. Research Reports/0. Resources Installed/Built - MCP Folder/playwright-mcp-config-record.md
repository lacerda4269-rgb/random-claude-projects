# Playwright MCP — Config Record

**Tool:** @playwright/mcp (Microsoft)
**Version:** 0
**Wired:** 2026-06-04 — Session 217
**Wired by:** Sage (CEO) — P7 Sandbox install queue
**Security status:** Cleared — Soren (Round 3, 2026-05-02; freshness confirmed Session 213)
**Research report:** Section 6 → 1. Research Reports → report-playwright-mcp.md

---

## .mcp.json config (project-level)

Added to `.mcp.json` in project root alongside context-mode:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp@latest"]
    }
  }
}
```

**Note:** `mcpServers` key in `settings.json` is not valid per Claude Code schema — MCP servers belong in `.mcp.json`. The research report showed a `settings.json` snippet (now outdated). Correct placement confirmed this session.

## Transport

stdio — npx auto-downloads the package on first use. No separate binary install required.

## Tool count

66 tools (June 2026). Accessibility-tree based. No vision model required.

---

*Config record by Sage (CEO) — Session 217, 2026-06-04.*
