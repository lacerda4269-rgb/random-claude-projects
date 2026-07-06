# Feynman-Session-Management-SOP

**Version:** 0
**Created:** 2026-05-18
**Session:** 158
**Paired with:** Feynman-Session-Management-SOP-Jay.md (Jay's plain-language version)
**Status:** Active
**HR13 Pair:** Feynman-Session-Management-SOP.md + Feynman-Session-Management-SOP-Jay.md

---

## Purpose

This SOP governs all session management for a [long-term academic project]: the structure and location of session records, the [program] Lessons Log (cross-unit lessons log), session open and close procedures, [unit] setup, and [unit] close-out. It replaces the TEMPORARY session close triggers previously held in Feynman-Scholar-SOP.md, Feynman-Scholar-SOP-Jay.md, and feynman-academic-project-map.md.

---

## Core Architecture

A [long-term academic project] uses a three-layer session management system.

**Layer 1 — Per-[unit] session summaries**
Each [unit] maintains its own session record. Files live in the [unit]'s support doc folder.

Naming standard:
- `[course-code]-Session-Summary.md`
- `[course-code]-Session-Summary-Index.md`

Example: `[course-code]-Session-Summary.md` + `[course-code]-Session-Summary-Index.md` in `[Unit] - Support Doc Folder - PM Lead\[course-code]-Session-Summary\`

These files are [unit]-scoped. They record what was worked in each session for that [unit] only.

**Layer 2 — [Program] Lessons Log**
A single project-wide file that accumulates cross-[unit] lessons and insights. Lives in `[Feynman P/M Lead Folder]\[Program] Lessons Log.md`. Updated selectively — only when an entry meets the transfer threshold (see [Program] Lessons Log section below).

**Layer 3 — Master Outcomes Log**
A single project-wide file that records outcomes for every completed [unit]. Lives in `[Feynman P/M Lead Folder]\Master-Outcomes-Log.md`. One entry per completed [unit], added at [unit] close-out. Entry format: [unit] code + name, [term] dates, credits/weight, key deliverables (brief list), final grade/result, C&P outcomes (what the [student/operator] came away knowing or able to do — concise and precise, not a one-liner), [Program] Lessons Log pointers (or "None"). This file does not close until the [student/operator]'s final [unit] result is recorded.

**One-[unit] rule:** The [student/operator] works one [unit] at a time. There is never more than one active [unit] in a session.

---

## [Unit] Setup Step

At COURSESTART ([student/operator] says go), before the first session entry is written:

1. Confirm the [unit] folder exists at `[project]\[Unit Folder]\`
2. Confirm the support doc folder exists at `[Unit Folder]\[course-code] - Support Doc Folder\`
3. Create `[course-code]-Session-Summary.md` in the support doc folder — use the header format defined in the Session Summary Entry Format section below
4. Create `[course-code]-Session-Summary-Index.md` in the support doc folder — paired with the summary
5. This step is part of the [Unit] Activation Process (CM-1 through CM-7) defined in feynman-academic-project-map.md

Do not create these files on the fly mid-session. Setup happens at COURSESTART, not at first use.

---

## Session Open Procedure

At the start of every Feynman session:

1. The [student/operator] names the active [unit] (or it is clear from context)
2. Feynman runs the gate check for that [unit] only — "Any [unit] updates this week?"
   - **No (nothing new):** Color-only pass — recalculate time-remaining % for all deliverables; update Structure Map - Visual Tracker if any thresholds crossed; Weekly Trackers unchanged
   - **Yes ([unit] updates):** Full pass — update future Weekly Trackers from the [student/operator]'s input, then recalculate % and deliver rebuilt map
3. Color recalculation always runs regardless of gate answer — time passing alone can shift thresholds

---

## Color Status Update Protocol

Two rules govern color status changes during the weekly gate check and color pass.

**Submission notification — Green override:**
When the [student/operator] submits an assignment, they notify Feynman, Sophia, or Sage. Feynman updates the node to `:::statusGreen` and passes the change to Sophia for execution in the Structure Map - Visual Tracker. Feynman may proactively ask the [student/operator] about submitted items as a reminder check. Green overrides the formula entirely — no recalculation needed once submitted.

**Past-due protocol — ask before Black:**
Before marking any node `:::statusBlack` (past due), Feynman asks the [student/operator] directly: *"Did you submit [item]? Should this be Black or Green?"* Feynman marks Black only after the [student/operator] confirms the item was not submitted. This check runs every time — no exceptions.

---

## Session Summary Entry Format

Every session close entry in a [unit] session summary includes these fields:

| Field | Content |
|-------|---------|
| **[Unit]** | [Unit] code and name |
| **IP Session** | Corresponding IP session number |
| **Feynman Session #** | Session number within this [unit] (sequential from 1) |
| **Type** | Gate check / [Unit] activation / Content work / Close-out |
| **What was worked** | Plain summary of what was done this session |
| **Gate check result** | Color-only pass / Full pass / N/A (activation session) |
| **Deliverable changes** | What changed in Weekly Trackers or deliverable status |
| **Color status snapshot** | Table: Deliverable | Due | % | Status |
| **Flags surfaced to [student/operator]** | Any items needing the [student/operator]'s attention (or "None") |
| **What's next** | One or two lines on what comes next |

---

## Session Close Procedure

At the end of every Feynman session, in this order:

**Step 1 — Write session summary entry**
Feynman writes the entry using the format above. Entry goes in the active [unit]'s session summary file.

**Step 2 — Update the index**
Index updated in the same close step — always paired with the summary. Never update one without the other.

**Step 3 — [Program] Lessons Log check**
Ask: did anything in this session meet the transfer threshold — a lesson that will genuinely change how I approach a future [unit]? If yes, add entry to `[Feynman P/M Lead Folder]\[Program] Lessons Log.md`. If no, no entry is added. "No entry" is the expected outcome most sessions.

**Step 4 — Sophia executes; Feynman writes content**
Feynman writes all session entries and log entries. Sophia executes the file writes. Sage reviews before commit.

**Step 5 — Mixed sessions (IP + Feynman)**
When a session covers both IP work and Feynman work: IP Session Summary covers IP work; this SOP covers Feynman work. Sophia closes both in the same git push.

*Parallel/split-session close (rare):* When Feynman runs in a concurrent session separate from the main IP session, Feynman completes his own [unit] session close in his session, then signals Sage (via the [student/operator]). Sophia then captures Feynman's closed entries into the main session close and includes them in the same git push. Sage reviews before commit.

---

## [Program] Lessons Log

**Location:** `[project]\[Feynman P/M Lead Folder]\[Program] Lessons Log.md`

**Purpose:** Accumulate cross-[unit] lessons and insights over the [program]. Not a session record.

**Entry trigger criteria:** An entry fires when a lesson transfers — when Feynman can honestly say "this will change how I approach a future [unit], not just the current assignment." Examples: study/work strategy breakthroughs, how accelerated formats behave vs. standard-length [units], patterns in how the [student/operator] processes material under deadline pressure. [Unit]-specific observations stay in the [unit] session summary.

**Entry format:**

```
## [course-code] — [Short Lesson Title] — [Date]

**Origin [unit]:** [unit code + name]
**Lesson:** [What was learned — plain, one paragraph max]
**Forward-facing:** [Specifically what to apply differently in a future [unit]]
```

**Update timing:** At session close (if trigger criteria met) or during [unit] close-out review. Not mandatory every session — most sessions will produce no [Program] Lessons Log entry.

---

## [Unit] Close-Out Procedure

When a [unit] ends:

1. Review the full [unit] session summary for any entries that meet the [Program] Lessons Log transfer threshold that were not promoted mid-[unit]
2. Add qualifying entries to the [Program] Lessons Log
3. Add a Master Outcomes Log entry — [unit] code + name, [term] dates, credits/weight, key deliverables (brief list), final grade/result, C&P outcomes, [Program] Lessons Log pointers (or "None")
4. Mark the [unit] complete in the Structure Map - Visual Tracker per feynman-academic-project-map.md
5. No files moved or archived — [unit] summary and index stay in the support doc folder indefinitely
6. New [units] do not affect completed [unit] files

---

## Naming Standard Reference

| File | Naming Convention | Location |
|------|------------------|----------|
| [Unit] session summary | `[course-code]-Session-Summary.md` | [Unit]'s support doc folder |
| [Unit] session index | `[course-code]-Session-Summary-Index.md` | [Unit]'s support doc folder (always paired) |
| [Program] Lessons Log | `[Program] Lessons Log.md` | `[Feynman P/M Lead Folder]\` |
| Master Outcomes Log | `Master-Outcomes-Log.md` | `[Feynman P/M Lead Folder]\` |

[Unit] code format: uppercase, hyphenated (e.g., `[course-code]` such as `ABC-101`).

---

## SOP Version Log

| Version | Date | Session | What Changed | Why |
|---------|------|---------|-------------|-----|
