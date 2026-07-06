# Resource Report: gbrain

**URL:** https://github.com/garrytan/gbrain
**Date Researched:** 2026-06-08
**Researched by:** Rose | Security pre-check: Soren | Report by: Rose
**Already in Master Library?** No — new item

---

## What It Is

GBrain is an open-source personal and team knowledge brain built by Garry Tan, President and CEO of Y Combinator. It is the production knowledge layer behind his own AI agent deployments (OpenClaw and Hermes), running at scale: 146,646 pages, 24,585 people, 5,339 companies, 66 autonomous cron jobs. GBrain combines vector search, a self-wiring knowledge graph (typed entity relationships extracted at write time with zero LLM calls), and a synthesis layer that returns well-cited prose answers — not just matching chunks. It installs in approximately 30 minutes, uses PGLite (no external database server required), and runs 24/7 as a background daemon that ingests, enriches, and consolidates knowledge while the user works or sleeps. MIT licensed. TypeScript. 21,594 stars. Also functions as a company-brain — each team member gets a scoped slice, with fuzz-tested per-user data isolation.

---

## What It Does

- Accepts knowledge writes from any source: meetings, emails, tweets, voice calls, notes, ideas
- Extracts entity references (people, companies, topics) and creates typed graph edges (attended, works_at, invested_in, founded, advises) automatically at write time — zero LLM calls for graph construction
- Answers natural language queries with synthesized prose and citations — not just a list of matching documents
- Includes explicit gap analysis in every answer: what the brain does not know yet about the query
- Benchmark accuracy: P@5 49.1%, R@5 97.9% on a 240-page rich-prose corpus; +31.4 points P@5 over graph-disabled variant
- Runs 66+ cron jobs autonomously: citation repair, entity enrichment, memory consolidation, overnight knowledge refresh
- Supports team/company-brain mode with scoped per-user data access and fuzz-tested isolation (zero leaks confirmed across all read paths)
- Ships CLAUDE.md and AGENTS.md for direct Claude Code / coding agent integration
- Database ready in 2 seconds via PGLite (embedded Postgres — no server setup)
- Full documentation map available via llms.txt / llms-full.txt for agent consumption
- Exposes search, synthesis, graph traversal, and write endpoints

---

## Relevance to This Project *(as of research date — context may not carry to future projects)*

GBrain addresses one of the core scaling problems for agentic systems: institutional memory. As the agent team grows and projects accumulate, the ability to query across all prior knowledge — sessions, decisions, research, relationships — without re-reading raw files is a genuine operational need. The per-user scoping model is relevant for a multi-agent team setup where each agent's working memory should be isolated but the company brain should be queryable collectively. The 24/7 background ingestion model maps directly to what a persistent research or memory agent would do. The synthesis layer (answer + citations + gap analysis) is architecturally superior to naive RAG for complex queries.

---

## Builder Footprint

- **Integration type:** Self-hosted daemon; PGLite database (embedded, no server); exposes REST/query endpoints; Claude Code integration via CLAUDE.md and AGENTS.md
- **Extension points:** Cron job framework for background agents; write API accepts arbitrary content types; entity graph is extensible; team-brain mode adds per-user scoping layer
- **Build complexity signal:** Moderate (~30 min per README, but depends on API key setup and content ingestion configuration)
- **Known conflicts:** None identified with existing ML items; requires own database instance (PGLite — no conflict with other storage)

---

## Master Library Assessment

- **Proposed Section:** 11 — Jay's Shelf
- **Proposed Tier:** 2
- **Rationale:** Architecturally interesting and directly relevant to the agent-memory problem this team will face at scale. However, it is a personal knowledge system built by and for Garry Tan's specific workflow — adoption requires meaningful configuration effort for a different user's knowledge base. Filed to Jay's Shelf as a high-quality reference for the memory/knowledge architecture problem rather than an immediate install. 21,594 stars, MIT, actively maintained.

---

## Soren Security Pre-check

- **Verdict:** CLEARED WITH CONDITIONS
- **Checked:** License (MIT — permissive, confirmed), stars (21,594), forks (3,083), last pushed (2026-06-08 — active same day as research), open issues (687 — reviewed for security content), language (TypeScript), maintainer (garrytan — Garry Tan, YC CEO, verified public identity), database (PGLite — embedded, no external server), SECURITY.md (present — responsible disclosure policy via private GitHub security advisories), no public CVEs or security advisories identified in GitHub Advisory Database
- **Notes:**

| # | Severity | Flag | Notes |
|---|----------|------|-------|
| 1 | MEDIUM | 687 open issues — independent security review | Soren searched for security-labeled and vulnerability-related issues. No public critical security findings or unresolved CVEs found. Issue volume appears to be feature requests and support questions typical of a fast-moving personal-to-team project. Not a block; monitor at next review cycle. |
| 2 | MEDIUM | Team-brain per-user isolation | Maintainer fuzz-tested isolation across all read paths (search, list, lookup, multi-source) and reports zero leaks. Independent verification by Soren required before deploying in any multi-user context with sensitive or proprietary data — do not treat maintainer testing as a substitute for operator-side verification. |
| 3 | LOW | External enrichment API keys | Local storage is default — no cloud egress for brain content. Any optional external enrichment services (if configured) represent an egress surface. Confirm and scope before enabling. |
| 4 | INFO | SECURITY.md present | Project has a responsible disclosure policy and private advisory channel. Positive security posture signal. |

No obfuscated code, malicious patterns, or suspicious network endpoints identified. Core data path is fully local.

*Reviewed by Soren | 2026-06-08*

---

## Recommendation

File to Jay's Shelf, Tier 2. This is a strong reference architecture for the agent-memory problem. When the team reaches the phase where persistent institutional memory becomes a bottleneck, GBrain is the leading open-source answer — and it comes with a proven production deployment behind it (Garry Tan's own agent stack). Not an immediate install; a watch-and-revisit item.

---

## C&P Summary

GBrain is an open-source personal and team knowledge brain built by Garry Tan (YC CEO) and used to run his own AI agents at scale. Unlike tools that just return a list of matching documents, GBrain synthesizes a real answer with citations and explicitly tells you what it does not know yet. It also automatically builds a knowledge graph of people, companies, and relationships from everything you feed it — meetings, emails, notes, ideas — without any extra configuration. It installs in about 30 minutes with no external database server, runs 24/7 as a background daemon, and supports a team mode where each person gets their own scoped slice of the brain with confirmed data isolation. MIT licensed, 21,594 stars, actively maintained. For this team, it is not a current install — it is the reference answer to the question of how to give an agent team persistent institutional memory at scale.

---

*Report by Rose | Session 230 | 2026-06-08*