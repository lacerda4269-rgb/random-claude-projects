# Resource Report: claude-mem

> ⚠️ **REMOVED FROM STACK — Session 251 (2026-06-13).** claude-mem was installed Session 239, never functioned (Bun worker blocked/uninitialized on this host), and was uninstalled completely in Session 251. Its only function — a session-activity timeline — is fully covered by claude-remember, context-mode `ctx_search`, Graphify, and Sophia's Session Summary. This report is retained as a research record only. Removal plan: `~/.claude/plans/that-took-away-to-validated-sunrise.md`.

**URL:** https://github.com/thedotmack/claude-mem
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No

---

## What It Is
claude-mem is a persistent memory MCP plugin for Claude Code that automatically captures, compresses, and surfaces context from coding sessions so it is available in future conversations.

## What It Does
It records tool usage and observations throughout a session, then uses Claude's agent SDK to generate semantic summaries that persist across sessions. A "3-layer workflow" with 4 MCP tools provides token-efficient memory retrieval. A real-time web UI runs at `http://localhost:37777` for inspecting stored memories. Privacy controls allow users to exclude sensitive content via `<private>` tags. Built with TypeScript, Node.js, Bun, SQLite, and Chroma (vector database) for hybrid semantic search. AGPL-3.0 license (with Ragtime sub-component under PolyForm Noncommercial). Version 13.4.1, 81.2k stars, 7.0k forks — actively maintained with documentation at `docs.claude-mem.ai`.

## MCP Tool Manifest

- **Tool count:** 4 tools (token-efficient 3-layer workflow pattern)
- **Tools:**
  - `search` — Full-text search of the memory index; returns compact summary table (~50–100 tokens per result) with IDs, titles, dates, and types; supports filtering by type/date/project
  - `timeline` — Retrieve chronological context around a specific observation or query; parameters: anchor (observation ID), depth_before, depth_after
  - `get_observations` — Fetch full observation details by IDs; always batch multiple IDs in a single call for token efficiency
  - `save_memory` — Manually save a specific piece of information as a persistent memory entry (triggered by user or agent)
- **Transport type:** stdio (MCP server at `~/.claude/plugins/marketplaces/thedotmack/plugin/scripts/mcp-server.cjs`)
- **settings.json registration:**
```json
{
  "mcpServers": {
    "claude-mem": {
      "command": "node",
      "args": ["${HOME}/.claude/plugins/marketplaces/thedotmack/plugin/scripts/mcp-server.cjs"]
    }
  }
}
```
Note: Preferred install method is `npx claude-mem install` which handles registration automatically. Manual path configuration above is for reference only — use the install command in practice.
- **Recommended serverInstructions:** "claude-mem provides persistent memory across coding sessions. Use search to find past context, timeline for chronological context around a specific observation, and get_observations to retrieve full details. Always batch IDs in get_observations calls."

## Relevance to This Project
Directly relevant — the project already has a manual MEMORY.md system (this file's project uses it). claude-mem is the automated version of that pattern: it captures what Claude does during sessions and makes it searchable later. The key question is whether it complements or competes with the existing MEMORY.md approach. Assessment: these are different layers. MEMORY.md captures strategic decisions and project state (human-curated, Sage-owned). claude-mem captures operational session activity (tool calls, observations — machine-captured). They could coexist cleanly. Worth evaluating when the project scales to the point where manual memory curation becomes a bottleneck.

## Master Library Assessment
- **Proposed Section:** 1 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** This is an MCP server — exactly Section 1. Tier 2 because the current project's memory needs are met by the existing MEMORY.md system. Becomes Tier 1 when scaling demands automated memory capture.

## Soren Security Pre-check
- **Verdict:** FLAG
- **Checked:** Repo age (active 2026), star count (81.2k as of 2026-06-08, up from 41.9k at research date), fork count (7.0k, up from 3.1k), AGPL-3.0 + PolyForm Noncommercial dual-licensing, TypeScript/SQLite/Chroma stack, author "thedotmack" (unverified identity), local-first architecture
- **Notes:** FLAG for licensing, not security. AGPL-3.0 means any derivative networked service must be open-source. The Ragtime sub-component under PolyForm Noncommercial is non-commercial-only — if this project ever becomes commercial, that component requires a separate license. The local-first architecture (SQLite, localhost web UI) means no data leaves the machine by default — positive signal. No malicious patterns detected. Flagging licensing complexity so it is documented before any production use.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Stars now 81.2k (nearly doubled from 41.9k at research date); last push 2026-06-08; latest release v13.4.1 (released today). Explosive adoption — strong signal the tool is in active production use broadly. No new CVEs or security disclosures. FLAG for licensing complexity (AGPL-3.0 + PolyForm Noncommercial) remains the correct posture. Conditions unchanged — confirm commercial licensing terms with Ragtime before any commercial deployment.

## Recommendation
Enter the library in Section 1 at Tier 2 with a Soren licensing flag. Revisit when the project scales and manual memory curation becomes a bottleneck. Confirm commercial licensing terms with Ragtime before any commercial deployment.

---
*Report by Sophia | Session 29 | 2026-03-28*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---

## C&P Summary

claude-mem is a persistent memory MCP plugin for Claude Code that automatically captures, compresses, and surfaces context from coding sessions across conversations. It records tool usage and observations throughout a session, uses Claude's agent SDK to generate semantic summaries, and stores them in a SQLite + Chroma vector database for hybrid semantic search — with a localhost web UI for inspection. For this project, it sits alongside the existing MEMORY.md system as a complementary layer: MEMORY.md holds human-curated strategic decisions (Sage-owned), while claude-mem captures machine-level operational session activity. Worth evaluating when the project scales and manual memory curation becomes a bottleneck. Flagged for licensing complexity — AGPL-3.0 main license plus a PolyForm Noncommercial sub-component that requires a separate license for any commercial deployment.
