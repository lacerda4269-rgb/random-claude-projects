# Resource Report: Claude Managed Agents (Official Anthropic Docs)

**URL:** https://platform.claude.com/docs/en/managed-agents/quickstart
**Date Researched:** 2026-04-12
**Researched by:** Rose | Security pre-check: Soren | Filed by: Lexi
**Already in Master Library?** No — new item

---

## What It Is
The official Anthropic documentation and quickstart guide for Claude Managed Agents — Anthropic's production API for running autonomous Claude agents inside sandboxed cloud containers. This is a Beta feature requiring the `managed-agents-2026-04-01` header. Not a GitHub repo — official Anthropic platform documentation.

## What It Does
Defines four core concepts: Agent (model + system prompt + tools + MCP servers + skills), Environment (configured cloud container with networking controls), Session (a running agent instance executing a specific task), and Events (real-time messages between your application and the agent). 

The API allows:
- Creating reusable, versioned agent configurations via API or CLI (`ant`)
- Spinning up containerized execution environments with configurable networking
- Starting sessions that run agents against specific tasks
- Streaming real-time events (tool use, messages, status) as the agent works
- Sending messages mid-session to steer the agent

Full SDK support: Python, TypeScript, Java, Go, C#, Ruby, PHP. Also includes an `ant` CLI for terminal management.

## Relevance to This Project
This is the reference source for Anthropic's official multi-agent architecture — directly relevant to the team's multi-agent coordination design decisions. Jay flagged it as a potential use for multiple agents. Key architectural insight: Managed Agents gives agents a real execution environment (bash, file ops, web search) rather than just prompting. This is the official pattern for what this project is building toward.

## Master Library Assessment
- **Proposed Section:** 7 — Reference & Ecosystem
- **Proposed Tier:** 1
- **Rationale:** Official Anthropic source material. Core reference for multi-agent architecture decisions. This is the canonical guide for running Claude agents in production containers. Tier 1 — core, critical reference.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** Source (official Anthropic platform documentation — platform.claude.com), API header (`managed-agents-2026-04-01` beta), no third-party dependencies, no code to install — documentation and API reference only
- **Notes:** This is official Anthropic documentation. No security review needed beyond confirming the source is legitimate — it is. The beta API header confirms this is an active, in-development Anthropic product.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Official Anthropic documentation; no versioned metrics to track; source URL confirmed live by Rose. No new risk factors. CLEARED stands.

## Recommendation
File to Section 7 — Reference & Ecosystem, Tier 1. This belongs near the top of the reference stack alongside the Anthropic Skills and Awesome Claude Code entries. No operator decisions required.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---
*Report by Rose + Sage | Session 39 | 2026-04-12*
*Updated by Rose | Session 230 | 2026-06-08*

---

## C&P Summary

The official Anthropic documentation and quickstart guide for Claude Managed Agents — a Beta API that runs autonomous Claude agents inside sandboxed cloud containers with real execution environments (bash, file ops, web search). The four core concepts are Agent (model + system prompt + tools), Environment (configured cloud container), Session (a running agent instance), and Events (real-time stream between your app and the agent). Full SDK support across Python, TypeScript, Java, Go, C#, Ruby, and PHP, plus an `ant` CLI. This is the canonical Anthropic reference for multi-agent architecture — directly relevant to how this team designs agent coordination and the patterns it builds toward in later phases.
