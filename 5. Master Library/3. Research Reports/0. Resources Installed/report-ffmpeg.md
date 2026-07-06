# Resource Report: ffmpeg

**URL:** https://ffmpeg.org / https://github.com/BtbN/FFmpeg-Builds (Windows builds)
**Date Documented:** 2026-06-11
**Documented by:** Sophia (COO) | Soren pre-check: ⬜ PENDING — next COHK | Report by: Sophia
**Already in Master Library?** Partial — entry exists in master list (#12) but no detail section or ML record

---

## What It Is

ffmpeg is the gold-standard open-source CLI for video and audio processing. It is used by virtually every major media platform, streaming service, and production pipeline in the industry. It handles transcoding, filtering, compositing, encoding, decoding, format conversion, and streaming — all from a single command-line binary. No GUI, no account, no API key required.

## What It Does

- Transcode video and audio between virtually any format (MP4, MOV, MKV, WebM, MP3, AAC, etc.)
- Apply filter graphs: xfade transitions, overlay compositing, color correction, scaling, cropping, watermarking
- Build final video assembly pipelines — concat, trim, merge audio/video tracks
- Upscale and resize video frames (nearest-neighbor, Lanczos, bilinear)
- Extract audio from video, or mux audio into video
- Generate thumbnails and image sequences from video
- Stream output to RTMP, HLS, or file
- Encode for web delivery (H.264/H.265/AV1 with quality controls)
- Full filter graph API for complex multi-input compositing
- Ships as a static binary — no runtime dependencies, no install script
- Version: 8.1.1 (full build — includes all optional codecs and filters)
- License: LGPL 2.1+ (core) / GPL 2+ (when built with GPL components — full build uses GPL)
- Maintained by the FFmpeg project (community-driven, ~30 years active development)

## Installation & Location

- **Install type:** CLI static binary (Windows full build)
- **Build source:** BtbN/FFmpeg-Builds (GitHub) — `ffmpeg-master-latest-win64-gpl-shared` full build
- **Version:** 8.1.1
- **Binary location:** `C:\ClaudeTools\ffmpeg\ffmpeg-8.1.1-full_build\bin\ffmpeg.exe`
- **Full build path:** `C:\ClaudeTools\ffmpeg\ffmpeg-8.1.1-full_build\`
- **PATH status:** Confirm at next COHK — directory may not be on system PATH; call via full path or add `C:\ClaudeTools\ffmpeg\ffmpeg-8.1.1-full_build\bin\` to PATH
- **Session installed:** Sessions 221–225 (2026-06-05 through 2026-06-06, during MKT 311 video production)
- **Install method:** Manual download and extraction — no installer

## Relevance to This Project

ffmpeg is Vicky's core production pipeline tool for all video deliverables. Used first in MKT 311 (Session 221–225) for: final video assembly (concat), filter graph transitions (xfade), audio/video muxing, overlay compositing, and format output for submission. Any future video production task — Remotion render post-processing, MoneyPrinterTurbo output handling, or client deliverable assembly — routes through ffmpeg. It is the lowest-level and most capable video manipulation layer in the stack.

## Master Library Assessment

- **Proposed Section:** 5 — CLIs
- **Proposed Tier:** 1
- **Rationale:** Static binary CLI — Section 5 fits. Tier 1 because it is Vicky's primary production tool and is already in active use on delivered work.
- **Sub-filing:** Route to Vicky's ML section when Vicky's ML record is established (pending note already in master list Open Items)

## Soren Security Pre-check

- **Verdict:** ⬜ PENDING — flag for next COHK
- **Note:** ffmpeg was installed during MKT 311 production (Sessions 221–225) without a formal Soren review pass — noted in the master list Open Items since Session 227. Pre-check factors: GPL/LGPL license, static binary (no install script, no network calls at runtime), extremely well-established project (30+ years, industry-standard), no known malware incidents, BtbN/FFmpeg-Builds is the canonical Windows binary source. Risk profile is very low; formal clearance still required per process.

## Recommendation

File in Section 5 (CLIs) at Tier 1, sub-filed to Vicky's ML section when her record is established. Queue Soren formal clearance at next COHK — this has been pending since Session 227 and should be prioritized given active production use. Confirm PATH configuration at same COHK.

---
*Report by Sophia | Session 242 | 2026-06-11*

---

## C&P Summary

ffmpeg (v8.1.1 full build, GPL) is the industry-standard CLI for video and audio processing — transcoding, filter graphs, compositing, format conversion, streaming, and final assembly. Static binary installed at `C:\ClaudeTools\ffmpeg\ffmpeg-8.1.1-full_build\bin\ffmpeg.exe` during MKT 311 production (Sessions 221–225). Vicky's primary production tool: used for xfade transitions, audio/video muxing, overlay compositing, and final video delivery in MKT 311. Any future video work (Remotion post-processing, MoneyPrinterTurbo output, client deliverables) routes through ffmpeg. No account, no API key, no runtime dependencies. Soren clearance has been pending since Session 227 — queued for next COHK. PATH configuration should be confirmed at the same time.

---

## Report Version Log

| Version | Date | What Changed |
|---------|------|--------------|

---
*Consolidated S264: install-folder copy was the base (fuller — had Installation & Location); reattached the **Report Version Log** from the category copy. Category copy superseded. ML Stage 1.*
