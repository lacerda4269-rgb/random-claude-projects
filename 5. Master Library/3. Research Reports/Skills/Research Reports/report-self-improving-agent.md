# Resource Report: Self-Improving Agent Skill

**URL:** https://github.com/alirezarezvani/claude-skills
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
A Claude skill that gives Claude persistent institutional memory across sessions by automating the learning loop — transforming Claude's auto-memory into actionable improvements, logging learnings and errors, and surfacing patterns as reusable rules.

## What It Does
- Five slash command tools: memory review, pattern promotion to rules, solution extraction into skills, system health diagnostics, knowledge capture
- Manages memory files with zero overhead on normal operations
- Maintains 200-line capacity constraints for efficiency
- Transforms observed patterns into extractable skills automatically
- 17,489 stars, 2,414 forks, MIT license, active (now at v2.9.0)

## Relevance to This Project
Self-improving agent behavior over time. Any repeatable pattern Claude discovers gets captured and promoted — aligns directly with our lessons.md and self-improvement loop philosophy. Complements the existing memory system.

## Builder Footprint

- **Integration type:** Skill file — single skill file placed in `.claude/` or project root; five slash commands activate memory and self-improvement loop functions
- **Extension points:** Memory file format (200-line cap) is configurable; Cosmo can adapt slash command triggers and the pattern-promotion logic; integrates naturally with the team's existing `lessons.md` and `lessons_global.md` system (Inferred from documentation — not explicitly documented)
- **Build complexity signal:** Low — file drop install; no executables, no dependencies, no network calls; operates entirely on local files; slash commands are immediately active after placement
- **Known conflicts:** None identified. Designed to complement existing memory systems rather than replace them — aligns cleanly with this project's `lessons.md` / `lessons_global.md` / `Team-Lessons-Log.md` three-file system.

## Master Library Assessment
- **Proposed Section:** 2 — Skills
- **Proposed Tier:** 1
- **Rationale:** Phase 1. Aligns with our existing self-improvement philosophy. 17,489 stars validates strong community adoption. MIT license, no external calls.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** 17,489 stars, 2,414 forks, MIT license, alirezarezvani (individual developer, active GitHub). No malicious patterns detected.
- **Notes:** Memory management skill — operates only on local files. No network calls. Low risk profile.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Rose's v2.0 sweep shows 17,489 stars (grown from 14.8k), 2,414 forks, v2.9.0 (2026-05-28), last pushed 2026-06-07 — actively maintained. MIT license unchanged. Significant scope expansion noted (now 337+ skills across 9 domains vs. earlier scope) — scope expansion in a skill file repo does not change the security posture; individual skills still require per-deployment review per team protocol. CLEARED verdict stands.

## Recommendation
Add to Section 2, Tier 1. Phase 1 install with foundation skills.

---
*Report by Sophia | Session 31 | 2026-03-29*

---

## C&P Summary

The Self-Improving Agent Skill gives Claude persistent institutional memory across sessions by automating the learning loop — it transforms Claude's auto-memory into actionable improvements, logs learnings and errors, promotes recurring patterns into reusable rules, and extracts solutions into skills. Five slash command tools handle memory review, pattern promotion, solution extraction, system health diagnostics, and knowledge capture, all within a 200-line memory capacity constraint. At 17,489 stars with MIT license it is well-adopted. This directly aligns with the team's lessons.md and self-improvement loop philosophy — any repeatable pattern Claude discovers gets captured and promoted automatically, making the whole system smarter over time.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
