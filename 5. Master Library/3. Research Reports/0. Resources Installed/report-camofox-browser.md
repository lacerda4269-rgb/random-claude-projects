# Resource Report: Camofox Browser

**URL:** https://github.com/jo-inc/camofox-browser
**Date Researched:** 2026-06-12
**Researched by:** Rose | Security pre-check: Soren 2026-06-12 | Trivy install scan: Soren (2026-06-12) | Report by: Rose
**Already in Master Library?** No — new research, Session 244

---

## What It Is

Camofox Browser is a stealth headless browser server designed specifically for AI agents. It wraps the open-source Camoufox anti-detection engine (a hardened Firefox fork) in a REST API layer, making it a drop-in replacement for Playwright or Puppeteer. Its core purpose is to let agents browse the web without triggering bot-detection systems — Cloudflare, anti-scraping middleware, fingerprint-based blockers, and similar defenses that stop standard headless browsers cold. The server exposes an HTTP API rather than a JavaScript library, meaning any language or agent that can make HTTP calls can use it.

---

## What It Does

- Runs a local REST API server that proxies browser automation commands through a stealth-hardened Firefox engine
- Bypasses Cloudflare challenges, CAPTCHA gates, and fingerprint-based bot detection
- Exposes a Playwright-compatible and Puppeteer-compatible API surface (drop-in replacement pattern)
- Supports OpenClaw plugin integration for additional agent browser capabilities
- Provides anti-detect fingerprint randomization (user agent, canvas fingerprint, WebGL, audio context, timezone)
- Runs as a standalone background process — agents POST commands to it over HTTP rather than importing a library
- Supports Windows, macOS, and Linux (Windows Support added v1.11.0)
- Provides a CLI binary for direct launch (`camofox-browser` command after npm install)

---

## Invocation Interface

- **Typical command pattern:** `npx camofox-browser` or `camofox-browser` (after npm global install); agents interact via `POST /api/browser/...` HTTP endpoints
- **Output format:** JSON (REST API responses); browser page content returned as structured JSON payloads
- **Key structured output flags:** API-driven — no CLI output flags; results are JSON response bodies from the local server
- **Exit code behavior:** exit 0 = server running successfully; non-zero exits indicate startup failure (port conflict, missing dependencies); server logs to stdout
- **Stdin/stdout/stderr notes:** Server runs persistently as a background process; all automation interaction is via HTTP REST calls to the configured local server port

---

## Relevance to This Project *(as of research date — context may not carry to future projects)*

The MIP stack currently uses Microsoft Playwright (Section 3 CLI, Tier 1, CLEARED) as the browser automation layer. Playwright works well for straightforward automation — form fills, navigation, DOM interaction. The gap Camofox addresses is specific: pages that actively block headless browsers. When AI agents need to access financial data sites, news sources behind soft paywalls, or any site with Cloudflare or bot-detection middleware deployed, Playwright will often fail silently or hit challenge loops. Camofox is built exactly for that class of problem.

This is not a replacement for Playwright in general — it is a specialized stealth layer for the subset of automation tasks where bot detection is the blocker. The two can coexist: Playwright for routine browsing, Camofox for protected targets. For MIP, the most relevant use cases are Rose's research tasks (fetching documentation from bot-protected sources), trading agent research workflows (financial data sites with aggressive bot detection), and any future web-scraping automation.

The REST API architecture is a meaningful architectural difference from Playwright's library model. Any agent — including those not written in JavaScript — can call it over HTTP, which makes it useful for Pete (Python Specialist) and other agents without Playwright bindings.

---

## Builder Footprint

- **Integration type:** CLI-invocable / Standalone tool
- **Extension points:** REST API — HTTP endpoints; Cosmo can build a skill or hook wrapper that starts the server, manages its lifecycle, and routes requests from any agent
- **Build complexity signal:** Simple (~1–2 hours — REST API wrapping is straightforward; server lifecycle management adds minor complexity)
- **Known conflicts:** Overlaps with Microsoft Playwright (Section 3, Tier 1) as a browser automation layer — not a conflict, a complement; Cosmo should document the routing logic clearly (Playwright for standard tasks; Camofox for bot-protected targets)

---

## Master Library Assessment

- **Proposed Section:** Section 10 — Alternative Tools & Notable Ecosystem
- **Proposed Tier:** 2
- **Rationale:** Not a core replacement for Playwright — Playwright stays Tier 1 and covers the majority of use cases. Camofox earns Tier 2 as a high-value specialized complement: when bot detection is the blocker, there is no fallback in the current stack, and this is the right tool for that gap. Tier 3 would undersell its utility; Tier 1 would overstate its role.

---

## Soren Security Review

### Pre-check (Research Phase)

**CLI Intake Checklist Results:**

