# Resource Report: Playwright MCP (Microsoft)

**URL:** https://github.com/microsoft/playwright-mcp
**Date Researched:** 2026-05-02 | **Freshness Update:** 2026-06-03 (Session 213)
**Researched by:** Rose | Security pre-check: Soren | Report by: Rose
**Already in Master Library?** Yes — Section 4 (MCP Servers), Tier 2.

---

## C&P Summary

Playwright MCP is Microsoft's official plug-in that lets Claude control a web browser directly without needing to "see" the screen through screenshots. Instead, it reads the browser's accessibility data — the same structured information used by screen readers — so Claude can navigate pages, fill forms, click buttons, and extract content using text descriptions instead of images. It is the best choice when Claude needs to browse interactively or maintain browser context across multiple steps, rather than running a single automated script. Full tool schema inspected and confirmed clean — no telemetry, no data collection, no phone-home behavior. Microsoft-built, Apache-2.0 license, 33,427 stars (June 2026). 66 confirmed tools. Microsoft now explicitly documents this tool as the complement to Playwright CLI — MCP for persistent, iterative browser sessions; CLI for token-efficient high-throughput agent automation.

---

## What It Is

An official Microsoft MCP server that exposes Playwright browser automation capabilities to LLMs. Uses Playwright's accessibility tree — structured, deterministic representations of web page content — to let Claude interact with browsers through text. The accessibility-tree approach is faster and lighter than visual approaches and does not require a vision model.

---

## What It Does

- Full browser automation accessible to Claude via MCP tools
- Accessibility-tree based — no vision model required; structured data only
- Tabs management, network mocking, storage management, PDF generation
- DevTools integration and tracing
- Deterministic interactions — avoids the ambiguity of screenshot-based approaches
- 66 tools organized into modes (accessibility tree mode is default; screenshot mode adds vision-based equivalents) — up from 63 at original report; new additions include cookie management, session/local storage CRUD, form-fill, and video chapter tools

---

## MCP Tool Manifest

- **Tool count:** 66 tools confirmed (June 2026) — core, tab, network, storage, DevTools, coordinate, PDF, test-assertion, cookie, session/local storage, form, video chapter categories
- **Selected core tools:**
  - `browser_navigate` — Open a URL in the browser
  - `browser_snapshot` — Get the current page accessibility tree
  - `browser_click` — Click an element identified by accessibility tree selector
  - `browser_type` — Type text into a focused input element
  - `browser_fill` — Fill a form field with a value
  - `browser_screenshot` — Take a screenshot
  - `browser_run_code_unsafe` — Execute arbitrary Playwright script for complex interactions
  - `browser_generate_pdf` — Generate a PDF of the current page
- **Transport type:** stdio
- **settings.json registration:**
```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp@latest"]
    }
  }
}
```

---

## How It Differs from Playwright CLI (already in ML)

- **Playwright CLI** — best for coding agents doing token-efficient, task-specific automation
- **Playwright MCP (this item)** — best for exploratory, long-running workflows where Claude needs persistent browser context, rich introspection, and iterative reasoning over page structure

Both belong in the ML — they serve different use cases.

---

## Builder Footprint

- **Integration type:** MCP tool layer
- **Build complexity signal:** Simple (~1–2 hours) — npx auto-install; no separate browser binary install required
- **Known conflicts:** None. Playwright CLI and Playwright MCP are complementary. The parent Playwright framework (Section 5, CLI) is the foundational dependency.

---

## Master Library Assessment

- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** 33,427 stars (June 2026), Apache-2.0, Microsoft-maintained. Tier 2 over Tier 1 because the CLI covers most agent browser automation needs; this is the right tool for richer interactive sessions. Microsoft now explicitly positions MCP vs CLI in the README — MCP for persistent exploratory loops, CLI for token-efficient coding agent workflows.

---

## Soren Security Pre-check

- **Verdict:** CLEARED
- **Notes:** Full tool schema inspected (63 tools confirmed). No telemetry tools. No analytics endpoints. No data collection packages. License (Apache-2.0), maintainer (official Microsoft organization). The `browser_run_code_unsafe` capability is documented by Microsoft as "not a security boundary" — operator responsibility.

*Source: Soren Security Review — Round 3 Follow-Up Verdicts, 2026-05-02. Clearance confirmed in Full Database.*

---

*Report by Rose — Research Specialist | 2026-05-02 | Freshness update by Sophia (COO) — Session 213, 2026-06-03*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---
*Consolidated S264: the `-updated` body was current but had dropped provenance; reattached the **Report Version Log** from the original category copy. Canonical renamed to drop the `-updated` suffix. Both prior copies superseded. ML Stage 1.*
