# Resource Report: Andrej Karpathy Skills (CLAUDE.md)

**URL:** https://github.com/multica-ai/andrej-karpathy-skills (transferred from forrestchang/andrej-karpathy-skills — old URL redirects)
**Site:** https://www.claudepluginhub.com/plugins/forrestchang-andrej-karpathy-skills
**Date Researched:** 2026-04-21
**Researched by:** Rose | Security pre-check: Soren (pending) | Report by: Rose
**Already in Master Library?** No — new submission, Batch 1

---

## What It Is

A single `CLAUDE.md` configuration file (plus a Claude Code plugin wrapper) that improves Claude Code's coding behavior by embedding four principles derived from Andrej Karpathy's documented observations on common LLM coding mistakes.

## What It Does

- Ships as a `CLAUDE.md` file that can be dropped into any project root or merged with an existing one — Claude Code auto-loads it at session start
- Also installable as a Claude Code plugin via the plugin marketplace
- Cursor support included: a `.cursor/rules/karpathy-guidelines.mdc` file applies the same rules in Cursor
- The four principles it encodes:
  1. **Think Before Coding** — surface hidden assumptions, flag confusion, and identify tradeoffs before writing any code
  2. **Simplicity First** — write the minimum code that solves the problem; no speculative features, no unnecessary abstractions
  3. **Surgical Changes** — modify only what the request requires; do not refactor unrelated sections or touch code that isn't fully understood
  4. **Goal-Driven Execution** — define verifiable success criteria; let the AI loop toward completion rather than following prescriptive step-by-step instructions

## Technical Details

- **Language:** Markdown (100%) — no code, no dependencies, no install required
- **License:** MIT
- **Stars:** ~171k (as of June 2026) — exceptionally high for a single-file Markdown repo
- **Forks:** ~17.5k
- **Contributors:** Forrest Chang (primary) + community PRs
- **Last Commit:** April 20, 2026 — actively maintained
- **Created by:** Forrest Chang (GitHub: forrestchang)
- **Origin:** Karpathy's observations on LLM coding pitfalls — the repo translates those observations into an actionable `CLAUDE.md` ruleset

## How It Works

The `CLAUDE.md` file is injected into every Claude Code session automatically when placed in a project root. No runtime, no server, no install script — it is plain text that shapes Claude Code's behavior from the system prompt level. The plugin marketplace version wraps the same file for one-command installation: `/plugin marketplace add forrestchang/andrej-karpathy-skills`.

## Relevance to This Project

Directly relevant to how this team operates. The four principles (think first, stay simple, surgical changes, goal-driven execution) align with Jay's operating standards and the behavioral rules already in Sage's soul and the agent souls. This is not a new tool — it is a well-validated behavioral overlay for Claude Code that reinforces what the team already tries to do. High-signal, zero-risk, no dependencies.

## Builder Footprint

- **Integration type:** CLAUDE.md behavioral overlay — pure Markdown file; install via Claude Code plugin marketplace (`/plugin marketplace add forrestchang/andrej-karpathy-skills`) or drop `CLAUDE.md` into any project root; Cursor support also included (`.cursor/rules/karpathy-guidelines.mdc`)
- **Extension points:** Four principles are individually editable plain-text blocks — Cosmo can merge select principles into the project `CLAUDE.md` rather than maintaining a separate file; the report recommends inline merging to reduce tracking overhead (Inferred from documentation — not explicitly documented)
- **Build complexity signal:** Lowest possible — single Markdown file; zero dependencies, zero executables, zero configuration; auto-loads at Claude Code session start when placed in project root
- **Known conflicts:** None. If merged into the existing project `CLAUDE.md`, verify that the four principles do not contradict any soul-level behavioral rules already defined (they are designed to be complementary, but a quick read confirms it). Compatible with all other Section 2 skills.

## Master Library Assessment

- **Proposed Section:** 2 — Skills (Claude Code Skills / Behavioral Overlays)
- **Proposed Tier:** 1
- **Rationale:** This is a skill in the exact technical sense — a `CLAUDE.md` file loaded via the Claude Code plugin system. 71.5k stars is exceptional validation for a Markdown file. Tier 1 because it is immediately applicable to every session, zero-cost to install, and directly reinforces existing team behavioral standards. No Soren security review needed — it is plain Markdown text with no executable components.

## Soren Security Pre-check

- **Verdict:** LOW RISK — recommend expedited review
- **Notes for Soren:** Pure Markdown file, no code, no executables, no install script, no network calls. Only risk: content of the `CLAUDE.md` could theoretically contain prompt injection or behavioral overrides that conflict with project standards. Recommend a quick read of the actual file content before adoption — likely a 5-minute review. MIT license.
- **Re-reviewed 2026-06-08 — verdict confirmed. Repo transfer assessed.** Rose's v2.0 sweep flagged the repo transfer from forrestchang/andrej-karpathy-skills to multica-ai/andrej-karpathy-skills. Transfer is legitimate: (1) the old URL redirects cleanly to the new org — no content disruption; (2) Multica is documented in Rose's v1.0 freshness sweep as companion work by the same original author (Forrest Chang); (3) the transfer aligns with a known pattern of open-source developers moving popular repos under an org account as the project matures; (4) stars (~171k) and fork counts (~17.5k) are consistent with the repo's growth trajectory — no anomalous activity post-transfer; (5) no license change, no new executable components, still pure Markdown. No red flags detected in the transfer. LOW RISK verdict stands. The formal "expedited review" step (read the CLAUDE.md file content before adoption) remains the only required step before deployment — this condition is unchanged.

## Recommendation

Fast-track through Soren (content read, not a full audit). Add to Section 2, Tier 1. Consider merging its four principles into the existing project `CLAUDE.md` at next session rather than maintaining a separate plugin — this avoids one more thing to track and the principles are simple enough to inline.

---

## C&P Summary

This is a single text file — about one page long — that improves how Claude Code behaves when writing code. It was created by a developer named Forrest Chang based on public observations by Andrej Karpathy (a well-known AI researcher and former Tesla AI director) about mistakes AI tools consistently make when coding: running on wrong assumptions, overcomplicating things, changing code they shouldn't touch, and following steps instead of working toward a real goal. Dropping the file into a project folder makes Claude Code apply those four lessons automatically on every session. It has 71,000 stars on GitHub — which for a single-page text file is extraordinary — meaning a very large number of developers find it genuinely useful. For this project, it is the simplest possible upgrade to Claude Code's coding discipline, with no installation risk and no ongoing maintenance.

---

## Sources

- [GitHub — forrestchang/andrej-karpathy-skills](https://github.com/forrestchang/andrej-karpathy-skills)
- [CLAUDE.md file — forrestchang/andrej-karpathy-skills](https://github.com/forrestchang/andrej-karpathy-skills/blob/main/CLAUDE.md)
- [Claude Plugin Hub — andrej-karpathy-skills](https://www.claudepluginhub.com/plugins/forrestchang-andrej-karpathy-skills)
- [Trendshift — forrestchang/andrej-karpathy-skills trending stats](https://trendshift.io/repositories/21654)
- [Antigravity.codes — Karpathy's CLAUDE.md Skills File: The Complete Guide](https://antigravity.codes/blog/karpathy-claude-code-skills-guide)
- [Commit history — forrestchang/andrej-karpathy-skills](https://github.com/forrestchang/andrej-karpathy-skills/commits/main)

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
