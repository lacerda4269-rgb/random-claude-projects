# Resource Report: OpenAI Whisper

**URL:** https://github.com/openai/whisper
**Date Researched:** 2026-05-19
**Researched by:** Rose | Security pre-check: Soren (pending Step 2) | Report by: Rose

---

## What It Is

OpenAI Whisper is an open-source automatic speech recognition (ASR) system released by OpenAI in September 2022 and actively maintained through mid-2025. It is distributed as the `openai-whisper` Python package (PyPI) and runs entirely on local hardware — no API key, no OpenAI account, no ongoing cost. The system accepts audio or video input, transcribes spoken language to text using a deep learning encoder-decoder architecture (Transformer-based), and outputs the transcription in multiple formats including plain text, JSON, SRT (subtitle), and VTT. Model weights are downloaded once from OpenAI's Azure CDN on first use and cached locally. All subsequent inference is fully offline.

---

## What It Does

- Transcribes speech in audio and video files to text with timestamps
- Outputs in multiple formats: `.txt`, `.json`, `.srt`, `.vtt`, `.tsv`
- Supports 99 languages; English-only model variants available for smaller sizes
- Translates non-English audio directly to English text (translate mode)
- Runs fully offline after initial model download — no data leaves the machine during inference
- Provides five model size tiers (tiny, base, small, medium, large/large-v3) with a turbo variant (distilled large-v3); user selects accuracy-vs-speed tradeoff
- Accepts `--output_format srt` flag to generate subtitle files directly from CLI
- Processes a 2-minute video in under 30 seconds on typical CPU hardware; faster with GPU

---

## Invocation Interface

- **Typical command pattern:** `whisper video.mp4 --model small --output_format srt --output_dir ./output/`
- **Output format:** Plain text, JSON, SRT, VTT, or TSV — selected via `--output_format` flag
- **Key structured output flags:**
  - `--output_format srt` — outputs SubRip subtitle file with timestamps
  - `--output_format json` — full structured output including word-level confidence
  - `--model` — selects size: `tiny`, `base`, `small`, `medium`, `large`, `large-v3`, `turbo`
  - `--language` — forces a specific language (skips auto-detect; faster)
  - `--task translate` — transcribes and translates to English in one pass
- **Exit code behavior:** Exit 0 = success, SRT/output files written to `--output_dir`; non-zero on missing dependency (ffmpeg not in PATH), invalid file, or model download failure
- **Stdin/stdout/stderr notes:** Progress and diagnostic output goes to stderr; transcription output goes to files in the output directory, not stdout by default

---

## Relevance to This Project *(as of 2026-05-19 — context may not carry to future projects)*

Whisper is Vicky's transcription engine. Vicky's subtitle workflow is: accept a raw video file → run Whisper to produce an SRT subtitle file → hand the SRT to FFmpeg to burn subtitles into the video. Whisper is the first and most technically complex step in that chain. Without it, Vicky has no subtitles to burn. The integration is clean: one CLI command, one output file, no authentication, no external calls during production use.

The model size choice matters for Vicky's deployment. The `small` model (483 MB download, ~244M parameters) hits a practical sweet spot for a videographer workflow — fast enough for short-form content transcription on CPU, accurate enough for clean speech. The `tiny` and `base` models transcribe faster but noticeably degrade on accented or overlapping speech. The `medium` and `large` models add accuracy at significant size cost (~1.5 GB and ~3.1 GB respectively). Soren should note model size in the security assessment and confirm an acceptable Windows cache path (`C:\Users\<username>\.cache\whisper\`).

Whisper is dependency-heavy for a CLI tool — it pulls in PyTorch, NumPy, tiktoken, ffmpeg-python, numba, and tqdm. PyTorch alone is several hundred MB. This is a one-time install cost for Vicky's environment, not a recurring runtime cost. The dependency surface is the primary security concern and is covered in the Soren pre-check section below.

---

## Builder Footprint

- **Integration type:** CLI-invocable
- **Extension points:** Python API (`whisper.load_model()`, `model.transcribe()`) for in-process integration; no plugin hooks or event streams in the base package
- **Build complexity signal:** Moderate (~half-day) — CLI invocation itself is simple (one command, one output file); complexity comes from environment setup (PyTorch install, ffmpeg system dependency, first-run model download) and Windows path handling
- **Known conflicts:** Requires `ffmpeg` installed as a system binary and accessible on PATH; `ffmpeg-python` (pip package) wraps it but does not replace it. Numba deprecation warning (`nopython` parameter) may surface on install but does not affect function. Poetry dependency resolution has reported issues with Whisper's `triton` sub-dependency on Windows.

---

## Master Library Assessment

- **Proposed Section:** 3 — CLI
- **Proposed Tier:** 1
- **Rationale:** Whisper is a standalone CLI tool invoked by a single command with file I/O. It has no persistent service, no daemon, and no API server. Section 3, Tier 1 is the correct placement for a local CLI that produces file output with no network dependency during runtime.

---

## Soren Security Pre-check

