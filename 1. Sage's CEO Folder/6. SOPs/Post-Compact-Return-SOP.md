# Post-Compact-Return SOP

**Owner:** Sage
**Version:** 0
**Created:** 2026-06-15 (Session 254)
**Updated:** 2026-06-17 (Session 257)
**Status:** Active
**Future:** Convert to Cosmo skill during Master Library tasking

---

## Purpose

This SOP defines how to return to work after a mid-session compaction. Compaction compresses the context window — the conversation history is gone, but the work is not. This is the recovery path: how to re-orient quickly, confirm where things stand, and resume the in-flight task without losing what was underway.

It is written for a disoriented reader. After a compact, you do not have the prior conversation in context. You are standing in the project with the work half-done and no memory of the last few hours. This SOP assumes exactly that state and gets you back to productive in the fewest reads possible. Read it standalone — it does not require any other document to be read first.

**The core discipline: one mandatory read, everything else just-in-time.** The single biggest mistake after a compact is re-running the full fresh-session read-in. That refills the context window you just cleared and forces a second compact almost immediately. Do not do it.

**Scope — post-compact only.** This SOP runs ONLY after a mid-session compaction. If you are opening a fresh session (a new session, not a mid-session compact), do NOT run this — follow `Session-Start-SOP.md` instead. Know which you are in: returning after the window was compressed mid-session → this SOP; opening the project anew → Session-Start-SOP.

---

## The Return at a Glance

1. Read the most recent CP section in `Session Summary.md` — the ONLY mandatory read.
2. Check the **Files Modified** field — know what was touched this session.
3. Do NOT run the full session-start sequence.
4. Confirm oriented.
5. Re-activate embedded agents (Sophia / P/M Lead) — they do not survive a compact.
6. Resume the in-flight task — just-in-time reads only, as the task requires.

---

## Step 1 — Read the CP Section (the only mandatory read)

**What persists across a compact:** the global `~/.claude/CLAUDE.md` (identity / corporate charter) and the project `CLAUDE.md` (the loader) auto-reload into context — so identity and the loader survive. **What does NOT auto-restore is the session's working state** — what you were doing and where it stands. That is exactly why the CP section is the one mandatory read.

The most recent CP (compact checkpoint) section in `Session Summary.md` is the single mandatory read after a compaction. It holds full state — what the session was doing, what was decided, what was changed, and where the work stands.

That CP section is **produced by `Compact-Wrap-Up-SOP.md` (Step 1)** during the pre-compact wrap-up — that is, the wrap-up writes the snapshot precisely so this SOP can read it. This SOP **consumes** the CP section; it does not re-create it and does not repeat the wrap-up procedure. If you need to know how the CP section was built, that is Compact-Wrap-Up's lane — not this one.

Read the most recent CP section only — find the last CP entry and read from there to the end of that section. Do not read earlier CP sections or earlier session entries unless a specific gap requires it.

---

## Step 2 — Check Files Modified

Within the CP section, read the **Files Modified** field. This tells you exactly which files were touched this session before the compact. It is your map of what is in-flight: any file listed there was being worked on and may be mid-change. This is what orients you to the actual work state without reading the files themselves yet.

---

## Step 3 — Do NOT Run the Full Session-Start Sequence

The fresh-session read-in (`Session-Start-SOP.md`) exists to build context from nothing at the start of a session. After a compact you already have full state from the CP section — running the full read-in on top of it refills the window you just cleared and forces a second compact.

The CP section replaces the full read-in here. That is the entire point of writing it at wrap-up. Trust it.

---

## Step 4 — Confirm Oriented

After reading the CP section and the Files Modified field, confirm you know:
- What the session was working on
- What was decided or changed before the compact
- What the next action is
- Whether any task was left in-flight or parked

If all four are clear, you are oriented — proceed to re-activate agents (Step 5) and resume (Step 6). If any is unclear, that is the trigger for a just-in-time read — not a reason to re-run the full read-in.

**Context-window milestones reset to zero** after any compaction. Start counting fresh.

**Gotcha.md is NOT re-read post-compact.** Its read cadence is session start only. If a new Gotcha entry was added during the compact close, that fact was noted in the compact summary — no re-read is required.

---

## Step 5 — Re-Activate Embedded Agents

A compaction wipes the conversation context — which means embedded subagents do NOT survive it. Sophia (COO) and any active P/M Lead were running in-session before the compact; after it, they are gone and must be re-spawned to continue their lane of work.

- The compact summary records who was active before the compact. Check it.
- **If Sophia was active before the compact** — re-activate her as part of resuming, before continuing any work in her lane. Her standing-activation principle applies the same as at session start. **Re-spawn her as an embedded observer in `acceptEdits` mode** — a re-activated embedded agent fails closed on writes exactly as at first spawn (Sage MG v2.72 Operating Model; failure mode: Gotcha #35).
- **If a P/M Lead was active** — re-activate them as well.
- Embedded agents do not persist across a compaction. Re-spawn before continuing their work — do not assume they are still present just because the work was mid-flight when the compact happened.

This is the most common post-compact miss: resuming the work without re-spawning the agent who was doing it.

---

## Step 6 — Resume the In-Flight Task

Pick the work back up where it left off.

- **If a task was parked at compact** (the mid-task gate requires any unfinished task to be either finished or explicitly parked before a compact proceeds), this is where you pick it up. The CP section records what was parked and where it stands — resume from there.
- **Just-in-time reads only.** Read a file only when the resumed task actually needs it — and only that file. Do not pre-read. The files named in Files Modified are the likely candidates, but read them when the work reaches them, not before.

Resume work where the session left off.

---

## Notes

- This SOP is the authoritative procedure for returning after a compaction. The project CLAUDE.md post-compact section points here — it does not duplicate these steps.
- One mandatory read (the CP section); everything else just-in-time. This is the discipline that prevents a second compact.
- Boundary: `Compact-Wrap-Up-SOP.md` owns the pre-compact wrap-up and writes the CP section; this SOP owns the return and resume. The CP section is the artifact passed between them — this SOP reads it, it does not restate how it is built.
- Companion to `Session-Start-SOP.md` (fresh session) — the two together cover both ways back into a session. The scope fork at the top of each routes the reader to the right one.
- If a step cannot be completed, document why before moving on — never skip silently.
- Convert to Cosmo skill at Master Library tasking. SOP stays as the authored source.

---

