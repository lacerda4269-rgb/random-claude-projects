# Resource Report: claude-remember (remember@dpt-plugins)

**URL:** https://github.com/dpt-plugins/remember
**Date Documented:** 2026-06-11
**Documented by:** Sophia (COO) | Soren pre-check: ⬜ PENDING — next COHK | Report by: Sophia
**Already in Master Library?** No

---

## What It Is

claude-remember is a Claude Code plugin that provides persistent cross-session memory by writing structured Markdown files to a `.remember/` directory in each project. It captures session notes in a rolling buffer system (now.md, today-*.md, recent.md, archive.md, core-memories.md) and surfaces them automatically at session start via startup hooks.

## What It Does

- Writes session notes and handoffs to `.remember/remember.md` in the project root
- Maintains a multi-tier memory buffer: `now.md` (current session buffer), `today-*.md` (daily logs), `recent.md` (7-day rolling window), `archive.md` (older entries), `core-memories.md` (key moments — permanent)
- Injects memory context into session start via the `remember:remember` skill/hook
- Searchable history: `.remember/` directory is browseable and queryable directly
- Plain Markdown output — no database, no binary format, fully human-readable
- Works alongside other memory systems (MEMORY.md, claude-mem) as a complementary layer
- Provides the `/remember` skill command for explicit manual memory saves
- Plugin ID: `remember@dpt-plugins` | Scope: user-level (applies across all projects)
- Version: 0.7.3
- License: MIT (dpt-plugins)

## Installation & Location

- **Install type:** Claude Code plugin (user scope)
- **Plugin ID:** `remember@dpt-plugins`
- **Install location:** `C:\Users\jlacerda\.claude\plugins\cache\dpt-plugins\remember\0.7.3\`
- **Data directory:** `C:\Users\jlacerda\.claude\plugins\data\remember-dpt-plugins\`
- **Skill provided:** `remember:remember` — accessible via `/remember` command
- **Session installed:** 239 (2026-06-11, P7 memory stack)
- **Install method:** Claude Code plugin marketplace

## Relevance to This Project

claude-remember is the third layer of the P7 memory stack — positioned between MEMORY.md (strategic, Sage-curated) and claude-mem (operational, machine-captured). It fills the middle tier: session-by-session narrative memory written in plain Markdown that any agent can read without tooling. The `.remember/` directory is visible in the project root and already active in this project — session startup hooks surface its content automatically, providing handoff context before the MEMORY.md index loads.

## Master Library Assessment

- **Proposed Section:** 3 — Skills and Plugins
- **Proposed Tier:** 1
- **Rationale:** claude-remember is a Claude Code plugin providing a skill and hooks — Section 3 fits. Tier 1 because it is active and load-bearing in the P7 memory stack from first use.

## Soren Security Pre-check

- **Verdict:** ⬜ PENDING — flag for next COHK
- **Note:** claude-remember was installed as part of the P7 memory stack without a formal Soren review pass. Pre-check factors: MIT license, plain Markdown output with no database or network calls, reads/writes only to the `.remember/` directory in the project root, no external API dependency, small and auditable codebase. Risk profile is low; formal clearance still required per process.

## Recommendation

File in Section 3 (Skills and Plugins) at Tier 1. Queue Soren formal clearance at next COHK. No blockers for continued use — plugin is active, operational, and load-bearing in the current memory architecture.

---
*Report by Sophia | Session 242 | 2026-06-11*

---

## C&P Summary

claude-remember (v0.7.3, remember@dpt-plugins) is a user-scope Claude Code plugin that provides persistent session memory via a `.remember/` directory of plain Markdown files. It maintains a rolling buffer — `now.md` (current session), `today-*.md` (daily), `recent.md` (7-day), `archive.md` (older), `core-memories.md` (permanent) — and surfaces memory context at session start via hooks. Installed as part of the P7 memory stack (Session 239) at `~/.claude/plugins/cache/dpt-plugins/remember/0.7.3/`. Its role in the stack is the middle tier between Sage's curated MEMORY.md (strategic) and claude-mem's machine-captured operational log. MIT license, no network calls, plain Markdown output — low-risk profile. Soren clearance pending; queued for next COHK.

---
*Keep-both pair (S264): this is the **install/deployment record**. Full research report → `Hooks/Research Reports/report-claude-remember.md`.*
