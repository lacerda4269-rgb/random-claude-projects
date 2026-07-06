# Resource Report: Obsidian Skills

**URL:** https://github.com/kepano/obsidian-skills
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No

---

## What It Is
A collection of five agent skills for working with Obsidian vaults, file formats, and CLIs — built to the Agent Skills specification and compatible with Claude Code, Codex CLI, and OpenCode.

## What It Does
The repo provides five modular skills: `obsidian-markdown` (create/edit Obsidian-flavored markdown with wikilinks, embeds, and properties), `obsidian-bases` (work with Bases files including views, filters, and formulas), `json-canvas` (manage JSON Canvas files with nodes, edges, and groups), `obsidian-cli` (interact with Obsidian vaults via CLI including plugin development), and `defuddle` (extract clean markdown from web pages to reduce token usage). Installable via marketplace plugin, npx, or manual setup.

## Relevance to This Project
Low direct relevance right now — this project is not built around Obsidian. However, the `defuddle` skill (clean markdown extraction from web pages) has standalone utility for Rose's research workflow, and the skills format is worth studying as a reference for the team's own skill-building work. If Obsidian is ever adopted as a knowledge management layer, this becomes immediately relevant.

## Master Library Assessment
- **Proposed Section:** 2 — Skills
- **Proposed Tier:** 3
- **Rationale:** Legitimate, high-quality skills package from a credible creator (Steph Bing, creator of Obsidian Minimal theme), but use is conditional on Obsidian adoption. The `defuddle` skill has narrower standalone value. Tier 3 is correct — useful when the time comes, not urgent now.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** Repo age (created January 2026), star count (34,913), forks (2,464), MIT license, creator identity (kepano = Steph Bing, well-known Obsidian community figure), README structure
- **Notes:** No suspicious patterns. Creator is a verified, well-regarded figure in the Obsidian ecosystem. High star count relative to repo age suggests genuine community traction. MIT licensed. No obfuscated code or external call-home patterns noted.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Rose's v1.0 sweep shows 34,913 stars (grown from 17,800+), 2,464 forks, last pushed 2026-06-08 — pushed today, highly active. MIT license unchanged. Exceptional growth trajectory. CLEARED verdict stands.

## Recommendation
Enter library at Section 2 (Skills), Tier 3. Flag `defuddle` as a potential standalone addition to Rose's research toolkit at a later review. No urgency — hold until Obsidian is on the roadmap or a web-scraping need arises.

---

## Rose's Freshness Review

**Date reviewed:** 2026-04-14 | **Reviewed by:** Rose

**What changed:** Obsidian's role has expanded in this session — it is now the recommended pairing with NotebookLM as the operator's notes/memory/code stack. This skills package supports that use case directly. The tool itself is unchanged — MIT license, actively maintained by Steph Bing (kepano), well-regarded in the Obsidian community.

**C&P Summary:** Obsidian is a note-taking app that stores everything as plain markdown files on your own machine — you own the files, there's no vendor lock-in, and the core app is free. This skills package gives Claude five specialized abilities for working with Obsidian vaults: create and edit Obsidian-flavored markdown with all its features (wikilinks, embeds, tags), work with Obsidian's database-style Bases files, manage JSON Canvas visual maps, interact with the Obsidian CLI for vault operations and plugin development, and (the standout) `defuddle` — a tool that strips web pages down to clean readable markdown, cutting the noise before sending content to Claude. Together with NotebookLM, the setup is: you build and maintain your notes in Obsidian (your permanent, private archive), then upload exported notes to NotebookLM when you want to query across them. This skills package makes Claude a direct participant in managing that archive. A Google Workspace account for NotebookLM eliminates the personal-account ToS risk for that layer.

**Updated recommendation:** Tier should move from 3 to 2 given the operator's confirmed interest in the Obsidian + NotebookLM stack. If that stack is adopted, this skills package becomes immediately relevant. The `defuddle` skill alone is a useful standalone addition to Rose's toolkit.

---
*Report by Sophia | Session 29 | 2026-03-28*
*Rose Freshness Review — Session 42 | 2026-04-14*

---

## C&P Summary

Obsidian Skills is a collection of five agent skills for working with Obsidian vaults, file formats, and CLIs — covering vault-flavored markdown, Bases database files, JSON Canvas maps, CLI-based vault and plugin operations, and `defuddle` (strips web pages to clean markdown to cut noise before sending content to Claude). It is built by Steph Bing (kepano), the well-known creator of the Obsidian Minimal theme, with 34,913 stars. With Obsidian now confirmed as the recommended notes/memory layer paired with NotebookLM, this skills package moves from Tier 3 to Tier 2 — it makes Claude a direct participant in managing the operator's knowledge archive, and `defuddle` alone is useful for Rose's research workflow.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
