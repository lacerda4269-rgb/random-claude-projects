# Resource Report: RYS (dnhkng blog post + GitHub repo)

**URL:** https://dnhkng.github.io/posts/rys/
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No

---

## What It Is
RYS is a novel LLM optimization technique — and associated blog post — by researcher "dnhkng" that improves model intelligence by duplicating existing layers without changing any weights.

## What It Does
The core idea: take a decoder-based language model and traverse a subset of its layers twice in the forward pass, without modifying any weights. The result is a meaningful performance boost with zero additional training cost. The companion GitHub repo (`github.com/dnhkng/RYS`, 77 stars as of 2026-06-08) provides reproducibility tools: parameter sweep scripts, benchmarking on Math and Equivalence tasks, multi-block beam search optimization, XGBoost surrogate modeling for candidate ranking, and Hugging Face export utilities. The RYS-XLarge model built with this technique achieved benchmark improvements of +2.61% IFEval, +8.16% MATH Lvl 5, and +17.72% MMLU-PRO, placing it among the top models on relevant leaderboards at time of research. A paper is reportedly in preparation.

**Note:** The blog post URL (`dnhkng.github.io/posts/rys/`) was inaccessible via direct fetch during this research session. This report draws on the companion GitHub repo and web search results. Substance appears consistent.

## Relevance to This Project
Peripheral. This project is not building or fine-tuning LLMs — it is building an agent orchestration framework on top of existing models. RYS is a model-level technique, not an agent-level or tooling-level resource. It is worth awareness — particularly if Jay ever evaluates which base models to use for specific agent roles (a faster, smarter base model is always relevant) — but it does not affect any current build decision.

## Master Library Assessment
- **Proposed Section:** 5 — Reference & Ecosystem
- **Proposed Tier:** 3
- **Rationale:** This is research-layer material — a technique and a blog post, not an installable tool or pattern. Section 5 is the right home for "read and learn from" items. Tier 3 because it has no near-term operational impact on this project.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** GitHub repo (`dnhkng/RYS`) — 77 stars (updated 2026-06-08), single contributor, Python-only, no install scripts or credential requests, pure research/reproducibility code; no releases published; blog post inaccessible for direct review but consistent with academic research posting pattern
- **Notes:** No executable installs, no network calls, no credential handling. Pure research content. No concerns.

## Recommendation
Enter the library in Section 5 at Tier 3. Reference-only — no install, no action required. Revisit if model selection becomes a design decision in a future phase.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---
*Report by Sophia | Session 29 | 2026-03-28*
*Updated by Rose | Session 230 | 2026-06-08*

---

## C&P Summary

RYS is a model-level optimization technique that improves LLM intelligence by routing the forward pass through a subset of existing layers twice — without changing any weights and without retraining. The companion GitHub repo provides benchmarking and reproducibility tools; the technique produced +8.16% on MATH Level 5 and +17.72% on MMLU-PRO on Gemma. No relevance to this project's current build phases — this team builds on hosted Claude API, not local model weights. Worth awareness for the future if base model selection ever becomes a design decision; parked at Tier 3 as research-layer reference material.
