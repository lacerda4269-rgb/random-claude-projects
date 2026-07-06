# Resource Report: code-review-graph — Local Knowledge Graph MCP for Claude Code

**URL:** https://github.com/tirth8205/code-review-graph
**Date Researched:** 2026-04-18
**Researched by:** Rose | Security pre-check: Soren (pending) | Report by: Rose
**Already in Master Library?** No — Rose Research Round 2 (Session 60)

---

## What It Is
A local knowledge graph tool that parses a codebase into a persistent structural map, then exposes that map to Claude Code via MCP — so Claude reads only the relevant code rather than the entire repository.

## What It Does
- Parses repository source code using Tree-sitter into an Abstract Syntax Tree; extracts nodes (functions, classes, imports) and edges (calls, inheritance, test coverage relationships)
- Persists the graph in a local SQLite database in a .code-review-graph/ directory — no external dependencies
- Computes blast radius analysis: identifies which files and functions are affected by a given change, so Claude reads only relevant code during reviews
- Applies community detection (Leiden algorithm) and centrality measures to the graph for deeper structural analysis
- Exposes 28 MCP tools to Claude Code: impact analysis, graph queries, semantic search, dependency chain traversal, test coverage gap identification
- Incremental updates on file edits and commits — under 2 seconds for subsequent builds after initial parse
- Benchmarks: average 8.2x token reduction; description claims 6.8x on reviews and up to 49x on daily coding tasks
- Supports Claude Code, Cursor, Windsurf, Zed, Continue, and other MCP-compatible environments
- Setup: three commands — pip install code-review-graph, code-review-graph install (auto-detects platform), code-review-graph build
- **Stars:** 18,219 | **Forks:** 1,958 | **Language:** Python | **License:** MIT
- **Created:** 2026-02-26 | **Last pushed:** 2026-05-25 | **Latest release:** v2.3.5 | **Maintainer:** tirth8205 (actively maintained)

## MCP Tool Manifest

- **Tool count:** 28 tools (configurable via --tools flag or CRG_TOOLS env var; all read-only by design)
- **Tools (confirmed names — partial list; full list in docs/COMMANDS.md or via `code-review-graph serve --help`):**
  - `get_minimal_context_tool` — Ultra-compact context summary (~100 tokens); recommended first call before any code review
  - `get_impact_radius_tool` — Blast radius of changed files — identifies which functions and modules are affected
  - `get_review_context_tool` — Token-optimized review context with structural summary for PR or diff review
  - `query_graph_tool` — Query callers, callees, tests, imports, and inheritance relationships for any node
  - `traverse_graph_tool` — BFS/DFS graph traversal from any node with configurable token budget
  - `semantic_search_nodes_tool` — Search code entities by name or semantic meaning using embeddings
  - `embed_graph_tool` — Compute vector embeddings for semantic search (run once after build)
  - `build_or_update_graph_tool` — Build the initial graph or incrementally update after file edits
  - `list_graph_stats_tool` — Graph health and size metrics (node count, edge count, last updated)
  - `get_docs_section_tool` — Retrieve project documentation sections from indexed docs
  - `detect_changes_tool` — Pre-commit check identifying affected processes from pending changes
  - *(plus ~17 additional tools for community detection, centrality analysis, test coverage gap identification, import chain traversal, and dependency queries)*
- **Transport type:** stdio
- **settings.json registration:**
```json
{
  "mcpServers": {
    "code-review-graph": {
      "command": "code-review-graph",
      "args": ["serve"]
    }
  }
}
```
Note: Run `pip install code-review-graph` then `code-review-graph build` in the target repo before first use. Subsequent builds are incremental (under 2 seconds).
- **Recommended serverInstructions:** "code-review-graph provides a persistent structural map of the codebase for token-efficient code reviews. Always call get_minimal_context_tool first, then query_graph_tool or get_review_context_tool as needed. Do not use this MCP for write operations — it is read-only analysis only."

