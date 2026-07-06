# Resource Report: Agent-Browser (Browser Automation for AI Agents)

**URL:** https://github.com/vercel-labs/agent-browser
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)
**Type:** Agent Skill + CLI Tool (hybrid — filed under Skills as primary type)

---

## What It Is
A headless browser automation CLI from Vercel Labs built natively in Rust — optimized specifically for AI agents. Agents can open pages, click, fill forms, capture screenshots, and verify web outputs without dumping full DOM trees into context.

## What It Does
- 15+ command categories: navigation, page inspection, element interactions, data extraction, JavaScript execution
- Three browser modes: headless Chromium, real Chrome (with profile support), cloud-hosted remote browsers
- Works with Claude Code, Codex, Cursor, Gemini CLI, and other AI platforms
- Token-efficient design: structured output instead of raw HTML
- Built in Rust — fast and lightweight
- 25.6k stars, 492 commits, active development

## Relevance to This Project
Web verification and content extraction for agents. Verify platform changes, extract data from web-based tools, check broker interface updates — without loading raw HTML into context. Also useful for content workflows (scrape → summarize → report).

## Builder Footprint

- **Integration type:** Skill + CLI Hybrid — Rust binary (`agent-browser`) installed via cargo or release download; invoked as a CLI tool; skill documentation loaded into `.claude/` for agent instruction
- **Extension points:** Each of the 15+ command categories (navigation, page inspection, element interactions, data extraction, JavaScript execution) is independently usable; Cosmo can write skill files wrapping specific command sequences for common agent workflows (Inferred from documentation — not explicitly documented)
- **Build complexity signal:** Medium — Rust binary install + PATH configuration; three browser modes require different setup (headless Chromium auto-included; real Chrome needs local Chrome install; cloud mode needs credentials); no MCP overhead
- **Known conflicts:** Cloud browser mode transmits data to external servers — do not use cloud mode for sensitive operations; headless/local modes are clean. Compatible with playwright-cli and Playwright MCP (different use cases — Agent-Browser is token-efficient task automation; Playwright is full framework).

## Master Library Assessment
- **Proposed Section:** 2 — Skills (primary); CLI capability noted
- **Proposed Tier:** 1
- **Rationale:** Phase 1 install. 25.6k stars, Vercel Labs (highly reputable), Rust-native, token-efficient. Broad usefulness across all domains.

## Soren Security Pre-check
- **Verdict:** CLEARED — re-check complete (Session 146 freshness sweep; license change trigger)
- **License at original check:** MIT
- **License at re-check:** Apache-2.0 (confirmed current; change detected during Session 146 freshness sweep)
- **Re-evaluation:** Apache-2.0 is a permissive open-source license. For this team's use case (installation and internal use — no distribution), the license change introduces no new deployment restrictions or conditions. Key differences vs. MIT: (1) Apache-2.0 includes an explicit patent grant — a net benefit, not a restriction; (2) Apache-2.0 requires preservation of NOTICE files when redistributing the software — this requirement does not apply to installation or internal use; the team is not a redistributor. No behavioral change required. Prior clearance conditions carry forward unchanged.
- **Checked:** Original check criteria confirmed still valid — Vercel Labs organization (reputable), Rust-based (memory-safe), no external data transmission required for headless/local mode. No malicious patterns detected. License change reviewed and cleared.
- **Notes:** Cloud-hosted browser mode involves external data transmission — use headless or local Chrome mode for sensitive operations. This condition is unchanged from original clearance.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Rose's v2.0 freshness sweep shows 35,562 stars, v0.27.1 (2026-06-01), last pushed 2026-06-05 — actively maintained. Apache-2.0 license unchanged. CLEARED verdict stands. Cloud-mode data-transmission condition unchanged.

## Recommendation
Add to Section 2, Tier 1. Phase 1 install. Use local/headless mode for operations involving sensitive data.

---
*Report by Sophia | Session 31 | 2026-03-29*

---

## C&P Summary

Agent-Browser is a headless browser automation CLI from Vercel Labs built in Rust, designed specifically for AI agents to navigate pages, click elements, fill forms, capture screenshots, and extract data — without dumping raw HTML into context. It supports 15+ command categories and three browser modes (headless Chromium, real Chrome with profile, cloud-hosted), and is compatible with Claude Code, Cursor, Gemini CLI, and others. The token-efficient structured output design is a direct fit for this project's cost optimization focus. Installed at Phase 1; use local or headless mode for any operations involving sensitive data.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
