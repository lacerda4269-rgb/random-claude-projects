# Hard Rules — Master List

**Version:** 0
**Date:** 2026-06-11
**Owner:** Sage
**Source:** Master Guide — Sage's Version (SOP v1) — Standing Rules section
**Status:** Active

---

## What This Is

The complete list of Hard Rules — every non-negotiable rule that applies to every project, without exception. These are not project-specific; they are universal. Every project Jay and the team run operates under all 21 of these rules from Day 1.

The full rationale for each rule lives in the Master Guide — Sage's Version (SOP v1). This document is the quick-reference master list.

---

## The 21 Hard Rules

### Git & Version Control

| # | Rule | What It Means |
|---|------|--------------|
| 1 | **Main branch is always protected** | All edits go into a feature branch first. Nothing goes directly to main. |
| 2 | **GitHub repo created at project start (for projects with code)** | Before any code is written. Confirmed during Phase 0 for all projects — Sage asks if it hasn't been mentioned. |
| 3 | **GitHub automatic backup via Cron Job before serious coding begins** | Required safety net before any substantial code work starts. |

### Security

| # | Rule | What It Means |
|---|------|--------------|
| 4 | **NEVER put credentials, passwords, or API keys in code** | Always use `.env` files. Credentials in code is a hard stop — no exceptions. |
| 5 | **Rose conducts a periodic security META check** | At the start of every new project, Rose researches the latest AI security threats, prompt injection vectors, new attack methods, and emerging protective measures. Soren reviews all findings and flags anything that affects active project workflows. Sage and Jay are notified of any action items. Ad-hoc META checks are triggered any time Rose identifies an emerging critical threat mid-project. Cadence details and triggers live in Rose's SOP and Soren's SOP. Any resource arriving from outside the cleared library that was not sourced by Rose is an automatic denial — no exceptions. |

### Project Setup & Structure

| # | Rule | What It Means |
|---|------|--------------|
| 6 | **Phase 0 and Phase 1 are mandatory — no exceptions** | Every project brainstorms first (Phase 0) and blueprints second (Phase 1). No matter how simple the project. |
| 7 | **Every project has a Sage-project-soul.md** | Created during Phase 0–1. Always built first, before Skills, Hooks, CLIs, and MCPs. |
| 8 | **Every project includes a COO** | Sophia (COO) is active from Day 1: documentation, operational health monitoring, and AAR at close. |
| 9 | **Build order: Soul → Skills → Hooks → CLIs → MCPs — no exceptions** | The sequence is the rule. Hooks come after Skills and before CLIs. CLIs are always evaluated before MCPs. An MCP is only added when no CLI exists or OAuth/statefulness is genuinely required. Other resources (Subagents, Agent Teams, Plugins) are project-dependent and slot in where genuinely required. |

### Session Standards

| # | Rule | What It Means |
|---|------|--------------|
| 10 | **Declare session mode at the start of every session** | Ask / Plan / Auto — said out loud before any work begins. No silent defaults. |
| 11 | **Every project includes the model-switching guide** | The guide lives in Master Guide — Sage's Version (SOP v1). It ships with every project. |
| 12 | **Every project has a living summary file updated at end of each session** | The Session Summary — cumulative, never replaced, pushed to GitHub each session close. |

### Document & Content Standards

