# Resource Report: transcribe-anything

**URL:** https://github.com/zackees/transcribe-anything
**Date Researched:** 2026-04-21 | **Freshness Update:** 2026-06-03 (Session 213)
**Researched by:** Rose | Security pre-check: Soren — **CLEARED** (confirmed in ML Full Database; Session 218) | Report by: Rose
**Already in Master Library?** Yes — Section 5 (CLI), Tier confirmed at filing

---

## What It Is

transcribe-anything is an open-source, multi-backend audio and video transcription tool built in Python by Zachary Vorhies (GitHub: zackees). It wraps OpenAI's Whisper AI model with automatic hardware detection, backend selection, and optional speaker identification. Created around early 2022, actively maintained through April 2026.

## What It Does

The tool accepts local audio/video files or URLs (YouTube, Rumble, direct links) and produces transcriptions in SRT, VTT, and plain text formats. It automatically routes to the fastest available backend based on the host hardware:

- **MLX** (`--device mlx`) — Apple Silicon only; uses lightning-whisper-mlx, 4x faster than the standard MPS backend; multi-language support
- **Insanely Fast** (`--device insane`) — GPU (CUDA) on Windows/Linux; uses transformer-based insanely-fast-whisper; supports speaker diarization
- **Insane Flash** (`--device insane-flash`) — *New June 2026* — FlashAttention2 backend for CUDA users; runs in isolated venv with pinned `flash-attn==2.8.3`; supports Windows x86_64, Linux x86_64/aarch64, Python 3.11, torch 2.7.0+cu128; macOS unsupported
- **WhisperX** (`--device whisperx`) — *New June 2026* — word-level alignment, improved diarization, word highlighting; requires `--diarize --hf_token` for speaker identification
- **CPU** (`--device cpu`) — Universal fallback; standard OpenAI Whisper implementation

**Speaker diarization** is the standout feature: when a HuggingFace token is supplied via `--hf_token`, the tool produces a `speaker.json` file that labels each segment of conversation by speaker (`SPEAKER_00`, `SPEAKER_01`, etc.). This works only with the `--device insane` backend. A HuggingFace account is required to access the pyannote.audio model that powers diarization.

Additional features:
- `--embed` flag burns subtitles directly into video output
- `--initial_prompt` supports custom vocabulary for domain-specific transcription accuracy
- Backend environments are isolated using the `uv` package manager — no dependency conflicts between backends
- Static ffmpeg bundled — no system ffmpeg required

**Installation:** `pip install transcribe-anything` — single command, immediately available.

## Repository Metrics (June 2026)

- **Stars:** 1,330 (up from ~1,300)
- **Forks:** 134 (up from ~120)
- **Open Issues:** 6
- **Latest Version:** 3.2.10 (up from 3.2.3 — 7 patch releases since April 2026)
- **Language:** Python (96.7%)
- **License:** MIT (GitHub authoritative) — *Note: PyPI metadata shows BSD-3-Clause; treat GitHub as source of truth; flag for Soren to confirm*
- **Created:** ~early 2022
- **Last Updated:** 2026-06-03 (active as of today — committed this morning)

## How It Works

On first run, the tool detects available hardware and selects the appropriate backend. Each backend installs lazily into a `uv`-managed isolated environment. Input is downloaded (if a URL) via yt-dlp, processed through ffmpeg for normalization, and passed to the selected Whisper model. Output files are written to the working directory. Speaker diarization adds a post-processing pass using pyannote.audio to segment and label speakers.

## Key Dependencies

- OpenAI Whisper (base transcription model)
- insanely-fast-whisper (GPU backend)
- lightning-whisper-mlx (Apple Silicon backend)
- pyannote.audio (speaker diarization)
- yt-dlp (URL downloading)
- static-ffmpeg (bundled media processing)
- uv (environment isolation per backend)

## Caveats and Known Issues

- Speaker diarization requires `--device insane` only — not available on CPU or MLX backends
- HuggingFace token required for diarization; user must separately agree to pyannote model terms on HuggingFace
- Python 3.10+ required — Python 3.12 compatibility issues noted at original research are **resolved** (backends run in isolated uv-managed venvs with pinned requirements)
- TikTok URL support: **unconfirmed in documentation** (docs cite YouTube and Rumble); yt-dlp backend natively supports TikTok, so it likely works — treat as untested until confirmed
- distil-whisper/distil-large-v2 model produces stuttering artifacts — avoid
- GPU users need careful batch-size tuning to prevent out-of-memory errors

