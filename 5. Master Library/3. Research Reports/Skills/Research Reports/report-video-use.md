# Resource Report: video-use

**URL:** https://github.com/browser-use/video-use
**Date Researched:** 2026-06-02 | **Updated:** 2026-06-08
**Researched by:** Rose | Security pre-check: Soren | Report by: Rose
**Already in Master Library?** No — GitHub repository

---

## What It Is

video-use is an open-source Claude Code skill that turns natural-language conversation into a finished video edit. You drop raw footage into a folder, open Claude Code, and describe what you want — the agent transcribes the audio, reasons from a compact transcript and on-demand visual composites, proposes a cut strategy for your approval, renders the result using ffmpeg, and self-evaluates the output before handing it back. It never feeds raw video frames to the LLM; instead it uses ElevenLabs Scribe for word-level transcription (~12KB per project) plus occasional filmstrip+waveform PNGs, reducing token usage from a naive ~45M tokens per project to a minimal amount. The skill installs as a symlink in `~/.claude/skills/` and activates through Claude Code native skill-loading.

---

## What It Does

- Transcribes source footage via ElevenLabs Scribe to get word-level timestamps and speaker diarization; caches results to avoid re-transcribing unchanged sources
- Removes filler words (umm, uh, false starts) and dead space between takes by snapping cuts to word boundaries from the transcript
- Applies per-segment color grading using an ASC CDL mental model (slope/offset/power reasoning, not presets); ships two example grades: `warm_cinematic` and `neutral_punch`
- Applies 30ms audio fades at every cut boundary to eliminate pops
- Burns customizable subtitles (default: 2-word UPPERCASE chunks; configurable by style and placement)
- Spawns parallel sub-agents for animation overlays using HyperFrames (browser-native/kinetic typography), Remotion (React component-based), Manim (formal diagrams/math), or PIL+PNG sequences
- Generates an EDL (Edit Decision List) in JSON format capturing source, in/out points, beat labels, grade, overlays, and subtitle reference
- Self-evaluates the render at every cut boundary before presenting output; caps evaluation passes at 3 and flags remaining issues rather than looping indefinitely
- Persists session memory and editorial notes in `project.md` across editing sessions
- Requires explicit strategy confirmation before any editing begins — no silent execution
- Produces output in `<videos_dir>/edit/final.mp4`; intermediate deliverables (preview, transcripts, graded clips, animations, SRT) organized in a defined directory structure
- Optional yt-dlp integration for pulling source footage from URLs

---

## Relevance to This Project

This project is building an automated trading system with a full agent pipeline. At first pass, video-use appears outside that domain — this is a video editing skill, not a trading or data tool. The relevance is indirect but real in two ways.

First, the architectural pattern here is one of the cleanest examples of a well-engineered Claude Code skill currently available: strict lane discipline (strategy confirmation before execution, self-evaluation before delivery, session memory via project.md), parallel sub-agent orchestration for independent tasks (animation rendering), a defined hard-rules set that prevents silent failures, and a token-efficient data representation strategy (transcript + selective visuals instead of raw frame feeds). These are all patterns directly applicable to how Cosmo should build skills in this project, and how agents should be designed to handle multi-step execution sequences with verification gates.

Second, as the pipeline matures and Jay needs to produce content around the trading system — demos, tutorials, explanatory videos — video-use is the tool that handles that without requiring a separate workflow or external editing software. It is not a Phase 1 install, but it belongs in the library for that future use.

---

## Builder Footprint

- **Integration type:** Skill-composable — installs as a directory symlinked into `~/.claude/skills/video-use`; loads into Claude Code native skill system; no CLI binary, no MCP server
- **Extension points:** Six Python helper scripts (`transcribe.py`, `transcribe_batch.py`, `pack_transcripts.py`, `timeline_view.py`, `render.py`, `grade.py`) are independently callable; the EDL JSON format is a structured interface Cosmo can read or write against; animation engine selection (HyperFrames / Remotion / Manim / PIL) is modular and swappable; the SKILL.md hard-rules set is a reusable design pattern for any skill Cosmo builds
- **Build complexity signal:** Moderate (~half-day) — repository clone + symlink + uv sync + ffmpeg install + ElevenLabs API key configuration; Node.js 22+ required only if HyperFrames animations are used; animation engines install lazily on first use
- **Known conflicts:** None identified with existing ML items. ElevenLabs Scribe is an external paid API (free tier available); any project using this skill incurs transcription costs per source file. Not to be confused with MCP-based video tools (different integration layer entirely).

