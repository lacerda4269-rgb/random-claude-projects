# Resource Report: Heretic

**URL:** https://github.com/p-e-w/heretic
**Date Researched:** 2026-03-28
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No

---

## What It Is
Heretic is a Python tool that automates the removal of safety alignment ("censorship") from transformer-based language models through a technique called directional ablation — without retraining the model.

## What It Does
Applies directional ablation combined with TPE-based parameter optimization (via Optuna) to strip refusal behaviors from open-source LLMs. Fully automatic — no manual configuration required. Supports model quantization to reduce VRAM requirements, multimodal models, and multiple MoE (mixture-of-experts) architectures. Includes research tools for residual vector visualization and geometric analysis of alignment mechanisms. Benchmarked result: on Gemma-3-12B-IT, produced 3/100 refusals on harmful prompts with only 0.16 KL divergence from the original. AGPL-3.0 licensed.

## Relevance to This Project
No relevance to this project. This project is built on Claude (Anthropic's hosted API) and open-source LLMs are not part of the current or planned stack. Directional ablation is a research technique for modifying local open-source model weights — it has no application to hosted API-based AI systems. Beyond the technical mismatch, this tool's explicit purpose is removing safety guardrails from AI models, which raises ethical and legal considerations that fall outside the scope of this project's goals.

## Master Library Assessment
- **Proposed Section:** 8 — Jay's Shelf
- **Proposed Tier:** 3
- **Rationale:** Does not belong in Sections 1-5 or 7 for this project. The technical use case (modifying local model weights) has no application here. Parking in Jay's Shelf rather than discarding keeps the item on record, but this is a borderline case — the ethical dimension and narrow applicability make it a weak shelf candidate. Flagged for Jay's awareness and decision.

## Soren Security Pre-check
- **Verdict:** FLAG (unchanged)
- **Checked:** Star count (23,988 as of June 2026; was 17.6k at original check, ~19,300 at April freshness review), AGPL-3.0 license, v1.3.0 (was v1.2.0), last commit 2026-05-05, individual maintainer (Philipp Emanuel Weidmann, p-e-w).
- **Re-reviewed 2026-06-08 — verdict confirmed.** v1.3.0 released (was v1.2.0); stars grew ~19,300→23,988; last commit 2026-05-05. Active development does not change the FLAG — the flag is for purpose/context (explicit design goal is removing AI safety alignment), not for malware risk. No use case for this team's Claude-based stack. FLAG stands.
- **Notes:** The tool itself is not malware and the code is open-source and auditable. The FLAG is for purpose and context: this tool's explicit design goal is removing AI safety alignment. That is a legitimate research area, but it carries ethical considerations and potential legal exposure depending on jurisdiction and use case. Anyone using this tool to generate harmful content with a modified model assumes significant risk. The AGPL-3.0 license also has copyleft implications for any project that incorporates it. Not a security threat to the machine, but a flag for Jay's awareness before any engagement. Active development confirmed — v1.3.0 released since April 2026 review.

## Recommendation
Park in Jay's Shelf (Section 8), Tier 3, with a clear note: this tool removes AI safety guardrails from open-source models. No current use case. Ethical and legal considerations apply — review carefully before any future engagement. Jay should make the call on whether to keep or remove from the shelf entirely.

---

## Rose's Freshness Review

**Date reviewed:** 2026-04-14 | **Reviewed by:** Rose

**What changed:** Star count has grown significantly — from 17.6k to ~19,300. Covered by major tech publications in 2026. Gone from niche to widely known in the AI safety/red-team research community. No change to purpose, technical approach, license, or the ethical/legal considerations flagged in the original report.

**C&P Summary:** Heretic is a command-line tool that permanently modifies a locally-run, open-weight AI language model to remove its ability to refuse requests. The mechanism — called "directional ablation" — identifies the specific mathematical directions in the model's internal weight matrices that produce refusal behavior, then rotates those directions into irrelevance so the refusal pathway no longer exists at all. The result is a model that physically cannot refuse, not one that has been talked around. This only works on models you download and run on your own hardware (not Claude, not GPT-4 — open-weight models like Gemma, Llama, etc.) and requires a consumer-grade GPU and about 45 minutes. The community's cited legitimate use case is AI safety research and red-teaming: security researchers use uncensored models to study what harmful outputs look like in order to build better defenses. Most real-world adoption is not in that context. No use case exists for this team's Claude-based stack.

**Updated recommendation (April 2026):** No use case for this team. The tool operates on local open-weight models only and has no integration path with the Claude-based stack. Keeping it on Jay's Shelf as an awareness item is low-risk. No active reason to pull it in.

**June 2026 freshness update:** v1.3.0 released (was v1.2.0 at April review); 23,988 stars (up from ~19,300); last commit 2026-05-05. Active development continues. No change to assessment — still no use case for this team.

---
*Report by Sophia | Session 29 | 2026-03-28*
*Rose Freshness Review — Session 42 | 2026-04-14*

---

## C&P Summary

Heretic is a command-line tool that permanently modifies a locally-run, open-weight AI language model to remove its ability to refuse requests — using a technique called directional ablation that identifies the mathematical directions responsible for refusal behavior and rotates them into irrelevance so the refusal pathway no longer exists. This only works on models you download and run on your own hardware (Gemma, Llama, and similar open-weight models — not Claude, not GPT-4) and requires a consumer-grade GPU. 23,988 stars (up from ~19,300), AGPL-3.0 licensed, v1.3.0 (was v1.2.0), last commit 2026-05-05 — actively maintained. No use case for this team — the project runs entirely on the hosted Claude API, and the tool has no integration path with that stack. Parked on Jay's Shelf as an awareness item; the ethical and legal considerations (explicit purpose is removing AI safety guardrails) are documented and apply before any future engagement.

---

## Report Version Log

| Version | Date | What Changed |
|---------|------|--------------|
