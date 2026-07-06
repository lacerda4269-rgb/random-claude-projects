# Resource Report: last30days-skill

**URL:** https://github.com/mvanhorn/last30days-skill
**Date Researched:** 2026-06-08
**Researched by:** Rose | Security pre-check: Soren | Report by: Rose
**Already in Master Library?** No — external GitHub repository, first submission

---

## What It Is

`/last30days` is a Claude Code skill (and multi-harness agent skill) that functions as a multi-source social intelligence research engine. Given any topic — a person, company, product, trend, or event — it searches Reddit, X/Twitter, YouTube, TikTok, Instagram, Hacker News, Polymarket, GitHub, Bluesky, Threads, Pinterest, TruthSocial, and the web in parallel, scores results by real user engagement (upvotes, likes, view counts, prediction market odds), and synthesizes a grounded, citation-backed research brief. It is a Python-backed skill with a 1,400+ line runtime contract (SKILL.md) that governs exactly how the AI agent executes the pipeline. Current stable version is 3.3.2. It is authored by mvanhorn (Matt Van Horn) and licensed MIT.

---

## What It Does

- Searches 14+ platforms simultaneously for real-time social signal on any topic, scoring results by actual engagement rather than editorial judgment or SEO
- Resolves entities before searching — converts a person's name to their X handle, GitHub username, and relevant subreddits via a Python pre-research brain before any API call fires
- Clusters cross-source coverage of the same story into single items (Reddit + X + YouTube on the same event = one merged cluster, not three entries)
- Runs competitor comparisons in a single parallel pass — "OpenAI vs Anthropic vs xAI" fans out 3 full pipelines simultaneously and merges into a side-by-side brief
- Emits a shareable self-contained HTML brief on request, saved to a configurable output directory
- Scores results on both relevance and humor/virality (dual-judge system); surfaces "Best Takes" — cleverest one-liners from the community
- Operates free at baseline: Reddit, Hacker News, Polymarket, and GitHub work with no API keys; X via browser cookie extraction; YouTube via yt-dlp
- Unlocks additional sources progressively via optional API keys: ScrapeCreators (TikTok, Instagram, Threads, Pinterest), xAI (X), Brave/Exa/Serper (web search), Bluesky (app password), OpenRouter (Perplexity deep research)
- Supports a `--competitors` flag that auto-discovers top peers via WebSearch and runs full pipeline per entity
- Saves raw output as slug-named markdown files to a configurable local directory (default: `~/Documents/Last30Days/`)
- Includes a `--diagnose` flag that prints per-source availability without running a full search — useful for setup verification
- Ships with 1,012 passing tests and active CI (validate, security, release workflows on GitHub Actions)

---

## Relevance to This Project *(as of research date — context may not carry to future projects)*

This skill is directly relevant to the Master Library as a Tier 1 candidate for the Skills section. The MIP is building out a library of deployable capabilities for the agent team; a battle-tested, widely adopted research skill with 33,000+ GitHub stars and active maintenance addresses a standing need. Rose's current research lane covers CLI-based internet access — this skill extends that surface substantially by aggregating social platforms that have no single CLI equivalent. For Jay specifically, the use cases documented in the README (pre-meeting intelligence, product trend research, learning something fast before building it) map directly to how he works. This could become a standing research augmentation tool for the team, usable by Rose as a sub-capability or by any agent needing rapid social signal on a topic.

---

## Builder Footprint

- **Integration type:** Skill-composable / CLI-invocable / Hook-triggerable
- **Extension points:** The Python engine accepts CLI flags (`--emit`, `--search`, `--days`, `--deep`, `--competitors`, `--github-user`, `--diagnose`, `--save-dir`, `--save-suffix`); output is structured markdown or HTML saved to disk; the engine's library modules (lib/pipeline.py, lib/planner.py, lib/fanout.py, lib/render.py) are individually importable for custom integrations. The `.claude-plugin/plugin.json` and `marketplace.json` files expose the standard Claude Code plugin contract. Hooks can trigger on skill output files via the configurable output directory.
- **Build complexity signal:** Simple (~1–2 hours) — install via `/plugin marketplace add mvanhorn/last30days-skill` in Claude Code; zero additional build required for baseline use. Moderate (~half-day) if wrapping the Python engine in a custom skill or integrating output into a pipeline that reads the saved markdown files.
- **Known conflicts:** None identified — this is an additive research capability. No overlap with existing cataloged items detected.

---

## Master Library Assessment

- **Proposed Section:** Section 3 — Skills
- **Proposed Tier:** 1
- **Rationale:** Actively maintained (latest commit 2026-06-06), 33,741 stars, 2,778 forks, MIT license, 1,012 passing tests, CI security workflow, extensive documentation. Directly installable via Claude Code's plugin marketplace with zero configuration for baseline use. Addresses a genuine standing need (multi-source real-time social research) that no other current ML item covers.

---

## Soren Security Pre-check

- **Verdict:** CLEARED WITH CONDITIONS
- **Checked:** 2026-06-08 — Soren full source review (chrome_cookies.py, safari_cookies.py, security.yml, bird-search vendor directory — all 12 JS files reviewed)
- **Reviewed by:** Soren

### Verdict Summary

**CLEARED WITH CONDITIONS.** No malicious behavior, no data exfiltration, no third-party transmission of credentials or cookie values confirmed across all reviewed source files. Two conditions attached — one operational, one advisory — both manageable at install time. Lexi is cleared to file.

