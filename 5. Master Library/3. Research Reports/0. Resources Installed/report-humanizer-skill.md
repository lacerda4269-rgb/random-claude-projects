# Resource Report: Humanizer — AI Writing Detector and Rewriter Skill

**URL:** https://github.com/blader/humanizer
**Date Researched:** 2026-04-18
**Researched by:** Rose | Security pre-check: Soren (pending) | Report by: Rose
**Already in Master Library?** No — Rose Research Round 2 (Session 60)

---

## What It Is
A Claude Code skill that rewrites AI-generated text to remove characteristic AI writing patterns, producing output that reads as natural human prose instead.

## What It Does
- Analyzes text against 29 documented AI writing patterns drawn from a documented reference on AI writing signs
- Four pattern categories: Content (significance inflation, vague attributions, formulaic language), Language (AI vocabulary, passive voice overuse, synonym cycling), Style (em dash overuse, title case, emoji use), Communication (sycophantic tone, chatbot artifacts, filler phrases)
- Two-pass rewriting: first pass transforms, second pass audits for remaining AI-isms and cleans them
- Voice calibration feature: user can provide writing samples to match their personal style, not just generic humanized output
- Triggered via /humanizer command followed by text, or natural language equivalent
- No installation of code — this is a skill file (prompt/instructions)
- Compatible with Claude Code and OpenCode
- **Stars:** 22,923 | **Forks:** 2,192 | **Language:** None (skill file) | **License:** MIT
- **Created:** 2026-01-18 | **Last pushed:** 2026-06-07 | **Maintainer:** blader

## Relevance to This Project
Relevant to Sophia (Project Scribe) and to any content the team produces that will be read externally — SOPs, AARs, documentation, or any client-facing writing. Sophia already produces written deliverables; a skill that removes AI-isms from her outputs could improve the quality of final documents. Also relevant if Jay uses Claude for any writing outside this project that needs to read as human-authored. The voice calibration feature is particularly useful — it means Sophia could be trained to match a specific writing style rather than defaulting to a generic output.

## Master Library Assessment
- **Proposed Section:** 2 — Skills
- **Proposed Tier:** 2
- **Rationale:** Section 2 is correct — this is a Claude skill file. Tier 2 rather than Tier 1 because it is not needed immediately (current phase is not producing public-facing content), but will be useful when the team is producing SOPs, AARs, or any externally visible deliverables. 14k stars and MIT license make it well-validated.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Date reviewed:** 2026-04-18
- **Checked:** License, author provenance, repository activity, skill file content scope, embedded instruction profile, dependency surface, network exposure.
- **Notes:** MIT license — clean. blader is a transparent individual GitHub account. 22,923 stars with a last-push date of 2026-06-07 represents strong community validation for a skill file. Similar to Caveman, the traction level makes undetected malicious instruction embedding highly unlikely.
  Skill file only — no executable code, no dependencies, no API keys, no network calls, no credentials. The security surface is the skill file content itself. The stated scope (rewrite text to remove AI writing patterns across 29 documented categories, with a two-pass audit and optional voice calibration) is behaviorally bounded and legible. The 29-pattern reference is drawn from publicly documented sources, which is a transparent design choice. Nothing in the feature set suggests instruction override, persona injection, or data handling outside the rewrite task itself.
  One note on the voice calibration feature: the user provides writing samples to calibrate style matching. Those samples stay local — this is a prompting feature, not a data-collection feature. No external transmission of user-provided samples is implied or architecturally possible for a skill file. Cleared for filing and deployment.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Rose's v1.0 sweep shows 22,923 stars (grown from 14,383), last pushed 2026-06-07 — recently active. MIT license unchanged. CLEARED verdict stands.

## Recommendation
File in Section 2 (Skills) as a Tier 2 item. Flag for Sophia as a quality tool for final document delivery. Voice calibration capability makes it more useful than standard humanizer tools.

---
*Report by Rose | Session 60 | 2026-04-18*

---

## C&P Summary
Humanizer is a Claude Code skill — a set of instructions you install once — that rewrites AI-generated text to sound like a person wrote it. It works by checking your text against 29 known patterns that AI models tend to produce: things like overusing em dashes, writing in overly formal passive voice, repeating the same filler phrases, inflating the significance of everything, and using an AI-typical vocabulary. The skill does two passes — the first rewrites, the second audits the rewrite for any remaining AI-isms and cleans them out. There is also a voice calibration feature: you give it samples of your own writing and it rewrites to match your style rather than producing generic output. For this project, it is most relevant for Sophia (Project Scribe) and for any documents this team produces that are meant to be read externally — SOPs, AARs, reports. It is a Claude skill file with no executable code, MIT licensed, and 22,923 stars, which makes it one of the more validated skill repos available.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

