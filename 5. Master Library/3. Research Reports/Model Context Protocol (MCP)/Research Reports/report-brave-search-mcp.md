# Resource Report: Brave Search MCP

**URL:** https://github.com/brave/brave-search-mcp-server
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
Official MCP server from Brave — integrates the Brave Search API directly into Claude Code sessions for real-time web search across six endpoint types.

## What It Does
- Web search, news search, image search, video search, local business search, AI-powered summarization
- Privacy-focused independent search index (not Google/Bing results)
- Sub-second response times; returns clean JSON
- Dual transport modes: STDIO (default) and HTTP
- Deploy via NPX, Docker, or Smithery
- 2,000 free queries/month; no credit card required for free tier

## MCP Tool Manifest

- **Tool count:** 6 tools
- **Tools:**
  - `brave_web_search` — Full web search using Brave's independent index; returns title, URL, description, and optional extra snippets
  - `brave_news_search` — News-specific search across current events and recent articles
  - `brave_image_search` — Image search returning image URLs and metadata
  - `brave_video_search` — Video search returning video results with source URLs
  - `brave_local_search` — Local business and place search with location context
  - `brave_summarize` — AI-powered summarization of a topic using Brave's LLM layer
- **Transport type:** stdio (default) or HTTP (optional via BRAVE_MCP_TRANSPORT env var)
- **settings.json registration:**
```json
{
  "mcpServers": {
    "brave-search": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-brave-search"],
      "env": {
        "BRAVE_API_KEY": "your_brave_api_key_here"
      }
    }
  }
}
```
- **Recommended serverInstructions:** "Brave Search MCP provides real-time web, news, image, video, and local search using Brave's independent search index. 2,000 free queries/month. Use for any research or current-information lookup tasks."

## Relevance to This Project
Real-time research for Rose and all agents. Check recent news on instruments, verify economic events, research broker/platform changes, look up API changes and library updates. Replaces manual browser searching within agent sessions.

## Master Library Assessment
- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 2
- **Rationale:** High value across all workflows but Phase 2 — not needed until research becomes a regular part of active builds. Official Brave source.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** 1,160 stars (was 842), MIT license, official Brave organization repo, free API tier with no credit card required. No malicious patterns detected.
- **Notes:** Privacy-focused design reduces data exposure risk. Clean JSON output means no raw HTML parsing — lower injection surface than scraping alternatives.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Stars now 1,160 (was 842); last push 2026-06-04; latest release v2.0.83 (2026-06-01). Actively maintained by official Brave org. MIT license unchanged. No new CVEs or security disclosures. CLEARED status stands with no conditions.

## Recommendation
Add to Section 4, Tier 2. Phase 2 install. Free tier (2,000 queries/month) sufficient for initial use.

---
*Report by Sophia | Session 31 | 2026-03-29*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---

## C&P Summary

Brave Search MCP is the official MCP server from Brave that connects Claude Code sessions directly to the Brave Search API for real-time web search. It covers web, news, image, video, local business, and AI summarization — using Brave's independent search index (not Google or Bing). It is the research backbone for Rose and all agents: checking news on instruments, verifying economic events, looking up API changes, and replacing manual browser searching within sessions. Free tier provides 2,000 queries per month with no credit card required. Phase 2 install; official Brave source, MIT license, cleared with no concerns.
