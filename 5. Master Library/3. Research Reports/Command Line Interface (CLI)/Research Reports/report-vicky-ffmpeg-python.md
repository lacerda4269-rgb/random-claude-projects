# Resource Report: ffmpeg-python

**URL:** https://pypi.org/project/ffmpeg-python/
**Date Researched:** 2026-05-19
**Researched by:** Rose | Security pre-check: Soren (pending Step 2) | Report by: Rose

---

## What It Is

`ffmpeg-python` (PyPI package name: `ffmpeg-python`, installed as `ffmpeg`; GitHub: `kkroening/ffmpeg-python`) is a pure-Python API wrapper around the FFmpeg command-line tool. It does not ship or install FFmpeg — it delegates all media processing to the FFmpeg binary already present on the system. The library provides a fluent, chainable Python interface for constructing FFmpeg processing pipelines (inputs, filters, outputs, and complex filtergraphs) without writing raw subprocess calls or manually quoting command strings. Current published version on PyPI is **0.2.0**, released July 6, 2019. No newer PyPI release exists as of 2026-05-19. The underlying GitHub repo has unreleased commits and open pull requests but no official release since 2019.

---

## What It Does

- Builds FFmpeg command pipelines in Python using a fluent method-chaining API (`input()`, `output()`, `filter()`, `run()`)
- Supports complex filtergraphs including split, overlay, concat, and custom filter chains — capabilities that are painful to construct manually as raw CLI strings
- Wraps subprocess execution of FFmpeg, capturing stdout/stderr and surfacing process errors as Python exceptions
- Supports `run_async()` for non-blocking execution, enabling async video pipeline management in longer workflows
- Provides `probe()` to query media file metadata (codec, duration, streams) via FFmpeg's `-show_format`/`-show_streams` flags
- Supports piped input/output (`pipe:`) for in-memory processing without intermediate files
- Works on Windows, Linux, and macOS wherever the FFmpeg binary is installed and accessible on PATH
- Produces an ffmpeg CLI command string via `compile()` for inspection or logging before execution

---

## Invocation Interface

- **Typical command pattern:**
  ```python
  import ffmpeg
  stream = ffmpeg.input('input.mp4')
  stream = ffmpeg.output(stream, 'output.mp4', vcodec='libx264')
  ffmpeg.run(stream)
  ```
- **Output format:** `run()` returns a tuple of `(stdout_bytes, stderr_bytes)`; `run_async()` returns a `subprocess.Popen` object; `probe()` returns a parsed dict of stream/format metadata
- **Key structured output flags:** `quiet=True` suppresses FFmpeg console output; `capture_stdout=True` / `capture_stderr=True` capture streams as bytes; `overwrite_output()` appends the `-y` flag
- **Exit code behavior:** Non-zero FFmpeg exit codes raise `ffmpeg.Error` (a subclass of `RuntimeError`) with `stdout` and `stderr` attributes — no silent failure
- **Stdin/stdout/stderr notes:** When using `pipe:` input/output, stdin/stdout are passed through the subprocess handle; callers manage the byte stream directly

---

## Relevance to This Project *(as of 2026-05-19 — context may not carry to future projects)*

Vicky's video automation work requires building FFmpeg processing pipelines — trimming, transcoding, resizing, overlaying, and concatenating video files. Pete (Python Specialist) is the scripter for these pipelines. Without a wrapper, Pete must construct raw subprocess strings with careful argument quoting and manage error handling manually. That approach is fragile and increasingly messy as pipelines grow complex. `ffmpeg-python` solves that problem directly: it turns an FFmpeg command pipeline into readable, testable Python code.

The integration model is clean for this stack. FFmpeg is already cleared (`report-vicky-ffmpeg.md`). This wrapper adds zero new external network surface — it makes subprocess calls to the local FFmpeg binary and nothing else. Pete imports the library, builds the graph in Python, and calls `run()`. The output is the same as if Pete had typed the FFmpeg command manually; the wrapper just constructs and executes it.

The stale release history (0.2.0, 2019) is worth naming plainly: the API is stable and the feature set is complete for standard use cases, but the package is not actively releasing. For Pete's intended use — scripted video processing pipelines, not cutting-edge FFmpeg features — the 2019 API covers the full scope of work. The dependency flag on `future` (see Security section) is the operative risk item, not the wrapper's age.

---

## Builder Footprint