- **Version evaluated:** v2.4.5 (npm latest) | Latest available: v2.4.5 | GitHub latest binary release: v1.11.2 | Delta: npm and GitHub releases are parallel tracks — npm is the standard install path
- **License:** MIT | Flag: none — permissive, commercial use permitted
- **CVE check:** 0 vulnerabilities found | Sources checked: osv.dev (npm package: camofox-browser)
- **Alternatives evaluated:** Microsoft Playwright (already in stack — no stealth capability), puppeteer-extra + stealth plugin (community plugin, less maintained, no Windows CLI binary), Camoufox Python library (lower-level, no REST API) | Preferred because: Camofox Browser provides a language-agnostic REST API over the same stealth engine, compatible with MIP's multi-language agent stack
- **Summary rating:** Flagged | Flags: (1) REST API server runs on localhost — default auth posture needs Soren review; (2) new repo (created January 2026, 94 open issues) — active development, stability not yet proven; (3) org "jo-inc" has limited public history — single-product org; Soren should review source code for server startup and API authentication behavior

**Verdict:** CLEARED WITH CONDITIONS
**Checked:** OSV.dev CVE sweep (npm: camofox-browser) — 0 vulnerabilities. npm registry full version history (33 releases, v1.0.0 2026-02-15 through v2.4.5 2026-05-25). Source code review — `src/utils/config.ts`, `src/middleware/auth.ts`, `src/routes/core.ts` read directly from the canonical source repo (redf0x1/camofox-browser — confirmed as the true upstream; jo-inc/camofox-browser is the org mirror). MIT license confirmed from npm registry `"license": "MIT"`. Maintainer identity: single maintainer `redf0x1` (email: tl667564@gmail.com). Dependency audit: express ^4.18.2, playwright-core ^1.58.0, camoufox-js ^0.8.5, commander ^14.0.0, css-tree ^3.2.1, swagger-ui-express ^5.0.1. No postinstall script surprises: `"postinstall": "npx camoufox-js fetch || true"` (downloads the Camoufox browser binary — expected, non-malicious). Supply chain note: npm `repository` field points to `redf0x1/camofox-browser`, not `jo-inc/camofox-browser`; both are active and the code is identical; the org is a GitHub org wrapping a solo maintainer.

**Auth model — source-confirmed findings:**
- Default host: `127.0.0.1` (loopback only — hardcoded default in `loadConfig`)
- Default authMode: `'auto'` (no env var set = no API key required)
- Auth enforcement pattern: `if (CONFIG.apiKey && !isAuthorizedWithApiKey(req, CONFIG.apiKey))` — authentication is only enforced when `CAMOFOX_API_KEY` is set
- `assertServerExposureSafety()` **throws and refuses to start** if `CAMOFOX_HOST` is set beyond loopback without an API key — network exposure without auth is structurally blocked at startup
- Auth implementation uses `crypto.timingSafeEqual` — no timing-attack vulnerability

**Conditions:**
1. Default install (localhost-only, no API key): acceptable. The server is physically unreachable from the network and the exposure guard prevents misconfiguration. This is the standard local-agent use case.
2. If ever configured to bind beyond localhost (not expected for MIP): `CAMOFOX_API_KEY` must be set — the server enforces this and will not start without it.
3. Single-maintainer supply chain risk: monitor for maintainer abandonment or ownership transfer. This is low risk today but a standing watch item for a solo-maintainer npm package with growing adoption.
4. 94 open issues on a 5-month-old repo: a stability signal, not a security signal. Expected for a fast-moving early-stage tool. Mitigated by version pinning at adoption.

### Trivy Install Scan (2026-06-12 — Session 245)
- **Verdict:** CLEARED
- **Scanned:** camofox-browser (latest, resolved to installed version) via `trivy fs package-lock.json` (Trivy v0.71.0, DB updated 2026-06-12)
- **CVEs found:** 0
- **Install notes:**
  - 161 packages installed globally via `npm install -g camofox-browser`. Two deprecated dependency warnings: `lodash.isequal@4.5.0` (deprecated, superseded by Node.js native `isDeepStrictEqual`) and `prebuild-install@7.1.3` (deprecated, contact native addon author). Neither is a CVE — both are maintenance-status deprecations only.
  - Verified: `camofox-browser --version` → v2.4.5.
- **Final verdict: CLEARED — conditions from pre-check remain active.**

---

## Recommendation

Add to Master Library at Section 10, Tier 2, pending Soren clearance. This fills a genuine gap: browser automation capable of penetrating bot-protection systems that Playwright cannot handle. Do not install until Soren clears the server authentication and network exposure model. Once cleared, Cosmo should build a skill wrapper that manages the server lifecycle and routes requests from any agent.

---

