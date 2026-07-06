# Web-Only Pre-Approved Tools

**Owner:** Soren (Security Manager) | Sage (CEO)
**Version:** 0
**Created:** 2026-06-02
**Status:** Active
**Subordinate to:** `Soren-Security-Manager-SOP.md` — Behavioral Standards (Web-Only Access governance rule, Item 66)

---

## Purpose

This document maintains the standing list of pre-approved web-only tools for the team. "Web-only" means the tool is accessed exclusively via web interface — no download, no install, no account required for the relevant use, no API keys, no local code execution. These tools do not enter the Soren clearance pipeline because nothing is downloaded, installed, or deployed.

**Soren is the defender.** Any new tool proposed for the pre-approved list requires Jay's or Sage's approval before it is added here. Agents do not self-authorize web-only tools.

---

## Criteria for Web-Only Classification

All five criteria must be met:

1. **Web interface only** — accessed via browser; no download or installation required
2. **No data submission beyond intended function** — the tool does not collect or transmit sensitive project data as a side effect of use
3. **No account required** — or account is already established and Sage-approved; not a new signup
4. **No API keys or credentials** — no authentication artifacts that could constitute a deployable or credentialed resource
5. **No local code execution** — nothing runs on the local machine as a result of using the tool

If any criterion is not met: the tool is not web-only. It requires Sage review and, if deployable, the full clearance pipeline (Rose → Soren → Lexi).

---

## Pre-Approved Web-Only Tools

| Tool | URL | Use Case | Approved By | Approved Session |
|------|-----|----------|-------------|------------------|
| GitReverse | gitreverse.com | Reverse-engineer GitHub repository structure; read public repo file trees | Sage (Jay direction) | Session 104 |

---

## Adding a New Tool

1. Any agent or Jay identifies a tool they want to use
2. Propose to Sage — include the tool name, URL, and intended use case
3. Sage evaluates against the five criteria above
4. If criteria are met and Sage or Jay approves: Sage adds the tool to this list
5. If any criterion fails: tool is not web-only — route through standard clearance pipeline

**Agents do not self-add.** All additions require explicit Sage (or Jay) approval.

---

## Version Log

| Version | Date | What Changed | Why |
|---------|------|-------------|-----|
