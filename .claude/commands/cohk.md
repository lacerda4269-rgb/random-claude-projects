# COHK — CloseOut-HouseKeeping Navigator Skill

**Skill name:** `/cohk`
**Built by:** Cosmo (Skill Creator)
**Source:** Internal — converted from CloseOut-HouseKeeping SOP v5.4
**Soren status:** CLEARED (internal build — no external resource)
**Version:** 0
**Built:** 2026-06-01
**Cataloged section:** 3 — Skills | Tier 1
**Item:** 123

---

## What It Does

Step-by-step navigator for the CloseOut-HouseKeeping (COHK) sequence. Displays each step of the COHK process, confirms completion before advancing, and tracks loop state across Phase 1 and Phase 2. Guides Sage through the full 20-step sequence from Scope Check through Branch Execution.

This skill is a navigation and checklist layer only. It does NOT execute step content — that requires Sage's judgment and agent coordination. It keeps the sequence visible, ordered, and confirmed-complete at each gate.

---

## Invocation

```
/cohk
```

Optional modifiers:

```
/cohk start          → begin from Scope Check (default)
/cohk phase2         → jump to Phase 2 (Step 8) — use only when Phase 1 is already confirmed closed
/cohk closing        → jump to Closing Sequence (Step 12) — use only when Phase 2 is confirmed closed
/cohk step N         → jump to a specific step number — use for resuming after interruption
```

---

## COHK Structure — Full Sequence

When invoked, display the current step with its description and a confirmation prompt before advancing. Track which phase is active. Honor loop logic at Steps 7 and 11.

---

### PRE-STEP — Scope Check

**Display:**

```
╔══════════════════════════════════════════════════════╗
║  COHK NAVIGATOR — Scope Check (Pre-Step)            ║
╚══════════════════════════════════════════════════════╝

Before Step 1 begins: Sage proposes a scope list to Jay.
Jay reviews and approves, adjusts, or adds items.
A zero-item scope is a valid COHK.

Scope items are worked through as part of the steps below —
not as a separate phase.

SPECIAL NOTE — Structural Overhaul in Scope:
If scope includes a major structural overhaul, Sophia must
produce a pre-overhaul nested tree inventory snapshot BEFORE
overhaul execution begins. Save to: 4. Project Artifacts/
(dated reference). This is Phase 4's starting point.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Scope confirmed with Jay? (y to proceed to Phase 1)
```

---

### PHASE 1 — Cleanup and Jay Review (Steps 1–7)

**Phase 1 Loop Rule:** After Step 7, if new work was found → loop back to Step 3 and repeat Steps 3–7. Jay may alternatively queue new items to Sophia's pending list and proceed. If clean → Phase 1 closed, proceed to Phase 2.

**Jay's override:** Jay may call Phase 1 closed at any time.

---

**Step 1 — Sage's Opening Sweep**

```
╔══════════════════════════════════════════════════════╗
║  PHASE 1 | Step 1 — Sage's Opening Sweep            ║
╚══════════════════════════════════════════════════════╝

Sage scans the full project state — gaps, missing captures,
stale items, implicit tasks from recent sessions not yet
permanently recorded.

READ for this step:
  → Session Summary.md — most recent session only
    (find last ## Session N header; read to end of that section)
  → Session Summary Index.md — spot check only (current through last session)
  → All current state files: LHF, project_context.md,
    Sage-project-soul.md, Sophia's Pending Changes, other
    active tracking files

Minor fixes: resolve on the spot.
Major fixes: flag as due outs for Step 5.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Step 1 complete? (y to advance to Step 2)
```

---

**Step 2 — LHF Formal Cleanup**

```
╔══════════════════════════════════════════════════════╗
║  PHASE 1 | Step 2 — LHF Formal Cleanup              ║
╚══════════════════════════════════════════════════════╝

Agent-led cleanup of the Low Hanging Fruit list.
Jay's personal LHF section is excluded — Jay handles that in Step 7.

FIRST ACTION: Sophia creates COHK-[N]-Step2-Tracker.md
(auto-compaction safeguard — recovery point if context resets mid-cleanup).
Delete this file when Step 2 closes clean.

Execution model:
  → Sage assigns each LHF item to the correct agent
  → Items requiring Jay's call → flagged as due outs for Step 5
  → Sophia tracks all assignments, dispositions, completion status
  → Agents execute: close completed, retire stale, defer consciously

GOAL: Every LHF item has a disposition before Step 2 closes.

Minor fixes: resolve on the spot.
Major fixes: flag as due outs for Step 5.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Step 2 complete? (y to advance to Step 3)
```

