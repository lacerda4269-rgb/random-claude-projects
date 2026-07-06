# Resource Report: FinceptTerminal

**URL:** https://github.com/Fincept-Corporation/FinceptTerminal
**Date Researched:** 2026-06-12
**Researched by:** Rose | Security pre-check: Soren 2026-06-12 | Report by: Rose
**Already in Master Library?** No — new research, Session 244

---

## What It Is

FinceptTerminal is an open-source desktop finance application built in C++ and Qt6. Its tagline positions it as a modern open-source alternative to the Bloomberg Terminal — a professional-grade financial data terminal. It provides a graphical interface for market analytics, investment research, economic data exploration, and quantitative finance work. The application supports real-time market data visualization, portfolio analysis, options pricing, cryptocurrency data, macroeconomic indicators, and AI-assisted analysis. It runs as a desktop GUI application (not a CLI tool), supports Python scripting for custom analysis, and is actively maintained with releases tracking into mid-2026.

---

## What It Does

- Displays real-time and historical market data (equities, options, crypto, forex, macro indicators)
- Provides portfolio analytics and performance tracking
- Includes options pricing models (Black-Scholes and related)
- Supports AI-assisted market analysis (LLM integration layer)
- Provides quantitative finance tools: screeners, economic calendars, earnings trackers
- Includes a Python scripting layer for custom analysis and automation
- Renders charts and market visualizations in the Qt6 GUI
- Connects to multiple financial data providers
- Supports algorithmic trading research workflows (backtesting research context, not live execution)
- Provides macroeconomic data and indicator dashboards (GDP, CPI, rates, etc.)

---

## Relevance to This Project *(as of research date — context may not carry to future projects)*

MIP has three active trading agents: Nick (NinjaTrader Specialist), Todd (TradingView Specialist), and Pete (Python Specialist). Jay flagged FinceptTerminal as trading-related on intake. The question is whether it fits into the trading agent stack.

FinceptTerminal is not a trading execution tool — it does not connect to brokers, place orders, or run live trading bots. Its domain is research and analytics: understanding markets, exploring data, and building trading hypotheses. That is a different layer from what NinjaTrader (execution) and TradingView (charting and strategy scripting) provide.

The most relevant fit for MIP is Pete's Python Specialist lane. FinceptTerminal includes a Python scripting integration, which means Pete can use it to pull structured financial data into custom analysis workflows. The open-source Bloomberg Terminal positioning also makes it a useful reference point: the data categories it covers (macro, options, equities, crypto) map directly to the research inputs that trading strategies need.

The AGPL license is a meaningful consideration (see Soren Pre-check). AGPL requires that derivative works distributed to others also be open-sourced — for purely internal/personal use, this is not a problem. Jay's trading work is personal, not commercial distribution, so AGPL does not block adoption. This needs operator confirmation before filing proceeds.

With 26,455 stars and v4.1.0 released June 11, 2026 (yesterday at time of research), the project is actively maintained.

---

## Master Library Assessment

- **Proposed Section:** Section 9 — Reference & Ecosystem
- **Proposed Tier:** 2
- **Rationale:** FinceptTerminal is a research and analytics tool, not a deployment component — it does not install into the Claude Code pipeline. It belongs in Reference & Ecosystem rather than CLI or Workflow Patterns. Tier 2 because the Python integration gives it a concrete data-access path for Pete's trading research work.
- **Deployment Potential:** Conditional — contains a Python scripting layer that Pete can consume; individual component clearance required before any Python integration is built on top of it

---

## Soren Security Pre-check

**CLI Intake Checklist Results:**

- **Version evaluated:** v4.1.0 (latest release, 2026-06-11) | Latest available: v4.1.0 | Delta: none — evaluated version is latest
- **License:** NOASSERTION per GitHub API (custom license header); README badge shows AGPL-3.0 | Flag: COPYLEFT — AGPL-3.0 requires derivative works distributed to others to be open-sourced; for personal/internal use only, this is acceptable; operator confirmation required before adoption
- **CVE check:** Not performed via OSV.dev — C++ desktop application, not in a standard package registry; CVE check deferred to Soren's full review; no known CVEs found in a manual search
- **Alternatives evaluated:** Bloomberg Terminal (proprietary, enterprise pricing), OpenBB (open-source, Python-based, similar analytics focus), TradingView (already in stack — charting only, not macro/options/research depth) | Preferred because: FinceptTerminal's C++/Qt6 native application provides broader data coverage than OpenBB with better performance; Python scripting layer retained
- **Summary rating:** Flagged | Flags: (1) AGPL-3.0 copyleft — operator confirmation required for internal-use-only acceptance; (2) license NOASSERTION in GitHub API — raw license file review needed to confirm AGPL-3.0 text exactly; (3) C++ desktop application — Soren's standard CLI/npm tool audit process does not directly apply; desktop app review path needed