### Rose's Flags — Soren Findings

| # | Severity | Flag | Soren Finding | Disposition |
|---|----------|------|---------------|-------------|
| 1 | HIGH | Cookie/token extraction from local browser | **CLEARED.** Verified read-only behavior. `chrome_cookies.py` uses `subprocess` only to call macOS system `openssl` and `security find-generic-password` (Keychain access) — both are local, no network. Zero `requests`, `urllib`, `http`, `socket`, or any other network import in either file. Safari extractor parses `~/Library/Cookies/Cookies.binarycookies` from local filesystem only — zero network calls. Logging of cookie values is at DEBUG level only and logs error conditions (decryption failures, DB not found) — not the cookie values themselves. Cookie data is returned to the calling pipeline and used to authenticate against Twitter/X's own API — confirmed in bird-search vendor code. No third-party transmission found. | No condition required. |
| 2 | HIGH | API key handling — `.env` file with broad secrets scope | **CLEARED WITH CONDITION.** No key leakage to logs or output files found in reviewed source. The `chmod 600` documentation note is accurate — file permissions are not programmatically enforced at runtime. This is standard for `.env`-based tools across the ecosystem. **Condition:** At install, operator should manually set `chmod 600 ~/.config/last30days/.env` (or equivalent for Windows analog). This is a one-time step and is documented by the maintainer. | Condition 1 attached. |
| 3 | MEDIUM | Security CI advisory-only, not blocking | **NOTED — advisory accepted.** Verified in `security.yml` source. Both `pip-audit` and TruffleHog jobs carry `continue-on-error: true` with explicit maintainer comments: *"Advisory-first: visibility before enforcement… Set continue-on-error: false once a clean baseline run is confirmed."* This is a legitimate staged approach for a project with broad optional dependency surface. No open issues with a `security` label exist on the repo. The tool does not block merges on CVEs today, which is a real gap — but acceptable for a Tier 1 library resource given the advisory framing and active CI presence. | Advisory noted. No blocking condition. |
| 4 | MEDIUM | Vendored third-party JavaScript | **CLEARED.** Full review of all 12 files in `skills/last30days/scripts/lib/vendor/bird-search/` (bird-search.mjs + 11 lib/*.js files). Zero eval(), atob(), obfuscation, or external non-Twitter network calls anywhere in the vendor tree. `twitter-client-base.js` uses native Node.js `fetch()` — confirmed to call Twitter/X API endpoints only; zero outbound URLs to any other host detected across all files. Vendor code is a clean subset of `@steipete/bird` v0.8.0 (MIT licensed, credited in file header). Not managed by npm but the code is small, readable, and fully auditable. | No condition required. |
| 5 | LOW | 119 open GitHub issues | **CLEARED.** Zero open issues with a `security` label confirmed via GitHub API. High issue count is consistent with a 33,000+ star project with active community use. Not a security concern. | No condition required. |
| 6 | INFO | No required env vars at baseline | **CONFIRMED POSITIVE.** Zero env vars required at install. Good security posture. | No action. |

### Conditions

**Condition 1 (Operational — apply at install):** Set restrictive file permissions on the env file at first-time setup: `chmod 600 ~/.config/last30days/.env`. Document in any install runbook or team SOP that references this skill. This is a one-time step already documented by the maintainer; the condition is to make it explicit and tracked rather than optional.

### What Was Reviewed

- `skills/last30days/scripts/lib/chrome_cookies.py` — full source, network and logging analysis
- `skills/last30days/scripts/lib/safari_cookies.py` — full source, network analysis
- `.github/workflows/security.yml` — full source, CI configuration
- `skills/last30days/scripts/lib/vendor/bird-search/bird-search.mjs` — full source
- `skills/last30days/scripts/lib/vendor/bird-search/lib/` — all 11 JS files (cookies.js, twitter-client-base.js, twitter-client-search.js, twitter-client-utils.js, twitter-client-features.js, twitter-client-constants.js, twitter-client-types.js, runtime-features.js, runtime-query-ids.js, paginate-cursor.js, features.json, query-ids.json)
- GitHub Issues API — security-labeled open issues
- GitHub API — repository metadata and directory structure

---

## Recommendation

Add to Master Library at Section 3 (Skills), Tier 1, pending Soren clearance. The cookie extraction and `.env` key handling flags are worth a close look but are not expected to be blockers — both are standard patterns for this class of tool and the implementation appears careful. Install for Claude Code is one command with auto-updates. Recommend Soren focus review on the browser cookie extraction modules and the vendored bird-search JS library.

---

## C&P Summary

`/last30days` is a research skill for Claude Code (and other AI agent hosts) that searches Reddit, X/Twitter, YouTube, TikTok, Instagram, Hacker News, prediction markets, GitHub, and more — all at once — on any topic you give it. Instead of ranking results by SEO or editorial picks, it scores them by what real people actually engaged with: upvotes, likes, video views, and real money bet on prediction markets. It synthesizes everything into one clean research brief with citations. It works at no cost out of the box (Reddit, Hacker News, and Hacker News require no API keys), and progressively unlocks more platforms as you add optional API credentials. It is authored by Matt Van Horn, has over 33,000 GitHub stars, is MIT licensed, actively maintained, and installs in Claude Code with a single command.

---

*Report by Rose | Session 230 | 2026-06-08*
