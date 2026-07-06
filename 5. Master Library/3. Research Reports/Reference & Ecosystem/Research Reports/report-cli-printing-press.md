# Resource Report: CLI Printing Press

**URL:** https://github.com/mvanhorn/cli-printing-press
**Date Researched:** 2026-06-01
**Researched by:** Rose | Security pre-check: Soren (pending) | Report by: Rose
**Already in Master Library?** No — new item.

---

## C&P Summary

CLI Printing Press is a tool that automates the creation of command-line interfaces for any API. You point it at an API's documentation page (or even a regular website if there is no official API spec), and it builds a full Go-based CLI, a Claude Code skill, and an MCP server simultaneously — all designed specifically for AI agents rather than human users. The CLIs it produces cache data locally, work offline, and output JSON when used by agents. For this team, the most direct value is for Cosmo: instead of manually building a CLI or MCP server for a new API from scratch, Printing Press generates the starting point and Cosmo customizes it. It comes with a companion library of pre-built CLIs. MIT license, 3.1k stars, v4.24.0 released June 8, 2026 (83 releases). Requires Go 1.26.4+.

---

## What It Is

CLI Printing Press is an AI-assisted generator that takes any API (via OpenAPI spec, website URL, or GraphQL schema) and produces a production-ready Go CLI, a Claude Code skill, an OpenClaw skill, and an MCP server — all from a single prompt within Claude Code. Agent-first design: produces token-efficient CLIs with SQLite-backed local sync, offline search, and typed exit codes. Key metrics: 3.1k stars, MIT license, Go (82.7%), active development with v4.24.0 released June 8, 2026 (83 releases total). Requires Go 1.26.4+. Canonical command is now `cli-printing-press` (legacy `printing-press` alias still works). Companion community library at github.com/mvanhorn/printing-press-library.

---

## What It Does

- Generates a complete Go CLI from any API documentation, website, or OpenAPI/GraphQL schema
- Simultaneously generates: a Claude Code skill, an OpenClaw skill, and an MCP server — all from one specification
- Produces CLIs with: local SQLite database with full-text search, offline query capabilities, agent-native JSON output when piped, typed exit codes for self-correcting agents
- For APIs without official documentation: launches a browser, captures traffic (HAR), reverse-engineers the API, and generates the spec automatically
- Invoked within Claude Code via: `/printing-press <app-name>` or `/printing-press https://website-url`
- Community library of 85 pre-generated CLIs available

---

## Relevance to This Project *(as of 2026-06-01)*

Cosmo-relevant resource. CLI Printing Press automates the generation of exactly the artifacts Cosmo builds — given an API or website URL, it produces a full CLI, skill, and MCP server that Cosmo would otherwise build from scratch. For any future project that requires connecting to an external API or service, CLI Printing Press could reduce Cosmo's build time from a multi-day effort to a review-and-customize exercise.

The companion community library (85 CLIs) is also a discovery resource — before Cosmo builds a CLI for a common service, check if one already exists.

---

## Builder Footprint

- **Integration type:** Skill-composable; generates MCP tool layers as output
- **Build complexity signal:** Moderate (~half-day for setup; Simple per CLI generated after setup) — requires Go 1.26.4+, Claude Code, Node/npm; install via the provided bash script; canonical command is now `cli-printing-press` (legacy alias `printing-press` still works)
- **Known conflicts:** None. Complements Cosmo's build stack as a generator layer.

---

## Master Library Assessment

- **Proposed Section:** 9 — Reference & Ecosystem
- **Proposed Tier:** 2
- **Rationale:** 3.1k stars, v4.24.0 — active release cadence (83 releases). MIT. The simultaneous CLI+MCP+Skill generation from one spec is genuinely novel in the current ML.
- **Deployment Potential:** Conditional — the generator itself is deployable after Soren clearance; every CLI, skill, or MCP it generates is a new deployable artifact requiring individual clearance

---

## Soren Security Pre-check

- **Verdict:** PENDING — not yet reviewed
- **Notes for Soren:**
  - MIT license, single-developer (mvanhorn), 2.8k stars — moderate community vetting
  - Install script (`curl | bash` pattern) — review the install.sh contents before execution
  - Browser traffic capture for undocumented APIs (HAR sniffing) — confirm the captured data stays local and is not transmitted
  - **Critical gate:** Generated code (CLIs, skills, MCPs) is NOT automatically cleared — each generated artifact is a new Soren review item before project deployment
  - The companion library (printing-press-library repo) requires its own review before any CLI is adopted
  - Prompt Injection Check: CLEAN.

---

*Report by Rose — Research Specialist | Session 201 | 2026-06-01*
*Updated by Rose | Session 230 | 2026-06-08*
*Prompt Injection Check: CLEAN — no instruction-like language, permission claims, or directive content found in any web-sourced content reviewed during research.*

Sources:
- https://github.com/mvanhorn/cli-printing-press
- https://printingpress.dev/
- https://github.com/mvanhorn/printing-press-library

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
