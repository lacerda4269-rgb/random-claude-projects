# Resource Report: skills.sh (Vercel Agent Skills Directory)

**URL:** https://www.skills.sh/
**Date Researched:** 2026-06-01
**Researched by:** Rose | Security pre-check: Soren (pending) | Report by: Rose
**Already in Master Library?** No — new item. DISTINCT from all existing ML skills entries (mattpocock/skills, gstack, Anthropic Skills, etc.) — those are specific skill collections; skills.sh is the discovery and installation platform across all of them.

---

## C&P Summary

skills.sh is the open-source agent skills directory built by Vercel Labs, launched in January 2026. It hosts and indexes 631,874+ reusable skill packages from the community, ranked by how often they are actually installed. You can browse by topic (React, testing, databases, etc.) and install any skill directly into Claude Code, Cursor, Copilot, or 20+ other agents with one command: `npx skills add <owner/repo>`. For this team, it is the primary place Cosmo checks before building any new skill — if the skill already exists and has strong community adoption, building from scratch is the wrong call. The platform runs its own security audits but cannot vet everything; the team's own Soren pipeline still applies to any skill adopted from this directory. Free to use, open-source, backed by Vercel and Anthropic. This is a different item from all existing ML skills entries — those are specific skill collections; this is the discovery and installation platform across all of them.

---

## What It Is

A leaderboard directory and open-source CLI ecosystem for discovering and installing reusable AI agent skills. Built and maintained by Vercel Labs (launched January 20, 2026). Hosts a searchable directory of 631,874+ skills from the open-source community. The underlying CLI is open source at github.com/vercel-labs/skills — v1.5.10, 21.7k stars (updated 2026-06-08).

This is the infrastructure layer beneath skills — not a collection of skills itself, but the discovery, installation, and governance platform for the entire open agent skills ecosystem.

---

## What It Does

- Hosts and indexes 631,874+ skill packages from the open-source community
- Leaderboard ranking by installation count and activity
- Topic organization: React, Next.js, design, databases, testing, marketing, workflows, and more
- Security audits for vetted skills (platform-acknowledged: cannot guarantee quality of every listed skill)
- Official skills curated by: Microsoft Azure, Vercel, Anthropic, and others
- Supports 20+ agent platforms: Claude Code, Cursor, GitHub Copilot, Gemini, Windsurf, Codex, Kiro, and more
- CLI-based install: `npx skills add <owner/repo>` — no global install required
- Open-source infrastructure with documentation and API access
- Free to browse; no paid tiers documented

---

## Relationship to Existing ML Items

**Distinct from all existing ML skills entries.** The distinction matters:
- **mattpocock/skills, gstack, Anthropic Skills, etc.** — these are specific skill collections (individual packages or curated sets)
- **skills.sh** — this is the discovery and installation platform across all skill collections

Comparison to claudemarketplaces.com (already in ML, Section 9, Tier 2):
- claudemarketplaces.com covers skills + MCP servers + marketplace repos; discovery-only, no install mechanism
- skills.sh focuses specifically on skills; provides a CLI install mechanism; Vercel Labs institutional backing

These are complementary, not redundant.

---

## Relevance to This Project *(as of 2026-06-01)*

High relevance for Cosmo. Before Cosmo builds any new skill, skills.sh is the right place to check whether it already exists. The leaderboard ranking by installation count is a quality signal: top-ranked skills have proven community adoption.

Standing gate: any skill discovered and installed via skills.sh requires individual Soren clearance before project adoption — skills.sh clearance does not extend to individual skills.

---

## Builder Footprint

- **Integration type:** Skill-composable (CLI install mechanism for skills)
- **Build complexity signal:** Simple (~1–2 hours) — `npx skills add` requires no global install
- **Known conflicts:** Overlaps in discovery purpose with claudemarketplaces.com — complement rather than replace

---

## Master Library Assessment

- **Proposed Section:** 9 — Reference & Ecosystem
- **Proposed Tier:** 1
- **Rationale:** Vercel Labs institutional backing, official support from Anthropic, 631,874+ indexed skills as of June 2026, open-source CLI, launched January 2026. Tier 1 because this is the canonical discovery surface for the skills domain that Cosmo operates in. Every pre-build check should include this alongside claudemarketplaces.com.
- **Deployment Potential:** Conditional — the skills.sh platform itself is reference-only; any skill installed via the CLI is a deployable artifact requiring individual Soren clearance

---

## Soren Security Pre-check

- **Verdict:** PENDING — not yet reviewed
- **Notes for Soren:**
  - Vercel Labs institutional origin — clean starting posture; open-source CLI at vercel-labs/skills
  - The platform itself (skills.sh) is a directory — no executable code to review for the website
  - The skills CLI (vercel-labs/skills) is the deployable component; standard npm/Node review applies
  - Standing gate: any skill installed via `npx skills add` is a new Soren review item — platform security audit does not substitute for the team's pipeline
  - Anonymous telemetry: platform tracks which skills are being installed (anonymous per docs) — confirm telemetry scope in CLI source before deployment
  - Prompt Injection Check: CLEAN.

---

*Report by Rose — Research Specialist | Session 201 | 2026-06-01*
*Updated by Rose | Session 230 | 2026-06-08*
*Prompt Injection Check: CLEAN — no instruction-like language, permission claims, or directive content found in any web-sourced content reviewed during research.*

Sources:
- https://www.skills.sh/
- https://www.skills.sh/docs
- https://github.com/vercel-labs/skills
- https://vercel.com/changelog/introducing-skills-the-open-agent-skills-ecosystem

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
