# Rose — Research Report: `board` (The-Coding-Trader/board)

**Filed by:** Sage (capture of Rose's delivered report, verbatim) — Session 1, 2026-07-06
**Routing:** Project-specific → Jot mini-project folder (not Master Library)
**Status of flags:** Provenance RESOLVED post-report (Jay: friend's account). Soren clearance delivered separately — see `soren-security-clearance-board-repo.md`.

---

**URL:** https://github.com/The-Coding-Trader/board
**Date Researched:** 2026-07-06
**Researched by:** Rose | Security pre-check: Soren (in parallel) | Report by: Rose
**Already in Master Library?** No — external GitHub repo, read-only research
**Prompt Injection Check:** None detected. Scanned README, store.go, model.go, go.mod. No instruction-like text, directives, or embedded prompts in any fetched content.

---

## What It Is

`board` is a lightweight terminal app (a "TUI" — a keyboard-driven interface that runs inside your terminal window, no mouse, no browser) that gives you a three-column kanban board — Backlog, In Progress, Done — plus a free-text scratchpad. Everything it stores lives in a single plain-text Markdown file called `.board.md` sitting in whatever folder you launch it from. Its whole design premise is co-editing: you edit in the TUI, and Claude Code (or any editor) can read and rewrite the same file at the same time, with the board updating live on screen.

## What It Does

- Three-column kanban with add / edit / delete / move cards (`H`/`L` between columns), mark-done with Space, vim-style navigation
- A scratchpad for quick note capture, with one-key promotion of a scratch line into a Backlog card (`Ctrl-P`)
- Stores all state as human-readable Markdown (`- [ ]` / `- [x]` checkboxes under `##` headers) — no database, no server
- **Live reload** — polls the file once per second (checks modified-time + size) and redraws when it changes on disk, so external edits appear automatically
- **Atomic saves** — writes to a temp file, fsyncs, then renames over the target, so a reader never catches a half-written file
- **Conflict-aware scratchpad** — if you're mid-edit and the file changes underneath you, it flags the conflict instead of clobbering your in-flight text; preserves unknown sections/headers verbatim on round-trip

## Tech Stack & Architecture

- **Language:** Go (1.26.4). **Verified.**
- **Framework:** Charmbracelet's Bubble Tea v2 stack (bubbletea v2.0.8, bubbles v2.1.1, lipgloss v2.0.4) — the standard, well-regarded Go toolkit for terminal UIs. Custom "Reef" teal theme. **Verified** (go.mod).
- **Storage:** one local Markdown file per board. No server, no DB, no network calls, runs entirely local. **Verified** (store.go).
- **Size:** ~27 KB, 7 source files. Clean layout: `cmd/board/main.go` entry point, `internal/board` (store + parser), `internal/ui` (model/columns/keys), `internal/theme`. UI model is ~250–280 lines, moderate complexity. Has unit tests (`store_test.go`, `model_test.go`). **Verified** (file tree).

## Maturity & Provenance

- **Brand new.** Created 2026-07-05, last push 2026-07-06 — literally one day old at time of research. 0 stars, 0 forks, 0 open issues, 0 watchers. Not archived, not itself a fork. **Verified** (GitHub API).
- **License: MIT.** Fully permissive — we can legally fork, revamp, relicense-in-use, and ship it, provided the MIT copyright notice is retained. **Verified.**
- **Provenance flag — Single-source / Inferred:** The owning org is `The-Coding-Trader`. Given Jay's trading context and the repo's age (one day) and total obscurity (zero external traction), it is plausible this is **Jay's own account or one close to him** rather than a third party. I can't confirm ownership from public data alone. **This matters:** if it's Jay's repo, the "can we legally fork it" question is moot entirely — worth a 10-second confirm from Jay before Soren spends cycles on external-provenance vetting.
  - *[Post-report resolution — Sage, same session: Jay confirmed the account belongs to a friend who built it and showed it to him. Provenance settled. Soren's clearance conditions unaffected.]*

## Fit Assessment — "a personal notes system that's always there"

**What's already good and directly on-target:**
- The storage pattern is exactly right for "something I can just have": one plain Markdown file, human-readable, no server to start, no database, survives forever, greppable, git-friendly.
- The **AI co-edit + live-reload + atomic-save** trio is the genuinely valuable, non-trivial part — Claude can rewrite your notes file and you see it update live without corruption. That's the hard engineering already solved.
- Scratchpad = the seed of a quick-capture notes surface.
- Tiny, clean, tested, modern stack — pleasant to build on.

**Where it misses the "notes system" target (honest gaps):**
- It is fundamentally a **kanban task board**, not a notes system. The bulk of the code is columns/cards/task-flow — task-shaped, not note-shaped.
- The scratchpad is a **single free-text blob**, not multiple notes. No note titles, no timestamps, no tags, no folders, no search, no per-note files. "Take a note" today means "append to one big text box."
- **One file = one board.** No concept of a notes library or many notes.
- **"Always there" is aspirational, not literal.** It's a TUI you launch inside a directory. It is not a background daemon, not a global capture hotkey, not always-on. To get Jay's "always ready" feel, that layer doesn't exist yet.

## Revamp Scope Estimate — honest take

**Verdict: strong source of inspiration and a proven storage/co-edit engine — a good skeleton, not a drop-in base.**

- If we fork it: we'd **keep** the `internal/board` store (markdown parse/serialize, atomic save), the theme scaffolding, the live-reload polling, and the Bubble Tea harness. That's the reusable core and the hardest ~40%.
- We'd **rewrite** the UI/model layer — swap the kanban-columns mental model for a notes model (list of notes, titles, quick-capture, search, maybe tags). The columns/cards logic is the majority of the current UI code and mostly wouldn't survive the pivot.
- Realistic effort signal: **Moderate** (roughly half-day to a day for a working notes-flavored fork on top of the existing store), *not* Simple (it's a genuine repurpose, not a config tweak) and *not* Complex (the stack is small and clean, storage is done). Build-fresh would cost more and throw away a working co-edit engine — so forking wins **if** we want the terminal-Markdown-file approach.
- **The real decision isn't this repo — it's the product shape.** If Jay wants terminal + one Markdown file + Claude co-editing, this is a great head start. If he pictures many discrete notes, search, tags, or an always-on background capture surface, this repo gets him the storage engine and about a third of the way, and the notes UX is net-new regardless.

## Master Library Assessment

- **Proposed Section:** Not a catalog candidate yet — this is a fit/base-selection evaluation, not a resource intake. If we proceed to fork, the *forked* artifact becomes an internal build, not an ML external entry.
- **Provisional if cataloged as reference:** Section 7 (Reference & Ecosystem), Tier 2 — clean reference implementation of the markdown-file + AI-coedit + live-reload pattern.
- **Deployment Potential:** Conditional — contains deployable code; requires Soren clearance before any fork is built or run.

## Soren Security Pre-check

- **Verdict:** DEFERRED to Soren (reviewing in parallel). *[Resolved same session: Soren delivered CLEARED WITH CONDITIONS — see companion file.]*
- **Rose's read from source (Inferred, not a clearance):** No network calls, no shell-out, no obvious data exfiltration in the files I read (store.go, model.go). Only concerns for Soren: (1) it's a one-day-old repo with zero community vetting — provenance rests entirely on the code, so a full code audit is warranted before any build; (2) confirm the `charm.land/*` module path resolves to the legitimate Charmbracelet libraries and not a typosquat (new module namespace — worth a look). *[Both addressed by Soren: full source read completed; charm.land verified as Charmbracelet's official vanity import domain.]*

## Recommendation

Treat this as a **strong base skeleton, contingent on two confirmations.** (1) Get Jay to confirm whether `The-Coding-Trader` is his own account — if yes, licensing/provenance is settled instantly. *(Resolved: friend's account.)* (2) Get Jay to confirm the product shape: terminal + single Markdown file + Claude co-edit? If both land favorably, forking is the efficient path — keep the store/reload/save engine, rewrite the UI for notes. If Jay wants multi-note management, search, or an always-on capture surface, use this as **inspiration and a storage-pattern reference** and scope a fresh notes UX on top of its proven engine. Either way, no build until Soren clears it. *(Cleared with conditions.)*

## C&P Summary

`board` is a tiny, brand-new, free-to-use terminal program that shows you a to-do board (three columns: to-do, doing, done) plus a scratch area for quick notes — and it saves everything into one ordinary text file you can read with any editor. Its clever part is that Claude can edit that same file while the board is open, and the screen updates instantly without ever corrupting the file. For Jay's "notes system I can just have," the good news is the storage approach is exactly right and the hard save-and-sync engineering is already done; the catch is that today it's built for tasks, not notes — it keeps one big scratch blob, not many separate notes, and it isn't a background always-on tool yet. So it's an excellent starting skeleton and idea source, not a finished notes app: worth forking if Jay wants the terminal-plus-text-file style, with the note-taking experience still to be built on top.

---
*Report by Rose | 2026-07-06*

**Adversarial pass:** Cross-checked README claims against actual source (store.go, model.go, go.mod, file tree) — storage format, atomic save, live-reload polling, and dependency stack all confirmed in code, no contradiction between marketing and implementation. Single unverified item flagged explicitly: repo ownership/provenance (`The-Coding-Trader`). *(Resolved post-report.)*
