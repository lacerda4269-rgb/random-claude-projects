# Resource Report: Stirling-PDF

**URL:** https://github.com/Stirling-Tools/stirling-pdf
**Date Researched:** 2026-04-21
**Researched by:** Rose | Security pre-check: Soren (2026-06-12) | Report by: Rose
**Already in Master Library?** No

---

## What It Is

Stirling-PDF is a self-hosted, open-source PDF manipulation platform — the most-starred PDF application on GitHub. It provides 60+ PDF tools (merge, split, convert, compress, OCR, sign, redact, rotate, watermark, and more), all running locally without sending files to any external server. Operates as a web-based tool, a Docker container, a desktop client, or a self-hosted server with a full REST API. Created in January 2023 by Anthony Stirling, a UK-based developer who built the first version in a single day after refusing to pay Adobe to sign a PDF. The project has since grown to 77,300+ GitHub stars, 6.7k forks, 25M+ downloads, 150+ contributors, and $2M in funding.

## What It Does

Complete browser-based or API-accessible PDF operations suite:

- **Document manipulation:** merge, split, rotate, reorder, extract pages, compress, repair, flatten
- **Conversion:** PDF to/from Word, Excel, PowerPoint, image formats, HTML, Markdown
- **Content editing:** add/edit text, images, watermarks, headers/footers, page numbers
- **Security:** add/remove passwords, redact content, sign with digital signatures, sanitize metadata
- **OCR:** extract text from scanned PDFs via Tesseract integration
- **Forms:** fill and extract PDF form data
- **Automation:** no-code workflow pipelines built in the UI; REST API available for nearly all tools to enable programmatic batch processing

All file processing is local — files exist in-memory during operations and are deleted immediately after download. Nothing transmitted to external services.

## Who Built It

Founded by Anthony Stirling (UK developer) in January 2023. Now maintained by the Stirling-Tools GitHub organization with 150+ contributors. Backed by Open Core Ventures with $2M in funding. The project has grown from a personal tool into a full company — Stirling PDF Inc. — pursuing an open-core business model with free self-hosted tiers and paid enterprise/SaaS plans.

## Activity Level

- **Stars:** 80,400+
- **Forks:** 6,700+
- **Releases:** 178 total; latest v2.11.0 (May 19, 2026)
- **Docker pulls:** 25M+
- **Activity:** Extremely active. Releases ship continuously. Community is large and engaged. One of the highest-starred self-hosted tools on GitHub.
- **Updated:** 2026-06-08

## License

Open-core model. The base repository uses MIT as the foundation but with tiered exceptions: several subdirectories (`app/proprietary/`, `engine/`, `frontend/src/proprietary/`, `desktop/`, `saas/`, `prototypes/`) carry separate proprietary license files. The self-hosted community edition is free. Enterprise features (SSO, auditing, advanced on-prem deployments) require paid plans. For plain self-hosted personal or team use without enterprise features, the MIT-based open portion applies cleanly.

## Dependencies / Tech Stack

- **Backend:** Java 21+ (JDK 25 recommended), Spring Boot, Spring Security (optional), Lombok
- **PDF processing:** Apache PDFBox (merge, split, rotate, in-memory operations), LibreOffice (document format conversions), qpdf (PDF optimization), Tesseract (OCR)
- **Frontend:** React SPA (TypeScript 47.8% of codebase)
- **Build system:** Gradle (multi-module)
- **Containerization:** Docker; multiple image variants — standard, fat (highest quality conversions), ultra-lite (minimal hardware)
- **API:** Stateless REST API under `/api/v1/*`; JWT authentication when auth is enabled

## How It Works

User requests flow from the React frontend to Spring Boot backend controllers, through a service layer, to external processing tools (PDFBox, LibreOffice, Tesseract, qpdf), and back. PDF operations run in-memory using PDDocument objects; large files are streamed to avoid memory issues. The system is configuration-driven — environment variables and a `settings.yml` file bind to Java objects at startup. Docker is the recommended deployment path. A workflow pipeline builder (no-code) allows chaining multiple PDF operations into automated sequences via the UI. The REST API mirrors every UI tool for programmatic use.

