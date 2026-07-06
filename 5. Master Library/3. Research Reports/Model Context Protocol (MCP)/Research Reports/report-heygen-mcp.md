# Resource Report: HeyGen MCP

**URL:** https://github.com/heygen-com/heygen-mcp — **404 as of 2026-06-08** (repo fully removed; was archived March 9, 2026; no longer accessible)
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
Official HeyGen MCP server connecting Claude to HeyGen's AI avatar video generation platform.

## What It Does
- Avatar selection, voice selection, script writing, video generation, and status polling — all via Claude prompts
- Tools: get_remaining_credits, get_voices, get_avatar_groups, get_avatars_in_avatar_group, generate_avatar_video, get_avatar_video_status
- Turn strategy insights, weekly recaps, or backtest summaries into short-form video content automatically

## MCP Tool Manifest

**Note: This server is ARCHIVED (March 9, 2026). Repository is read-only. Tool manifest documented for reference only — do not install.**

- **Tool count:** 6 tools
- **Tools:**
  - `get_remaining_credits` — Check remaining HeyGen API credits on the account
  - `get_voices` — List available AI voices for avatar video narration
  - `get_avatar_groups` — List all available avatar groups
  - `get_avatars_in_avatar_group` — List individual avatars within a specific group
  - `generate_avatar_video` — Generate an AI avatar video from a script, avatar, and voice selection
  - `get_avatar_video_status` — Poll the status of a video generation job and retrieve the output URL
- **Transport type:** stdio (was stdio prior to archival)
- **settings.json registration:** Not applicable — archived; do not register
- **Recommended serverInstructions:** N/A — archived server. Do not use. Monitor for a replacement official HeyGen MCP if published.

## Current Status
**ARCHIVED by owner — as of March 9, 2026.** Repository is now read-only. HeyGen described the MCP as being in early development with limited official support; community contributions welcome but unsupported going forward.

## Master Library Assessment
- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 2 (was), now 🗄️ Archived
- **Rationale:** Archived by HeyGen less than one month ago. Not suitable for installation or active use. File as archived. Revisit if HeyGen publishes a new, supported MCP.

## Soren Security Pre-check
- **Verdict:** VOID — Repo fully removed from GitHub (404 as of 2026-06-08)
- **Notes:** Originally N/A — Archived (March 9, 2026); repo was read-only at time of original review. As of June 8, 2026 the repository has been fully deleted from GitHub — it no longer exists at any URL. No security review is possible or needed. No installation path exists. This entry is dead. If HeyGen publishes a new MCP, that is a new report from scratch.
- *Re-reviewed 2026-06-08 — verdict updated from N/A to VOID. Repo deletion confirmed by Rose freshness sweep. No clearance issued; none possible.*

## Recommendation
Add to Section 4 as 🗄️ Archived. Note archive date (March 9, 2026) and reason (early development, limited official support). Revisit if HeyGen releases a supported replacement.

---
*Report by Sophia | Session 31 | 2026-03-29*

---

## C&P Summary

HeyGen MCP was HeyGen's official MCP server for AI avatar video generation — it would have allowed Claude to select avatars, choose voices, write scripts, and generate short-form video content entirely through prompts. It was archived by HeyGen on March 9, 2026, less than one month before this report was filed; the repository is now read-only with no active maintenance. As of June 8, 2026 the repo URL returns 404 — the repository has been fully removed from GitHub. Filed as Archived in Section 4. Revisit only if HeyGen publishes a new, officially supported replacement.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
