# Resource Report: GitHub MCP

**URL:** https://github.com/github/github-mcp-server
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
GitHub's official MCP server — connects AI tools directly to the GitHub platform for repository management, issue tracking, PR workflows, and code analysis via natural language.

## What It Does
- Read repositories and code files
- Manage issues and pull requests
- Analyze code and automate workflows
- Supports GitHub Enterprise Server and Enterprise Cloud
- Insiders Mode for early access to experimental features
- Multi-IDE integration (VS Code, Claude, Cursor, Windsurf, and others)
- Authentication via GitHub Personal Access Token

## MCP Tool Manifest

- **Tool count:** 26+ tools (organized into toolsets; default toolsets: context, issues, pull_requests, repos, users)
- **Tools:**
  - `get_file_contents` — Read a file from a GitHub repository
  - `create_or_update_file` — Create or update a single file with a commit message
  - `push_files` — Push multiple files in a single commit
  - `search_repositories` — Search GitHub repositories by name, description, or topic
  - `create_repository` — Create a new GitHub repository
  - `get_repository` — Get details about a repository
  - `list_branches` — List branches in a repository
  - `list_commits` — List commits in a repository with optional path filter
  - `create_branch` — Create a new branch
  - `search_code` — Search code across GitHub repositories
  - `search_issues` — Search GitHub issues and pull requests
  - `list_issues` — List issues in a repository
  - `get_issue` — Get details of a specific issue
  - `create_issue` — Create a new issue
  - `add_issue_comment` — Add a comment to an issue
  - `update_issue` — Update an existing issue
  - `list_pull_requests` — List pull requests in a repository
  - `get_pull_request` — Get details of a specific pull request
  - `create_pull_request` — Create a new pull request
  - `merge_pull_request` — Merge a pull request
  - `create_pull_request_review` — Submit a code review on a pull request
  - `list_workflow_runs` — List GitHub Actions workflow runs
  - `get_workflow_run` — Get details of a workflow run
  - `search_users` — Search GitHub users
  - `get_user` — Get details of a GitHub user
  - `get_code_scanning_alert` — Get a code scanning security alert
- **Transport type:** stdio
- **settings.json registration:**
```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "your_github_pat_here"
      }
    }
  }
}
```
- **Recommended serverInstructions:** "GitHub MCP provides access to the GitHub platform — read repositories, manage issues and pull requests, search code, list commits, and automate workflows. Authenticate with a scoped Personal Access Token."

## Builder Footprint

- **Integration type:** MCP Server (stdio, npx) — registered in `claude_desktop_config.json` or VS Code `settings.json`; requires GitHub Personal Access Token in `env` block; 26+ tools organized into toolsets (context, issues, pull_requests, repos, users)
- **Extension points:** Toolsets are selectable — enable only the toolsets relevant to the current project phase to limit tool scope; Insiders Mode available for early access features; GitHub Enterprise Server and Enterprise Cloud supported; scoped PAT permissions configurable at token creation
- **Build complexity signal:** Low — npx auto-install; one GitHub PAT required (create at github.com → Settings → Developer settings → Personal access tokens); scope PAT to minimum required permissions; token stored in settings.json env block
- **Known conflicts:** GitHub MCP and GitHub CLI (`gh`) can coexist — MCP for Claude-native interactive operations, CLI for terminal/scripted operations. PAT must not be hardcoded anywhere except the designated `settings.json` env block — use environment variable injection if settings.json is ever committed to a repo.

## Relevance to This Project
Version control for every strategy and parameter iteration. Commit messages can include stop/target distances, win rate, profit factor. Branching for aggressive strategy variations without touching stable code. Full audit trail of what changed and when. Equally useful for any non-trading codebase.

## Master Library Assessment
- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 1
- **Rationale:** Foundation-level. Version control is non-negotiable for any serious build. Official GitHub source, 30.5k stars.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** 30,514 stars (was 28.4k at original review), official GitHub organization repo, PAT-based authentication (scoped permissions), MIT license. No malicious patterns detected.
- **Notes:** Authentication requires a GitHub Personal Access Token — scope it to minimum required permissions at setup. Enterprise features available if needed at scale. Latest release v1.2.0; last push 2026-06-08 (active today).
- **Re-reviewed 2026-06-08 — verdict confirmed.** Stars now 30,514 (was 29.8k); last push 2026-06-08 (active today); latest release v1.2.0 (continued feature development past v1.0 GA milestone). Official GitHub org repo — provenance is as solid as it gets. No new CVEs or security disclosures. CLEARED status stands with no conditions.

## Recommendation
Add to Section 4, Tier 1. Phase 1 install alongside Desktop Commander MCP.

---
*Report by Sophia | Session 31 | 2026-03-29*

---

## C&P Summary

GitHub MCP is GitHub's official MCP server, connecting AI tools directly to the GitHub platform for repository management, issue tracking, PR workflows, and code analysis via natural language. It supports GitHub.com, GitHub Enterprise Server, and Enterprise Cloud, with multi-IDE integration including VS Code, Claude, Cursor, and Windsurf. For this project, it is foundation-level infrastructure: version control for every strategy and parameter iteration, with commit messages that can include stop/target distances, win rate, and profit factor. Phase 1 install alongside Desktop Commander MCP. Official GitHub source, 28k+ stars, MIT license, cleared with no concerns.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
