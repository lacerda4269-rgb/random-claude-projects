# CloseOut-HouseKeeping SOP

**Owner:** Sage
**Version:** 0
**Created:** 2026-04-21
**Updated:** 2026-06-01 (Session 199)
**Status:** Active
**Future:** Convert to Cosmo skill during Master Library tasking

---

## Purpose

CloseOut-HouseKeeping (COHK) is the major milestone event that precedes every Session Summary Split (SSS). COHK is the full event — the SSS mechanical split (archiving the active Session Summary and Index, creating fresh files) is one output of COHK, not the event itself.

This SOP defines what COHK is, when it fires, and exactly how to execute it.

---

## What COHK Is

COHK is a deliberate, team-wide operational event that runs before every SSS. Its purpose: close out accumulated work, clean up all active tracking files, align the full team, and ensure the project enters its next part clean and current.

COHK is not the same as a session close or compact wrap-up — those are routine. COHK is exceptional. Every COHK is a milestone.

The mechanical split (SSS) happens at Step 17 of COHK — not before, and not instead of it.

---

## Relationship to the SSS

**COHK = the event.** The full process: scope check, 20 steps, two loop phases, Jay's all-clear, soul sync, split.

**SSS = one output.** The mechanical file operation that happens at Step 17: archiving the active Session Summary and Index, creating fresh files.

The SOP is named for the event. The split is a step inside it.

---

## Visual Workflow — Quick Reference

```
SCOPE CHECK (Pre-step)
Sage proposes → Jay approves
          │
          ▼
══════════════════════════════════════════════════════════
  PHASE 1 — Cleanup and Jay Review
══════════════════════════════════════════════════════════
  Step 1  │  Sage's Opening Sweep          ┐
  Step 2  │  LHF Formal Cleanup            ┘  (run once)
          │
  Step 3  │  Sophia Pending Changes Review  ◄────────────┐
  Step 4  │  Cross-Reference Sweep                        │
           │  [forward-only by design — Step 8 adds backward sweep]
  Step 5  │  Due Outs Collected (Steps 1–4)              │
  Step 6  │  Mini-AAR (Sophia's Pending AAR List)        │
  Step 7  │  Jay's Review + Personal LHF                 │
           │  (covers Step 5 due outs + Step 6 items)    │
          │                                               │
          │  7a │ New work found?                        │
          ├──── YES ──────────────────────────────────────┘
          │         (or queue to Sophia's pending + proceed)
         NO
          │  7b │ [SAGE CALL] Phase 1 loop: clean —
          │       no new work. Phase 1 closed. → Phase 2.
          │
          ▼
══════════════════════════════════════════════════════════
  PHASE 2 — Verification and Final Jay Review
══════════════════════════════════════════════════════════
  Step 8  │  Cross-Reference Sweep (2nd pass) ◄─────────┐
           │   → FORWARD: confirm all references exist    │
           │   → BACKWARD: confirm all existing refs accurate
  Step 9  │  Insanity Check                              │
  Step 10 │  Due Outs Collected (Steps 8–9)              │
  Step 11 │  Jay's Review                                │
          │                                               │
          ├──── New work found? ──── YES ─────────────────┘
          │
         NO  (or Jay calls Phase 2 closed)
          │
          ▼
══════════════════════════════════════════════════════════
  CLOSING SEQUENCE
══════════════════════════════════════════════════════════
  Step 12 │  Gate — Jay's All-Clear ✓
  Step 13 │  Soul Sync
  Step 14 │  project_context.md Review
  Step 15 │  Final Wrap-Up Notes
  Step 16 │  Jay's Personal Housekeeping  ← Jay confirms before proceeding
  Step 17 │  Create New Files + Archive  ← SSS Split here
  Step 18 │  GitHub Verify + Push
  Step 19 │  Continue or Done?
  Step 20 │  Branch Execution
          │
          ▼
  COHK COMPLETE ✓  │  SSS COMPLETE ✓
```

---

## Triggers

A COHK fires when one or more of the following occurs:

