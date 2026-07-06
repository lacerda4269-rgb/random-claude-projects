# Resource Report: Playwright (Microsoft — Main Framework)

**URL:** https://github.com/microsoft/playwright
**Date Researched:** 2026-05-02 (Freshness check: 2026-05-14)
**Researched by:** Rose | Security pre-check: Soren | Report by: Rose
**Already in Master Library?** Yes — Section 5 (CLI), Tier 1. Full Database entry references Round 3 consolidated report. This individual file is a retrofit — content extracted from Rose-Research-Report-Round-3.md and the Tier 1 Freshness Addendum.

---

## C&P Summary

Playwright is Microsoft's web browser automation framework — the industry standard for writing code that controls browsers automatically. Think of it as the engine underneath all web testing and scraping work. It supports Chrome, Firefox, and Safari from a single codebase, handles timing automatically so tests do not break unpredictably, and runs tests in parallel for speed. The team already has Playwright CLI (the agent-optimized command-line version) and Playwright MCP (the stateful browser session plugin) in the Master Library — this is the full parent framework that both of those layers sit on top of. Pete, Nick, and Todd will need it when building or testing anything browser-dependent. Apache-2.0 license, 90,511 stars as of June 2026 (was 88.7k in May), latest version v1.60.0, actively maintained by Microsoft.

---

## What It Is

Playwright is Microsoft's flagship web testing and automation framework. It lets developers write code that controls browsers — Chromium, Firefox, and WebKit — through a single unified API. One test suite runs across all three engines. It is the most widely adopted browser automation framework in active use today, and the parent framework that both playwright-cli (already in ML) and playwright-mcp (also in ML) are built on top of.

---

## What It Does

- Cross-browser testing and automation (Chromium, Firefox, WebKit) from one codebase
- Auto-wait assertions — no manual sleeps or fragile timeouts
- Resilient locators based on user-visible attributes
- Test isolation via browser contexts (each test gets a clean session)
- Parallel test execution across configured browsers
- Execution tracing with screenshots, video capture, and network logs
- Device emulation and network request interception
- Multiple interfaces: test runner, library API, CLI for coding agents, MCP server

---

## Relationship to Other Playwright ML Items

The ML has three Playwright items that serve distinct needs:
- **Playwright (this item)** — the full framework; parent of the other two. Primary use: writing test code and running automation scripts.
- **playwright-cli** (Section 5) — AI-specific CLI layer; agent use without test code authorship; token-efficient.
- **playwright-mcp** (Section 4) — MCP server for stateful interactive Claude sessions using accessibility tree.

---

## Invocation Interface

- **Node.js:** `npx playwright test` (test suite) or programmatic via `const { chromium } = require('playwright')`
- **Python:** `playwright install` then `from playwright.sync_api import sync_playwright`
- **Key flags:** `--reporter=json` for machine-readable results; `--output` for artifacts directory
- **Exit codes:** 0 = all tests passed; 1 = tests failed

---

## Builder Footprint

- **Integration type:** Framework library (TypeScript/Node.js and Python)
- **Build complexity signal:** Medium (~half-day) — npm or pip install + separate browser binary install (`playwright install` downloads ~300–500MB of browser binaries)
- **Known conflicts:** None. Playwright CLI and Playwright MCP are the agent-optimized layers built on top of this framework — they require this framework for full capability.

---

## Master Library Assessment

- **Proposed Section:** 5 — CLI (alongside playwright-cli; same family; note parent/child relationship)
- **Proposed Tier:** 1
- **Rationale:** 90,511 stars (as of June 2026; was 88.7k in May 2026), Apache-2.0, Microsoft-maintained, v1.60.0. The most validated browser automation framework available. Foundational dependency for multiple future project tracks.

---

## Soren Security Pre-check

- **Verdict:** CLEARED
- **Notes:** Apache-2.0. Microsoft-maintained. No credentials required for the framework itself. No prompt injection vectors. No unusual permissions.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Stars updated 88.7k → 90,511; forks confirmed (5,881); latest version v1.60.0; last push 2026-06-08. Actively maintained. No new CVEs, no ownership changes, no license changes. Clearance holds.

*Source: Soren Security Review — Round 3, 2026-05-02. Clearance confirmed in Full Database.*

---

## Version Log

| Version | Date | What Changed |
|---------|------|--------------|

---

*Report by Rose — Research Specialist | 2026-05-02 (Retrofit to individual file — Session 201)*
*Prompt Injection Check: Not applicable — content extracted from internal Round 3 consolidated report.*
