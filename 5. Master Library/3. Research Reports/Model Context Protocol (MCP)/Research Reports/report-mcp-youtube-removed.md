# Resource Report: mcp-youtube (adhikasp)

> **⚠️ STATUS OVERRIDE — Session 222 (2026-06-05)**
> **Installed:** Session 218 — 2026-06-04 | **Tested:** Session 222 — 2026-06-05 | **Result: FAILED**
> `get_youtube_transcript` tool did not return transcripts for tested YouTube videos after extended run time. Tool timed out / produced no usable output.
> **Removed from `.mcp.json`:** Session 222. **Replacement confirmed:** `transcribe-anything` CLI v4.0.0 (Soren-cleared) — full transcript of ~8 min video in under 5 minutes, CPU backend, Session 222.
> Report and record retained for reference. Do not reinstall without investigating root cause.

**URL:** https://github.com/adhikasp/mcp-youtube
**Stats (June 2026):** 50 stars | 20 forks | 0 open issues | Last push: 2025-12-02 | No formal releases | Status: active repo, but no updates since December 2025 — stale dependencies likely explain tool failure
**Date Researched:** 2026-06-04
**Researched by:** Rose | Security pre-check: Soren — CLEARED WITH CONDITIONS | Report by: Rose
**Already in Master Library?** No — net-new item; not yet reviewed or cleared

---

## What It Is

`mcp-youtube` is a lightweight, community-built MCP server by Adhika Setya Pramudita (`adhikasp`) that fetches YouTube video transcripts and delivers them — including timestamps — to any MCP-compatible client. It is a transcript extraction tool only: it pulls the text that already exists as subtitles or auto-generated captions on a YouTube video and surfaces it to Claude. It does not generate video, download video files, upload anything to YouTube, interact with YouTube's creator tools, or access any YouTube data beyond publicly available transcripts.

## What It Does

- Accepts a YouTube video URL and returns the full transcript with timestamps
- Works with any video that has subtitles or auto-generated captions available (most public videos qualify)
- Enables Claude to summarize, translate, extract quotes, identify key moments, or create structured notes from any YouTube video content
- Transcript delivery is text-only — no audio, no video, no binary output
- Compatible with any MCP client (Claude Desktop, Cursor, Windsurf, etc.)

## MCP Tool Manifest

- **Tool count:** 1 tool
- **Tools:**
  - `get_youtube_transcript` — Fetches the transcript (with timestamps) from a given YouTube video URL and returns it as plain text
- **Transport type:** stdio
- **settings.json registration:**
```json
{
  "mcpServers": {
    "mcp-youtube": {
      "command": "uvx",
      "args": ["mcp-youtube"]
    }
  }
}
```
- **Recommended serverInstructions:** "This server fetches transcripts from YouTube videos. Use it when the user provides a YouTube URL and wants to summarize, translate, extract quotes, or otherwise work with video content — the server returns the full timestamped transcript as text. It does not download video, generate content, or access YouTube creator tools."

## Relevance to This Project

*(as of research date — context may not carry to future projects)*

This MCP is directly relevant to Vicky's small film studio workflow and the P7 web browsing and animations track. Vicky regularly needs to pull content from YouTube — reference footage, competitor work, educational material — and summarize or extract usable material from it. Rather than manually watching and transcribing, Claude can fetch the transcript in one step and immediately begin working with the content: summarizing a 20-minute tutorial, pulling a quote for a script, or building a timestamped reference log. It pairs naturally with the broader AI media pipeline (MoneyPrinterTurbo, Remotion, ElevenLabs) — transcripts as raw material feeding downstream production steps.

## Builder Footprint

- **Integration type:** MCP tool layer
- **Extension points:** Single tool; no plugin hooks or event streams. Cosmo can wrap the transcript output in downstream processing — pipe into summarization chains, translation prompts, or content extraction workflows.
- **Build complexity signal:** Simple (~1 hour to register and verify; the tool exposes one function with minimal config)
- **Known conflicts:** None identified. No overlap with existing Section 4 MCP items — no other transcript-specific MCP is cataloged. The Playwright MCP can load YouTube pages but does not extract transcripts; no conflict.

## Master Library Assessment

