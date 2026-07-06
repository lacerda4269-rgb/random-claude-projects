# Resource Report: LLM Guard

**Prepared by:** Rose (Researcher)
**Reviewed by:** Soren (Security Manager)
**Tasked by:** Sage (COO)
**Date:** April 15, 2026
**Category:** Soul Folder — Security Tools
**Role in Stack:** Standby (runtime) — Category 1 (Prompt Injection / LLM Content)
**Status:** Research complete — pending Soren configuration

---

## What It Is

LLM Guard is an open-source Python library and standalone API server from Protect AI (`protectai/llm-guard`). It provides input and output scanning for LLM pipelines — designed to run inline as a guardrail between users and LLM responses. Last known version: v0.3.16. GitHub: 3,049 stars, 400 forks (as of 2026-06-08). **Maintenance flag: last push to GitHub was December 15, 2025 — approximately 6 months of inactivity. Dormancy risk elevated. Verify PyPI for any updates before deployment.** License: MIT — fully free including commercial use. Self-hosted only — no data leaves the local infrastructure.

---

## What It Does

- 35 built-in scanners: 15 input scanners, 20 output scanners
- Input scanning: prompt injection detection, jailbreak pattern detection, PII leakage, hardcoded secrets, toxicity, invisible/hidden text
- Output scanning: response safety, PII in responses, sensitive data leakage, harmful content detection
- Deployable as a Python library (embedded in code) or as a standalone Docker-hosted API server
- Self-hosted — all scanning runs locally, no telemetry

---

## Installation & Setup (Windows)

**Important: LLM Guard requires Python 3.10, 3.11, or 3.12. It does NOT support Python 3.13 or higher. This is a hard constraint — see Limitations.**

1. Install a supported Python version (3.10, 3.11, or 3.12) — use pyenv-win or direct installer from python.org
2. Create a dedicated virtual environment: `python -m venv llmguard-env`
3. Activate it: `llmguard-env\Scripts\activate`
4. Install LLM Guard: `pip install llm-guard`
5. GPU acceleration is available but not required — CPU-only works fine
6. For standalone API server mode: Docker is required; pull the official image and run as a local service

---

## Free Tier Details

Completely free. No usage limits. No account required. No API key required. MIT license allows commercial use without restriction. Self-hosted only — there is no cloud-hosted paid tier for LLM Guard itself.

---

## Limitations

- **Python version constraint: requires Python 3.10–3.12. Does NOT support Python 3.13+.** This conflicts directly with Snyk Agent Scan (Cat 3), which requires Python 3.13+. If both are installed on the same machine, they need separate Python environments. This is a known conflict and must be managed before either tool is configured.
- Not a file scanner — designed for runtime pipeline integration, not one-off file checks. Using it for static file scanning is inefficient and not its intended purpose.
- Heavier than SecureClaw for static file scans — requires a Python environment and has more dependencies
- GPU acceleration improves performance but adds setup complexity
- 35 scanners means there is a learning curve to understand what each one does and which ones to enable

---

## Role in Soren's Pipeline

LLM Guard is the standby, not the primary. SecureClaw handles Soren's file-based pre-deployment scans. LLM Guard comes in if and when the team needs runtime API-level protection — a live guardrail sitting between agent inputs/outputs and the LLM itself. That use case does not currently exist at this project stage. When it does, LLM Guard is the confirmed tool for that layer. Pre-deployment file scanning: SecureClaw. Runtime API guardrail: LLM Guard.

---

## Soren's Operational Note

**Re-reviewed 2026-06-08 — STANDBY status with ELEVATED DORMANCY FLAG.** This is a verdict-condition update, not a clearance change — LLM Guard was never formally cleared because it was never slated for immediate deployment (standby role). That standby status is now reinforced with a stronger caution.

Rose's freshness sweep confirmed: last GitHub push December 15, 2025 — **approximately 6 months of GitHub inactivity as of this review**. No GitHub releases found (no formal versioned release history on record). Stars have grown (2,500 → 3,049) indicating continued community interest, but that does not compensate for an inactive codebase. Version remains v0.3.16; PyPI activity has not been directly verified in this sweep.

**Assessment:** The dormancy flag is now material, not precautionary. Six months of no commits on an active security tool is a meaningful signal. Before this tool is approved for deployment, two things must happen: (1) PyPI must be checked to confirm whether any releases shipped after December 2025 that did not appear in the GitHub push history; (2) the project's maintenance status must be re-evaluated — if the last PyPI push also predates Q1 2026, the tool should be reclassified as dormant and a replacement identified for the runtime guardrail role. The Python version conflict with Snyk (LLM Guard caps at Python 3.12; Snyk requires Python 3.13+) remains a known planning issue.

**Action required before deployment:** Verify PyPI for post-December-2025 releases. If none found, escalate to Sage — the dormancy risk may warrant identifying an actively maintained alternative before the runtime guardrail use case arrives.

I do not need to configure this now. SecureClaw is handling Category 1 for the current phase. LLM Guard is the tool I reach for when the team gets to a point where agents are running live and I need a guardrail between agent inputs and LLM responses — not for reviewing files before they enter the library. When that time comes, the critical thing I need to resolve first is the Python version conflict: Snyk Agent Scan requires Python 3.13+, and LLM Guard caps at Python 3.12. I cannot run both in the same environment. The solution is a dedicated virtual environment for LLM Guard on Python 3.12, separate from the Python 3.13 environment used for Snyk Agent Scan. I need to have that environment architecture planned before I install either tool and treat them as sharing a runtime.

---

## Sage's COO Note

The Python version conflict between LLM Guard (Python 3.12 cap) and Snyk Agent Scan (Python 3.13+ requirement) is a real dependency management issue that affects any developer on this team who installs both tools. Before either is configured, the environment separation approach needs to be documented in Soren's SOP so every future team member knows which Python version lives where. This is worth a brief planning conversation before configuration begins.

---

## C&P Summary

LLM Guard is Soren's standby tool for Category 1 — a runtime pipeline guardrail with 35 scanners for prompt injection, PII, jailbreak patterns, toxicity, and hidden text in LLM inputs and outputs. It is not used for file scanning (that is SecureClaw's job) — it comes in if and when the team needs live API-level protection between agents and an LLM. MIT licensed, fully free, self-hosted. Key constraint: Python 3.12 maximum, which conflicts with Snyk Agent Scan's Python 3.13+ requirement — separate virtual environments are required if both tools are installed. **Dormancy flag: last GitHub push December 2025 — verify PyPI activity before deployment.**

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
