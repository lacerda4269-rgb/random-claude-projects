# Resource Report: claude-mcp-sentinel

**URL:** https://github.com/soy-rafa/claude-mcp-sentinel
**Date Researched:** 2026-05-03
**Researched by:** Rose | Security pre-check: Soren (direct code review) | Filed by: Lexi
**Already in Master Library?** No — queued since Session 104; first full review this session

---

## What It Is
claude-mcp-sentinel is a security monitoring tool for Claude Code's MCP system. It functions as a runtime watchdog that monitors MCP server activity, logs tool calls, and can block or flag suspicious operations before they execute. Built by soy-rafa. Zero external dependencies — pure local operation. Designed specifically for the Claude Code ecosystem.

## What It Does
Intercepts and monitors MCP tool calls in real time during Claude Code sessions. Maintains a running activity log of all MCP operations. Supports configurable block rules — operators define what classes of tool calls require approval or should be denied. Fails-open by design: if the sentinel process goes down, MCP operations continue unimpeded (the sentinel is a guard layer, not a required gate for operations to proceed).

## Relevance to This Project
High relevance to Soren's operational stack. Currently, Soren's primary security role is pre-deployment — reviewing resources before they are cleared for the library. claude-mcp-sentinel adds a runtime monitoring layer: a standing check running after a resource is deployed. Soren would use this to implement tighter runtime control over MCP operations in live sessions. Also a strong candidate for the security hardening pass during Agent Onboarding.

## Master Library Assessment
- **Proposed Section:** 3 — Command Line Interface (CLI), Section 3a (Security Tools)
- **Proposed Tier:** 1
- **Rationale:** Tier 1 — directly relevant to the team's operational security posture; Soren is the primary user; zero external dependencies; code audited directly. The fails-open design is a documented and intentional limitation, not a disqualifier.

## Soren Security Pre-check
- **Verdict:** CLEARED WITH CONDITIONS
- **Special protocol applied:** Direct code review substituted for AV scan — this is the trust bootstrapping rule. A security tool designed to monitor other tools cannot verify itself via an automated scan. Soren executed a manual code review instead, which satisfies the security requirement for this tool type.
- **Checked:** Full direct code review (purpose, logic, data handling, output scope); dependency profile (zero external dependencies confirmed); fail behavior analysis (fails-open — documented in code; intended by design)
- **Conditions:**
  1. Fails-open by design — if sentinel goes down, MCP operations proceed without interception. This is documented and intentional; not a flaw. Account for this in deployment design (monitor sentinel availability; do not rely on it as a hard gate).
  2. Single-developer project — bus factor of 1. If the repository goes dormant, there is no community maintenance path. Monitor repository health periodically.
  3. AV not available in Agent context — direct code review substituted and completed; this satisfies the security requirement.
- **Notes:** Code does exactly what it claims. Clean clearance with the noted caveats.
- **Re-reviewed 2026-06-08 — verdict confirmed. CLEARED WITH CONDITIONS stands.** Rose's freshness sweep: stars 164 (was 145), forks 22, last push 2026-04-18 — activity has slowed since v2.0 release (April 17, 2026). No new CVEs or security disclosures. All three original conditions remain active. The v2.0 architectural change (daemon → PreToolUse hook mechanism) noted in v1.1 version log is still an open item — Soren must re-review v2.0 code before deployment. That re-review has not yet occurred; treat as a prerequisite to deployment, not a re-clearance blocker for the library entry itself.

## Builder Footprint

- **Integration type:** Python CLI / runtime daemon — zero external dependencies; local operation only; intercepts MCP tool calls during Claude Code sessions; block rules configured in local config file
- **Extension points:** Configurable block rules allow Soren to define what classes of MCP tool calls require approval or should be denied; activity log format is inspectable; fails-open design means the sentinel can be started/stopped without disrupting active MCP sessions (Inferred from documentation — not explicitly documented)
- **Build complexity signal:** Low — Python install; zero external dependencies; single-developer project with clean code (confirmed via direct Soren code review); config file for block rules is the only setup step beyond install
- **Known conflicts:** Fails-open by design — if sentinel process dies, MCP operations continue without monitoring (documented intentional behavior; not a flaw); do not rely on it as a hard gate in any deployment. Single-developer bus factor — monitor repository health; no community maintenance path if dormant. AV scan not available in Agent context — trust bootstrapping rule already applied.

## Recommendation
File to Section 3 (CLI), Section 3a (Security Tools), Tier 1. Primary user: Soren. Target deployment: Agent Onboarding security hardening phase. Monitor sentinel availability in any deployment; do not rely on it as a mandatory gate.

---
*Report by Rose + Soren (direct code review) + Sage | Session 106 | 2026-05-03*

---

## C&P Summary

claude-mcp-sentinel is a runtime security monitoring tool for Claude Code's MCP system — a local watchdog that intercepts MCP tool calls, maintains an activity log, and can block suspicious operations before they execute. Built by soy-rafa; zero external dependencies; MIT-class license. Soren cleared it via direct code review (trust bootstrapping rule: a security tool cannot verify itself via automated scan; manual review substituted). CLEARED WITH CONDITIONS: fails-open by design (sentinel down = MCP ops continue — documented, intentional design choice); single-developer bus factor; AV not available in Agent context. Tier 1 — directly relevant to Soren's runtime security posture and the team's MCP hardening. Filed to Section 3a (CLI Security Tools). Target deployment: Agent Onboarding. Monitor sentinel availability; do not rely on it as a hard gate.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
