# Session Close SOP

**Owner:** Sage
**Version:** 0
**Created:** 2026-03-24
**Updated:** 2026-06-23
**Status:** Active
**Future:** Convert to Cosmo skill during Master Library tasking

---

## Purpose

This SOP defines the complete session close sequence. Every step must be confirmed complete before the session is declared done. Nothing is implied — if it is not checked, it is not done.

---

## Mid-Task Gate — fires the moment session close is signaled, before Step 0

**The instant Jay signals session close, before anything else runs, check: is any agent mid-task?** This gate fires ahead of the Step 0 Pre-Close Sweep — Step 0 is itself work, and it should not begin while an agent is still changing files.

**"Mid-task" means:** an agent has an open, undelivered task in a declared in-progress state — a TodoWrite/TaskList item marked in-progress, or an explicitly declared "in-progress" marker in the session record or a handoff. An agent is NOT mid-task if its assigned work has been delivered, reported, or explicitly parked. **Scope includes embedded agents** — Sophia (COO) and any active P/M Lead are explicitly in scope.

**Detection — explicit task-state only:** read declared state. A TaskList/TodoWrite item still marked in-progress, or a standing in-progress declaration, means mid-task. **Detection is never by observation** — Sage does not infer or watch what an agent is "probably still doing." If no task is declared in-progress, the gate is clear. Absence of a declared in-progress marker = clear to proceed.

