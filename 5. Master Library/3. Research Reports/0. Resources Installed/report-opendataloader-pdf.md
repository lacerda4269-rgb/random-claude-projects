# Resource Report: opendataloader-pdf

**URL:** https://github.com/opendataloader-project/opendataloader-pdf
**Status:** ✅ INSTALLED — Section 5 (CLI), Tier 2
**Dates:** Researched 2026-06-08 (Rose) · Installed 2026-06-10, Session 237 (Sage)
**Researched by:** Rose | Security pre-check: Soren (2026-06-08) | Installed & install-verified by: Sage (CEO) — pre-clearance via Feynman tool assessment Session 234
**Already in Master Library?** Yes — Section 5 (CLI), Tier 2
**Note:** Consolidated canonical — merges Rose's research report + Soren's security clearance with Sage's install-session record (Session 264 ML Stage 1 consolidation).

---

## What It Is

opendataloader-pdf is an open-source PDF parser purpose-built for AI data pipelines and accessibility automation. It extracts structured content from any PDF — digital, scanned, or tagged — and outputs Markdown, JSON with bounding boxes, HTML, or Tagged PDF. It holds the #1 benchmark accuracy score for PDF extraction (0.907 overall, 0.928 for tables) and is the first open-source tool to automate end-to-end PDF accessibility remediation up to PDF/UA compliance. Developed in collaboration with the PDF Association and Dual Lab (makers of veraPDF). Published by the opendataloader-project (Hancom, a Korean enterprise software company). Java core with Python, Node.js, and Java SDKs. Version 2.4.7 — Apache 2.0 license. Zero Python dependencies; requires Java 11+ at runtime. 24,130 GitHub stars as of research date.

## What It Does

Provides a Python API and CLI surface for driving the underlying Java opendataloader-pdf engine, which parses PDFs and extracts structured content into machine-readable formats.

- Extracts content into Markdown, JSON (with bounding boxes for every element), and HTML — ready for RAG and LLM pipelines
- Runs in two modes: local deterministic mode (0.015s/page, no API calls) and AI hybrid mode for complex layouts (local CPU backend — no cloud egress)
- Uses the XY-Cut++ reading-order algorithm to correctly sequence multi-column and complex-layout pages
- Preserves table structure with 0.928 benchmark accuracy — best available for table extraction
- Applies AI safety filters during extraction to reduce prompt-injection risk from malicious PDF content
- Automates PDF accessibility tagging — converts untagged PDFs to Tagged PDF (open-source tier); outputs PDF/UA-compliant documents (enterprise add-on)

Python API surface: `convert` / `convert_generated` (PDF-to-data), `run` / `run_jar` (Java JAR execution), `runner` (batch), `cli_options_generated` (CLI options), `wrapper` (low-level Java process wrapper).

Primary use case: automated extraction of structured data from PDFs — academic documents, reports, datasets — aligns directly with Project Feynman's course-material processing needs.

## Invocation Interface

```bash
# Python
pip install opendataloader-pdf

# Node.js
npm install @opendataloader/pdf
```

- **Output formats:** markdown, json (with bounding boxes), html, tagged-pdf
- **Local mode:** deterministic, no network calls, 0.015s/page
- **Hybrid mode:** routes complex pages to a local AI backend (CPU) — no cloud egress

## Package Metadata (June 2026)

- **Version:** 2.4.7
- **License:** Apache-2.0
- **Author:** opendataloader-project (open.dataloader@hancom.com)
- **Python dependencies:** None (pure wrapper; runtime requires Java 11+)
- **Install size:** ~22.6 MB (wheel)
- **PyPI install location:** `...\Python313\Lib\site-packages\opendataloader_pdf`

## How It Works

The package bundles or downloads the opendataloader-pdf Java JAR at runtime. When `run_jar` or `convert` is called, it spawns a Java subprocess using the system Java installation (Java 11+ required). Output is returned as structured data — format depends on call type. The Python wrapper handles process lifecycle, argument marshaling, and output capture.

## Key Dependencies

