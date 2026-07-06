# Compact Wrap-Up SOP

**Owner:** Sage
**Version:** 0
**Created:** 2026-03-25
**Updated:** 2026-06-23
**Status:** Active
**Future:** Convert to Cosmo skill during Master Library tasking

---

## Purpose

This SOP defines the Compact Wrap-Up sequence — what Sage does before a context compaction occurs. Its goal is to ensure all files are current and pushed before the context window is compressed, so the post-compact re-read restores full, accurate state.

This is not a session close. The session continues after compaction.

---

## Trigger

Jay signals intent to compact. The signal is intent-based — any message where it is clear the context is about to be compacted. Context clues do the work; no specific phrase is required.

---

## Mid-Task Gate — fires the moment intent to compact is signaled, before Step 0

**The instant Jay signals intent to compact, before anything else runs, check: is any agent mid-task?** This gate fires ahead of the Step 0 Pre-Compact Sweep — Step 0 is itself work, and it should not begin while an agent is still changing files.

**"Mid-task" means:** an agent has an open, undelivered task in a declared in-progress state — a TodoWrite/TaskList item marked in-progress, or an explicitly declared "in-progress" marker in the session record or a handoff. An agent is NOT mid-task if its assigned work has been delivered, reported, or explicitly parked. **Scope includes embedded agents** — Sophia (COO) and any active P/M Lead are explicitly in scope.

**Detection — explicit task-state only:** read declared state. A TaskList/TodoWrite item still marked in-progress, or a standing in-progress declaration, means mid-task. **Detection is never by observation** — Sage does not infer or watch what an agent is "probably still doing." If no task is declared in-progress, the gate is clear. Absence of a declared in-progress marker = clear to proceed.

**If an agent is mid-task — compact does NOT begin. Resolve one of two ways first:**
1. **Finish** — the agent completes and delivers the task; its TaskList item flips to done.
2. **Park** — the task is explicitly parked: declared incomplete, and captured to the relevant landing spot (Sophia's pending list, a handoff note, or the Session Summary in-flight field) so it survives the compact and can be resumed. Parking is a deliberate, recorded act — not silence.

Only when every agent is either finished or explicitly parked does compact proceed to Step 0.

**How this differs from the Active Agents Check (below):** this gate **BLOCKS the start** — it prevents compact from beginning while work is still unfinished. The Active Agents Check **GATHERS** — it runs later (before the 8-step sequence) to collect each active agent's finished contributions into the record. Gate first (don't start on incomplete work); Active Agents Check later (capture completed work). Complementary, not redundant.

---

## Step 0 — Pre-Compact Sweep (runs before the Multi-Agent Check and 8-step sequence)

When Jay signals intent to compact, this runs first. The Multi-Agent Check and 8-step sequence do not begin until Jay reviews the report and gives the go-ahead.

**Scope:** Session-scoped — not a full project audit. Targeted check: what changed this session so far, and are the files that depend on those changes current?

