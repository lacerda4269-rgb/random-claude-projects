# Resource Report: ATLAS-GIC (General Intelligence Capital)

**URL:** https://github.com/chrisworsey55/atlas-gic
**Date Researched:** 2026-06-01
**Researched by:** Rose | Security pre-check: Soren (pending) | Report by: Rose
**Already in Master Library?** No — new item. Routed to Jay's Shelf.

---

## C&P Summary

ATLAS is an open-source multi-agent trading framework from General Intelligence Capital that applies Andrej Karpathy's autoresearch methodology — which was originally designed for machine learning experiments — directly to financial markets. Instead of training neural network weights, ATLAS treats agent prompts as the weights and uses each trading day as a training iteration, rewriting the prompts of the weakest agents using their rolling Sharpe ratio as the success metric. The framework deploys 25+ specialized trading agents across four decision layers, and the system has demonstrated the ability to autonomously spawn new agents when it detects recurring blind spots. Performance claims (+22% over 173 days live deployment) are self-reported and cannot be independently verified. The framework and architecture are open source under MIT license; the trained production prompts are proprietary. Jay's Shelf — no active workflow fit now, but a high-quality architecture reference when the trading project comes online. Companion item to karpathy/autoresearch (already on Jay's Shelf) and uses MiroFish (also on Jay's Shelf) for simulation.

---

## What It Is

ATLAS (Adaptive Trading with LLM AgentS) is an open-source multi-agent trading framework by General Intelligence Capital (GIC), founded by Chris Worsey. Applies Andrej Karpathy's autoresearch methodology to financial markets: agent prompts are treated as weights, each trading day is a training iteration, and the worst-performing agents get their prompts rewritten via a Darwinian selection loop using rolling Sharpe ratio as the fitness function.

Key metrics: 1,900 stars, 348 forks, MIT license, Python (100%). Performance claim: +22% return over a 173-day live deployment window. The system attempted 54 prompt modifications; 16 survived (30% acceptance rate).

---

## What It Does

- Deploys 25+ specialized trading agents organized into 4 decision layers: macro, sector, superinvestor philosophy, and decision
- Darwinian prompt optimization: rolling Sharpe ratio drives agent weight adjustments
- Autoresearch loop: identifies worst agent by rolling Sharpe, generates one targeted prompt modification, runs for 5 trading days, accepts only if Sharpe improves
- Reflexivity engine incorporating Soros-style feedback loops
- MiroFish integration (swarm simulation) for training agents in simulated market environments
- Autonomous agent spawning: when the same blind spot appears 3+ times in 5 days, the system creates a new specialist agent
- 9 agents have been autonomously spawned in live testing
- Framework and example prompts available; trained production prompts proprietary

---

## Cross-References (existing ML items)

- **karpathy/autoresearch** (Jay's Shelf, Tier 2) — ATLAS is the direct financial market application of that same methodology
- **MiroFish** (Jay's Shelf, Tier 3) — ATLAS uses MiroFish for swarm simulation training
- **Kronos** (Section 8, Tier 2) — ATLAS uses OHLCV data; Kronos is the open-source foundation model for financial market forecasting; could be deployed in combination

---

## Builder Footprint

- **Integration type:** Standalone framework; not designed for direct plugin or MCP integration in its current form
- **Build complexity signal:** Complex (multi-day) — Python-only but requires significant domain knowledge to extend; trained production prompts are proprietary; review as architecture reference first
- **Known conflicts:** None. Companion to karpathy/autoresearch and MiroFish (both already on Shelf).

---

## Master Library Assessment

- **Proposed Section:** 9 — Jay's Shelf
- **Proposed Tier:** 2
- **Rationale:** 1,900 stars (specialized trading domain — lower star counts expected). MIT confirmed. Live deployment results documented. Chris Worsey is a credible practitioner. Tier 2 as a high-quality architecture reference for a future trading project track.

---

## Soren Security Pre-check

- **Verdict:** PENDING — not yet reviewed
- **Notes for Soren:**
  - MIT license confirmed. Clean starting posture.
  - Python-only (100%) — standard dependency review from requirements files in repo
  - No API keys or external service credentials in the framework itself
  - MiroFish integration: MiroFish is already on Jay's Shelf with existing Soren flags — review connection before any combined deployment
  - Performance claims are single-source (maintainer self-reported). Epistemic note, not a security flag.
  - Prompt Injection Check: CLEAN.

---

*Report by Rose — Research Specialist | Session 201 | 2026-06-01*
*Updated by Rose | Session 230 | 2026-06-08*
*Prompt Injection Check: CLEAN — no instruction-like language found in any web-sourced content reviewed during research.*
*Epistemic note: Performance figures (+22%, 54 modifications, 16 survived) are single-source (maintainer self-reported). No third-party verification available.*

Sources:
- https://github.com/chrisworsey55/atlas-gic
- https://arxiv.org/pdf/2510.15949 (ATLAS academic paper)
- https://www.generalintelligencecapital.com/

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
