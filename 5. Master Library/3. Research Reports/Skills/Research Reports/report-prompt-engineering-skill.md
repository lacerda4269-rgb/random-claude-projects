# Resource Report: Prompt Engineering Skill

**URL:** https://github.com/ckelsoe/prompt-architect (renamed from ckelsoe/claude-skill-prompt-architect — old URL redirects)
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
A Claude Code skill that transforms vague prompts into structured, expert-level prompts using 27 research-backed frameworks (CO-STAR, RISEN, RISE, TIDD-EC, and others). Available via NPM package.

## What It Does
- Applies 27 named prompt engineering frameworks
- Takes any prompt input and restructures it for maximum clarity and output quality
- Available as NPM package for easy install
- MIT license, 20 stars

## Relevance to This Project
Prompt quality affects every output across every agent. Better prompts = better results, fewer rounds of correction, lower token cost. Relevant for any complex instruction-writing task.

## Master Library Assessment
- **Proposed Section:** 2 — Skills
- **Proposed Tier:** 2
- **Rationale:** Useful but low community validation (20 stars). Medium priority — practical value is real but the skill itself is relatively simple to replicate. Monitor for a higher-adoption alternative.

## Soren Security Pre-check
- **Verdict:** FLAG — Low community validation
- **Checked:** 20 stars, MIT license, ckelsoe (individual developer). No malicious patterns detected.
- **Notes:** 20 stars is minimal validation. Functional based on description but low community adoption signals limited external review. Operator aware before install.
- **Re-reviewed 2026-06-08 — original FLAG cleared. Repo rename assessed.** Rose's v1.0 sweep (2026-06-08) confirms: 191 stars (was 105 at freshness review), MIT license confirmed, last pushed 2026-06-04, actively maintained. The low-validation flag from the original check was already resolved by Rose's Session 42 freshness review (stars grew 5x to 105). Current count of 191 reinforces that trajectory further. Repo rename from ckelsoe/claude-skill-prompt-architect to ckelsoe/prompt-architect is assessed as benign: (1) same author account (ckelsoe) — continuity confirmed; (2) old URL redirects cleanly; (3) rename reflects the tool's expanded cross-tool compatibility (Claude Code, ChatGPT, Gemini CLI, Cursor, Copilot, 30+ others) — the original name was Claude-specific, the new name is accurate; (4) no content disruption, no license change, no executable components added. Identity continuity confirmed. **Verdict updated: FLAG CLEARED.** Ready to deploy per Rose's Session 42 recommendation.

## Recommendation
Add to Section 2, Tier 2 with FLAG. Functional but low adoption — acceptable for use, monitor for better-validated alternatives.

---

## Rose's Freshness Review

**Date reviewed:** 2026-04-14 | **Reviewed by:** Rose

**What changed:** Significant. Stars have grown from 20 to 105 — more than 5x since the original report. Now confirmed as v3.2.2, last commit March 26, 2026, actively maintained. Framework count expanded to 27 across 7 intent categories. Cross-tool compatibility explicitly confirmed: Claude Code, ChatGPT, Gemini CLI, Cursor, Copilot, and 30+ others. The low-validation concern from the original report is resolved.

**Note:** Repository has been renamed from `claude-skill-prompt-architect` to `prompt-architect` — old URL redirects, no content disruption.

**C&P Summary:** This skill acts as a prompt coach inside your AI tool. You give it a rough or vague instruction — the kind you'd normally just type and hope for the best — and it scores it across five quality dimensions (clarity, specificity, context, completeness, structure), asks you targeted questions to fill any gaps, then rewrites the prompt using whichever of the 27 supported frameworks best fits the job. The result is a structured, expert-grade prompt ready to use immediately. It does not write code or run tasks — it improves your instructions before you send them, so the AI's output is more likely to match what you actually wanted the first time.

**Updated recommendation:** Low-validation flag is no longer valid. Star count has more than tripled, the skill is actively developed, and cross-tool compatibility is confirmed. Ready to accept.

---
*Report by Sophia | Session 31 | 2026-03-29*
*Rose Freshness Review — Session 42 | 2026-04-14*

---

## C&P Summary

The Prompt Engineering Skill is a Claude Code skill that acts as a prompt coach: it scores any input prompt across five quality dimensions (clarity, specificity, context, completeness, structure), asks targeted questions to fill gaps, then rewrites it using the best-fit framework from a library of 27 research-backed frameworks. The output is a structured, expert-grade prompt ready to use. Better prompts mean better results on the first pass and lower token cost across every agent interaction — relevant across all domains this project operates in. Originally flagged for low community validation (20 stars), that concern is resolved: the tool is now at v3.2.2 with 191 stars and confirmed cross-tool compatibility.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
