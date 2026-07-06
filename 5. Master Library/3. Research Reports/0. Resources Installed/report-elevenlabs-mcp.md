# Resource Report: ElevenLabs MCP (elevenlabs-mcp)

**URL:** https://github.com/elevenlabs/elevenlabs-mcp
**Date Researched:** 2026-06-04
**Researched by:** Rose | Security pre-check: Soren — CLEARED WITH CONDITIONS | Report by: Rose
**Already in Master Library?** No — net-new item; not yet reviewed or cleared

---

## What It Is

ElevenLabs MCP is the official Model Context Protocol server published by ElevenLabs — the AI voice and audio generation company. It connects Claude and other MCP clients directly to ElevenLabs' API, enabling voice generation, voice cloning, audio transcription, sound effect creation, and voice design entirely through Claude prompts. This is not a playback tool or a media player — it is a production tool: it generates new audio files from text instructions and returns them to the client. It requires an ElevenLabs API key and consumes account credits per operation. The repository is MIT-licensed, maintained by the official ElevenLabs team, and has 1,395 stars on GitHub as of 2026-06-08 (was 706 at research date). Latest release v0.9.1. It is Python-based and installs via `uv`.

## What It Does

- Converts text to speech using ElevenLabs' voice library — any available voice, with fine-grained control over stability, style, and similarity settings
- Clones a voice from an audio sample provided by the user
- Designs new synthetic voices from a text description (specify age, gender, accent, tone, etc.)
- Transcribes audio files to text, with speaker identification (diarization) support
- Generates sound effects and ambient soundscapes from text descriptions (e.g., "thunderstorm in a dense jungle")
- Isolates speech from background noise in an audio file
- Lists available voices and checks remaining API credits on the account
- Produces audio as files saved to disk, as MCP resources (base64-encoded), or both — controlled via an environment variable

## MCP Tool Manifest

- **Tool count:** Approximately 10–12 tools (full manifest confirmed via ElevenLabs official docs; exact count subject to version changes)
- **Tools:**
  - `text_to_speech` — Convert a text string to audio using a selected voice; returns audio file
  - `voice_clone` — Clone a voice from an uploaded audio sample
  - `voice_design` — Generate a new voice from a text description of desired characteristics
  - `speech_to_text` — Transcribe an audio file to text with optional speaker diarization
  - `sound_effects` — Generate sound effects or ambient audio from a text description
  - `isolate_speech` — Remove background noise and isolate speech from an audio file
  - `list_voices` — Return all voices available on the account (pre-made + cloned)
  - `get_credits` — Check remaining API credits on the ElevenLabs account
- **Transport type:** stdio
- **settings.json registration:**
```json
{
  "mcpServers": {
    "elevenlabs-mcp": {
      "command": "uvx",
      "args": ["elevenlabs-mcp"],
      "env": {
        "ELEVENLABS_API_KEY": "your_api_key_here",
        "ELEVENLABS_MCP_OUTPUT_MODE": "files"
      }
    }
  }
}
```
  *Output mode options: `"files"` (default — saves to disk), `"resources"` (returns as base64 MCP resource), `"both"`.*
- **Recommended serverInstructions:** "This server generates and processes audio using the ElevenLabs API. Use it when the user wants to convert text to speech, clone a voice, transcribe audio, or generate sound effects — it produces audio files as output. Requires an active ElevenLabs API key and consumes account credits per operation; check credits before large jobs."

## Relevance to This Project

*(as of research date — context may not carry to future projects)*

This MCP is a direct fit for Vicky's film studio production pipeline. The current stack (MoneyPrinterTurbo, Remotion) produces video and animation — but voice-over and audio are separate gaps. ElevenLabs MCP closes both. Vicky can instruct Claude to generate a narration track for a video, clone a house voice once and reuse it across projects, or produce a soundscape to layer under footage — all without leaving the Claude interface or opening a separate audio tool. It also pairs with the mcp-youtube transcript tool: pull a transcript → edit the script → generate the voice-over in the same session. The sound effects capability adds another production layer that would otherwise require a separate library or contract tool.

## Builder Footprint

