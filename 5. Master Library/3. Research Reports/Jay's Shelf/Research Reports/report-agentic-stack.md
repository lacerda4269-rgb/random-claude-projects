# Resource Report: agentic-stack

**URL:** https://github.com/codejunkie99/agentic-stack
**Date Researched:** 2026-04-22
**Researched by:** Rose | Security pre-check: Soren | Orchestrated by: Sage
**Already in Master Library?** No

---

## Data Integrity Notice

> **Read this first.** The initial fetch of the repo landing page returned a detailed description of features, file structure, and internal scripts. Every follow-up attempt to access individual files (README.md, install.sh, install.ps1, auto_dream.py, adapters/claude-code.md, tree/main) returned HTTP 404. The main repo page, releases page, and stargazers page returned successfully.
>
> **What this means:** The detailed feature descriptions in this report (four-layer memory, auto_dream.py, specific skill names, etc.) come from the first fetch only and could not be independently verified. It is possible the WebFetch model generated plausible-sounding descriptions based on the repo name and visible metadata rather than actual file content. All unverified content is clearly marked below.
>
> **The verified facts** are limited to: repo existence, star/fork count, release history, license, primary language, and author identity.

---

## What It Claims to Do (UNVERIFIED — from initial fetch only)

agentic-stack describes itself as a portable `.agent/` folder system that maintains AI agent memory, skills, and protocols across multiple coding environments — Claude Code, Cursor, Windsurf, and others. The concept is a shared coordination layer that persists across harnesses so you do not lose accumulated context when switching surfaces.

Claimed features (unverified):
- Four-layer memory architecture: working, episodic, semantic, personal
- Query-aware retrieval with salience × relevance scoring
- Nightly compression script (`auto_dream.py`) that stages lessons for agent review
- Five seed skills: skillforge, memory-manager, git-proxy, debug-investigator, deploy-checklist
- CLI review tools: graduate.py, reject.py, reopen.py
- Optional FTS5 full-text search (beta); falls back to ripgrep/grep
- Eight harness adapters including Claude Code, Cursor, Windsurf

**Because individual files could not be loaded, none of the above has been audited.**

---

## What Is Verified

| Item | Verified Value |
|------|---------------|
| Repo URL | https://github.com/codejunkie99/agentic-stack |
| Stars | 2,091 (up from 1,357 at original research) |
| License | Apache 2.0 |
| Primary language | Python (95.7%) |
| Author | codejunkie99 (v0.8.0 contributors: @aliirz, @smartsastram) |
| Oldest release | v0.3.0 — April 16, 2026 |
| Latest release | v0.18.0 (as of June 2026; was v0.8.0 at original research) |
| Last commit | 2026-05-10 |
| License history | Relicensed to Apache 2.0 at v0.7.2 (previously unknown license) |
| Repo age at time of research | ~6 days (original); now ~7 weeks old |

---

## Relevance to This Project

High concept relevance, zero deployment readiness.

Jay's stated interest is exactly on target conceptually — a single `.agent/` folder that bridges Claude Code, Cursor, and any future surface (Desktop Code tab, CoWork) would directly address the cross-surface coordination challenge the team has been designing around. The four-layer memory model and harness adapter architecture map well to what this project is trying to build.

The gap between concept and deployment is wide, and until the source code can actually be read and audited, it stays a concept.

---

## Soren Security Pre-check

**Verdict: HOLD (cannot clear what cannot be read)**

| Check | Finding |
|-------|---------|
| File accessibility | All individual file paths returned 404 — source code cannot be audited |
| Repo age | ~6 days old. No track record. |
| Star acquisition rate | 1,357 stars in ~6 days. Highly abnormal. Comparable legitimate repos take months to reach that level organically. |
| Stargazer quality | Mix of multi-year accounts and several 2026-created accounts. Possible artificial inflation. |
| License change | Relicensed to Apache 2.0 at v0.7.2. Prior license is unknown — cannot determine if original terms imposed restrictions that survived the relicense. |
| Release cadence | 6 releases in 5 days. Extremely fast — either genuine rapid iteration or cosmetic versioning to simulate maturity. |
| Auto-execution risk | Repo claims a nightly Python cron script (`auto_dream.py`). Unauditable. Any auto-executing script that cannot be read is automatically a HOLD. |
| Installation scripts | install.sh and install.ps1 claimed but inaccessible. Installer scripts not audited = no clearance to run. |
| Author identity | codejunkie99 — no known reputation, no organizational backing, anonymous. |
| Commit history | Not visible during research. Absence of visible history is atypical for a repo with 6 releases. |

