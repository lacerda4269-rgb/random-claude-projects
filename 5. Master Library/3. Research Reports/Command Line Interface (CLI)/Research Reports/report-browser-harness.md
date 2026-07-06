# Resource Report: Browser Harness

**URL:** https://github.com/browser-use/browser-harness
**Site:** https://github.com/browser-use
**Date Researched:** 2026-04-21
**Researched by:** Rose | Security pre-check: Soren — REJECTED | Report by: Rose
**Already in Master Library?** No — new submission, Batch 1

---

## What It Is

A self-healing browser automation harness built directly on Chrome DevTools Protocol (CDP) that gives an LLM complete autonomy to complete any browser task — including writing its own missing helper functions mid-execution.

## What It Does

- Connects an LLM directly to Chrome via CDP WebSocket — no heavyweight framework in between
- Self-healing design: when the agent encounters a missing function, it writes it into `helpers.py` and continues without interruption
- Core codebase is intentionally minimal — approximately 592 lines of Python across five files
- Domain skills system: contributors submit agent-generated site-specific skill folders (`domain-skills/<site>/`) covering selectors, flows, and edge cases discovered during real task execution; example skills ship for GitHub, LinkedIn, and Amazon
- Setup via a single prompt pasted into Claude Code or any LLM interface after enabling Chrome remote debugging
- No external service dependencies; requires only a Chrome instance with remote debugging enabled

## Technical Details

- **Language:** Python (100%)
- **License:** MIT
- **Stars:** ~14.5k (as of 2026-06-08; was ~3.5k–4.3k in April 2026 — major growth)
- **Forks:** ~1,347
- **Open Issues:** 118
- **Contributors:** 14
- **Last Commit:** May 20, 2026 — actively maintained
- **Main Maintainer:** sauravpanda; part of the browser-use GitHub organization (which also owns the main browser-use repo at 89k stars)
- **Notable Sibling:** `browser-use/browser-harness-js` — TypeScript port, 104 stars, newer and less mature
- **Key Files:** `run.py` (36 lines), `helpers.py` (195 lines, agent-editable), `admin.py` + `daemon.py` (361 lines managing CDP WebSocket and socket bridge)

## How It Works

The agent runs a loop via `run.py`, which pre-loads `helpers.py` into context. When the agent needs a capability that doesn't exist (e.g., `upload_file()`), it edits `helpers.py` directly, then resumes the task. `admin.py` and `daemon.py` manage the CDP WebSocket connection and socket bridging between the LLM and Chrome. No framework constraints — the agent is the only decision-maker.

## Relevance to This Project

Directly relevant as a lightweight browser automation layer for any agent on the team that needs to interact with web pages — scraping, form completion, or site-based research tasks. Lighter-weight alternative to full frameworks like Playwright or Selenium. Pairs naturally with any Claude Code agent that needs browser access.

## Master Library Assessment

- **Proposed Section:** 3 — CLI & Standalone Tools
- **Proposed Tier:** 2
- **Rationale:** Standalone tool invoked via prompt/CLI, not an MCP or skill in the technical sense. MIT-licensed, actively maintained by a credible organization. Tier 2 because it is not core infrastructure but is immediately useful for web-facing agent tasks. Soren review required before installation.

## Soren Security Pre-check

- **Verdict:** **REJECTED**
- **Reviewed by:** Soren | 2026-06-04

**Checked:**
- Manual read (Cat 1): pass — README, SKILL.md, AGENTS.md, install.md, run.py, helpers.py reviewed; no prompt injection signals; no obfuscated code; install.md instruction to import SKILL.md into `~/.claude/CLAUDE.md` is a legitimate setup feature, not an injection attempt; SKILL.md content reviewed and confirmed clean; self-healing mechanic (agent edits `agent_helpers.py` at runtime) is deliberate design, documented, and architecturally contained
- Cat 2 — Trivy (repo scan): no supported lockfile detected; no vulnerabilities, secrets, or misconfigs found; tool has minimal Python dependencies (cdp-use, fetch-use, pillow, websockets — all pinned)
- Cat 2 — Gitleaks (secrets scan): **8 leaks found** — all `generic-api-key` rule — see findings
- Cat 3: not applicable — this is a CLI tool, not an MCP server

**Findings:**
- Gitleaks: 8 `generic-api-key` findings in `agent-workspace/domain-skills/metacritic/scraping.md`
  - Match pattern: `API_KEY = "<REDACTED-S264>"`
  - This is a hardcoded Metacritic backend API key embedded in a community-contributed domain skill file. The key is publicly accessible and committed to the repository's default branch. It is a third-party service key, not an internal team credential — but a hardcoded API key in a committed file is a Gitleaks finding regardless of origin.

**Reason for rejection:** Hardcoded API key committed to the public repository at `agent-workspace/domain-skills/metacritic/scraping.md`. Per SOP: any unresolved Gitleaks finding → REJECTED.

**What would clear it:** Repository maintainers remove the hardcoded key from `agent-workspace/domain-skills/metacritic/scraping.md` and replace it with a placeholder (e.g., `API_KEY = "<REDACTED-S264>"`), confirm no other committed files contain hardcoded credentials, and release a new version. Soren re-scans the cleared version — full pipeline, no abbreviated process.

**Freshness note (2026-06-08):** Hardcoded key confirmed still present on latest main branch. REJECTED status unchanged. Stars have grown significantly (4.3k → 14.5k), indicating strong community momentum — worth re-checking once the key is removed.

**Re-reviewed 2026-06-08 — verdict confirmed. REJECTED stands.** The disqualifying finding — hardcoded Metacritic API key in `agent-workspace/domain-skills/metacritic/scraping.md` — is confirmed still present per Rose's freshness sweep. Star growth (4.3k → 14.5k) is noted and encouraging for future consideration, but star count is irrelevant to a Gitleaks finding. This resource does not enter the library until the key is removed, a new version is released, and a full re-scan is completed.

## Recommendation

Queue for Soren security review. If cleared: add to Section 3, Tier 2. Activate when an agent needs browser automation capability. The self-healing mechanic is novel — read the SKILL.md file during onboarding before production use.

---

## C&P Summary

Browser Harness is a lightweight Python tool that lets an AI agent like Claude Code control a real Chrome browser directly — no heavy framework required. What makes it unusual is that when the agent needs a capability that doesn't exist yet, it writes the missing code itself and keeps going without stopping. It is built by the same organization behind browser-use (one of the most-starred browser automation repos on GitHub) and is intentionally kept tiny — about 600 lines of Python total. For this project, it is the lightest available path to giving any agent on the team real browser access, which matters whenever work involves navigating websites, filling forms, or pulling information from the web.

---

## Sources

- [GitHub — browser-use/browser-harness](https://github.com/browser-use/browser-harness)
- [GitHub — browser-use/browser-harness-js (TypeScript sibling)](https://github.com/browser-use/browser-harness-js)
- [GitHub — browser-use organization repositories](https://github.com/orgs/browser-use/repositories)
- [Commit history — browser-use/browser-harness](https://github.com/browser-use/browser-harness/commits/main)
- [Gist — Hermes Agent + Browser Harness setup commands](https://gist.github.com/davidondrej/6f158de34ce83c530526011054fde8d3)

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
