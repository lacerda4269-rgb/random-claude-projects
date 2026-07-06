# Resource Report: HyperFrames

**URL:** https://github.com/heygen-com/hyperframes
**Date Researched:** 2026-06-12
**Researched by:** Rose | Security pre-check: Soren 2026-06-12 | Trivy install scan: Soren (2026-06-12) | Report by: Rose
**Already in Master Library?** No — new research, Session 244

---

## What It Is

HyperFrames is an open-source, agent-first video rendering framework built by HeyGen, the AI video company. The premise is simple: write HTML and CSS, render video. It treats video as a declarative output format — you describe what a frame should look like using standard web markup, and HyperFrames converts it to MP4 via Puppeteer and FFmpeg. It is explicitly designed for AI agents: agents can generate or template HTML, hand it off to HyperFrames, and receive a rendered video without any knowledge of video codecs, timelines, or export settings. It includes an MCP server component, a CLI, a visual Studio interface, cloud render support (AWS Lambda, GCP Cloud Run), and a full animation layer (GSAP-based, shader transitions).

---

## What It Does

- Renders video from HTML/CSS/JavaScript input — write web markup, get an MP4
- Provides frame-level timeline control: each "frame" is an HTML template with defined duration and transitions
- Includes a GSAP-based animation engine for CSS transitions and motion effects
- Ships a CLI (`@hyperframes/cli`) for command-line render invocations
- Includes an MCP server — agents can invoke renders directly via MCP tool calls
- Provides a visual Studio UI for previewing and editing frame compositions
- Supports cloud rendering via AWS Lambda and GCP Cloud Run adapters
- Handles shader-based transitions between frames
- Provides a Puppeteer rendering engine (HTML-to-frame capture pipeline)
- Exports to MP4 via FFmpeg integration
- TypeScript SDK for programmatic composition by agents or code

---

## Relevance to This Project *(as of research date — context may not carry to future projects)*

Remotion (already in the Master Library, Section 11, Tier 3, CLEARED) is the existing video rendering candidate for MIP. The key comparison Jay is asking for is whether HyperFrames is better. The answer is: they solve different problems.

Remotion uses React components as the authoring layer — you write React code describing video frames, and Remotion renders it. This is powerful but requires React knowledge. HyperFrames uses plain HTML/CSS as the authoring layer, which is a lower barrier and more natural for AI agents to generate. An agent that knows how to write HTML can author a HyperFrames video without any React knowledge.

The agent-native MCP integration is the most significant differentiator for MIP. HyperFrames ships an MCP server out of the box — meaning Sage, Vicky, or any other agent can invoke a video render as a direct MCP tool call, not by generating code and running a build pipeline. This is a meaningful workflow difference in an agent-orchestrated project. Remotion has no equivalent MCP integration.

For Vicky's video production workflows, HyperFrames is a stronger fit for agent-generated content (data cards, title sequences, presentation-style video). Remotion remains relevant for complex motion design work where a developer is composing the animation in code. The two are not mutually exclusive.

The 27,044 star count and HeyGen organizational backing (a funded AI video company) gives HyperFrames strong legitimacy and an active maintenance posture — the repo had three releases on the day of this research.

---

## Builder Footprint

- **Integration type:** CLI-invocable / MCP tool layer / Skill-composable
- **Extension points:** MCP server (out of the box); CLI (`@hyperframes/cli`); TypeScript SDK; cloud render adapters (Lambda, Cloud Run); Cosmo can build a skill that wraps the CLI or the MCP server for agent-triggered renders
- **Build complexity signal:** Moderate (~half-day — MCP server registration is straightforward; skill wrapper needs to handle render lifecycle, input templating, and output path management)
- **Known conflicts:** Functional overlap with Remotion (Section 11, Tier 3) — not a hard conflict; both can coexist with different roles (Remotion for developer-authored motion design; HyperFrames for agent-generated HTML-to-video). Cosmo should document the routing logic at adoption time.

---

## Master Library Assessment

- **Proposed Section:** Section 10 — Alternative Tools & Notable Ecosystem
- **Proposed Tier:** 2
- **Rationale:** HyperFrames is stronger than Remotion for agent-native video generation tasks specifically because of the MCP integration and the HTML authoring model. It earns Tier 2 as a high-value tool with direct relevance to Vicky's domain and agent workflow integration. It is not Tier 1 because Remotion is already in the stack and a migration decision requires more deliberate evaluation.

---

## Soren Security Review

### Pre-check (Research Phase)

**CLI Intake Checklist Results:**

