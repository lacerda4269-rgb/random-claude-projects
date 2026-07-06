# [Project Name] — Project CLAUDE.md

**Version:** 0
**Project:** [Project name — fill in during Phase 0]
**Phase:** [Current phase — update each phase]
**Status:** [Active / On Hold / Complete]

---

## Session Start — Auto Instructions

**Authoritative procedure: `Session-Start-SOP.md`** (`1. Sage's CEO Folder/6. SOPs/`). This section is the auto-load summary; the SOP governs the full sequence, fallbacks, and detail.

> **Technical stack layer:** Before this sequence runs, plugins and hooks initialize automatically. See `~/.claude/startup-stack-reference.md` for the full technical layer map, hook load order, and failure recovery guide.

**At-a-glance** (query first, read second):

1. MEMORY.md index files
2. `~/.claude/lessons_global-CP.md`
3. Graphify query — current state
4. Session activity recall (claude-remember buffer + context-mode timeline)
5. Just-in-time reads (gap-triggered only)
6. Activate Sophia (COO) — opening brief + `Gotcha.md` pulse check

Then confirm the current phase and wait for direction — or proceed if the next action is unambiguous from the query. **No wake-up prompt required.**

> **After a mid-session compaction:** do NOT re-run this sequence — follow `Post-Compact-Return-SOP.md` (same SOPs folder). See the Post-Compact Protocol section below.

> **Personal notes folder:** Every project has an operator-owned personal notes folder (name varies per project). Sage never reads it. Identify the folder name during Phase 0 housekeeping review and note it here: `[Personal notes folder — name at Phase 0]`

> **First session is a valid state:** on a brand-new project there is no knowledge graph and no `Session Summary.md` yet — that is normal, not an error. The `Session-Start-SOP.md` fallbacks cover it.

---

## What This File Is

This is the project-level auto-loader. Claude Code injects it into every prompt automatically when opened in this project folder.

- It is **not** a soul file — project identity lives in `Sage-project-soul.md`.
- It is **not** Sage's identity — that lives in `~/.claude/CLAUDE.md` (global, auto-loads separately).
- Its only job: tell Sage what to read at session start so no manual wake-up prompt is needed.

**Keep this file lean.** If you are tempted to add content here, ask whether it belongs in `Sage-project-soul.md` instead. These two files must never overlap.

---

## Context Window — Compact Wrap-Up & Post-Compact Protocol

**Before compaction:** When Jay signals intent to compact, Sage runs the **Compact-Wrap-Up-SOP** before compaction occurs — all files updated and pushed first. The signal is intent-based (context clues, not a specific phrase). The **mid-task gate** fires first: no compact begins while any agent (Sophia / P/M Lead in scope) is mid-task. SOP: `1. Sage's CEO Folder/6. SOPs/Compact-Wrap-Up-SOP.md`

**After any compaction:** follow the **Post-Compact-Return-SOP** — `1. Sage's CEO Folder/6. SOPs/Post-Compact-Return-SOP.md`. In brief: the one mandatory read is the most recent CP section in `Session Summary.md` (check the **Files Modified** field); do NOT re-run the full session-start sequence; re-activate embedded agents (Sophia / P/M Lead) before resuming; context-window milestones reset to zero.

---

*This file lives in the project root folder. Do not move it.*
*Update only when: project name, current phase, status, file paths, or session start steps change.*
*Both Master Guides must be updated if this template changes — same session, no exceptions.*

