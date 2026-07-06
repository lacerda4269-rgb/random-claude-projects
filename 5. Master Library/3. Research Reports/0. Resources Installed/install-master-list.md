# P7 Sandbox — Install Master List

**Project:** Initial Package Project — Project Sandbox (P7)
**Created:** 2026-06-04 (Session 218 return)
**Created by:** Sage (CEO) + Sophia (COO)
**Purpose:** Single reference for everything in the P7 install queue — what it is, where it lives, and its current status.

---

## Summary

| # | Tool | Type | Status | Version |
|---|------|------|--------|---------|
| 1 | Playwright CLI | CLI (npm global) | ✅ ACTIVE | 0.1.13 |
| 2 | Playwright MCP | MCP (npx) | ✅ ACTIVE | latest |
| 3 | transcribe-anything | CLI (pip) | ✅ ACTIVE | 4.0.0 |
| 5 | MoneyPrinterTurbo | Python app (git clone) | ⚠️ INSTALLED — CAVEATS | latest main |
| 6 | ElevenLabs MCP | MCP (uvx) | ✅ ACTIVE | 0.9.1 |
| 7 | Trivy | CLI (binary) | ✅ ACTIVE | v0.71.0 |
| 8 | Gitleaks | CLI (binary) | ✅ ACTIVE | v8.30.1 |
| 9 | Remotion | Framework (npm) | ✅ ACTIVE | 4.0.472 |
| 11 | NotebookLM | Web tool | 🌐 NO INSTALL NEEDED | — |
| 12 | ffmpeg | CLI (binary) | ✅ ACTIVE | 8.1.1 |
| 13 | Mermaid CLI | CLI (npm --prefix) | ✅ ACTIVE | v11.15.0 |
| 14 | Humanizer | Skill (npx skills, global) | ✅ ACTIVE | latest (blader/humanizer) |
| 15 | opendataloader-pdf | CLI (pip) | ✅ ACTIVE | 2.4.7 |
| 16 | Obsidian | Desktop app (Electron) | ✅ ACTIVE | 1.12.7 |
| 17 | claude-remember | Plugin (Claude Code) | ✅ ACTIVE | 0.7.3 |
| 18 | Graphify | CLI (Python/uv) | ✅ ACTIVE | 0.8.37 |
| 19 | Camofox Browser | CLI (npm global) | ✅ ACTIVE | v2.4.5 |
| 20 | HyperFrames | CLI (npm) | ✅ ACTIVE | v0.6.95 |
| 21 | RAG-Anything | Python library (pip) | ✅ ACTIVE | v1.3.1 |
| 22 | context-mode | MCP (npx) | ✅ ACTIVE | v1.0.162 |

**Removed tools** (full history in the *Removed — History* section below; not counted as installed): mcp-youtube (MCP — Session 222), claude-mem (Plugin — Session 251).

---

## Detail

---

