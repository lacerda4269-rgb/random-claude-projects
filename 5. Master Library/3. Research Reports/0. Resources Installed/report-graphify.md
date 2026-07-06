# Resource Report: Graphify (graphifyy)

**URL:** https://github.com/graphifyy/graphifyy
**Date Documented:** 2026-06-11
**Documented by:** Sophia (COO) | Soren pre-check: ⬜ PENDING — next COHK | Report by: Sophia
**Already in Master Library?** No

---

## What It Is

Graphify (PyPI package: `graphifyy`) is a Python CLI tool that converts any corpus of documents — Markdown files, code, PDFs, images, videos — into a persistent semantic knowledge graph. It uses LLM-based extraction to identify entities, relationships, and communities, then stores them as a queryable graph index that survives across sessions. A companion `graphify-mcp` MCP server exposes the graph to Claude Code directly.

## What It Does

- **Detect phase:** Scans a directory, catalogs all files, detects encoding, and builds a file manifest
- **Extract phase:** Sends document chunks to an LLM (Gemini or OpenAI) for semantic entity and relationship extraction — parallelizable via multiple extraction chunks
- **Merge phase:** Combines all extracted chunks into a unified graph, deduplicates nodes and edges, assigns community labels via Leiden algorithm
- **Query tools:** `graphify query` (semantic search), `graphify path` (shortest path between nodes), `graphify explain` (community-level summary), `graphify community` (list communities)
- **graphify-mcp:** MCP server that exposes the same query/path/explain tools to Claude Code as callable tools — integrates with the `graphify` skill
- **Output format:** JSON graph files in a `graphify-out/` directory (nodes, edges, community metadata) — committed to the repo or excluded via `.gitignore`
- **God nodes:** Automatically identifies highly connected hub nodes that summarize entire topic clusters
- **Community detection:** Leiden algorithm groups related nodes into labeled communities (e.g., "Agent Architecture", "Session Management", "Security Pipeline")
- **Supported inputs:** Markdown, code files, PDFs, images, videos (multimodal extraction)
- PyPI package name: `graphifyy` | CLI commands provided: `graphify`, `graphify-mcp`
- Version: 0.8.37
- License: MIT

## Installation & Location

- **Install type:** Python CLI tool via uv
- **PyPI package:** `graphifyy`
- **Install command:** `uv tool install graphifyy`
- **uv tool name:** `graphifyy`
- **Commands available:** `graphify`, `graphify-mcp`
- **Skill location:** `C:\Users\jlacerda\.claude\skills\graphify\` (Claude Code skill — provides the `/graphify` command)
- **Index output:** `graphify-out/` directory in each indexed project root
- **Session installed:** 239 (2026-06-11, P7 memory stack)
- **First live use:** Session 241 — built full per-project index for Initial-Package-Project (1,056 nodes, 1,466 edges, 77 communities, 394 source files)

## Live Results — Initial-Package-Project Index

Built and verified Session 241 (2026-06-11):

| Metric | Value |
|---|---|
| Source files indexed | 394 |
| Extraction chunks | 18 (run in parallel via subagents) |
| Total nodes | 1,056 |
| Total edges | 1,466 |
| Communities detected | 77 |
| Index location | `graphify-out/` (project root) |

Query system confirmed working. Community labels include: Agent Architecture, Session Management, Security Pipeline, Knowledge Graph, Memory Systems, and others.

## Relevance to This Project

Graphify is the knowledge indexing layer of the P7 memory stack. Its per-project index gives Sage and all agents a queryable semantic map of the entire project corpus — replacing the need to read dozens of files to locate relevant context. The `/graphify` skill (Claude Code) turns any natural language question into a graph query, returning focused excerpts instead of raw file content. This directly reduces session start token cost and enables targeted just-in-time file reads rather than bulk session read-ins. A global index covering `~/.claude/` is planned for Session 242.

## Master Library Assessment

- **Proposed Section:** 5 — CLIs
- **Proposed Tier:** 1
- **Rationale:** Python CLI tool installed via uv — Section 5 fits. Tier 1 because Graphify is active, producing live results, and is a foundational layer of the P7 memory stack from first use.

## Soren Security Pre-check

- **Verdict:** ⬜ PENDING — flag for next COHK
- **Note:** Graphify was installed as part of the P7 memory stack without a formal Soren review pass. Pre-check factors: MIT license, local-first processing (LLM API calls use configured API keys, no proprietary data exfiltration), output is JSON files written to the project directory, Python/uv install chain. LLM API key configuration (Gemini or OpenAI) is the primary external dependency — keys are user-managed. Risk profile is moderate (network calls to LLM APIs); formal clearance required per process.

## Recommendation

File in Section 5 (CLIs) at Tier 1. Queue Soren formal clearance at next COHK — note the LLM API key dependency for the extraction phase. No blockers for continued use — tool is active, producing live results, and central to the P7 memory architecture.

---
*Report by Sophia | Session 242 | 2026-06-11*

---

## C&P Summary

Graphify (PyPI: `graphifyy`, v0.8.37) is a Python CLI tool installed via `uv tool install graphifyy` that converts document corpora into persistent semantic knowledge graphs. It runs a three-phase pipeline: detect (catalog files) → extract (LLM-based entity/relationship extraction, parallelizable) → merge (deduplicate, assign community labels via Leiden algorithm). Output lands in a `graphify-out/` directory as queryable JSON. A companion `graphify-mcp` MCP server exposes query/path/explain tools to Claude Code, wired through the `/graphify` skill. First live use in Session 241 indexed the full Initial-Package-Project corpus: 394 files, 1,056 nodes, 1,466 edges, 77 communities. The index is the knowledge-layer foundation of the P7 memory stack — enables targeted semantic queries instead of bulk file reads at session start. MIT license; Soren clearance pending (LLM API key dependency flagged); queued for next COHK.

---
*Disambiguation (S264): this is **graphifyy** (PyPI `graphifyy`, github.com/graphifyy) — the live `/graphify` skill backend. A different tool sharing the name (safishamsi/graphify) is documented at `Skills/Research Reports/report-graphify-safishamsi.md`.*
