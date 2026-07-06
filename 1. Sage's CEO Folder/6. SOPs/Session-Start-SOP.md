# Session Start SOP

**Owner:** Sage
**Version:** 0
**Created:** 2026-06-15 (Session 254)
**Updated:** 2026-06-17 (Session 257)
**Status:** Active
**Future:** Convert to Cosmo skill during Master Library tasking

---

## Purpose

This SOP defines the standard sequence Sage runs at the start of every session to resume work with full context — without a manual wake-up prompt. It is the authoritative procedure for session start. The project CLAUDE.md loader points here; this SOP holds the steps.

The operating principle is **query first, read second.** The session-start tools (the per-project knowledge graph, the activity-recall buffer) are designed to surface current state cheaply. Full file reads are on-demand only — triggered by a gap the query surfaces, never run pre-emptively. The goal is to resume oriented while spending as little of the fresh context window as possible.

Nothing here is implied. If a step is skipped, it is skipped deliberately and the reason is stated — never silently.

**Scope — fresh session only.** This is the FRESH-session procedure. After a mid-session compaction, do NOT run this full sequence — follow `Post-Compact-Return-SOP.md` instead. The compact summary already holds full state; re-running the fresh read-in after a compact refills the context window and forces a second compact. Know which of the two procedures you are in before you start: opening a new session → this SOP; returning after a compaction → Post-Compact-Return-SOP.

---

## Technical Stack Layer — runs before this sequence

Before the read-in sequence below begins, the technical layer initializes automatically: plugins and hooks load at session start without manual action. This SOP does not manage that layer — it assumes it. For the full technical map (plugin init, hook load order, failure recovery), see `~/.claude/startup-stack-reference.md`.

**Identity layer auto-loads first.** Two files load into context automatically before this sequence: the global `~/.claude/CLAUDE.md` (Sage's identity and corporate charter) and the project `CLAUDE.md` (the loader that points to this SOP). This read-in sequence assumes the identity layer is already loaded — this SOP is the project *operating* layer, not the identity layer.

If a session opens and the read-in tools below behave unexpectedly (a query returns nothing, a buffer is absent), check the stack reference first — a missing hook or plugin is the likely cause, not a missing file.

---

## The Sequence at a Glance

1. Read all MEMORY.md index files (auto-loaded)
2. Read `lessons_global-CP.md`
3. Graphify query — current state (with file-read fallback)
4. Session activity recall — recent activity buffer + timeline (with fallback)
5. Just-in-time reads — only if steps 3–4 flag a gap
6. Activate Sophia (COO)

Then run the PBM fallback check (if PBM-eligible), confirm the current phase, and wait for direction — or proceed if the next action is unambiguous from the query.

---

## Step 1 — MEMORY.md Index Files

Read every file listed in the MEMORY.md index. These are the project-specific learning, feedback, and accumulated context for this project. The MEMORY.md index is auto-loaded by Claude Code at session start; read each file it links to. This is the project's standing memory — read it in full every session.

---

## Step 2 — Global Lessons (C&P Companion)

Read `~/.claude/lessons_global-CP.md` — the condensed companion to the global lessons file: one line per rule. Read this every session. Pull the full `~/.claude/lessons_global.md` only on demand, when a specific entry needs its full context.

---

## Step 3 — Graphify Query (current state)

Query the per-project knowledge graph to surface current state — current phase, active work, recent decisions, session state — without full reads of the soul and navigation files. Run the query from the project root; the CLI reads the project graph automatically from the current directory.

This query is what replaces bulk-reading the project's core soul and navigation set at every start. It is the primary "where are we?" instrument.

**Fallback — graph absent:** If the project graph file does not exist (fresh install, deleted index, or a brand-new project before the graph is built), read the five core files directly, in this order: `ME - Jay` → `Sage-project-soul` → `project-file-index` → `project-navigation-map` → the most recent `Session Summary` section only (find the last session header, read from there to the end of that section). A missing graph is not an error — it means the graph hasn't been built yet; fall back and proceed.

> **Boundary:** `project-file-index` and `project-navigation-map` are **artifacts this step consumes** — the file catalog and the operational/navigation layer respectively. This SOP names them and their role; it does not restate their contents. When a gap needs the file catalog or the navigation/trigger layer, consult those artifacts directly — they hold the data.

---

## Step 4 — Session Activity Recall

Recover what happened most recently, two ways:

- **Activity buffer:** the recent-activity buffer is surfaced automatically at session start via its hook and carries the last session's activity handoff. Read what it surfaces.
- **Timeline:** for deeper recall, query the activity timeline (context-mode `ctx_search`, sorted by timeline) to pull prior decisions, errors, plans, and prompts.

Together these replace reading the full Session Summary at start.

**Fallback — buffer absent and timeline empty:** read the most recent `Session Summary` section directly (last session header to the end of that section only).

---

## Step 5 — Just-in-Time Reads

Only if steps 3 or 4 flag a gap or missing context, read the specific file at that point — and only that file. Do not pre-read files the query has already covered. Earlier sessions and full soul files are available on demand; read them only if the current task requires it. This is the discipline that keeps the fresh context window intact: query first, read second, read narrowly.

---

## Step 6 — Activate Sophia (COO)

After completing the query sequence, activate Sophia before any work begins. Do not wait for Jay to prompt this — it is standing, not on-demand.

1. Send Sophia an opening brief and confirm she is active. Spawn her as an **embedded observer in `acceptEdits` mode** — per the canonical run-model rule (Sage MG v2.72, *Agent Teams — Operating Model*), an in-session subagent is non-interactive and cannot self-approve, so `acceptEdits` is what lets her documentation writes auto-approve. A default-mode spawn fails closed on every write (failure mode: Gotcha #35).
2. Sophia reads `Gotcha.md` — the CEO pulse check; know the active watch-out rules and documented traps before the session begins.
3. Sophia's Pending Changes List is open and active from session start. Sage reviews it at session start and again at session close. Sophia is ready to receive notes, document decisions, and queue any source-material changes the moment work begins.

**P/M Lead activation:** If a designated P/M Lead is active on the project (e.g., a coursework lead), session-start activation extends to them under the same standing-activation principle as Sophia. A full brief is required only on first introduction, not every session. Sophia's activation remains the primary; the P/M Lead activation is additive.

---

## After the Sequence

**PBM fallback check.** When the project is PBM-eligible — a live/operational track running alongside an infrastructure track — and Jay opens the session without declaring which track is active, Sage asks which track before any work begins. This is the CEO's responsibility, not the agents'. Do not assume a track from context.

Then confirm the current phase and wait for Jay's direction — or proceed immediately if the next action is unambiguous from the query results. No wake-up prompt is required; this sequence handles session continuity.

---

## Notes

- This SOP is the authoritative procedure for session start. The project CLAUDE.md loader points here — it does not duplicate these steps.
- Query first, read second. The graph query (Step 3) plus activity recall (Step 4) are sufficient to resume in most sessions. Full reads are the exception, not the rule.
- Companion to `Session-Close-SOP.md` and `Compact-Wrap-Up-SOP.md` — those govern session end and compaction; this governs session start. The post-compact *return* path is governed by `Post-Compact-Return-SOP.md` (built alongside this SOP).
- **First session is a valid state.** A brand-new project — Session 1, with no Session Summary and no knowledge graph built yet — is normal, not an error. Missing artifacts at first run mean the project hasn't generated them yet. Note it and proceed; the fallbacks in Steps 3 and 4 cover this.
- If a step cannot be completed, document why before moving on — never skip silently.
- Convert to Cosmo skill at Master Library tasking. SOP stays as the authored source.

---

