# Resource Report: Mermaid CLI

**Prepared by:** Rose (Researcher)
**Reviewed by:** Soren (Security Manager)
**Installed by:** Sage (CEO)
**Date:** 2026-06-09 (Session 232)
**Category:** CLI — Diagram Rendering
**Role in Stack:** Diagram rendering for all MIP workflow diagrams, flowcharts, and visual aids. Converts Mermaid code blocks (.mmd / fenced Markdown) to SVG, PNG, or PDF. Activated at MUIP finalization to generate image pairs for all Mermaid .md files.
**Status:** ✅ ACTIVE — v11.15.0 installed and verified

---

## What It Is

Mermaid CLI (`mmdc`) is the command-line interface for the Mermaid.js diagramming library. It converts text-based Mermaid diagram definitions into rendered image files (SVG, PNG, or PDF). It is the canonical tool for generating diagram output in automated pipelines, documentation builds, and server-side rendering workflows. Under the hood it drives headless Chromium via Puppeteer.

- **Package:** `@mermaid-js/mermaid-cli`
- **License:** MIT — free, no commercial restrictions
- **Ecosystem:** mermaid-js (74k+ stars on core library)
- **Cleared version:** v11.15.0

---

## What It Does

- Converts `.mmd` diagram definition files → SVG, PNG, or PDF
- Processes full Markdown files — replaces fenced ` ```mermaid ` blocks with rendered images inline
- Supports: flowcharts, sequence diagrams, class diagrams, state diagrams, ER diagrams, Gantt charts, Git graphs, pie charts, journey maps, C4 diagrams, Venn diagrams, and more
- Output: SVG (default, best quality), PNG, PDF

**Key CLI flags:**
- `-i <file>` — input file (.mmd or .md)
- `-o <file>` — output file (.svg, .png, .pdf)
- `-t <theme>` — theme: `default`, `forest`, `dark`, `neutral`
- `-b <color>` — background color

---

## Installation

- **Install method:** npm global with `--prefix` to ClaudeTools
- **Install command:** `npm install -g @mermaid-js/mermaid-cli --prefix "C:/ClaudeTools/mermaid-cli"`
- **Binary location:** `C:\ClaudeTools\mermaid-cli\mmdc.cmd`
- **Verify:** `mmdc.cmd --version` → `11.15.0`
- **Session installed:** 232 (2026-06-09)
- **Note — Puppeteer/Chrome:** Puppeteer auto-downloads Chrome headless shell on install. Requires a clean cache — if the cache folder exists without the binary (partial prior download), remove `C:\Users\[user]\.cache\puppeteer\` before retrying.

**Usage:**
```bash
# Render single diagram
C:\ClaudeTools\mermaid-cli\mmdc.cmd -i diagram.mmd -o diagram.svg

# Transform Markdown file (replaces all ```mermaid blocks with images)
C:\ClaudeTools\mermaid-cli\mmdc.cmd -i document.md -o document-rendered.md
```

---

## Soren Security Review

- **Verdict:** CLEARED
- **Scan date:** 2026-06-09
- **Trivy v0.71.0:** 0 vulnerabilities across 355-package dependency tree
- **Gitleaks v8.30.1:** No leaks found
- **All four CVEs** (CVE-2026-41159, CVE-2026-41148, CVE-2026-41149, CVE-2026-41150) confirmed resolved in v11.15.0

**Carry-forward conditions:**
1. Install `@mermaid-js/mermaid-cli` only — do not install the deprecated `mermaid.cli` package
2. npm global install is acceptable for local agent use; Docker preferred for CI/server environments
3. Do not use `--no-sandbox` on production systems
4. Do not install v11.14.0 — four CVEs are unpatched in that version

---

## Project Pairing Convention (Wired in Session 232)

During active MIP development, all diagrams remain as live Mermaid code in `.md` files — this is the source of truth. At MUIP finalization, Mermaid CLI runs once to generate a static image pair (SVG or PNG) for each diagram file. After that, whenever a diagram's `.md` is updated, the image pair must be regenerated to match. Convention: `.md` = source of truth; image = final-state companion.

---

## ML Record

- **Section:** 5 — Command Line Interface (CLI)
- **Tier:** 2
- **Full report:** `5. Master Library/5. Command Line Interface (CLI)/1. Research Reports/report-mermaid-cli.md`

---

## C&P Summary

Mermaid CLI (`mmdc`) is installed at `C:\ClaudeTools\mermaid-cli\mmdc.cmd` — v11.15.0, CLEARED by Soren (Trivy: 0 vulns, Gitleaks: clean, all four CVEs resolved). It converts Mermaid diagram definitions to SVG/PNG/PDF from the CLI. Primary role in the MIP: rendering the existing Mermaid visual aids as image pairs at MUIP finalization. Source of truth for all diagrams is always the `.md` file; images are generated output, not maintained manually.

---
*Keep-both pair (S264): this is the **install/deployment record**. Full research report (incl. free-alternatives survey) → `Command Line Interface (CLI)/Research Reports/report-mermaid-cli.md`.*
