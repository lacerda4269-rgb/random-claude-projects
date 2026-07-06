# Resource Report: Visual Explainer

**URL:** https://github.com/nicobailon/visual-explainer
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
An agent skill that transforms complex terminal output into professionally styled HTML pages — interactive visualizations, Mermaid diagrams, data tables, and slide decks — invoked via slash commands.

## What It Does
- Generates rich HTML pages or interactive slide decks for: diagrams, diff reviews, plan audits, data tables, project recaps
- Activated via slash commands: `/diff-review`, `/plan-review`, `/generate-slides`
- Dark/light theme support
- Useful for presenting backtest results, strategy comparisons, architecture diagrams, and session recaps
- MIT license, v0.6.3 (latest March 9, 2026), 7k stars

## Relevance to This Project
Visual output layer for any agent. Strategy performance summaries, parameter sweep results, plan audits — anything that benefits from a formatted visual output rather than raw terminal text. Relevant across trading, coding, and documentation workflows.

## Builder Footprint

- **Integration type:** Skill file — slash commands (`/diff-review`, `/plan-review`, `/generate-slides`) installed via Claude Code plugin marketplace or `.claude/` file placement; generates local HTML output files
- **Extension points:** HTML templates for each output type (diff review, plan audit, slide deck, data table) are customizable by Cosmo; dark/light theme toggles are configurable; Mermaid diagram support is built-in and automatically triggered by the relevant slash commands (Inferred from documentation — not explicitly documented)
- **Build complexity signal:** Low — file drop install; no dependencies beyond Mermaid.js (embedded in generated HTML, no separate install); output is local HTML files opened in browser; no server, no credentials
- **Known conflicts:** None identified. Output is local HTML — no external transmission. Compatible with all other Section 2 skills. Pair with Caveman to write compressed reports then render them as styled HTML.

## Master Library Assessment
- **Proposed Section:** 2 — Skills
- **Proposed Tier:** 1
- **Rationale:** Phase 1 core skill. 7k stars, MIT, active. Low setup overhead — invoke by slash command. High value across all domains.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** 7k stars, MIT license, v0.6.3 active release (March 9, 2026), nicobailon (individual developer, active GitHub). No malicious patterns detected.
- **Notes:** Generates local HTML output — no external network calls during use. Read-only skill access model.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Rose's v2.0 sweep shows 8,726 stars (grown from 8.2k), 584 forks, v0.7.1 (2026-04-27) unchanged — last pushed 2026-04-27. MIT license unchanged. No new releases since v1.0 check, but still active and maintained. CLEARED verdict stands.

## Recommendation
Add to Section 2, Tier 1. Phase 1 install alongside foundation skills.

---
*Report by Sophia | Session 31 | 2026-03-29*

---

## C&P Summary

Visual Explainer is an agent skill that transforms complex terminal output into professionally styled HTML pages — interactive visualizations, Mermaid diagrams, data tables, diff reviews, plan audits, and slide decks — via slash commands (`/diff-review`, `/plan-review`, `/generate-slides`). It generates local HTML output with no external network calls, runs at v0.6.3 with MIT license and 7k stars. For this project it is the visual output layer across all domains: strategy performance summaries, parameter sweep results, architecture diagrams, and session recaps all benefit from formatted visual output rather than raw terminal text.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