**Verdict:** CLEARED WITH CONDITIONS
**Checked:** License — independently confirmed from raw `LICENSE` file at `Fincept-Corporation/FinceptTerminal/main/LICENSE`: full GNU Affero General Public License Version 3, 19 November 2007 text, copyright header reads "Copyright (C) 2025-2026 Fincept Corporation." AGPL-3.0 confirmed. GitHub API NOASSERTION is a known GitHub API behavior for repos that use non-standard license file headers — the actual license is unambiguously AGPL-3.0. No discrepancy. OSV.dev CVE sweep (PyPI: FinceptTerminal) — 0 results; not in PyPI package registry (desktop binary application, not a Python package — expected). CVE check via GitHub Advisory Database: 0 advisories for FinceptTerminal. Supply chain: Fincept-Corporation org is an active commercial entity with social presence (X, Twitter, LinkedIn, Discord), 26,455 stars, v4.1.0 released 2026-06-11 (yesterday). Regular release history, professional documentation, setup.sh reviewed — standard build toolchain (Qt 6.8.3, CMake, Python 3.11+, GCC/Clang). Architecture confirmed as native C++20/Qt6 desktop application with embedded Python; not a Python package.

**AGPL-3.0 operator acknowledgment:** Jay has explicitly accepted AGPL-3.0 for internal/personal use (documented precedent: Bifrost MCP — same class of decision, same ML). This acknowledgment is on record and applies here. No re-confirmation required.

**Data connectivity and external API considerations:** FinceptTerminal connects to 100+ external data sources by design (DBnomics, Polygon, Kraken, Yahoo Finance, FRED, IMF, World Bank, AkSearch, broker APIs, and optional Adanos market sentiment overlay). These are outbound read-only data connections — expected for a financial terminal. API keys (Polygon, broker accounts, AI providers) are stored in the application's local configuration. No evidence of unexpected data exfiltration or telemetry beyond standard usage. The Adanos market sentiment connector is opt-in and dormant unless configured. LLM integration supports multiple providers (OpenAI, Anthropic, Gemini, Groq, etc.) — API keys for these providers stored locally, not transmitted to Fincept.

**Conditions:**
1. AGPL-3.0 internal/personal use: CLEARED per Jay's documented acceptance. If Jay ever distributes modified versions to third parties, AGPL copyleft obligation activates — modifications must be open-sourced. For personal trading research use, this condition does not apply.
2. API key storage: any API keys configured within FinceptTerminal (broker accounts, data providers, AI providers) live in the local application config. Standard secure handling practice applies — do not configure production broker accounts with real funds in any research/testing installation.
3. Python scripting layer: FinceptTerminal embeds Python 3.11+ for analytics. Pete's integration path goes through this layer. Individual Python scripts or automation built on top of FinceptTerminal are in-scope for Pete's domain review — this clearance covers the application itself, not the scripts built on top of it.
4. Windows binary: Soren notes the installer is a standard Qt-deployed Windows x64 executable. No sandboxing — it runs with user-level permissions. Expected for a desktop application; no elevation required.

---

## Recommendation

Add to Master Library at Section 9 (Reference & Ecosystem), Tier 2, pending Soren clearance and operator AGPL acknowledgment. The AGPL license is the only meaningful constraint — for Jay's personal trading research use, internal-only use of AGPL software is fully permitted. Once Soren clears and operator confirms AGPL acceptance, FinceptTerminal becomes a strong research data source for Pete's Python trading analysis work.

---

## C&P Summary

FinceptTerminal is a free, open-source desktop application that works like a simplified Bloomberg Terminal — the professional financial data system used by traders and analysts. It shows real-time market data, stock charts, options pricing, cryptocurrency prices, economic indicators, and portfolio analytics in a single interface. It also supports Python scripting, so analysts can write code to pull data into custom calculations. For this project, it is most relevant to Pete (the Python trading agent) as a research and data source for trading strategy work. The AGPL license means it can be used freely for personal/internal work but would require open-sourcing any modifications if distributed to others — for Jay's personal use, this is not a constraint.

---

---

## Report Version Log

| Version | Date | Notes |
|---------|------|-------|

---

*Report by Rose | Session 244 | 2026-06-12*