**1. +20 Session Milestone (Recurring)**
Every 20 sessions since the last split, Sage asks whether a split is warranted. This repeats — at 20, 40, 60 sessions, and so on. Jay decides. Sage never forces the split.

**2. Version Update (Hard Rule)**
Any project version change (v0 → v1, v1 → v2, etc.) triggers an automatic COHK. No exception. If Jay does not initiate it, Sage flags it and the version change does not proceed without the COHK first.

**3. Operator Decision**
Jay may call a COHK at any time for any reason. No trigger required.

**Rule:** If two or more triggers fire at the same time — one COHK covers all of them, not two.

---

## Naming Convention

| File | Active (always) | Archived |
|---|---|---|
| Session Summary | `Session Summary.md` | `Session Summary — vN.md` |
| Session Summary Index | `Session Summary Index.md` | `Session Summary Index — vN.md` |

The active file always carries no prefix or suffix. Archived versions get `— vN` appended. N starts at 0 for the first archive and increments by 1 at each subsequent COHK. Both files stay in their existing location — no subfolder.

**Legacy naming note:** Any project with prior archives using the `— Part N` convention should rename them to the appropriate `— vN` at the first COHK run under this SOP — Part 1 → v0, Part 2 → v1, and so on. One naming convention, no mixed legacy. Applied in the Initial Package Project during COHK 3 (2026-04-30).

---

## Minor and Major Fixes

Two fix classifications apply throughout COHK — referenced at Steps 1, 2, 3, 4, 6, 8, and 9.

**Minor fix (handle now):** Self-contained correction, under 5 minutes, no Jay input required, does not affect any other step or agent's work, reversible without Jay's approval if wrong. *Examples: stale date in a header, broken link, version number bump.*

**Major fix (flag as due out):** Anything that requires Jay's decision, changes scope or direction, touches multiple files in non-obvious ways, could be wrong without more information, cannot be undone without Jay's approval — or requires a file, folder, or subfolder to be renamed (A → B). Version bumps do not count as renames.

**Minor fix execution — when a minor fix is identified at any step:**

1. Apply the correction directly.
2. Paired file check — does this correction affect any other file (cross-reference, version number, header, index entry)? If yes, apply those corrections now.
3. Verify the fix is complete and correct before moving on.

Done signal: the correction is applied, paired files are clean, and work continues. No flag, no queue, no Jay input. Minor fixes do not interrupt the flow of the step in progress.

Major fixes found in Phase 1 (Steps 1–4) surface as due outs at Step 5. Major fixes found in Phase 2 (Steps 8–9) surface as due outs at Step 10.

---

## COHK Steps

### Scope Check (before Step 1)

Sage reviews the current project state and proposes a scope list to Jay. Jay reviews and approves, adjusts, or adds items. A zero-item scope is a valid COHK. Scope items are worked through as part of the steps below — not as a separate phase.

**Pre-overhaul inventory (applies when scope includes a structural overhaul):** Before any major structural overhaul phase begins, Sophia produces a pre-overhaul nested tree inventory snapshot of the current project structure. Saved to `4. Project Artifacts/` as a dated reference document — this is Phase 4's starting point. Fire this step during scope confirmation, before overhaul execution begins. (Item 141)

---

### Phase 1 — Cleanup and Jay Review (Steps 1–7)

**Phase 1 loop:** After Step 7, Sage evaluates whether Jay's review generated new work. If yes — loop back to Step 3 and repeat Steps 3–7. Jay may alternatively direct new items to Sophia's pending list and proceed without looping. If clean — Phase 1 closed; proceed to Phase 2.

**Jay's override:** Jay reserves the right to call Phase 1 closed at any time and proceed to Phase 2, regardless of outstanding items.

---

#### Step 1 — Sage's Opening Sweep

Sage scans the full project state before any structured checks begin: gaps, missing captures, stale items, anything that should be on the LHF list but isn't, and any implicit tasks or decisions from recent sessions not yet recorded permanently. This is the diagnostic pass — surfaces raw material for the steps that follow.