### 15. opendataloader-pdf
- **Type:** CLI — pip package (Python wrapper for Java PDF extraction engine)
- **Version:** 2.4.7
- **Install command:** `pip install opendataloader-pdf`
- **Location:** `C:\Users\jlacerda\AppData\Local\Programs\Python\Python313\Lib\site-packages\opendataloader_pdf`
- **Runtime dependency:** Java 11+ — confirmed OpenJDK 25.0.3 (Temurin) at `C:\Program Files\Eclipse Adoptium\jdk-25.0.3.9-hotspot\`
- **Soren status:** Pre-cleared — Tier 2, Apache 2.0 (Feynman tool assessment Session 234)
- **Trivy scan:** 0 CVEs, 0 secrets (2026-06-10)
- **Session installed:** 237 (2026-06-10)
- **ML record:** Section 5 → CLI → Built → `opendataloader-pdf-install-record.md`
- **Primary use:** PDF structured data extraction — Feynman academic coursework (course materials, datasets)
- **Status:** ✅ ACTIVE

---

### 1. Playwright CLI
- **Type:** CLI — npm global package
- **Version:** 0.1.13
- **Install command:** `npm install -g @playwright/cli@latest` + `playwright-cli install --skills`
- **Location:** npm global + `.claude/skills/playwright-cli/` (10 reference skill files)
- **Soren status:** CLEARED (Round 3, 2026-05-02; freshness confirmed Session 213)
- **Session installed:** 217 (2026-06-04)
- **ML record:** Section 5 → CLI → Built → `playwright-cli-install-record.md`
- **Status:** ✅ ACTIVE

---

### 2. Playwright MCP
- **Type:** MCP — Microsoft (@playwright/mcp)
- **Version:** latest (npx auto-install on each run)
- **Config location:** `.mcp.json` at project root
- **Entry:**
  ```json
  "playwright": {
    "command": "npx",
    "args": ["-y", "@playwright/mcp@latest"]
  }
  ```
- **Soren status:** CLEARED (Round 3, 2026-05-02; freshness confirmed Session 213)
- **Session wired:** 217 (2026-06-04)
- **ML record:** Section 6 → MCP → Built → `playwright-mcp-config-record.md`
- **Status:** ✅ ACTIVE

---

### 3. transcribe-anything
- **Type:** CLI — pip package
- **Version:** 4.0.0 (note: report cited v3.2.10; actual install pulled a major version bump — Rose freshness pass pending)
- **Install command:** `pip install transcribe-anything`
- **Location:** pip global; backends run in isolated `uv`-managed venvs
- **Trivy scan:** 0 CVEs — clean
- **Soren status:** CLEARED (Full Database — confirmed pre-install)
- **Session installed:** 218 (2026-06-04)
- **ML record:** Section 5 → CLI → Built → `transcribe-anything-install-record.md`
- **Status:** ✅ ACTIVE

---

### 5. MoneyPrinterTurbo
- **Type:** Python application (git clone + pip install)
- **Version:** latest main branch (cloned 2026-06-04)
- **Install method:** `git clone https://github.com/harry0703/MoneyPrinterTurbo` + `pip install -r requirements.txt`
- **Location:** `C:\ClaudeTools\MoneyPrinterTurbo\`
- **Launch:** `cd C:\ClaudeTools\MoneyPrinterTurbo && streamlit run webui/Main.py`
- **Soren status:** CLEARED WITH CONDITIONS (Session 214) — one condition unresolvable (see caveats)
- **Session installed:** 218 (2026-06-04)
- **ML record:** Section 5 → CLI → Built → `moneyprinterturbo-install-record.md`
- **Status:** ⚠️ INSTALLED — CAVEATS

**Known issue — Pillow CVEs (unresolvable at install time):**
Soren's condition required `pillow ≥ 12.2.0`. MoviePy 2.2.1 pins `pillow < 12.0` — pip ResolutionImpossible. Installed at pillow 11.3.0.

| CVE | Severity | Fixed In |
|-----|----------|----------|
| CVE-2026-25990 | HIGH | 12.1.1 |
| CVE-2026-40192 | HIGH | 12.2.0 |
| CVE-2026-42311 | HIGH | 12.2.0 |
| CVE-2026-42308 | MEDIUM | 12.2.0 |
| CVE-2026-42309 | MEDIUM | 12.2.0 |
| CVE-2026-42310 | MEDIUM | 12.2.0 |

All are image-processing attack vectors (PSD/FITS/PDF crafted inputs). Low exploitability in sandbox context — MoneyPrinterTurbo does not process untrusted user images. **Flag for Soren at next COHK.**

**API keys required before use:**
- `PEXELS_API_KEY` — Pexels (free tier available)
- `PIXABAY_API` — Pixabay (free tier available)
- `LLM API` — OpenAI / Azure / Moonshot / other (configured in UI)
- `TTS API` — Azure / Google / ElevenLabs (configured in UI)

---

### 6. ElevenLabs MCP
- **Type:** MCP — Python (uvx, official ElevenLabs)
- **Version:** 0.9.1
- **Config location:** `.mcp.json` at project root
- **Entry:**
  ```json
  "elevenlabs-mcp": {
    "command": "uvx",
    "args": ["elevenlabs-mcp"],
    "env": {
      "ELEVENLABS_API_KEY": "[API key configured in .mcp.json, untracked]",
      "ELEVENLABS_MCP_OUTPUT_MODE": "files"
    }
  }
  ```
- **Soren status:** CLEARED WITH CONDITIONS (Session 216) — one condition UNMET
- **Session wired:** 218 (2026-06-04)
- **ML record:** Section 6 → MCP → Built → `elevenlabs-mcp-config-record.md`
- **Status:** ✅ ACTIVE

**Resolved (Session 219):**
1. ✅ `mcp` version — forced to `>=1.23.0` via `uvx --with mcp>=1.23.0` in `.mcp.json`; CVE-2025-66416 condition met
2. ✅ `ELEVENLABS_API_KEY` — key added to `.mcp.json`; `.mcp.json` untracked from git + added to `.gitignore`
3. ⬜ Free tier — no commercial use rights; paid plan required for commercial production (non-blocker for sandbox use)

---

### 7. Trivy
- **Type:** CLI — Go static binary
- **Version:** v0.71.0
- **Binary location:** `C:\ClaudeTools\Soren-security\trivy.exe` ✓
- **PATH:** `C:\ClaudeTools\Soren-security` added to user PATH (Session 219) — callable as `trivy` from any new terminal
- **Soren status:** PATH configured; pipeline integration pending (next COHK)
- **ML record:** Section 5 → CLI → 1. Research Reports → `report-trivy.md`
- **Status:** ✅ ACTIVE

---

### 8. Gitleaks
- **Type:** CLI — Go static binary
- **Version:** v8.30.1
- **Binary location:** `C:\ClaudeTools\Soren-security\gitleaks.exe` ✓
- **PATH:** `C:\ClaudeTools\Soren-security` added to user PATH (Session 219) — callable as `gitleaks` from any new terminal
- **Soren status:** PATH configured; pre-commit hook setup + pipeline integration pending (next COHK)
- **ML record:** Section 5 → CLI → 1. Research Reports → `report-gitleaks.md`
- **Status:** ✅ ACTIVE

---

### 9. Remotion
- **Type:** Framework — npm (React-based programmatic video)
- **Version:** 4.0.472
- **Location:** `C:\ClaudeTools\Remotion\`
- **Template:** Audiogram
- **Launch command:** `cd C:\ClaudeTools\Remotion && npm run dev`
- **Render command:** `npx remotion render`
- **Skills installed:** `remotion-best-practices` (symlink, project scope); `find-skills` (global)
- **Soren status:** 2 low severity npm vulnerabilities flagged — review at next COHK
- **Session installed:** 220 (2026-06-05)
- **Note:** `source-map@0.8.0-beta.0` deprecation warning — minor, non-blocking
- **Status:** ✅ ACTIVE

---

### 11. NotebookLM
- **Type:** Web tool — Google (browser-only, no install)
- **URL:** `https://notebooklm.google.com`
- **Version:** N/A (Google-hosted, continuously updated)
- **Location:** Browser — no installation required
- **Authenticated:** lacerda4269@gmail.com ✓ (confirmed Session 219)
- **Soren status:** N/A — Google-hosted; no security review required
- **ML location:** Section 9 (Jay's Shelf) → Full Database + all 3 index cards updated Session 219
- **Status:** ✅ OPERATIONAL — READY TO USE

**Primary agents:** Feynman (coursework Q&A, study guides, Audio Overview for MKT 311 + future courses); Vicky (creative research, Audio Overview for client deliverables, YouTube reference analysis)
**Secondary:** Rose (cross-source research synthesis when needed)
**SOP updates:** Deferred until each agent's first live use — Phase 0 shopping list surfaces this via ML

---

### 12. ffmpeg
- **Type:** CLI — static binary (Windows full build, GPL)
- **Version:** 8.1.1 (full build)
- **Build source:** BtbN/FFmpeg-Builds — `ffmpeg-master-latest-win64-gpl-shared`
- **Binary location:** `C:\ClaudeTools\ffmpeg\ffmpeg-8.1.1-full_build\bin\ffmpeg.exe`
- **Full build path:** `C:\ClaudeTools\ffmpeg\ffmpeg-8.1.1-full_build\`
- **PATH status:** ⬜ UNCONFIRMED — confirm and add `C:\ClaudeTools\ffmpeg\ffmpeg-8.1.1-full_build\bin\` to PATH at next COHK if not already set
- **Install method:** Manual download and extraction (no installer)
- **License:** LGPL 2.1+ (core) / GPL 2+ (full build)
- **Session installed:** Sessions 221–225 (2026-06-05 through 2026-06-06, MKT 311 video production)
- **Primary use:** Video processing — xfade transitions, overlay compositing, audio/video muxing, final assembly, format conversion. Vicky's core production pipeline tool.
- **Soren status:** ⬜ PENDING — flag for next COHK (pending since Session 227)
- **ML record:** Pending — add to Vicky's ML section at next COHK; report on file: `report-ffmpeg.md`
- **Status:** ✅ ACTIVE

---

### 13. Mermaid CLI
- **Type:** CLI — npm global with `--prefix` (`@mermaid-js/mermaid-cli`, `mmdc`)
- **Version:** v11.15.0
- **Install command:** `npm install -g @mermaid-js/mermaid-cli --prefix "C:/ClaudeTools/mermaid-cli"`
- **Binary location:** `C:\ClaudeTools\mermaid-cli\mmdc.cmd` (verify: `mmdc.cmd --version` → 11.15.0)
- **License:** MIT
- **Runtime note:** Puppeteer auto-downloads headless Chrome on install — needs a clean `~/.cache/puppeteer/`; remove a partial prior download before retrying.
- **Soren status:** CLEARED (2026-06-09) — Trivy v0.71.0: 0 vulns across 355-package tree; Gitleaks: clean; all four CVEs (CVE-2026-41159/41148/41149/41150) resolved in v11.15.0. Carry-forward conditions: install `@mermaid-js/mermaid-cli` only (not deprecated `mermaid.cli`); do not install v11.14.0 (4 unpatched CVEs); no `--no-sandbox` on production.
- **Session installed:** 232 (2026-06-09)
- **ML record:** Section 5 → CLI → Built → `report-mermaid-cli.md` (keep-both pair: install/deployment record here; full research report incl. free-alternatives survey at `Command Line Interface (CLI)/Research Reports/report-mermaid-cli.md`)
- **Primary use:** Render all MIP Mermaid diagrams (`.md` code blocks → SVG/PNG/PDF) as image pairs at MUIP finalization. Pairing convention: `.md` = source of truth; image = final-state companion, regenerated whenever the `.md` changes.
- **Status:** ✅ ACTIVE

---

### 14. Humanizer
- **Type:** Skill — npx skills (global, symlinked to Claude Code)
- **Version:** latest (blader/humanizer — last pushed 2026-06-07)
- **Install command:** `npx skills add blader/humanizer -g -y`
- **Location:** `C:\Users\jlacerda\.agents\skills\humanizer\` (canonical) → symlinked at `~/.claude/skills/humanizer/`
- **Trigger:** `/humanizer` slash command or natural language equivalent
- **Soren status:** CLEARED (Session 60; re-confirmed 2026-06-08) — MIT license, no executable code, no dependencies, no network calls
- **Session installed:** 233 (2026-06-09)
- **ML record:** Section 3 (Skills) → `1. Research Reports/report-humanizer-skill.md`
- **Status:** ✅ ACTIVE

**What it does:** Rewrites AI-generated text to remove characteristic AI writing patterns across 29 documented categories (em dash overuse, passive voice, sycophantic tone, filler phrases, etc.). Two-pass rewrite: first transforms, second audits. Voice calibration feature — provide writing samples to match a specific style.

**Primary users:** Sophia (SOPs, AARs, external deliverables); any agent producing externally-visible content.

---

### 16. Obsidian
- **Type:** Desktop app — Electron (local-first Markdown knowledge management)
- **Version:** 1.12.7
- **Install location:** `C:\Users\jlacerda\AppData\Local\Programs\obsidian\`
- **Executable:** `C:\Users\jlacerda\AppData\Local\Programs\obsidian\Obsidian.exe`
- **Install method:** GUI installer downloaded from obsidian.md
- **License:** Proprietary — free for personal use; commercial license required for business use with 2+ users
- **Session installed:** 239 (2026-06-11, P7 memory stack)
- **Soren status:** ⬜ PENDING — flag for next COHK
- **ML record:** Section 9 → Tier 1 → `report-obsidian.md`
- **Primary use:** Human-readable visualization layer for Graphify graph output; Jay's personal knowledge vault
- **Status:** ✅ ACTIVE

---

### 17. claude-remember
- **Type:** Plugin — Claude Code (session memory via .remember/ Markdown files)
- **Version:** 0.7.3
- **Plugin ID:** `remember@dpt-plugins`
- **Install location:** `C:\Users\jlacerda\.claude\plugins\cache\dpt-plugins\remember\0.7.3\`
- **Data directory:** `C:\Users\jlacerda\.claude\plugins\data\remember-dpt-plugins\`
- **Scope:** User-level (applies across all projects)
- **Skill provided:** `remember:remember` — `/remember` command
- **License:** MIT
- **Session installed:** 239 (2026-06-11, P7 memory stack)
- **Soren status:** ⬜ PENDING — flag for next COHK
- **ML record:** Section 3 → Tier 1 → `report-claude-remember.md`
- **Primary use:** Session narrative memory — middle tier of P7 memory stack (MEMORY.md strategic → claude-remember narrative → claude-mem operational)
- **Status:** ✅ ACTIVE

---

### 18. Graphify
- **Type:** CLI — Python tool (uv) + MCP server
- **PyPI package:** `graphifyy`
- **Version:** 0.8.37
- **Install command:** `uv tool install graphifyy`
- **Commands:** `graphify`, `graphify-mcp`
- **Skill location:** `C:\Users\jlacerda\.claude\skills\graphify\`
- **Index output:** `graphify-out/` directory in each indexed project root
- **License:** MIT
- **Session installed:** 239 (2026-06-11, P7 memory stack)
- **First live use:** Session 241 — per-project index for Initial-Package-Project (394 files → 1,056 nodes, 1,466 edges, 77 communities)
- **Soren status:** ⬜ PENDING — flag for next COHK (note: LLM API key dependency for extraction phase)
- **ML record:** Section 5 → Tier 1 → `report-graphify.md`
- **Primary use:** Knowledge graph construction from document corpora; enables semantic query instead of bulk file reads at session start
- **Status:** ✅ ACTIVE

---

### 19. Camofox Browser
- **Type:** CLI — npm global + REST API server (stealth headless browser for AI agents)
- **Version:** v2.4.5
- **Install command:** `npm install -g camofox-browser`
- **Location:** npm global; server binds to `127.0.0.1` (localhost only — hardcoded default; network exposure without API key structurally blocked at startup)
- **Soren status:** CLEARED WITH CONDITIONS — localhost-only default confirmed safe (source-verified); auth enforcement confirmed in source (`assertServerExposureSafety()` throws on non-loopback without API key); single-maintainer watch item. Full clearance record: `report-camofox-browser.md`
- **ML record:** Section 10 → Alternative Tools & Notable Ecosystem → Tier 2 → `report-camofox-browser.md`
- **Primary use:** Stealth browser automation for bot-protected targets (Cloudflare challenges, fingerprint detection, anti-scraping middleware). **Routing rule: Playwright first → Camofox when bot-detection/Cloudflare blocks Playwright.**
- **Skill:** `~/.claude/skills/camofox-browser/SKILL.md` — CLI commands and server lifecycle documented (Session 245)
- **Session installed:** 245 (2026-06-12)
- **Status:** ✅ ACTIVE

---

### 20. HyperFrames
- **Type:** CLI (npm) — HTML-to-video agent-first rendering framework (HeyGen)
- **Version:** v0.6.95 — **PINNED** (`@hyperframes/core@0.6.95` + `hyperframes@0.6.95`; breaking changes expected at v1.0; do not upgrade without Soren review)
- **Install command:** `npm install @hyperframes/core hyperframes` → `C:\ClaudeTools\HyperFrames\` (local install; CLI at `C:\ClaudeTools\HyperFrames\node_modules\.bin\hyperframes`)
- **MCP status:** NOT in v0.6.95 — `mcp` subcommand absent from CLI; `@hyperframes/mcp` not yet on npm. MCP registration deferred — revisit when MCP support ships in a future release.
- **Dependencies:** Node.js (present), FFmpeg (present — system binary used by HyperFrames), Puppeteer (auto-installs second Chromium binary; expected, no security concern)
- **Soren status:** CLEARED WITH CONDITIONS — core/engine/CLI cleared; cloud adapters (aws-lambda, gcp-cloud-run packages) **NOT cleared** — require individual review before any cloud deployment. Full clearance record: `report-hyperframes.md`
- **ML record:** Section 10 → Alternative Tools & Notable Ecosystem → Tier 2 → `report-hyperframes.md`
- **Primary use:** Agent-generated video (HTML/CSS-to-MP4, data cards, presentation sequences). **Routing rule: HyperFrames first → Remotion only for developer-authored complex motion design in React code.**
- **Skill:** `~/.claude/skills/hyperframes/SKILL.md` — CLI render workflow documented; MCP deferred (Session 245)
- **Session installed:** 245 (2026-06-12)
- **Status:** ✅ ACTIVE

---

### 21. RAG-Anything
- **Type:** Python library — pip package (multimodal RAG framework built on LightRAG + MinerU; no CLI entry points)
- **Version:** v1.3.1
- **Install command:** `pip install raganything`
- **Location:** `C:\Users\jlacerda\AppData\Local\Programs\Python\Python313\Lib\site-packages\raganything\`
- **Soren status:** CLEARED — 0 CVEs (Trivy scan Session 245); same trusted org as LightRAG (HKUDS); MIT-compatible license. Full clearance record: `report-rag-anything.md`
- **Dependency note:** 3 downgrades at install: pandas 3.0.3→2.3.3, huggingface_hub 1.17.0→0.36.2, tokenizers 0.23.1→0.22.2. No CVEs introduced — monitor if tools relying on huggingface_hub 1.x exhibit unexpected behavior.
- **ML record:** Section 8 → Alternative Tools & Notable Ecosystem → Tier 3 → `report-rag-anything.md`
- **Primary use:** Multimodal RAG for mixed-format document corpora (PDFs with charts, tables, equations, images). **Routing rule: RAG-Anything (multimodal default) → LightRAG (text-primary/text-only fallback).**
- **Skill:** `~/.claude/skills/rag-anything/SKILL.md` — Python API documented; ingest/query patterns; MinerU first-run note (Session 245)
- **Session installed:** 245 (2026-06-12)
- **Status:** ✅ ACTIVE

---

### 22. context-mode
- **Type:** MCP — Node (npx, mksglu) — context-window virtualization layer
- **Version:** v1.0.162 (daily release cadence; npx pulls latest on each run)
- **Config location:** `.mcp.json` at project root
- **Entry:**
  ```json
  "context-mode": {
    "command": "cmd",
    "args": ["/c", "npx", "-y", "context-mode"]
  }
  ```
- **No API key required**
- **Transport:** stdio. `cmd /c` wrapper is the Windows-host launch form (live config differs from the report's `npx -y context-mode` snippet).
- **Tool count:** 11 (6 sandbox + 5 meta/utility); `ctx_search` is the session-start retrieval tool (replaced the dropped claude-mem timeline, Session 251)
- **Soren status:** CLEARED — Active Deployment Confirmed (re-review 2026-06-08; upgraded from FLAG — Review Before Install). ELv2 license — acceptable for internal/personal use; single maintainer (mksglu) — abandonment risk resolved by daily release cadence; SQLite local storage — no data leaves machine.
- **ML record:** Section 6 → MCP → Built → `context-mode-mcp-config-record.md` (written Session 265)
- **Primary use:** Context-window virtualization and session continuity across compactions — intercepts raw outputs (file reads, API calls, shell, code) and passes only compressed summaries into context (documented ~98% reduction). Active in the P7 session-start + context-discipline stack.
- **Status:** ✅ ACTIVE

---

## Removed — History

Tools that were installed and later removed. Retained here as historical record only — they are **not** counted in the live Summary table above. Each tool's research report has been evicted from `0. Resources Installed\` to its category folder (a removed tool is not an installed resource).

---

### R1. mcp-youtube (removed)
- **Type:** MCP — Python (uvx)
- **Version:** 0.2.0
- **Config location (former):** `.mcp.json` at project root
- **Entry (former):**
  ```json
  "mcp-youtube": {
    "command": "uvx",
    "args": ["mcp-youtube"]
  }
  ```
- **No API key required**
- **Dependency check:** h11 0.16.0 ✓, mcp 1.27.2 ✓ — all conditions met
- **Trivy scan:** CVEs in dev lock only — resolved clean via uvx
- **Soren status:** CLEARED WITH CONDITIONS (Session 216) — conditions met
- **Session wired:** 218 (2026-06-04)
- **ML record:** N/A — `mcp-youtube-config-record.md` was never written (config record MOOT for a removed tool; confirmed disk-truth sweep Session 259). Removal documented via report rename.
- **Report home (NEW):** `Model Context Protocol (MCP)\Research Reports\report-mcp-youtube-removed.md` (evicted from Resources Installed — Session 265)
- **Status:** ❌ REMOVED — Session 222 (failed in testing; get_youtube_transcript non-functional; replaced by transcribe-anything)

---

### R2. claude-mem (removed)
> ❌ **REMOVED — Session 251.** Installed S239, never functional (Bun worker blocked/uninitialized on this host); uninstalled completely (plugin + thedotmack marketplace + auto-update + `~/.claude-mem` data + self-heal hook). Function was redundant — covered by claude-remember + context-mode + Graphify + Session Summary. Details below are historical. Removal plan: `~/.claude/plans/that-took-away-to-validated-sunrise.md`.
- **Type:** Plugin — Claude Code (persistent memory MCP + observation system)
- **Version:** 13.5.6
- **Plugin ID:** `claude-mem@thedotmack`
- **Install command:** Claude Code plugin marketplace
- **Install location:** `C:\Users\jlacerda\.claude\plugins\cache\thedotmack\claude-mem\13.5.6\`
- **Scope:** User-level (applies across all projects)
- **Soren status:** CLEARED with licensing flag (AGPL-3.0 main + PolyForm Noncommercial sub-component — commercial deployment requires separate Ragtime license)
- **Session installed:** 239 (2026-06-11, P7 memory stack)
- **ML location:** Section 1 → Tier 2 (with Soren licensing flag) — ML catalogs marked REMOVED (S251)
- **Report home (NEW):** `Claude - Plugins\Research Reports\report-claude-mem-removed.md` (evicted from Resources Installed — Session 265)
- **Status:** ❌ REMOVED — Session 251

**Note:** Installed as part of P7 memory stack (Session 239); removed completely Session 251 (never functional; redundant). The running memory stack is now MEMORY.md (strategic) + claude-remember (session narrative) + context-mode + Graphify.

---

## Open Items

| # | Item | Owner | When |
|---|------|-------|------|
| 1 | ElevenLabs MCP — mcp version gap ✅ RESOLVED (Session 219 — forced >=1.23.0 via uvx --with) | — | Done |
| 2 | ElevenLabs API key ✅ RESOLVED (Session 219 — added; .mcp.json untracked from git) | — | Done |
| 3 | MoneyPrinterTurbo — pillow CVEs (3 HIGH, 3 MEDIUM) | Soren | Next COHK |
| 4 | Trivy + Gitleaks — PATH ✅ RESOLVED (Session 219); pipeline integration + pre-commit hook still pending | Soren | Next COHK |
| 5 | Remotion — commercial license review + re-file to Vicky's ML section | Soren → Lexi | When Vicky activates on a video project |
| 6 | transcribe-anything — Rose freshness pass (report cites v3.2.10; actual install is v4.0.0) | Rose | Next research pass |
| 7 | Remotion npm vulns (2 low severity) | Soren | Next COHK |
| 8 | ffmpeg — Soren formal clearance + PATH confirmation | Soren | Next COHK |
| 9 | Obsidian — Soren formal clearance | Soren | Next COHK |
| 10 | claude-remember — Soren formal clearance | Soren | Next COHK |
| 11 | Graphify — Soren formal clearance (note: LLM API key dependency) | Soren | Next COHK |
| 12 | claude-mem — REMOVED Session 251 (closed — ML "Built" update moot; ML catalogs marked REMOVED) | Lexi | Closed S251 |

---

*Created Session 218 return — 2026-06-04*
*Updated Session 227 — 2026-06-07: ffmpeg (#12) added — installed during MKT 311 production (Sessions 221–225); Soren review + ML record pending.*
*Updated Session 232 — 2026-06-09: Mermaid CLI (#13) added — npm install to C:\ClaudeTools\mermaid-cli\; v11.15.0; CLEARED (Soren live scan clean); mmdc.cmd verified.*
*Updated Session 233 — 2026-06-09: Humanizer (#14) added — npx skills add global; blader/humanizer; CLEARED (Soren — Session 60, re-confirmed 2026-06-08); active in ~/.claude/skills/humanizer.*
*Updated Session 237 — 2026-06-10: opendataloader-pdf (#15) added — pip install; v2.4.7; pre-cleared Tier 2 Apache 2.0 (Feynman S234); Java 25.0.3 (Temurin) confirmed as runtime; Trivy 0 CVEs.*
*Updated Session 242 — 2026-06-11: claude-mem (#10) status corrected to ACTIVE (v13.5.6; installed Session 239 P7 memory stack); ffmpeg (#12) version confirmed (v8.1.1) + full detail section added; Obsidian (#16), claude-remember (#17), Graphify (#18) added — all P7 memory stack installs (Session 239); reports filed in 999. MU-IP Installed; Open Items 8–12 added (Soren pending for 4 tools + claude-mem ML record update).*
*Updated Session 244 — 2026-06-12: Camofox Browser (#19), HyperFrames (#20), RAG-Anything (#21) added as ⏳ PENDING INSTALL; routing rules documented; research reports placed in 999. MU-IP Installed.*
*Updated Session 245 — 2026-06-12: #19/#20/#21 updated to ✅ ACTIVE; install locations, skill files, and Soren clearance details documented; HyperFrames MCP deferred (not in v0.6.95); Items 171/172/173 closed in Pending Changes.*
*Updated Session 251 — 2026-06-13: claude-mem (#10) REMOVED completely — never functional (Bun worker blocked/uninitialized); uninstalled (plugin + thedotmack marketplace + auto-update + `~/.claude-mem` data + self-heal hook); all references scrubbed across all prior environments. Open Item #12 closed (ML "Built" update moot). Function covered by claude-remember + context-mode + Graphify + Session Summary.*
*Updated Session 252 — 2026-06-14: mcp-youtube detail section status corrected to ❌ REMOVED (was showing ✅ ACTIVE); report-claude-mem.md renamed to report-claude-mem-removed.md; master list reference updated.*
*Updated Session 265 — 2026-06-20 (P7 end-pass, Phase B): context-mode promoted to Summary #22 + full Detail section (✅ ACTIVE; MCP via `cmd /c npx -y context-mode`; Soren CLEARED — active deployment); config record written at `Built - MCP Folder\context-mode-mcp-config-record.md`. New "Removed — History" section added — mcp-youtube (#4) and claude-mem (#10) detail blocks relocated there (R1/R2) and removed from the live Summary table so it reflects installed tools only; each report's NEW home recorded (mcp-youtube-removed → MCP category; claude-mem-removed → Plugins category). Install count of live tools unchanged.*
*Updated Session 265 — 2026-06-20 (P7 end-pass, Phase C): #13 Mermaid CLI Detail section added (was missing — Summary row + report-mermaid-cli.md existed but no Detail block; Stage-1 straggler). report→Detail parity now resolves for all installed tools.*
*Updated Session 270 — 2026-06-23: Hygiene — ElevenLabs MCP config snippet (#6) literal key slot `ADD_KEY_HERE` replaced with neutral note `[API key configured in .mcp.json, untracked]`. Install record otherwise intact; no records removed. Updated by Sophia — COO.*
*Sophia reviewed. Sage approved.*