## Relevance to This Project

Practical infrastructure. Any project that generates, processes, or handles PDFs — contracts, reports, government documents — could use Stirling-PDF as a local, private, zero-cost alternative to Adobe Acrobat or cloud PDF services. Not an AI or agent tool — purely document infrastructure. Catalog now; deploy when the project needs PDF handling.

## Builder Footprint

- **Integration type:** Self-hosted web application — Docker container (recommended) or local Java 21+ install; REST API under `/api/v1/*`; no cloud dependency; stateless request/response model
- **Extension points:** Full REST API for programmatic access to all 60+ PDF tools; workflow pipeline builder (no-code, UI-based) for chaining operations; JWT auth optional when auth is enabled; environment variables and `settings.yml` for configuration; multiple Docker image variants (standard, fat for highest quality conversions, ultra-lite for minimal hardware)
- **Build complexity signal:** Low-to-Medium for Docker path (docker pull + run + port mapping); Medium for non-Docker Java path (Java 21+ + Gradle build + LibreOffice + Tesseract installs for conversion and OCR features); Docker is the recommended path for minimal setup friction
- **Known conflicts:** Open-core license — MIT core applies to personal/team self-hosting; enterprise features (SSO, advanced auditing) require paid plan; confirm no enterprise features are needed before assuming full MIT coverage. LibreOffice dependency required for document format conversions (PDF↔Word/Excel/PowerPoint) — fat Docker image bundles this; standard image may require separate LibreOffice install for conversion tasks.

## Master Library Assessment

- **Proposed Section:** 8 — Alt Tools
- **Proposed Tier:** 1
- **Rationale:** Best-in-class open-source replacement for a common vendor dependency (Adobe/cloud PDF processors). 77k stars, 25M downloads, actively maintained, immediately deployable via Docker. Tier 1 because it is the leading option in its category by every metric. Section 8 is the right home for proven self-hosted infrastructure tools.

## Soren Security Pre-check

- **Verdict:** CLEARED WITH CONDITIONS
- **Checked:** GitHub Security Advisories API (all published advisories, 2026-06-12); OSV database (Maven + general search); NVD keyword search; OpenSSF Scorecard API v5.3.0 (scored 2026-06-11, commit 946c032); root LICENSE file (raw GitHub); SECURITY.md policy; repository commit activity and top-level directory tree.
- **Notes:** 10 published CVEs on record — all patched in versions well before the current v2.11.0. No open/unresolved advisories. Full CVE table below. License confirmed: MIT core applies cleanly to personal/team self-hosted use; proprietary subdirectories are enterprise-only extensions, confirmed absent from the core processing path. Data-handling claim (local-only, in-memory, deleted after download) is consistent with the architecture documentation and Spring Boot stateless REST model — no evidence of external transmission. OpenSSF Scorecard 7.4/10 (scored 2026-06-11): strong on maintenance, code review, dependency updates, security policy, token permissions, and dangerous-workflow checks. Partial weaknesses: no fuzzing (0/10), signed releases incomplete (4/10 — 2 of last 5 releases signed), branch protection not maximal (5/10), CII Best Practices in-progress (2/10). None of these represent active exploits or deployment blockers for self-hosted personal use. The scorecard "Vulnerabilities: 0/10 — 50 existing vulnerabilities detected" reflects transitive dependency tracking across the full ecosystem, not unpatched Stirling-PDF core issues; all 10 Stirling-PDF advisories show patched versions in the GitHub advisory record.

**Conditions:**
1. **Deploy at v2.11.0 or later** — do not run any version below v2.8.0. The HIGH-severity path traversal (v2.5.2) and stored XSS (v2.8.0) are the two most recent serious findings; both are patched at current release.
2. **Do not expose the web UI to the public internet without authentication enabled** — the SSRF vulnerabilities (fixed v1.1.0) were exploitable via unauthenticated API endpoints. For self-hosted personal/team use behind a local network or VPN, risk is low; public exposure requires auth enabled in config.
3. **Confirm no enterprise features needed before deployment** — MIT core is clean for personal/team use; SSO and audit features require a paid plan. No risk to basic self-hosted use.

