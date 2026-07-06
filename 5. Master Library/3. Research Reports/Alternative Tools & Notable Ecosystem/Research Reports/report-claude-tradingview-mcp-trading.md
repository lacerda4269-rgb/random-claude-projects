# Resource Report: Claude + TradingView MCP — Automated Trading (jackson-video-resources)

**URL:** https://github.com/jackson-video-resources/claude-tradingview-mcp-trading
**Date Researched:** 2026-04-18
**Researched by:** Rose | Security pre-check: Soren (pending) | Report by: Rose
**Already in Master Library?** No — Rose Research Round 2 (Session 60)

---

## What It Is

A Claude Code + TradingView workflow repo that reads live TradingView chart data and executes automated trades on BitGet (and other exchanges), deployed to a cloud scheduler for 24/7 operation.

## What It Does

- Connects Claude Code to TradingView (via an existing TradingView MCP) and a crypto exchange (BitGet primary, Binance/Bybit/OKX/Coinbase/Kraken/KuCoin/Gate.io/MEXC/Bitfinex documented)
- Reads a user-defined `rules.json` strategy file; checks all entry conditions against live indicator data before placing any trade
- Calculates MACD from raw candle data and evaluates market bias (bullish / bearish / neutral)
- Enforces configurable safety guardrails: daily trade cap, max trade size, max 1% portfolio risk per trade
- Logs every decision to `safety-check-log.json` and every executed trade to a tax-ready `trades.csv`
- Deployable to Railway for cloud-based cron scheduling (runs without TradingView Desktop in cloud mode — pulls from Binance's free market API instead)
- Includes a one-shot Claude Code prompt (`prompts/02-one-shot-trade.md`) that handles onboarding end-to-end
- Includes a strategy extraction prompt (`prompts/01-extract-strategy.md`) for building `rules.json` from YouTube trader transcripts via Apify
- Paper trading mode included (`PAPER_TRADING=true`) — logs decisions without placing real orders
- **Stars:** 468 | **Forks:** ~105 | **Language:** JavaScript (Node.js 18+) | **License:** None listed
- **Created:** 2026-04-07 | **Last pushed:** 2026-04-09 | **Updated:** 2026-06-08
- **Maintainer:** jackson-video-resources (organization account; YouTube channel "Lewis Jackson" implied by affiliate links in README)
- **Dependencies:** `dotenv`, `node-fetch` — extremely minimal
- **Note:** No new releases published; repo appears dormant since April 9.

## Relevance to This Project

This is not a standalone MCP server — it is a **workflow repo** that sits on top of the existing TradingView MCP. It requires the atilaahmettaner TradingView MCP (or the jackson-video-resources variant) to already be installed and running. That distinction matters: this is an application layer, not an infrastructure layer.

For this project's workflow, the relevance is real but indirect. Todd (TradingView/PineScript specialist) and Nick (NinjaTrader) are the primary trading workflow agents. This repo is most useful as a reference for how a working Claude + TradingView + exchange execution pipeline is structured — specifically the `rules.json` strategy pattern, the one-shot prompt architecture, and the safety check model. Pete (Python/quant) would likely approach this differently (Python vs. Node.js), but the design pattern is instructive.

**Comparison to the existing library entry (atilaahmettaner/tradingview-mcp):**
The atilaahmettaner repo is the underlying MCP infrastructure — it exposes TradingView data to Claude via the MCP protocol (technical indicators, screening, backtesting, no API keys required, Python-based). This jackson-video-resources repo is the application built on top of it — it adds exchange connectivity, trade execution, risk rules, and cloud scheduling. They are complementary, not competing. The atilaahmettaner MCP is the data layer; this is the execution layer.

## Master Library Assessment

- **Proposed Section:** 8 — Alternative Tools & Notable Ecosystem
- **Proposed Tier:** 2
- **Rationale:** This is not an MCP server and should not be filed in Section 4 — it is an application workflow that depends on Section 4 infrastructure. Section 8 is the right home: it is a notable ecosystem item that demonstrates a working pattern, is worth knowing about, and may inform how we build our own execution layer — but it is not something we install or integrate directly. Tier 2 because the execution pattern (rules.json + safety check + one-shot prompt) is genuinely useful reference material once trading workflow begins.

## Soren Security Pre-check

- **Verdict:** FLAG
- **Date reviewed:** 2026-04-18
- **Checked:** License status, author/org provenance, dependency surface, API credential handling, bot.js network call patterns, cloud deployment model, affiliate disclosure.
- **Notes:** No license declared — all-rights-reserved by default. This is a hard stop for any code reuse or adaptation from this repo. If any patterns from bot.js (rules.json structure, safety check logic, one-shot prompt architecture) are adapted into our own build, that requires either a license being added by the author or our own independent implementation from scratch. Filing as a reference item is fine — adapting its code without a license is not.
  Organization account (jackson-video-resources) has limited public history, which reduces provenance confidence. The connection to a YouTube channel (Lewis Jackson) is noted — the repo appears to be companion content for a video, which is a legitimate but commercial context. The BitGet affiliate link in the README is a commercial signal, not a security red flag.
  The repo is twelve days old at time of research. 156 stars and 105 forks for a two-week-old repo attached to a YouTube channel is plausible organic growth from video traffic. Not artificially inflated based on the fork-to-star ratio, but community vetting is effectively zero.
  Dependency surface is minimal and clean: dotenv and node-fetch only. No supply chain concern at the package level. bot.js (20KB) should be reviewed at any point before code patterns are adapted — specifically to confirm no undisclosed network calls (beyond the documented Binance public API pull and exchange API calls), no telemetry, and no credential exfiltration paths.
  Exchange API credential handling: .env excluded from git, README warns explicitly. Pattern is implemented correctly. If this repo were ever deployed, the credential management would need a separate review — specifically: key scoping (read-only vs. trade-enabled), key rotation policy, and Railway environment variable security. That review is only relevant if deployment is ever considered, which it is not for this library entry.
  FLAG conditions: (1) No code adaptation without license resolution. (2) bot.js review required before any adaptation of its code patterns. Filing as Section 8 Tier 2 reference is clear — this flag applies to code reuse, not to filing or study.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Stars 156 → 468; last pushed confirmed still 2026-04-09 (dormant since April). No license added. Both FLAG conditions unchanged. Repo is now eight weeks dormant — further reduces suitability for any future deployment consideration. FLAG stands.

## Recommendation

File in Section 8 (Alternative Tools & Notable Ecosystem) as a Tier 2 reference item. The execution pattern — rules.json strategy, safety check architecture, one-shot Claude Code prompt, tax-ready logging — is solid reference material for when we build our own trading execution layer. The no-license flag should be noted clearly. Not a direct install candidate.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---
*Report by Rose | Session 60 | 2026-04-18*
*Updated by Rose | Session 230 | 2026-06-08*

---

## C&P Summary

This is a GitHub repo by a YouTube creator (Lewis Jackson) that shows how to use Claude Code and TradingView together to actually execute cryptocurrency trades automatically. You point it at your TradingView chart, it reads your strategy rules from a configuration file, checks all the conditions are met, and then places the trade on your exchange (BitGet, Binance, and several others are supported). It also logs every trade in a tax-ready spreadsheet and can run 24/7 in the cloud via a service called Railway. It is not the TradingView MCP itself — it is a workflow application built on top of one. The one already in the library (atilaahmettaner) is the data connection; this is the trading bot that uses that connection. For this project, it is most useful as a reference for how a Claude-driven execution pipeline is structured, rather than something we would install directly. Stars grew from 156 → 468 (updated 2026-06-08) — still no license, no new commits since April 9, 2026. The no-license FLAG remains in effect for any code reuse.