| # | Rule | What It Means |
|---|------|--------------|
| 13 | **Paired documents always updated together — pairing decision required before every build** | Any document with a paired counterpart (Sage/Agent version + Jay's version) must be updated in the same session. Applies to both Master Guides and all SOPs. A change to either version is a trigger to sync the other version before the session closes — applies in both directions. Same session — not next session. **Pre-build gate:** Before any SOP build begins, Sage confirms with Jay whether a Jay's version will be built. The answer is documented at Step 0 before any drafting begins. "No" is a valid and documented decision — not an oversight. Once a Jay's version exists, the full pairing rule applies from that point forward. **Visual workflow alternative:** A visual workflow or flowchart (e.g., a Mermaid diagram) may fulfill the role of Jay's version when the visual fully represents the SOP workflow and there is no genuine operational need for a separate plain-text Jay's version. This determination is made and documented at Step 0 — not assumed. Once a true Jay's version is independently created, the full pairing rule applies from that point forward. |
| 14 | **Cross-reference updates are mandatory — same session** | Any change to any document (SOP, Master Guide, soul, template, or process doc) requires a cross-reference pass in the same session: identify all related documents that reference the changed content and update them before the session closes. The session is not clean until all cross-references reflect the change. Sage owns this pass for every update. No exceptions. |
| 15 | **No absolute file paths in operational documents** | SOPs, templates, instructions, and any document that ships with or is created during a project must use role-based references and descriptive labels — not machine-specific paths. The project CLAUDE.md resolves actual paths at setup for each machine. Keeps every document portable and machine-agnostic. **Carve-out (by reference TYPE, not environment):** project-navigation paths (where files and folders live within a project) are always role-based; machine-fact paths (tool install locations, binary paths, OS paths literally true of the machine) may be stated literally. |
| 16 | **Universal logical ordering — lists, tables, and collections** | Any list, table, or collection of items — when created, updated, added to, or reorganized — must be placed in logical order. Creation order is not logical order. Applies universally across all documents: Hard Rules, Quick Reference tables, agent rosters, task lists, and any other organized collection. Applies on creation and on every update. |

### Project Lifecycle

| # | Rule | What It Means |
|---|------|--------------|
| 17 | **Source materials frozen during any active project** | Source materials = `~/.claude/CLAUDE.md`, both Master Guides, all Initial Package templates. Changes identified mid-project go into Sophia's Pending Changes List — applied only after AAR. **Emergency exception:** Jay explicitly approves — flagged in pending list, evaluated at AAR. **Exempt:** Project `CLAUDE.md` (project root) — updated mid-project when phase, status, or file paths change. |
| 18 | **CLAUDE.md + backup soul repo updated at every project close (AAR)** | After every project is marked fully done, Sage updates global CLAUDE.md with any AAR changes and pushes to `lacerda4269-rgb/0-GitHub-Sages-True-Soul-Never-Delete`. Happens automatically — no separate prompt from Jay required. |

### Agent Behavior

| # | Rule | What It Means |
|---|------|--------------|
| 19 | **Semi-AGI problem-solving framework — three-altitude approach applies to all agents** | Before retrying or escalating any blocked task, every agent classifies the problem by altitude: Task level (within the agent's lane and scope) → apply the two-round rule; System level (affects overall approach, design decisions, or other agents' lanes) → escalate to Sage immediately, do not apply two-round rule first; Vision level (touches company direction or end goals) → Sage escalates to Jay. Resource access: Master Library first; information-only needs (research, facts — nothing deployable) → submit to Sage, routed to Rose (Soren review not required); new external deployable resource (tool, CLI, MCP, or artifact) → full pipeline (Sage → Rose → Soren → Lexi). Applies to all agent souls (built and generic shells). Standing build input for all future agent SOPs. |

### P/M Lead Operations

| # | Rule | What It Means |
|---|------|--------------|
| 20 | **P/M Lead folder + escalation chain — universal standard for all projects with a P/M Lead** | Every project with a P/M Lead or P/M Lead group establishes a dedicated P/M Lead folder containing the project soul and master deliverable summary. Naming — single lead: `[N]. [Name]'s Folder (Project Lead Personal Folder)`; multiple leads: letter-prefix system (`[N]a.`, `[N]b.`, etc.). P/M Leads operate autonomously on all task-level project work. Escalation fires on process breakdowns, system-level gaps, or blockers outside the P/M Lead's control — chain: P/M Lead → Sophia → Sage → Jay. Both sides use the 0-10 involvement scale. Per-project tailoring of thresholds permitted in the project soul; the chain does not change. Maps to HR19 (three-altitude framework). Living framework — grows with each live project. |

### Resource Build Standards

| # | Rule | What It Means |
|---|------|--------------|
| 21 | **Tri-form assessment + paired-update for all built resources** | Before any build design commits, assess the tool against all three possible forms: (1) command/slash command — user-invoked; (2) skill — auto-invoked on trigger match; (3) hook — fires on a named system event. Build whatever forms apply; Cosmo decides and documents the rationale in the build brief. When any form of a multi-form resource is updated, ALL existing forms of that resource must be updated in the same pass. Extends Hard Rule 13 (paired documents always updated together) from document pairs to multi-form resource sets. |

---

## Are These Universal?

Yes. All 21 rules apply to every project — not just this one. They are designed to work at any scale and any involvement level (0–10). The only exceptions and nuances are noted in each rule row above.

---

## Where the Full Rationale Lives

Full explanation for each rule: **Master Guide — Sage's Version (SOP v1)**, section: *Hard Rules — Non-Negotiable for Every Project*.

Jay's plain-language version of the most important rules: **Master Guide — Jay's Version (SOP v1)**, section: *Quick Reference — Rules to Remember*.

---