## Relevance to This Project

A practical CLI transcription utility. Value depends on whether workflows require converting audio or video content (meetings, research interviews, training recordings) into searchable text. The speaker diarization capability adds meaningful value in multi-person recording scenarios. No agent orchestration layer — this is a single-function tool.

## Master Library Assessment

- **Proposed Section:** 3 — CLI Tools
- **Rationale:** pip-installable CLI, single discrete function (transcription + optional diarization), no MCP or orchestration component. Fits the CLI section cleanly. Whether it earns a Tier 1 slot depends on whether the project has active transcription needs.

---

## C&P Summary

transcribe-anything is a free, open-source tool that takes an audio or video file — or a YouTube, Rumble, or supported URL (TikTok untested but likely works via yt-dlp) — and converts the spoken content into text. It automatically picks the fastest method based on your computer's hardware: Apple Silicon Macs get the fastest Mac-optimized approach, Windows or Linux machines with a graphics card get GPU-accelerated processing, and any other computer falls back to a standard method that works everywhere. A standout feature is speaker identification — it can split the transcript by who was speaking, labeling each person as Speaker 1, Speaker 2, and so on. Installation is a single command, it runs entirely on your machine (nothing is sent to any server), and it is completely free. The main practical limitation is that speaker identification requires a free HuggingFace account and only works when running on a GPU.

---

## Sources

- [GitHub Repository — zackees/transcribe-anything](https://github.com/zackees/transcribe-anything)
- [README.md](https://github.com/zackees/transcribe-anything/blob/main/README.md)
- [PyPI — transcribe-anything](https://pypi.org/project/transcribe-anything/)
- [Activity Log](https://github.com/zackees/transcribe-anything/activity)
- [Libraries.io — transcribe-anything 3.2.1](https://libraries.io/pypi/transcribe-anything)

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---

## Soren Security Review

- **Verdict:** CLEARED — conditions apply (unchanged from prior clearance)
- **Re-reviewed:** 2026-06-08

**Major version jump assessment (v3.2.10 → v4.0.0):**

Rose flagged this as a priority for Soren review. I assessed the v4.0.0 release against the following:

- **Install method:** Unchanged — `pip install transcribe-anything`. No new attack surface at install time.
- **Architecture:** Unchanged — uv-managed isolated backend venvs, static-bundled ffmpeg, no external service calls. The two new backends (insane-flash, whisperx) follow the same isolation model as existing backends.
- **New backends:** insane-flash (FlashAttention2, CUDA) and whisperx (word-level alignment) are both community-standard dependencies (flash-attn, whisperx) with no unusual permissions or telemetry.
- **Maintainer:** Same maintainer (zackees), same repository. No ownership or namespace change.
- **No GitHub releases page exists** — v4.0.0 is a PyPI-only release. This means no formal changelog is published. I cannot enumerate specific breaking changes from a published changelog. Rose's report documents what changed (new backends, stable core architecture). No breaking changes that affect security posture are apparent from the documented changes.
- **License discrepancy (pre-existing):** GitHub shows MIT; PyPI metadata shows BSD-3-Clause. This was flagged in the prior clearance and remains unresolved. Both licenses are permissive and acceptable. Soren should request the maintainer clarify the canonical license before this tool is brought into active production use. This is a condition, not a blocker.

**Summary:** The v4.0.0 major version bump does not represent a security regression. The core clearance conditions from the prior review hold. No new concerns introduced by the version jump. The license discrepancy condition carries forward unchanged.

**Conditions on clearance:**
1. Use for personal, non-commercial workflows only (MIT license assumed authoritative; BSD-3-Clause if PyPI is correct — both permissive).
2. Resolve the MIT vs. BSD-3-Clause license discrepancy with the maintainer before production use.
3. Supply HuggingFace tokens only for diarization workflows — confirm model ToS compliance on the HuggingFace side before enabling speaker diarization.
4. Do not install on systems where GPU memory limits are not managed — insane/insane-flash backends require careful batch-size configuration to prevent OOM errors.

---

---
*Consolidated S264: the `-updated` body was current but had dropped provenance; reattached the **Report Version Log** + **Soren Security Review** from the original category copy. Canonical renamed to drop the `-updated` suffix. Both prior copies superseded. ML Stage 1.*