**If an agent is mid-task — session close does NOT begin. Resolve one of two ways first:**
1. **Finish** — the agent completes and delivers the task; its TaskList item flips to done.
2. **Park** — the task is explicitly parked: declared incomplete, and captured to the relevant landing spot (Sophia's pending list, a handoff note, or the Session Summary in-flight field) so it survives the close and can be resumed. Parking is a deliberate, recorded act — not silence.

Only when every agent is either finished or explicitly parked does session close proceed to Step 0.

**How this differs from the Active Agents Check (below):** this gate **BLOCKS the start** — it prevents close from beginning while work is still unfinished. The Active Agents Check **GATHERS** — it runs later (after Jay's go-ahead, before Step 1) to collect each active agent's finished contributions into the record. Gate first (don't start on incomplete work); Active Agents Check later (capture completed work). Complementary, not redundant.

---

## Step 0 — Pre-Close Sweep (runs before the 8-step sequence)

When Jay signals session close, this runs first. The 8-step sequence does not begin until Jay reviews the report and gives the go-ahead.

**Scope:** Session-scoped — not a full project audit. Targeted check: what changed this session, and are the files that depend on those changes current?

**What to check:**
- Every file edited or created this session → does it have a paired counterpart (full vs. blank, template vs. instance, Agent SOP vs. Jay's version) that also needed updating? Is that counterpart current? **Note (Item 121):** A Jay's version counterpart may be a visual workflow (Mermaid diagram) rather than a plain-text document — visual-as-default applies to non-technical process SOPs. The pairing check still fires regardless of the counterpart's format.
- Every structural change (new section, renamed concept, added rule, deleted item) → are all files that reference that section/concept/rule/item still accurate?
- Any version bumped this session → does the file header match the version log entry? Do paired files show the same version? Is the nav map version table current for that file?
- Any cross-reference sweep that was already run this session → were any dependent files identified then left pending?
- Any structural change to folders, subfolders, or files this session → confirm all three governance documents are current: `Folder & File Reference.md`, `Visual TreeView.md`, and `Folder & File Tree.md`. All three update together — never update one without checking the others. (Item 141)
- Any SOP, MG, pipeline, or process document with a paired Mermaid visual aid modified this session → confirm the visual aid was also updated in the same session. Paired visual aids live in permanent homes: SOPs folder, COO Suite, TLL, and relevant agent folders. (Item 142)

**Cross-reference + Backward Sweep (paired operation — runs as part of Step 0):**

Distinct from the pre-close sweep above. The pre-close sweep is session-scoped: what changed this session, are dependent files current? These sweeps are system-scoped: does the broader system remain consistent?

- **Cross-reference sweep:** For every change made this session, scan MG-SOPs, agent SOPs, and runbooks for any reference to the changed element that may now be inconsistent or stale.
- **Backward sweep:** Working backward through prior agent SOPs and MG-SOPs — do this session's changes introduce any clashes, gaps, stale references, or handoff mismatches?

**Rule:** Neither runs without the other. Trigger: any work done in a session — updates, fixes, additions, deletions, renames, new files or folders, anything. If the session was purely read-only with no changes, state it explicitly; sweeps are not required. Include findings in the Step 0 report.

**Output:** A concise report — what was checked, what (if anything) was found, and for each finding: which file, what the gap is, and a recommended fix. If nothing was found, say so explicitly: "Pre-close sweep complete — nothing found."

**Then stop.** Deliver the report. Wait for Jay's explicit direction before proceeding with Step 1. He decides: continue to close, fix something first, or pivot.

**Gate rule:** Jay's direction must come AFTER he has seen the report. Any direction given before Step 0 runs — including "do the full close," "run the SOP," or equivalent — does NOT satisfy this gate. Nothing bypasses the report-and-wait. No exceptions.

**Exception — Solo Close:** When both Sage and Sophia are not present at close (one runs close while the other is unavailable), the solo runner must complete a mandatory second verification pass before delivering the Step 0 report: re-examine the Path Change Log, Current Project Snapshot, and all tracking rows in the nav map against actual file state. Two-eye review is the normal safeguard; this pass replaces it.

---

## Active Agents Check — runs after Jay confirms, before Step 1

Were any agents active at any point during this session — including agents brought in and dismissed earlier in the session?

- **If YES:** Each agent who was active this session tells Sage their piece — what they did, any flags, any findings relevant to the session record. Dismissed earlier does not mean exempt — we brought them forward for a reason. Sophia captures all agent contributions in the Session Summary entry. Sage reviews the full entry before the Step 7 push.
- **If NO:** Proceed directly to Step 1.

**Done when:** All active agents have told Sage their piece and Sophia has captured it, or confirmed no agent was active this session.

**Rule:** Sage must address each active agent directly and explicitly by name before their check is complete. Self-concluding that an agent has nothing to add without asking them is a failed check — not only if their answer is missing from the written record, but at the moment of the live interaction.

---

## TodoWrite — Execution Sequences

**Before any execution sequence with 2+ steps that produces or changes something persistent, a TodoWrite task list is the first action.** Items are crossed off as each step is completed.

**Trigger test:** Does each step produce or change something that persists after the session? Yes → TodoWrite required. No → not required.

Excludes: session summary updates and compacting actions.

---

## Session Close Sequence — 8 Steps

### Step 1 — Session Summary.md and Session Summary Index
**Writer: Sophia. Review gate: Sage reviews before the Step 7 push.** If Sophia is unavailable (solo close by Sage), Sage writes; no review gate applies.

Update **Session Summary.md**: Append to the top of the file (most recent session first). Include: what was accomplished, key decisions and why, what to do next, open questions.

**"What to do next" must state explicit ordering** — not just a list of pending items. If item A must come before item B, say so explicitly. This is what the next session reads to know where to pick up.

**Source document capture:** If any source files were reviewed as meaningful inputs to this close — e.g., nav map for version verification, Sophia's Pending Changes for terminal item check, Gotcha.md at session start — name them in the Session Summary entry: file name → what it was used for → key outcome. Applies to the full summary entry, not the Index. (Item 15 — practice starts Session 123 Final Close.)

Update **Session Summary Index**: Add one entry for this session — session number, date, file pointer (which Session Summary file), key topics (concise comma-separated list, 6–10 words per topic).

**P/M Lead model (Item 103):** When a designated P/M Lead is active and managing a sub-project with their own dedicated folder and Session Summary (e.g., a live coursework or client track), the P/M Lead writes their sub-project session summary. Sophia writes the master IP Session Summary. Both are maintained independently and in parallel — neither replaces the other. The master IP summary covers IP-level decisions and progress only; sub-project detail stays in the P/M Lead's folder.

**Done when:** Both files are updated, complete, and accurate.

> **COHK (CloseOut-HouseKeeping):** If this session closes on a split trigger (+20 milestone, version update, or operator call), run the full COHK process before or after closing — not mid-session. Full process: `1. Sage's CEO Folder/6. SOPs/CloseOut-HouseKeeping-SOP.md`

### Step 2 — project_context.md
Review and update: current phase, what comes next, deferred items list, agent build status. Anything that changed this session gets reflected here.

Also check: did project direction, scope, roster, or objectives change this session? If yes, update `Sage-project-soul.md`.

**Nav map "As of:" sync (standing — every session close):** Update the navigation map "As of:" date to the current session number and date. This fires every session close regardless of whether any other nav map changes were made. The date field must match the session being closed.

**Done when:** All three files accurately reflect current project state — project_context.md, Sage-project-soul.md (if updated), and the nav map "As of:" date.

### Step 3 — MEMORY.md index files
Review all memory files. Update any that changed this session. Add new memory files if new feedback, lessons, or project context was generated. Update the MEMORY.md index if files were added or changed.
**Done when:** All memory files reflect current state; index is accurate.

### Step 4 — ME - Jay.md
Review: did this session surface anything new about the operator — thinking style, preferences, communication, things to avoid? If yes, add it.
**Done when:** File is current. If nothing new was learned, note it mentally and move on.

### Step 5 — Lessons Files + Team Lessons Log

**Sage's project lessons (lessons.md):** Were any corrections made or mistakes self-identified this session that are specific to this project's files, structure, or context? If yes, write the entry.

**Sage's global lessons (lessons_global.md in ~/.claude/):** Is this correction clearly universal — would it apply to every future project? If yes, write it to lessons_global.md instead (or in addition if it belongs in both). Hot path — do not wait for AAR.

**Team Lessons Log (`2. Sophia's COO Folder/3. Teams Lesson Log - TLL/Team-Lessons-Log.md`):** Was any agent actively deployed this session? If yes, did any lesson emerge worth logging? Route to Sophia. Sophia logs it. If the lesson is clearly universal and agent-specific, promote to that agent's soul immediately (hot path) and mark the entry accordingly. See Promotion-Pipeline-SOP.md for full decision tree. This check also fires at agent dismissal — not only at session close.

**Sophia's own lessons (standing check — every session):** Sophia works every session whether or not other agents are deployed. At session close, ask Sophia directly: "Do you have any lessons from this session worth logging?" She is both the manager of the Team Lessons Log and a contributor to it. If she surfaces a lesson, Sage confirms scope and Sophia self-logs.

**Gotcha.md (standing check — every session):** Did anything happen this session that belongs in Gotcha.md — an operational error, a trap encountered, a process gap that fired at the wrong time, or a repeated mistake? If yes, Sophia logs it immediately using v2.0 block format (field reference list — see Gotcha.md Field Definitions for the actual block format): Type (Gap/Issue) | Counter | Status (Applied/Verified) | What Happened | Root Cause | Fix Applied | Watch-Out Rule | Verified basis (when Status = Verified). No agent names as blame targets. Document the situation; name the trap. Sophia creates the entry in the same session if possible. See Gotcha.md Field Definitions for full format and field descriptions. **Read cadence:** Gotcha.md is a session-start read only — do not re-read post-compact. If a new entry was added during the compact close, that fact appears in the compact summary; no full re-read required. Team Lessons Log: same read cadence — session-start only; do not re-read post-compact.

**Done when:** All corrections and team lessons from this session are captured in the correct file(s). Gotcha.md is current. If none in any category, step is complete.

**Enforcement:** The Session Summary entry for this session must name each respondent by name and record their actual answer — "Sophia: [her words]" and "[Agent]: [their words]." A Sage-drawn conclusion with no named respondent is a failed check. This step is not complete until both the Sophia response and any active agent response appear in the record by name.

### Step 6 — Sophia — Pending Changes List
Review: were any changes to source materials identified this session (souls, MGs, CLAUDE.md, skills, templates)? If yes, queue them to Sophia's Pending Changes List — do not write them. They are reviewed at project AAR.

**Transfer eligible items:** Also check the Pending Changes List for any items at terminal status (`Complete ✓` or `Closed`). If any exist, execute the transfer batch to the Completed Changes List per the List Management SOP Transfer Protocol. Session close and compact close are both transfer triggers — transfers happen at both. Mid-session transfers outside these two checkpoints are not permitted.

**Catalog structural check:** Was any catalog restructure or new convention introduced this session? If yes, confirm all three before closing: (1) catalog footers updated in all affected catalog files; (2) project_context.md reflects the completed state; (3) new convention queued to Sophia for documentation.

**Safety net catch sweep (Item 76):** Before closing, run a final catch sweep across all work done in this session. Four questions:
- Anything missed, broken, or gapped that slipped through the cross-reference and backward sweeps?
- Any decision made or direction set this session that never got captured in a file?
- Any agent's output or flag from earlier in the session that didn't make it into the record?
- Any research reports produced this session → confirm routing: project-specific reports to WorkTree; reports with clear universal value to ML `3. Research Reports/Universal Research Reports/` (requires explicit AAR confirmation unless obviously universal). Never place new reports in ML Soul Folder.
When a gap surfaces: queue it to the Pending Changes List or note it in the Session Summary. This sweep is not optional.

**Agent Teams reconcile-back (conditional — project close or mid-project agent disable only):**
If this is a project close session, or an agent is being explicitly disabled mid-project, and that agent has a live soul in `.claude/agents/`: initiate the reconcile-back protocol.
1. Sophia compares the `.claude/agents/` copy to the dormant v0.1 copy — documents any delta
2. Sage reviews: what changed, what carries back
3. Approved changes applied to the v0.1 copy
4. Dormant marker removed from the v0.1 copy
5. `.claude/agents/` copy removed

**AAR gate:** No changes from a live `.claude/agents/` copy go to the Blank or MUIP directly — all changes pass through AAR review first. Jay approves what gets promoted.

This check is silent at standard session closes when Agent Teams remains active for all agents.

**Done when:** New items queued that need queuing. Terminal-status items transferred if any existed. Catalog structural check cleared. Safety net sweep complete. Agent Teams reconcile-back completed if triggered. If nothing in any category, step is complete.

### Step 7 — GitHub Push
Push all changes to GitHub. No confirmation required before pushing. Also stage and push any modified PPN files (Personal Project Notes — "Support docs for this project/" folder) in the same commit — Sage never reads PPN content; the push is the only PPN action permitted. Confirm after: *"Session Summary and PPN updated and pushed to GitHub."*
**Done when:** Push confirmed. No errors.

### Step 8 — git status check
Run `git status`. Working tree must be clean — zero modified, zero untracked files that should be committed.
**Done when:** Working tree is clean.

---

## Declaration

Session is not done until all 8 steps are confirmed. A clean git status is the final gate.

---

## Notes

- This SOP is the single source of truth for session close. MGs point here; soul points here.
- If a step cannot be completed, document why before moving on — do not skip silently.

---

