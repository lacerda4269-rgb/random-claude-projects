# Resource Report: Manim Community Edition (ManimCE)

**URL:** https://github.com/ManimCommunity/manim
**PyPI:** https://pypi.org/project/manim/
**Docs:** https://docs.manim.community/en/stable/
**Date Researched:** 2026-06-03
**Researched by:** Rose (Researcher Agent) | Security pre-check: Soren (CLEARED WITH CONDITIONS + LaTeX HOLD — Session 214) | Report by: Sophia (COO)
**Already in Master Library?** No — new entry, Session 213

> **Repo note:** Two Manim repos exist — `3b1b/manim` (Grant Sanderson's personal repo, not pip-installable) and `ManimCommunity/manim` (this report — community fork, actively maintained, pip-installable, documented). Always use the community edition.

---

## C&P Summary

Manim Community Edition is an open-source Python framework for creating programmatic mathematical and educational animations, originally forked from 3Blue1Brown's personal codebase and now maintained by 100+ community contributors. Write Python classes that define scenes, objects, and animations — Manim renders them to MP4, GIF, or WebM using Cairo, FFmpeg, and OpenGL. Current stable version is v0.20.1 (February 2026); requires Python ≥ 3.11. MIT licensed, 38,794 stars, updated today. Free, no API keys, no external services — runs entirely locally. For Vicky, this is the code-driven animation engine for explainer content, motion graphics, title sequences, and animated educational or data visualization video — no GUI, pure Python, fully agentic. **System dependencies required:** FFmpeg and a LaTeX distribution (MiKTeX or TeX Live) must be installed at the OS level.

---

## What It Is

Manim Community Edition is a Python-based animation engine purpose-built for mathematical and educational video production. It is the community-maintained successor to Grant Sanderson's (3Blue1Brown) personal `3b1b/manim` repo, forked in 2020 to provide stable pip releases, proper documentation, and an open contribution process. As of June 2026 it has 38,794 stars and remains the de facto standard for code-driven math and explainer animation. Every element — geometric shapes, equations, text, graphs, 3D objects — is a Python object. Every animation — creation, transformation, fade, rotation — is a method call. The output is a standard video file.

---

## What It Does

- **Scene-based animation authoring** — Python classes inheriting from `Scene`; each class renders to a video clip
- **Mathematical object library** — shapes, axes, number planes, graphs, matrices, LaTeX equations, arrows, vectors, function plots
- **Animation primitives** — `Create`, `Write`, `FadeIn`, `FadeOut`, `Transform`, `Rotate`, `Shift`, `Scale`, `ReplacementTransform` — fully composable
- **3D scene support** — `ThreeDScene` and `ThreeDCamera` for 3D objects, camera movement, surface rendering
- **LaTeX / MathTex rendering** — native `MathTex` and `Tex` classes render LaTeX equations to SVG, then animate them
- **SVG and image import** — load external SVG assets and PNG/JPEG images as scene objects
- **Audio sync** — `add_sound()` attaches audio files to scenes
- **Multi-format export** — MP4 (default), GIF, WebM, or PNG sequences; resolution and frame rate configurable
- **Quality flags** — `-ql` (low, fast iteration), `-qm` (medium), `-qh` (high, 1080p), `-qk` (4K)
- **Plugin system** — community plugins extend functionality (e.g., `manim-physics`, `manim-slides`)
- **Jupyter/notebook integration** — optional inline display in JupyterLab

---

## Repository Metrics (June 2026)

| Metric | Value |
|---|---|
| **Stars** | 38,869 |
| **Forks** | 2,893 |
| **Open Issues** | 549 |
| **Contributors** | 100+ |
| **Latest Version** | v0.20.1 (released 2026-02-27) |
| **Requires Python** | ≥ 3.11 |
| **Language** | Python |
| **License** | MIT |
| **Last Updated** | 2026-06-03 (report date); last push 2026-06-03 confirmed |
| **Release Cadence** | ~4 releases/year |

---

## How It Works

An agent writes a Python file containing one or more `Scene` subclasses. Each `Scene` defines a `construct()` method where objects are created and animated via `self.play()` and `self.add()` calls. When `manim render scene.py SceneName` is executed:

1. Manim instantiates the scene class and runs `construct()`
2. Frames are captured using **Cairo** (2D) or **ModernGL/OpenGL** (3D)
3. LaTeX content is compiled via the local LaTeX distribution and converted to SVG
4. FFmpeg encodes frames into the output video file
5. Output is written to `media/videos/scene/[quality]/SceneName.mp4`

The pipeline is deterministic — same script always produces the same output.

---

## Key Dependencies

| Dependency | Role |
|---|---|
| **FFmpeg** (system-level) | Video encoding — must be installed separately, not bundled |
| **LaTeX distribution** (system-level) | MiKTeX (Windows) or TeX Live (Linux/Mac) — required for equation rendering; 4–8 GB install |
| `pycairo ≥ 1.14` | 2D vector rendering |
| `moderngl ≥ 5.7` | OpenGL-based 3D rendering |
| `numpy ≥ 2.1` | Array math and coordinate transforms |
| `scipy ≥ 1.13` | Numerical methods |
| `pillow ≥ 11.0` | Image handling |
| `av ≥ 15.0` | Audio/video frame handling |
| `pydub ≥ 0.22` | Audio manipulation |
| `manimpango ≥ 0.6.1` | Text/font rendering |
| `networkx ≥ 2.6` | Graph data structures |

---

## Caveats and Known Issues

- **Rendering is slow** — a 60-second 1080p scene with heavy LaTeX can take 10–30+ minutes on CPU; 4K renders are substantially longer; no built-in GPU acceleration for 2D (Cairo is CPU-bound)
- **System dependency complexity** — FFmpeg must be in PATH; LaTeX distribution is 4–8 GB; Cairo/pycairo on Windows can require GTK runtime or manual DLL placement
- **Headless server** — ModernGL 3D rendering requires OpenGL 3.3+; on Linux headless servers, use Xvfb virtual display
- **Learning curve** — expressive API but not shallow; requires understanding coordinate systems, animation timing, object lifecycle, and updaters; iteration loop is write → render → review → adjust → re-render
- **LaTeX knowledge required** for equation-heavy content
- **549 open issues** — healthy level for an active library; core compositing and audio edge cases exist but are not blockers for typical use

---

## Relevance to This Project

**Code-driven animation engine for Vicky the Videographer — Movie Studio initiative.**

Manim gives Vicky the ability to produce animated explainer and educational video entirely in Python code, with zero GUI dependency:

- **Explainer animations** — trading concepts, financial models, statistics, probability — Manim renders publication-quality animated visualizations from code
- **Title sequences and motion graphics** — `Write`, `FadeIn`, and geometric transforms produce clean animated title cards, lower-thirds, and data callouts
- **Code-to-video pipeline** — Vicky receives a brief, writes a Manim scene script, renders it via CLI, hands back an MP4. Fully agentic.
- **Composability** — Manim output is standard MP4/GIF; slots into any downstream video editing pipeline (e.g., MoviePy for final assembly)

Main constraint: rendering time and system dependencies. Any environment Vicky runs in needs FFmpeg and a LaTeX distribution pre-installed.

---

## Master Library Assessment

| Field | Value |
|---|---|
| **Proposed Section** | CLI Tools |
| **Proposed Tier** | 2 — High Value |
| **Rationale** | Best-in-class for code-driven mathematical and explainer animation. 38K+ stars, MIT, active maintenance, clear CLI path. Tier 2 (not Tier 1) because this serves a specialized use case — programmatic animation — rather than general video assembly. Promote to Tier 1 if Vicky's scope confirms animation as a core output type. |

---

## Claude Code Compatibility

**Path: CLI via Bash tool — no MCP required.**

```python
# my_scene.py — agent writes this via Write tool
from manim import *

class TitleCard(Scene):
    def construct(self):
        title = Text("My Video Title", font_size=48)
        self.play(Write(title))
        self.wait(2)
        self.play(FadeOut(title))
```

```bash
# Install
pip install manim

# Render at low quality for fast iteration
manim render my_scene.py TitleCard -ql

# Render at high quality for final output
manim render my_scene.py TitleCard -qh

# List all scenes in a file
manim render my_scene.py --list_classes

# Render to GIF
manim render my_scene.py TitleCard --format gif
```

Output lands at `media/videos/my_scene/[quality]/TitleCard.mp4`.

**Infrastructure requirement:** Confirm FFmpeg is installed and in PATH before Vicky's first render task. LaTeX distribution needed only if `MathTex`/`Tex` objects are used.

---

## Soren Security Pre-check

- **Re-reviewed 2026-06-08 — verdict confirmed. CLEARED WITH CONDITIONS + LaTeX HOLD stands.** Rose's freshness sweep: stars 38,869 (was 38,794), v0.20.1 (February 2026 — no new release), last push 2026-06-03 — actively maintained. No new CVEs or security disclosures found. All three conditions remain active (pillow ≥ 12.2.0, urllib3 ≥ 2.7.0, exclude Jupyter packages). LaTeX HOLD unchanged — LaTeX distribution (MiKTeX/TeX Live) has not been cleared and must not be used until cleared through the full pipeline. No action required on the library entry itself.

- **Status:** CLEARED WITH CONDITIONS + DEPENDENCY HOLD (Soren, Session 214 — 2026-06-04)
- **Scanned by:** Trivy v0.71.0 + Gitleaks v8.30.1
- **Manual read:** Pass — no prompt injection signals detected
- **Trivy:** 0 CRITICAL, 13 HIGH — majority in Jupyter/notebook dev tooling (not rendering pipeline); pillow and urllib3 are the rendering-path findings with available fixes
- **Gitleaks:** Clean — 11.5 MB scanned, 0 secrets found
- **Conditions:**
  1. Pin `pillow` ≥ 12.2.0 and `urllib3` ≥ 2.7.0 before deployment
  2. Exclude Jupyter/notebook packages for CLI-only use — eliminates 9 of 13 HIGH findings
  3. FFmpeg clearance carries from Session 161 (v8.1.1, gyan.dev build, internal use only)
- **Dependency HOLD:** LaTeX distribution (MiKTeX or TeX Live) is required for ManimCE's LaTeX text rendering feature and has not been cleared. LaTeX features must not be used until the distribution goes through the full clearance pipeline. CLI-only animation rendering (no LaTeX) is unaffected.

---

*Report by Sophia (COO) | Research by Rose | Session 213, 2026-06-03*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
