# Resource Report: llmfit

**URL:** https://github.com/AlexsJones/llmfit
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No

---

## What It Is
llmfit is a terminal tool that matches open-source LLM models to your specific hardware capabilities — it tells you which models will actually run well on your machine before you try to install them.

## What It Does
Detects your system's RAM, CPU cores, and GPU specifications (including multi-GPU setups and Apple Silicon), then scores hundreds of models across quality, speed, fit, and context dimensions. Offers an interactive TUI with vim-like navigation, a classic CLI mode for scripting, a web dashboard at port 8787, and a REST API via `llmfit serve`. Includes a "Plan mode" to estimate what hardware you would need for a specific model configuration. Supports NVIDIA, AMD, Intel Arc, Apple Silicon, and Ascend NPUs. JSON output available for agent/script consumption. MIT licensed.

## Relevance to This Project
The operator note explicitly states: "Might not work with Anthropic but will work with OpenClaw (future project)." This is a future-project item, not a current-project item. The current project runs on Claude (Anthropic) — llmfit focuses on open-source models (Llama, Mistral, Qwen, Gemma, DeepSeek, etc.) and has no documented Anthropic support. This is correctly flagged as a future-project reference, specifically for the OpenClaw project where local/open-source model deployment will likely be a consideration.

## Master Library Assessment
- **Proposed Section:** 8 — Jay's Shelf
- **Proposed Tier:** 2
- **Rationale:** The operator has already scoped this to a future project (OpenClaw) and flagged the Anthropic incompatibility. It does not fit cleanly into Sections 1-5 or 7 for the current project. Jay's Shelf is the right parking spot — it keeps the item visible and contextualized without forcing it into an active section. Tier 2 because when the OpenClaw project begins, this becomes immediately relevant.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** Star count (27,586 as of 2026-06-08; was 19.6k at research — strong and continued growth), MIT license, actively developed, no suspicious patterns in README, individual maintainer (AlexsJones) with public GitHub history.
- **Notes:** Individual maintainer rather than organizational backing — not a concern at this star count and activity level. MIT license is clean. No red flags. Latest release: v0.9.30 (June 1, 2026).
- **Re-reviewed 2026-06-08 — verdict confirmed. CLEARED stands.** Rose's freshness sweep: stars 27,586 (was 19.6k — major growth), v0.9.30 (June 1, 2026), last push 2026-06-08 — very actively maintained. No security disclosures. Strong growth trajectory strengthens the original clearance. No action required.

## Recommendation
Park in Jay's Shelf (Section 8), Tier 2, with the note: "Flagged for OpenClaw project — hardware matching for local LLM deployment. Not compatible with Anthropic/Claude. Revisit when OpenClaw begins."

---
*Report by Sophia | Session 29 | 2026-03-28*

---

## C&P Summary

llmfit is a terminal tool that tells you which open-source LLM models will actually run well on your specific hardware before you commit to installing them. It detects your RAM, CPU, and GPU specs and scores hundreds of models across quality, speed, fit, and context dimensions. This tool has no compatibility with Anthropic/Claude and is explicitly scoped to a future project (OpenClaw) where local open-source model deployment will be relevant. Parked in Jay's Shelf for that reason — Tier 2 to ensure it surfaces when OpenClaw begins. Stars: 27,586 (was 19.6k at research — strong growth); latest release: v0.9.30 (June 2026).

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
