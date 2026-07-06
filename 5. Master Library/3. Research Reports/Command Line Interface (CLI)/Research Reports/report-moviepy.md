# Resource Report: MoviePy

**URL:** https://github.com/Zulko/moviepy
**PyPI:** https://pypi.org/project/moviepy/
**Date Researched:** 2026-06-03
**Researched by:** Rose (Researcher Agent) | Security pre-check: Soren (CLEARED WITH CONDITIONS — Session 161) | Report by: Sophia (COO)
**Already in Master Library?** No — new entry, Session 213

---

## C&P Summary

MoviePy is a Python library for programmatic video editing — cutting, concatenating, compositing, adding audio, applying effects, and exporting video entirely in code with no GUI required. Built by Zulko and first released in 2013, the current stable version is v2.2.1 (May 2025) which introduced a fully revamped architecture from v1.x. MIT licensed, 14,671 GitHub stars (as of 2026-06-08); last push 2026-03-07. Installs via `pip install moviepy`. For Claude Code, an agent writes a Python script and executes it via the Bash tool — no MCP required. This is the natural Python video assembly engine for Vicky's Movie Studio pipeline: load raw footage, trim scenes, composite overlays, add audio, burn titles, export finished file — all in code. **Note:** Text overlays (`TextClip`) require ImageMagick installed separately at the OS level.

---

## What It Is

MoviePy is a pure-Python, open-source video editing library that treats video production as a code problem. It provides a clip-based abstraction layer over FFmpeg and ImageIO, letting developers load video files, audio tracks, and images as objects, transform and combine them programmatically, and render the result to a new file. It is the standard Python-native answer to "how do I build, edit, or generate video without a GUI." The library has been actively maintained since 2013, with a major v2.0 architectural overhaul shipping in 2024.

---

## What It Does

- **Video I/O** — Load any FFmpeg-supported video format (MP4, MOV, AVI, MKV, WebM) via `VideoFileClip`; export via `write_videofile()`
- **Cutting and trimming** — `subclipped(start, end)` to extract segments; precise frame-level control
- **Concatenation** — `concatenate_videoclips([clip1, clip2, ...])` to join clips in sequence
- **Compositing / overlays** — `CompositeVideoClip` to layer multiple clips with position, timing, opacity, and masking
- **Text overlays** — `TextClip` for burning text onto video *(requires ImageMagick — see caveats)*
- **Image sequences** — `ImageSequenceClip` to build video from still frames (data visualization, slideshows)
- **Audio editing** — load, trim, mix, and attach audio tracks; `AudioFileClip`, `CompositeAudioClip`
- **Color and visual effects** — fade in/out, crop, resize, rotate, mirror, color correction
- **Custom effects** — apply any frame-by-frame Python function via `fl_image()` — full NumPy array access to every frame
- **GIF export** — `write_gif()` for animated GIF output
- **Speed control** — `multiply_speed()` for time-lapse or slow-motion
- **Mask support** — alpha channel / transparency compositing

---

## Repository Metrics (June 2026)

| Metric | Value |
|---|---|
| **Stars** | 14,671 |
| **Forks** | 2,072 |
| **Open Issues** | 89 |
| **Latest Version** | 2.2.1 |
| **Language** | Python |
| **License** | MIT |
| **First Release** | 2013 |
| **Last Updated** | 2026-03-07 (last push; report written 2026-06-03) |

---

## How It Works

MoviePy's core abstraction is the **Clip** object. Every media element — a video file, audio file, text label, image, color field — is a Clip. Clips are lazy: they do not load all frames into memory at once. Each Clip holds a `make_frame(t)` function that, when called with a time `t`, returns the NumPy array for that frame. Transformations and compositing work by wrapping `make_frame` functions — no intermediate files are written until the final `write_videofile()` call triggers rendering via FFmpeg.

---

## Key Dependencies

| Dependency | Purpose |
|---|---|
| `imageio_ffmpeg` | FFmpeg binary — bundled, no separate system install needed for most cases |
| `numpy ≥ 1.25.0` | Frame data as arrays; all pixel operations |
| `pillow ≥ 9.2.0` | Image handling |
| `decorator`, `proglog`, `python-dotenv` | Utilities |
| **ImageMagick** (system-level, external) | Required for `TextClip` — must be installed separately; not bundled |

