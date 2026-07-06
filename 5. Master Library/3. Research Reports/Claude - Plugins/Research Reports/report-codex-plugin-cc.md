# Resource Report: codex-plugin-cc

**URL:** https://github.com/openai/codex-plugin-cc
**Date Researched:** 2026-06-08
**Researched by:** Rose | Security pre-check: Soren | Report by: Rose
**Already in Master Library?** No — new item

---

## What It Is

codex-plugin-cc is an official OpenAI Claude Code plugin that brings OpenAI's Codex agent into the Claude Code workflow. It installs via the Claude Code plugin marketplace and adds a set of slash commands that let you run Codex code reviews, adversarial challenge reviews, and background task delegation without leaving Claude Code. Requires a ChatGPT subscription (including Free tier) or OpenAI API key. Apache 2.0 licensed. JavaScript. 20,439 stars. Last pushed April 2026 — not actively maintained since then.

---

## What It Does

- /codex:review — runs a Codex read-only code review on current uncommitted changes or a branch diff; supports --base <ref>, --wait, and --background flags
- /codex:adversarial-review — steerable challenge review; accepts custom focus text to target specific decisions or risk areas
- /codex:rescue — delegates a stuck or blocked task to Codex as a background agent; returns results when done
- /codex:status — checks status of a running background Codex job
- /codex:result — retrieves output from a completed background job
- /codex:cancel — cancels a running background job
- Adds a codex:codex-rescue subagent accessible via /agents
- /codex:setup — guided setup wizard that checks Codex readiness and offers to install if missing

---

## Relevance to This Project *(as of research date — context may not carry to future projects)*

Jay has an active OpenAI subscription. This plugin is the bridge between Claude Code and Codex — it enables second-opinion code reviews from Codex without leaving the Claude Code environment, and enables background task delegation to Codex when Claude Code is occupied with other work. The adversarial review command is particularly useful for pressure-testing decisions before committing to them. The background job model (rescue/status/result) provides a lightweight parallel agent pattern that does not require building a full agent team.

---

## Builder Footprint

- **Integration type:** Claude Code plugin (Section 7 format); installs via /plugin marketplace add openai/codex-plugin-cc; provides slash commands; no MCP server, no additional daemon
- **Extension points:** Slash commands are the interface; /codex:rescue accepts arbitrary task descriptions; --background flag enables fire-and-forget pattern
- **Build complexity signal:** Low — /plugin install, /reload-plugins, /codex:setup; requires Codex CLI installed (npm install -g @openai/codex) and OpenAI login
- **Known conflicts:** Requires Node.js 18.18+; review codex-plugin-cc version compatibility if Codex CLI is updated after April 2026 (last push date)

---

## Master Library Assessment

- **Proposed Section:** 7 — Claude Plugins
- **Proposed Tier:** 2
- **Rationale:** Official OpenAI plugin, Apache 2.0, 20k+ stars. Tier 2 because Jay has an active OpenAI subscription making this immediately usable, but the April 2026 last-push date means active development appears to have stalled — watch for updates before prioritizing deployment. Section 7 (Claude Plugins) is the correct home.

---

## Soren Security Pre-check

- **Verdict:** CLEARED WITH CONDITIONS
- **Checked:** License (Apache 2.0 — permissive, confirmed), stars (20,439), forks (1,239), last pushed (2026-04-18 — approximately 7 weeks before research date), language (JavaScript), maintainer (openai — official OpenAI organization, authoritative source), open issues (222), data routing model (all code transmitted to OpenAI Codex API — expected, documented, unavoidable), no obfuscated code or undisclosed endpoints
- **Notes:**

| # | Severity | Flag | Notes |
|---|----------|------|-------|
| 1 | HIGH | Code egress to OpenAI API | All code submitted via `/codex:review` and `/codex:rescue` is transmitted to OpenAI's Codex API for processing. This is expected, documented behavior — same as using Codex directly. Not a disqualifier given Jay's active OpenAI subscription, but must be a conscious decision on every use. Do not use on code that cannot leave the local environment. Confirm OpenAI's data handling and retention terms before use on any sensitive or proprietary project. |
| 2 | MEDIUM | Stale maintenance — 7 weeks without commits | Last pushed 2026-04-18. 222 open issues without recent activity is a stale maintenance signal for a plugin that wraps a fast-moving CLI (Codex). Risk: version incompatibility if Codex CLI updates break the plugin interface. Monitor before treating as a long-term dependency. Not a security issue — a reliability flag. |
| 3 | LOW | OpenAI API key handling | If API key is used instead of ChatGPT login, it must be set via environment variable only — never hardcoded in any file. Standard practice; flagged for hygiene enforcement. |
| 4 | INFO | Official OpenAI source | Repository published under the official OpenAI GitHub organization. Authoritative source — no supply chain or impersonation risk. |

*Reviewed by Soren | 2026-06-08*

---

## Recommendation

Add to Section 7 (Claude Plugins), Tier 2. Route to Soren for standard clearance. When cleared, install via the Claude Code plugin marketplace. Useful immediately given Jay's active OpenAI subscription — run /codex:adversarial-review before any significant code commit for a second-opinion pressure test. Note the stale maintenance signal; revisit if OpenAI resumes active updates.

---

## C&P Summary

codex-plugin-cc is an official OpenAI plugin for Claude Code that lets you run Codex code reviews and delegate tasks to Codex without leaving your Claude Code session. Once installed, you get slash commands for standard reviews, adversarial challenge reviews (which pressure-test specific decisions), and background task delegation — where you hand off a stuck problem to Codex and retrieve the result when it is done. It requires a ChatGPT subscription (including Free tier) or an OpenAI API key. Apache 2.0 licensed, 20,439 stars, published by OpenAI officially. The main flag: development appears to have stalled since April 2026 — there have been no commits in roughly 7 weeks. Still fully functional, but worth watching before treating it as a long-term dependency.

---

*Report by Rose | Session 230 | 2026-06-08*