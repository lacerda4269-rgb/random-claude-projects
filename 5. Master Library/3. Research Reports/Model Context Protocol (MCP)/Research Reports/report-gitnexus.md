# Resource Report: GitNexus

**URL:** https://github.com/abhigyanpatwari/GitNexus
**Date Researched:** 2026-04-12
**Researched by:** Rose | Security pre-check: Soren | Filed by: Lexi
**Already in Master Library?** No — new item

---

## What It Is
GitNexus is a codebase knowledge graph tool that indexes any codebase into a queryable graph — mapping every dependency, call chain, cluster, and execution flow. Built by Abhigyan Patwari. Available as a CLI, MCP Server, and browser-based Web UI. Integrates natively with Cursor, Claude Code, and Codex via MCP.

## What It Does
Two primary interfaces: (1) CLI + MCP Server for local indexing with editor integration; (2) Web UI for browser-based graph exploration with no installation required. Parsing uses Tree-sitter (native bindings for CLI, WASM for web). Database layer is LadybugDB. 41,698 stars, 1,194 commits, 4,754 forks, active development. Latest release: v1.6.6 (2026-06-08).

Key capabilities relevant to refactoring:
- Maps blast radius before changes — prevents breaking hidden dependencies
- Identifies unused code clusters safe for removal
- Visualizes call chains to surface coupling
- Provides AI agents architectural context before they touch code

## MCP Tool Manifest

- **Tool count:** 7 tools + 2 guided prompts
- **Tools:**
  - `query` — Hybrid semantic + BM25 search across the indexed codebase knowledge graph
  - `context` — 360-degree view of a symbol: callers, callees, processes, and dependencies
  - `impact` — Blast radius analysis — identify what breaks if a given file or function changes
  - `detect_changes` — Pre-commit risk check: verify affected processes before committing
  - `rename` — Safe multi-file symbol rename using graph intelligence to find all references
  - `list_repos` — List all repositories currently indexed in the global GitNexus registry
  - `generate_map` — Auto-generate a Mermaid architecture diagram from the knowledge graph
- **Transport type:** stdio
- **settings.json registration:**
```json
{
  "mcpServers": {
    "gitnexus": {
      "command": "npx",
      "args": ["-y", "gitnexus@latest", "mcp"]
    }
  }
}
```
Note: Run `gitnexus analyze <repo-path>` first to build the graph; `gitnexus setup` auto-detects editors and writes config automatically.
- **Recommended serverInstructions:** "GitNexus provides codebase knowledge graph intelligence — query dependencies, analyze blast radius before edits, perform safe multi-file renames, and generate architecture diagrams. Run gitnexus analyze on a repo before using any tools."

## Relevance to This Project
Directly relevant when working with legacy or complex codebases — particularly when refactoring existing projects. The MCP integration with Claude Code means agents (Nick, Pete, Todd) could use it to understand a codebase before modifying it, rather than reading raw files and guessing at structure. Jay flagged it specifically for refactoring use.

## Master Library Assessment
- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** Strong value for codebase analysis and refactoring phases, but not a day-one tool — its usefulness scales with project complexity. MCP is its primary integration mode with Claude Code. Tier 2 for high value, phase-dependent use.

## Soren Security Pre-check
- **Verdict:** FLAG: Polyform Noncommercial license — free for personal and non-commercial use; commercial use requires a separate licensing agreement from akonlabs.com
- **Checked:** License (Polyform Noncommercial — confirmed), star count (41,698 — strong community signal, significant growth since original report), authorship (Abhigyan Patwari, active maintainer), commercial licensing availability (akonlabs.com), commit history (1,194 commits, active), tech stack (TypeScript, Tree-sitter, LadybugDB — all standard), MCP integration (confirmed for Claude Code)
- **Notes:** Tool is clean from a security standpoint — no malicious patterns, no unusual dependencies. The flag is purely on the license. For personal project use (which this appears to be), Polyform Noncommercial is fine. If any future project involves commercial activity, the operator should review the commercial licensing terms before use.
- *Re-reviewed 2026-06-08 — FLAG verdict confirmed. Rose freshness sweep shows significant growth (26.7k → 41,698 stars, 615 → 1,194 commits, latest release v1.6.6). Strong active development continues. Security posture unchanged; license flag unchanged.*

## Recommendation
File to Section 4 — MCP Servers, Tier 2, with the license flag attached. Operator decision: for personal use, proceed as-is. For any commercial project, confirm the Polyform Noncommercial terms apply before deploying.

---
*Report by Rose + Sage | Session 39 | 2026-04-12*

---

## C&P Summary

GitNexus is a codebase knowledge graph tool that indexes any codebase into a queryable graph — mapping every dependency, call chain, cluster, and execution flow. It is available as a CLI, MCP Server, and browser-based Web UI, with native MCP integration for Claude Code, Cursor, and Codex. The primary value for this team is pre-change analysis: before any agent touches a codebase, GitNexus can map the blast radius of proposed changes, identify unused code safe for removal, and visualize coupling that would otherwise be invisible from raw file reads. Flagged for licensing: Polyform Noncommercial license is fine for personal project use; commercial use requires a separate agreement from akonlabs.com. Section 4, Tier 2. 41,698 stars, 4,754 forks, 1,194 commits as of June 2026 — substantial growth confirming active development and strong community adoption.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
