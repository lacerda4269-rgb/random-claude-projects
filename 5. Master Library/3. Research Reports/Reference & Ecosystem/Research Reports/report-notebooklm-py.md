# Resource Report: notebooklm-py

**URL:** https://github.com/teng-lin/notebooklm-py
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** Yes — Section 1 Tier 1 AND Section 5 Tier 2 (dual entry), "notebooklm-py", status: ⏳ Pending

---

## What It Is
An unofficial Python API and agent skill for Google NotebookLM, providing programmatic access to features beyond the web UI — including bulk content generation, research automation, batch downloads, and agent integration via Claude Code and Codex.

## What It Does
Enables programmatic control of NotebookLM via Python API, CLI, and agent skill interface. Generates audio overviews (podcasts), videos, slide decks, quizzes, flashcards, infographics, data tables, and mind maps. Supports bulk source imports from URLs, PDFs, YouTube, and Google Drive with automated research agents. Provides batch downloads in MP3, MP4, PDF, PNG, CSV, and JSON formats. Offers features unavailable in the standard web UI (quiz/flashcard JSON export, mind map data extraction, PPTX downloads). 16.1k stars, 14 releases, latest v0.7.1 (June 7, 2026 — updated 2026-06-08). An upcoming v0.8.0 is documented with breaking-change migration guidance.

**Critical caveat from repo's own README:** "This library uses undocumented Google APIs that can change without notice" — explicitly recommended for prototypes and personal projects, not production use.

## Relevance to This Project
Medium relevance. The agent skill interface and research automation capabilities are aligned with Rose's research workflow and the team's broader knowledge processing needs. However, the undocumented API dependency is a meaningful operational risk — this is not production-stable. The dual ML entry is worth evaluating carefully (see below).

## Master Library Assessment — Dual Entry Evaluation

**Section 1 (MCP Servers), Tier 1 — Assessment: NEEDS CORRECTION**
Section 1 is for MCP Servers (tools connecting Claude to external systems via the Model Context Protocol). notebooklm-py is a Python API/CLI/skill — it is not an MCP server. The Section 1 entry appears to be a misclassification. Recommend moving to Section 2 (Skills) or flagging for reclassification.

**Section 5 (Reference & Ecosystem), Tier 2 — Assessment: ACCURATE**
Section 5 covers reference and source material to read from and learn from. A Python API wrapper for a major AI research tool is a reasonable Section 5 entry. Tier 2 is appropriate given its research automation utility.

**Recommended correction:** Remove the Section 1, Tier 1 entry. Retain Section 5, Tier 2. Optionally add a Section 2 (Skills) entry for the agent skill component specifically. Bring to operator's attention.

## Soren Security Pre-check
- **Verdict:** FLAG (not REJECT — FLAG for operational risk, not malice)
- **Checked:** Star count (16.1k — updated 2026-06-08), 14 releases, latest v0.7.1 (June 7, 2026), license (MIT), API dependency nature, README disclaimer
- **Notes:** The FLAG is not a security concern — the repo itself appears legitimate and is actively maintained (v0.7.1 shipped June 2026). The flag is for the undocumented Google API dependency. Google can break this without notice, and the repo's own README explicitly warns against production use. However, the active release cadence (14 releases, now at v0.7.1) suggests the maintainer is actively chasing API changes — this is a positive signal that reduces (but does not eliminate) availability risk. The v0.8.0 breaking-change migration indicates the API surface is still evolving. Cleared for research and prototype use with the caveat clearly documented in the ML entry.

## Recommendation
Two actions needed: (1) FLAG the Section 1, Tier 1 ML entry as a likely misclassification — notebooklm-py is not an MCP server. Recommend reclassification to Section 2 (Skills), Tier 2 for the skill component. (2) The Section 5, Tier 2 entry is accurate — confirm and retain. The undocumented API warning should be explicitly noted in the ML entry description so the team knows the stability constraints upfront.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---
*Report by Sophia | Session 29 | 2026-03-28*
*Updated by Rose | Session 230 | 2026-06-08*

---

## C&P Summary

An unofficial Python API and agent skill for Google NotebookLM that unlocks programmatic access to features not available in the web UI — including bulk audio overview (podcast) generation, batch source imports from URLs/PDFs/YouTube/Google Drive, and exports in MP3, MP4, PDF, PNG, CSV, and JSON formats. 16.1k stars, v0.7.1 (June 2026), MIT licensed (updated 2026-06-08). Relevant to Rose's research workflows and the team's knowledge processing needs. Critical caveat: this library uses undocumented Google APIs that can break without notice — the repo's own README explicitly flags it as unsuitable for production use. Actively maintained (14 releases, v0.8.0 forthcoming with breaking changes) — but the production-use warning stands. The ML entry misclassified it as an MCP Server (Section 1) — it is a Python API/skill, not an MCP server.
