# Resource Report: Graphify

**URL:** https://github.com/safishamsi/graphify
**Date Researched:** 2026-04-12
**Researched by:** Rose | Security pre-check: Soren | Filed by: Lexi
**Already in Master Library?** No — new item

---

## What It Is
Graphify is a Claude Code skill that transforms folders of code, documentation, papers, images, videos, and audio into queryable knowledge graphs. Created by Safi Shamsi. 62,965 stars, MIT licensed. Works as a skill in Claude Code, Codex, Cursor, OpenCode, Gemini CLI, and others — multi-platform from one install.

## What It Does
Three-pass extraction: (1) deterministic AST analysis via Tree-sitter across 20 programming languages, (2) media transcription using Whisper (local, audio never leaves machine), (3) LLM-powered semantic relationship extraction. Outputs: interactive HTML graph, JSON, and plain-language audit reports.

Token efficiency claim: **71.5x fewer tokens per query** on large mixed corpora vs. reading raw files. The graph is persistent across sessions — no re-reading files each time. Agents query the graph instead of the file system.

Supports: code, PDFs, markdown, images, video, audio — fully multimodal.

## Relevance to This Project
Directly addresses the token efficiency standing focus in both Master Guides. Large codebases are a known context window challenge — Graphify's persistent knowledge graph approach is the structural answer. Rather than loading files into context each session, agents query the graph. This is the kind of tool that pays off at Walk and Run phases when real project codebases get involved. Jay flagged it for memory and token management — that's exactly what it delivers.

## Builder Footprint

- **Integration type:** Skill + Python engine hybrid — installed as a Claude Code skill alongside a Python processing pipeline; requires Tree-sitter (AST parsing), Whisper via faster-whisper (local audio/video transcription), NetworkX + Leiden (graph community detection), and vis.js (HTML output rendering)
- **Extension points:** Graph output format (HTML, JSON, plain-language audit report) is configurable; multi-platform (Claude Code, Codex, Cursor, OpenCode, Gemini CLI); Cosmo can write skill invocation patterns that pre-scope the graph to specific directories or file types (Inferred from documentation — not explicitly documented)
- **Build complexity signal:** Medium-High — Python environment required; multiple dependencies (Tree-sitter, faster-whisper, NetworkX, Leiden, vis.js) must be installed and configured; initial graph build is a one-time processing step that may take time on large corpora; incremental updates are fast after first build
- **Known conflicts:** faster-whisper dependency for audio/video processing — confirm no Python environment conflict with Snyk Agent Scan (Python 3.13+) or LLM Guard (Python 3.12) if both are installed. Audio processing is fully local; no data leaves the machine. Compatible with code-review-graph (different approaches to codebase mapping — Graphify is broader/multimodal; code-review-graph is narrower/code-AST-focused).

## Master Library Assessment
- **Proposed Section:** 2 — Skills
- **Proposed Tier:** 1
- **Rationale:** Native Claude Code skill integration, MIT license, 62,965 stars, and direct relevance to the project's standing focus on token cost optimization. This addresses a core challenge — context window efficiency — at scale. Tier 1 for core/critical value.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** License (MIT — permissive, confirmed), star count (62,965 — exceptional community signal), authorship (Safi Shamsi, active maintainer), dependency stack (NetworkX, Leiden clustering, Tree-sitter, vis.js, faster-whisper — all well-established open-source), audio processing (local via faster-whisper — no cloud uploads), multi-platform skill compatibility confirmed, no unusual network calls or telemetry patterns flagged
- **Notes:** Clean clearance. Audio never leaves the machine (faster-whisper runs locally) — privacy concern is handled correctly. No suspicious patterns in the dependency chain.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Rose's v2.0 sweep shows 62,965 stars (grown from 47.9k), latest release v0.8.35 published 2026-06-07, last pushed 2026-06-08 — push today. MIT license unchanged. Exceptional growth and activity trajectory reinforce Tier 1 placement. CLEARED verdict stands.

## Recommendation
File to Section 2 — Skills, Tier 1. Strong candidate for early deployment when Walk phase starts. No operator decisions required at intake.

---
*Report by Rose + Sage | Session 39 | 2026-04-12*

---

## C&P Summary

Graphify is a Claude Code skill that converts folders of code, documentation, papers, images, video, and audio into a persistent, queryable knowledge graph — so agents query the graph instead of re-reading raw files each session. It uses a three-pass extraction process: deterministic AST analysis via Tree-sitter for 20 programming languages, local audio/video transcription via Whisper (nothing leaves the machine), and LLM-powered semantic relationship extraction. The claimed efficiency gain is 71.5x fewer tokens per query on large mixed corpora. This directly addresses the token cost optimization focus that runs through both Master Guides, and is a strong candidate for early deployment at Walk phase when real project codebases are in play.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---
*Disambiguation (S264): this is **safishamsi/graphify** — a distinct tool from the live `graphifyy` CLI (documented at `0. Resources Installed/report-graphify.md`). Renamed from `report-graphify.md` to resolve a filename collision; this one is NOT installed.*
