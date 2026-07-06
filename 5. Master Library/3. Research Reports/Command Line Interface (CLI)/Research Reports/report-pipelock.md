# Resource Report: Pipelock

**Prepared by:** Rose (Researcher)
**Reviewed by:** Soren (Security Manager)
**Tasked by:** Sage (COO)
**Date:** April 15, 2026
**Category:** Soul Folder — Security Tools
**Role in Stack:** Standby (runtime firewall) — Category 3 (MCP Server Scanning)
**Status:** Research complete — pending Soren configuration

---

## What It Is

Pipelock is an open-source AI agent firewall from the `luckyPipewrench/pipelock` GitHub project. Unlike Snyk Agent Scan (which performs pre-deployment configuration scanning), Pipelock sits inline as a runtime firewall between agents and the internet. It is built specifically for the agentic AI threat model — Claude Code, Cursor, OpenAI Agents SDK, and similar tools. License: Apache 2.0 — free including commercial use. Single Go binary with zero runtime dependencies. Self-hosted.

**Repository Metrics (June 2026):** 704 stars | 80 forks | v2.6.0 (latest release) | Last push: 2026-06-08 | Actively maintained.

---

## What It Does

- Bidirectional MCP scanning — scans both inbound tool descriptions and outbound agent responses for prompt injection and tool poisoning
- 48 built-in DLP (Data Loss Prevention) patterns for detecting data exfiltration attempts
- SSRF (Server-Side Request Forgery) protection with DNS rebinding prevention
- Per-domain rate limiting
- Tool poisoning detection at runtime
- Prompt injection blocking between agents and MCP servers
- Acts as a proxy layer: `pipelock mcp proxy` wraps stdio or HTTP MCP servers with scanning
- Compatible with Claude Code, Cursor, and OpenAI Agents SDK

---

## Installation & Setup (Windows)

1. Download the Pipelock binary from the GitHub releases page: `github.com/luckyPipewrench/pipelock/releases`
2. Place the binary in a folder on your system PATH
3. Verify: `pipelock --version`
4. To wrap an MCP server with Pipelock scanning: `pipelock mcp proxy --server [server-command]`
5. Configuration for specific MCP clients (Claude Code, Cursor, etc.) varies — refer to the Pipelock README for client-specific integration instructions

**Note:** Pipelock is more infrastructure than a one-command scan tool. It requires planning around which MCP servers to proxy and how to integrate it into the active agent environment. This is a Walk-phase setup, not a Crawl-phase install.

---

## Free Tier Details

Completely free. No usage limits. No account required. Self-hosted only. Apache 2.0 license allows commercial use without restriction. There is no paid tier.

---

## Limitations

- Runtime infrastructure commitment — unlike Snyk Agent Scan (run once, check a config), Pipelock must be deployed and maintained as a persistent proxy layer in the active environment
- More setup complexity than any other Cat 3 tool — it is a firewall, not a scanner
- Does not replace Snyk Agent Scan for pre-deployment configuration scanning — these tools serve different phases (Pipelock is runtime; Agent Scan is pre-deployment)
- Does not perform file malware scanning — DLP patterns catch data exfiltration but not traditional malware
- Newer and smaller community than Snyk Agent Scan
- Full capability assessment on Windows should be verified against current Pipelock documentation — the Go binary approach should work, but client-specific integration steps may vary

---

## Role in Soren's Pipeline

Pipelock is the standby for Category 3 — it is not needed in the Crawl phase but becomes the runtime layer when the team moves to Walk phase with live agents running MCP servers. Snyk Agent Scan handles pre-deployment: scan the MCP configuration before it goes live. Pipelock handles runtime: sit inline and actively block threats while agents are operating. The two tools cover different moments in the pipeline and are designed to complement each other, not replace each other.

---

## Soren Security Pre-check

- **Verdict:** CLEARED
- **Reviewed:** 2026-06-08

Apache 2.0, single Go binary, self-hosted, no external service calls, no account required, no telemetry. Maintained under `luckyPipewrench/pipelock` — an active, independent open-source project purpose-built for AI agent security. Stars (704) and release cadence (v2.6.0, last push 2026-06-08) confirm active maintenance. No suspicious patterns identified. The tool is a proxy/firewall, not an install-and-forget scanner — deployment requires architecture planning (which MCP servers get wrapped). That is an operational consideration, not a security concern. Cleared for Walk-phase deployment subject to Soren's proxy architecture review at that time.

**Re-reviewed 2026-06-08 — verdict confirmed.** No new CVEs, no ownership changes, no license changes. Rose metrics (704 stars, v2.6.0, last push 2026-06-08) consistent with healthy active project.

---

## Soren's Operational Note

I do not install this in the current phase. Snyk Agent Scan is my Cat 3 primary and it covers what I need right now — scanning MCP configurations before anything goes into production. Pipelock becomes relevant when we have live agents running, when MCP servers are actively in use, and when I need a runtime firewall that can intercept and block in real time rather than just catching issues in a config scan. When that time comes, the setup is more involved than most tools in my stack — I need to plan the proxy architecture, understand which MCP servers get wrapped, and integrate it into each client's configuration. That is a Walk-phase conversation, not something I configure alone during initial stack setup. Flag for Sage when we hit that phase.

---

## Sage's COO Note

Pipelock's deployment is a team coordination event — it requires Soren to plan the proxy architecture in the context of whatever MCP servers are actively running at Walk phase. This is not a solo install; it is a session with Soren and potentially the Desktop-CoWork Agent to map the environment, configure the proxying, and verify it is not breaking anything before it goes live. Worth putting on the Phase 1 → Phase 2 transition checklist.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

## C&P Summary

Pipelock is Soren's standby runtime firewall for Category 3 — an open-source Go binary that sits inline as a proxy between agents and MCP servers, providing real-time bidirectional scanning for prompt injection, tool poisoning, SSRF, and DLP (48 patterns). It is the complement to Snyk Agent Scan: Agent Scan covers pre-deployment config review; Pipelock covers live runtime protection. Not needed in the current Crawl phase — it comes in when live agents and active MCP servers are running at Walk phase. Apache 2.0, fully free, no account required.
