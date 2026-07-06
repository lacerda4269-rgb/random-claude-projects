# Resource Report: spec-kit (GitHub Spec-Driven Development Toolkit)

**URL:** https://github.com/github/spec-kit
**Date Researched:** 2026-06-01 | **Updated:** 2026-06-08
**Researched by:** Rose | Security pre-check: Soren (pending) | Report by: Rose
**Already in Master Library?** No — new item.

---

## C&P Summary

Spec-kit is GitHub's open-source toolkit for a development approach called Spec-Driven Development — essentially, a formalized way to make AI coding agents build the right thing by writing out the full specification before any code is written. The workflow moves through four stages: define requirements, create a technical plan, break the plan into tasks, then implement. Each stage produces a written document that feeds into the next, creating a clear trail of decisions rather than a single opaque "just build it" prompt. GitHub built and maintains this — 110,384 stars (updated 2026-06-08), MIT license, released June 2026. It supports Claude Code, Copilot, Gemini, Cursor, and 30+ other agents. For this team, it is a methodology reference for how Sage and Cosmo structure project phases, and a practical tool for any project where clear upfront requirements matter.

---

## What It Is

GitHub's open-source toolkit for Spec-Driven Development (SDD) — a methodology that puts specifications at the center of AI-assisted software development. Rather than prompting an AI agent directly with "build me X," SDD requires writing a formal specification first, then working through a structured four-phase workflow (Spec → Plan → Tasks → Implement) where each phase produces a Markdown artifact feeding the next. Released in late 2025 and rapidly adopted through 2026. 110,384 stars (updated 2026-06-08). MIT license. Python (92.9%), Shell (3.7%), PowerShell (3.4%). Latest: v0.9.0 (released June 1, 2026). Actively maintained — pushed 2026-06-08.

The toolkit includes the `specify` CLI — bootstraps projects for SDD by downloading official templates and setting up scaffolding for 30+ supported agents.

---

## What It Does

- Bootstraps any project for Spec-Driven Development via `specify init`
- Four-phase workflow: Spec → Plan → Tasks → Implement, each producing a Markdown artifact
- Slash commands: `/speckit.constitution`, `/speckit.specify`, `/speckit.plan`, `/speckit.tasks`, `/speckit.implement`
- Supports 30+ AI coding agent integrations: Claude Code, GitHub Copilot, Gemini, Cursor, Windsurf, Codex, Kiro, and more
- 70+ community-contributed extensions (docs, code, process, integration, visibility categories)
- Intent-driven multi-step refinement model: forces definition before build, preventing scope drift

---

## Relevance to This Project *(as of 2026-06-01)*

Addresses one of the most common failure modes in AI-assisted development: agents that start building before requirements are clear. The methodology maps closely to how this team already operates (define → plan → execute), but provides a formalized, artifact-producing version of that workflow for external projects.

Cosmo flag: the `/speckit.specify` and `/speckit.plan` slash commands are directly relevant to Cosmo's pre-build phase. Before starting any build, running a SDD phase may produce better-scoped task breakdowns than ad-hoc prompting.

---

## Builder Footprint

- **Integration type:** Skill-composable; the specify CLI bootstraps scaffolding; slash commands operate like skills within the agent session
- **Extension points:** 70+ community extensions in the official catalog; `specify init --integration claude` sets up Claude Code-specific templates
- **Build complexity signal:** Simple (~1–2 hours) — requires `uv` package manager and Python 3.11+; installed via `uv tool install specify-cli --from git+https://github.com/github/spec-kit.git@vX.Y.Z`
- **Known conflicts:** None.

---

## Master Library Assessment

- **Proposed Section:** 9 — Reference & Ecosystem
- **Proposed Tier:** 1
- **Rationale:** 108k stars, MIT, maintained by GitHub itself, v0.9.0 released June 1, 2026. The SDD methodology is directly relevant to how this team structures AI-assisted build phases.
- **Deployment Potential:** Conditional — the specify CLI is deployable; individual extension components require per-item review before adoption

---

## Soren Security Pre-check

- **Verdict:** CLEARED WITH CONDITIONS
- **Checked:** License (MIT — permissive, confirmed, published by GitHub official org), stars (110,384 — updated 2026-06-08), forks (9,741), last pushed (2026-06-08 — active same day as update), language (Python 92.9%, Shell 3.7%, PowerShell 3.4%), maintainer (github — official GitHub organization, authoritative source), PyPI namespace status (confirmed squatting risk — independently verified), community extensions (70+ third-party), Python dependency chain (uv + Python 3.11+), prompt injection check (CLEAN — confirmed by Rose and Soren)
- **Notes:**

| # | Severity | Flag | Notes |
|---|----------|------|-------|
| 1 | HIGH | PyPI namespace squatting — confirmed | A package named `specify-cli` exists on PyPI and is **not** affiliated with GitHub or the spec-kit project. Installing via `pip install specify-cli` would install an unaffiliated and unvetted package. **Install from GitHub source only:** `uv tool install specify-cli --from git+https://github.com/github/spec-kit.git@vX.Y.Z`. This is confirmed by official spec-kit installation docs and independently verified by Soren. |
| 2 | MEDIUM | Community extensions — not covered by this clearance | 70+ community extensions exist in the catalog. This clearance covers the core `specify` CLI and official spec-kit scaffolding only. Any community extension adopted by this team requires individual Soren review before use. |
| 3 | LOW | `uv` package manager dependency | Installation requires `uv`. `uv` is a well-maintained, widely-used Python package manager (Astral). No security concerns with `uv` itself; confirm install source is `pip install uv` or Astral's official installer. |
| 4 | INFO | Prompt injection check — CLEAN | No instruction-like language, permission claims, or directive content found in official documentation, source files, or web content reviewed. |

*Reviewed by Soren | 2026-06-08*

---

## Recommendation

Add to Section 9 (Reference & Ecosystem), Tier 1. Route to Soren for standard clearance. When cleared, flag to Cosmo as a pre-build methodology resource.

---

---

## Report Version Log

| Version | Date | What Changed |
|---------|------|--------------|


*Report by Rose — Research Specialist | Session 201 | 2026-06-01*
*Updated by Rose | Session 230 | 2026-06-08*
*Prompt Injection Check: CLEAN — no instruction-like language, permission claims, or directive content found in any web-sourced content reviewed during research.*

Sources:
- https://github.com/github/spec-kit
- https://github.github.com/spec-kit/
- https://developer.microsoft.com/blog/spec-driven-development-spec-kit
