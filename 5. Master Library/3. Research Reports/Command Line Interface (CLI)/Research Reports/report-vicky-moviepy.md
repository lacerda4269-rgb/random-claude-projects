# Resource Report: MoviePy

**URL:** https://pypi.org/project/moviepy/
**Date Researched:** 2026-05-19
**Researched by:** Rose | Security pre-check: Soren (pending Step 2) | Report by: Rose

---

## What It Is

MoviePy is an open-source Python library for programmatic video editing, released under the MIT license and maintained at https://github.com/Zulko/moviepy. It wraps FFmpeg under the hood for all encoding and decoding operations but exposes a high-level Python API that abstracts away the FFmpeg command-line interface entirely. The current stable release is **v2.2.1**, published February 1, 2026 — the v2.x line introduced breaking changes from v1.x (dropped ImageMagick, PyGame, OpenCV, scipy, and scikit as dependencies; adopted Pillow as the unified image-processing layer). The project carries a maintainer-bandwidth caveat in its own README: "this library has only been kept afloat by the involvement of its maintainers, and there are times where none of us have enough bandwidth." Active development is confirmed — v2.2.1 shipped in early 2026 — but the repo is community-sustained, not commercially backed, which bears watching at production scale.

---

## What It Does

- Load video files, images, and audio as clip objects; trim by time range with a readable Python API
- Layer multiple video and audio clips with precise timing, positioning, and opacity control via `CompositeVideoClip`
- Render text directly onto frames via `TextClip` (Pillow-backed in v2.x, no ImageMagick required)
- Apply built-in effects (fade in/out, color grading, speed changes, mirror, crop) and write custom per-frame effects as Python functions
- Load, trim, mix, and attach audio tracks to video clips; supports fade and volume controls
- Join clips end-to-end with `concatenate_videoclips`
- Render timed text overlays from subtitle data via `SubtitlesClip`
- Export final output to any FFmpeg-supported format (MP4, MOV, GIF, WebM, etc.) via `write_videofile()`
- Create animated GIFs via `write_gif()`
- Iterate or sample individual frames as NumPy arrays for custom processing pipelines

---

## Invocation Interface

- **Typical command pattern:** Python API only — no standalone CLI. Typical usage:
  ```python
  from moviepy import VideoFileClip, TextClip, CompositeVideoClip
  clip = VideoFileClip("input.mp4").subclipped(0, 10)
  txt = TextClip("Hello", font_size=50, color="white", duration=5)
  final = CompositeVideoClip([clip, txt.with_position("center")])
  final.write_videofile("output.mp4", codec="libx264")
  ```
- **Output format:** Video files in any FFmpeg-supported container; NumPy arrays when accessing individual frames; audio files via `write_audiofile()`
- **Key structured output flags:** `codec=` (video codec), `audio_codec=` (audio codec), `fps=` (frame rate), `preset=` (FFmpeg encoding preset), `logger=` (progress/verbosity control)
- **Exit code behavior:** Errors surface as Python exceptions — `OSError` for missing FFmpeg binary, `ValueError` for invalid clip parameters, general `Exception` for FFmpeg subprocess failures. Callers handle via try/except.
- **Stdin/stdout/stderr notes:** MoviePy spawns FFmpeg subprocesses internally. FFmpeg stderr output is captured by MoviePy's logger system and does not flow to the caller's stderr by default unless `logger="bar"` or a custom logger is passed. To suppress all output: `logger=None`.

---

## Relevance to This Project *(as of 2026-05-19 — context may not carry to future projects)*

MoviePy fills a specific and deliberate gap in Vicky's toolchain. The stack already includes raw FFmpeg (for maximum performance) and ffmpeg-python (for subprocess-level Python scripting). MoviePy operates at a higher abstraction layer than either: it is the right tool when a task requires multi-clip compositing, text overlay rendering, or per-frame effect work where Python readability and rapid iteration matter more than execution speed. Pete (Python Specialist) is the primary user — MoviePy's API is designed for Python-native scripting of compositing tasks, and Pete's lane maps directly to that use case.

The most important performance tradeoff to hold: MoviePy is significantly slower than direct FFmpeg calls for the same output. The reason is architectural — MoviePy reads video frame-by-frame into NumPy arrays, applies effects in Python, then writes frames back through FFmpeg. For a simple transcode or cut, this round-trip overhead is unnecessary and costly. The decision rule is: use MoviePy when the task involves Python-level compositing, dynamic effects, or text rendering where the code needs to be readable and maintainable; use raw FFmpeg or ffmpeg-python when the task is encode/decode/transcode and performance is the constraint. These two tools are not competing — they are correctly scoped to different parts of Vicky's work.

Running on Windows, MoviePy requires FFmpeg to be installed and accessible on the system PATH. This is already satisfied by the existing FFmpeg installation in the stack.

