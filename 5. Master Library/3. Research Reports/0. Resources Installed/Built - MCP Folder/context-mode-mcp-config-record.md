# context-mode MCP — Config Record

**Tool:** context-mode (mksglu)
**Version:** 0
**Wired:** Project root `.mcp.json` — P7 Sandbox install queue
**Wired by:** Sage (CEO)
**Security status:** CLEARED — Active Deployment Confirmed (Soren, re-review 2026-06-08; upgraded from FLAG — Review Before Install)
**Research report:** Section 6 → 1. Research Reports → report-context-mode.md

---

## .mcp.json config (project-level)

Wired to `.mcp.json` in project root alongside playwright and elevenlabs-mcp. Transport is **stdio**. The Windows `cmd /c` wrapper is required so the npx launch resolves correctly under Claude Code on this host.

```json
{
  "mcpServers": {
    "context-mode": {
      "command": "cmd",
      "args": ["/c", "npx", "-y", "context-mode"]
    }
  }
}
```

**Note:** the live config uses `cmd /c npx -y context-mode` rather than the report's documented `npx -y context-mode` snippet — the `cmd /c` wrapper is the Windows-host launch form. No API key required.

## Transport

**stdio** — npx auto-downloads/refreshes the package on each run (daily release cadence). No separate binary install required.

## Tool count

11 tools (6 sandbox tools + 5 meta/utility tools): `ctx_execute`, `ctx_batch_execute`, `ctx_execute_file`, `ctx_index`, `ctx_search`, `ctx_fetch_and_index`, `ctx_stats`, `ctx_doctor`, `ctx_upgrade`, `ctx_purge`, `ctx_insight`. Virtualizes the context window by sandboxing raw outputs (file reads, API calls, shell commands, code execution) and passing only compressed summaries into context; SQLite + FTS5 (BM25) retrieval layer restores only relevant content across compactions.

## Primary use

Context-window virtualization and session continuity across compactions. `ctx_search` is the session-start retrieval tool (replaces the dropped claude-mem timeline — Session 251). Directly relevant to active context-bloat management on this project.

---

*Config record by Sophia (COO) — Session 265. Created this session — the record was referenced in the install-master-list (context-mode promoted to MCP #22) but had never been physically written; this is the first copy. Pulled verbatim from `.mcp.json` (project root) + report-context-mode.md.*