---

## Master Library Assessment

- **Proposed Section:** 3 — Skills
- **Proposed Tier:** 2
- **Rationale:** Strong engineering quality, active maintenance (9,255 stars, 1,338 forks as of 2026-06-08; last pushed 2026-05-15 — approximately 3.5 weeks before research update), and a clean architectural pattern worth studying. Tier 2 rather than Tier 1 because it is domain-specific (video production) and not immediately relevant to the trading system build — useful when content production becomes a project need.

---

## Soren Security Pre-check

- **Verdict:** CLEARED WITH CONDITIONS
- **Checked (updated 2026-06-08):** License (MIT — permissive, confirmed), stars (9,255 — up from 8.8k), forks (1,338), last pushed (2026-05-15 — approximately 3.5 weeks before update), open issues (28 — up from 8; reviewed for security content), Python dependencies (requests, librosa, matplotlib, pillow, numpy — all standard scientific/utility packages, no supply chain concerns identified), external API surface (ElevenLabs Scribe only), install mechanism (git clone + symlink + uv sync), prompt injection check (CLEAN)
- **Notes:**

| # | Severity | Flag | Notes |
|---|----------|------|-------|
| 1 | MEDIUM | ElevenLabs Scribe — external audio egress | Audio data is transmitted to ElevenLabs servers for transcription. Not a concern for general video editing; becomes a concern if used on recordings containing proprietary business discussions, trading strategy calls, or any sensitive spoken content. Confirm acceptable use before deploying on any such recording. |
| 2 | MEDIUM | Open issues jump 8 → 28 (Soren re-review) | Soren reviewed the issue tracker for security-relevant entries. The 20-issue increase reflects new feature requests and usability questions — no security-related issues identified in current open set. Issue tracker moderation is low, but functional codebase quality is not affected. Not a security signal; flagged as an ongoing watch item. |
| 3 | LOW | .env file with ElevenLabs API key | Key is stored in a .env file at the repo root. Install documentation correctly flags exclusion from version control (chmod 600 recommended). Standard practice — enforce on install. |
| 4 | INFO | Prompt injection check — CLEAN | No instruction-like language or directive content detected in web content or codebase reviewed. |

No supply chain flags. No obfuscated code patterns. No undisclosed network endpoints beyond ElevenLabs. MIT license is clean. Clearance and conditions unchanged from prior review; issue count re-reviewed and confirmed not a security concern.

*Reviewed by Soren | 2026-06-08*

---

## Recommendation

Add to the Master Library at Section 3 — Skills, Tier 2. No immediate deployment needed; this is a content-production capability to pull when Jay needs to produce video around the trading system. Soren should confirm the ElevenLabs data egress condition is acceptable before any live use on recordings containing sensitive business content. Full Soren tool-stack review required before deployment.

---

## C&P Summary

video-use is a Claude Code skill that lets you edit videos by having a conversation. You drop your raw footage in a folder, tell Claude what you want the final video to look like, and it does the work — it transcribes all the audio, figures out where to cut, removes filler words and dead space, applies color grading, adds subtitles, and assembles a finished MP4. It never watches the video directly; instead it reads a compact text transcript of the audio and only looks at actual frames when it needs to make a specific visual decision, which keeps costs low. It is MIT-licensed, has about 8,800 GitHub stars, and was actively maintained through May 2026. For this project specifically, it is not needed right now — the focus is on building a trading system, not editing videos — but it belongs in the library for when content production becomes relevant. It also has one of the cleanest skill designs seen so far, and the patterns it uses (confirm strategy before executing, self-evaluate before delivering, run animations in parallel) are worth applying to skills Cosmo builds in this project.

---

---

## Report Version Log

| Version | Date | What Changed |
|---------|------|--------------|


*Report by Rose | Session 202 | 2026-06-02*
*Updated by Rose | Session 230 | 2026-06-08*