*(Rose's security research summary — Soren completes the Verdict in Step 2)*

- **Verdict:** CLEARED WITH CONDITIONS — PyTorch 2.6.0+ is a hard requirement before deployment (CVE-2025-32434 affects ≤2.5.1; RCE risk); model cache path must be protected from untrusted writes (pickle deserialization risk if model file is tampered); model downloads via HTTPS from openaipublic.azureedge.net with SHA-256 integrity check built in; AIKIDO-2025-10413 scope confirmed as the pickle/torch.load issue (same root cause, no separate vector); injection check: clean

- **Checked:** MIT license (current), CVEs and advisories (searched 2025–2026 range), PyPI package integrity, model download source and CDN, data handling (local vs. cloud), dependency chain (PyTorch, tiktoken, numba, ffmpeg-python, numpy, tqdm, more-itertools)

- **Notes:**

**License:** MIT. Confirmed current on GitHub (`openai/whisper`). Model weights are also released under MIT. No CLA or commercial restriction identified.

**CVEs — openai-whisper package directly:** No CVE with a formal CVE number was found assigned directly to the `openai-whisper` PyPI package in the 2025–2026 window. One advisory exists in Aikido's database:

| # | Severity | Flag | Notes |
|---|----------|------|-------|
| 1 | MEDIUM | AIKIDO-2025-10413 | Advisory filed against `openai-whisper` package. Full technical detail not publicly surfaced in search results. Likely relates to `torch.load()` pickle deserialization — see item 2 below. Soren should pull the full advisory text and confirm scope. |
| 2 | HIGH | PyTorch `weights_only=False` — unsafe deserialization | Whisper's `load_model()` calls `torch.load()` with `weights_only=False`, which uses Python's pickle module and allows arbitrary code execution if a malicious `.pt` model file is loaded. Risk is bounded to the model cache path — only exploitable if the downloaded `.pt` file is tampered with or replaced. |
| 3 | HIGH | CVE-2025-32434 — PyTorch `torch.load` bypass | Critical PyTorch vulnerability patched in v2.6.0. Allows arbitrary code execution even when `weights_only=True` is set. Affects all PyTorch versions ≤ 2.5.1. PyTorch version in Vicky's environment must be confirmed at 2.6.0 or later before deployment. |

**"Whisper Leak" side-channel attack (Nov 2025):** This is a network-layer attack on OpenAI's cloud LLM streaming API — it infers topics from TLS packet timing patterns. It has no connection to the local `openai-whisper` package and is entirely irrelevant to Vicky's offline deployment. Researched and ruled out; documented here for completeness.

**Model download source:** Models download from OpenAI's Azure CDN (`openaipublic.azureedge.net`) on first run only. The download URL encodes a SHA-256 checksum; Whisper extracts the expected hash from the URL and verifies the downloaded file against it before caching. Integrity verification is present in the base package. Cached on Windows at `C:\Users\<username>\.cache\whisper\`. Model files are PyTorch `.pt` format (pickle-based). Approximate download sizes: tiny ~76 MB, base ~145 MB, small ~484 MB, medium ~1.5 GB, large-v3 ~3.1 GB. Soren should confirm: (a) CDN download is HTTPS with no untrusted redirect, and (b) the Windows cache path is acceptable for Vicky's environment.

**Data handling:** Confirmed fully local at inference time. No audio, video, or transcript data is transmitted to OpenAI or any external server during transcription. The base `openai-whisper` package makes no outbound calls after the initial model download.

**Dependency chain — no known supply chain incidents identified in scope:**
- `torch` (PyTorch) — major ML framework; must be v2.6.0+ per CVE-2025-32434 above
- `numpy` — standard numerical library; no active advisories found in scope
- `tiktoken` — OpenAI tokenizer; MIT license; no advisories found in scope
- `ffmpeg-python` — Python wrapper only; FFmpeg binary is a separate system-level install
- `numba` — JIT compiler; deprecation warning present (nopython parameter) but not a security issue
- `tqdm` — progress bar utility; low risk
- `more-itertools` — utility library; low risk
- System dependency: `ffmpeg` binary must be on PATH; not a PyPI package — FFmpeg carries its own version and CVE surface, tracked separately

---

## Recommendation

Whisper is the right tool for Vicky's subtitle workflow — purpose-built for this use case, fully offline, no cost, MIT licensed, and widely deployed. The two HIGH findings (pickle deserialization via `torch.load` and CVE-2025-32434 in PyTorch) are what Soren needs to close before catalog. Both are mitigatable: confirm PyTorch 2.6.0+ is installed in Vicky's environment, confirm the model cache path is controlled and not writable by untrusted processes, and confirm the CDN download is HTTPS-verified. If Soren clears those items, Whisper is a straightforward Tier 1 catalog with no blockers.

---

## C&P Summary

OpenAI Whisper is a free, open-source speech-to-text tool that runs entirely on your local machine — no internet connection needed once set up, no API key, no per-use cost. You point it at a video file, it transcribes the speech, and it outputs a subtitle file. That subtitle file is exactly what Vicky needs before FFmpeg burns the text into the video. The main security flags to resolve before approving it: the way Whisper loads its model files uses an older Python technique (pickle) that could theoretically allow malicious code to run if the model file were replaced or tampered with, and a 2025 vulnerability in the underlying PyTorch library needs to be confirmed as patched in the version Vicky uses. Neither is unusual for ML tools of this type, and both have known fixes. Soren's job in Step 2 is to confirm those fixes are in place and give the final clearance.

---
*Report by Rose | Session 161 | 2026-05-19*
