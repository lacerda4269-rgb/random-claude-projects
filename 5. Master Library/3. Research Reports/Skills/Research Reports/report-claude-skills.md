# Resource Report: claude-skills

**URL:** https://github.com/secondsky/claude-skills
**Date Researched:** 2026-05-03
**Researched by:** Rose | Security pre-check: Soren | Filed by: Lexi
**Already in Master Library?** No — new item

---

## What It Is
claude-skills is a GitHub repository collecting reusable Claude Code skills — behavioral prompt instructions that extend or modify what Claude Code does in a project. Skills are `.md` files installed into `.claude/` — once present, they can be invoked in sessions to trigger specific behaviors, workflows, or coding constraints. Maintained by secondsky.

## What It Does
Provides a catalog of pre-built Claude Code skills covering development workflows: code review patterns, testing behaviors, documentation conventions, refactoring guidelines, and coding style enforcement. Each skill is a standalone `.md` file. Installation: copy to `.claude/` in the project or use the repository's install script. Modular by design — install only what the project needs.

## Relevance to This Project
Direct relevance to Cosmo (Skill Creator) — an existing external skill catalog is a research and reference resource. When Cosmo is asked to build a skill, claude-skills is a first stop: check whether a high-quality version already exists before building from scratch. Also relevant to Agent Onboarding — if the team needs a skill and a cleared version exists here, skip the build and deploy.

## Master Library Assessment
- **Proposed Section:** 2 — Skills
- **Proposed Tier:** 2
- **Rationale:** Useful skill catalog with real content. Cleared by Soren with conditions — per-skill review required before any individual skill deployment. Tier 2 reflects the standing condition: the repo is safe to browse and discover from; it is not safe to bulk-deploy from without individual Soren review.

## Soren Security Pre-check
- **Verdict:** CLEARED WITH CONDITIONS
- **Checked:** Repository structure, install scripts (reviewed — no malicious code detected), sample skill content (behavioral text, no code execution), dependency profile (none — pure markdown)
- **Conditions:**
  1. Per-skill Soren review required before any individual skill is deployed to any agent. Repo-level clearance is NOT blanket skill clearance.
  2. Do NOT run the bulk install script without completing per-skill review first.
- **Notes:** The repository itself is clean. The risk lives in deploying unreviewed content. Each skill gets its own Soren pass before going into active use.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Rose's v1.0 sweep shows 165 stars, 25 forks, MIT license confirmed, last pushed 2026-05-14. Conditions unchanged — per-skill Soren review required before any individual deployment. CLEARED WITH CONDITIONS verdict stands.

## Recommendation
File to Section 2 — Skills, Tier 2. Cosmo reference and discovery catalog. Individual skills deployed only after per-skill Soren review.

---
*Report by Rose + Sage | Session 106 | 2026-05-03*

---

## C&P Summary

claude-skills is a GitHub repository of reusable Claude Code behavioral skills — standalone `.md` files that extend or modify Claude Code's behavior in a project. Maintained by secondsky. Covers code review, testing, documentation, refactoring, and style enforcement patterns. Soren verdict: CLEARED WITH CONDITIONS — repository and install scripts are clean, but per-skill Soren review is required before any individual skill is deployed; do not bulk-install. Primary use for this team: Cosmo's reference catalog for discovering pre-built skills before building from scratch, and a sourcing resource for Agent Onboarding if a needed skill already exists in cleared form. Filed to Section 2 (Skills), Tier 2.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