**What to read for this step:**
- `Session Summary.md` — most recent session only. Find the last `## Session N` header and read from there to the end of that section. Do not read the full history or archived parts.
- `Session Summary Index.md` — spot check only: confirm the index is current through the last session. No full read required.
- All current state files: LHF, `project_context.md`, `Sage-project-soul.md`, Sophia's Pending Changes, and any other active project tracking files.

**Reading scope rule:** If it mattered, it was captured permanently in the living files. Historical session entries are not needed for a COHK diagnostic — the current state files hold everything relevant.

**Minor and Major fix rule:** Minor fixes resolved on the spot. Major fixes flagged as due outs for Step 5.

**Note — future splits for current state files:** If any current state file (project_context.md, LHF, Sophia's Pending Changes, etc.) ever grows unwieldy, apply the same split logic used for the Session Summary: archive the old version, keep only the active file in the standard read path. No design work needed now — flag it when it happens.

#### Step 2 — LHF Formal Cleanup

Agent-led cleanup of the Low Hanging Fruit list. Jay's personal LHF section is excluded — Jay handles that in Step 7.

**Before Step 2 begins — auto-compaction safeguard:** Sophia creates a dedicated temp file: `COHK-[N]-Step2-Tracker.md`. This file lists every LHF item in scope with its assigned agent, target disposition, and current status. It is the recovery point if auto-compaction fires mid-cleanup — the team opens this file on return and resumes exactly where they left off. The tracker is deleted when Step 2 closes clean.

**Execution model:**
- **Sage assigns** each LHF item to the correct agent based on their domain. Sage decides which items need Jay's call (those become due outs for Step 5). No agent acts on another agent's items without Sage's direction.
- **Sophia tracks** all assignments, dispositions, and completion status in the tracker file. She reports progress to Sage and ensures nothing is missed.
- **Agents execute** their assigned items: close completed items, retire stale ones, update statuses, consciously defer anything not ready to close.
- Items requiring Jay's decision are flagged as due outs and not acted on.

**Goal:** Every LHF item has a disposition before Step 2 closes — finished, updated, consciously deferred, or flagged as a Jay due out.

**Minor and Major fix rule:** Minor fixes resolved on the spot. Major fixes flagged as due outs for Step 5.

#### Step 3 — Sophia Pending Changes Review

Sophia reviews her Pending Changes list. Minor items closed on the spot. Stale or resolved items retired. Open questions raised and answered where possible. Any items surfaced by Sage's opening sweep that belong on the list are added here before Sophia's review runs.

**Minor and Major fix rule:** Minor fixes resolved on the spot. Major fixes flagged as due outs for Step 5.

*Note: Sophia also runs a standing 5-session review cadence — the COHK review is an additional trigger, independent of that cadence.*

#### Step 4 — Cross-Reference Sweep

Full forward sweep across all project files: souls, SOPs, MGs, index cards, tracking files. Runs after Steps 1–3 because those generate the changes — this sweep catches everything in one pass.

**Design note — forward-only by intent:** This step runs one direction only. The backward sweep (reverse — confirm all existing references are accurate) belongs in Phase 2 at Step 8, where it runs after Jay's Phase 1 review has finalized any remaining changes. Forward here; both directions in Step 8.

**Minor and Major fix rule:** Minor fixes resolved on the spot. Major fixes flagged as due outs for Step 5.

#### Step 5 — Due Outs for Steps 1–4

Sage collects all items from Steps 1–4 that require Jay's input and presents them as a single organized list. This is a structured briefing, not an open-ended review. Jay works through the list once in Step 7 — no piecemeal interruptions during Phase 1 prep work.

**LHF-soul gap check:** Before presenting the due outs list to Jay, confirm: did any LHF change made in Step 2 alter planned work order or scope? If yes — run a follow-up soul check on the Objectives table (Sage-project-soul.md) and resolve any discrepancy before Step 7 begins.

#### Step 6 — Mini-AAR: Sophia's Pending AAR Review

Review Sophia's pending AAR list item by item. By this point in COHK, Steps 2 and 3 have already run — the list should be lean and relatively current.

**Execution model:**
- Sage and Sophia work through the pending AAR list together — one item at a time.
- **Minor items:** action on the spot.
- **Major items:** flag as a due out for Step 7.
- **Stale or resolved items:** retire.

**Intent:** This step is designed to be quick when the list is current — thorough when it needs to be. Depth is item-dependent, not fixed. The goal is to enter Jay's review in Step 7 with the AAR list as clean as possible.

**Minor and Major fix rule:** Minor fixes resolved on the spot. Major fixes flagged as due outs for Step 7.

*Note: This step runs at every COHK regardless of whether any project has reached completion. It is the deliberate full-pass review of the pending AAR list.*

#### Step 7 — Jay's Review / Actions / Notes / Personal LHF Pass

Jay works through the due outs from **Step 5** and any items flagged from **Step 6 (Mini-AAR)**. Jay handles his personal LHF section and makes any observations or updates only he can make. Sage reads Jay's notes, shares her perspective where useful, and captures anything that changes project state. Any agent affected by Jay's decisions is briefed by Sage before Phase 1 loops or closes.

**After Step 7:**

**Step 7a — Loop check:** Was new work found?
- **YES** → loop back to Step 3. Repeat Steps 3–7. *(Jay may alternatively direct new items to Sophia's pending list and proceed without looping.)*
- **NO** → proceed to Step 7b.

**Step 7b — Phase 1 authorization:** Sage states explicitly: *"Phase 1 loop check: clean — no new work generated. Phase 1 closed. Proceeding to Phase 2."* Sage is authorized to make this call.

- Jay may call Phase 1 closed at any time regardless of outstanding items.

---

### Phase 2 — Verification and Final Jay Review (Steps 8–11)

**Phase 2 loop:** After Step 11, Sage evaluates whether Jay's review generated new work. If yes — loop back to Step 8 and repeat Steps 8–11. If clean — Phase 2 closed; proceed to Step 12.

**Jay's override:** Jay reserves the right to call Phase 2 closed at any time and proceed to Step 12, regardless of outstanding items.

---

#### Step 8 — Cross-Reference Sweep (Second Pass)

Full sweep — both directions. Runs after Jay's Phase 1 review (Step 7) because Jay's actions in Step 7 can create new changes that the Step 4 sweep did not see.

**→ FORWARD SWEEP (Pointer Scan):** Confirm all references that should exist do — every soul, SOP, MG, and index card points to the right target.

**→ BACKWARD SWEEP (Reverse Scan):** Confirm all existing references are accurate — every target file is still where it's referenced, at the correct version, with the correct name. No reference points to a renamed, moved, or deleted resource.

**Minor and Major fix rule:** Minor fixes resolved on the spot. Major fixes flagged as due outs for Step 10.

#### Step 9 — Insanity Check

A light review pass for anything that does not surface in the structured checks above. May be skipped if nothing surfaces. May also surface new future projects or quick open/close items that should be captured before the split.

**Standing check — Mermaid CLI version (Item 129):** At every COHK, check whether mermaid-cli has published an update bundling mermaid 11.15.0 or higher. The current LHF HOLD on mermaid-cli is waiting for exactly this version. Check the mermaid-cli release page (npmjs.com/package/@mermaid-js/mermaid-cli) — if mermaid 11.15.0+ is bundled, the HOLD is ready to clear (route to Rose for a standard update report → Soren clearance → Lexi cataloging). If not, note the check was run and move on. Takes under 2 minutes.

**Minor and Major fix rule:** Minor fixes resolved on the spot. Major fixes flagged as due outs for Step 10.

#### Step 10 — Due Outs for Steps 8–9

Sage collects all items from Steps 8–9 that require Jay's input and presents them as a single organized list. Jay works through the list once in Step 11.

#### Step 11 — Jay's Review / Actions / Notes

Jay works through the due outs from Step 10. Sage captures anything that changes project state and briefs any affected agent.

**After Step 11:**
- If Jay's review generated new work → loop back to Step 8. Repeat Steps 8–11.
- If Jay's review is clean → Phase 2 closed. Proceed to Step 12.
- Jay may call Phase 2 closed at any time regardless of outstanding items.

---

### Closing Sequence (Steps 12–20)

---

#### Step 12 — Gate: Jay's All-Clear

**This is the gate. No mechanical steps begin without Jay's signal here.**

Jay reviews the state of COHK and gives one of two signals:

- **Green — proceed:** COHK is in "good enough" shape. All critical items addressed; anything remaining is consciously deferred. Proceed to Step 13.
- **Not ready — pause:** Something needs more time, a decision, or further work. COHK pauses here. Project continues as normal until Jay is ready to resume.

#### Step 13 — Soul Sync

Verify `Sage-project-soul.md` is current. If project direction, scope, roster, or objectives shifted this COHK, the soul must reflect it before the new part starts. Bump the version and log the change.

#### Step 14 — project_context.md Review

Review and update `project_context.md`. Must be clean and current before the new part begins. Confirm the pipeline, current state, and "what comes next" are all accurate.

#### Step 15 — Final Wrap-Up and Closing Notes

Write the final session close entry into the current `Session Summary.md` and update `Session Summary Index.md`. This is the last content captured before the files are archived — the closing record of this part.

#### Step 16 — Jay's Personal Housekeeping

Sage prompts Jay to complete any personal last-minute housekeeping — personal notes, personal project folder, or any personal files that need to be saved or closed before the commit. This is Jay's lane; Sage does not touch these files.

Jay confirms "all set" (or equivalent) before the sequence continues.

#### Step 17 — Create New Files + Archive (the SSS Mechanical Split)

**This is where the SSS executes. Step 12 is the gate — Step 17 is the split. These are distinct steps.**

Executed in this order:

1. **Create** — Sage and Sophia create any last-minute files, folders, or subfolders needed for the next part to start clean.
2. **Archive** — Rename `Session Summary.md` → `Session Summary — vN.md`; rename `Session Summary Index.md` → `Session Summary Index — vN.md`.
3. **Create fresh files** — Create a new `Session Summary.md` and a new `Session Summary Index.md`. Capture first notes in both: date, session number, reason for split, version number. Include a pointer in the new Index back to `Session Summary Index — vN.md` for historical lookups.

Both archived files and both new files stay in their existing location — no subfolder.

**CQC-02 note:** No Session Summary archive subfolder is pre-built in the MIP. Archived files (`Session Summary — vN.md`) accumulate in the same `1. Session Summary/` folder alongside the active files. The `— vN` naming convention handles disambiguation — no subfolder needed. The archive subfolder pattern (if ever needed) would appear at the first COHK, not at project start. (CQC-02, Session 196)

#### Step 18 — GitHub Verify + Push

Commit all changes — project files, soul sync, session summary files (archived + new), and Jay's personal notes. Push to GitHub.

Run `git status`. Working tree must be clean — zero modified, zero untracked files that should be committed.

Confirm: *"All changes pushed. Working tree clean."*

#### Step 19 — Continue or Done?

Sage asks Jay directly: "Are you planning to continue working or are you done for now?"

#### Step 20 — Branch Execution

- **Continue** — Fresh Session Summary and Index are already live from Step 17. No additional action required — work proceeds. COHK is officially retired.
- **Done** — COHK is officially retired. Session is closed. Jay returns when ready.

**COHK COMPLETE ✓  |  SSS COMPLETE ✓**

---

## Cross-References

- Session Close SOP and Compact Wrap-Up SOP → point here for COHK procedures
- Both Master Guides → reference this SOP for COHK triggers and process
- `feedback_summary_split_rule.md` → this SOP is the source of truth

*Note: Cross-references to the prior filename (Session-Summary-Split-SOP.md) updated inline — Session 99.*

---

