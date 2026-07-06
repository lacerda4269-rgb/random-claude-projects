# Surface Transition — Cross-Surface Context Handoff Skill

**Skill name:** `/surface-transition`
**Built by:** Cosmo (Skill Creator)
**Source:** Internal — cross-surface handoff protocol (operational standard)
**Soren status:** CLEARED (internal build — no external resource)
**Version:** 0
**Built:** 2026-06-01
**Cataloged section:** 3 — Skills | Tier 1
**Item:** 147

---

## What It Does

Documents and guides the cross-surface context handoff protocol. When switching from one Claude surface to another (e.g., Claude Code CLI to Claude Desktop tab, or Claude Code to a new project session), this skill prompts the operator through the full handoff checklist — what to package before leaving, the standard handoff steps, how to pick up on the other side, and continuity verification before starting work on the new surface.

Prevents context loss, dropped tasks, and silent continuity failures when work moves across surfaces.

---

## When to Use

Invoke before:
- Switching from Claude Code CLI to a Claude Desktop tab or web session
- Switching between project worktrees or sessions within Claude Code
- Handing a task off to a different agent operating on a different surface
- Any planned surface change where active work, open tasks, or agent state is in play

Do NOT invoke for:
- Routine session closes (use the Session Close SOP)
- COHK events (use `/cohk`)
- Mid-session tool switches that don't involve a surface change

---

## Invocation

```
/surface-transition
```

Optional modifiers:

```
/surface-transition out       → package context for leaving (Steps 1–3 only)
/surface-transition in        → pick-up checklist for arriving on new surface (Steps 4–5 only)
/surface-transition verify    → continuity verification only (Step 5 only)
```

---

## The Protocol — Full Sequence

---

### STEP 1 — Session State Snapshot (Before Leaving)

```
╔══════════════════════════════════════════════════════╗
║  SURFACE TRANSITION | Step 1 — Session State        ║
╚══════════════════════════════════════════════════════╝

Capture the current session state before switching surfaces.
Answer each item:

  PROJECT STATE
  □ Active project: ___________________________________
  □ Current phase / track: ____________________________
  □ Last completed action: ____________________________
  □ Next action (what you were about to do): __________

  OPEN TASKS
  □ In-progress tasks (list each with status):
    ________________________________________________
    ________________________________________________
  □ Blocked tasks (list each with blocker):
    ________________________________________________
  □ Tasks queued to Sophia / pending list:
    ________________________________________________

  ACTIVE AGENTS
  □ Which agents are currently engaged / mid-task:
    ________________________________________________
  □ Pending handoffs or agent responses expected:
    ________________________________________________

  CONTEXT FLAGS
  □ Any decisions made this session not yet permanently captured:
    ________________________________________________
  □ Any open questions waiting on Jay:
    ________________________________________________

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Session state captured? (y to advance to Step 2)
```

---

### STEP 2 — Pre-Switch Handoff Checklist

```
╔══════════════════════════════════════════════════════╗
║  SURFACE TRANSITION | Step 2 — Pre-Switch Checklist ║
╚══════════════════════════════════════════════════════╝

Complete all that apply before leaving this surface:

  FILES & CAPTURES
  □ All decisions from this session written to the appropriate
    permanent file (Session Summary, project_context.md, etc.)
  □ Any in-progress file edits saved and committed or staged
  □ MEMORY.md index current (new entries added if needed)
  □ Sophia's Pending Changes updated with any unresolved items

  TASKS
  □ In-progress tasks documented in a recoverable state —
    if someone else opened this project right now, could they
    tell exactly where the work stopped?
  □ Blocked tasks flagged with blockers in writing
  □ All TodoWrite items current (completed marked, new items added)

  AGENTS
  □ Any mid-task agent briefed on the pause — they know work
    is stopping and why
  □ No agent is waiting on a response that won't come

  GITHUB (if leaving for an extended period or different machine)
  □ Git status clean or outstanding changes documented
  □ Push to GitHub if there are changes that should persist
    across the surface switch

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Pre-switch checklist complete? (y to advance to Step 3)
```

---

### STEP 3 — Context Package

