# Research Report — Mermaid CLI & Free Alternatives

**Report by:** Rose — Research Specialist
**Output Type:** Resource Report
**Date:** 2026-05-13
**Task Source:** Sage — Session 144 (Item 91)
**Routing:** Sage → Soren (security review) → Lexi (catalog)

---

## 1. Task Summary

Research the Mermaid CLI (`mmdc`, package `@mermaid-js/mermaid-cli`) — what it is, how it works, licensing and pricing, current version and maintenance health, installation and usage, and security posture. Additionally, survey the best free and open-source alternatives for generating diagrams from text or code (PlantUML, Graphviz, D2, others) with a brief comparison. Deliverable is a Resource Report routed to Soren for security review.

---

## 2. Output Type

**Resource Report.** Mermaid CLI is an installable npm package that runs as a local command-line tool (`mmdc`). It is deployable, not informational. Per team protocol, any installable/deployable resource routes as a Resource Report regardless of free/open-source status. Routes to Soren before Lexi.

---

## 3. Findings

### 3a. Mermaid CLI

#### What It Is and What It Does

Mermaid CLI (`mmdc`) is the command-line interface for the Mermaid.js diagramming library. It takes a Mermaid diagram definition file (`.mmd`) or a Markdown file as input and renders it to SVG, PNG, or PDF output. It is the primary way to use Mermaid in automated pipelines, CI/CD, documentation builds, and server-side rendering workflows where a browser is not present.

Under the hood, Mermaid CLI drives a headless Chromium instance (via Puppeteer) to render diagrams — this is why it has significant dependency weight and why Docker/sandbox issues arise on some environments.

#### Package Details

- **npm package name:** `@mermaid-js/mermaid-cli` (the correct, active package)
- **Deprecated package:** `mermaid.cli` — older package, no longer maintained, do not use
- **Current version:** 11.15.0 (released May 13, 2026 — CVE fix release; see Security Notes update)
- **Mermaid library dependency:** `^11.15.0` (updated in v11.15.0 release — CVE fix included)
- **GitHub repository:** `github.com/mermaid-js/mermaid-cli`
- **Total releases:** 78 versions published
- **Repository activity:** 1,050 commits; 82 open issues; 5 open PRs

#### License and Pricing

- **License:** MIT License — permissive, free for commercial and non-commercial use, no restrictions on redistribution or modification
- **Pricing:** 100% free. No paid tiers. No commercial restrictions.
- **Mermaid Chart (separate):** A commercial SaaS product (`mermaidchart.com`) exists for collaborative/hosted diagram editing. This is a distinct product — it does not affect the CLI's open-source status or licensing. The CLI is not connected to Mermaid Chart.

#### Installation and Usage

**Global install (recommended for regular use):**
```bash
npm install -g @mermaid-js/mermaid-cli
mmdc -i input.mmd -o output.svg
```

**One-off via npx (no install required):**
```bash
npx -p @mermaid-js/mermaid-cli mmdc -i input.mmd -o output.svg
```
Note: the `-p` flag is required because the package name (`@mermaid-js/mermaid-cli`) differs from the command it installs (`mmdc`).

**Docker (avoids Chromium sandbox issues on Linux):**
```bash
docker run --rm -u $(id -u):$(id -g) -v /path/to/diagrams:/data minlag/mermaid-js-renderer
```

**Key CLI flags:**
- `-i <file>` — input file (`.mmd` or `.md`)
- `-o <file>` — output file (`.svg`, `.png`, or `.pdf`)
- `-t <theme>` — theme: `default`, `forest`, `dark`, `neutral`
- `-b <color>` — background color (e.g., `transparent`, `white`, `#hex`)
- `-w <width>` — page width in pixels
- `-H <height>` — page height in pixels
- `--configFile <file>` — JSON config file for Mermaid settings
- `--cssFile <file>` — custom CSS file
- `--scale <factor>` — PNG pixel density scale factor

**Supported input diagram types:** Flowcharts, sequence diagrams, class diagrams, state diagrams, ER diagrams, Gantt charts, Git graphs, pie charts, journey maps, C4 diagrams, Venn diagrams (added in 11.14.0), and more.

**Supported output formats:** SVG (default, best quality), PNG (rasterized), PDF

