# Resource Report: OpenShell

**URL:** https://github.com/NVIDIA/OpenShell
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No

---

## What It Is
OpenShell is NVIDIA's open-source sandboxed runtime environment for autonomous AI agents — providing isolated execution spaces with policy-based access controls and four-layer protection.

## What It Does
OpenShell creates containerized sandbox environments where AI agents (including Claude Code, OpenCode, GitHub Copilot CLI, and Codex) operate with restricted filesystem, network, process, and inference access. Policies are defined in hot-reloadable YAML files. Credentials are injected without filesystem exposure. It includes a terminal UI dashboard (k9s-inspired), local GPU passthrough (experimental), Docker-based deployment with K3s Kubernetes support, and a community sandbox catalog. Built-in agent skills cover debugging, policy generation, and cluster management. Apache 2.0 license. 6,922 stars, 828 forks, 831 commits. Latest release: v0.0.57 (2026-06-05). Still Alpha — described as "proof-of-life" — but growth is significant and active development is confirmed.

## MCP Tool Manifest

- **Tool count:** OpenShell is an MCP-compatible agent runtime environment, not a traditional MCP tool server. It does not expose named tools to Claude directly. Instead, it provides a sandboxed execution container in which other MCP servers and tools run with policy-based access controls.
- **Tools:** N/A — OpenShell wraps and sandboxes other tools; it does not add Claude-callable tools of its own. Built-in agent skills (debugging, policy generation, cluster management) are invoked internally by the container environment.
- **Transport type:** Docker-based container runtime (not stdio or HTTP MCP transport); agents connect to OpenShell-managed containers via standard MCP from within the sandbox
- **settings.json registration:**

OpenShell is configured via Docker deployment + YAML policy files, not via a standard mcpServers block in settings.json. Basic deployment:
```bash
docker run -d --name openshell-sandbox \
  -v /path/to/policies:/etc/openshell/policies \
  nvcr.io/nvidia/openshell:latest
```
Policy files (YAML) define filesystem, network, process, and inference access rules for agents running inside the sandbox. Hot-reloadable without container restart.

- **Recommended serverInstructions:** "OpenShell is NVIDIA's agent sandboxing runtime. It does not expose MCP tools directly — it provides the secure execution environment in which other tools run. Configure via YAML policy files before deploying any agents into it."

## Relevance to This Project
Very relevant to the long-term architecture. As the agent team grows and agents start executing code autonomously — particularly Pete (Python Specialist) running trading scripts — having a sandboxed runtime that isolates agent actions from production infrastructure is a real need. The explicit Claude Code compatibility is a direct fit. The "credential injection without filesystem exposure" feature is directly applicable to the trading project's security requirements. That said, this is Alpha software with one developer — not production-ready today.

## Master Library Assessment
- **Proposed Section:** 1 — MCP Servers / Tools connecting Claude to external systems
- **Proposed Tier:** 2
- **Rationale:** Not technically an MCP server, but it is infrastructure that connects Claude Code agents to sandboxed execution environments — Section 1's "tools connecting Claude to external systems" framing applies. Tier 2 because it is phase-dependent: essential once agent code execution is in scope, not needed in the current documentation/planning phase.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** NVIDIA organization (verified major enterprise), Apache 2.0 license, 831 commits, 6,922 stars, 828 forks, Alpha status still in effect (v0.0.57), Docker/K3s-based architecture, credential injection mechanism documented transparently
- **Notes:** NVIDIA authorship is a strong legitimacy signal. Alpha status and single developer are not security concerns — they are maturity concerns. The sandbox architecture is itself a security tool; the design intent is protective, not harmful. Review the YAML policy schema carefully before deploying in a production environment.
- *Re-reviewed 2026-06-08 — verdict confirmed. Rose freshness sweep shows significant maturation (4k+ → 6,922 stars; 396 → 828 forks; 357 → 831 commits; v0.0.57 released 2026-06-05). Still Alpha but meaningfully more mature. NVIDIA organizational backing confirmed. Security posture unchanged.*

## Recommendation
Enter the library in Section 1 at Tier 2. Flag as the primary candidate for agent sandboxing when the build reaches autonomous code execution. Re-evaluate Alpha status at that time — by then it may have matured.

---
*Report by Sophia | Session 29 | 2026-03-28*

---

## C&P Summary

OpenShell is NVIDIA's open-source sandboxed runtime for autonomous AI agents — it creates containerized execution environments where agents operate with restricted filesystem, network, process, and inference access, all governed by hot-reloadable YAML policy files. Credentials are injected without filesystem exposure, which is directly applicable to this project's trading security requirements. For this team, it is the long-term answer to agent sandboxing: once agents like Pete (Python Specialist) begin running trading scripts autonomously, a sandboxed runtime that isolates their actions from production infrastructure becomes essential. Still Alpha (v0.0.57) but significantly more mature than at original report: 6,922 stars, 828 forks, 831 commits, actively releasing as of June 2026. Apache 2.0 license, NVIDIA organizational backing, cleared with no concerns. Section 1, Tier 2; security posture unchanged — Alpha label still applies.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