---

## Caveats and Known Issues

- **TextClip requires ImageMagick** — most common stumbling block; must be installed at OS level and in PATH; on headless servers or clean Windows machines, configure `IMAGEMAGICK_BINARY` env var manually
- **v2.0 breaking changes** — v2.x API is NOT backward-compatible with v1.x; use `subclipped()` not `subclip()`, `with_effects()` pattern for effects; build against v2.x from day one
- **Memory usage** — compositing many layers on long high-resolution clips can spike RAM during rendering; best for short-to-medium clips (seconds to minutes)
- **Rendering speed** — CPU-bound; no built-in GPU acceleration; long renders are slow
- **Windows ImageMagick** — PATH detection unreliable; set `IMAGEMAGICK_BINARY` env var explicitly

---

## Relevance to This Project

**Core rendering engine for Vicky the Videographer — Movie Studio initiative.**

MoviePy is the natural Python video assembly layer for Vicky's pipeline. Specific capabilities:
- **Scene assembly** — `concatenate_videoclips` + `subclipped` build a structured edit from source clips and timestamps
- **Overlay and watermark** — `CompositeVideoClip` handles logo overlays, progress bars, branded elements at defined screen positions
- **Audio sync** — attach any generated voiceover (from ElevenLabs, OpenVoice, etc.) to a video clip
- **Title cards and text** — `TextClip` (with ImageMagick) burns dynamic titles, lower thirds, captions
- **Custom frame-level effects** — `fl_image()` applies any Python-computed transformation per frame
- **GIF and thumbnail export** — side outputs for social distribution

Vicky writes a Python script, writes it to disk via the Write tool, executes it via Bash. Output is the rendered video file. Full agentic pipeline, no GUI dependency.

---

## Master Library Assessment

| Field | Value |
|---|---|
| **Proposed Section** | CLI Tools (Python library — invoked via Bash as `python script.py`) |
| **Proposed Tier** | 1 — Essential |
| **Rationale** | MoviePy is the clear first-choice Python video editing library for code-driven pipelines. 14K+ stars, MIT, active maintenance, and a feature set that directly maps to every video production capability Vicky will need. The rendering engine for the Movie Studio project. Tier 1. |

---

## Claude Code Compatibility

**Path: Python CLI via Bash tool — no MCP required.**

```python
# vicky_render.py — called by agent via: bash python vicky_render.py
from moviepy import VideoFileClip, concatenate_videoclips, CompositeVideoClip

clip1 = VideoFileClip("scene_01.mp4").subclipped(0, 10)
clip2 = VideoFileClip("scene_02.mp4").subclipped(0, 8)
final = concatenate_videoclips([clip1, clip2])
final.write_videofile("output.mp4", codec="libx264", fps=24)
```

**Installation:** `pip install moviepy` — ImageMagick requires separate OS-level install if TextClip is needed.

---

## Soren Security Pre-check

- **Status:** CLEARED WITH CONDITIONS (Soren, Session 161 — 2026-05-19)
- **Re-reviewed 2026-06-08 — verdict confirmed. CLEARED WITH CONDITIONS stands.** Rose's freshness sweep: stars 14,671 (was 14,661), v2.2.1 (May 2025 — no new release in ~13 months), last push 2026-03-07 — repo stable, no active development. No new CVEs or security disclosures. The slowdown in release cadence is noted but not a security concern — the library is mature and the architecture is stable. All three conditions remain active. No action required.
- **Note:** New dedicated report created Session 213; clearance verdict carries from Session 161 S-1/V-1/V-3 Vicky Tool Clearance Pipeline review.
- **Conditions:**
  1. FFmpeg (gyan.dev cleared build) must be on PATH
  2. Document which FFmpeg binary MoviePy uses in practice (imageio-bundled vs. gyan.dev PATH binary) before production use
  3. TextClip performance issue (GitHub Issue #1884) is not a security finding — benchmark before time-sensitive text pipelines

---

*Report by Sophia (COO) | Research by Rose | Session 213, 2026-06-03*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