```
╔══════════════════════════════════════════════════════╗
║  SURFACE TRANSITION | Step 3 — Context Package      ║
╚══════════════════════════════════════════════════════╝

Write the hand-off note. This is the artifact the new surface
reads to orient itself. Brief, precise, complete.

CONTEXT PACKAGE FORMAT:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Surface leaving: [Claude Code CLI / Desktop / Other]
Surface arriving: [Claude Code CLI / Desktop / Other]
Date/Session: [date] | Session [N]

PROJECT: [project name and version]
PHASE/TRACK: [current phase and track]

LAST ACTION COMPLETED:
[one sentence — what was just done]

NEXT ACTION (pick up here):
[one sentence — the very next thing to do]

OPEN TASKS:
- [task 1] — [status]
- [task 2] — [status]

ACTIVE AGENT STATE:
- [agent] — [what they're doing / waiting on]

CONTEXT FLAGS (decisions not yet permanent):
- [flag 1]

BLOCKERS:
- [blocker 1] — [what's needed to unblock]

FILES TO READ ON ARRIVAL:
- [file path 1] — [why]
- [file path 2] — [why]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Save this context package where the new surface can read it:
  Option A: Paste it as the first message on the new surface
  Option B: Save to a temp file and read it in on the new surface
  Option C: Capture it in Sophia's Pending Changes as a transition note

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Context package ready? (y — surface switch authorized)
```

---

### STEP 4 — Pick-Up on the New Surface

```
╔══════════════════════════════════════════════════════╗
║  SURFACE TRANSITION | Step 4 — Arrival Pick-Up      ║
╚══════════════════════════════════════════════════════╝

You have arrived on the new surface. Before starting any work:

  LOAD CONTEXT
  □ Read the context package from Step 3
  □ Read CLAUDE.md and MEMORY.md (if not already auto-loaded)
  □ Read the Session Summary — most recent session entry only
  □ Read project_context.md — current state section

  ORIENT
  □ Confirm you know: active project, current phase, next action
  □ Confirm open tasks are visible
  □ Confirm active agent state is known

  SURFACE-SPECIFIC SETUP
  □ Claude Code CLI: confirm working directory is correct project
  □ Claude Desktop tab: confirm project CLAUDE.md is accessible
  □ New session: confirm auto-load sequence ran (lessons files, soul, index)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Context loaded and orientation complete? (y to advance to Step 5)
```

---

### STEP 5 — Continuity Verification

```
╔══════════════════════════════════════════════════════╗
║  SURFACE TRANSITION | Step 5 — Continuity Check     ║
╚══════════════════════════════════════════════════════╝

Before starting any work on the new surface, confirm:

  □ Project state matches what Step 3 documented
    (nothing was changed on the prior surface after the package was written)

  □ Open tasks list matches — no tasks are missing or duplicated

  □ Next action is clear and unambiguous

  □ No agent is waiting on something that was never delivered
    (check Sophia's Pending Changes for any transition-flagged items)

  □ Git status checked — working tree state matches expectations

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SURFACE TRANSITION COMPLETE

If everything checks out → begin work on the new surface.

If continuity gap detected:
  → Document the gap
  → Surface to Sage before proceeding
  → Do not start work on an ambiguous state

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Continuity confirmed? (y — begin work | n — resolve gap first)
```

---

## Live-Process Requirements — MCP Upgrade Candidates

The following requirements were identified during this build that a simple Skill cannot fully address. These are flagged as MCP candidates for a future upgrade:

**1. Real-time session state inspection**
The skill currently relies on the operator to manually answer Step 1. An MCP that could read the current Claude Code session state (open files, recent tool calls, active TodoWrite list) and pre-populate Step 1 automatically would eliminate the manual capture burden and reduce the risk of missed context.

**2. Cross-surface session relay**
The context package in Step 3 requires manual copy/paste or file saves. An MCP with access to a shared, persisted context store (e.g., a lightweight key-value store or a shared memory endpoint) would allow the context package to be pushed from the departing surface and pulled automatically on the arriving surface — eliminating the manual transfer entirely.

**3. Git status check integration**
Step 2 and Step 5 reference git status. An MCP or CLI wrapper that surfaces git status inline during the transition flow (rather than requiring a separate terminal command) would tighten the handoff and catch uncommitted changes automatically.

All three are skill-to-MCP upgrade candidates. None block the current Skill from functioning — they enhance it. Flagged to Sage for future roadmap consideration.

---

## Scope Boundary

This skill does NOT:
- Automatically capture session state — the operator drives Step 1 manually
- Push context to the new surface automatically — context package requires manual transfer
- Replace the Session Close SOP for session closes
- Replace `/cohk` for COHK events
- Sync files between surfaces — that is GitHub's role (Step 2 pre-switch checklist)

---

## Dependencies

- Sage (steps 1–3 driven by Sage; steps 4–5 confirm continuity on arrival)
- Session Summary, project_context.md, MEMORY.md (read on arrival in Step 4)
- CLAUDE.md (auto-loaded on surface arrival)
- GitHub (pre-switch push in Step 2 when leaving for extended period)

---

## Deploy Path

```
[project root]/.claude/commands/surface-transition.md
```

---

*Built by Cosmo — Skill Creator | Item 147 | 2026-06-01*
*Source: Cross-surface handoff protocol (internal operational standard) | No external resource*
*MCP upgrade candidates identified and flagged to Sage (3 items)*
