# Resource Report: LibreChat

**URL:** https://github.com/danny-avila/LibreChat
**Date Researched:** 2026-06-12
**Researched by:** Rose | Security pre-check: Soren | Report by: Rose
**Already in Master Library?** No — new research, Session 244

---

## What It Is

LibreChat is an open-source, self-hostable web application that provides a unified chat interface for interacting with virtually any AI model. It is a feature-rich clone and extension of ChatGPT, designed to be deployed as a personal or team AI hub. Users get a single web UI to access Claude (Anthropic), GPT-5/o1 (OpenAI), Gemini (Google), DeepSeek, Mistral, Groq, Ollama local models, and dozens more — all in one place, with full conversation history, search, presets, and multi-user authentication. It ships with built-in MCP support, agent orchestration, a code interpreter, DALL-E image generation, OpenAPI action execution, and RAG (retrieval-augmented generation). It is actively maintained with 38,955 stars and a v0.8.6 release in June 2026.

---

## What It Does

- Provides a unified web chat interface for Claude, GPT, Gemini, DeepSeek, Mistral, Groq, Ollama, and many more models
- Supports real-time AI model switching within the same conversation
- Ships built-in MCP (Model Context Protocol) support — connect MCP servers to agents running inside LibreChat
- Provides multi-model agent orchestration with tool use, function calling, and agent memory
- Includes a built-in code interpreter for executing code in conversations
- Supports DALL-E 3 and other image generation models
- Provides OpenAPI Actions — connect any API to an agent via OpenAPI spec
- Supports RAG (retrieval-augmented generation) for document context injection
- Provides secure multi-user authentication with role-based access
- Supports conversation branching, search, presets, and message editing
- Deployable via Docker Compose (MongoDB + Meilisearch + RAG API + core app)
- Provides an Artifacts feature for rendering code output visually in-chat
- Supports AWS Bedrock, Azure OpenAI, Vertex AI, and OpenRouter as model endpoints

---

## Relevance to This Project *(as of research date — context may not carry to future projects)*

Jay's question was: "What can it do overall?" — a broad capability survey. The short answer: LibreChat is a self-hosted AI hub that unifies every major model and agent capability behind a single web interface.

For MIP, there are two concrete angles worth considering. First, it is a comparison reference: MIP uses Claude Code CLI as the primary development environment, and LibreChat is not a replacement for that. LibreChat is a chat interface, not a coding agent. The overlap is minimal.

Second, LibreChat has a potential role as a team collaboration surface. If Jay ever wants a way to run conversations with multiple models side-by-side, share AI conversations with collaborators, or give others on the team (future hires, contractors) a managed AI interface without giving them Claude Code CLI access, LibreChat is exactly that. Its MCP support means it can connect to the same MCP servers already in the MIP stack, so a self-hosted LibreChat instance could be a shared team surface for model access and agent interaction while Claude Code CLI remains Jay's power-user development environment.

The 38,955 star count, MIT license, active v0.8.x release cadence, and the explicit Anthropic/Claude support make this a legitimate and well-maintained option. Jay's Shelf is the right temporary home while no specific use case is active.

---

## Master Library Assessment

- **Proposed Section:** Section 11 — Jay's Shelf
- **Proposed Tier:** 2
- **Rationale:** LibreChat is a high-quality, well-maintained tool with genuine potential as a team collaboration surface or personal multi-model AI hub. It does not fit CLI, MCP, Workflow Patterns, or Alternative Tools neatly — it is a standalone application with broad capability. Shelf placement with Tier 2 reflects its quality and future potential without committing to a specific deployment path until a concrete use case is identified.

---

## Soren Security Pre-check

**CLI Intake Checklist Results:**

- **Version evaluated:** v0.8.6 (latest release, 2026-06-01) | Latest available: v0.8.6 | Delta: none — evaluated version is latest
- **License:** MIT | Flag: none — permissive, commercial use permitted
- **CVE check:** 0 vulnerabilities found at version level | Sources checked: osv.dev (package: librechat, ecosystem: npm, version: 0.8.6)
- **Alternatives evaluated:** OpenWebUI (open-source, similar multi-model hub, Ollama-focused), AnythingLLM (self-hosted, simpler feature set, no MCP support), Jan (desktop app, offline-first, narrower) | Preferred because: LibreChat has the broadest model support, the most active development, explicit MCP integration, and the largest community (38,955 stars vs. competitors' 10K-20K range)
- **Summary rating:** Flagged | Flags: (1) MongoDB + Meilisearch dependencies — additional services to maintain if self-hosted; (2) Docker deployment required for production — not a simple CLI install; (3) 502 open issues — large application with active bug tracking; (4) self-hosted means operator is responsible for all security patching; Soren should review the authentication configuration and any credential handling before deployment

**Verdict:** PENDING
**Checked:** Stars (38,955), license (MIT confirmed), OSV.dev CVE sweep (clean at v0.8.6), release history, Docker Compose stack review, Anthropic/MCP support confirmed
**Notes:** PENDING Soren full review. No HOLD criteria — MIT license clean, CVE sweep clean, well-established project. Soren should focus review on: authentication configuration, credential storage (API keys for all the connected models), multi-user access control, and MongoDB data persistence security. Self-hosted application — operator owns the security posture.

---

## Recommendation

Add to Master Library at Section 11 (Jay's Shelf), Tier 2, pending Soren clearance. LibreChat is too good to leave untracked — 38,955 stars, MIT license, built-in MCP support, and an explicit Claude/Anthropic integration make it a strong future candidate for a team collaboration surface. No active deployment path right now, but this should be the first tool Sage pulls when Jay needs a multi-model web interface or a shared team AI hub.

---

## C&P Summary

LibreChat is a free, open-source web application you install on your own server that gives you a ChatGPT-style interface for virtually every major AI model — Claude, ChatGPT, Gemini, DeepSeek, and dozens more — all in one place. It supports MCP (the protocol this project's agent tools use), can run code interpreters, generate images, connect to APIs, and handle multiple users with secure logins. Think of it as a personal AI hub that you control completely, with no usage fees beyond what the AI providers charge. For this project, it has no current active use case — the team works directly in Claude Code CLI. But if the need ever arises for a shared team AI interface, or a way to compare models side by side, LibreChat is the strongest open-source option available.

---

*Report by Rose | Session 244 | 2026-06-12*