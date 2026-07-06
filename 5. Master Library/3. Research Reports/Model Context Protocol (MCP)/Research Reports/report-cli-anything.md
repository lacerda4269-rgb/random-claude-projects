# Resource Report: CLI-Anything

**URL:** https://github.com/HKUDS/CLI-Anything
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** Yes — Section 7, Tier 2, status not specified in briefing

---

## What It Is
CLI-Anything is an open-source tool that automatically transforms any desktop software application into an agent-native command-line interface, enabling AI agents to control applications like GIMP, Blender, Audacity, and LibreOffice through structured CLI commands rather than fragile UI automation.

## What It Does
Runs a 7-phase generation pipeline: analyzes source code, designs command architecture, implements a Click CLI, plans and writes tests, generates documentation, and publishes packages. Outputs structured JSON responses alongside human-readable formats. Auto-generates SKILL.md files that agents can detect post-installation. Includes a CLI-Hub Marketplace for autonomous tool discovery and installation. Supports Claude Code, OpenCode, Codex, and GitHub Copilot CLI. 42.4k stars, 4.0k forks, 1,800+ passing tests, latest release v0.3.0 (2026-04-24), active as of 2026-06-08.

## MCP Tool Manifest

- **Tool count:** CLI-Anything does not expose pre-defined MCP tools directly. Instead, it generates new CLI interfaces for any target desktop application — those generated CLIs can then be registered as tools. The MCP component surfaces the auto-generated commands and the CLI-Hub Marketplace catalog.
- **Tools (framework-level):**
  - `generate_cli` — Run the 7-phase pipeline to auto-generate a CLI for a specified desktop application
  - `install_cli` — Install a generated CLI from the CLI-Hub Marketplace into the local environment
  - `list_available_clis` — Browse the CLI-Hub Marketplace for available auto-generated CLIs
  - `discover_skills` — Auto-detect installed CLIs and their generated SKILL.md files for agent use
  - `run_cli_command` — Execute a structured command on an installed auto-generated CLI and return structured JSON output
- **Transport type:** stdio
- **settings.json registration:**
```json
{
  "mcpServers": {
    "cli-anything": {
      "command": "python",
      "args": ["-m", "cli_anything.server"]
    }
  }
}
```
- **Recommended serverInstructions:** "CLI-Anything auto-generates structured CLIs for desktop applications (GIMP, Blender, Audacity, etc.) and makes them agent-callable. Use generate_cli to create a new CLI for a target app, then discover_skills to surface it. Output is always structured JSON."

## Relevance to This Project
Medium relevance currently — high potential relevance as the project scales to include desktop agent work (e.g., a NinjaTrader or TradingView desktop agent controlling native software). The ability to auto-generate a structured CLI for any application is directly aligned with the Desktop-CoWork Agent's role. Section 7 placement is appropriate now; this could move to Section 1 (MCP Servers) or Section 2 (Skills) when desktop agent phases begin.

## Master Library Assessment
- **Proposed Section:** 7 — Alternative Tools & Notable Ecosystem
- **Proposed Tier:** 2
- **Rationale:** The existing ML entry (Section 7, Tier 2) is accurate. 42.4k stars (up from 24.2k) and active maintenance confirm high-value ecosystem status. Tier 2 is correct — relevant when desktop automation phases begin, not a current priority.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** Star count (42.4k as of 2026-06-08, up from 24.2k), fork count (4.0k, up from 2.2k), commit count (261), test coverage (1,800+ passing tests), organization identity (HKUDS — same as LightRAG, Hong Kong University of Data Science), language composition, CLI-Hub Marketplace design, multi-platform support claims
- **Notes:** HKUDS is a credible academic research organization (same as LightRAG). High test coverage (1,800+ tests) signals engineering maturity. No suspicious patterns. The auto-generation pipeline and marketplace concept are ambitious but well-documented. No external call-home patterns noted beyond standard CLI-Hub registry queries.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Stars now 42.4k (was 24.2k); last push 2026-06-08 (active today); latest release v0.3.0 (2026-04-24). HKUDS academic provenance confirmed consistent with LightRAG track record. No new CVEs or security disclosures. CLEARED status stands with no conditions.

## Recommendation
Current ML entry is accurate — Section 7, Tier 2 is correct. Suggest noting in the ML entry that this is a strong candidate for promotion to Section 2 (Skills) or Section 1 when the NinjaTrader/TradingView desktop agent work begins. No corrections to current classification needed.

---
*Report by Sophia | Session 29 | 2026-03-28*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---

## C&P Summary

CLI-Anything is an open-source tool from Hong Kong University of Data Science (same team as LightRAG) that automatically transforms any desktop software application into an agent-native command-line interface. It runs a seven-phase pipeline — analyzing source code, designing command architecture, implementing a Click CLI, writing tests, generating documentation, and publishing packages — outputting structured JSON alongside human-readable formats. For this project, its most relevant future use is enabling the Desktop-CoWork Agent to control applications like NinjaTrader or TradingView through structured CLI commands rather than fragile UI automation. Currently Section 7, Tier 2 — strong candidate for promotion when desktop agent phases begin.
