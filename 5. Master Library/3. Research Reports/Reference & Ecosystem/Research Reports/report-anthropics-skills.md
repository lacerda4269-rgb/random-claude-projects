# Resource Report: Anthropic Skills (anthropics/skills)

**URL:** https://github.com/anthropics/skills
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** Yes — Section 5, Tier 1, status: Pending

---

## What It Is
The official Anthropic repository of Skills for Claude — a curated collection of skill folders containing SKILL.md instructions, scripts, and resources that Claude loads dynamically to perform specialized tasks.

## What It Does
Skills teach Claude how to complete specific repeatable tasks: document creation with brand guidelines, data analysis using organizational workflows, enterprise communication, development and technical tasks, and creative/design applications. The repository includes full DOCX, PDF, PPTX, and XLSX document creation capabilities (source-available). Skills install via `/plugin marketplace add anthropics/skills` in Claude Code, or via Claude.ai (paid plans) or the Skills API. The spec folder defines the Agent Skills Standard (`agentskills.io`). 148k+ stars, 38 commits (updated 2026-06-08).

## Relevance to This Project
This is the canonical source for how Claude Skills work — the spec, the templates, the examples. It is the reference the Skill Creator must know inside-out. The low commit count (25) is not a concern here; this is a curated, stable reference repo from Anthropic, not a fast-moving development project.

## Master Library Assessment
- **Proposed Section:** 5 — Reference & Ecosystem (confirmed)
- **Proposed Tier:** 1 (confirmed)
- **Rationale:** Maintained by Anthropic directly. Defines the skill standard the entire team operates under. Section 5, Tier 1 is correct.

## Master Library Entry Status
The existing ML entry (Section 5, Tier 1, status: Pending) is **accurate and confirmed**. No corrections needed. The entry can be updated to status "Verified" — this research confirms it is the right section, right tier, and the repository is exactly what the entry describes.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** Official Anthropic GitHub organization, 148k stars (updated 2026-06-08), mixed Apache 2.0 / source-available licensing, no suspicious patterns
- **Notes:** This is the source repository. Zero concerns.

## Recommendation
ML entry is accurate — confirm and move status from Pending to Verified. No new action required beyond updating the status entry.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---
*Report by Sophia | Session 29 | 2026-03-28*
*Updated by Rose | Session 230 | 2026-06-08*

---

## C&P Summary

The official Anthropic GitHub repository of Skills for Claude — the canonical source for how Claude Skills work, including the spec, templates, and working examples across document creation, data analysis, development, and enterprise communication tasks. Skills install via a single CLI command or through Claude.ai and are the standard the entire team builds against. This is the repo the Skill Creator must know inside-out: it defines the Agent Skills Standard (`agentskills.io`) and is maintained directly by Anthropic. 148k+ stars (updated 2026-06-08), stable by design — this is a curated reference, not a fast-moving dev project.
