# Gotcha.md — Project Watch List

**Owner:** Sophia (COO)
**CEO Accountability:** Sage — overall responsible and accountable for health, accuracy, and active use of this file.
**Project:** Random Projects
**Version:** 0
**Purpose:** Per-project operational watch list. Captures what went wrong, why, the fix applied, and the standing watch-out rule. Not a blame list — no agent names as blame targets. Entries describe situations and traps, not individuals.
**Philosophy:** Trust, but verify. Status reports — including this file — are inputs to independent verification, not substitutes for it. Approach agreements in good faith; confirm compliance independently. Collaboration and risk management run in parallel, not in trade-off. This is the standing operating principle behind why this file exists and how it is used.
**Entry standard:** Type | Counter | Status | Session | What Happened | Root Cause | Fix Applied | Watch-Out Rule
**Created:** Session 1 — 2026-07-06
**Last Updated:** Session 3 — 2026-07-10 (Entry 1 counter → 2: pattern recurred, caught + fixed same-session)

---

## Field Definitions

**Type:**
- **Gap** — The process, rule, or system didn't cover this scenario. Something was missing or undefined. Includes natural gaps from adding, changing, or revamping a process — those can't be helped. Fix = add something new.
- **Issue** — The process or rule exists but failed, wasn't followed, or didn't hold after a prior fix. Fix = reinforce or redesign what's already there.

**Counter:** How many times this entry's scenario has recurred.
- Starts at 1 on first documented occurrence; increments on each recurrence.
- 2+ = pattern. 3+ = systemic problem requiring deeper attention.
- Note: some entries were created *because* of a recurrence — those start at 2 or higher.

**Status:**
- **Applied** — Fix is in place. Watching to confirm it holds in real-world operation.
- **Verified** — Fix confirmed effective. Verification trigger priority: (1) event-based — scenario recurs and fix holds; (2) milestone-based — AAR, Walk phase, or equivalent; (3) Sage's judgment call.

---

## How to Use

- **Read cadence:** Session start — full read (loaded via Sophia activation step in CLAUDE.md; not a standalone session-start step). Post-compact — skip. If a new entry was added during the compact close sequence, that fact is noted in the compact summary. No full re-read required post-compact.
- **Contributing:** Any agent or Sage identifies a gotcha → report to Sophia. Sophia logs it in the same session if possible.
- **Counter updates:** Sophia increments the counter when a recurrence is confirmed. Sage approves the Verified status change.
- **At AAR:** Sophia reviews all entries for recurring patterns. Entries to promote → `lessons_global.md` or relevant agent souls. Single-project incidents → note for pattern review only.
- **Cosmo note:** This file is structured for agent parsing. Block format with labeled fields supports skill and hook development from watch-out patterns.
- **Relationship to other files:** See the lessons vs. Gotcha routing chart in the Session Summary for when something goes here vs. lessons.md vs. Team Lessons Log.

---

## Quick Reference

| # | Session | Type | Counter | Status | Topic |
|---|---------|------|---------|--------|-------|
| 1 | 1 | Gap | 2 | Applied | Structural folder change requires the Item 141 three-doc governance update (recurred S3 — caught + fixed same-session) |

---

## Entries

### Entry 1 — Session 1

**Type:** Gap
**Counter:** 2
**Status:** Applied
**Session:** 1 (first occurrence); recurred Session 3

**What Happened:** Phase 0 activation renamed the Live Folder (`Named Project` → `Random Projects`) and created a full set of new files (root CLAUDE.md, CEO index/nav-map, filled soul, session records, COO operational files, TLL log, tracker + status board, `.claude/agents/sophia-coo.md`). The three Folder Governance docs — `Folder & File Reference.md`, `Folder & File Tree.md`, `Visual TreeView.md` — were not updated at the time and stayed in pristine MUIP-baseline form. The staleness was caught at the Step 0 pre-close sweep, not during the work that caused it.

**Root Cause:** `Getting-Started.md`'s Phase 0 sequence has no explicit step to refresh the three governance docs after a structural change. The rename and file creation happened; nothing in the activation flow prompted the Item 141 three-doc update, so it was silently deferred to the close sweep.

**Fix Applied:** All three governance docs updated together this session per Item 141 (Live Folder rename, Jot subfolder, and all Phase 0 files reflected). Process fix queued to Sophia's Pending Changes List for AAR: add a governance-docs update step to the Getting-Started Phase 0 sequence.

**Watch-Out Rule:** Any folder rename or file creation — at Phase 0 or later — must trigger the Item 141 three-doc governance update in the same session as the change, not at the close sweep. Until Getting-Started codifies the step, treat it as a standing manual check at Phase 0 and confirm again at every Step 0 pre-close sweep.

**Recurrence — Session 3 (2026-07-10):** Jay made a between-sessions structural change ("housekeeping"): created `Personal Note taker/` inside the Live Folder and moved the Jot mini-project + Screenshots under it, created an empty `Pure randomness/` folder, and accidentally swept the container master trackers + README into `Personal Note taker/` along with it. The accidental tracker move was caught at session start by Sage's structure check (raised with Jay) and independently confirmed by Sophia's activation check without seeing Sage's position — the 3rd-set-of-eyes pattern. Jay confirmed it unintentional; Sage reverted it (masters back at Live Folder root). All five affected navigation docs (three governance docs + project-file-index + project-navigation-map) were updated the same session; project CLAUDE.md session-start paths were verified still correct (no edit). **What this recurrence shows:** the watch-out rule held — the change was caught and reconciled same-session rather than going stale — but it held on manual vigilance, not a codified step. The trigger recurring confirms this is a pattern (counter → 2) and strengthens Pending AAR #1 (add a governance-doc update step to Getting-Started's Phase 0 sequence). **Verification note for Sage:** this is event-based verification evidence (structural-change event recurred, fix held) — candidate for Applied → Verified at Sage's call, though the manual-vigilance dependency is the reason to keep AAR #1 open.

---

*Sophia creates this file at project open and maintains it throughout. Sage (CEO) is overall responsible and accountable for health, accuracy, and active use.*
*At AAR: review entries for recurring patterns; anything universal → promote to `lessons_global.md` or relevant soul.*
*Per-project file — does not carry forward automatically. Each project gets a fresh Gotcha.md seeded from the prior project's promoted patterns.*