**What to check:**
- Every file edited or created this session so far → does it have a paired counterpart (full vs. blank, template vs. instance, Agent SOP vs. Jay's version) that also needed updating? Is that counterpart current?
- Every structural change (new section, renamed concept, added rule, deleted item) → are all files that reference that section/concept/rule/item still accurate?
- Any version bumped this session → does the file header match the version log entry? Do paired files show the same version? Is the nav map version table current for that file?
- Any cross-reference sweep already run this session → were any dependent files identified then left pending?
- Any structural change to folders, subfolders, or files this session → confirm all three governance documents are current: `Folder & File Reference.md`, `Visual TreeView.md`, and `Folder & File Tree.md`. All three update together — never update one without checking the others. (Item 141)
- Any SOP, MG, pipeline, or process document with a paired Mermaid visual aid modified this session → confirm the visual aid was also updated in the same session. Paired visual aids live in permanent homes: SOPs folder, COO Suite, TLL, and relevant agent folders. (Item 142)

**Cross-reference + Backward Sweep (paired operation — runs as part of Step 0):**

Distinct from the pre-compact sweep above. The pre-compact sweep is session-scoped: what changed this session so far, are dependent files current? These sweeps are system-scoped: does the broader system remain consistent?

- **Cross-reference sweep:** For every change made this session so far, scan MG-SOPs, agent SOPs, and runbooks for any reference to the changed element that may now be inconsistent or stale.
- **Backward sweep:** Working backward through prior agent SOPs and MG-SOPs — do this session's changes introduce any clashes, gaps, stale references, or handoff mismatches?

**Rule:** Neither runs without the other. Trigger: any work done in a session — updates, fixes, additions, deletions, renames, new files or folders, anything. If no changes have been made yet this session, state it explicitly; sweeps are not required. Include findings in the Step 0 report.

**Output:** A concise report — what was checked, what (if anything) was found, and for each finding: which file, what the gap is, and a recommended fix. If nothing was found, say so explicitly: "Pre-compact sweep complete — nothing found."

**Then stop.** Deliver the report. Wait for Jay's explicit direction before proceeding with the Multi-Agent Check. He decides: continue to compact, fix something first, or keep working.

**Gate rule:** Jay's direction must come AFTER he has seen the report. Any direction given before Step 0 runs — including "compact now," "run the SOP," or equivalent — does NOT satisfy this gate. Nothing bypasses the report-and-wait. No exceptions.

**Exception — Solo Close:** When both Sage and Sophia are not present at compact wrap-up (one runs it while the other is unavailable), the solo runner must complete a mandatory second verification pass before delivering the Step 0 report: re-examine the Path Change Log, Current Project Snapshot, and all tracking rows in the nav map against actual file state. Two-eye review is the normal safeguard; this pass replaces it.

---

## Active Agents Check — Run Before the 8-Step Sequence

Before running the wrap-up sequence, check: are any agents currently active in this session?

**No agents active:** Proceed directly to the 8-Step Sequence below.

**Agents active:**
1. Each active agent tells Sage their piece — what they did, any flags, any findings relevant to the session record. Includes any agents dismissed earlier in the session — we brought them forward for a reason.
2. Sophia captures all agent contributions in the Session Summary entry (Step 1).
3. Sage reviews the full entry — including all agent contributions — before the Step 7 push.
4. Then Sage proceeds through the remaining steps.

**Rule:** A compact does not happen until all active agents have told Sage their piece and Sophia has captured it. No partial compacts. Sage must address each active agent directly and explicitly by name before their check is complete — self-concluding that an agent has nothing to add without asking them is a failed check at the moment of the live interaction, not only if their answer is missing from the written record.

---

## TodoWrite — Execution Sequences

**Before any execution sequence with 2+ steps that produces or changes something persistent, a TodoWrite task list is the first action.** Items are crossed off as each step is completed.

**Trigger test:** Does each step produce or change something that persists after the session? Yes → TodoWrite required. No → not required.

Excludes: session summary updates and compacting actions.

---

## Compact Wrap-Up Sequence — 8 Steps

### Step 1 — Session Summary.md and Session Summary Index
**Writer: Sophia. Review gate: Sage reviews before the Step 7 push.** If Sophia is unavailable (solo compact by Sage), Sage writes; no review gate applies.

Update **Session Summary.md**: Append to the top of the file (most recent first). Mark the entry clearly as a **mid-session checkpoint**, not a session close. Include: what was accomplished so far, key decisions and why, what to do next, open questions.

**Files Modified field (required in every CP entry):** List every file that was edited, created, or updated during this session before the compact. This field is what Sage reads post-compact to know what was touched — keep it complete and accurate. Format: bullet list of file names (role-based labels, no hard paths).

**"What to do next" must state explicit ordering** — not just a list of pending items. If item A must come before item B, say so explicitly. Sequence is as important as content here. This is what the post-compact wake-up reads to know what to do first.

**Source document capture:** If any source files were reviewed as meaningful inputs to this compact — e.g., nav map for version verification, Sophia's Pending Changes for terminal item check, Gotcha.md at session start — name them in the Session Summary entry: file name → what it was used for → key outcome. Applies to the full summary entry, not the Index. (Item 15 — mirrors Session-Close-SOP v2.5.)

Update **Session Summary Index**: Add one entry for this checkpoint — labeled `Session N — Compact Checkpoint N`, date, file pointer, key topics (concise comma-separated list, 6–10 words per topic).

**P/M Lead model (Item 103):** When a designated P/M Lead is active and managing a sub-project with their own dedicated folder and Session Summary (e.g., a live coursework or client track), the P/M Lead writes their sub-project session summary. Sophia writes the master IP Session Summary. Both are maintained independently and in parallel — neither replaces the other. The master IP summary covers IP-level decisions and progress only; sub-project detail stays in the P/M Lead's folder.

**Done when:** Both files are updated, complete, accurate, and the Session Summary entry is labeled as a mid-session checkpoint.

> **COHK (CloseOut-HouseKeeping):** If a split trigger fires during this session (+20 milestone, version update, or operator call), run the full COHK process at the appropriate break point — not mid-compact. Full process: `1. Sage's CEO Folder/6. SOPs/CloseOut-HouseKeeping-SOP.md`

### Step 2 — project_context.md
Review and update: current phase, what comes next, deferred items list, agent build status. Anything that changed this session gets reflected here.

Also check: did project direction, scope, roster, or objectives change this session? If yes, update `Sage-project-soul.md`.

**Nav map "As of:" sync (standing — every compact close):** Update the navigation map "As of:" date to the current session number and date. This fires every compact close regardless of whether any other nav map changes were made. The date field must match the current session.

**Done when:** All three files accurately reflect current project state — project_context.md, Sage-project-soul.md (if updated), and the nav map "As of:" date.

### Step 3 — MEMORY.md index files
Review all memory files. Update any that changed this session. Add new memory files if new feedback, lessons, or project context was generated. Update the MEMORY.md index if files were added or changed.
**Done when:** All memory files reflect current state; index is accurate.

### Step 4 — ME - Jay.md
Review: did this session surface anything new about the operator — thinking style, preferences, communication, things to avoid? If yes, add it.
**Done when:** File is current. If nothing new was learned, note it mentally and move on.

### Step 5 — Lessons Files + Team Lessons Log

**Sage's project lessons (lessons.md):** Were any corrections made or mistakes self-identified this session so far that are specific to this project's files, structure, or context? If yes, write the entry.

**Sage's global lessons (lessons_global.md in ~/.claude/):** Is this correction clearly universal — would it apply to every future project? If yes, write it to lessons_global.md instead (or in addition if it belongs in both). Hot path — do not wait for AAR.

**Team Lessons Log (`2. Sophia's COO Folder/3. Teams Lesson Log - TLL/Team-Lessons-Log.md`):** Was any agent actively deployed this session so far? If yes, did any lesson emerge worth logging? Route to Sophia. Sophia logs it. If the lesson is clearly universal and agent-specific, promote to that agent's soul immediately (hot path) and mark the entry accordingly. See Promotion-Pipeline-SOP.md for full decision tree. This check also fires at agent dismissal — not only at compact.

**Sophia's own lessons (standing check — every session):** Sophia works every session whether or not other agents are deployed. At compact wrap-up, ask Sophia directly: "Do you have any lessons from this session worth logging?" She is both the manager of the Team Lessons Log and a contributor to it. If she surfaces a lesson, Sage confirms scope and Sophia self-logs.

**Gotcha.md (standing check — every compact):** Did anything happen this session so far that belongs in Gotcha.md — an operational error, a trap encountered, a process gap that fired at the wrong time, or a repeated mistake? If yes, Sophia logs it immediately using v2.0 block format (field reference list — see Gotcha.md Field Definitions for the actual block format): Type (Gap/Issue) | Counter | Status (Applied/Verified) | What Happened | Root Cause | Fix Applied | Watch-Out Rule | Verified basis (when Status = Verified). No agent names as blame targets. Document the situation; name the trap. Sophia creates the entry in the same session if possible. See Gotcha.md Field Definitions for full format and field descriptions. **Read cadence:** Gotcha.md is a session-start read only — do NOT re-read post-compact. If a new entry was added during this compact close, note that fact in the compact summary; no full re-read required. Team Lessons Log: same read cadence — session-start only; do not re-read post-compact.

**Done when:** All corrections and team lessons from this session so far are captured in the correct file(s). Gotcha.md is current. If none in any category, step is complete.

**Enforcement:** The Compact Checkpoint entry for this session must name each respondent by name and record their actual answer — "Sophia: [her words]" and "[Agent]: [their words]." A Sage-drawn conclusion with no named respondent is a failed check. This step is not complete until both the Sophia response and any active agent response appear in the record by name.

### Step 6 — Sophia — Pending Changes List
Review: were any changes to source materials identified this session (souls, MGs, CLAUDE.md, skills, templates)? If yes, queue them to Sophia's Pending Changes List — do not write them.

After queueing: check the Pending Changes List for any terminal items (status `Complete ✓` or `Closed`). If any exist, run the physical transfer to sophia-completed-changes.md now — do not defer to session close. Transfer rules: `Sophia-List-Management-SOP.md` Transfer Protocol section. Update section counts and Quick Stats on both files.

**Catalog structural check:** Was any catalog restructure or new convention introduced this session so far? If yes, confirm all three before compacting: (1) catalog footers updated in all affected catalog files; (2) project_context.md reflects the completed state; (3) new convention queued to Sophia for documentation.

**Safety net catch sweep (Item 76):** Before compacting, run a final catch sweep across all work done in this session so far. Four questions:
- Anything missed, broken, or gapped that slipped through the cross-reference and backward sweeps?
- Any decision made or direction set this session that never got captured in a file?
- Any agent's output or flag from earlier in the session that didn't make it into the record?
- Any research reports produced this session → confirm routing: project-specific reports to WorkTree; reports with clear universal value to ML `3. Research Reports/Universal Research Reports/` (requires explicit AAR confirmation unless obviously universal). Never place new reports in ML Soul Folder.
When a gap surfaces: queue it to the Pending Changes List or note it in the Session Summary. This sweep is not optional.

**Done when:** New items queued (if any). Terminal items transferred to sophia-completed-changes.md (if any). Catalog structural check cleared. Safety net sweep complete. Pending Changes List has no remaining `Complete ✓` or `Closed` items.

### Step 7 — GitHub Push
Push all changes to GitHub. No confirmation required before pushing. Also stage and push any modified PPN files (Personal Project Notes — "Support docs for this project/" folder) in the same commit — Sage never reads PPN content; the push is the only PPN action permitted. Confirm after: *"Compact Wrap-Up complete. All files updated and pushed. Ready to compact."*
**Done when:** Push confirmed. No errors.

### Step 8 — git status check
Run `git status`. Working tree must be clean — zero modified, zero untracked files that should be committed.
**Done when:** Working tree is clean.

---

## After Compaction

After compaction, follow `Post-Compact-Return-SOP.md` — it is the authoritative return/resume procedure (one mandatory read, just-in-time discipline, agent re-activation). This SOP owns the pre-compact wrap-up and writes the CP section; the return path lives in Post-Compact-Return-SOP.

---

## Notes

- This SOP is the single source of truth for pre-compact actions. MGs point here.
- The 8 steps are identical to the Session Close SOP — the only differences are: (1) the Session Summary entry is labeled mid-session checkpoint, not session end; (2) there is no declaration of done; (3) the terminal item transfer check now fires at compact close — terminal items (Complete ✓ or Closed) are transferred to sophia-completed-changes.md in Step 6, same as Session-Close-SOP.
- If a step cannot be completed, document why before moving on — do not skip silently.
- Convert to Cosmo skill at Master Library tasking. SOP stays as the authored source.

---

