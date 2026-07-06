# Resource Report: n8n-mcp

**URL:** https://github.com/czlonkowski/n8n-mcp
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** Likely Yes — flagged as a possible match for the "N8N MCP" entry in Section 1. See ML Assessment below.

---

## What It Is
An MCP server by czlonkowski that gives AI assistants (including Claude) comprehensive access to n8n's full node library — covering documentation, properties, operations, and workflow templates.

## What It Does
The server exposes 1,396 n8n nodes (812 core + 584 community) with 99% property coverage and 87% documentation coverage. It provides 265 AI-capable tool variants with full documentation, 2,646 pre-extracted configurations from popular templates, and 2,709 workflow templates with complete metadata. Deployment options include a hosted service at `dashboard.n8n-mcp.com`, Docker, local `npx` install, or cloud deployment via Railway. MIT license. 21,613 stars, 3,493 forks, 1,023 commits. Latest release: v2.57.1 (2026-06-03).

## MCP Tool Manifest

- **Tool count:** ~20 tools across two categories: node documentation tools and n8n instance management tools
- **Tools:**
  - `search_nodes` — Full-text search across all n8n node documentation and descriptions
  - `list_nodes` — List all 1,396 n8n nodes with optional filtering by type or category
  - `get_node_info` — Get comprehensive documentation for a specific node including all properties and operations
  - `get_node_essentials` — Get only essential properties with examples (10–20 properties vs. 200+); token-efficient alternative to get_node_info
  - `search_node_properties` — Find specific properties within a node's configuration
  - `tools_documentation` — Get documentation for any available MCP tool
  - `n8n_create_workflow` — Create a new workflow in a connected n8n instance
  - `n8n_get_workflow` — Retrieve an existing workflow by ID
  - `n8n_update_full_workflow` — Replace an entire workflow definition
  - `n8n_update_partial_workflow` — Patch specific nodes or connections in a workflow
  - `n8n_delete_workflow` — Delete a workflow from the n8n instance
  - `n8n_list_workflows` — List all workflows in the n8n instance
  - `n8n_validate_workflow` — Check a workflow definition for structural errors
  - `n8n_autofix_workflow` — Automatically fix common workflow configuration issues
  - `n8n_manage_credentials` — Manage n8n credential configurations
  - `n8n_run_webhook` — Trigger a webhook-activated workflow
  - `n8n_get_templates` — Access the 2,709 pre-extracted workflow templates
  - `n8n_search_templates` — Search workflow templates by keyword or use case
- **Transport type:** stdio (local npx or Docker) or HTTP (hosted service at dashboard.n8n-mcp.com)
- **settings.json registration:**
```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "npx",
      "args": ["-y", "n8n-mcp"],
      "env": {
        "N8N_API_URL": "http://your-n8n-instance:5678/api/v1",
        "N8N_API_KEY": "your_n8n_api_key"
      }
    }
  }
}
```
Note: Node documentation tools (search_nodes, get_node_info, etc.) work without n8n API credentials. Instance management tools (n8n_create_workflow, etc.) require N8N_API_URL and N8N_API_KEY.
- **Recommended serverInstructions:** "n8n-mcp provides access to n8n's full node library (1,396 nodes) and workflow management. Use search_nodes and get_node_essentials for documentation. Use n8n_* tools to create, edit, and manage workflows in a live n8n instance. Validate workflows before deploying to production."

## Relevance to This Project
n8n is a workflow automation platform. This MCP server would allow Claude to read, understand, and help build n8n workflows — relevant if n8n ever becomes part of the project's automation layer. For the current phase (building the agent framework and trading system), n8n is not in scope. But if Jay decides to use n8n for connecting external services (data feeds, notifications, integrations), this MCP becomes the bridge between Claude and that automation layer.

## Master Library Assessment
- **Proposed Section:** 1 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** This is a purpose-built MCP server — definitively Section 1. Tier 2 because n8n is not in the current build scope, but this would become immediately relevant if n8n enters the stack.

## Master Library Entry Status — N8N MCP Check
**Assessment: This IS the repo behind the "N8N MCP" entry in the ML, or the most likely candidate.**
- The entry describes an MCP server for n8n workflow automation.
- This repo (`czlonkowski/n8n-mcp`) is by far the most prominent, most complete, and most actively maintained MCP server for n8n — 16.8k stars, 937 commits, dedicated hosted service.
- No other n8n MCP server of comparable maturity was identified in research.
- **Recommendation for the ML entry:** Confirm `czlonkowski/n8n-mcp` as the source repo and update the entry URL accordingly. Section 1, Tier 2 placement is appropriate.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** Repo age (active 2026), star count (21,613), fork count (3,493), 1,023 commits, MIT license, author czlonkowski (individual developer — active, public GitHub profile), hosted service at `dashboard.n8n-mcp.com`, multiple deployment options documented
- **Notes:** README explicitly warns against editing production n8n workflows directly with AI — advising test/dev workflow copies first. This is a responsible security disclosure, not a red flag. MIT license, no copyleft concerns. Hosted service option means optional external data transmission — users who want full local control should use the Docker or `npx` install path. No malicious patterns detected.
- *Re-reviewed 2026-06-08 — verdict confirmed. Rose freshness sweep shows substantial growth (16.8k → 21,613 stars; 2.8k → 3,493 forks; 937 → 1,023 commits; v2.57.1 released 2026-06-03). Strong active development. Security posture unchanged.*

## Recommendation
Confirm this as the source repo for the existing ML "N8N MCP" entry and update the entry's URL. Section 1, Tier 2 placement confirmed. Note the hosted vs. local deployment distinction for any future install decision.

---
*Report by Sophia | Session 29 | 2026-03-28*

---

## C&P Summary

n8n-mcp is the leading community MCP server for n8n, a workflow automation platform. It gives Claude comprehensive access to n8n's full node library — 1,396 nodes (812 core + 584 community) with 99% property coverage, 265 AI-capable tool variants, and 2,709 workflow templates with full metadata. In practical terms, it means Claude can read, understand, and help build n8n automation workflows from within a session. For this project, n8n is not currently in scope, but this MCP becomes immediately relevant if n8n is ever adopted for connecting external services — data feeds, notifications, and integrations. MIT license, 21,613 stars, 3,493 forks, v2.57.1 (June 2026), cleared with no concerns. Section 1, Tier 2.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
