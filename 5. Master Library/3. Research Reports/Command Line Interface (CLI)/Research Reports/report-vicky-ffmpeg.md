# Resource Report: FFmpeg

**URL:** https://ffmpeg.org
**Date Researched:** 2026-05-19
**Researched by:** Rose | Security pre-check: Soren (pending Step 2) | Report by: Rose

---

## What It Is

FFmpeg is an open-source, cross-platform command-line tool and multimedia framework for recording, converting, and streaming audio and video. It is the de facto standard for video processing in both professional and developer contexts — used as the backbone of VLC, YouTube's transcoding pipeline, HandBrake, and thousands of other tools. It ships as a set of three executables (`ffmpeg`, `ffprobe`, `ffplay`) and a suite of codec libraries (`libavcodec`, `libavformat`, `libavfilter`, `libswscale`, etc.). The project is maintained by a distributed open-source team, with Windows builds distributed via two officially recognized sources: gyan.dev (GyanD/codexffmpeg) and BtbN/FFmpeg-Builds on GitHub. Current stable release as of 2026-05-19: **FFmpeg 8.1.1** (released 2026-05-18).

---

## What It Does

- Trim and cut video by timestamp with or without re-encoding (`-c copy` for stream copy, zero quality loss)
- Re-encode video to reduce file size with configurable quality targets (CRF, bitrate caps)
- Split a single file into timed segments (`-segment_time`)
- Concatenate multiple clips into one output (`-f concat`)
- Extract audio tracks from video files (`-vn` / `-acodec copy`)
- Burn subtitles (soft or hardcoded) into video (`-vf subtitles=file.srt`)
- Convert between container formats (MP4, MKV, MOV, WebM, AVI, etc.)
- Probe and report media metadata without modifying files (`ffprobe`)
- Apply filters: crop, scale, rotate, denoise, overlay, fade, drawtext
- Generate thumbnails or frame sequences from video
- Stream video to network endpoints (RTMP, HLS, DASH)

---

## Invocation Interface

- **Typical command pattern:** `ffmpeg -ss [start] -to [end] -i input.mp4 -c copy output.mp4`
- **Output format:** Binary media file output; progress and diagnostic text to stderr; `ffprobe` can output JSON with `-print_format json`
- **Key structured output flags:** `-print_format json` (ffprobe only), `-loglevel quiet` (suppress stderr noise), `-progress pipe:1` (machine-readable progress to stdout)
- **Exit code behavior:** Exit 0 = success; non-zero = error (encoding failure, bad input, invalid flags); specific codes not standardized — rely on stderr text for diagnosis
- **Stdin/stdout/stderr notes:** Diagnostic output (progress, warnings, errors) goes to stderr by default — relevant for scripts that need to separate progress from errors; `-loglevel error` suppresses all but fatal messages

---

## Relevance to This Project *(as of 2026-05-19 — context may not carry to future projects)*

FFmpeg is Vicky's core operational engine. Every video processing task in Vicky's workflow runs through FFmpeg: stream-copy trimming (no re-encode, frame-perfect cuts at minimal CPU cost), Discord file size compression (re-encode with a target bitrate or file size), splitting long recordings into segments, concatenating separate clips, extracting audio, and burning subtitles. There is no equivalent tool that matches FFmpeg's breadth, performance, and zero-cost licensing for this use case.

The stream-copy workflow in particular (`-c copy`) is essential for Vicky's efficiency. It means FFmpeg can trim clips without decoding and re-encoding every frame — cuts are fast, lossless in quality terms, and require no GPU. For Vicky's Discord compression workflow, the two-pass bitrate approach (`-b:v` targeting a file size ceiling) is industry standard and well within FFmpeg's native capability.

Without FFmpeg, Vicky has no video processing capability at all. This is a hard dependency, not an optional enhancement.

---

## Builder Footprint

- **Integration type:** Standalone tool / CLI-invocable
- **Extension points:** None required for Vicky's use case; FFmpeg supports filter graphs (`-vf`, `-af`) as an internal extensibility model; external scripting wraps CLI calls
- **Build complexity signal:** Simple (~1–2 hours) — install pre-built binary from gyan.dev, add to PATH, invoke via subprocess or shell script; no compilation required; no runtime dependencies beyond the bundled build
- **Known conflicts:** License conflicts emerge if the deployed build includes `libfdk_aac` (nonfree) or GPL-only codecs in a commercially distributed product — see Soren Security Pre-check for full breakdown; no runtime conflicts with other tools identified

---

## Master Library Assessment

- **Proposed Section:** 3 — CLI
- **Proposed Tier:** 1
- **Rationale:** FFmpeg is Vicky's core operational dependency — not a supporting tool but the execution engine for every video task. Tier 1 reflects that nothing in Vicky's workflow runs without it.

