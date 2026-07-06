# Resource Report: Skill-Vetter

**URL (best match found):** https://github.com/UseAI-pro/openclaw-skills-security
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
A security-first vetting skill for agent skills before installation. The best current match found is openclaw-skills-security by UseAI-pro, built for OpenClaw (the open-source Claude Code alternative) — functionally equivalent to the Skill-Vetter concept described in the old list.

## What It Does
- Four-step vetting: metadata validity check → permission scope analysis → content analysis for suspicious patterns → typosquuat detection
- Read-only file access (does not modify anything it reviews)
- Trust scoring system (v1.0.0 scores: 97 on self-check)
- 62 stars, 9 forks, last pushed 2026-03-10

## Important Note on Scope
The old list described a generic "Skill-Vetter" for any skill before installation. The best current match is scoped to OpenClaw skills. It may not natively cover Claude Code SKILL.md files in the same way. Soren's pipeline already fulfills this function for all incoming resources — this skill would provide agent-level automated vetting as an additional layer.

## Master Library Assessment
- **Proposed Section:** 2 — Skills
- **Proposed Tier:** 2
- **Rationale:** Useful security layer but lower priority than foundation skills. Soren already covers manual vetting. 42 stars — limited community validation. Revisit when a more broadly-scoped version exists.

## Soren Security Pre-check
- **Verdict:** CLEARED with note
- **Checked:** 62 stars, MIT license (confirmed), UseAI-pro organization. No malicious patterns detected.
- **Notes:** Limited community adoption. Last pushed 2026-03-10 — not updated in 3+ months. Scope is OpenClaw-specific — may need adaptation for pure Claude Code use. Functional but narrow.
- **Re-reviewed 2026-06-08 — verdict confirmed with staleness flag.** Rose's v1.0 sweep shows 62 stars (minor growth from 42), 9 forks, last pushed 2026-03-10 — repo now inactive for approximately 3 months. MIT license confirmed. The CLEARED with note verdict stands; staleness is noted but not a disqualifier at this tier given the narrow scope and existing caveat. Soren's pipeline remains the primary security gate. CLEARED with note verdict stands.

## Recommendation
Add to Section 2, Tier 2 with note on scope limitation. Monitor for a broader Claude Code-native Skill-Vetter. Soren's pipeline remains the primary security gate.

---
*Report by Sophia | Session 31 | 2026-03-29*

---

## C&P Summary

Skill-Vetter (filed as openclaw-skills-security) is a security vetting skill for agent skills before installation — running a four-step check: metadata validity, permission scope analysis, content scanning for suspicious patterns, and typosquuat detection. It is the best current match for the "Skill-Vetter" concept in the old source list, though its scope is OpenClaw-specific and may need adaptation for pure Claude Code use. At 62 stars it has limited community validation. Soren's manual vetting pipeline already fulfills this function as the primary security gate; this skill would add an automated agent-level layer on top of it.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
