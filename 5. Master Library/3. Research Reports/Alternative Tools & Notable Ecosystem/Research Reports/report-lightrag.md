# Resource Report: LightRAG

**URL:** https://github.com/hkuds/lightrag
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** Yes — Section 7, Tier 3, status: ⏳ Pending

---

## What It Is
LightRAG is an open-source retrieval-augmented generation system that combines knowledge graphs with vector databases for enhanced document indexing and querying.

## What It Does
Provides dual-level retrieval using both vector similarity and knowledge graph structures. Supports multiple storage backends (PostgreSQL, MongoDB, Neo4j, OpenSearch). Includes a web UI and REST API. Handles multimodal inputs (text, images, tables, equations) via RAG-Anything integration. Offers reranking, source citation, and evaluation tooling via RAGAS and Langfuse. Companion projects include VideoRAG. Active development — 36.3k stars, 5.1k forks, v1.5.0 (June 3, 2026), 73 releases (updated 2026-06-08).

## Relevance to This Project
Awareness-level relevance. LightRAG is a powerful research and knowledge retrieval engine — not a direct tool for trading system development or agent orchestration right now. In future phases, if the team needs to give agents access to a searchable, graph-structured knowledge base (e.g., documentation corpora, trading research), this becomes relevant. Section 7 placement is appropriate.

## Master Library Assessment
- **Proposed Section:** 7 — Alternative Tools & Notable Ecosystem
- **Proposed Tier:** 3
- **Rationale:** The existing ML entry (Section 7, Tier 3) is accurate. LightRAG is a mature, high-value ecosystem tool — not needed for current phases, but worth tracking as the team scales toward more sophisticated knowledge management needs.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** Star count (36.3k — updated 2026-06-08), forks (5.1k), v1.5.0 (June 3, 2026), 73 releases, MIT license, HKUDS organization identity
- **Notes:** Academic research origin with strong community adoption. Active release cadence (73 releases, v1.5.0 current). No suspicious patterns.

## Recommendation
Current ML entry is accurate — Section 7, Tier 3, status Pending is correct. No corrections needed. Confirm and move forward.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---
*Report by Sophia | Session 29 | 2026-03-28*
*Updated by Rose | Session 230 | 2026-06-08*

---

## C&P Summary

LightRAG is an open-source retrieval-augmented generation system that combines knowledge graphs with vector databases for enhanced document indexing and querying — providing dual-level retrieval via both vector similarity and graph structure. Supports multiple storage backends (PostgreSQL, MongoDB, Neo4j, OpenSearch), includes a web UI and REST API, and handles multimodal inputs via RAG-Anything integration. 36.3k stars, v1.5.0 (June 3, 2026), 73 releases, actively maintained (updated 2026-06-08). No active workflow fit for current phases — relevant in a future phase if the team needs agents to search a structured, graph-backed knowledge base from large document corpora. Awareness-level item at Tier 3.
