# Resource Report: Firecrawl MCP Server

**URL:** https://github.com/firecrawl/firecrawl-mcp-server
**Note:** Repo previously at `github.com/mendableai/firecrawl-mcp-server` — transferred to the `firecrawl` org. Both URLs resolve to the same repo (GitHub redirect active as of 2026-06-08).
**Date Researched:** 2026-05-02
**Researched by:** Rose | Security pre-check: Soren | Report by: Rose
**Already in Master Library?** Yes — Section 4 (MCP Servers), Tier 2. Full Database entry references Round 3 consolidated report. This individual file is a retrofit — content extracted from Rose-Research-Report-Round-3.md.

---

## C&P Summary

Firecrawl MCP is the official plug-in from the Firecrawl team that gives Claude the ability to scrape websites, run web searches that return full page content (not just links), and conduct autonomous web research. You give it a URL or a research goal and it handles the crawling, extraction, and structuring of the results. It is the most capable web data tool in the current Master Library — especially useful for Rose when research tasks require pulling live web content at scale. Requires a Firecrawl API key; the free tier is 500 lifetime credits (enough for testing), with paid plans starting at $16/month for regular use. MIT license, actively maintained, 6.2k stars.

---

## What It Is

The official Firecrawl MCP server — adds powerful web scraping, full-content web search, and autonomous browser automation to Claude and other LLM clients. Firecrawl is a commercial web scraping platform with an AI-optimized API; this MCP server is the bridge that connects it to Claude Code. Requires a Firecrawl API key (free tier available).

---

## What It Does

- **Web search with full page content** — not just search results, but the actual page content
- **URL scraping** — extract structured JSON or markdown from any URL
- **Batch processing** — scrape multiple URLs in parallel
- **Site mapping** — discover and map all indexed pages on a domain
- **Autonomous web research via AI agent** — give it a research goal, it figures out what to crawl
- **Interactive browser sessions** — click, fill forms, navigate (cloud browser)
- **Automatic retry logic and rate limiting**
- **Cloud or self-hosted deployment**

**Pricing/API key:** Requires a Firecrawl API key. Free tier: 500 lifetime credits (not per month — lifetime). No credit card required to start. Paid plans start at $16/month (3,000 credits/month).

---

## MCP Tool Manifest

- **Tool count:** 12 tools
- **Tools:**
  - `firecrawl_scrape` — Scrape a single URL and return structured JSON or clean markdown
  - `firecrawl_batch_scrape` — Submit multiple URLs for parallel batch scraping; returns a job ID
  - `firecrawl_check_batch_status` — Poll the status of a batch scrape job and retrieve completed results
  - `firecrawl_search` — Web search that returns full page content (not just links/snippets)
  - `firecrawl_crawl` — Crawl an entire website starting from a root URL; discovers and scrapes all pages
  - `firecrawl_extract` — Extract structured data from a URL using a custom schema
  - `firecrawl_deep_research` — Autonomous web research agent: given a goal, it figures out what to crawl and returns synthesized findings
  - `firecrawl_generate_llmstxt` — Generate LLMs.txt file (documentation manifest) for a website
  - `firecrawl_map` — Map all indexed URLs on a domain (site structure discovery)
  - `firecrawl_agent` — Submit a complex web automation task to an autonomous browser agent; returns job ID immediately
  - `firecrawl_agent_status` — Poll the status of a firecrawl_agent job
  - `firecrawl_interact` — Click buttons, fill forms, and navigate in a live cloud browser session
- **Transport type:** stdio
- **settings.json registration:**
```json
{
  "mcpServers": {
    "mcp-server-firecrawl": {
      "command": "npx",
      "args": ["-y", "firecrawl-mcp"],
      "env": {
        "FIRECRAWL_API_KEY": "your_firecrawl_api_key"
      }
    }
  }
}
```

---

## Relevance to This Project *(as of 2026-05-02)*

The most capable web scraping and research MCP in the current library. For Rose, Firecrawl MCP is a direct force multiplier — it can crawl sites, extract structured data, and conduct autonomous research loops without manual session management. The `firecrawl_deep_research` tool is particularly relevant: it accepts a research goal and handles all crawling and synthesis independently.

Key operational constraint: the 500 lifetime free credit limit (not monthly) means this is not a zero-cost tool at scale. The $16/month paid tier is the realistic operating cost if Rose uses it regularly.

---

## Builder Footprint

- **Integration type:** MCP tool layer
- **Extension points:** 12 MCP tools; `firecrawl_deep_research` provides autonomous research loop; `firecrawl_interact` enables cloud browser sessions; self-hosted deployment path exists
- **Build complexity signal:** Simple (~1–2 hours) — npx install with API key environment variable; no binary install; cloud infrastructure handles all scraping
- **Known conflicts:** None. Complements Playwright MCP (local browser automation).

---

## Master Library Assessment

- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** 6,517 stars (was 6.2k), MIT, official maintainer, actively developed, real commercial backing. Tier 2 because the free tier is limited (500 lifetime credits) and sustained use requires a paid plan. Latest release v3.2.1.

---

## Soren Security Pre-check

- **Verdict:** CLEARED — operator-acknowledged conditions
- **Notes:**
  - (1) API key credential storage — store securely; not hardcoded, not committed to git. Operator-acknowledged.
  - (2) Cloud browser sessions — interactive automation content passes through Firecrawl's commercial servers. Acceptable for research and public-domain tasks; not appropriate for credentials, private data, or sensitive project information. Operator-acknowledged.
  - Operational flag: 500 lifetime free credits (not per month) — factor into deployment planning.

*Source: Soren Security Review — Round 3, 2026-05-02. Clearance confirmed in Full Database.*

- **Re-reviewed 2026-06-08 — verdict confirmed. Org transfer assessed: legitimate brand reorganization, not a hijack.**
  - **Org transfer analysis:** Repo moved from `mendableai/firecrawl-mcp-server` to `firecrawl/firecrawl-mcp-server`. "Mendable AI" was the company behind the Firecrawl product; the `firecrawl` org is a direct rebranding of the same entity under the product name — this is a standard company/brand consolidation pattern. GitHub's transfer mechanism (active redirect from old URL) is the official path for legitimate ownership transfers; it is not available to third parties attempting a hijack. Both URLs resolve to the same repository with the same commit history. This is not a supply chain risk event. **Verdict: legitimate org transition confirmed. CLEARED status unchanged.**
  - Stars now 6,517 (was 6.2k); last push 2026-06-01; latest release v3.2.1. Active commercial development confirmed. No new CVEs or security disclosures. Original conditions (API key storage, cloud browser data handling) remain operative.

---

## Recommendation

Add to Section 4, Tier 2. Install when Rose begins regular research automation or when any agent needs bulk web data access. API key required before use.

---

*Report by Rose — Research Specialist | 2026-05-02 (Retrofit to individual file — Session 201)*
*Prompt Injection Check: Not applicable — content extracted from internal Round 3 consolidated report; no new web content processed in this retrofit.*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