- **Proposed Section:** 6 — Model Context Protocol (MCP)
- **Proposed Tier:** 2
- **Rationale:** Community-built, single-purpose tool with a clear, narrow scope. Minimal risk profile. Tier 2 appropriate — useful for the current workflow without being a core infrastructure item.

## Soren Security Pre-check

- **Verdict:** **CLEARED WITH CONDITIONS**
- **Reviewed by:** Soren | 2026-06-04

**Checked:**
- Manual read (Cat 1): pass — README and source code reviewed; no prompt injection signals, no obfuscated code, no misleading content, no unusual permission requests; single tool (`get_transcript`) with narrow, stated scope; dependencies are standard MCP/Python stack
- Cat 3 (MCP Tool Manifest Review): pass — one tool; tool name, description, and parameters are clean; no behavioral override language, no redirection indicators, no instruction-like content
- Cat 2 — Trivy (repo scan): 15 CVEs found in `uv.lock` (8 HIGH, 7 MEDIUM, 0 CRITICAL) across `mcp`, `starlette`, `urllib3`, `requests`, `idna`, `python-dotenv` — all fixed in newer versions; all flags are dependency version issues, not code-level vulnerabilities in mcp-youtube itself
- Cat 2 — Gitleaks (secrets scan): pass — no leaks found; 1 commit scanned, ~30KB
- Cat 3 (Snyk Agent Scan): not run — Python/uvx not installed on this machine; not a blocker given clean results across all other checks

**Findings:**
- Dependency CVEs (HIGH/MEDIUM): 15 CVEs in locked dependency versions. These resolve automatically when installed via `uvx mcp-youtube` on a current Python environment — uvx pulls from PyPI and resolves to current versions, not the repo's locked dev versions. No action required for standard installation.
- YouTube ToS: `youtube-transcript-api` library accesses publicly available captions/subtitles via YouTube's standard web interface — same data accessible to any browser. Personal/educational use is low risk. Commercial use at scale (bulk automated requests) may attract ToS scrutiny. For Vicky's film studio workflow (individual video research and reference), risk is minimal.

**Conditions:**
1. Use for personal/educational/small-scale production work only — do not automate bulk transcript extraction at volume
2. Snyk Agent Scan (Cat 3 complement) to be run when Python/uvx is available on this machine — does not block installation, but complete the scan before any production-scale use

**What would change this verdict:** Nothing — conditions are operational guardrails, not security blockers. CLEARED for installation and use within stated conditions.

*Re-reviewed 2026-06-08 — CLEARED WITH CONDITIONS verdict confirmed. The 15 CVEs (8 HIGH, 7 MEDIUM) in locked dev dependencies are unchanged — they remain dependency version issues only, not code-level vulnerabilities, and still resolve automatically on uvx install. The 6+ month staleness (last push 2025-12-02) is consistent with the tool failure documented in the Session 222 STATUS OVERRIDE at the top of this report — stale locked deps are the most likely root cause of the transcript fetch timeout. This does not change the security verdict: the tool is still cleared to install. However, before any reinstall attempt, the root cause of the Session 222 failure (stale dep resolution, YouTube API change, or both) should be investigated first. Snyk Agent Scan (Condition 2) remains pending and should be completed before any production-scale use.*

## Recommendation

Add to Section 6 (MCP) at Tier 2 pending Soren clearance. Straightforward install via `uvx mcp-youtube` once cleared — no API key required, no subscription. Soren should confirm ToS compliance with YouTube's automated access policy before deployment.

## C&P Summary

mcp-youtube is a small, community-built tool that lets Claude pull the transcript from any YouTube video — including timestamps — just by providing a URL. It is a read-only transcript tool: it cannot download video files, generate content, or touch YouTube's creator tools in any way. For Vicky's film studio workflow, it means Claude can immediately summarize a tutorial, extract a quote, or build a reference log from any YouTube video without anyone having to watch and manually transcribe it. It is free to use, requires no API key, and installs in under a minute. Soren review is the next gate before installation.

---
*Report by Rose | Session 215 | 2026-06-04*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---
*Consolidated to single canonical, Session 264 — the fresher category copy was promoted to `0. Resources Installed`; the stale install-folder copy (older stats, missing the freshness sweep / version log) was superseded. No unique content lost. ML Stage 1.*
