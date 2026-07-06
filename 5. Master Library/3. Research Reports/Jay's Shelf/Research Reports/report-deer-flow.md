# Resource Report: DeerFlow

**URL:** https://github.com/bytedance/deer-flow
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No

---

## What It Is
DeerFlow is an open-source multi-agent orchestration harness built by ByteDance on LangGraph and LangChain, designed to run complex, multi-step tasks lasting minutes to hours.

## What It Does
DeerFlow orchestrates sub-agents with sandboxed execution environments (local, Docker, Kubernetes), long-term memory across sessions, extensible skills and tooling, and multi-channel integration (Telegram, Slack, Feishu/Lark). It supports OpenAI, Anthropic Claude, DeepSeek, and other providers. MCP server integration is built-in. Version 2.0 is a complete rewrite of the earlier "Deep Research" framework, now repositioned as a general-purpose agent orchestration platform. Ranked #1 on GitHub Trending as of February 28, 2026 with 51.1k stars. As of June 2026: 70,745 stars (up from 51.1k). No formal versioned releases — development is delivered directly via commits to the main branch. ByteDance authorship flag unchanged.

## Relevance to This Project
DeerFlow is a direct parallel to what this project is building — an orchestrated multi-agent system with persistent memory, skill extensibility, and multi-provider LLM support. It includes MCP integration and a clean dependency-mapping model for sequential vs. parallel task execution. The sandboxed execution approach (Docker/K8s) is worth studying for how it handles the security and isolation concerns that come up when agents run code. ByteDance authorship warrants awareness but not automatic rejection — the code is public and inspectable.

## Master Library Assessment
- **Proposed Section:** 3 — Agents & Autonomous Systems
- **Proposed Tier:** 2
- **Rationale:** This is one of the most complete open-source agent orchestration frameworks available right now. Tier 2 rather than Tier 1 because the project is building on Claude Code's native orchestration model rather than adopting an external framework — but DeerFlow is high-value as a design reference and possible future layer.

## Soren Security Pre-check
- **Verdict:** FLAG (unchanged)
- **Checked:** Repo age (active 2026), star count (70,745 as of June 2026; was 51.1k), fork count (6.1k at original check), MIT license, LangGraph/LangChain dependency chain, ByteDance authorship
- **Re-reviewed 2026-06-08 — verdict confirmed.** Star growth (51.1k→70,745) and confirmed absence of formal versioned releases (development via direct commits) noted. Active development does not change the ByteDance data posture or the PRC legal exposure. FLAG remains advisory, not blocking, for reference/study use. Full dependency audit remains required before any production deployment involving sensitive data.
- **Notes:** FLAG is advisory, not blocking. ByteDance is the author — a Chinese technology company subject to PRC data laws. The code is fully open-source and inspectable. For a self-hosted reference/study use case this is acceptable. For any production deployment handling sensitive trading data or personal credentials, the ByteDance origin warrants a full dependency audit before install. Flagging so the team is aware; not rejecting. No change to security posture from freshness sweep.

## Recommendation
Enter the library in Section 3 at Tier 2 with a Soren flag noted. Study the orchestration architecture and MCP integration pattern — both are directly applicable to the current build. Do not install without a dependency audit if sensitive data will be in scope.

---
*Report by Sophia | Session 29 | 2026-03-28*
*Freshness sweep: Rose | Session 229 | 2026-06-08 — stars updated (51.1k → 70,745); no formal versioned releases confirmed (development via direct commits); ByteDance flag and assessment unchanged.*

---

## C&P Summary

DeerFlow is an open-source multi-agent orchestration framework built by ByteDance on LangGraph, designed for complex multi-step tasks running minutes to hours. It includes sandboxed execution (local, Docker, Kubernetes), long-term cross-session memory, built-in MCP integration, and support for Claude, OpenAI, DeepSeek, and other providers. 70,745 stars as of June 2026 (up from 51.1k). No formal versioned releases — development is delivered via direct commits to the main branch. It is a direct parallel to what this project is building and is stored as a high-value design reference — particularly for its orchestration model, dependency mapping, and MCP integration patterns. A ByteDance authorship flag is noted: safe for reference use, but requires a dependency audit before any production deployment involving sensitive data.

---

## Report Version Log

| Version | Date | What Changed |
|---------|------|--------------|
