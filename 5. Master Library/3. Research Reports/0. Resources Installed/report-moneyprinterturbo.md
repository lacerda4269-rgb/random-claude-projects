# Resource Report: MoneyPrinterTurbo

**URL:** https://github.com/harry0703/MoneyPrinterTurbo
**Date Researched:** 2026-06-03
**Researched by:** Rose (Researcher Agent) | Security pre-check: Soren (CLEARED WITH CONDITIONS — Session 214) | Report by: Sophia (COO)
**Already in Master Library?** No — new entry, Session 213

---

## C&P Summary

MoneyPrinterTurbo is an end-to-end AI short-form video generation pipeline — provide a topic or script, and it generates the script via LLM, produces a voiceover via TTS, selects stock footage, adds captions, and assembles a finished short-form video (YouTube Shorts / TikTok style) ready to publish. It orchestrates multiple AI services (LLM provider, TTS provider, stock footage API, subtitle generation, FFmpeg final assembly) through a web UI and HTTP API. MIT licensed, 78,778 stars, updated today (2026-06-03) — most stars of any tool in the current Movie Studio / Vicky research batch. Free and open source; requires API keys for the services it calls (all configurable to free-tier services). No native MCP, but the built-in HTTP API makes custom integration straightforward. CLI via Bash tool or HTTP API endpoint.

---

## What It Is

MoneyPrinterTurbo is a fully automated short-form video factory in code. Give it a topic (or write your own script), configure your preferred AI providers, and it handles the full production pipeline: script writing, voice generation, footage sourcing, subtitle burning, and final video export. Designed specifically for YouTube Shorts, TikTok, and Instagram Reels formats. Includes a web-based UI for manual operation and an HTTP API for programmatic use. Built by harry0703 (GitHub), actively maintained with commits today.

---

## What It Does

**Full pipeline (automatic or semi-automatic):**
1. **Script generation** — LLM generates a short-form video script from a topic or keyword
2. **Voiceover generation** — TTS converts the script to audio; multiple providers supported
3. **Stock footage selection** — queries Pexels or Pixabay APIs for relevant B-roll clips
4. **Subtitle generation** — auto-generates captions synced to the voiceover
5. **Video assembly** — FFmpeg concatenates footage, lays the voiceover, burns subtitles, exports final MP4

**LLM providers supported:**
- OpenAI, Moonshot, Azure OpenAI, Ollama (local), and others

**TTS providers supported:**
- Azure TTS, OpenAI TTS, ElevenLabs, edge-tts (free, no API key), and others

**Stock footage APIs:**
- Pexels (free tier available), Pixabay (free tier available)

**Output formats:**
- Short-form vertical video (9:16), configurable resolution and duration

**Interface:**
- Web UI — launch locally, configure and generate via browser
- HTTP API — programmatic endpoint for agent integration

**Additional features:**
- Custom script input (bypass LLM generation)
- Background music support
- Multiple language support (via TTS provider selection)
- Subtitle style customization

---

## Repository Metrics (June 2026)

| Metric | Value |
|---|---|
| **Stars** | 78,778 |
| **License** | MIT |
| **Last Updated** | 2026-06-03 (today — actively maintained) |
| **Language** | Python |
| **Interface** | Web UI + HTTP API |

---

## How It Works

MoneyPrinterTurbo is a Python orchestration layer. On a generation request (via web UI or API), it:
1. Calls the configured LLM API to generate a script
2. Calls the configured TTS API to convert the script to an audio file
3. Calls Pexels or Pixabay API to search for and download relevant video clips
4. Uses FFmpeg to cut clips to required duration, concatenate, and add the audio track
5. Generates subtitle file (SRT) and burns it onto the final video via FFmpeg
6. Exports the finished MP4

Each provider is swappable via config. All API keys are stored in a local `.env` file.

---

## Key Dependencies

- **FFmpeg** — video assembly, subtitle burning, final export (system-level install required)
- **LLM API** — OpenAI, Azure, Ollama, etc. (configurable)
- **TTS API** — Azure, OpenAI, ElevenLabs, edge-tts (configurable; edge-tts is free)
- **Pexels API or Pixabay API** — stock footage (both have free tiers)
- **Python** — base runtime

---

## Caveats and Known Issues

- **API key dependencies** — the pipeline requires at least one LLM, one TTS, and one stock footage API key. All have free tiers, but production volume will hit rate limits.
- **Stock footage quality** — Pexels/Pixabay results are keyword-matched, not semantically matched. Footage relevance depends on how well the script's keywords map to available stock clips.
- **No native MCP** — custom integration via HTTP API required for agent-native use. Medium integration effort.
- **GPU not required** — the pipeline is I/O bound (API calls + FFmpeg); no local GPU needed.
- **Windows compatibility** — FFmpeg must be installed separately and in PATH on Windows.

---

## Relevance to This Project

**Direct fit for Vicky the Videographer — Movie Studio initiative.**

MoneyPrinterTurbo is the fastest path from zero to a finished short-form video. For Vicky, this is the "start here" tool for short-form content production (YouTube Shorts, TikTok, Instagram Reels). It handles the full production loop in one orchestrated pipeline. Vicky can call it via its HTTP API endpoint — no manual web UI required once configured.

The edge-tts option (free, no API key) makes the TTS layer accessible immediately. Combined with Pexels (free tier), the entire pipeline can be tested at zero cost before committing to paid API tiers.

---

## Master Library Assessment

| Field | Value |
|---|---|
| **Proposed Section** | CLI Tools (Python / HTTP API — invoked via Bash or HTTP call) |
| **Proposed Tier** | 1 — Essential |
| **Rationale** | 78,778 stars (highest in the Movie Studio batch), MIT, actively maintained, most complete end-to-end pipeline in the class. When Vicky needs to produce short-form video output, this is the first tool to reach for. Tier 1 for any project where short-form video production is in scope. |

---

## Soren Security Pre-check

- **Status:** CLEARED WITH CONDITIONS (Soren, Session 214 — 2026-06-04)
- **Scanned by:** Trivy v0.71.0 + Gitleaks v8.30.1
- **Manual read:** Pass — no prompt injection signals detected
- **Trivy:** 0 CRITICAL, 3 HIGH — all in `pillow` v11.3.0 pinned in uv.lock (dev lock, not installed packages). Fix: pillow 12.2.0 resolves all three HIGH CVEs.
- **Gitleaks:** Clean — 207 MB scanned, 0 secrets found
- **Conditions:**
  1. Pin `pillow` ≥ 12.2.0 before deployment
  2. FFmpeg clearance carries from Session 161 (v8.1.1, gyan.dev build, internal use only)

---

*Report by Sophia (COO) | Research by Rose | Session 213, 2026-06-03*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---
*Consolidated S264: the `-updated` body was current but had dropped provenance; reattached the **Report Version Log** from the original category copy. Canonical renamed to drop the `-updated` suffix. Both prior copies superseded. ML Stage 1.*
