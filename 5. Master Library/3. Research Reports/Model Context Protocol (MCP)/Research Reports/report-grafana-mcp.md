# Resource Report: Grafana MCP

**URL:** https://github.com/grafana/mcp-grafana
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
Official Grafana MCP server — bridges Grafana instances and AI systems, providing intelligent access to monitoring data, dashboards, alerting systems, and related services.

## What It Does
- Dashboard management: search, retrieve, modify, and extract data
- Data querying across Prometheus, Loki, ClickHouse, CloudWatch, Elasticsearch
- Alerting: rules, notifications, routing
- On-call management (Grafana OnCall integration)
- Incident tracking (Grafana Incident support)
- Administrative functions: user, team, and role management
- Read-only mode available for safe monitoring
- Requires Grafana 9.0+

## MCP Tool Manifest

- **Tool count:** 50+ tools (configurable; categories can be enabled/disabled via --enable-<category> / --disable-<category> flags)
- **Tools (representative by category):**
  - `search_dashboards` — Search for Grafana dashboards by keyword or tag
  - `get_dashboard` — Retrieve a dashboard by UID including panels and queries
  - `update_dashboard` — Create or update a dashboard with new panel/query configuration
  - `get_panel_queries` — Extract datasource queries from a specific panel
  - `test_connection` — Verify connectivity to Grafana instance
  - `query_prometheus` — Execute a PromQL query against Prometheus datasource
  - `query_loki` — Query Grafana Loki for log data with LogQL
  - `query_datasource` — Query any connected datasource (ClickHouse, CloudWatch, Elasticsearch, etc.)
  - `list_alert_rules` — List all Grafana alert rules
  - `get_alert_rule` — Get details of a specific alert rule
  - `list_oncall_schedules` — List Grafana OnCall on-call schedules
  - `get_incident` — Get details of a Grafana Incident
  - `list_incidents` — List active and resolved incidents
  - `list_users` — List Grafana users
  - `list_teams` — List Grafana teams and memberships
  - *(additional tools for folders, annotations, data source management, and admin functions)*
- **Transport type:** stdio
- **settings.json registration:**
```json
{
  "mcpServers": {
    "grafana": {
      "command": "docker",
      "args": [
        "run", "-i", "--rm",
        "-e", "GRAFANA_URL",
        "-e", "GRAFANA_SERVICE_ACCOUNT_TOKEN",
        "mcp/grafana"
      ],
      "env": {
        "GRAFANA_URL": "http://your-grafana-instance:3000",
        "GRAFANA_SERVICE_ACCOUNT_TOKEN": "your_service_account_token"
      }
    }
  }
}
```
- **Recommended serverInstructions:** "Grafana MCP connects to a Grafana instance for dashboard management, metric and log querying across datasources, alerting, on-call management, and incident tracking. Requires GRAFANA_URL and a Service Account Token. Use read-only mode at initial setup."

## Relevance to This Project
Live monitoring layer. Feed Python trade logs and performance metrics into visual dashboards. Query dashboards conversationally: "which strategy had the highest drawdown this week?" Phase 3 — only needed once live trading and multi-strategy monitoring begins.

## Master Library Assessment
- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** Phase 3 per the original stack plan. High value for monitoring at scale. Official Grafana source, 3,111 stars.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** 3,111 stars, 377 forks, 634 commits, official Grafana organization repo, open-source license confirmed. Latest release: v0.15.2 (2026-06-04). No malicious patterns detected.
- **Notes:** Read-only mode is available — use it first when setting up dashboards. Full write access only when dashboard management is needed.
- *Re-reviewed 2026-06-08 — verdict confirmed. Rose freshness sweep shows continued active development (stars 2,700+ → 3,111; forks 310 → 377; commits 509 → 634; v0.15.2 released 2026-06-04). Official Grafana organization. Security posture unchanged.*

## Recommendation
Add to Section 4, Tier 2. Phase 3 install. Use read-only mode at setup.

---
*Report by Sophia | Session 31 | 2026-03-29*

---

## C&P Summary

Grafana MCP is the official Grafana MCP server that bridges Grafana monitoring instances to AI systems, providing natural language access to dashboards, alerting rules, on-call management, incident tracking, and data queries across sources like Prometheus, Loki, ClickHouse, and CloudWatch. For this project, it is the live monitoring layer: once live trading and multi-strategy tracking begins, trade logs and performance metrics feed into Grafana dashboards that agents can query conversationally. Phase 3 — not needed until live trading monitoring is in scope. Official Grafana source, 3,111 stars, 377 forks, v0.15.2 (June 2026), cleared with no concerns. Use read-only mode at setup.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
