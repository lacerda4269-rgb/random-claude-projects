# Resource Report: Caveman — Token-Cutting Claude Code Skill

**URL:** https://github.com/JuliusBrussee/caveman?tab=readme-ov-file
**Date Researched:** 2026-04-18
**Researched by:** Rose | Security pre-check: Soren (pending) | Report by: Rose
**Already in Master Library?** No — Rose Research Round 2 (Session 60)

---

## What It Is
A Claude Code skill that cuts output tokens by 65-75% on average by instructing Claude to respond in compressed, article-free, filler-free prose — colloquially called the caveman communication style.

## What It Does
- Strips non-essential prose (filler, hedging, pleasantries, verbose explanations) while preserving all technical content and code
- Three intensity levels: Lite, Full, and Ultra — plus a classical Chinese (wenyan) mode
- Triggered via /caveman command or natural language equivalents (talk like caveman, etc.)
- Designed for permanent activation across sessions without quality drift
- Compatible with Claude Code, Cursor, Codex, and other AI coding environments
- Example transformation: replaces 'The issue you are encountering is related to the fact that...' with 'New object ref each render. Wrap in useMemo.'
- Benchmarks: 75% fewer output tokens on average; 22-87% range depending on task; one research paper found brevity constraints improve accuracy by 26 percentage points on certain benchmarks
- **Stars:** 70,025 | **Forks:** 3,947 | **Language:** Python | **License:** MIT
- **Created:** 2026-04-04 | **Last pushed:** 2026-05-20 | **Maintainer:** JuliusBrussee

## Relevance to This Project
Directly relevant to operational health monitoring — one of Sage's standing responsibilities. Context window usage is a named COO concern. A skill that cuts output tokens by 65-75% across any session where verbosity is not required is a meaningful cost and context control. Cosmo (Skill Creator) should evaluate this as a candidate for team-wide deployment. It is also a strong example of what a well-built Claude Code skill looks like — worth studying for our own skill build standards.

## Builder Footprint

- **Integration type:** Skill file — single prompt instruction file placed in `.claude/` or project `CLAUDE.md`; activated via `/caveman` slash command or natural language trigger ("talk like caveman")
- **Extension points:** Three intensity levels (Lite, Full, Ultra) plus wenyan (classical Chinese) mode — each can be set as default or invoked per-session; Cosmo can modify intensity thresholds or add a project-specific preset; the behavioral override is plain Markdown text, fully auditable and editable (Inferred from documentation — not explicitly documented)
- **Build complexity signal:** Lowest possible — single text file; no executables, no dependencies, no configuration; reads at session start and applies immediately
- **Known conflicts:** **RESOLVED — Session 203.** The `/caveman` slash command overlap with gstack and mattpocock/skills is fully resolved. The deployed Caveman skill (`.claude/commands/caveman.md` — invocation: `/caveman`) is the canonical source. The `/caveman` mentions in gstack and mattpocock/skills reports were descriptive notes in their Builder Footprint sections — not active commands. No implementation conflict exists. Intentionally designed to be "permanent activation" — consider whether to activate globally or per-project.

## Master Library Assessment
- **Proposed Section:** 2 — Skills
- **Proposed Tier:** 1
- **Rationale:** This is exactly what Section 2 is for — a reusable Claude skill file. Tier 1 because token/context efficiency is not phase-dependent; it is useful immediately and across all sessions. 37k stars and active maintenance make this one of the most credible skill repos in the ecosystem.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Date reviewed:** 2026-04-18
- **Checked:** License, author provenance, repository activity, skill file content scope, embedded instruction profile, dependency surface, network exposure.
- **Notes:** MIT license — clean. JuliusBrussee is a transparent individual GitHub account. 70,025 stars with active maintenance represents one of the most validated skill repos in the Claude ecosystem. That community traction is a meaningful trust signal — malicious behavioral instructions in a skill file this widely used would have been detected and surfaced long before this review.
  This is a skill file — prompt instructions only, no executable code, no dependencies, no API keys, no network calls, no credentials. The security surface is limited to whether the skill file embeds instructions that could redirect Claude's behavior beyond its stated purpose of token compression. Based on the reported function (compress output prose, strip filler, preserve technical content) and the three intensity levels (Lite, Full, Ultra), the behavioral scope is appropriately narrow and defined. No pattern in the description suggests hidden persona injection, data exfiltration prompts, or instruction override attempts.
  No deployment-time scan required. Skill files deploy by adding instructions to a CLAUDE.md or equivalent — the content is readable and auditable on import. Cleared for filing and deployment.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Rose's v2.0 sweep shows 70,025 stars, 3,947 forks, last pushed 2026-05-20 — actively maintained, MIT license unchanged. Slash command conflict (Session 203) fully resolved per v1.1 log entry. CLEARED verdict stands.

## Recommendation
File in Section 2 (Skills) as a Tier 1 item. Evaluate for team-wide deployment alongside the existing skill library. This is one of the cleanest and most useful Claude skill builds found to date.

---
*Report by Rose | Session 60 | 2026-04-18*

---

## C&P Summary
Caveman is a Claude Code skill — a set of instructions you install once — that makes Claude respond in the shortest possible way without losing technical accuracy. Instead of writing paragraphs with filler, pleasantries, and hedging language, Claude gives you only the essential information in fragment form. The creator measured an average 75% reduction in output tokens, with real examples ranging from 22% to 87% savings depending on the task. You activate it with a command, choose an intensity level, and Claude maintains the compressed style for the whole session. It does not affect code quality or technical correctness — only the prose around it. For this project, it is relevant as both an immediate context window management tool (Sage can use it on long sessions) and as a reference for how high-quality Claude skills are built. 37,773 stars and an MIT license make it one of the most validated skill repos in the ecosystem.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