- **Integration type:** CLI-invocable (Python-layer wrapper over the FFmpeg CLI binary)
- **Extension points:** Custom filter nodes can be registered via `ffmpeg.filter()`; `run_async()` enables integration with async orchestration patterns
- **Build complexity signal:** Simple (~1–2 hours) — `pip install ffmpeg-python`; no configuration files, no environment setup beyond FFmpeg binary on PATH; first pipeline functional in under an hour
- **Known conflicts:** Package installs as `ffmpeg` in the Python namespace — conflicts with the separate PyPI package also named `ffmpeg` (a stub/placeholder). Both cannot be installed simultaneously. Pete must install `ffmpeg-python`, not `ffmpeg`.

---

## Master Library Assessment

- **Proposed Section:** 3 — CLI
- **Proposed Tier:** 2
- **Rationale:** Pure-Python wrapper over a Tier 1 CLI tool (FFmpeg). No independent network surface; clearance is derivative of FFmpeg's clearance. Tier 2 reflects the dependency relationship — not a standalone tool, but a scripting layer on top of one.

---

## Soren Security Pre-check

*(Rose's security research summary — Soren completes the Verdict in Step 2)*

- **Verdict:** CLEARED WITH CONDITIONS — wrapper itself has no direct CVEs; python-future dependency is EoS with CVE-2025-50817 filed (advisory withdrawn; exploitation requires local write access to sys.path — not a remote vector); install as `ffmpeg-python` not `ffmpeg` (namespace conflict); monitor PR #795 for eventual merge; FFmpeg binary must be the cleared gyan.dev build; injection check: clean
- **Checked:** PyPI version and release history; GitHub repository activity and open issues; CVE databases for the `ffmpeg-python` wrapper itself; GitHub Security Advisories page for the repo; dependency chain; MIT license status; supply chain posture
- **Notes:**

**CVEs against ffmpeg-python directly:** None identified. No CVE has been issued against the `kkroening/ffmpeg-python` wrapper itself. The GitHub Security Advisories page for the repo shows no published advisories.

**CVE-2025-50817 — python-future dependency:**

The published 0.2.0 release lists `future` (the `python-future` package) as an `install_requires` dependency. CVE-2025-50817 was filed against `python-future` in August 2025 for arbitrary code execution via unintended import of a `test.py` file present in `sys.path`. Key context: the advisory has been withdrawn by multiple parties on the grounds that it describes expected Python import system behavior, not a flaw in `python-future`; exploitation requires an attacker to already have write access to the target filesystem or `sys.path`. `python-future` has been declared End-of-Support by its own maintainer, meaning no patches will be issued. GitHub Issue #877 (opened August 2025) formally requests that the maintainer drop the `future` dependency; Pull Request #795 implements the removal but has not been merged.

| # | Severity | Flag | Notes |
|---|----------|------|-------|
| 1 | MEDIUM | CVE-2025-50817 (python-future dependency) | Advisory withdrawn; exploitation requires local write access; python-future is EoS; fix PR #795 unmerged in ffmpeg-python repo |
| 2 | LOW | Stale release (last release 2019) | No patch path via official PyPI channel; API stable but supply chain hygiene degraded |

**Maintenance status:** Last PyPI release: 0.2.0, July 6, 2019 — over six years ago. The GitHub repository has accumulated unreleased commits and 45+ open pull requests. The maintainer (kkroening) has not cut a new release or responded to the dependency CVE issue. Stale-flagged under Rose's standard criteria.

**Supply chain:** Minimal. The wrapper itself is pure Python with no compiled extensions. Single runtime dependency: `future`. No other third-party packages in `install_requires`.

**License:** MIT — confirmed current on PyPI and in the GitHub repository.

---

## Recommendation

Clear conditionally. The wrapper itself is clean — no direct CVEs, MIT license confirmed, minimal surface area. The `future` dependency flags as a supply chain concern (EoS package, CVE filed and disputed, fix unmerged), but the CVE has been withdrawn and real-world exploitation requires local write access. Soren should confirm verdict and severity classification. If cleared, Pete should be briefed on the namespace conflict (`ffmpeg-python` vs. `ffmpeg` on PyPI) and the `future` dependency status.

---

## C&P Summary

`ffmpeg-python` is a Python wrapper that lets Pete write FFmpeg video processing pipelines in clean Python code instead of raw command strings. It calls the FFmpeg binary already installed on the system — it adds no new external connections. The package is stable and covers all standard video automation needs, but it has not had an official release since 2019. Its one runtime dependency (`python-future`) has been flagged by a since-withdrawn CVE and is End-of-Support; a fix exists as an unmerged pull request but has not been officially released. License is MIT. The wrapper itself has no direct security findings. Soren reviews the dependency risk and issues the final clearance verdict.

---
*Report by Rose | Session 161 | 2026-05-19*
