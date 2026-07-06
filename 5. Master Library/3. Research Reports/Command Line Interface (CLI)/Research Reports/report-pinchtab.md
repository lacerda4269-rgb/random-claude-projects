# Resource Report: PinchTab

**URL:** https://github.com/pinchtab/pinchtab
**Site:** https://pinchtab.com/
**Date Researched:** 2026-04-21
**Researched by:** Rose | Security pre-check: Soren (pending) | Report by: Rose
**Already in Master Library?** No — new submission, Batch 1

---

## What It Is

A high-performance, self-contained Go binary that gives AI agents direct control over Chrome via a plain HTTP API — purpose-built for AI agent browser automation with a focus on token efficiency, stealth, and session persistence.

## What It Does

- Runs as a standalone HTTP server (defaults to `127.0.0.1:9867`) — any agent, script, or language can call it via HTTP
- Headless and headed Chrome operation: supports invisible task execution and visible profiles with persisted auth, cookies, and extensions
- Multi-instance orchestration: runs multiple parallel Chrome processes with isolated profiles simultaneously
- Token efficiency: uses the browser's Accessibility Tree instead of screenshots — approximately 5–13x cheaper than screenshot-based approaches; 9.5–20.3% cheaper than comparable tools in benchmarks
- Stable Element References (e.g., `e0`, `e5`, `e21`) — avoids flaky CSS selectors
- Stealth mode: patches `navigator.webdriver`, spoofs user-agent, hides automation flags — passes major bot detection checks
- Session persistence: cookies, auth, and tabs survive restarts; log in once, stay logged in
- Installs as a user-level daemon for persistent background operation
- ~12–15MB self-contained binary; no external service dependencies

## Technical Details

- **Language:** Go (65.3%), TypeScript dashboard (12.5%), Shell (15.9%)
- **License:** MIT
- **Stars:** 9,169 (as of June 2026; was 8.8k in April 2026)
- **Forks:** 678
- **Total Commits:** 1,666+
- **Last Release:** v0.13.2 — June 2026 (was v0.9.1, April 15, 2026 — rapid release cadence)
- **Created:** February 15, 2026 (rapid growth from launch)
- **Go version requirement:** Go 1.25+
- **Platform:** macOS and Linux primary; Windows supported but less automated test coverage
- **Installation:** `curl -fsSL https://pinchtab.com/install.sh | bash`, Homebrew, npm, or Docker
- **No telemetry; no required outbound dependencies**

## How It Works

Three-tier architecture:
- **Server** — main control plane managing profiles, instances, routing, and the dashboard
- **Instance** — a running Chrome process associated with one profile
- **Bridge** — lightweight runtime managing a single browser instance, typically spawned by the server

The server exposes an HTTP API. Agents interact via simple commands (`pinchtab nav`, `pinchtab snap`, `pinchtab click`, `pinchtab fill`) or via direct HTTP calls to `localhost:9867` for multi-instance programmatic workflows. The dashboard is TypeScript-based and locks to localhost unless HTTPS is configured.

## Relevance to This Project

A strong alternative to Browser Harness for agent browser automation, with more features, more maturity, and more explicit security design. The token-efficiency angle is significant for cost-aware agent pipelines. Multi-instance support means it can serve multiple parallel agents simultaneously — relevant if the team scales to parallel agent sessions.

## Master Library Assessment

- **Proposed Section:** 3 — CLI & Standalone Tools
- **Proposed Tier:** 2
- **Rationale:** Standalone CLI/daemon — not an MCP or skill. MIT-licensed, 9,169 stars, actively maintained, strong security posture. Tier 2 because it is not core infrastructure but is the strongest available option for AI agent browser control. Compare and choose against Browser Harness at deployment time — both are Section 3, Tier 2 candidates. Soren review required before installation.

## Soren Security Pre-check

- **Verdict:** PENDING — not yet reviewed
- **Re-reviewed:** 2026-06-08 — verdict remains PENDING. Rose's freshness sweep (v0.9.1 → v0.13.2, stars 8.8k → 9,169, last push 2026-06-06) confirms active maintenance and no new security disclosures. The PENDING status reflects that Soren has not yet performed a full security review — not that concerns were found. Full review required before install. The items flagged below for Soren's review remain unchanged.
- **Notes for Soren:** Go binary, MIT license, ~12–15MB self-contained — no external dependencies. Loopback-only default binding is a positive security posture. Stealth mode (webdriver patching, UA spoofing) is worth understanding from a use-ethics standpoint. Install script (`install.sh`) should be reviewed before execution. No telemetry confirmed. Developers explicitly warn against internet-facing deployment without explicit security configuration — document this as an operator responsibility.

## Recommendation

Queue for Soren security review alongside Browser Harness (report-browser-harness.md) — Lexi and Sage should choose one or both at deployment time. If cleared: add to Section 3, Tier 2. PinchTab is the more feature-complete option; Browser Harness is the more minimal one. Review the install script before running it.

---

## C&P Summary

PinchTab is a small, fast Go program (about 12MB) that runs in the background and lets AI agents control a real Chrome browser by sending simple web requests — no complicated setup, no framework required. It is specifically designed for AI agents: instead of taking expensive screenshots, it reads the page as text (the same way a screen reader would), which can be 5 to 13 times cheaper in terms of AI token usage. It supports running multiple browser sessions at once with separate logins, and browsers remember your login information between restarts. For this project, it is the most capable and cost-efficient browser automation option available — relevant any time an agent needs to interact with a website, and especially valuable if multiple agents are running browser tasks in parallel.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

## Sources

- [GitHub — pinchtab/pinchtab](https://github.com/pinchtab/pinchtab)
- [PinchTab website](https://pinchtab.com/)
- [Dataconomy — PinchTab: The next big leap in AI browser control after OpenClaw](https://dataconomy.com/2026/03/04/pinchtab-ai-browser-control-guide/)
- [Emelia.io — PinchTab: A 12MB Binary That Replaces Playwright for AI Agents](https://emelia.io/hub/pinchtab-browser-ia)
- [GitHub Projects on Threads](https://www.threads.com/@githubprojects/post/DVUnFQjgfrw/high-performance-browser-control-for-ai-agents-pinchtab-is-a-lightweight-mb-go)
- [Hermes Agent Issue #493 — Pinchtab Skill feature request](https://github.com/NousResearch/hermes-agent/issues/493)
- [Ecosyste.ms — pinchtab/pinchtab](https://awesome.ecosyste.ms/projects/github.com/pinchtab/pinchtab)
