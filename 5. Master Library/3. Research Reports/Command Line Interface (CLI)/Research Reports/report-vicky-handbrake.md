# Resource Report: HandBrake

**URL:** https://handbrake.fr
**Date Researched:** 2026-05-19
**Researched by:** Rose | Security pre-check: Soren (pending Step 2) | Report by: Rose

---

## What It Is

HandBrake is a free, open-source video transcoder available for Windows, macOS, and Linux. Originally released in 2003, it has been actively maintained for over 20 years and is widely regarded as the most accessible desktop tool for video compression and format conversion. It wraps a stack of professional-grade encoding libraries — including FFmpeg, x264, x265, SVT-AV1, and libvpx — behind a graphical interface that makes codec selection, resolution, bitrate, and quality settings approachable without requiring command-line fluency. A companion CLI (HandBrakeCLI) ships alongside the GUI and exposes the same encoding engine for scripted or automated workflows. The current stable release is **version 1.11.1** (released March 22, 2026), which requires Microsoft .NET Desktop Runtime 10.0.x on Windows.

---

## What It Does

- Transcodes video between a wide range of input formats and output containers (MP4, MKV, MOV, WebM)
- Encodes using H.264 (x264), H.265/HEVC (x265), VP8/VP9 (libvpx), AV1 (SVT-AV1), ProRes, and DNxHR
- Provides GPU-accelerated encoding via Intel QSV, NVIDIA NVENC, and AMD VCE on supported hardware
- Applies resolution scaling, frame rate conversion, and cropping through a visual settings panel
- Offers quality-based encoding (constant quality / CRF) or target-bitrate encoding
- Includes preset library with named profiles (e.g., Fast 1080p30, HQ 720p30 Surround) for common use cases
- Provides a live preview window to inspect encoding output before committing a full encode
- Supports subtitle tracks (SRT, SSA/ASS, PGS burn-in) and audio stream remuxing or re-encoding
- Queues multiple jobs for batch processing
- Outputs file size estimates to help users target a specific upload limit (e.g., Discord's 10 MB cap)
- HandBrakeCLI enables the same encoding pipeline from scripts, automation tools, or agents without a GUI session

---

## Invocation Interface

- **Typical command pattern:**
  `HandBrakeCLI -i input.mp4 -o output.mp4 --encoder x265 --quality 28 --width 1280 --height 720 --rate 30 --cfr`
  For target file size: `HandBrakeCLI -i input.mp4 -o output.mp4 --encoder x265 --vb 800 --two-pass --turbo --width 1280 --height 720`
- **Output format:** Media file (MP4, MKV, MOV, WebM) — binary, not text
- **Key structured output flags:**
  - `--encoder` — codec selection (x264, x265, svt_av1, vp9, etc.)
  - `--quality` — CRF-style constant quality value (lower = higher quality / larger file)
  - `--vb` — target video bitrate in kbps
  - `--width` / `--height` — output resolution
  - `--rate` / `--cfr` — frame rate and constant frame rate lock
  - `--two-pass` — two-pass bitrate encoding for more accurate file size targeting
  - `--preset` — named preset (e.g., `HQ 720p30 Surround`)
  - `--json` — outputs encode progress and metadata as JSON to stdout (useful for scripted monitoring)
- **Exit code behavior:** Returns 0 on success; non-zero on error. Error messages written to stderr.
- **Stdin/stdout/stderr notes:** `--json` flag sends structured progress data to stdout during encode; human-readable progress also available. Errors and warnings go to stderr. Output file path is always specified explicitly via `-o` — HandBrakeCLI does not write to stdout.

---

## Relevance to This Project *(as of 2026-05-19 — context may not carry to future projects)*

Vicky's primary compression task is preparing video files to meet Discord's 10 MB upload limit, where visual control over quality tradeoffs — codec, resolution, bitrate — is more practical than scripting. HandBrake's GUI is the purpose-built tool for this: it exposes every relevant setting in a single window, shows a live preview, and provides real-time file size estimates. For Vicky, this means she can iterate on settings visually before committing an encode, rather than running multiple FFmpeg CLI commands and inspecting outputs manually. The H.265 codec, 720p resolution, and 30fps target that define her Discord compression workflow map directly to HandBrake's built-in `HQ 720p30 Surround` preset family, which reduces the decision surface further.

HandBrake is not a replacement for Pete's FFmpeg scripting capability — it complements it. Pete handles automation, batch pipeline work, and cases where encoding is one step in a larger programmatic workflow. HandBrake handles cases where Vicky needs to visually tune a specific file quickly, without requiring Pete to write a one-off script. The two tools share the same underlying encoding libraries (both use x264, x265, and libvpx), so output quality at equivalent settings is comparable.

HandBrakeCLI also opens a future integration path: if Vicky's compression workflow becomes repetitive enough to warrant automation, Pete can invoke HandBrakeCLI directly from a script with known-good flags derived from Vicky's tested GUI settings — no translation required.

---

## Builder Footprint

- **Integration type:** Standalone tool (GUI primary) / CLI-invocable (HandBrakeCLI for scripted use)
- **Extension points:** HandBrakeCLI flags expose the full encoding engine; `--json` output enables progress monitoring from a parent script; presets can be exported and imported as JSON files for consistent re-use across machines
- **Build complexity signal:** Simple (~15–30 minutes) — Windows installer from handbrake.fr, verify checksum, install .NET Desktop Runtime 10.0.x if not already present, confirm HandBrakeCLI is on PATH if CLI invocation is needed
- **Known conflicts:** Windows Update KB5066835 (released October 2025 for Windows 11) caused HandBrake to freeze on encode start; resolved in HandBrake 1.11.1. No conflicts with FFmpeg coexistence.

---

## Master Library Assessment

- **Proposed Section:** 8 — Alternative Tools & Notable Ecosystem
- **Proposed Tier:** 2
- **Rationale:** HandBrake is a mature, purpose-built GUI tool that fills a real gap in Vicky's workflow — visual compression control — without duplicating Pete's FFmpeg scripting lane. Tier 2 reflects active use within an agent's workflow rather than a peripheral reference tool.

---

## Soren Security Pre-check

*(Rose's security research summary — Soren completes the Verdict in Step 2)*

- **Verdict:** CLEARED — version updated from v1.10.2 (Session 105) to v1.11.1 (re-reviewed); no 2025-2026 CVEs; 2017 mirror compromise was macOS-only and has not recurred; handbrake.fr is the sole approved source; SHA-256 verify before install; .NET Desktop Runtime 10.0.x required on Windows; bundled library stack (FFmpeg 8.0.1, x265, SVT-AV1, libvpx) reviewed — no unpatched HIGH/CRITICAL upstream CVEs identified at research date; injection check: clean
- **Checked:** CVE databases (NVD, CVEdetails) for 2025–2026 HandBrake-specific entries; GitHub Security Advisories page (github.com/HandBrake/HandBrake/security); historical incident record (2017 mirror compromise); official download source integrity; bundled dependency versions; Linux Foundation OpenSSF Security Insights page
- **Notes:**

**CVEs (2025–2026):** No HandBrake-specific CVEs were identified in the 2025–2026 window across NVD, CVEdetails, and the project's GitHub Security Advisories page. Assessment: no known direct CVEs at time of research.

**Bundled dependency exposure:** HandBrake bundles its own versions of encoding libraries rather than relying on system-installed copies. As of version 1.11.1, confirmed bundled versions include: FFmpeg 8.0.1, x265 r13309, SVT-AV1 4.0.1, libdav1d 1.5.3, libvpx 1.16.0, and oneVPL 2.16.0. x264 is also bundled (specific revision not surfaced in research). Vulnerabilities in any of these upstream libraries would affect HandBrake builds until the project updates its bundled versions — this is a standing dependency-chain risk common to all applications that bundle encoding libraries. No HIGH or CRITICAL upstream library CVEs were identified as specifically unpatched in HandBrake's current bundled versions during this research pass, but Soren should confirm.

**Download source integrity:** handbrake.fr is confirmed as the sole official download source. GitHub Releases and Flathub (Linux) are the only other sanctioned sources. The project publishes SHA-256 checksums at handbrake.fr/checksums.php and mirrors them on the GitHub wiki. Third-party sites (Softonic, FileHorse, SourceForge mirrors) are not endorsed and should be avoided.

**2017 mirror compromise — recurrence check:** The 2017 incident involved a compromised secondary download mirror (download.handbrake.fr) that served a macOS installer trojanized with the Proton backdoor for approximately 72 hours (May 2–6, 2017). The team detected and removed it within days, shut down the mirror, and issued a public advisory with checksum verification instructions. No recurrence of a similar mirror or distribution compromise has been identified in 2025–2026. The incident was macOS-specific; this deployment is Windows. The secondary mirror infrastructure involved in the attack has not been restored.

**Windows compatibility note:** Windows Update KB5066835 (October 2025) caused a freeze-on-encode bug due to interference with HandBrake's internal worker-process communication. This is a compatibility issue, not a security vulnerability. It is resolved in HandBrake 1.11.1.

**License:** GPL v2. fdk-aac is excluded from the default build due to license incompatibility — not relevant to Vicky's workflow.

**Overall Rose risk read:** Low. No current CVEs, no recurrence of the 2017 incident, active maintenance with a March 2026 stable release, published checksums, and a clear official download path. The primary standing risk is bundled upstream library dependencies — standard for this class of tool.

---

## Recommendation

HandBrake 1.11.1 is a well-maintained, purpose-appropriate tool for Vicky's visual compression workflow and should clear Soren's review without significant obstacles. Download exclusively from handbrake.fr, verify the SHA-256 checksum before installation, and confirm .NET Desktop Runtime 10.0.x is installed. If Soren surfaces any upstream library CVEs in the bundled dependency stack, assess whether the specific vulnerability is reachable through HandBrake's usage pattern before treating it as a blocker.

---

## C&P Summary

HandBrake is a free, open-source video compression tool that has been actively maintained for over 20 years. The current Windows version is 1.11.1, released March 2026. It gives Vicky a visual interface to compress videos using the H.265 codec, set resolution to 720p, lock frame rate to 30fps, and adjust bitrate until the output file fits under Discord's 10 MB upload limit — all without needing Pete to write a script. It also ships a command-line version (HandBrakeCLI) that Pete can use if the workflow ever needs automation. Security research found no CVEs specific to HandBrake in the past 12 months. The only notable historical incident was a 2017 mirror compromise that served malware to Mac users for about 72 hours — it was quickly contained, has not recurred, and did not affect Windows. The official download is handbrake.fr; the project publishes checksums to verify every installer. Overall risk profile is low, consistent with the META report's MEDIUM rating as a conservative starting point for Soren's formal review.

---
*Report by Rose | Session 161 | 2026-05-19*
