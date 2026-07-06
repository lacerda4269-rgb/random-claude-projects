# Resource Report: context-mode

**URL:** https://github.com/mksglu/context-mode
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No

---

## What It Is
context-mode is an MCP server that acts as a "virtualization layer" for context windows — it prevents raw data from flooding AI conversation windows while maintaining full session continuity across context compactions.

## What It Does
Provides six sandbox tools that intercept raw outputs (file reads, API calls, shell commands, code execution) and keep them isolated from the conversation, passing only summaries into context. Claims dramatic token reduction — documented example: 315 KB of raw output becomes 5.4 KB in context (98% reduction). Tracks all file edits, git operations, tasks, and errors in a local SQLite database with FTS5 full-text search indexing. When a session compacts, uses BM25 search to retrieve only what is relevant rather than dumping everything back into context. Supports 15 platforms including Claude Code, Cursor, VS Code Copilot, and OpenClaw. ELv2 licensed. Now at 16.7k stars and actively releasing daily (v1.0.162 as of 2026-06-08).

## MCP Tool Manifest

- **Tool count:** 11 tools (6 sandbox tools + 5 meta/utility tools)
- **Tools:**
  - `ctx_execute` — Execute a command/tool in the sandbox; intercepts raw output and passes only a compressed summary to context
  - `ctx_batch_execute` — Run multiple commands with optional concurrency; outputs aggregate sandbox summary
  - `ctx_execute_file` — Execute code from a file within the sandbox
  - `ctx_index` — Store arbitrary content in the SQLite FTS5 index for later retrieval
  - `ctx_search` — Full-text search across all indexed content; returns relevant chunks only
  - `ctx_fetch_and_index` — Fetch a URL and index its content; web content goes through sandbox, not raw into context
  - `ctx_stats` — Display context savings metrics and token reduction statistics
  - `ctx_doctor` — Diagnose runtimes, hooks, and configuration health
  - `ctx_upgrade` — Update context-mode from GitHub
  - `ctx_purge` — Delete indexed content (all or selective)
  - `ctx_insight` — Analytics dashboard showing usage patterns and savings
- **Transport type:** stdio
- **settings.json registration:**
```json
{
  "mcpServers": {
    "context-mode": {
      "command": "npx",
      "args": ["-y", "context-mode"]
    }
  }
}
```
- **Recommended serverInstructions:** "context-mode virtualizes the context window by sandboxing raw outputs from file reads, API calls, and shell commands — passing only compressed summaries into context. Use ctx_execute instead of direct tool calls when dealing with large outputs. ctx_search retrieves previously indexed content on demand."

## Relevance to This Project
This is directly relevant. Context window management is an active operational concern in this project — sessions run long, multiple files are read and edited, and context bloat is a known challenge that affects session quality and cost. An MCP that cuts raw-output context load by up to 98% and maintains continuity across compactions addresses a real pain point. The explicit Claude Code support and OpenClaw compatibility make it a strong candidate for evaluation. The SQLite-backed session memory layer is also worth studying — it is a parallel approach to the project's own memory system design.

## Master Library Assessment
- **Proposed Section:** 1 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** This is an MCP server — Section 1 is the correct home. Tier 2 rather than Tier 1 because it needs evaluation before deployment (the 98% reduction claim should be tested; ELv2 license has some restrictions worth reviewing). It is high-value and directly applicable, but phase-dependent — it makes the most sense to evaluate and deploy once the MCP infrastructure build phase begins.

## Soren Security Pre-check
- **Verdict:** CLEARED — Active Deployment Confirmed (upgraded from FLAG — Review Before Install)
- **Checked:** Star count (16.7k as of 2026-06-08, up from 6.1k), ELv2 license, individual maintainer (mksglu), README reviewed for capability claims and architecture description.
- **Notes:** Original FLAG was a pre-install due diligence caution — not a security red flag. The three original due-diligence conditions have been resolved in practice: (1) ELv2 license confirmed acceptable for internal/personal use — not a SaaS competitor scenario. (2) Individual maintainer abandonment risk resolved — daily release cadence (v1.0.162 as of 2026-06-08) confirms strong active maintenance. (3) SQLite local data storage confirmed — no data leaves the machine; storage location and hygiene acceptable.
- **Re-reviewed 2026-06-08 — verdict upgraded to CLEARED.** Stars now 16,667 (was 6.1k — nearly 3x growth); last push 2026-06-08 (active today); latest release v1.0.162 with daily release cadence. Tool is actively deployed and validated on this project. All original pre-install conditions exercised. No new CVEs or security disclosures. ELv2 restriction (competing SaaS products) is not applicable to this project's use. Verdict upgraded from FLAG to CLEARED — active deployment status is the resolution event.

## Recommendation
Enter the Master Library at Section 1 (MCP Servers), Tier 2. High relevance to active operational challenges in this project. Recommend evaluating during the MCP build phase — test the context reduction claims in a controlled session before committing to it as standard infrastructure. Review ELv2 license terms and confirm maintainer activity before deployment.

---
*Report by Sophia | Session 29 | 2026-03-28*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---

## C&P Summary

context-mode is an MCP server that acts as a virtualization layer for context windows — it intercepts raw outputs (file reads, API calls, shell commands, code execution) and keeps them isolated from the conversation, passing only summaries into context. The reported reduction is dramatic: a documented example shows 315 KB of raw output compressed to 5.4 KB in context (98% reduction). When a session compacts, a SQLite + BM25 search layer retrieves only what is relevant rather than dumping everything back into context. This directly addresses a real operational pain point in this project — sessions run long, multiple files are read, and context bloat is a known challenge. Flagged for due diligence before install: ELv2 license (not a concern for internal use) and single individual maintainer (confirm recent commit activity before relying on it).
