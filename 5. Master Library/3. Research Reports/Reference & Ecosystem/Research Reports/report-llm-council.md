# Resource Report: LLM Council — Multi-Model Collaborative Answering

**URL:** https://github.com/karpathy/llm-council
**Date Researched:** 2026-04-18
**Researched by:** Rose | Security pre-check: Soren (pending) | Report by: Rose
**Already in Master Library?** No — Rose Research Round 2 (Session 60)

---

## What It Is
A local web application by Andrej Karpathy that routes a single user question to multiple LLMs simultaneously, has each model evaluate the others responses, and synthesizes a final answer via a designated Chairman model.

## What It Does
- Three-stage pipeline: (1) each LLM independently answers the query in parallel, (2) each model reviews and ranks the other responses with anonymized identities to prevent bias, (3) a designated Chairman LLM synthesizes a final comprehensive answer
- Side-by-side response comparison across all participating models in tabbed UI
- Customizable council composition — choose which models participate and which serves as Chairman
- Built on OpenRouter API — accesses any model available through that service
- Local web app: FastAPI backend, React + Vite frontend
- Conversations stored as JSON files locally
- Creator explicitly states: weekend project, vibe-coded, no support provided
- **Stars:** 20,400 | **Forks:** 3,800 | **Language:** Python | **License:** None declared
- **Created:** 2025-11-22 | **Last pushed:** 2025-11-22 | **Maintainer:** Andrej Karpathy
- **Updated:** 2026-06-08

## Relevance to This Project
Conceptually relevant rather than operationally relevant. The council pattern — multiple agents independently answer, evaluate each other, then synthesize — is a pattern we should understand because it is a serious approach to reducing individual model errors. Karpathy is one of the most credible names in AI (former OpenAI research director, former Tesla AI director). The fact that his personal side project has 17k stars and this architecture signals that multi-model consensus is worth tracking. It is not something we would deploy in our current stack (our team runs on Claude; OpenRouter multi-model is a different architecture), but the design pattern is reference-worthy.

## Master Library Assessment
- **Proposed Section:** 7 — Reference & Ecosystem
- **Proposed Tier:** 3
- **Rationale:** This is a reference and architectural pattern item, not an install or deploy candidate. Section 7 is the right home. Tier 3 because it is not phase-dependent and not urgent — it is the kind of thing worth knowing about and potentially revisiting when the team architecture conversation matures.

## Soren Security Pre-check
- **Verdict:** FLAG
- **Date reviewed:** 2026-04-18
- **Checked:** License status, author provenance, deployment surface, credential model, network exposure, maintainability status.
- **Notes:** Andrej Karpathy is one of the most credible individuals in the AI field — former OpenAI research director, former Tesla AI director, current AI educator. Author provenance is as strong as it gets. 17,249 stars and 3,411 forks confirm the project is widely known and studied.
  The FLAG is on two items. First: no license declared. All-rights-reserved by default. The same rule applies here as with other unlicensed repos — any code adaptation requires either a license being added or independent reimplementation. For reference and study, no action needed. For code reuse, the license gap is a blocker.
  Second: deployment status. Karpathy explicitly described this as a weekend project built through vibe coding with no support provided. It has not been updated since November 22, 2025 (the creation date — confirmed unchanged as of 2026-06-08 check). If this were ever considered for deployment, it would carry the risk of an unmaintained codebase — no bug fixes, no security patches, no dependency updates. The OpenRouter API dependency means API credentials for multiple LLM providers would be required, and the credential handling in an unsupported project would need review before any deployment.
  Neither flag is relevant to the current use case, which is reference only. Filing in Section 7 as a Tier 3 architectural reference is appropriate and unaffected by these flags. They become relevant only if deployment is ever considered, which the report explicitly excludes.
  FLAG conditions: (1) No code adaptation without license resolution. (2) Any future deployment consideration requires unsupported-codebase risk assessment and credential handling review before proceeding.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Stars 17,249 → 20,400; forks 3,411 → 3,800. Last pushed date confirmed still 2025-11-22 — repo remains unmaintained since creation. No license added. Both FLAG conditions still apply. FLAG stands.

## Recommendation
File in Section 7 (Reference & Ecosystem) as a Tier 3 item. Worth knowing about as an architectural pattern; not worth building toward in the current phase.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---
*Report by Rose | Session 60 | 2026-04-18*
*Updated by Rose | Session 230 | 2026-06-08*

---

## C&P Summary
LLM Council is a project by Andrej Karpathy — one of the most respected AI researchers in the field — that lets you ask a question to multiple AI models at once instead of just one. Each model answers independently, then each model reads and rates the other answers without knowing who wrote them, and finally one designated model reads everything and writes a single best answer. The idea is that the weakest individual model responses get filtered out by the others, and the final synthesis is more reliable than any single answer. It is built as a local web app, runs on OpenRouter (a service that provides access to many different AI models through one API), and was described by Karpathy himself as a weekend project built primarily through vibe coding. For this project, it is reference material rather than something to install — we run on Claude, not a multi-model architecture. But the consensus pattern it demonstrates is worth understanding as the team scales.

