# Resource Report: NotebookLM Skill (PleasePrompto)

**URL:** https://github.com/PleasePrompto/notebooklm-skill
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No

---

## What It Is
A Claude Code Skill that enables direct integration between Claude Code and Google NotebookLM — allowing agents to automate queries to NotebookLM notebooks and retrieve citation-backed answers sourced exclusively from uploaded documents.

## What It Does
Uses Patchright (Chrome automation) to interact with NotebookLM via browser. Supports persistent Google authentication (one-time login, reusable across sessions). Provides smart library management for saving and organizing notebooks with metadata. Returns source-grounded responses only — answers come from uploaded documents, not general LLM knowledge, making this a hallucination-reduction tool for document-specific research. Self-contained with an isolated Python environment and no global dependencies. 6,940 stars, 787 forks. Local Claude Code only — does not work in web UI due to sandbox restrictions.

**⚠️ MAINTENANCE NOTE:** Last pushed 2025-11-21 — repository has not been updated in 7+ months as of June 2026. Given the dependency on Patchright browser automation and Google NotebookLM (which frequently updates its interface), the Patchright automation approach may be broken or degraded. Verify functionality before deployment.

**Key limitation:** Each query opens a fresh browser session (stateless). Notebooks must be publicly shared to work.

## Relevance to This Project
Medium relevance — distinct from notebooklm-py (different approach, different creator). Where notebooklm-py is a Python API wrapper for generating NotebookLM content, this skill is specifically for querying existing notebooks and getting citation-backed answers. For this project, it is most relevant as a research verification tool: load a set of documents into a NotebookLM notebook, then use this skill to query across them with guaranteed source grounding. The browser automation approach is less fragile than undocumented API calls in some ways, but introduces its own dependencies (Patchright, Chrome, public notebook requirement).

## Master Library Assessment
- **Proposed Section:** 2 — Skills
- **Proposed Tier:** 2
- **Rationale:** This is a directly installable Claude Code skill (not a reference or ecosystem item) — Section 2 is the right home. Tier 2 is appropriate: high value for document-grounded research workflows, but phase-dependent on when the team builds out NotebookLM integration.

## Soren Security Pre-check
- **Verdict:** FLAG (operational caveat, not malice)
- **Checked:** Star count (5.2k), fork count (542), primary language (Python 3.8+), implementation method (browser automation via Patchright), authentication model (persistent Google login), public notebook requirement, isolation model (self-contained virtual environment)
- **Notes:** The FLAG is for the browser automation approach and the public notebook requirement. Patchright is described as using "human-like interaction (realistic typing speeds and delays to avoid detection)" — this language warrants attention. Automating Google services in ways designed to evade detection carries terms-of-service risk. The repo itself appears legitimate (5.2k stars, clean structure, MIT-style license implied), but the automation model creates ToS exposure with Google. Recommend documenting this risk clearly in the ML entry. Not a malicious repo — a FLAG for operational/legal caution.
- **Re-reviewed 2026-06-08 — HOLD verdict confirmed. Staleness reinforces the HOLD.** Rose's v1.0 sweep (2026-06-08) confirms: repo last pushed 2025-11-21 — 7+ months without an update as of this review. The original FLAG conditions are unchanged (browser automation ToS risk, public notebook requirement). The staleness materially worsens the risk profile: the Patchright automation approach depends on Google NotebookLM's interface, which updates frequently. A 7-month inactive repo against a frequently-changing target is operationally suspect — the automation is likely degraded or broken. Stars have grown to 6,940 (from 5.2k) but star count is a lagging indicator and does not speak to current functionality. The Rose freshness review (Session 42) HOLD recommendation stands and is strengthened: use NotebookLM directly in a browser on a Google Workspace account rather than through this skill. This resource is not cleared for deployment in its current state. If the operator ever wants to revisit, a fresh functionality test against a current NotebookLM interface is required before any clearance consideration.

## Recommendation
Enter library at Section 2 (Skills), Tier 2 with a clear note in the ML entry flagging: (1) public notebook requirement as an operational constraint, and (2) browser automation ToS risk with Google. This is a distinct resource from notebooklm-py and warrants its own ML entry. Useful when the team needs document-grounded, citation-backed research automation.

---

## Rose's Freshness Review

**Date reviewed:** 2026-04-14 | **Reviewed by:** Rose

**What changed:** The ToS flag from the original report remains valid. The broader context has evolved: the operator is now explicitly interested in using this (or something better) as part of a notes/memory/code stack. The NotebookLM + Obsidian pairing has become a well-established community workflow in 2026 with substantial documentation. A key mitigation for the ToS risk has been identified (see C&P below). Decision is HOLD pending operator direction.

**C&P Summary — NotebookLM + Obsidian META Stack:** The operator wants a stack for notes, memory, and code management across sessions. The current recommendation is NotebookLM paired with Obsidian. Obsidian stores all your notes as plain markdown files on your own machine — no vendor lock-in, no subscription required for the core app, fully portable and private. NotebookLM (this tool) lets you upload exported Obsidian notes and ask questions across them — it summarizes, cross-references, and cites which source it's drawing from so you can verify. Together: Obsidian is the permanent archive you own and build over time; NotebookLM is the active research assistant you query when you need to pull insight out of that archive. The ToS risk (browser automation designed to avoid Google detection) is specific to this skill — it does not apply to using NotebookLM directly through your browser. **Key mitigation for direct NotebookLM use:** switching from a personal Google account to a Google Workspace account eliminates the data-training risk — Workspace terms explicitly exclude uploaded data from model training. Alternatives reviewed: Obsidian + local LLM (Ollama) for zero cloud exposure; Notion AI for a simpler all-in-one; Mem and Tana as AI-native notes apps. NotebookLM + Obsidian remains the recommended pairing for 2026.

**Updated recommendation:** HOLD. The notebooklm-skill specifically carries ToS risk from its browser automation approach. The operator's actual goal (notes/memory/code stack) is best served by using NotebookLM directly in a browser (not through this skill) paired with Obsidian, on a Google Workspace account. Whether this skill is still needed once that setup is in place is the open question. Decision deferred to operator after Obsidian + NotebookLM setup is evaluated.

---
*Report by Sophia | Session 29 | 2026-03-28*
*Rose Freshness Review — Session 42 | 2026-04-14*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---

## C&P Summary

This is a Claude Code skill that automates queries to Google NotebookLM notebooks via browser automation, returning citation-backed answers sourced exclusively from the uploaded documents — making it a hallucination-reduction tool for document-specific research. It pairs with Obsidian in the recommended notes/memory/code stack: Obsidian is the permanent private archive you build and own, NotebookLM is the active research layer you query across it. The skill itself carries a ToS flag from its browser automation approach (designed to avoid Google detection), so the current recommendation is HOLD — use NotebookLM directly in a browser (not through this skill) on a Google Workspace account, which eliminates the data-training risk. Whether this skill remains necessary once that setup is in place is the open question for the operator.
