# Resource Report: GitHub CLI

**URL:** https://cli.github.com/ | https://github.com/cli/cli
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No

---

## What It Is
GitHub CLI (`gh`) is GitHub's official command-line tool that brings pull requests, issues, and all core GitHub concepts into the terminal.

## What It Does
Provides terminal-based access to GitHub operations including creating and reviewing pull requests, managing issues, handling releases, running GitHub Actions workflows, and making authenticated API calls to GitHub — all without leaving the command line. Works across macOS, Windows, and Linux, and supports GitHub.com, GitHub Enterprise Cloud, and GitHub Enterprise Server 2.20+. Built in Go and maintained directly by GitHub.

## Relevance to This Project
This project uses GitHub as its version control and collaboration backbone. GitHub CLI is already in active use — Sage and the team issue `gh` commands for commits, PR creation, branch management, and repo operations throughout every session. This is infrastructure, not a candidate for installation consideration. It is already installed and operational.

## Builder Footprint

- **Integration type:** CLI (Go binary) — already installed and active; `gh` command available in all terminal sessions; authenticates via `gh auth login` using OAuth or personal access token
- **Extension points:** GitHub CLI extensions (`gh extension install`) allow custom commands; Cosmo can write skill files wrapping common `gh` command sequences (e.g., PR creation templates, release workflows, issue triage patterns); `gh api` enables arbitrary GitHub REST/GraphQL API calls (Inferred from documentation — not explicitly documented; `gh extension install` and `gh api` are documented features; Cosmo-specific skill file wrapping is inferred)
- **Build complexity signal:** None for current project — already deployed and operational; for new projects, install via `winget install GitHub.CLI` or `brew install gh` plus a one-time `gh auth login`
- **Known conflicts:** None. GitHub CLI and GitHub MCP (Section 4, Tier 1) can coexist — CLI for terminal/scripted operations, MCP for Claude-native interactive operations. No version conflicts with any other tool in the stack.

## Master Library Assessment
- **Proposed Section:** 5 — Reference & Ecosystem
- **Proposed Tier:** 1
- **Rationale:** Core infrastructure used in every session. Not a tool to evaluate or install — it is already part of the standard operating environment. Section 5 is the right home: it is reference material that documents what the team uses, not something to be built or deployed. Tier 1 because it is foundational to all project operations.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** Organizational standing (GitHub/Microsoft), official repository, star count (43.4k), active maintenance (v2.89.0 released March 26, 2026, 601 contributors, 11,043 commits, 193 releases), no suspicious patterns.
- **Notes:** This is a first-party tool from GitHub itself. No concerns of any kind. Stars: 44,762. Latest version: v2.93.0 (May 27, 2026).
- **Re-reviewed 2026-06-08 — verdict confirmed. CLEARED stands.** Rose's freshness sweep: v2.93.0 (May 27, 2026), stars 44,762, last push 2026-06-08 — actively maintained by GitHub/Microsoft. No security disclosures. Core infrastructure in active daily use. No action required.

## Recommendation
Enter the Master Library at Section 5 (Reference & Ecosystem), Tier 1, as a reference item documenting current active infrastructure. No installation action needed — already in use.

---
*Report by Sophia | Session 29 | 2026-03-28*

---

## C&P Summary

GitHub CLI (`gh`) is GitHub's official command-line tool that brings the full GitHub platform — pull requests, issues, releases, Actions workflows, and API calls — into the terminal. It is already installed and in active use by this team; every session uses `gh` commands for commits, PR creation, and repo management. This is core infrastructure, not a candidate for evaluation. It is built and maintained directly by GitHub (Microsoft), carries 44.7k+ stars, and has zero concerns of any kind.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