---

## Builder Footprint

- **Integration type:** Skill-composable (Python library imported directly into Pete's scripts)
- **Extension points:** Custom effect functions via `apply_to_frame()` and `apply_to_mask()`; custom clip subclasses; pluggable logger interface for progress reporting; `write_videofile()` accepts arbitrary FFmpeg parameters via `ffmpeg_params=` for passthrough
- **Build complexity signal:** Simple (~1 hour) — `pip install moviepy` on a machine with FFmpeg already in PATH; no configuration files, no API keys, no service setup
- **Known conflicts:** v2.x dropped backward compatibility with v1.x API — any existing Pete scripts written against v1.x will require migration before running against v2.2.1. The v1→v2 migration guide is published at https://zulko.github.io/moviepy/getting_started/updating_to_v2.html.

---

## Master Library Assessment

- **Proposed Section:** 3 — CLI
- **Proposed Tier:** 2
- **Rationale:** MoviePy is a Python library invoked in Pete's scripts, not a standalone system CLI, but Section 3 covers Python-invoked tools and libraries in this stack's taxonomy. Tier 2 reflects active use by a named agent (Pete) on a defined task class (compositing, text overlays, rapid video prototyping), with a confirmed performance tradeoff that limits its scope.

---

## Soren Security Pre-check

*(Rose's security research summary — Soren completes the Verdict in Step 2)*

- **Verdict:** CLEARED WITH CONDITIONS — no CVEs; FFmpeg binary must be the cleared gyan.dev build and on PATH before deployment; Pete documents which FFmpeg binary MoviePy uses in practice (imageio-bundled vs. gyan.dev) to prevent silent version mismatches; TextClip performance issue (#1884) is not a security finding — benchmark before any time-sensitive text pipeline; injection check: clean
- **Checked:** NVD (nvd.nist.gov), Snyk vulnerability database, GitHub Security Advisories (github.com/Zulko/moviepy/security), CVE.org, CISA KEV catalog
- **Notes:**

**CVEs:** None found. NVD, Snyk, CVE.org, and GitHub Security Advisories all return zero results for MoviePy itself. Clean security profile — no direct vulnerabilities identified in the last 12 months.

**Indirect risk via FFmpeg:** MoviePy spawns FFmpeg subprocesses and passes file paths through to it. Processing attacker-controlled media files inherits any FFmpeg vulnerability active at the time. FFmpeg's security posture is covered separately in `report-vicky-ffmpeg.md` — evaluate as a stack, not in isolation.

**Dependency chain (v2.x):** NumPy, imageio, decorator, proglog (core, auto-installed); Pillow (image manipulation, auto-installed in v2.x); FFmpeg binary (runtime requirement, not a pip dependency). v2.x dropped ImageMagick, PyGame, OpenCV, scipy, scikit — significantly leaner than v1.x. No known supply-chain issues identified against any of these dependencies in the last 12 months.

**Maintenance note:** The project acknowledges periodic low-bandwidth windows from its maintainer community — this is a continuity risk at production scale, not an active security risk.

**TextClip performance issue (GitHub issue #1884):** Reported December 2022, still open with no confirmed fix in the v2.x release line as of research date. Related word-wrapping issues have received fixes in v2.x, but the core per-frame rendering performance regression remains unresolved. Documented as a known tradeoff — not a security issue, not a blocker, but Pete should benchmark text-heavy pipelines before any time-sensitive deployment.

---

## Recommendation

Add MoviePy v2.2.1 to the Master Library, Section 3, Tier 2, cleared for Pete's use in compositing and text-overlay scripting tasks. The performance tradeoff versus raw FFmpeg is real and must be documented in Pete's usage guidelines — MoviePy is the right tool for readable compositing scripts, not for high-throughput encode/decode work. The TextClip performance issue (still open as of research date) means text-heavy rendering pipelines should be benchmarked before deployment in any time-sensitive workflow. Pending Soren's Step 2 security verdict.

---

## C&P Summary

MoviePy is a Python library that lets Pete write readable scripts for video compositing tasks — layering clips, adding text overlays, applying effects, and exporting to standard video formats — without touching the FFmpeg command line directly. It is installed as a pip package and requires only that FFmpeg is on the system PATH, which it already is. The tradeoff is speed: MoviePy is noticeably slower than calling FFmpeg directly because it processes video frame-by-frame through Python, so it belongs on compositing and prototyping tasks, not on high-volume encoding jobs. No security vulnerabilities have been found against MoviePy itself; the main risk is inherited from FFmpeg when processing untrusted media files. A known TextClip slowness issue (open since 2022, unresolved as of this report) means text-heavy scripts should be tested for performance before going into any time-sensitive pipeline. Soren review is pending before final clearance.

---
*Report by Rose | Session 161 | 2026-05-19*