**Markdown transformation mode:** Can process a full Markdown file, replacing all ` ```mermaid ` blocks with rendered images inline.

#### Maintenance Health

- **Status:** Actively maintained
- **Latest release:** v11.15.0, May 13, 2026 — CVE fix release (mermaid library upgraded to 11.15.0, resolving four CVEs); previously v11.14.0 (April 29, 2026) added Venn diagram support and ESM performance improvements
- **Release cadence:** Regular — 78 releases across the project's history
- **Community signals:** The core mermaid library (`mermaid`) has 74,000+ GitHub stars and 6,800+ forks — extremely popular and well-supported ecosystem

---

### 3b. Free Alternatives

| Tool | License | CLI Support | Language/Runtime | Key Strengths | Key Limitations |
|---|---|---|---|---|---|
| **PlantUML** | GPL (default); LGPL/MIT/Apache also available | Yes — Java JAR, `plantuml.jar` | Java | Mature (est. 2009); widest diagram type coverage; widely integrated; free commercial use under LGPL; latest v1.2025.2 | Requires Java runtime; syntax can be verbose; slower rendering |
| **Graphviz** | Eclipse Public License 2.0 | Yes — `dot`, `neato`, `fdp`, `circo`, `twopi` | C | Extremely powerful graph layouts; handles very large graphs; decades of maturity; current v14.x series (Sept 2025) | No UML support; DOT syntax not human-friendly; visual output less polished |
| **D2** | Mozilla Public License 2.0 (MPL-2.0) | Yes — `d2` binary | Go | Modern (est. 2022); clean syntax; responsive dark mode; native GitHub rendering; strong error messages; 23,700+ GitHub stars; v0.7.1 (Aug 2025) | Younger ecosystem; smaller integration surface than PlantUML; PDF export requires extra setup |
| **Kroki** | MIT | Yes — self-hosted API server | Multi-engine (Docker) | One unified API supporting 20+ diagram engines (Mermaid, PlantUML, Graphviz, D2, etc.); useful for teams using multiple tools | Not a standalone renderer — wraps other tools; requires Docker/server to self-host |

**Brief assessment by use case:**
- **Documentation pipelines / CI:** Mermaid CLI is the easiest integration for Markdown-native workflows. D2 is the strongest modern alternative.
- **Complex UML diagramming:** PlantUML has the broadest UML coverage and longest track record.
- **Pure graph/network diagrams:** Graphviz has no peer for complex directed/undirected graph layouts.
- **Multi-engine environments:** Kroki is the right abstraction if a team already uses multiple diagram formats.

---

### 3c. Security Notes

**This section is the primary handoff to Soren.**

#### CVE STATUS UPDATE (2026-06-08 Freshness Sweep)

**mermaid-cli v11.15.0 was released on May 13, 2026** — the same day as this report. The four CVEs documented below are **RESOLVED** in v11.15.0. Soren should scan v11.15.0 before approving installation (full pipeline required — do not treat the CVE resolution as automatic clearance).

#### Previously CRITICAL — Four CVEs in v11.14.0 (RESOLVED in v11.15.0)

These CVEs were present in v11.14.0 (the version at report time). All four are fixed in v11.15.0, which upgrades the bundled mermaid library to 11.15.0.

**Affected CVEs (all fixed in mermaid 11.15.0 / mermaid-cli v11.15.0):**

| CVE | Severity | Description | Status |
|---|---|---|---|
| CVE-2026-41159 | HIGH (7.1) | CSS injection via `fontFamily`, `themeCSS`, `altFontFamily` config params — CSS escapes diagram boundary | Fixed v11.15.0 |
| CVE-2026-41148 | HIGH (7.1) | CSS injection via `classDefs` — enables page defacement, user tracking, DOM attribute exfiltration | Fixed v11.15.0 |
| CVE-2026-41149 | HIGH (7.1) | HTML injection via `classDef` in state diagrams — DOM injection, breaks out of SVG context | Fixed v11.15.0 |
| CVE-2026-41150 | MEDIUM (4.7) | Gantt chart infinite loop DoS — `excludes` attribute eliminating all dates causes crash | Fixed v11.15.0 |

**CVSS vector (all HIGH severity):** `AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:L`
**Weakness classifications:** CWE-94 (Code Injection) for three; CWE-835 (Infinite Loop) for one

**Next step for Soren:** Run full security pipeline scan against v11.15.0. CVE fix is confirmed shipped — this resource is ready for Soren's formal clearance review.

#### General Security Posture

- **Supply chain:** Mermaid CLI depends on Puppeteer (headless Chromium) — a large dependency surface area. Standard tradeoff for browser-based rendering but worth noting for air-gapped or restricted environments.
- **Chromium sandboxing:** Documented known issues with Linux sandbox configuration. On some Linux environments, the `--no-sandbox` flag may be required, which reduces Chromium's process isolation. Documented tradeoff, not a vulnerability, but Soren should confirm the deployment context.
- **Docker permission issues:** Also documented in the repository. Mitigated by using the official Docker image and correct user flag (`-u $(id -u):$(id -g)`).
- **No npm supply chain compromise:** Snyk reports no known vulnerabilities directly in the `@mermaid-js/mermaid-cli` package itself — the risks are in its bundled mermaid library dependency (above).
- **Old mermaid.cli package:** The legacy `mermaid.cli` npm package is deprecated, unmaintained (last updated 11 years ago), Snyk health score 36/100. Do not use — it is not the same as `@mermaid-js/mermaid-cli`.
- **License flags:** MIT license. No GPL, LGPL, or copyleft obligations. No commercial restrictions. Clean for enterprise use.

---

## Soren Security Review

- **Verdict: CLEARED**
- **Reviewed by:** Soren | 2026-06-08 (advisory review) → 2026-06-09 (live scan — final clearance)
- **Previous status:** CLEARED WITH CONDITIONS — PENDING LIVE SCAN
- **Status change reason:** Live pipeline scan (Trivy + Gitleaks) completed 2026-06-09. Both scans returned clean. All conditions met. Resource is cleared for installation.

**What I reviewed:**
- Rose's full security notes section, including CVE documentation with CVSS vectors and CWE classifications
- CVE fix confirmation: mermaid library upgraded to 11.15.0 in the cli package, directly resolving all four vulnerabilities
- General security posture: Puppeteer/Chromium dependency noted; supply chain concern is a known architectural tradeoff, not a new finding; npm supply chain confirmed clean by Snyk per Rose's research
- License: MIT — clean
- **Live Trivy scan (2026-06-09):** `@mermaid-js/mermaid-cli@11.15.0` installed (355 packages). Trivy v0.71.0, DB updated 2026-06-09. Scanned `package-lock.json` (full dependency tree). Result: **0 vulnerabilities** — UNKNOWN: 0, LOW: 0, MEDIUM: 0, HIGH: 0, CRITICAL: 0.
- **Live Gitleaks scan (2026-06-09):** Gitleaks v8.30.1, `--no-git` mode. Scanned 71.11 KB of mermaid-cli source (`dist/`, `dist-types/`, `src/`, `LICENSE`, `package.json`, `README.md`). Result: **no leaks found**.

**What changed from HOLD:**
The original HOLD was issued because four CVEs (three HIGH CSS/HTML injection, one MEDIUM DoS) were present in v11.14.0, the version available at report time. v11.15.0 shipped the same day as the original report and fixes all four. Rose's 2026-06-08 freshness sweep confirmed the fix is in the released version. The blocking condition is cleared. Live scan on 2026-06-09 confirms no new vulnerabilities introduced and no secrets embedded in the published package source.

**Remaining conditions (carried forward for installation):**
1. ~~Run full pipeline scan (Trivy + Gitleaks) against v11.15.0 before installation.~~ **COMPLETE — 2026-06-09. Both scans clean.**
2. Use `@mermaid-js/mermaid-cli` only — do not install the deprecated `mermaid.cli` package (Snyk health score 36/100, unmaintained).
3. Confirm deployment context: npm global install or Docker (`minlag/mermaid-js-renderer`). Security surface area differs — Docker is preferred for CI/server environments; npm global is acceptable for local agent use. Chromium `--no-sandbox` flag must not be used on production systems without explicit acknowledgment of the reduced process isolation.
4. Do not install v11.14.0 under any circumstances — the four CVEs are unpatched in that version.

**Notes:** Live scan completed 2026-06-09 using Trivy v0.71.0 (DB updated same day) and Gitleaks v8.30.1. Full 355-package dependency tree scanned with zero findings. This resource is clean and ready for library entry. The mermaid ecosystem (74,000+ core library stars) is one of the most established in the documentation tooling space.

---

## 4. C&P Summary

Mermaid CLI is a free, open-source command-line tool (MIT license) that converts text-based diagram definitions into SVG, PNG, or PDF images. It is installed via npm and run as `mmdc`. It has no paid tiers, no commercial restrictions, and is actively maintained by the mermaid-js community. Current release is v11.15.0 (May 13, 2026).

**Security posture update (2026-06-09 — CLEARED):** The four CVEs documented in this report (three HIGH CSS/HTML injection, one MEDIUM DoS) that were present in v11.14.0 have been resolved in v11.15.0. Live Trivy + Gitleaks scan completed 2026-06-09: 0 vulnerabilities across 355 packages, no secrets found. Soren verdict: **CLEARED**. Do not install v11.14.0 — use v11.15.0 only.

For alternatives: D2 (MPL-2.0, modern, Go-based, actively maintained, no known vulnerabilities) and PlantUML (GPL/LGPL, mature, Java-based, broadest UML coverage) are both strong free options. Graphviz (EPL-2.0) remains the gold standard for pure graph/network layouts. Kroki is a meta-wrapper that unifies multiple engines under one API, useful if the team already uses several tools.

---

## 5. Sources

1. GitHub — mermaid-js/mermaid-cli repository: https://github.com/mermaid-js/mermaid-cli (accessed 2026-05-13)
2. GitHub — mermaid-js/mermaid-cli releases: https://github.com/mermaid-js/mermaid-cli/releases (accessed 2026-05-13)
3. npm — @mermaid-js/mermaid-cli package: https://www.npmjs.com/package/@mermaid-js/mermaid-cli (accessed 2026-05-13)
4. mermaid-cli package.json — confirmed `"mermaid": "^11.14.0"` via GitHub source (accessed 2026-05-13)
5. GitLab Advisory Database — CVE-2026-41159: https://advisories.gitlab.com/npm/mermaid/CVE-2026-41159/ (accessed 2026-05-13)
6. GitLab Advisory Database — CVE-2026-41148: https://advisories.gitlab.com/npm/mermaid/CVE-2026-41148/ (accessed 2026-05-13)
7. GitLab Advisory Database — CVE-2026-41149: https://advisories.gitlab.com/npm/mermaid/CVE-2026-41149/ (accessed 2026-05-13)
8. GitLab Advisory Database — CVE-2026-41150: https://advisories.gitlab.com/npm/mermaid/CVE-2026-41150/ (accessed 2026-05-13)
9. Snyk — mermaid-cli vulnerability database: https://security.snyk.io/package/npm/mermaid-cli (accessed 2026-05-13)
10. Snyk — mermaid vulnerability database: https://security.snyk.io/package/npm/mermaid (accessed 2026-05-13)
11. mermaid.js official documentation: https://mermaid.js.org/config/mermaidCLI.html (accessed 2026-05-13)
12. PlantUML FAQ and licensing: https://plantuml.com/faq (accessed 2026-05-13)
13. PlantUML command line documentation: https://plantuml.com/command-line (accessed 2026-05-13)
14. Chocolatey — PlantUML v1.2025.2: https://community.chocolatey.org/packages/plantuml (accessed 2026-05-13)
15. GitHub — terrastruct/d2: https://github.com/terrastruct/d2 (accessed 2026-05-13)
16. GitHub — terrastruct/d2 LICENSE: https://github.com/terrastruct/d2/blob/master/LICENSE.txt (accessed 2026-05-13)
17. Graphviz official site: https://graphviz.org/ (accessed 2026-05-13)
18. Graphviz license page: https://graphviz.org/license/ (accessed 2026-05-13)
19. Chocolatey — Graphviz 14.1.5: https://community.chocolatey.org/packages/Graphviz (accessed 2026-05-13)
20. Text-to-diagram tools comparison: https://text-to-diagram.com/?example=text (accessed 2026-05-13)
21. Swimm — Top 6 Mermaid.js alternatives: https://swimm.io/learn/mermaid-js/top-6-mermaid-js-alternatives (accessed 2026-05-13)
22. Kroki unified diagram renderer: https://kroki.io/ (accessed 2026-05-13)
23. Wikipedia — Mermaid software: https://en.wikipedia.org/wiki/Mermaid_(software) (accessed 2026-05-13)

---

## 6. Additional Findings

**A. Four CVEs, not two — broader scope than initial search suggested**
Initial search surfaced two CVEs. Follow-up confirmed two additional in the same batch fix: CVE-2026-41149 (HTML injection in state diagrams, HIGH) and CVE-2026-41150 (Gantt chart DoS, MEDIUM). All four fixed in mermaid 11.15.0. Soren should be briefed on all four.

**B. Mermaid Chart (SaaS) vs. Mermaid CLI (open source) — common confusion point**
There is widespread confusion in the ecosystem between the open-source Mermaid library/CLI and the commercial "Mermaid Chart" product at mermaidchart.com. These are separate products. The CLI is pure MIT. Mermaid Chart has its own pricing and terms. Any future documentation or onboarding material should clarify this distinction to avoid licensing misread.

**C. Skill candidate flag**
The research pattern used here — "CLI tool intake: current version + license + CVE sweep + alternatives comparison" — is repeatable. This is the standard template Rose runs on every candidate tool. Worth surfacing to Sage for Cosmo to evaluate as a formal research skill template or checklist. Not building it here — Cosmo's lane.

**D. mermaid-cli dependency on Puppeteer / headless Chromium**
For teams building in Docker or CI environments, the Puppeteer/Chromium dependency is the single largest operational friction point. The official Docker image (`minlag/mermaid-js-renderer`) handles this cleanly and is the recommended path for CI use. Soren should confirm whether the team will use npm global install or Docker, as the security surface area differs.

**E. D2's TALA layout engine — commercial note**
D2 itself (MPL-2.0) is fully free. However, Terrastruct also offers TALA, a proprietary advanced auto-layout engine, as a paid add-on. TALA is optional — D2's built-in layout engines are free and capable. This is the one commercial component in the D2 ecosystem and does not affect the tool's free-and-open status for the team's likely use cases.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---
*Keep-both pair (S264): this is the **full research report** (incl. free-alternatives survey). Install/deployment record → `0. Resources Installed/report-mermaid-cli.md`.*