## Relevance to This Project
High relevance. This is an MCP server that directly addresses one of this project's core operational challenges: context window management. As codebases grow, Claude reads more and more files it does not need, burning context and increasing cost. Code-review-graph solves this at the structural level — it builds a persistent map of what matters, so Claude pulls only the relevant nodes rather than scanning entire directories. Pete (Python/quant) would benefit most directly, especially once strategy code grows. Cosmo (Skill Creator) and the broader team benefit from the review and impact analysis tools. The 8.2x average token reduction is a credible, meaningful number if the benchmark holds. Actively maintained — last pushed today as of research date.

## Master Library Assessment
- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** Section 4 is correct — this is an MCP server that installs via pip and connects to Claude through MCP protocol. Tier 2 rather than Tier 1 because it is most valuable once we have a substantial codebase to parse — in the early phases, the graph is small and the benefit is proportionally smaller. Phase 2+ is where this tool earns its keep. That said, the case for Tier 1 is real: the token savings benefit from day one, and 18k stars confirms sustained community traction well beyond initial hype.

## Soren Security Pre-check
- **Verdict:** FLAG
- **Date reviewed:** 2026-04-18
- **Checked:** License, author provenance, pip/PyPI supply chain alignment, local data handling, MCP tool surface scope, network exposure, dependency profile, repository activity.
- **Notes:** MIT license — clean and permissive, no copyleft concerns. Author tirth8205 is a transparent individual GitHub account; 11,048 stars in under two months is exceptional traction and indicates broad community adoption, which meaningfully raises confidence. The tool's core data flow is local-only by design: source code is parsed via Tree-sitter into a local SQLite database in a .code-review-graph/ directory, and no data leaves the machine during normal operation. That is the right architecture for this use case.
  The FLAG is on two specific items. First: PyPI package alignment. The tool installs via pip (pip install code-review-graph) and the PyPI package must be confirmed to correspond to the GitHub source before deployment. Mismatched PyPI packages are a known supply chain attack surface — the match should be verified at deployment time by checking the PyPI project page author, repository link, and release provenance. Second: MCP tool surface breadth. 28 MCP tools exposing structural code data to Claude is a wide surface. The tool is designed for read-only structural analysis, but Soren should confirm at deployment that none of the 28 tools permit file writes, code execution, or data export outside the local SQLite store. A tool that reads "only the relevant code" by design should not have write or execution permissions anywhere in its MCP schema.
  No network calls expected during normal use (local SQLite, no external APIs). If the tool does phone home for telemetry or version checks, that should be disabled before deployment.
  FLAG resolves at deployment after: (1) PyPI package confirmed to match GitHub source, (2) MCP tool schema reviewed to confirm no write/execute permissions.
  **Re-reviewed 2026-06-08 — verdict confirmed.** Stars now 18,219 (was 11,048); last push 2026-05-25; latest release v2.3.5. Sustained post-hype growth confirms active production use at scale. No new CVEs detected. Both FLAG conditions remain open — neither can be resolved without hands-on deployment verification. Do not clear until (1) PyPI package alignment confirmed and (2) MCP tool schema reviewed for write/execute permissions.

## Recommendation
File in Section 4 (MCP Servers) as a Tier 2 item. High priority for Soren review — if it clears, this should move to active consideration for Phase 2 when the codebase is large enough to benefit meaningfully. The token savings claim (8.2x average) combined with the structural analysis tools make this one of the more compelling MCP finds in recent research rounds.

---
*Report by Rose | Session 60 | 2026-04-18*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---

## C&P Summary
Code-review-graph is a tool that reads your entire codebase once, builds a structural map of it (which functions call which other functions, which classes inherit from what, which tests cover which code), and stores that map in a local database. From then on, when Claude needs to review code or answer a question about your codebase, instead of reading every file in the project, it queries the map and pulls only the files and functions that are actually relevant to what you asked. The documented result is an average 8.2x reduction in tokens used, with some tasks showing up to 49x savings. It connects to Claude Code via MCP — the same protocol our other tools use — and installs in three commands. It updates the map automatically when you edit files or make commits. For this project, it is most relevant once the codebase grows to a meaningful size (Phase 2 and beyond), but the token savings benefit from day one. 11,048 stars in under two months is exceptional community traction. MIT licensed, actively maintained.

