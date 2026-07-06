# Resource Report: Bifrost MCP

**URL:** https://github.com/biegehydra/BifrostMCP
**VS Code Marketplace:** Search "BifrostMCP"
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren (Tier 2 — VS Code extension) | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
A VS Code extension that exposes VS Code's language server capabilities to Claude and other AI assistants via an MCP server running locally on port 8008.

## What It Does
- Find references, definitions, and implementations across a full codebase
- Symbol search across the entire workspace
- Semantic code analysis and type information
- Works with any VS Code-supported language (C#, Python, etc.)
- C# support via the VS Code C# extension — critical for NinjaScript files
- Runs as HTTP/SSE server; multi-project setup supported

## MCP Tool Manifest

- **Tool count:** ~8 tools (VS Code language server capabilities exposed via local HTTP/SSE on port 8008)
- **Tools:**
  - `find_usages` — Find all references/usages of a symbol across the entire workspace; takes textDocument URI and cursor position
  - `find_definitions` — Jump to the definition(s) of a symbol; returns file path and position
  - `find_implementations` — Find all implementations of an interface or abstract method
  - `find_type_definitions` — Find the type definition for a symbol
  - `rename_symbol` — Rename a symbol across all files in the workspace; returns proposed changes as diff
  - `get_symbol_info` — Get type information and documentation for a symbol at a given position
  - `list_workspace_symbols` — Search all symbols in the workspace by name or pattern
  - `get_diagnostics` — Retrieve current error and warning list from the Problems panel
- **Transport type:** HTTP/SSE (local server on port 8008; not stdio — Bifrost runs as a VS Code extension that starts the HTTP server)
- **settings.json registration:**
```json
{
  "mcpServers": {
    "bifrost": {
      "type": "http",
      "url": "http://localhost:8008"
    }
  }
}
```
Note: VS Code must be open with the BifrostMCP extension active for the server to be available. Install from VS Code Marketplace ("BifrostMCP" by Connor Hallman). C# support requires the VS Code C# extension installed alongside.
- **Recommended serverInstructions:** "Bifrost MCP exposes VS Code's language server capabilities — find all references, jump to definitions, list workspace symbols, and get type information. Requires VS Code with BifrostMCP extension running. For NinjaScript (C#) work, also requires the VS Code C# extension."

## Relevance to This Project
NinjaScript is C#. When Claude edits strategy files, Bifrost lets it understand the full codebase — not just one file. Traces how indicators connect to entry logic, finds where variables are used across files, catches type errors before compiling in NinjaTrader.

## Master Library Assessment
- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** High value for NinjaScript development but phase-dependent. Most useful once active strategy coding begins. VS Code extension — install path is simpler than Docker-based MCPs.

## Soren Security Pre-check
- **Verdict:** FLAG — AGPL-3.0 License
- **Checked:** 205 stars, 68 commits, available on VS Code Marketplace (Tier 2 review applied — publisher reputation checked, actively maintained, recent commits confirmed). No malicious patterns detected in README or description.
- **Notes:** AGPL-3.0 is a copyleft license. For local/personal use in a development environment this does not create obligations. However, if any software incorporating Bifrost's output is ever distributed or run as a service, AGPL terms apply. Operator decision: acceptable for personal dev use; flag before any commercial distribution.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Stars now 215 (was ~207–209); last push 2026-03-27 (~2 months ago — activity slowed but repo is not abandoned). No new security disclosures. AGPL-3.0 flag for personal dev use remains the correct posture. No changes to clearance conditions.

## Recommendation
Add to Section 4, Tier 2. Operator aware of AGPL-3.0 terms — acceptable for personal development use. Install when active NinjaScript coding begins.

---

## Rose's Freshness Review

**Date reviewed:** 2026-04-14 | **Reviewed by:** Rose

**What changed:** Stars have grown significantly — now ~207–209 (the original report noted 205). Actively maintained, AGPL-3.0 confirmed. The tool has gained clear traction in the VS Code / MCP developer community. No change to the license situation.

**C&P Summary:** Bifrost is a VS Code extension that acts as a bridge between Claude and VS Code's internal code intelligence tools — the same tools VS Code uses when you right-click and choose "Find All References" or "Rename Symbol." Without Bifrost, Claude working on your code has to guess at how functions and variables relate to each other by reading raw text. With Bifrost installed, it can actually query VS Code's language server: find every place a function is called, look up type definitions, get the full error list from the Problems panel, and understand what a symbol means in context. For NinjaScript (C#) work specifically, this means Claude can trace how indicators connect across files and catch type errors before they hit the NinjaTrader compiler. The AGPL-3.0 license is fine for personal development — the only constraint is if software incorporating Bifrost were ever distributed commercially, at which point legal review would be needed.

**Updated recommendation:** Strong tool with growing adoption. AGPL license is a non-issue for personal dev use. Original recommendation stands — install when active NinjaScript coding begins.

---
*Report by Sophia | Session 31 | 2026-03-29*
*Rose Freshness Review — Session 42 | 2026-04-14*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---

## C&P Summary

Bifrost is a VS Code extension that acts as a bridge between Claude and VS Code's internal code intelligence tools — the same tools VS Code uses when you right-click and choose "Find All References" or "Rename Symbol." Without Bifrost, Claude working on your code has to guess at how functions and variables relate to each other by reading raw text. With Bifrost installed, it can actually query VS Code's language server: find every place a function is called, look up type definitions, get the full error list from the Problems panel, and understand what a symbol means in context. For NinjaScript (C#) work specifically, this means Claude can trace how indicators connect across files and catch type errors before they hit the NinjaTrader compiler. The AGPL-3.0 license is fine for personal development — the only constraint is if software incorporating Bifrost were ever distributed commercially, at which point legal review would be needed.
