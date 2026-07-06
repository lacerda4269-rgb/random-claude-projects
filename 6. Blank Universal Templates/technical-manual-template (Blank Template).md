# [StrategyName / IndicatorName] — Technical Manual

**Version:** 0
**Platform:** [NinjaTrader 8 / TradingView]
**Script Type:** [Strategy / Indicator]
**Owner:** [Owner agent — the relevant platform specialist]
**Build Date:** [YYYY-MM-DD]
**Session:** [Session Number]
**Status:** [In Progress / Complete]

**Paired document:** [[StrategyName / IndicatorName]-user-guide.md]

---

*This is a living technical record — not SOP format. Fill each section as the build reaches that milestone. Do not defer to the end.*

---

## 1. Identity

| Field | Value |
|-------|-------|
| Name | [StrategyName / IndicatorName] |
| Version | [e.g., 1.0] |
| Platform | [NinjaTrader 8 / TradingView] |
| Script Type | [Strategy / Indicator] |
| Owner | [Owner agent — the relevant platform specialist] |
| Build Date | [YYYY-MM-DD] |
| Session | [Session Number] |

---

## 2. Approved Shell

**Parameters declared in the Shell:**

| Parameter Name | Type | Default Value | Description |
|---------------|------|---------------|-------------|
| [param] | [type] | [default] | [plain-language description] |

**Script type declaration (TradingView only):** [strategy() / indicator()] — locked at Shell stage; never changes after approval.

**NT8 build number (NinjaTrader only):** [NT8 build at time of Shell approval]

**Shell structure:** [Brief description of the logical families declared in the Shell — entry region, exit region, stop/target region, plot/signal region, etc.]

**Shell approval:** Jay approved [YYYY-MM-DD], Session [N].

---

## 3. Platform Declarations (Strategies Only)

> *Complete one section below — whichever matches this build's platform. Omit the other. Omit this entire section for indicators.*

### NinjaTrader 8 — Order Approach Declaration

*(NinjaTrader strategies only.)*

**Order approach:** [Managed / Unmanaged]

- **Managed:** Order handling via `EnterLong`, `ExitLong`, `SetStopLoss`, etc. (NinjaTrader's built-in management).
- **Unmanaged:** Direct submission via `SubmitOrderUnmanaged`. Full control; full responsibility.

**Decision date:** [YYYY-MM-DD], Session [N]
**Rationale:** [Brief note on why this approach was selected for this strategy]

Locked for the life of this strategy. Switching approaches requires a full rebuild (v1 → v2), new Shell, new Jay approval. Flag this explicitly when the question arises.

---

### TradingView — Strategy Settings Declaration

*(TradingView strategies only.)*

| Setting | Value | Note |
|---------|-------|------|
| `initial_capital` | [value] | Starting equity for the simulation |
| `default_qty_type` | [value] | How position size is calculated |
| `commission_value` | [value] | Commission applied per trade |
| `pyramiding` | [value] | Multiple entries in same direction allowed? |
| `calc_on_every_tick` | [value] | Recalculate on every tick or bar close only |
| `calc_on_order_fills` | [value] | Recalculate after each order fill within a bar |

**Decision date:** [YYYY-MM-DD], Session [N]
**Pine Script version:** [v6 / version at time of declaration]

Locked for the life of this strategy. Any scope change that would require revising these settings surfaces to Sage before proceeding.

---

## 4. Build Log

| Date | Session | Milestone | What Was Done | Notes |
|------|---------|-----------|--------------|-------|
| [YYYY-MM-DD] | [N] | Shell approved | | |
| [YYYY-MM-DD] | [N] | [Logic family] complete | | |
| [YYYY-MM-DD] | [N] | Full build complete | | |

Update after each meaningful milestone — Shell approval, each major logic family, full build complete.

---

## 5. Repainting Assessment (TradingView Only)

> *TradingView builds only. Omit for NinjaTrader builds.*

**Current status:** [Not yet assessed / Tested — none found / Tested — found and disclosed]

| Date | Session | Pine Script Version | Assessment | Details |
|------|---------|---------------------|-----------|---------|
| [YYYY-MM-DD] | [N] | [v6] | [Tested — none found / Found — see details] | [If found: where and why. If clean: "Repainting tested via bar replay — none found."] |

If repainting is found: documented here and disclosed in the user guide. Sage and Jay decide whether to fix or document-and-accept. The disclosure belongs to Todd; the decision belongs to Jay.

---

## 6. Test Log

| Date | Session | What Was Tested | Platform Version | Result | Notes |
|------|---------|----------------|-----------------|--------|-------|
| [YYYY-MM-DD] | [N] | [Description of test scope] | NT8 Build [N] *or* Pine Script v[N] | [Pass / Fail / Partial] | [Edge cases reviewed; failures noted] |

**Testing standard — NinjaTrader:** Sim mode. Primary use cases confirmed; edge cases reviewed: partial fills, cancellations, session boundaries, state transitions.

**Testing standard — TradingView:** Strategy Tester report reviewed: net profit, drawdown, trade count, average win/loss. Repainting tested as a dedicated step via bar replay (strategies). Visual output confirmed for indicators.

Done means tested — not built. Undocumented fixes are not fixes.

---

## 7. Ownership History

**Current owner:** [Owner agent — the relevant platform specialist]

| Version | Date | Session | Owner | Transfer Reason |
|---------|------|---------|-------|----------------|
| 1.0 | [YYYY-MM-DD] | [N] | [Owner agent — the relevant platform specialist] | Original build |
| [x.y] | [date] | [N] | [Agent] | [Full version increment + different agent, or Jay direction] |

Ownership transfers only on full version increment (v1 → v2) with a different agent doing the rebuild, or on Jay's explicit direction. Minor bumps (v1.0 → v1.1) do not transfer ownership regardless of who made the change. Every transfer recorded here: date, session, reason.

---

## 8. Version History

| Version | Date | Session | What Changed | Why |
|---------|------|---------|-------------|-----|

---

*Template source: Blank Universal Templates folder — Initial Package Project. Rename this file to `[StrategyName / IndicatorName]-technical-manual.md` when in use.*