## C&P Summary

Camofox Browser is a specialized browser automation tool built for AI agents. Unlike standard tools like Playwright, it is designed to look like a real human browser to websites that try to block bots — bypassing Cloudflare challenges, fingerprint detection, and anti-scraping systems. It runs as a small local server that agents talk to over a simple HTTP interface, meaning any agent (regardless of programming language) can send it browsing commands and get page content back. For this project, it fills a specific gap: when Rose or a trading agent needs to fetch data from a site that blocks standard automated browsers, Camofox is the tool that makes that possible. It does not replace Playwright — it handles the harder cases Playwright cannot.

---

---

## Report Version Log

| Version | Date | Notes |
|---------|------|-------|

---

*Report by Rose | Session 244 | 2026-06-12*
---

## Soren Security Pre-check

**CLI Intake Checklist Results:**

- **Version evaluated:** v2.4.5 (npm latest) | Latest available: v2.4.5 | GitHub latest binary release: v1.11.2 | Delta: npm and GitHub releases are parallel tracks — npm is the standard install path
- **License:** MIT | Flag: none — permissive, commercial use permitted
- **CVE check:** 0 vulnerabilities found | Sources checked: osv.dev (npm package: camofox-browser)
- **Alternatives evaluated:** Microsoft Playwright (already in stack — no stealth capability), puppeteer-extra + stealth plugin (community plugin, less maintained, no Windows CLI binary), Camoufox Python library (lower-level, no REST API) | Preferred because: Camofox Browser provides a language-agnostic REST API over the same stealth engine, compatible with MIP's multi-language agent stack
- **Summary rating:** Flagged | Flags: (1) REST API server runs on localhost — default auth posture needs Soren review; (2) new repo (created January 2026, 94 open issues) — active development, stability not yet proven; (3) org "jo-inc" has limited public history — single-product org; Soren should review source code for server startup and API authentication behavior

**Verdict:** CLEARED WITH CONDITIONS
**Checked:** OSV.dev CVE sweep (npm: camofox-browser) — 0 vulnerabilities. npm registry full version history (33 releases, v1.0.0 2026-02-15 through v2.4.5 2026-05-25). Source code review — `src/utils/config.ts`, `src/middleware/auth.ts`, `src/routes/core.ts` read directly from the canonical source repo (redf0x1/camofox-browser — confirmed as the true upstream; jo-inc/camofox-browser is the org mirror). MIT license confirmed from npm registry `"license": "MIT"`. Maintainer identity: single maintainer `redf0x1` (email: tl667564@gmail.com). Dependency audit: express ^4.18.2, playwright-core ^1.58.0, camoufox-js ^0.8.5, commander ^14.0.0, css-tree ^3.2.1, swagger-ui-express ^5.0.1. No postinstall script surprises: `"postinstall": "npx camoufox-js fetch || true"` (downloads the Camoufox browser binary — expected, non-malicious). Supply chain note: npm `repository` field points to `redf0x1/camofox-browser`, not `jo-inc/camofox-browser`; both are active and the code is identical; the org is a GitHub org wrapping a solo maintainer.

**Auth model — source-confirmed findings:**
- Default host: `127.0.0.1` (loopback only — hardcoded default in `loadConfig`)
- Default authMode: `'auto'` (no env var set = no API key required)
- Auth enforcement pattern: `if (CONFIG.apiKey && !isAuthorizedWithApiKey(req, CONFIG.apiKey))` — authentication is only enforced when `CAMOFOX_API_KEY` is set
- `assertServerExposureSafety()` **throws and refuses to start** if `CAMOFOX_HOST` is set beyond loopback without an API key — network exposure without auth is structurally blocked at startup
- Auth implementation uses `crypto.timingSafeEqual` — no timing-attack vulnerability

**Conditions:**
1. Default install (localhost-only, no API key): acceptable. The server is physically unreachable from the network and the exposure guard prevents misconfiguration. This is the standard local-agent use case.
2. If ever configured to bind beyond localhost (not expected for MIP): `CAMOFOX_API_KEY` must be set — the server enforces this and will not start without it.
3. Single-maintainer supply chain risk: monitor for maintainer abandonment or ownership transfer. This is low risk today but a standing watch item for a solo-maintainer npm package with growing adoption.
4. 94 open issues on a 5-month-old repo: a stability signal, not a security signal. Expected for a fast-moving early-stage tool. Mitigated by version pinning at adoption.

---

---
*Consolidated S264 (dual-Soren merge): this canonical retains BOTH the research-phase **Soren Security Review** + Trivy install scan (2026-06-12, from the category copy, above) AND the install-phase **Soren Security Pre-check** (reattached from the install-folder copy). Category copy superseded; no Soren provenance lost. ML Stage 1.*