- **Version evaluated:** v0.6.95 (@hyperframes/core npm, 2026-06-12) | Latest available: v0.6.95 | Delta: none — evaluated version is latest; active daily release cadence
- **License:** Apache-2.0 | Flag: none — permissive, commercial use permitted, patent grant included
- **CVE check:** 0 vulnerabilities found | Sources checked: osv.dev (@hyperframes/core npm package)
- **Alternatives evaluated:** Remotion (already in ML, React-based, no MCP integration, no HTML authoring), Revideo (Remotion fork, similar React model), MotionCanvas (code-first, TypeScript, no agent MCP) | Preferred because: HyperFrames is the only HTML-based agent-first video renderer with a built-in MCP server; its HeyGen backing indicates active investment
- **Summary rating:** Flagged | Flags: (1) pre-1.0 version (v0.6.x) — API surface is not yet stable; breaking changes possible before v1.0; (2) Puppeteer rendering engine introduces a Chromium dependency — Soren should note this alongside existing Playwright install; (3) FFmpeg dependency — MIP already has FFmpeg in stack; confirm version compatibility

**Verdict:** CLEARED WITH CONDITIONS
**Checked:** OSV.dev CVE sweep (npm: @hyperframes/core) — 0 vulnerabilities. npm registry: @hyperframes/core v0.6.95, @hyperframes/engine v0.6.95. Apache-2.0 license confirmed from raw LICENSE file (Apache License Version 2.0, January 2004 — full SPDX-compliant text, NOTICE obligation confirmed). HeyGen org trust signals: established AI video company, 27,044 stars, active daily release cadence (3 releases on research day), monorepo with 10 active packages. Puppeteer version in engine package: `"puppeteer": "^24.0.0"` and `"puppeteer-core": "^24.39.1"` — both are current stable versions; no known CVEs for puppeteer ^24.x in GitHub Advisory Database or OSV.dev. GitHub Advisories search confirmed no puppeteer-specific security advisories in current results. Cloud render adapters (aws-lambda, gcp-cloud-run) are separate packages — not auto-installed; clearance applies to core/engine/CLI only; cloud adapters require individual review before use.

**Pre-1.0 stability as a security consideration:** v0.6.x is a feature-stability concern, not a security-specific one. Breaking API changes at this stage are a deployment risk, not a vulnerability vector. Mitigated by version pinning at adoption.

**Puppeteer + Playwright coexistence:** No hard conflict. Both are separate packages; Playwright is the MIP stack standard for general automation, Puppeteer is bundled inside HyperFrames' engine and used only for its internal HTML-to-frame rendering pipeline. They do not share a Chromium binary by default — Puppeteer downloads its own. This means a second Chromium installation on the machine. No security issue; disk space is the only cost.

**FFmpeg:** HyperFrames uses FFmpeg for MP4 export. MIP already has FFmpeg installed. HyperFrames calls the system `ffmpeg` binary — it does not bundle its own. No version conflict expected; the tool uses standard encoding flags compatible with any recent FFmpeg release.

**Conditions:**
1. Pin to `@hyperframes/engine@0.6.95` and `@hyperframes/core@0.6.95` at adoption; review before any version bump to v1.0 or beyond — breaking changes are expected at that boundary.
2. Apache-2.0 NOTICE obligation: if MIP distributes software that incorporates HyperFrames, a NOTICE file must be included. For internal/agent use with no distribution, NOTICE obligation does not apply.
3. Cloud render adapters (aws-lambda, gcp-cloud-run packages): **not cleared** — require individual security review before any deployment against those adapters. These packages make external network calls to cloud infrastructure and have a different attack surface than the local rendering engine.
4. Puppeteer Chromium: a second Chromium binary will be installed alongside Playwright's. No security concern; note it as an expected artifact during adoption.

