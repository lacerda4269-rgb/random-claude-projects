# Resource Report: Superpowers

**URL:** https://github.com/obra/superpowers
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** Yes — Section 5, status: 🗄️ Archived

---

## What It Is
Superpowers is an agentic skills framework and software development methodology for coding agents — providing composable skills for design, planning, execution, testing, and code review workflows.

## What It Does
Provides structured workflow skills including: `brainstorming` (Socratic design refinement), `writing-plans` (breaking work into 2-5 minute tasks), `subagent-driven-development` (dispatches specialized agents per task with two-stage review), and `test-driven-development` (enforces RED-GREEN-REFACTOR cycles). Available on Claude Code marketplace, Cursor, Codex, OpenCode, and Gemini CLI. Built by Jesse Vincent (Prime Radiant). Currently at v5.1.0 (May 4, 2026), with 221,099 stars, 19,668 forks.

## Relevance to This Project
The archive decision needs revisiting. This repo is actively maintained (v5.0.6 released March 25, 2026 — three days ago), has 120k stars, and is available on the Claude Code marketplace. The `subagent-driven-development` and `writing-plans` skills are directly relevant to this project's orchestration and task breakdown patterns. Archiving this was premature.

## Builder Footprint

- **Integration type:** Skill framework — installed via Claude Code marketplace (`/plugin marketplace add obra/superpowers`) or by placing the skill files in `.claude/`; each skill is individually invocable
- **Extension points:** Each workflow skill (brainstorming, writing-plans, subagent-driven-development, TDD) is independently modifiable; Cosmo can layer project-specific variants on top; multi-platform (Claude Code, Cursor, Codex, OpenCode, Gemini CLI) (Inferred from documentation — not explicitly documented)
- **Build complexity signal:** Low — marketplace install or file drop; no CLI, no dependencies, no configuration; all five phases (Brainstorm → Plan → Execute → Verify → Review) activate on invocation
- **Known conflicts:** None identified. `/caveman` exists in both Superpowers and the standalone Caveman skill — functionally the same; no conflict, just overlap to note. Compatible with gstack, mattpocock/skills, Andrej Karpathy Skills.

## Master Library Assessment
- **Proposed Section:** 2 — Skills
- **Proposed Tier:** 1
- **Rationale:** 120k stars, active v5 release, and Claude Code marketplace availability make this a tier-1 skills resource. The workflow patterns — particularly subagent dispatching with two-stage review and TDD enforcement — are directly applicable to this project's agent orchestration work.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** Star count (221,099), fork count (19,668), latest release (v5.1.0, May 4 2026), creator identity (Jesse Vincent, Prime Radiant), license (MIT), marketplace listing, active Discord community
- **Notes:** No security concerns. Active development, credible creator, MIT license, multi-platform marketplace listing. The project is demonstrably legitimate and widely adopted.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Rose's v2.0 sweep shows 221,099 stars (grown from 191k), 19,668 forks, v5.1.0 unchanged (last pushed 2026-06-03), MIT license unchanged. One of the most widely adopted skills frameworks in the Claude ecosystem. CLEARED verdict stands.

## Recommendation
FLAG the archive decision for review. This repo is actively maintained, just released v5.0.6, and has 120k stars — archiving is not justified by any standard criteria. Recommend moving to Section 2 (Skills), Tier 1, status Pending. Bring to the operator's attention before finalizing the ML entry change.

---
*Report by Sophia | Session 29 | 2026-03-28*

---

## C&P Summary

Superpowers is an agentic skills framework and software development methodology by Jesse Vincent (Prime Radiant) providing composable workflow skills for design, planning, execution, testing, and code review — including Socratic design refinement, task breakdown into 2–5 minute units, subagent-dispatched development with two-stage review, and enforced TDD cycles. At 221,099 stars, v5.1.0 released May 4, 2026, with a Claude Code marketplace listing, it is one of the most widely adopted skills frameworks available. The `subagent-driven-development` and `writing-plans` skills are directly applicable to this project's orchestration and task breakdown patterns. The original archive decision is flagged for reversal — a resource this active and broadly adopted does not belong archived.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
