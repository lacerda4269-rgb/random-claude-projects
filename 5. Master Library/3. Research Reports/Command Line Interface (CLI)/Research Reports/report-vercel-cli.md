# Resource Report: Vercel CLI

**URL:** https://vercel.com/docs/cli
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No

---

## What It Is
Vercel CLI is the official command-line interface for the Vercel deployment and hosting platform, enabling full project management and deployment operations from the terminal.

## What It Does
Covers the complete Vercel project lifecycle from the command line: deploying projects (including production deploys), running local dev environments that replicate Vercel's production environment, managing environment variables, handling DNS and custom domains, managing certificates, pulling remote project settings locally, rolling back deployments, managing Blob storage, managing feature flags, and setting up MCP client configuration for Vercel projects. Notably includes a `vercel mcp` command for MCP integration. Requires npm/yarn/pnpm/bun to install.

## Relevance to This Project
This project does not currently use Vercel for hosting or deployment. Vercel is a web app deployment platform — it is relevant if a future project involves building and deploying a web application or API. The current project is a framework build for AI agent orchestration, with no web deployment surface today. The operator note on this batch flags "only looking for free or what we can create" — Vercel has a free tier but is a commercial platform.

## Master Library Assessment
- **Proposed Section:** 5 — Reference & Ecosystem
- **Proposed Tier:** 3
- **Rationale:** Standard developer CLI for a specific deployment platform. No active use case in this project. Section 5 is the right home — worth knowing exists if Vercel ever enters the stack. Tier 3 because there is no current or near-term application.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** Organizational standing (Vercel Inc., major commercial hosting platform), official documentation domain (vercel.com), actively maintained product with comprehensive command reference, no suspicious patterns.
- **Notes:** Major commercial platform. The docs page is legitimate and well-structured. No concerns. **June 2026 metrics:** 15,627 stars, 3,617 forks, v54.9.1 latest release, last push 2026-06-08. Actively maintained.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Stars (15,627), forks (3,617), v54.9.1, last push 2026-06-08. No new CVEs, no ownership changes, no license changes. Clearance holds. Reference-only status unchanged — no active use case in this project.

## Recommendation
Enter the Master Library at Section 5 (Reference & Ecosystem), Tier 3, as a reference item. No action needed now. Revisit if web deployment enters any future project scope.

---
*Report by Sophia | Session 29 | 2026-03-28*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

## C&P Summary

Vercel CLI is the official command-line interface for the Vercel web deployment platform — it covers the full project lifecycle from local dev to production deployment, including environment variable management, DNS, certificates, rollbacks, Blob storage, and feature flags. It also includes a `vercel mcp` command for MCP integration. No current use case in this project, which has no web deployment surface today. Relevant if any future project involves building and deploying a web application or API. Filed as reference in Section 5.
