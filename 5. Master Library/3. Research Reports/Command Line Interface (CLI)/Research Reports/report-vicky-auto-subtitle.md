# Resource Report: auto-subtitle

**URL:** https://github.com/m1guelpf/auto-subtitle
**Date Researched:** 2026-05-19
**Researched by:** Rose | Security pre-check: Soren (pending Step 2) | Report by: Rose

---

## What It Is

auto-subtitle is a lightweight Python CLI wrapper written by Miguel Piedrafita (m1guelpf) that chains OpenAI Whisper transcription and FFmpeg subtitle burning into a single command. It takes a video file as input, runs Whisper to generate a transcript, produces a `.srt` subtitle file, and optionally burns the subtitles directly into the output video — all in one step. The latest PyPI release is **v1.0.1**, published January 25, 2023. The package is MIT-licensed. It is not a standalone transcription or video-processing engine — it is purely a convenience orchestration wrapper around two tools (Whisper and FFmpeg) that are already cleared separately.

---

## What It Does

- Accepts a video file path and a `--model` flag specifying which Whisper model to use (e.g., `tiny`, `base`, `small`, `medium`, `large`)
- Runs Whisper transcription internally to produce a `.srt` subtitle file alongside the input video
- Burns subtitles into the output video via FFmpeg's `subtitles` filter, producing a new video file with hardcoded captions
- Supports `--output_dir` to direct output files to a specified folder
- Supports `--output_srt` flag to save the `.srt` file separately without burning
- Supports `--language` flag to pass a language hint to Whisper for faster/more accurate transcription
- Supports `--task` flag to switch between transcription and translation modes (mirrors Whisper's own task parameter)
- Exits cleanly on success; raises on FFmpeg or Whisper errors with non-zero exit

---

## Invocation Interface

- **Typical command pattern:** `auto_subtitle input.mp4 --model medium`
- **Output format:** Burned-subtitle video file (e.g., `input.mp4` → `output/input.mp4`) plus optional `.srt` file in the same output directory
- **Key structured output flags:** `--output_dir <path>` (output folder), `--output_srt` (save `.srt` alongside video), `--model <name>` (Whisper model size), `--language <code>` (language hint), `--task transcribe|translate`
- **Exit code behavior:** Exit 0 on success; non-zero on Whisper transcription failure or FFmpeg processing error; errors surface as Python exceptions rather than structured stderr messages
- **Stdin/stdout/stderr notes:** No stdin use. Progress output (Whisper loading, transcription progress) goes to stdout/stderr via tqdm and Whisper's own logging. Not designed for piped output — all results are written to files.

---

## Relevance to This Project *(as of 2026-05-19 — context may not carry to future projects)*

Vicky's workflow includes a one-step subtitle burn path: video in, subtitled video out, no manual two-step process. auto-subtitle is the clearest existing CLI wrapper for that exact pattern. The alternative is Vicky manually chaining Whisper transcription → `.srt` generation → FFmpeg subtitle filter herself, which is achievable but adds scripting overhead. auto-subtitle eliminates that overhead when the use case is straightforward.

Because both core dependencies — Whisper and FFmpeg — are already cleared in `report-vicky-whisper.md` and `report-vicky-ffmpeg.md`, auto-subtitle does not introduce any new execution surface for those engines. The risk assessment for this tool is narrowly scoped to the wrapper itself: its own code, its PyPI package integrity, and its maintenance posture.

The maintenance concern (see Soren section) is the primary flag. For a single-developer open-source CLI wrapper with no active maintainer, the practical risk for Vicky is functional rather than security-related: broken behavior with updated Whisper or FFmpeg versions, unmerged community bug fixes, and no upstream support channel. If auto-subtitle breaks in the field, Vicky will need a fallback path. That fallback is already available: direct Whisper + FFmpeg chaining via the cleared tools. Soren's verdict will determine whether the tool ships as primary or as a convenience-only option with the chained path as the default.

---

## Builder Footprint

- **Integration type:** CLI-invocable
- **Extension points:** None identified — the tool is a thin script with no plugin architecture or hook system
- **Build complexity signal:** Simple (~15–30 minutes) — single `pip install`, single command invocation, no configuration files or service setup required
- **Known conflicts:** `setup.py` lists only `openai-whisper` in `install_requires`; `ffmpeg-python` is used at runtime but **not formally declared** as a Python dependency. This means `pip install auto-subtitle` will not automatically install `ffmpeg-python`, creating a silent failure condition if `ffmpeg-python` is not already present. Because both are cleared separately for Vicky, this is mitigated in practice — but it is a packaging defect worth flagging.

---

## Master Library Assessment

- **Proposed Section:** 3 — CLI
- **Proposed Tier:** 2
- **Rationale:** Thin convenience wrapper with no independent execution engine; value is orchestration only. Tier 2 reflects its derivative nature — it adds no capability beyond what Whisper + FFmpeg already provide, and its usefulness is conditional on those Tier 1 tools being present.

---

## Soren Security Pre-check

*(Rose's security research summary — Soren completes the Verdict in Step 2)*

- **Verdict:** CLEARED WITH CONDITIONS — effectively abandoned (GitHub Issue #116 "DEAD ☠", June 2025, unacknowledged by maintainer; ~20 unreviewed PRs); no CVEs — attack surface is essentially zero independent of dependencies; fallback path (direct Whisper + FFmpeg chaining) is mandatory and must be documented before deployment; FFmpeg and Whisper/faster-whisper must be deployed first; package installs as a convenience shortcut only — not as a primary or sole subtitle burn mechanism; injection check: clean

- **Checked:** PyPI package listing and version history; GitHub repository activity, open issues, and pull request queue; CVE databases and security advisories (CISA, NVD) for auto-subtitle specifically; dependency declarations in `setup.py` and `requirements.txt`; MIT license status

- **Notes:**

**Maintenance status — FLAG: EFFECTIVELY ABANDONED.**

The repository has not received a commit from the maintainer in approximately two years as of mid-2025. GitHub Issue #116, titled "DEAD ☠", was opened June 27, 2025, by a community member noting the absence of commits and the accumulation of unreviewed pull requests. As of research date (2026-05-19), the issue remains open and unacknowledged by the maintainer. There are currently ~20 open pull requests — including bug fixes for known FFmpeg subtitle overlay errors — that have not been reviewed or merged. The latest PyPI release (v1.0.1) dates to January 25, 2023. There is no indication the maintainer intends to resume work on this project.

**CVEs:** No CVEs or security advisories specific to auto-subtitle were found in NVD, CISA, or the GitHub Advisory Database. Given the tool's narrow scope (a thin Python script), this is expected — the attack surface is essentially zero independent of its dependencies.

**Dependency chain:**
- `openai-whisper` — formally declared in `setup.py`; cleared separately (`report-vicky-whisper.md`)
- `ffmpeg-python` — used at runtime but **not declared** in `setup.py` (packaging defect); cleared separately (`report-vicky-ffmpeg-python.md`)
- `tqdm` — used for progress display; standard utility library, no known issues
- System-level `ffmpeg` binary — required; cleared separately (`report-vicky-ffmpeg.md`)
- Whisper transitive dependencies (torch, numpy) — covered by Whisper report

**License:** MIT confirmed on PyPI and GitHub.

**Packaging defect (functional risk, not a security issue):** The missing `ffmpeg-python` declaration in `setup.py` means a clean install may produce a runtime import error if `ffmpeg-python` is not already installed. Not a supply-chain or security risk, but a reliability flag Soren should note in the verdict context.

**No HIGH or CRITICAL security findings identified.** Primary risk is operational: the tool is unmaintained and may silently break as Whisper and FFmpeg release new versions with incompatible interfaces.

---

## Recommendation

Clear for use as a convenience wrapper with a mandatory fallback path documented for Vicky: if auto-subtitle breaks due to dependency drift or FFmpeg/Whisper API changes, Vicky falls back to direct Whisper + FFmpeg chaining using the two already-cleared tools. Do not deploy as Vicky's sole subtitle burn mechanism — flag it as convenience-tier, not primary-tier. Soren should confirm the verdict and specify whether any version-pinning is required given the unmaintained state.

---

## C&P Summary

auto-subtitle is a small Python command-line tool that takes a video file, runs it through Whisper to generate subtitles, and burns those subtitles into the output video — all in one command. It is useful for Vicky because it removes the need to run Whisper and FFmpeg as two separate manual steps. The tool itself is MIT-licensed, has no known security vulnerabilities, and its two core dependencies (Whisper and FFmpeg) are already cleared. The main concern is that the original developer stopped maintaining the project around 2023, has not responded to bug reports or pull requests since, and a community issue filed in 2025 formally flagged it as abandoned. This means the tool may stop working as Whisper or FFmpeg release updates, and there is no one fixing it upstream. The recommendation is to use it as a convenience shortcut for Vicky's workflow, but always have the direct Whisper + FFmpeg chain available as a fallback so Vicky is never blocked if auto-subtitle breaks.

---
*Report by Rose | Session 161 | 2026-05-19*
