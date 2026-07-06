# Resource Report: HF Hub MCP Server (Hugging Face)

**URL:** https://github.com/huggingface/hf-mcp-server
**Date Researched:** 2026-05-02
**Researched by:** Rose | Security pre-check: Soren | Report by: Rose
**Already in Master Library?** Yes — Section 4 (MCP Servers), Tier 2. Full Database entry references Round 3 consolidated report. This individual file is a retrofit — content extracted from Rose-Research-Report-Round-3.md.

---

## C&P Summary

The Hugging Face Hub MCP Server is an official plug-in from Hugging Face that connects Claude directly to the world's largest library of open-source AI models, research papers, and AI apps. Once connected, Claude can search for the right model for a task, browse current documentation, find research papers by topic, and even run compute jobs on Hugging Face's infrastructure — all without leaving the current session. The most relevant uses for this team are Pete finding and working with pre-trained models, and Rose using the paper search and documentation tools as additional research infrastructure. Seven independently toggleable tools; the job submission tool incurs compute costs and must only be triggered with explicit user authorization. 247 stars, 68 forks on this specific repo but built and maintained by Hugging Face itself. Latest release: v0.3.19 (2026-06-04). MIT license.

---

## What It Is

The official Hugging Face MCP server, maintained by Hugging Face. Connects Claude to the Hugging Face Hub — the world's largest repository of open-source AI models, datasets, and AI application "Spaces." Seven built-in tools, each independently togglable, covering model discovery, dataset search, paper retrieval, documentation lookup, and compute job management.

---

## What It Does

- **Spaces Semantic Search** — find AI apps via natural language
- **Papers Semantic Search** — find ML research papers via natural language
- **Model Search** — search models by task, library, and other filters
- **Dataset Search** — search datasets by author, tags, etc.
- **Documentation Semantic Search** — search Hugging Face docs by natural language
- **Run and Manage Jobs** — run, monitor, and schedule compute jobs on HF infrastructure (write/execute capability — see Soren notes)
- **Hub Repository Details** — get detailed info about any model, dataset, or Space

---

## MCP Tool Manifest

- **Tool count:** 7 tools (each independently togglable)
- **Transport type:** stdio (confirmed)
- **settings.json registration:**
```json
{
  "mcpServers": {
    "hf-mcp-server": {
      "command": "npx",
      "args": ["-y", "@huggingface/mcp-server"],
      "env": {
        "HF_TOKEN": "your_huggingface_token"
      }
    }
  }
}
```

---

## Builder Footprint

- **Integration type:** MCP tool layer
- **Build complexity signal:** Simple (~1–2 hours) — npx install with HF token environment variable; tools are individually toggleable in config
- **Known conflicts:** None. Complements Rose's research stack as ML-specific search infrastructure.

---

## Master Library Assessment

- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** MIT, official HF organization, actively maintained. Tier 2 because it is highly relevant for ML-adjacent work but not core to current project phase. Tier 1 candidate when Pete's Python work begins in earnest.

---

## Soren Security Pre-check

- **Verdict:** CLEARED WITH CONDITIONS
- **Notes:**
  - (1) DEFAULT_HF_TOKEN: local/dev/test only, never production/shared — acts as silent write-auth bypass if set in environment.
  - (2) Write-scoped HF token required for job/repo operations; read-only tokens fail silently on write — confirm token scope before deployment.
  - (3) `run_and_manage_jobs` tool submits compute jobs to HF infrastructure — incurs cost on external infrastructure. Must be gated behind explicit user authorization before invoking in any agent context.

*Source: Soren Security Review — Round 3 HOLD follow-up, Session 104. Clearance confirmed in Full Database with conditions.*
*Re-reviewed 2026-06-08 — CLEARED WITH CONDITIONS verdict confirmed. Rose freshness sweep shows active development (stars 224 → 247; forks confirmed 68; v0.3.19 released 2026-06-04). Official Hugging Face organization. All three conditions unchanged and still in force.*

---

*Report by Rose — Research Specialist | 2026-05-02 (Retrofit to individual file — Session 201)*
*Prompt Injection Check: Not applicable — content extracted from internal Round 3 consolidated report.*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
