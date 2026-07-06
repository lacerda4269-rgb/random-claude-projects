# Resource Report: Kronos

**URL:** https://github.com/shiyu-coder/Kronos
**Date Researched:** 2026-04-12 | **Updated:** 2026-06-08
**Researched by:** Rose | Security pre-check: Soren | Filed by: Lexi (v1.0) / Rose update (v1.1)
**Already in Master Library?** No — new item

---

## What It Is
Kronos is an open-source foundation model built specifically for financial market forecasting using K-line (candlestick) data from global exchanges. Developed by Yu Shi and collaborators; accepted at AAAI 2026. It is not a general-purpose time series model — it is purpose-built for the structure and noise characteristics of market data.

## What It Does
Two-stage framework: a specialized tokenizer converts continuous OHLCV (open, high, low, close, volume) data into discrete tokens, which a transformer model then processes for forecasting tasks. Users can generate price predictions, run backtests, and fine-tune models on custom datasets. Covers 45+ global exchanges. Fine-tuning scripts released August 2025. **Updated 2026-06-08:** 28,967 stars (up from 14.8k — significant growth). Last pushed: 2026-04-13 — no new commits in approximately 7 weeks. 216 open issues.

## Relevance to This Project
High relevance to the trading strategy side of this project — directly applicable to Pete (Python) workflows for quantitative research and strategy development. Could be used alongside NinjaTrader and TradingView work as a forecasting layer. AAAI 2026 acceptance adds credibility. This is research-grade tooling, not a plug-in-and-trade solution — operator should treat it as a model resource requiring integration effort.

## Master Library Assessment
- **Proposed Section:** 8 — Alternative Tools & Notable Ecosystem
- **Proposed Tier:** 2
- **Rationale:** Strong trading relevance and research credibility but requires significant integration effort to put to use. Not a ready-to-run tool — a framework that Pete would build around. Tier 2 for high value, phase-dependent use.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked (updated 2026-06-08):** License (MIT — permissive, confirmed), stars (28,967 — up from 14.8k; nearly doubled), forks (4,993 — up from 2.9k), open issues (216), authorship (Yu Shi et al. — academic, AAAI 2026 publication), dependency stack (PyTorch, Transformers, pandas — all standard scientific Python packages, no supply chain concerns), last pushed (2026-04-13 — 7 weeks inactive as of update), community activity (issues opened June 2026 — community still engaged), optional integrations (Qlib — legitimate quant research framework; Comet.ml — legitimate ML experiment tracker), no known CVEs
- **Notes:**
  1. **Maintenance assessment — not abandoned:** Despite 7 weeks without commits, new issues were opened in June 2026 by community members, indicating ongoing external engagement. Pattern is consistent with an academic research release where the codebase is considered feature-complete post-paper. Authors' primary delivery (AAAI 2026 paper + fine-tuning scripts) has shipped. The project is likely in maintenance mode, not abandonment. Monitoring at next review cycle is warranted.
  2. **Star growth (14.8k → 28,967 in ~8 weeks):** Rapid growth increases community scrutiny. No new security issues surfaced with the expanded user base — positive signal.
  3. **Open issues (216):** Mix of feature requests, integration questions, and usage support. No unresolved security issues identified.
  4. MIT license and academic backing remain clean. CLEARED verdict confirmed. No conditions added.

*Reviewed by Soren | 2026-06-08*

## Recommendation
File to Section 8 — Alternative Tools & Notable Ecosystem, Tier 2. Strong pick for the trading research phase — Pete is the primary owner when it comes time to use it. No operator decisions required at intake.

---
*Report by Rose + Sage | Session 39 | 2026-04-12*

---

---

## Report Version Log

| Version | Date | What Changed |
|---------|------|--------------|


## C&P Summary

Kronos is an open-source foundation model built specifically for financial market forecasting using K-line (candlestick/OHLCV) data from 45+ global exchanges — purpose-built for the noise and structure of market data, not general time series. Accepted at AAAI 2026. It uses a two-stage framework: a specialized tokenizer converts continuous price/volume data into discrete tokens, which a transformer then processes for forecasting, backtesting, and fine-tuning tasks. Directly applicable to Pete's quantitative research workflows when the project reaches the trading strategy build phase — this is research-grade tooling that requires integration effort, not a plug-in-and-trade solution. 28,967 stars (updated 2026-06-08; nearly doubled since original research in April), MIT licensed. Note: no new commits since 2026-04-13 — watch maintenance status.

*Updated by Rose | Session 230 | 2026-06-08*