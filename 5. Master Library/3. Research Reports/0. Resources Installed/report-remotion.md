# Resource Report: Remotion

**URL:** https://github.com/remotion-dev/remotion
**Date Researched:** 2026-03-28 | **Freshness Update:** 2026-06-03 (Session 213 — significant update; AI/LLM integration added; re-classification warranted)
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia (original) | Updated by: Sophia (COO)
**Already in Master Library?** Yes — currently Section 11 (Jay's Shelf), Tier 3. **⚠️ Re-classification flag:** Original "no use case" verdict was for trading infrastructure project. Context has changed — Vicky the Videographer is now active and Remotion has made AI-driven video production a primary use case. Re-file to Vicky's active tool section after Soren confirms commercial license terms. See notes below.

---

## C&P Summary

Remotion is an open-source framework for creating videos programmatically using React — developers write videos as React components with CSS, Canvas, SVG, and WebGL, and Chromium renders them as video files. As of June 2026 it has 48,887 stars (up from 41k in March), is at v4.0.471, and has made AI-driven video production a primary use case: it now ships a dedicated `/docs/ai` section, Claude Code skill files, an MCP server, and a "Prompt to Motion Graphics" workflow. Production AI video SaaS companies are building on it — Submagic reportedly hit $1M+ ARR within 3 months using Remotion as their foundation. Commercial license required for revenue-generating use (open source core free). Still under `remotion-dev/` GitHub org, actively maintained with commits today.

---

## What It Is

Remotion is a React-based video production framework — the only tool in this class that treats video as a first-class React rendering problem. Every frame is a React component; Chromium renders those components frame-by-frame into video. This means every capability of the web platform (CSS animations, WebGL shaders, SVG, Canvas, web fonts, external data fetching) is available inside a video. As of mid-2026, Remotion has moved AI-driven video production to a primary positioning angle — with explicit integrations for Claude Code, coding agents, and LLM-prompted video generation.

---

## What It Does

- **Programmatic video authoring** — write videos as React components; Chromium renders each frame
- **Data-driven video** — fetch external data, APIs, or dynamic content; render personalized video at scale
- **Full web platform access** — CSS, Canvas, SVG, WebGL, web fonts, all available per frame
- **AI/LLM integration (new as of 2026):**
  - Claude Code skill files — agent can generate Remotion components directly
  - MCP server — Remotion-domain MCP for LLM editor support
  - Bolt.new integration — prompt-to-video via Bolt.new
  - "Prompt to Motion Graphics" — documented workflow
  - Just-in-time compilation — compile Remotion components at runtime (AI-generated code → video pipeline)
  - AI SaaS template — starter template for building AI video SaaS products
- **Remotion Studio** — browser-based visual editor with timeline, drag-and-drop effects (maturing toward full editing environment)
- **Visual effects library** (`@remotion/effects`) — `waves()`, `rings()`, `zigzag()`, `pixelDissolve()` and growing
- **Captions and audio** — `@remotion/captions` package; audio sync built in
- **Rendering pipeline** — `npx remotion render` produces MP4/GIF/WebM; serverless rendering via Lambda, Cloud Run, or local
- **TypeScript-first** — full type safety throughout the component tree

---

## Repository Metrics (June 2026)

| Metric | Value |
|---|---|
| **Stars** | 48,887 (up from 41k in March 2026) |
| **Forks** | 3,436 |
| **Projects using** | 4,681 repositories |
| **Latest Version** | v4.0.471 (released 2026-06-01) |
| **Release Cadence** | Multiple patch releases per week (v4.0.467–471 all shipped May 26–June 1) |
| **Last Commit** | 2026-06-03 (today) |
| **Language** | TypeScript (74.1%) |
| **License** | Custom — see licensing note below |
| **Maintained by** | Jonny Burger (JonnyBurger), remotion-dev/ org |

---

## Licensing Note ⚠️

Remotion uses a **custom license** (not a standard SPDX open source license). The model:
- **Open source core** — free to use for personal, educational, and open source projects
- **Commercial license required** — for any company or product generating revenue

**This is a blocker before Vicky ships anything commercially.** The license cost must be evaluated before committing to Remotion as the Movie Studio foundation for any revenue-generating product. This is a one-time purchase, not a subscription — but the exact pricing requires checking `remotion.pro/license`. Sage to flag for Jay's decision when Vicky's commercial scope is defined.

---

## Production Use Cases (confirmed)

- **Submagic** — AI short-form video SaaS, reportedly $1M+ ARR within 3 months of launch; built on Remotion
- **Typeframes** — product video generation in minutes
- **GitHub "GitHub Unwrapped"** — personalized year-in-review videos for all GitHub users
- **Fireship** — YouTube tutorial video series
- Conference asset generation, personalized marathon finisher videos

---

## Relevance to This Project — Updated for Vicky

**Original assessment (March 2026):** "No use case — trading infrastructure project."
**Revised assessment (June 2026):** Direct fit for Vicky the Videographer and the Movie Studio initiative.

Remotion is the most capable code-based video production framework available. With AI now a primary use case (Claude Code skills, MCP server, coding agent workflows), Vicky can generate React components that render as video — enabling data-driven, personalized, or scripted video production entirely in code. The Submagic proof point is significant: an AI video SaaS product reached $1M ARR in 3 months on this foundation.

**Re-classification decision:** Move from Jay's Shelf (Section 11, Tier 3) to Vicky's active tool section (Section TBD — pending ML section structure for Movie Studio tools) after Soren confirms commercial license terms are acceptable. Do not deploy in any revenue-generating context until license is purchased.

---

## Master Library Assessment

- **Current Section:** 11 — Jay's Shelf, Tier 3 *(stale — reassess)*
- **Recommended Section:** Active tools section for Vicky / Movie Studio (Section TBD)
- **Recommended Tier:** 1 — Essential (for any project where Vicky is active and code-based video production is in scope)
- **Action required:** Sage flags for Lexi to re-file after Soren confirms license terms

---

## Soren Security Pre-check

- **Verdict:** CLEARED (original March 2026)
- **Checked:** Star count (41,000+), active community (320+ contributors), well-documented, official `remotion-dev/` org, active maintenance.
- **Freshness note:** No new security concerns from June 2026 check. Still under `remotion-dev/` org. Custom license model unchanged — Soren to confirm commercial license acceptability before any revenue-generating deployment.
- **New flag:** MCP server and Claude Code skill files are new additions since original check — Soren to review these specifically when re-classification pass occurs.

---

## Install / Quickstart

```bash
# Create a new Remotion project
npx create-video@latest

# Blank template
npx create-video@latest --yes --blank my-video
cd my-video
npm i
npx remotion studio

# Add Claude Code skills for agent-based video generation
npx -y skills@latest add remotion-dev/skills -g -y
```

---

*Report by Sophia — COO | Session 29, 2026-03-28 (original) | Significantly updated Sophia (COO) — Session 213, 2026-06-03*

---

## Report Version Log

| Version | Date | What Changed |
|---------|------|--------------|

---
*Consolidated S264: the `-updated` body was current but had dropped provenance; reattached the **Report Version Log** from the original category copy. Canonical renamed to drop the `-updated` suffix. Both prior copies superseded. ML Stage 1.*
