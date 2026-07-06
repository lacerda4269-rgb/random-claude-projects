# Resource Report: gstack

**URL:** https://github.com/garrytan/gstack
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No

---

## What It Is
gstack is an open-source Claude Code extension toolkit by Garry Tan (YC President & CEO) that adds 28 specialized AI agent skills as slash commands, turning a solo developer's setup into a role-based engineering team.

## What It Does
gstack provides structured slash commands covering the full development lifecycle: `/office-hours` (CEO perspective), `/review` (code review), `/qa` (QA lead), `/ship` (release engineer), `/browse` (real browser automation via Chromium), `/careful`, `/freeze`, `/guard` (safety guardrails), and more. It includes security auditing with OWASP Top 10 and STRIDE threat modeling, multi-AI cross-model code review, and parallel sprint management supporting 10-15 concurrent tasks. Built with TypeScript/JavaScript on the Bun runtime, MIT license. 108,241 stars, 16,091 forks, actively maintained.

## Relevance to This Project
High relevance — gstack is a skill collection purpose-built for Claude Code, which is exactly what this project operates on. The role-based skill structure (CEO, designer, engineer, QA lead, security officer, release engineer) directly mirrors the agent-team model being built here. Several of the included skills — particularly `/review`, `/qa`, `/security` (OWASP/STRIDE), and the safety guardrail commands — are worth reviewing as templates or direct inputs when building out the Skill Creator's library. The "parallel sprint management" model is also directly relevant to the orchestration architecture.

## Builder Footprint

- **Integration type:** Skill collection (TypeScript/Bun-backed) — 28 slash commands installed via Claude Code plugin marketplace or by placing the extension files in `.claude/`; each skill is independently callable
- **Extension points:** All 28 slash commands are independently usable; role-based skill structure (CEO, QA, security officer, release engineer) maps directly to the team's agent roles — Cosmo can adapt individual commands as skill templates; `/browse` provides real Chromium browser access for agent tasks (Inferred from documentation — not explicitly documented)
- **Build complexity signal:** Low-to-Medium — marketplace install is low friction; Bun runtime dependency required for underlying TypeScript execution; `/browse` skill requires a Chromium instance; OWASP/STRIDE security skills are ready-to-invoke with no additional configuration
- **Known conflicts:** `/browse` activates a real Chromium browser — declare this clearly in any agent brief. The `/caveman` mention in this report was a descriptive note in the Builder Footprint only — **RESOLVED Session 203:** the deployed Caveman skill (`.claude/commands/caveman.md` — invocation: `/caveman`) is the canonical source; gstack's mention is descriptive, not an active command. No implementation conflict. Compatible with Superpowers, mattpocock/skills, Andrej Karpathy Skills.

## Master Library Assessment
- **Proposed Section:** 2 — Skills
- **Proposed Tier:** 1
- **Rationale:** This is a production-grade skill collection for Claude Code from a credible, high-visibility author, covering roles that directly map to the standing team structure. Tier 1 because it is immediately actionable — these skills can inform or directly accelerate the current build.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** Repo age (active 2026), star count (108,241), fork count (16,091), MIT license, authored by Garry Tan (YC President — public figure with verified identity), TypeScript/Bun codebase, no hidden network calls described in README
- **Notes:** Authorship by a well-known, publicly identified tech figure (Garry Tan, YC) is a strong legitimacy signal. MIT license — no copyleft concerns. Browser automation via Chromium (`/browse` skill) warrants awareness but is a declared, documented feature — not a hidden capability. No concerns.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Rose's v2.0 sweep shows 108,241 stars (grown from 96.3k), 16,091 forks, last pushed 2026-06-08 — push today. MIT license unchanged. Tool count note (23 vs. 28) from v1.0 log is a consolidation, not a capability reduction. Caveman slash command conflict fully resolved (Session 203). CLEARED verdict stands.

## Recommendation
Enter the library in Section 2 at Tier 1. Review the full skill list during the next Skill Creator work session — several skills here are direct candidates for adoption or adaptation into the standing team's playbook.

---
*Report by Sophia | Session 29 | 2026-03-28*

---

## C&P Summary

gstack is a Claude Code extension toolkit by Garry Tan (YC President) that adds 23 specialized slash-command skills (originally documented as 28, consolidated/reorganized) covering the full development lifecycle — code review, QA, release engineering, real browser automation, OWASP/STRIDE security auditing, multi-AI cross-model review, and parallel sprint management. At 108,241 stars with MIT license it is production-grade and broadly adopted. The role-based skill structure directly mirrors the standing agent team being built here, and several skills — particularly review, QA, security, and safety guardrails — are direct candidates for adoption or adaptation by the Skill Creator.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