**Bottom line:** The concept cannot be separated from the code, and the code cannot be read. Operator decision Session 73: repo RETIRED — do not use, do not revisit. Concept preserved for a future Cosmo build instead.

**Re-reviewed 2026-06-08 — verdict confirmed.** Rose's freshness sweep noted version jump v0.8.0→v0.18.0 and star growth (1,357→2,091). Continued active development does not resolve the core flags: source files were unauditable at original research (404s), abnormal star acquisition pattern, auto-executing scripts that cannot be verified, anonymous author. Growth is not a clearance signal. RETIRED verdict stands — operator decision Session 73 remains in effect.

---

## Master Library Assessment

- **Proposed Section:** 9 — Jay's Shelf (archived reference — concept only)
- **Proposed Tier:** 3
- **Status:** RETIRED — DO NOT USE. Do not revisit this repo.
- **Rationale:** Too many unanswered flags. Unauditable source code, abnormal star acquisition, suspicious engagement pattern, auto-executing scripts that cannot be read. The concept is sound; this repo is not the vehicle. Operator decision: Session 73.

---

## Recommendation

Do not use. Do not revisit. The repo is retired from consideration entirely.

**What to do with the concept:** The cross-harness memory and coordination idea is the right direction for this team. Cosmo should build it. A purpose-built coordination layer tailored to this team's specific surfaces — using Claude's Agent Teams feature, Pete's Python/LiteLLM bridge, and the existing soul/skill architecture — would be more useful than any third-party dependency. Full auditability, no unknown code running on the system, designed around how this team actually works. See Cosmo Concept Note below.

---

## Cosmo Concept Note

**Concept:** Build a portable cross-surface coordination layer for this team — the idea behind agentic-stack, built right and built specifically for us.

**What it would do:** Maintain agent memory, skills, and behavioral context persistently across Claude Code (VS Code extension + terminal), Cursor extension, Desktop Code tab, and any future surface. A coordination structure that any surface can read and write, so context does not reset when switching harnesses.

**Why Cosmo, why later:** This is a Skill or MCP build — Cosmo's lane. Not actionable until Agent Onboarding (Project 5), when the team's surface architecture is fully defined and Pete's Python layer is in place. The right time to design this is after the first real project, when the team knows exactly what cross-surface friction looks like in practice.

**Inputs Cosmo should reference at build time:**
- Claude's Agent Teams feature (experimental now — revisit when stable; report-parallel-agents-cross-llm.md)
- Pete's LiteLLM cross-LLM bridge (cross-model coordination layer)
- Pete's PyWinAuto/PyDirectInput desktop automation layer
- The existing soul/skill architecture (what's already persistent vs. what resets per session)
- Active surfaces at build time: Claude Code, Cursor, Desktop Code tab, potential CoWork

**Source:** Concept inspired by agentic-stack research — Session 73. This file is the record.

---

*Researched and written: Sage (Rose role — operator-directed single-item override, outside normal submission list protocol) | Session 73 — COHK 2 | 2026-04-22*
*Updated: Operator decision Session 73 — repo RETIRED, Cosmo concept note added.*
*Freshness sweep: Rose | Session 229 | 2026-06-08 — stars updated (1,357 → 2,091), latest release updated (v0.8.0 → v0.18.0), last commit date added (2026-05-10). Repo is still active — continued development since retirement decision. Status remains RETIRED per operator decision — the security flags and auditability concerns that drove that decision have not been resolved; continued growth does not change the verdict.*

---

## C&P Summary

agentic-stack is a Python-based system that claims to provide a portable `.agent/` folder maintaining AI agent memory, skills, and protocols across multiple coding harnesses — Claude Code, Cursor, Windsurf, and others. 2,091 stars (up from 1,357), Apache 2.0 license, latest release v0.18.0 (was v0.8.0), last commit 2026-05-10. **Operator decision: RETIRED — do not use, do not revisit.** Individual source files returned 404 during research — code is unauditable. Continued growth and active releases do not resolve the underlying security flags. Soren verdict: too many flags. The concept (cross-surface agent coordination layer) is sound and worth building — queued as a future Cosmo build at Agent Onboarding, using Pete's Python/LiteLLM layer and the existing soul/skill architecture instead of a third-party dependency.

---

## Report Version Log

| Version | Date | What Changed |
|---------|------|--------------|