---

**Step 3 — Sophia Pending Changes Review**

```
╔══════════════════════════════════════════════════════╗
║  PHASE 1 | Step 3 — Sophia Pending Changes Review   ║
╚══════════════════════════════════════════════════════╝

Sophia reviews her Pending Changes list.
  → Minor items: closed on the spot
  → Stale or resolved items: retired
  → Open questions: raised and answered where possible
  → Items surfaced by Sage's opening sweep that belong on
    the list: added here before Sophia's review runs

Note: Sophia also runs a standing 5-session review cadence —
this COHK review is an additional trigger, independent.

Minor fixes: resolve on the spot.
Major fixes: flag as due outs for Step 5.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Step 3 complete? (y to advance to Step 4)
```

---

**Step 4 — Cross-Reference Sweep (Forward Only)**

```
╔══════════════════════════════════════════════════════╗
║  PHASE 1 | Step 4 — Cross-Reference Sweep           ║
║  (Forward direction only — backward sweep at Step 8) ║
╚══════════════════════════════════════════════════════╝

Full FORWARD sweep across all project files: souls, SOPs,
MGs, index cards, tracking files.

FORWARD SWEEP: Confirm all references that should exist do —
every soul, SOP, MG, and index card points to the right target.

Runs after Steps 1–3 because those generate the changes —
this sweep catches everything in one pass.

Design note: Backward sweep belongs at Step 8 — after Jay's
Phase 1 review has finalized any remaining changes.

Minor fixes: resolve on the spot.
Major fixes: flag as due outs for Step 5.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Step 4 complete? (y to advance to Step 5)
```

---

**Step 5 — Due Outs Collected (Steps 1–4)**

```
╔══════════════════════════════════════════════════════╗
║  PHASE 1 | Step 5 — Due Outs Collected (Steps 1–4)  ║
╚══════════════════════════════════════════════════════╝

Sage collects all items from Steps 1–4 that require Jay's input.
Present as a single organized list — structured briefing,
not open-ended review.

LHF-SOUL GAP CHECK (before presenting to Jay):
Did any LHF change in Step 2 alter planned work order or scope?
If YES → run a follow-up soul check on the Objectives table
(Sage-project-soul.md) and resolve any discrepancy before Step 7.

Jay works through the list once in Step 7.
No piecemeal interruptions during Phase 1 prep.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Due outs list ready for Step 7? (y to advance to Step 6)
```

---