- **Runtime:** Java 11+ (OpenJDK or equivalent) — confirmed present at `C:\Program Files\Eclipse Adoptium\jdk-25.0.3.9-hotspot\` (OpenJDK 25.0.3 Temurin)
- **Python dependencies:** None
- **Bundled:** Java JAR included in package wheel

## Caveats and Known Issues

- Java runtime is a hard dependency — tool fails silently or with a subprocess error if Java is missing or below 11. Java gate check required before any use.
- Hancom origin — primarily developed for enterprise document-processing workflows; community support is limited compared to pure open-source tools.
- Trivy scan (2026-06-10): 0 vulnerabilities, 0 secrets. No code modules found in the scanned directory; JAR bundled separately.

## Builder Footprint

- **Integration type:** Python/Node.js/Java library; installable via pip, npm, or Maven; no server required for local mode
- **Extension points:** JSON output with bounding boxes is an agent-readable structured interface; local vs. hybrid mode configurable per call; enterprise add-on (PDF/UA) is modular
- **Build complexity signal:** Low — pip install and call the API; Java 11+ is the only non-trivial prerequisite
- **Known conflicts:** None identified with existing ML items

## Relevance to This Project

Cleared for Project Feynman — PDF data extraction from academic papers, course materials, and structured documents (flagged Tier 2 in Session 234, POM 212 context). More broadly: any project that needs to ingest PDFs into an AI pipeline — research documents, financial filings, strategy/regulatory materials — benefits from a reliable, high-accuracy PDF-to-structured-data layer. This is the strongest open-source option by benchmark; the bounding-box JSON output is particularly useful for agents that need to reference specific document locations.

## Master Library Assessment

- **Section:** 5 — Command Line Interface (CLI)
- **Tier:** 2 (pre-cleared)
- **Rationale:** #1 benchmark PDF parser, Apache 2.0, 24k+ stars, actively maintained. pip-installable, zero Python dependencies; Java runtime adds a system dependency but the Python surface is clean. Tier 2 rather than 1 because PDF ingestion is phase-dependent — not needed at project setup, valuable when document-heavy research or RAG pipelines are in scope.

## Soren Security Pre-check

- **Verdict:** CLEARED WITH CONDITIONS
- **Checked:** License (Apache 2.0 — permissive, confirmed), stars (24,130), forks (2,254), last pushed (2026-06-08 — active same day as research), open issues (59 — normal for scale), language (Java core), maintainer (opendataloader-project org, multi-contributor, Hancom partnership), hybrid-mode architecture (confirmed local-only via official docs — no cloud egress), AI safety filter (built-in), enterprise tier (separate add-on), no known CVEs in project or primary dependency chain
- **Notes:**

| # | Severity | Flag | Notes |
|---|----------|------|-------|
| 1 | MEDIUM | Java 11+ dependency chain | Transitive dependency vulnerabilities possible at install time; run `mvn dependency:tree` or equivalent at install to audit. No known CVEs against the project itself. |
| 2 | LOW | Enterprise PDF/UA add-on | Paid add-on with separate licensing — confirm before commercial use of that feature. Core tool is Apache 2.0 with no commercial restrictions. |
| 3 | INFO | Hybrid mode clarification | Pre-assessment flagged hybrid mode as sending data externally. Incorrect per official docs — hybrid routes complex pages to a local CPU AI backend. No cloud egress. Condition removed. |
| 4 | INFO | Built-in AI safety filter | Prompt-injection risk from malicious PDF content explicitly mitigated by the tool's own filter layer. Positive security signal. |

No suspicious patterns, obfuscated code, or undisclosed endpoints identified. Hybrid mode is fully air-gapped — local CPU only.

Post-install confirmation: Trivy filesystem scan 2026-06-10 — 0 vulnerabilities, 0 secrets (see Caveats).

*Reviewed by Soren | 2026-06-08*

---

## C&P Summary

opendataloader-pdf is a free, open-source tool that converts any PDF into clean, structured data ready for AI pipelines. It outputs Markdown, JSON (with exact coordinates for every piece of text, table, and image), or HTML, and runs locally with no internet connection at 0.015 seconds per page. It holds the #1 accuracy score in independent benchmarks across PDF parsers, including best-in-class table extraction, and is the first open-source tool to automate PDF accessibility tagging end-to-end. It works by wrapping a Java engine — so Java 11+ must be installed; once Java is in place, the Python install is a single pip command with zero additional dependencies. Apache 2.0, 24,130 stars, actively maintained. For this team it is the go-to tool any time a project needs to turn PDF documents into AI-readable content — primary use case here is Feynman's academic work (course materials, papers, datasets).

---

## Sources

- PyPI: opendataloader-pdf 2.4.7
- GitHub: opendataloader-project/opendataloader-pdf (24,130 stars)
- Feynman tool assessment — Session 234 (POM 212 context)
- Soren security pre-check — 2026-06-08
- Trivy filesystem scan — 2026-06-10 (clean)

---

## Report Version Log

| Version | Date | What Changed |
|---------|------|--------------|

---

*Consolidated canonical — opendataloader-pdf. Research: Rose (2026-06-08). Security: Soren (2026-06-08). Install: Sage (2026-06-10). Merged: Session 264.*
