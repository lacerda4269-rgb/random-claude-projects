# Resource Report: OpenJarvis

**URL:** https://github.com/open-jarvis/OpenJarvis
**⚠️ URL Note:** Report originally listed URL as `https://github.com/openjarvis/openjarvis` — that path returns HTTP 404. Correct URL is `https://github.com/open-jarvis/OpenJarvis` (confirmed live, June 2026).
**Date Researched:** 2026-04-12
**Researched by:** Rose | Security pre-check: Soren | Filed by: Lexi
**Already in Master Library?** No — new item

---

## What It Is
OpenJarvis is a local-first personal AI agent framework developed at Stanford's Hazy Research lab and Scaling Intelligence Lab (Jon Saad-Falcon, Avanika Narayan, and others). 6,357 stars (up from 2,500+), Apache 2.0 licensed. Desktop release March 12, 2026. Built in Python, Rust, and TypeScript.

## What It Does
Framework for building personal AI agents that run locally on your device. CLI agents (`jarvis ask`, `jarvis digest`), preset configurations (morning briefings, research assistants, code companions), and skill installation from public repositories. Supports local inference engines (Ollama, vLLM) and cloud providers (Anthropic, OpenAI, Google) — operator picks the backend.

Core premise: local models already handle 88.7% of single-turn reasoning queries, but the software infrastructure to actually use them was missing. OpenJarvis fills that gap.

## Relevance to This Project
Jay flagged this as a concept for talking to Sage in a more personal, voice-like or direct-command way. The idea has merit — OpenJarvis with an Anthropic backend could serve as an interaction layer. That said, this is a concept for future exploration, not a current workflow need. The project already has Claude Code as the interaction model; OpenJarvis would only become relevant if Jay wants a dedicated local assistant interface separate from the IDE.

## Master Library Assessment
- **Proposed Section:** 9 — Jay's Shelf
- **Proposed Tier:** 3
- **Rationale:** Interesting concept with legitimate academic backing, but no current workflow fit. Jay's Shelf is the right home — keeps it on the radar without forcing a premature use case. Revisit when the question of personal interaction modes becomes concrete.

## Soren Security Pre-check
- **Verdict:** CLEARED (unchanged)
- **Checked:** License (Apache 2.0 — permissive, confirmed), authorship (Stanford Hazy Research + Scaling Intelligence Lab — academic, legitimate), star count (6,357 as of June 2026; was 2,500+), commit history (565+ commits, March 2026 release), tech stack (Python, Rust, TypeScript — standard), local inference support (Ollama, vLLM — both trusted, well-known), cloud provider integration (Anthropic, OpenAI, Google — API-key based, standard pattern)
- **Re-reviewed 2026-06-08 — verdict confirmed.** URL correction noted: the original report URL (`openjarvis/openjarvis`) returns 404; the correct URL is `open-jarvis/OpenJarvis`. Soren confirms this is the same project — same authorship (Stanford Hazy Research / Scaling Intelligence Lab, Jon Saad-Falcon, Avanika Narayan), same Apache 2.0 license, same tech stack, same 565+ commit history, same March 2026 desktop release. The 404 was a namespace capitalization difference, not a different entity. CLEARED verdict carries over to the corrected URL without reservation. Stars updated 2,500+→6,357.
- **Notes:** Clean clearance. Academic origin adds credibility. Local-first design means no unusual data routing — audio and queries stay on device unless cloud backend is selected. No change to security posture from freshness sweep.

## Recommendation
File to Section 9 — Jay's Shelf, Tier 3. No operator decisions required at intake. Revisit when there's a concrete use case for a personal assistant interface layer.

---
*Report by Rose + Sage | Session 39 | 2026-04-12*
*Freshness sweep: Rose | Session 229 | 2026-06-08 — correct URL confirmed as `open-jarvis/OpenJarvis` (original report URL `openjarvis/openjarvis` returns 404); stars updated (2,500+ → 6,357); Soren clearance unchanged.*

---

## C&P Summary

OpenJarvis is a local-first personal AI agent framework from Stanford's Hazy Research lab and Scaling Intelligence Lab — designed to fill the gap between capable local models and the software infrastructure needed to actually use them daily. Supports CLI agents, preset configurations (morning briefings, research assistants, code companions), skill installation, and both local inference engines (Ollama, vLLM) and cloud providers (Anthropic, OpenAI, Google). 6,357 stars (up from 2,500+), Apache 2.0 licensed, March 2026 desktop release. Relevant to this team as a potential personal interaction layer — the operator is interested in a more direct, voice-like way to talk to Sage. No current workflow fit; Jay's Shelf holds it until there's a concrete use case for a personal assistant interface separate from the IDE. **URL correction:** correct GitHub path is `open-jarvis/OpenJarvis`.

---

## Report Version Log

| Version | Date | What Changed |
|---------|------|--------------|