### Trivy Install Scan (2026-06-12 — Session 245)
- **Verdict:** CLEARED
- **Scanned:** @hyperframes/core@0.6.95 + hyperframes@0.6.95 (CLI package — correct name is `hyperframes`, not `@hyperframes/cli` as originally noted in plan) via `trivy fs package-lock.json` in `C:\ClaudeTools\HyperFrames\` (Trivy v0.71.0, DB updated 2026-06-12)
- **CVEs found:** 0 (196 packages scanned)
- **Install notes:**
  - Install location: `C:\ClaudeTools\HyperFrames\` (following Remotion pattern at `C:\ClaudeTools\Remotion\`).
  - CLI package name correction: npm package is `hyperframes` (not `@hyperframes/cli`). `@hyperframes/cli` returns 404 — the CLI is distributed under the flat `hyperframes` name. All plan and soul references to `@hyperframes/cli` should use `hyperframes`.
  - One deprecated dependency warning: `node-domexception@1.0.0` (use platform native DOMException). Maintenance deprecation only — not a CVE.
  - Puppeteer Chromium download: expected artifact per pre-check Condition 4.
  - Verified: `npx hyperframes --version` (via `node_modules/.bin/hyperframes`) → 0.6.95.
- **Final verdict: CLEARED — pre-check conditions remain active; cloud adapters still not cleared.**

---

## Recommendation

Add to Master Library at Section 10, Tier 2, pending Soren clearance. HyperFrames is the stronger tool for agent-generated video specifically — its MCP integration and HTML authoring model are genuine advantages over Remotion in an agent-orchestrated stack. The pre-1.0 status is the only meaningful caution: pin the version at adoption and monitor for breaking changes. Cosmo should build an MCP-based skill wrapper for Vicky once Soren clears it.

---

## C&P Summary

HyperFrames is a video rendering framework built by HeyGen (the AI video company) that works by converting HTML and CSS into video. The idea is straightforward: instead of writing complex video editing code, you write a web page layout for each frame, and HyperFrames turns those frames into an MP4. It is specifically designed for AI agents — it includes a built-in MCP server so agents can trigger video renders as direct commands, without writing any code. This is a meaningful upgrade from Remotion (the current MIP candidate) for agent-generated video: Remotion requires React code, HyperFrames accepts plain HTML that any agent can write. With 27,000 stars and daily releases from a funded AI video company, it is actively developed and well-supported.

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

- **Version evaluated:** v0.6.95 (@hyperframes/core npm, 2026-06-12) | Latest available: v0.6.95 | Delta: none — evaluated version is latest; active daily release cadence
- **License:** Apache-2.0 | Flag: none — permissive, commercial use permitted, patent grant included
- **CVE check:** 0 vulnerabilities found | Sources checked: osv.dev (@hyperframes/core npm package)
- **Alternatives evaluated:** Remotion (already in ML, React-based, no MCP integration, no HTML authoring), Revideo (Remotion fork, similar React model), MotionCanvas (code-first, TypeScript, no agent MCP) | Preferred because: HyperFrames is the only HTML-based agent-first video renderer with a built-in MCP server; its HeyGen backing indicates active investment
- **Summary rating:** Flagged | Flags: (1) pre-1.0 version (v0.6.x) — API surface is not yet stable; breaking changes possible before v1.0; (2) Puppeteer rendering engine introduces a Chromium dependency — Soren should note this alongside existing Playwright install; (3) FFmpeg dependency — MIP already has FFmpeg in stack; confirm version compatibility

**Verdict:** CLEARED WITH CONDITIONS
**Checked:** OSV.dev CVE sweep (npm: @hyperframes/core) — 0 vulnerabilities. npm registry: @hyperframes/core v0.6.95, @hyperframes/engine v0.6.95. Apache-2.0 license confirmed from raw LICENSE file (Apache License Version 2.0, January 2004 — full SPDX-compliant text, NOTICE obligation confirmed). HeyGen org trust signals: established AI video company, 27,044 stars, active daily release cadence (3 releases on research day), monorepo with 10 active packages. Puppeteer version in engine package: `"puppeteer": "^24.0.0"` and `"puppeteer-core": "^24.39.1"` — both are current stable versions; no known CVEs for puppeteer ^24.x in GitHub Advisory Database or OSV.dev. GitHub Advisories search confirmed no puppeteer-specific security advisories in current results. Cloud render adapters (aws-lambda, gcp-cloud-run) are separate packages — not auto-installed; clearance applies to core/engine/CLI only; cloud adapters require individual review before use.

**Pre-1.0 stability as a security consideration:** v0.6.x is a feature-stability concern, not a security-specific one. Breaking API changes at this stage are a deployment risk, not a vulnerability vector. Mitigated by version pinning at adoption.

**Puppeteer + Playwright coexistence:** No hard conflict. Both are separate packages; Playwright is the MIP stack standard for general automation, Puppeteer is bundled inside HyperFrames' engine and used only for its internal HTML-to-frame rendering pipeline. They do not share a Chromium binary by default — Puppeteer downloads its own. This means a second Chromium installation on the machine. No security issue; disk space is the only cost.

**FFmpeg:** HyperFrames uses FFmpeg for MP4 export. MIP already has FFmpeg installed. HyperFrames calls the system `ffmpeg` binary — it does not bundle its own. No version conflict expected; the tool uses standard encoding flags compatible with any recent FFmpeg release.

**Conditions:**
1. Pin to `@hyperframes/engine@0.6.95` and `@hyperframes/core@0.6.95` at adoption; review before any version bump to v1.0 or beyond — breaking changes are expected at that boundary.
2. Apache-2.0 NOTICE obligation: if MIP distributes software that incorporates HyperFrames, a NOTICE file must be included. For internal/agent use with no distribution, NOTICE obligation does not apply.
3. Cloud render adapters (aws-lambda, gcp-cloud-run packages): **not cleared** — require individual security review before any deployment against those adapters. These packages make external network calls to cloud infrastructure and have a different attack surface than the local rendering engine.
4. Puppeteer Chromium: a second Chromium binary will be installed alongside Playwright's. No security concern; note it as an expected artifact during adoption.

---

---
*Consolidated S264 (dual-Soren merge): this canonical retains BOTH the research-phase **Soren Security Review** + Trivy install scan (2026-06-12, from the category copy, above) AND the install-phase **Soren Security Pre-check** (reattached from the install-folder copy). Category copy superseded; no Soren provenance lost. ML Stage 1.*