**Step 6 — Mini-AAR (Sophia's Pending AAR Review)**

```
╔══════════════════════════════════════════════════════╗
║  PHASE 1 | Step 6 — Mini-AAR                        ║
╚══════════════════════════════════════════════════════╝

Sage and Sophia work through the pending AAR list together —
one item at a time.

  → Minor items: action on the spot
  → Major items: flag as due out for Step 7
  → Stale or resolved items: retire

Runs at every COHK regardless of whether any project has
reached completion. Goal: enter Jay's review (Step 7)
with the AAR list as clean as possible.

Minor fixes: resolve on the spot.
Major fixes: flag as due outs for Step 7.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Mini-AAR complete? (y to advance to Step 7)
```

---

**Step 7 — Jay's Review / Actions / Notes / Personal LHF**

```
╔══════════════════════════════════════════════════════╗
║  PHASE 1 | Step 7 — Jay's Review                    ║
╚══════════════════════════════════════════════════════╝

Jay works through due outs from Step 5 and flagged items
from Step 6 (Mini-AAR). Jay handles personal LHF section.

Sage reads Jay's notes, shares perspective where useful,
and captures anything that changes project state.

Any agent affected by Jay's decisions is briefed by Sage
before Phase 1 loops or closes.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
AFTER STEP 7 — LOOP CHECK (Step 7a):

Was new work found?

  y = YES — new work found
      Options:
        (a) Loop back to Step 3 and repeat Steps 3–7
        (b) Queue new items to Sophia's pending + proceed to Phase 2
      Jay decides which path.

  n = NO — Phase 1 clean
      → Sage states: "Phase 1 loop check: clean — no new work
        generated. Phase 1 closed. Proceeding to Phase 2."
      Sage is authorized to make this call.

  o = JAY OVERRIDE — Jay calls Phase 1 closed regardless of
      outstanding items. Proceed to Phase 2.

New work found? (y/n/o)
```

---

### PHASE 2 — Verification and Final Jay Review (Steps 8–11)

**Phase 2 Loop Rule:** After Step 11, if new work was found → loop back to Step 8 and repeat Steps 8–11. If clean → Phase 2 closed, proceed to Step 12.

**Jay's override:** Jay may call Phase 2 closed at any time.

---

**Step 8 — Cross-Reference Sweep (Second Pass — Both Directions)**

```
╔══════════════════════════════════════════════════════╗
║  PHASE 2 | Step 8 — Cross-Reference Sweep (2nd Pass)║
║  BOTH DIRECTIONS                                     ║
╚══════════════════════════════════════════════════════╝

Runs after Jay's Phase 1 review (Step 7) — Jay's actions
in Step 7 can create new changes Step 4 did not see.

→ FORWARD SWEEP (Pointer Scan):
  Confirm all references that should exist do — every soul,
  SOP, MG, and index card points to the right target.

→ BACKWARD SWEEP (Reverse Scan):
  Confirm all existing references are accurate — every target
  file is still where it's referenced, at the correct version,
  with the correct name. No reference points to a renamed,
  moved, or deleted resource.

Minor fixes: resolve on the spot.
Major fixes: flag as due outs for Step 10.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Step 8 complete? (y to advance to Step 9)
```

---

**Step 9 — Insanity Check**

```
╔══════════════════════════════════════════════════════╗
║  PHASE 2 | Step 9 — Insanity Check                  ║
╚══════════════════════════════════════════════════════╝

Light review pass for anything that does not surface in
the structured checks above. May be skipped if nothing
surfaces. May also surface new future projects or quick
open/close items that should be captured before the split.

Minor fixes: resolve on the spot.
Major fixes: flag as due outs for Step 10.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Step 9 complete? (y to advance to Step 10)
```

---

**Step 10 — Due Outs Collected (Steps 8–9)**

```
╔══════════════════════════════════════════════════════╗
║  PHASE 2 | Step 10 — Due Outs Collected (Steps 8–9) ║
╚══════════════════════════════════════════════════════╝

Sage collects all items from Steps 8–9 that require Jay's
input and presents them as a single organized list.
Jay works through the list once in Step 11.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Due outs list ready for Step 11? (y to advance to Step 11)
```

---

**Step 11 — Jay's Review / Actions / Notes**

```
╔══════════════════════════════════════════════════════╗
║  PHASE 2 | Step 11 — Jay's Review                   ║
╚══════════════════════════════════════════════════════╝

Jay works through due outs from Step 10.
Sage captures anything that changes project state and
briefs any affected agent.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
AFTER STEP 11 — LOOP CHECK:

New work found?

  y = YES — loop back to Step 8, repeat Steps 8–11
  n = NO — Phase 2 clean, proceed to Step 12
  o = JAY OVERRIDE — Jay calls Phase 2 closed, proceed to Step 12

New work found? (y/n/o)
```

---

### CLOSING SEQUENCE (Steps 12–20)

---

**Step 12 — Gate: Jay's All-Clear**

```
╔══════════════════════════════════════════════════════╗
║  CLOSING SEQUENCE | Step 12 — Jay's All-Clear        ║
║  *** THIS IS THE GATE — NO MECHANICAL STEPS BEGIN   ║
║      WITHOUT JAY'S SIGNAL HERE ***                   ║
╚══════════════════════════════════════════════════════╝

Jay reviews the state of COHK and gives one of two signals:

  g = GREEN — proceed: COHK is in "good enough" shape.
      All critical items addressed; anything remaining is
      consciously deferred. Proceed to Step 13.

  p = PAUSE — not ready: Something needs more time,
      a decision, or further work. COHK pauses here.
      Project continues as normal until Jay is ready to resume.

Jay's signal? (g/p)
```

---

**Step 13 — Soul Sync**

```
╔══════════════════════════════════════════════════════╗
║  CLOSING SEQUENCE | Step 13 — Soul Sync             ║
╚══════════════════════════════════════════════════════╝

Verify Sage-project-soul.md is current.

If project direction, scope, roster, or objectives shifted
this COHK → the soul must reflect it before the new part starts.
Bump the version and log the change.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Soul Sync complete? (y to advance to Step 14)
```

---

**Step 14 — project_context.md Review**

```
╔══════════════════════════════════════════════════════╗
║  CLOSING SEQUENCE | Step 14 — project_context Review ║
╚══════════════════════════════════════════════════════╝

Review and update project_context.md.
Must be clean and current before the new part begins.

Confirm the pipeline, current state, and "what comes next"
are all accurate.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
project_context.md complete? (y to advance to Step 15)
```

---

**Step 15 — Final Wrap-Up Notes**

```
╔══════════════════════════════════════════════════════╗
║  CLOSING SEQUENCE | Step 15 — Final Wrap-Up Notes   ║
╚══════════════════════════════════════════════════════╝

Write the final session close entry into the current
Session Summary.md and update Session Summary Index.md.

This is the LAST CONTENT captured before the files are archived —
the closing record of this part.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Final wrap-up notes complete? (y to advance to Step 16)
```

---

**Step 16 — Jay's Personal Housekeeping**

```
╔══════════════════════════════════════════════════════╗
║  CLOSING SEQUENCE | Step 16 — Jay's Personal HK     ║
╚══════════════════════════════════════════════════════╝

Sage prompts Jay to complete any personal last-minute
housekeeping — personal notes, personal project folder,
or any personal files that need to be saved or closed.

THIS IS JAY'S LANE. Sage does not touch these files.

Jay confirms "all set" (or equivalent) before proceeding.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Jay confirmed all set? (y to advance to Step 17)
```

---

**Step 17 — Create New Files + Archive (the SSS Mechanical Split)**

```
╔══════════════════════════════════════════════════════╗
║  CLOSING SEQUENCE | Step 17 — SSS Mechanical Split  ║
║  *** STEP 12 IS THE GATE. STEP 17 IS THE SPLIT. *** ║
║  THESE ARE DISTINCT STEPS.                          ║
╚══════════════════════════════════════════════════════╝

Execute in this order:

  1. CREATE — Sage and Sophia create any last-minute files,
     folders, or subfolders needed for the next part to
     start clean.

  2. ARCHIVE — Rename:
       Session Summary.md → Session Summary — vN.md
       Session Summary Index.md → Session Summary Index — vN.md
     (N starts at 0 for the first archive; increments by 1 each COHK)

  3. CREATE FRESH FILES — Create new Session Summary.md and
     Session Summary Index.md. Capture first notes in both:
     date, session number, reason for split, version number.
     Include a pointer in the new Index back to
     Session Summary Index — vN.md for historical lookups.

NAMING NOTE: Active file always carries NO prefix or suffix.
Archived versions get — vN appended. No subfolder needed —
archived files accumulate in the same folder as active files.
The vN naming handles disambiguation.

LEGACY: If prior archives use — Part N convention, rename
to vN at first COHK under this SOP: Part 1 → v0, Part 2 → v1.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SSS split complete? (y to advance to Step 18)
```

---

**Step 18 — GitHub Verify + Push**

```
╔══════════════════════════════════════════════════════╗
║  CLOSING SEQUENCE | Step 18 — GitHub Verify + Push  ║
╚══════════════════════════════════════════════════════╝

Commit all changes — project files, soul sync, session
summary files (archived + new), and Jay's personal notes.
Push to GitHub.

Run: git status
Working tree must be clean — zero modified, zero untracked
files that should be committed.

Confirm: "All changes pushed. Working tree clean."

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
GitHub push confirmed and working tree clean? (y to advance to Step 19)
```

---

**Step 19 — Continue or Done?**

```
╔══════════════════════════════════════════════════════╗
║  CLOSING SEQUENCE | Step 19 — Continue or Done?     ║
╚══════════════════════════════════════════════════════╝

Sage asks Jay directly:
"Are you planning to continue working or are you done for now?"

  c = CONTINUE → proceed to Step 20 (Branch: Continue)
  d = DONE → proceed to Step 20 (Branch: Done)

Jay's answer? (c/d)
```

---

**Step 20 — Branch Execution**

```
╔══════════════════════════════════════════════════════╗
║  CLOSING SEQUENCE | Step 20 — Branch Execution      ║
╚══════════════════════════════════════════════════════╝

CONTINUE branch:
  Fresh Session Summary and Index are already live from Step 17.
  No additional action required. Work proceeds.
  COHK is officially retired.

DONE branch:
  COHK is officially retired. Session is closed.
  Jay returns when ready.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  ██████╗ ██████╗ ██╗  ██╗██╗  ██╗     ██████╗ ██████╗ ███╗   ███╗██████╗ ██╗     ███████╗████████╗███████╗ ██╗
 ██╔════╝██╔═══██╗██║  ██║██║ ██╔╝    ██╔════╝██╔═══██╗████╗ ████║██╔══██╗██║     ██╔════╝╚══██╔══╝██╔════╝ ██║
 ██║     ██║   ██║███████║█████╔╝     ██║     ██║   ██║██╔████╔██║██████╔╝██║     █████╗     ██║   █████╗   ██║
 ██║     ██║   ██║██╔══██║██╔═██╗     ██║     ██║   ██║██║╚██╔╝██║██╔═══╝ ██║     ██╔══╝     ██║   ██╔══╝   ╚═╝
 ╚██████╗╚██████╔╝██║  ██║██║  ██╗    ╚██████╗╚██████╔╝██║ ╚═╝ ██║██║     ███████╗███████╗   ██║   ███████╗ ██╗
  ╚═════╝ ╚═════╝ ╚═╝  ╚═╝╚═╝  ╚═╝    ╚═════╝ ╚═════╝ ╚═╝     ╚═╝╚═╝     ╚══════╝╚══════╝   ╚═╝   ╚══════╝ ╚═╝

  COHK COMPLETE ✓  |  SSS COMPLETE ✓
```

---

## COHK Triggers — Quick Reference

| Trigger | Rule |
|---------|------|
| +20 Session Milestone | Recurring — Sage asks at 20, 40, 60, etc. sessions since last split. Jay decides. |
| Version Update | Hard rule — any version change (v0→v1, v1→v2, etc.) triggers automatic COHK. No exception. |
| Operator Decision | Jay may call a COHK at any time for any reason. |
| Multiple triggers | One COHK covers all — never two for the same event. |

---

## Minor vs. Major Fix — Quick Reference

| Fix Type | What It Is | How to Handle |
|----------|------------|---------------|
| **Minor** | Self-contained, under 5 min, no Jay input, reversible without Jay approval. *Examples: stale date, broken link, version number bump.* | Apply directly → paired file check → verify. No flag, no queue. |
| **Major** | Requires Jay's decision, changes scope/direction, touches multiple files non-obviously, could be wrong without more info, irreversible without Jay approval, or requires rename (A→B). | Flag as due out for Step 5 (Phase 1) or Step 10 (Phase 2). |

---

## Scope Boundary

This skill does NOT:
- Execute any COHK step content — that is Sage's and the agents' work
- Auto-perform sweeps, cleanups, or file operations
- Replace the CloseOut-HouseKeeping SOP — this is the navigation layer above it
- Make decisions on loop exits (Sage calls Phase 1 and Phase 2 closure)

---

## Dependencies

- CloseOut-HouseKeeping SOP v5.4 (source of truth for all step content)
- Sage (Step 7 and Step 11 loop decisions, Phase 1/2 closure calls)
- Jay (all review and approval gates)
- Sophia (Step 2 tracker file, Step 3 pending changes, Step 6 Mini-AAR)

---

## Deploy Path

```
[project root]/.claude/commands/cohk.md
```

---

*Built by Cosmo — Skill Creator | Item 123 | 2026-06-01*
*Source: CloseOut-HouseKeeping SOP v5.4 (internal) | No external resource*
