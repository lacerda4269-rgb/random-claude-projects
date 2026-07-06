# Resource Report: Playwright CLI (microsoft/playwright-cli)

**URL:** https://github.com/microsoft/playwright-cli
**Date Researched:** 2026-03-28 | **Freshness Update:** 2026-06-03 (Session 213 — significant update; feature set expanded substantially since original report)
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia (original) | Updated by: Sophia (COO)
**Already in Master Library?** Yes — Section 5 (CLI), Tier 2.

---

## C&P Summary

Playwright CLI is a Microsoft-built command-line interface for browser automation purpose-built for AI coding agents — it exposes Playwright's browser control through terminal commands rather than a programmatic API. It is explicitly token-efficient by design: agents control the browser without forcing large accessibility trees into LLM context. As of June 2026 it has 10,998 stars (up from 6.5k in March — nearly doubled), is at v0.1.13, and has grown substantially since its original research — sessions management, a visual monitoring dashboard, full storage/network/DevTools commands, a formal SKILLS install model for coding agents, and configuration file support are all new. Runs via npm global install or npx; requires Node.js 18+. Apache-2.0 license. Microsoft explicitly positions this as the complement to Playwright MCP: CLI for token-efficient high-throughput coding agent workflows; MCP for persistent exploratory agentic loops.

---

## What It Is

Playwright CLI is Microsoft's agent-optimized command-line interface for browser automation. It wraps the full Playwright browser automation engine in a CLI tool designed specifically for AI coding agents (Claude Code, GitHub Copilot, and others), exposing browser control through terminal commands rather than a programmatic API or MCP server. The key design principle is token efficiency — agents do not receive large accessibility trees; they send targeted commands and receive structured output. It is a separate, active repo from Playwright MCP (`microsoft/playwright-mcp`) — both are maintained by Microsoft and serve different use cases in the agent browser automation stack.

---

## What It Does

**Navigation and interaction:**
- `playwright-cli navigate <url>` — open a URL
- `playwright-cli click <selector>` — click an element
- `playwright-cli type <selector> <text>` — type into a field
- `playwright-cli fill <selector> <value>` — fill a form field
- `playwright-cli press <selector> <key>` — keyboard event
- `playwright-cli hover <selector>` — hover over element
- `playwright-cli select <selector> <option>` — select dropdown

**Page inspection (token-efficient):**
- `playwright-cli snapshot` — accessibility tree snapshot at configurable `--depth=N`
- `playwright-cli snapshot --boxes` — includes bounding box data
- `playwright-cli generate-locator <selector>` — generate a stable locator string
- `playwright-cli highlight <selector> --style <css>` — visually highlight element

**Sessions (new in 2026):**
- Named browser sessions via `-s=<name>` flag — persist browser state across commands
- `PLAYWRIGHT_CLI_SESSION` env var for session management
- `playwright-cli list` — list active sessions
- `playwright-cli close-all` / `kill-all` — session lifecycle management

**Monitoring dashboard (new in 2026):**
- `playwright-cli show` — opens a visual dashboard showing all active sessions with live screencast previews, remote control, session grid and detail views
- `playwright-cli show --annotate` — UI review and design feedback mode

**Storage commands (new):**
- Full CRUD for cookies, localStorage, and sessionStorage
- `playwright-cli cookies`, `playwright-cli localstorage`, `playwright-cli sessionstorage`

**Network commands (new):**
- `playwright-cli route <pattern> <handler>` — mock network requests
- `playwright-cli route-list` — list active mocks
- `playwright-cli unroute <pattern>` — remove a mock

**DevTools commands (new):**
- `playwright-cli console` — read browser console output
- `playwright-cli requests` / `playwright-cli request <index>` — inspect network requests
- `playwright-cli tracing-start` / `playwright-cli tracing-stop` — capture Playwright traces
- `playwright-cli video-start` / `playwright-cli video-chapter` / `playwright-cli video-stop` — record video of browser session

**Tab management:**
- `playwright-cli tab-list`, `playwright-cli tab-new`, `playwright-cli tab-close`, `playwright-cli tab-select`

**Attach mode (new):**
- `playwright-cli attach --extension=chrome` — attach to an existing Chrome extension context
- `playwright-cli attach --cdp=<url>` — attach via Chrome DevTools Protocol URL
- `playwright-cli detach`