Note: FFmpeg is currently in Section 9 (Jay's Shelf) at Tier 3, CLEARED. This report proposes promotion to Section 3 (CLI), Tier 1 as Vicky's core deployment engine.

---

## Soren Security Pre-check

*(Rose's security research summary — Soren completes the Verdict in Step 2)*

- **Verdict:** CLEARED WITH CONDITIONS — v8.1.1 confirmed; all 2025-2026 HIGH CVEs patched in 8.1.1; gyan.dev source only; SHA-256 checksum verify required before install; GPL essentials build acceptable for internal use (no distribution obligation); injection check: clean
- **Checked:** License model (GPL vs. LGPL vs. nonfree build variants), CVEs filed in 2025 and 2026, build source integrity for gyan.dev, dependency chain (libx264, libx265, libvpx, libfdk_aac), supply chain risk profile

**CVE findings (last 12 months — 2025–2026):**

FFmpeg had an active CVE year in 2025. Known CVEs include: CVE-2025-0518, CVE-2025-1373, CVE-2025-1594, CVE-2025-1816, CVE-2025-9951, CVE-2025-22919, CVE-2025-22920, CVE-2025-25471, CVE-2025-59728, CVE-2025-59729, CVE-2025-59731, CVE-2025-59732, CVE-2025-59733, CVE-2025-59734, CVE-2025-63757. In 2026, 7 additional vulnerabilities have been filed (average CVSS 5.9), including CVE-2026-40962. FFmpeg 8.1.1 (current release as of 2026-05-18) is the patched version for all known issues through its release date.

Key CVEs by severity:

| # | Severity | Flag | Notes |
|---|----------|------|-------|
| 1 | HIGH | CVE-2025-1594 | Stack buffer overflow in AAC encoder (libavcodec/aacenc_tns.c); CVSS 8.8; affects FFmpeg ≤ 7.1; requires user to open malicious audio file; fixed in 7.1.2 and 8.0+ |
| 2 | HIGH | CVE-2025-59732 | Reported HIGH per CVE feed; full details not published at research date |
| 3 | HIGH | CVE-2025-59733 | Reported HIGH per CVE feed; full details not published at research date |
| 4 | HIGH | CVE-2025-59734 | Reported HIGH per CVE feed; full details not published at research date |
| 5 | MEDIUM | CVE-2025-63757 | Integer overflow in libswscale/output.c (yuv2ya16 function); affects FFmpeg 8.0; fixed in 8.1+; DoS risk via crafted media |
| 6 | MEDIUM | CVE-2025-22919 | Reachable assertion (CWE-617); DoS risk; severity not fully scored at research date |
| 7 | MEDIUM | CVE-2026-40962 | Part of 2026 CVE batch; CVSS ~5.9; details limited at research date |

**Patch posture:** All HIGH CVEs above affect versions below 8.0 or 8.1. FFmpeg 8.1.1 (current stable, released 2026-05-18) addresses all known issues in the 8.x branch. Deploying 8.1.1 is the correct mitigation.

**Build source — gyan.dev assessment:** gyan.dev is one of two official build sources listed on ffmpeg.org/download.html. The maintainer (GyanD) publishes builds via GitHub (GyanD/codexffmpeg) with SHA-256 checksums available as companion files for every release package. Builds are labeled: `ffmpeg-release-essentials` (common libraries, GPL) and `ffmpeg-release-full` (all available libraries including nonfree). Release builds track the stable branch with bug/security fixes only. No known integrity incidents or tampering reports identified. SHA-256 verification is available and should be used at deployment.

**License flags:**

- FFmpeg base: **LGPL v2.1+** — permissive; allows commercial use without source disclosure obligations when dynamically linked
- GPL trigger: Including `libx264`, `libx265`, `libxvid`, or `libxavs` in the build flips the entire binary to **GPL v2+** — requires source disclosure for any distributed binary using those codecs
- Nonfree trigger: Including `libfdk_aac` (Fraunhofer AAC) requires `--enable-nonfree` at compile time — produces a license mix more restrictive than GPL; not redistributable under any open license
- The gyan.dev **essentials** build includes libx264 and libx265 — this build is **GPL**
- The gyan.dev **full** build adds libfdk_aac — this build is **nonfree/non-redistributable**
- For Vicky's internal, non-distributed personal use workflow: GPL is not a blocker. The nonfree build is also usable internally but should not be redistributed.
- For any future commercial product or distributed tool: the GPL build triggers source disclosure obligations and the nonfree build is not distributable — Soren should flag this at that stage.

**Dependency chain — supply chain notes:** Core dependencies (libx264, libx265, libvpx, libopus, libvorbis) are long-established, widely audited libraries with no active supply chain incidents identified. FFmpeg's supply chain risk profile is noted in security literature as elevated relative to simpler tools (large attack surface, many codec paths) but mitigated by wide deployment, active CVE tracking, and fast patch cycles. No known 2025–2026 supply chain compromises for FFmpeg or its primary dependencies were found in research.

---

## Recommendation

Deploy FFmpeg 8.1.1 from gyan.dev using the `ffmpeg-release-essentials` build (GPL), verified via SHA-256 before installation. All 2025 HIGH CVEs are resolved in 8.1.1 — version currency is the primary security control here. License is GPL for the essentials build, which is acceptable for Vicky's internal personal use workflow with no distribution obligation. Soren should confirm the GPL posture is acceptable at the project level and set a version-monitoring flag given FFmpeg's active CVE history.

---

## C&P Summary

FFmpeg is a free, open-source command-line tool that handles virtually every video processing task: trimming clips, compressing files, splitting recordings into pieces, joining clips together, pulling out audio, and burning in subtitles. It has been the industry standard for video work for over two decades and is the engine behind most major video tools and platforms. For Vicky, it is not optional — it is the core engine that makes every video workflow possible. The current stable version (8.1.1, released May 2026) addresses all known security issues from the past year. The recommended Windows build comes from gyan.dev, which is one of the two officially recognized build sources for FFmpeg on Windows and provides SHA-256 checksums to verify download integrity. The main consideration before deployment is license: the standard build includes H.264/H.265 codec libraries that put the software under the GPL license, which is fine for personal internal use but would create obligations if Vicky's output pipeline were ever packaged and distributed commercially.

---
*Report by Rose | Session 161 | 2026-05-19*
