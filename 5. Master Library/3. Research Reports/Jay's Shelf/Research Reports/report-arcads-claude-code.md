# Resource Report: arcads-claude-code

**URL:** https://github.com/krusemediallc/arcads-claude-code
**Date Researched:** 2026-06-01
**Researched by:** Rose | Security pre-check: Soren (pending) | Report by: Rose
**Already in Master Library?** No — new item. Routed to Jay's Shelf.

---

## C&P Summary

Arcads Claude Code is a workspace toolkit from Kruse Media LLC that connects Claude Code to the Arcads API — a commercial platform for generating AI marketing videos and static ad images. The repo includes skill files for generating video content via models like Seedance 2.0, Sora 2, and Kling 3.0, plus workflows for cloning ads, creating YouTube thumbnails, and publishing directly to Meta advertising. Everything runs through the Arcads API (commercial subscription required); the repo is the client-side layer that makes those capabilities available as Claude Code skills. No active workflow fit for the current project phase. 701 stars, MIT license. Most relevant for Jay if marketing automation or AI video creation becomes a future project direction, and for Vicky when video pipeline work begins.

---

## What It Is

A GitHub repository from Kruse Media LLC that provides Claude Code and Cursor workspace integration for the Arcads API — a commercial AI marketing video and image generation platform. The repository bundles agent skills, a prompting library, workflow scripts, and a MASTER_CONTEXT.md workspace memory file. Key metrics: 701 stars, MIT license, Python (53.8%) and Shell (46.2%). Requires the Arcads API (commercial; API key from app.arcads.ai/settings/api).

---

## What It Does

- Generates AI video content via Seedance 2.0, Sora 2, Veo 3.1, Kling 3.0, and other models
- Generates static image ads from a library of 37 templates via the Arcads API
- YouTube thumbnail generation using Nano Banana 2
- Clone-ad skill: end-to-end analysis of a reference ad adapted to a new product
- Meta Marketing API integration for ad publishing
- Workspace memory via MASTER_CONTEXT.md

---

## Relevance to This Project *(as of 2026-06-01)*

No active workflow fit in the current project phase. Relevant if Jay moves into marketing automation work or if a future project requires AI video generation for promotional content. Vicky (Videographer agent) is the most likely future user if this is ever activated.

Architecture note for Cosmo: the MASTER_CONTEXT.md workspace memory file and structured skill workflows organized around a single commercial API is a clean reference pattern for how to build API-specific skill sets.

---

## Master Library Assessment

- **Proposed Section:** 9 — Jay's Shelf
- **Proposed Tier:** 3
- **Rationale:** 701 stars — low validation. MIT license. Recent and actively maintained. Tier 3 reflects low community validation and no current workflow fit. Promote when a marketing automation or AI video generation project becomes active.

---

## Soren Security Pre-check

- **Verdict:** PENDING — not yet reviewed
- **Notes for Soren:**
  - MIT license, single-developer (Kruse Media LLC / Caleb Kruse), 635 stars — low community vetting
  - Shell scripts (46.2% of codebase) warrant a review for unexpected system commands; setup.sh in particular
  - Requires Arcads API key — confirm credential handling in setup.sh and skill files before deployment
  - All video/image generation executes on Arcads' commercial infrastructure — content submitted to API passes through Arcads' servers
  - Meta Marketing API integration requires separate Meta credentials — dual-credential surface
  - Prompt Injection Check: CLEAN — no instruction-like language found in GitHub pages or search results during research.

---

*Report by Rose — Research Specialist | Session 201 | 2026-06-01*
*Updated by Rose | Session 230 | 2026-06-08*
*Prompt Injection Check: CLEAN — no instruction-like language, permission claims, or directive content found in any web-sourced content reviewed during research.*

Sources:
- https://github.com/krusemediallc/arcads-claude-code

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