**Known CVE History (all patched):**

| # | CVE | GHSA | Severity | CVSS | Summary | Fixed In |
|---|-----|------|----------|------|---------|----------|
| 1 | CVE-2026-27625 | GHSA-wccq-mg6x-2w22 | HIGH | 8.1 | Path Traversal via /api/v1/convert/markdown/pdf | v2.5.2 |
| 2 | CVE-2025-55161 | GHSA-ff33-grr6-rmvp | HIGH | 8.6 | SSRF via /api/v1/convert/markdown/pdf | v1.1.0 |
| 3 | CVE-2025-55151 | GHSA-76hv-h7g2-xfv3 | HIGH | 8.6 | SSRF via /api/v1/convert/file/pdf | v1.1.0 |
| 4 | CVE-2025-55150 | GHSA-xw8v-9mfm-g2pm | HIGH | 8.6 | SSRF via /api/v1/convert/html/pdf | v1.1.0 |
| 5 | CVE-2025-46568 | GHSA-998c-x8hx-737r | HIGH | — | SSRF + arbitrary file read | v0.45.0 |
| 6 | CVE-2026-33438 | GHSA-3932-2rfq-87xm | MEDIUM | 6.5 | DoS via add-watermark endpoint | v2.5.2 |
| 7 | CVE-2026-34071 | GHSA-xmhg-fv84-jgfc | MEDIUM | 5.4 | Stored XSS via EML-to-HTML export | v2.8.0 |
| 8 | CVE-2026-33436 | GHSA-q5j3-4m5w-wp75 | LOW | 3.1 | Reflected XSS via crafted filename in upload | v2.0.0 |
| 9 | CVE-2026-41580 | GHSA-rjjx-43g5-mp76 | LOW | 3.1 | Reflected XSS via PDF metadata fields | v2.0.0 |
| 10 | CVE-2024-52286 | GHSA-9j55-gvf2-cqwv | LOW | — | Self-XSS in Merge functionality | v0.32.0 |

All 10 advisories patched. Current release v2.11.0 is clear of all listed CVEs.

## Recommendation

Enter the library in Section 8 at Tier 1. No install now — catalog for future reference when PDF handling becomes a project requirement. If any phase involves processing PDFs (contracts, signed documents, report exports), Stirling-PDF is the recommended default over any cloud service. Docker deployment is straightforward.

---

## C&P Summary

Stirling-PDF is a free, self-hosted tool that gives you over 60 PDF functions — merge files, split them, convert to and from Word or Excel, add passwords, remove them, sign documents, compress, extract text, redact information, and more — all running on your own computer or server. Nothing gets uploaded to the internet; every file stays local and is deleted as soon as you are done. It started in 2023 when a developer named Anthony Stirling needed to sign a PDF, refused to pay Adobe, built his own tool in a day, and posted it on Reddit. It now has over 80,000 GitHub stars and 25 million Docker pulls (updated 2026-06-08), making it the most popular open-source PDF tool on the internet. For this project, it is worth keeping in the library for any moment a PDF needs to be processed — contracts, government documents, signed agreements — as a free, private, and fully self-controlled alternative to Adobe or any online PDF service.

---

## Sources

- [GitHub — Stirling-Tools/stirling-pdf](https://github.com/Stirling-Tools/stirling-pdf)
- [Official site — stirling.com](https://www.stirling.com/)
- [Documentation — docs.stirlingpdf.com](https://docs.stirlingpdf.com/)
- [Docker Hub — stirlingtools/stirling-pdf](https://hub.docker.com/r/stirlingtools/stirling-pdf)
- [Open Core Ventures — Anthony Stirling launch announcement](https://www.opencoreventures.com/blog/open-source-creator-anthony-stirling-launches-stirling-pdf-to-build-the-first-open-core-pdf-editing-suite)
- [Stirling PDF License file](https://github.com/Stirling-Tools/Stirling-PDF/blob/main/LICENSE)
- [Stirling PDF Paid Offerings](https://docs.stirlingpdf.com/Paid-Offerings/)

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
