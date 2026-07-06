# [ScriptName] — Technical Manual

**Version:** 0
**Script Type:** [Backtesting / Optimization / Automation / Analysis / Cross-LLM]
**Owner:** [Owner agent — the Python specialist]
**Build Date:** [YYYY-MM-DD]
**Session:** [Session Number]
**Status:** [In Progress / Complete]

**Paired document:** [[ScriptName]-user-guide.md]

---

*This is a living technical record — not SOP format. Fill each section as the build reaches that milestone. Do not defer to the end.*

---

## 1. Identity

| Field | Value |
|-------|-------|
| Script Name | [ScriptName] |
| Version | [e.g., 1.0] |
| Script Type | [Backtesting / Optimization / Automation / Analysis / Cross-LLM] |
| Owner | [Owner agent — the Python specialist] |
| Build Date | [YYYY-MM-DD] |
| Session | [Session Number] |
| Validation Target | [Nick — NinjaTrader 8 / Todd — TradingView / N/A] |
| Python Version | [e.g., 3.11.x] |

---

## 2. Design Decisions and Approach

**What this script does:**

[One to two sentences. What problem does it solve? What is it doing in Python terms?]

**In trading terms:**

[Plain-language description of what this script is doing in the context of the trading system — what strategy is being tested, what is being optimized, what the automation handles, or what analysis is being run.]

**Scope:**

[What this script covers and what it explicitly does not cover. Be specific — what is in Pete's lane here, and what belongs elsewhere.]

**Systems map:**

[Brief description of what pieces of the stack this script touches — which agents' outputs it reads, which outputs it produces, which files or data structures it interacts with.]

**Approach rationale:**

[Why this approach was chosen over alternatives. Key design decisions made before or during build — documented here so future Pete (or any agent taking ownership) understands the reasoning, not just the implementation.]

---

## 3. Dependencies and Version Pins

All external packages are pinned. No unversioned installs.

| Package | Version Pin | Purpose | PyPI Supply Chain Check |
|---------|-------------|---------|------------------------|
| [package] | [==X.Y.Z] | [plain-language purpose] | [Checked YYYY-MM-DD / Not required — low risk] |

**Python version:** [e.g., 3.11.x]

**Supply chain check note:** Any package handling credentials or with elevated system access requires a release history check before install (Soren Advisory I — PyPI supply chain protocol). Document the check date in the table above. Flag to Sage if an anomaly is found before installing.

---

## 4. Handoff Spec

> *Required for any deliverable that feeds another agent. Fill in at brief stage — before building. Omit for standalone analysis tasks with no cross-agent output.*

| Field | Value |
|-------|-------|
| Input source | [Nick's backtest data / Todd's TradingView Strategy Tester data / Other] |
| Output format | [JSON / CSV / Other — describe structure] |
| Validation target | [Nick — NinjaTrader 8 / Todd — TradingView / N/A] |
| Pass/fail result structure | [How results are flagged pass or fail in the output] |

**Additional project-specific fields:** [per activation brief — list any fields beyond the minimum floor]

**Minimum floor confirmed:** input source ✓ / output format ✓ / validation target ✓ / pass/fail result ✓

---

## 5. Data Validation Gate Log

> *Required for backtesting and optimization tasks. Omit for automation or standalone analysis tasks with no cross-agent validation target.*

**Validation type:** [OBC (Order Bar Count) / OET (Order Entry Time) / OPC (Order Close/PnL) / Multiple]

| Date | Session | Test Scope | Nick / Todd Live Result | Pete Python Result | Outcome | Notes |
|------|---------|-----------|------------------------|-------------------|---------|-------|
| [YYYY-MM-DD] | [N] | [OBC / OET / OPC — describe what was compared] | [live backtest result from Nick or Todd] | [Pete's Python output] | [Match / Discrepancy — flagged to Sage] | [If discrepancy: magnitude documented; Jay decides tolerance] |

**Gate rules:**
- **OBC:** Exact match expected. Any discrepancy → flag to Sage; Jay decides.
- **OET / OPC:** Document the discrepancy and its magnitude → flag to Sage; Jay decides whether to proceed or disregard.
- Pete does not make the tolerance call. Gate is not cleared until Sage or Jay confirms.

---

## 6. Test Log

| Date | Session | What Was Tested | Python Version | Result | Notes |
|------|---------|----------------|----------------|--------|-------|
| [YYYY-MM-DD] | [N] | [Description of what was tested and why] | [3.x.x] | [Pass / Fail / Partial] | [Edge cases reviewed; failures noted] |

Done means tested — not built. Undocumented fixes are not fixes. If a fix was made after a failed test: document the fix and the re-test result before reporting completion.

---

## 7. Build Log

| Date | Session | Milestone | What Was Done | Notes |
|------|---------|-----------|--------------|-------|
| [YYYY-MM-DD] | [N] | Systems analysis complete | | |
| [YYYY-MM-DD] | [N] | [Module / family] complete | | |
| [YYYY-MM-DD] | [N] | Full build complete | | |

---

## 8. Ownership History

**Current owner:** [Owner agent — the Python specialist]

| Version | Date | Session | Owner | Transfer Reason |
|---------|------|---------|-------|----------------|
| 1.0 | [YYYY-MM-DD] | [N] | [Owner agent — the Python specialist] | Original build |
| [x.y] | [date] | [N] | [Agent] | [Full version increment + different agent, or Jay direction] |

Ownership transfers only on full version increment (v1 → v2) with a different agent doing the rebuild, or on Jay's explicit direction. Minor bumps do not transfer ownership regardless of who made the change. Every transfer recorded here: date, session, reason.

---

## 9. Version History

| Version | Date | Session | What Changed | Why |
|---------|------|---------|-------------|-----|

---

*Template source: Blank Universal Templates folder — Initial Package Project. Rename this file to `[ScriptName]-technical-manual.md` when in use.*