- **Integration type:** MCP tool layer / Skill-composable
- **Extension points:** Audio file output path is configurable; Cosmo can build skills that chain transcript → script edit → TTS generation into a single workflow. The `resources` output mode enables direct MCP resource passing to downstream tools.
- **Build complexity signal:** Moderate (~half-day to integrate with the broader media pipeline; basic registration is simple, but chaining with Remotion or MoneyPrinterTurbo for synced audio/video output adds complexity)
- **Known conflicts:** None identified against existing MCP catalog items. HeyGen MCP (archived) had overlapping video generation scope but is out of service; no active conflict. No other audio generation MCP is currently in the ML.

## Master Library Assessment

- **Proposed Section:** 6 — Model Context Protocol (MCP)
- **Proposed Tier:** 1
- **Rationale:** Official vendor MCP, actively maintained, 1,395 stars (up from 706 at research date), MIT license, direct production value for the film studio track. Tier 1 appropriate — core infrastructure for the audio/voice layer of Vicky's workflow.

## Soren Security Pre-check

- **Verdict:** **CLEARED WITH CONDITIONS**
- **Reviewed by:** Soren | 2026-06-04

**Checked:**
- Manual read (Cat 1): pass — README, server.py, and config files reviewed; no prompt injection signals, no obfuscated code, no behavioral override language; code is well-structured and consistent with stated purpose; server.py header explicitly warns against calling tools without user request; API key is loaded from environment variable (not hardcoded)
- Cat 3 (MCP Tool Manifest Review): pass — all tool descriptions reviewed; descriptions are scoped to their stated functions; cost warning annotations on billable tools are appropriate user-protection language, not override language; no redirection indicators; no instruction-like content designed to alter Claude's routing behavior
- Cat 2 — Trivy (repo scan): findings — 32 CVEs in `uv.lock` (2 CRITICAL, 13 HIGH, 15 MEDIUM, 2 LOW) + 3 Dockerfile misconfigs; see findings below
- Cat 2 — Gitleaks (secrets scan): pass — no leaks found; 1 commit scanned (~320KB)
- Cat 3 (Snyk Agent Scan): not run — Python/uvx not installed on this machine; flagged for follow-up

**Findings:**

| Severity | CVE | Package | Installed | Fixed | Issue |
|----------|-----|---------|-----------|-------|-------|
| CRITICAL | CVE-2026-32871 | fastmcp | 0.4.1 | 3.2.0 | SSRF via path traversal in OpenAPI path |
| CRITICAL | CVE-2025-43859 | h11 | 0.14.0 | 0.16.0 | Accepts malformed chunked-encoding bodies |
| HIGH | CVE-2025-69196 | starlette | 0.46.2 | — | DoS |
| HIGH | CVE-2026-26007 | (dependency) | — | — | See Trivy output |
| HIGH | CVE-2024-47874 | (dependency) | — | — | See Trivy output |
| HIGH | CVE-2025-66416 | mcp | 1.6.0 | 1.23.0 | DNS rebinding protection disabled by default |
| HIGH | CVE-2025-66418 | urllib3 | 2.4.0 | 2.6.0 | Unbounded decompression chain |
| HIGH (×7) | various | various | — | — | Additional HIGH CVEs in urllib3, starlette, others |
| MEDIUM (×15) | various | various | — | — | MEDIUM CVEs across idna, requests, starlette, urllib3, fastmcp, mcp |
| Dockerfile | DS-0002 (HIGH) | — | — | — | Container runs as root — no USER command |
| Dockerfile | DS-0026 (LOW) | — | — | — | No HEALTHCHECK instruction |

**CRITICAL CVE assessment:** Both CRITICAL CVEs are in the dev lockfile (`uv.lock`) — these are locked development dependency versions. When installed via `uvx elevenlabs-mcp` from PyPI, the package manager resolves current versions. The published `pyproject.toml` specifies `mcp[cli]>=1.9.0` (not pinned to 1.6.0) — current PyPI releases likely install clean versions. Dockerfile CVEs are not relevant to stdio MCP deployment (team does not use Docker deployment path). The SSRF finding in fastmcp warrants note: fastmcp 0.4.1 is locked in dev, but pyproject.toml does not pin fastmcp directly — it is a transitive dependency; current resolution should pull a clean version.

