# [StrategyName / IndicatorName / ScriptName] — User Guide

**Version:** 0
**Type:** [Strategy / Indicator / Python Script]
**Platform:** [NinjaTrader 8 / TradingView / Python]
**Built by:** [Owner agent — the relevant specialist]
**Guide Last Updated:** [YYYY-MM-DD], Session [N]

**Paired document:** [[StrategyName / IndicatorName / ScriptName]-technical-manual.md]

---

*This is Jay's plain-language reference for this [strategy / indicator / script]. Not a technical document. Updated alongside the technical manual at every meaningful build milestone.*

---

## What This [Strategy / Indicator / Script] Does

[One to two sentences. What is it? What problem does it solve?]

**In trading terms:** [Describe what this is doing as a trader would think about it — not in code terms. What market behavior is it responding to? What edge or analysis does it provide? What does it help Jay do?]

---

## When It Triggers

> *For strategies and indicators. Omit for Python analysis scripts.*

**What it's watching for:** [Plain-language description of the market condition or calculation this is based on.]

**Entry signal (strategies):** [What causes the strategy to enter a long or short position? Describe in trading terms — what has to be true for the trade to fire?]

**Exit signal (strategies):** [What causes the strategy to close the position — beyond stops and targets? Any time-based exits, signal reversals, or conditions?]

**Signal appearance (indicators):** [What does the indicator show on the chart when a condition is met? A line crossing, a shape, a label, a color change?]

---

## How It Manages the Position

> *Strategies only — NinjaTrader 8 and TradingView. Omit for indicators and Python scripts.*

**Stop loss:** [How is the stop placed? Fixed distance, ATR-based, structure-based? Does it trail?]

**Take profit / target:** [How are profit targets set? Fixed, R-multiple, partial exits?]

**Position sizing:** [How is the position size determined? Fixed contracts/shares, percent of equity, other?]

**Re-entry behavior:** [After a trade closes, can it re-enter immediately? Are there filters or cool-down periods?]

---

## What You See on the Chart

> *Indicators only. Omit for strategies and Python scripts.*

**Plots:** [What does this indicator add to the chart? Lines, shapes, labels, background fills — describe each one.]

**Signals:** [What does a buy or sell signal look like visually? What does a neutral or no-signal state look like?]

**How to read it:** [Plain-language guide for Jay — what should he look at when he opens a chart with this indicator? What does it mean when he sees [specific visual]? What is actionable and what is just context?]

---

## How to Interpret Results

> *Python scripts and analysis only. Omit for NinjaTrader and TradingView builds.*

**What the output shows:** [What does this script produce — a report, a table, a JSON file, optimized parameter recommendations, a validation result?]

**How to read the results:** [Plain-language guide. What does a pass look like? What does a fail look like? What are the key numbers or fields to focus on? What does a discrepancy between Pete's output and the live results mean?]

**How to use the output:** [What does Jay do with these results? Does he send them to Nick or Todd? Does he make a decision based on the output? Walk through the next step in plain terms.]

---

## How to Configure It

**Parameters:**

| Parameter | What It Controls | Default | Notes for Jay |
|-----------|-----------------|---------|--------------|
| [Parameter Name] | [Plain-language: what does adjusting this do? What does a higher value mean vs. a lower value?] | [default] | [Guidance on how Jay should set this — recommended range, common configurations, what to watch out for] |

**First-time setup:**

- [ ] [Any platform steps Jay needs to take before using this for the first time — where to load it, what to apply it to, any settings to confirm in the platform]

---

## What to Expect Under Different Conditions

> *Fill in as testing and live use reveal behavior patterns. Leave as N/A until data exists.*

| Market Condition | What Happens | Notes |
|-----------------|-------------|-------|
| [Trending market] | [e.g., strategy stays in trade longer / indicator fires fewer signals] | |
| [Ranging / choppy market] | [e.g., more frequent small stops / indicator may whipsaw] | |
| [High volatility] | [e.g., stops may be hit on noise before the move completes] | |
| [Session open / close] | [e.g., strategy may fire differently at market open due to spread/gaps] | |
| [other condition] | | |

---

## Repainting Disclosure

> *TradingView builds only. Omit for NinjaTrader and Python builds.*

**Status:** [Tested — none found / Tested — found; see note below]

[If none found: "Repainting was tested on [YYYY-MM-DD], Session [N] using bar replay. None found."]

[If found: Plain-language explanation — what repaints, what it means for Jay, whether it affects real-time use vs. historical display, and what Jay and Sage decided about it. Do not use technical jargon. Make it concrete: "The [signal / line] may appear on a historical bar after the bar has closed. This means looking at the chart after the fact will show signals that were not available at the time the bar was live. This does not affect [real-time signal / bar close signal] behavior."]

---

## Known Limitations and Watch-outs

[Behaviors Jay should know about that aren't obvious from the parameter list. Things that affect real use: edge cases, market conditions where this underperforms, platform quirks that affect what Jay sees. Be specific — vague watch-outs are not useful.]

- [Limitation or watch-out 1]
- [Limitation or watch-out 2]

---

## Version History

| Version | Date | Session | What Changed |
|---------|------|---------|-------------|

---

*Template source: Blank Universal Templates folder — Initial Package Project. Rename this file to `[StrategyName / IndicatorName / ScriptName]-user-guide.md` when in use.*
