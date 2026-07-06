# Resource Report: Google Workspace CLI

**URL:** https://github.com/googleworkspace/cli
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No

---

## What It Is
Google Workspace CLI (`gws`) is a unified command-line tool providing access to all Google Workspace APIs — Drive, Gmail, Calendar, Sheets, Docs, Chat, Admin, and others — through a single interface.

## What It Does
Dynamically generates its full command surface at runtime from Google's Discovery Service, meaning it automatically picks up new API endpoints as they are released. Returns structured JSON output suitable for automation and scripting. Includes 40+ built-in AI agent skills and integrates with Gemini CLI. Supports multiple authentication methods (OAuth, service accounts, access tokens, encrypted credential storage). Includes pre-built helper commands for common workflows — send email, create calendar events, upload files. Also includes Model Armor integration for response sanitization. Available via npm, cargo, Homebrew, and Nix.

## Relevance to This Project
No current use case in this project. The trading system and agent framework being built here do not depend on Google Workspace integration today. However, this is a genuinely powerful automation tool — the dynamic API generation approach means one CLI covers the entire Google Workspace surface, and the built-in AI agent skills make it agent-ready out of the box. Worth keeping on the radar for future projects involving Google Workspace automation (reporting, data management, team communication flows).

## Master Library Assessment
- **Proposed Section:** 5 — Reference & Ecosystem
- **Proposed Tier:** 3
- **Rationale:** A standard (if unusually capable) developer CLI for a specific platform. No active use case in this project. Section 5 is the right home. Tier 3 because it is not urgent and has no current application — but the agent-skill integration makes it more interesting than a typical CLI reference entry.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** Organizational standing (googleworkspace/ official GitHub org, Google-backed project), star count (22.9k — notably high for a workspace CLI), active maintenance (272 commits, multiple auth methods, active PR queue), no suspicious patterns.
- **Notes:** Stars: 26,919 (was 22.9k — significant growth). Official Google organizational home. No concerns. Note: project documentation flags breaking changes expected before v1.0. Latest release: v0.22.5 (March 31, 2026).
- **Re-reviewed 2026-06-08 — verdict confirmed. CLEARED stands.** Rose's freshness sweep: v0.22.5 (March 31, 2026), stars 26,919, last push 2026-06-01 — actively maintained by Google. No security disclosures. Pre-v1.0 breaking-change caveat still applies but is not a security concern. No action required.

## Recommendation
Enter the Master Library at Section 5 (Reference & Ecosystem), Tier 3, as a reference item. The agent-ready feature set (40+ built-in skills, Gemini CLI integration) makes this worth revisiting if any future project involves Google Workspace automation. Caveat: pre-v1.0, breaking changes expected.

---
*Report by Sophia | Session 29 | 2026-03-28*

---

## C&P Summary

Google Workspace CLI (`gws`) is an official Google-backed command-line tool that exposes the entire Google Workspace API surface — Drive, Gmail, Calendar, Sheets, Docs, Chat, and more — through a single interface. It dynamically generates its command structure at runtime from Google's Discovery Service, so it automatically picks up new API endpoints as they are released. It includes 40+ built-in AI agent skills and Gemini CLI integration, making it agent-ready out of the box. No current use case exists in this project, but it is worth keeping on the radar for any future work involving Google Workspace automation. Note: pre-v1.0, breaking changes expected. Stars: 26,919 (strong growth from 22.9k at research).

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