**Conditions:**
1. API key handling — `ELEVENLABS_API_KEY` must be stored only in `settings.json` env block or local `.env`; never committed to version control; verify `.gitignore` covers `settings.json` and any local config before adding the key
2. Audio data to external servers — all TTS, cloning, and transcription operations send content to ElevenLabs servers; acceptable for Vicky's film studio workflow; confirm before sending sensitive or proprietary audio
3. Free tier commercial license — free plan (10,000 credits/month) does not include commercial usage rights; paid plan required before any commercial production use
4. Verify PyPI install resolves clean versions — before first use, confirm that `uvx elevenlabs-mcp` installs `fastmcp >= 3.2.0`, `h11 >= 0.16.0`, and `mcp >= 1.23.0`; if any CRITICAL or HIGH CVEs persist in the resolved install, halt and flag to Sage
5. Snyk Agent Scan to be completed when Python/uvx is available — does not block installation

**What would change this verdict:** If the PyPI install resolves to the locked vulnerable versions (fastmcp 0.4.1, h11 0.14.0), verdict reverts to ESCALATE pending Sage direction on whether to wait for ElevenLabs to update their lockfile or proceed with a known-CVE dependency.

**Re-reviewed 2026-06-08 — verdict confirmed: CLEARED WITH CONDITIONS. Conditions 4 and 5 remain open.**

Assessment of open conditions from available data:
- **Condition 4 (PyPI install CVE check):** The published `pyproject.toml` specifies `mcp[cli]>=1.9.0` — a floor, not a pin — so current PyPI resolution *should* pull `mcp >= 1.23.0` (clean). The fastmcp SSRF CVE (0.4.1) and h11 chunked-encoding CVE (0.14.0) are locked in the dev `uv.lock` file, not in the published package constraints. However, "should resolve clean" is not confirmed — PyPI dependency resolution depends on the exact package graph at install time. **This condition cannot be closed from document review alone. It requires a live `uvx elevenlabs-mcp` install and version check before deployment.** Condition 4 remains open.
- **Condition 5 (Snyk Agent Scan):** Python/uvx availability is an environment question. This does not block installation but should be completed as a post-install step before active production use. Condition 5 remains open.
- Stars have grown to 1,395 (was 706 at research date); last push 2026-05-18; latest release v0.9.1. Official ElevenLabs team maintenance confirmed. No new public CVEs at the repo level since original review. The CRITICAL CVE situation (fastmcp SSRF, h11 malformed encoding) is contained in the dev lockfile and the path to clean PyPI resolution is credible — but unconfirmed.
- **Do not install until Condition 4 is verified.** If PyPI resolves to the vulnerable locked versions, escalate to Sage before proceeding.

## Recommendation

Add to Section 6 (MCP) at Tier 1 pending Soren clearance. ElevenLabs API key is required — obtain from elevenlabs.io before installation. Free tier (10,000 credits/month ≈ 10,000 characters of TTS) is sufficient for testing; a paid plan ($5–$22/month depending on tier) is required for commercial production use. Soren should review the API key handling and data transmission flags before deployment.

## C&P Summary

ElevenLabs MCP is the official tool from ElevenLabs that lets Claude generate AI voices, clone voices, transcribe audio, and create sound effects — all through simple text instructions. For Vicky's film studio, it fills the audio gap in the current production stack: Claude can write a script, generate the voice-over in a chosen voice, and produce the sound effects for a video, without opening any separate audio software. It runs on credits (10,000 free per month, roughly 10 minutes of speech), and an API key from ElevenLabs is required before it can be installed. Soren reviews it next before it goes live.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---
*Report by Rose | Session 215 | 2026-06-04*

---
*Consolidated to single canonical, Session 264 — the fresher category copy was promoted to `0. Resources Installed`; the stale install-folder copy (older stats, missing the freshness sweep / version log) was superseded. No unique content lost. ML Stage 1.*