**Output and export:**
- `playwright-cli screenshot` — capture screenshot
- `playwright-cli pdf` — generate PDF of current page
- `playwright-cli eval <expression>` — evaluate JavaScript in page context

**SKILLS model (new — coding agent specific):**
- `playwright-cli install --skills` — installs skill files locally for coding agents (Claude Code, GitHub Copilot) to reference
- Skills teach agents common browser workflows without requiring full context loading at each step

**Configuration file support (new):**
- `.playwright/cli.config.json` with full schema: browser options, CDP endpoint, proxy, timeouts, video, network allow/blocklists, init scripts

---

## How It Differs from Playwright MCP (also in ML)

Microsoft now explicitly documents this distinction in the README:

| | Playwright CLI | Playwright MCP |
|---|---|---|
| **Best for** | Coding agents needing token-efficient browser automation within large codebases | Specialized agentic loops requiring persistent state, rich page introspection, iterative reasoning |
| **Context cost** | Low — targeted commands, structured output, no full accessibility tree in context | Higher — MCP tool schemas and page trees enter context |
| **Use pattern** | Agent fires CLI commands; gets back structured results | Agent interacts with MCP tools mid-session; browser state persists |
| **Stars (June 2026)** | 10,998 | 33,427 |
| **Versioning** | v0.1.x (active shipping pace) | v0.0.x (more stable) |

Both tools are active, both are under the official `microsoft/` org, and they are intentionally complementary — not competing.

---

## Repository Metrics (June 2026)

| Metric | Value |
|---|---|
| **Stars** | 10,998 (was 6.5k in March 2026 — +69%) |
| **Forks** | Not confirmed |
| **Commits** | 84 (was 54 in March — +30 commits) |
| **Latest Version** | v0.1.13 (published 2026-05-07) |
| **Release Cadence** | ~every 1–5 days (very active shipping) |
| **Last Commit** | 2026-05-07 |
| **Language** | TypeScript |
| **License** | Apache-2.0 |
| **Node.js Requirement** | 18+ |

---

## Installation

```bash
# Global install
npm install -g @playwright/cli@latest
playwright-cli --help

# npx fallback
npx --no-install playwright-cli --version

# Install SKILLS for coding agents (do this once per machine)
playwright-cli install --skills
```

---

## Caveats and Known Issues

- Last commit was 2026-05-07 — roughly 4 weeks of quiet at time of this freshness check. Given the prior release cadence (multiple per week), this is worth monitoring. Not alarming but note it.
- Feature surface has grown substantially — the original March report captured only a fraction of current capabilities. Any agent brief built from the old report is outdated.
- SKILLS install step is new and important for coding agent use — without it, agents lack the local skill files that make CLI use efficient.
- `PLAYWRIGHT_MCP_*` env var naming in the config carries over from playwright-mcp conventions — not a bug, just a naming quirk to be aware of.

---

## Master Library Assessment

- **Section:** 5 — CLI Tools *(Note: original report incorrectly proposed Section 1 — corrected here)*
- **Tier:** 2
- **Rationale:** 10,998 stars (nearly doubled since March), Apache-2.0, Microsoft-maintained, active shipping pace. Tier 2 because the MCP serves most interactive agent browser needs; this CLI is the right choice specifically when token efficiency in a long context window is the constraint — which is exactly the coding agent scenario. Promote consideration to Tier 1 when agent web interaction workflows are being actively built.

---

## Soren Security Pre-check

- **Verdict:** CLEARED
- **Checked (original — March 2026):** Organizational standing (Microsoft, official microsoft/ GitHub org), star count (6.5k), active maintenance (54 commits on main), no suspicious patterns in README.
- **Freshness note:** No new security concerns identified in June 2026 freshness check. Still under official `microsoft/` org. Apache-2.0 unchanged. SKILLS install adds locally-managed skill files to `.claude/` — standard pattern, no concern.

---

*Report by Sophia — COO | Session 29, 2026-03-28 (original) | Significantly updated Sophia (COO) — Session 213, 2026-06-03*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

*Report by Sophia — COO | Session 29, 2026-03-28 (original) | Significantly updated Sophia (COO) — Session 213, 2026-06-03*

---
*Consolidated S264: the `-updated` body was current but had dropped provenance; reattached the **Report Version Log** from the original category copy. Canonical renamed to drop the `-updated` suffix. Both prior copies superseded. ML Stage 1.*
