# Sophia — List Management SOP (Sage/Agent Version)

**Version:** 0
**Owner:** Sophia (COO)
**Created:** 2026-05-05
**Updated:** 2026-06-23
**Status:** Active (Sage/Agent version)
**Applies to:** All projects — standing team member

---

## Purpose

This SOP governs how Sophia manages her four lists across the life of every project. It is the single source of truth for all list definitions, status labels, session-start protocols, transfer rules, cross-reference procedures, and backwards sweep cadence.

The legends inside the actual list files are summaries only. They reference this SOP. They do not define anything themselves.

**Why this SOP exists separately from the COO SOP:** The COO SOP defines what Sophia does and when. This SOP defines how the list infrastructure works — the architecture, the labels, the protocols, and the transfer logic. Both are required; neither replaces the other.

---

## Trigger

**Activation:** This SOP governs Sophia's list behavior at all times — from session start through project close. It fires continuously, not on a discrete trigger.

**Applies to:**
- Every session open and session close
- Every compact open and compact wrap-up
- Every review cadence checkpoint
- Every AAR

---

## Step-by-Step Procedures

### Phase 0 — Project Start

**Step 1 — Initialize the four-list architecture.**
When a new project opens and Sophia activates, confirm all four lists are in place:

1. **Sophia's Pending Changes List** — created during Phase 0 setup (governed by this SOP and the COO SOP Step 4). Home: Sophia's COO Folder → Operational Files (`sophia-pending-changes.md`).
2. **Sophia's Completed Changes List** — created during Phase 0 setup. Stored alongside Pending Changes. See File Organization table for location.
3. **Gotcha.md** — created during Phase 0 setup per COO SOP Step 6. Home: Sophia's COO Folder → Operational Files (`Gotcha.md`).
4. **Team Lessons Log** — Sophia manages this file for the whole team. Home: Sophia's COO Folder → Teams Lesson Log - TLL (`Team-Lessons-Log.md`).

If any of the four lists is missing when Sophia activates, create it immediately using the appropriate template before any other work proceeds.

---

### Phase 1 — Ongoing Session Work

**Step 2 — Manage Pending Changes (List 1).**
The Pending Changes List is the active operational queue. Sophia manages it. It is open from the first moment of every session.

Inbound items arrive from any source — any agent, Sage, or Jay. Sophia receives the item, categorizes it (agent, phase, section), assigns the correct status label (see Status Labels section), and adds it to the correct internal section.

Status assignment is Sophia's call — not the source agent's call. The source surfaces the item; Sophia categorizes and assigns.

**No item is applied mid-project.** Everything queues here first. Emergency exception: explicit operator approval required; flag on the list with the approval noted; flag at AAR.

**Step 3 — Manage Completed Changes (List 2).**
The Completed Changes List is the archive. Items move here from Pending Changes per the Transfer Protocol (see dedicated section below). This file is not an active queue — it is loaded on demand only.

**Step 4 — Manage Gotcha.md (List 3) and Team Lessons Log (List 4).**
See the dedicated sections below. Both are governed by existing SOPs with cross-references here.

---

### Phase 2 — Review Cadence

**Step 5 — Pending Changes review.**
Review cadence: every 5 sessions or compacts. Flex to 10 if the list stabilizes and additions slow significantly.

**Ad-hoc trigger:** If something on the list is actively being worked on mid-session, flag it for reclassification immediately — do not wait for the cadence.

**Quality check at every review:** "Does any `Pending AAR` item actually have a known activation point before project close? If yes, reclassify to `Moved to [project] — build input for [agent]`."

**Volume check:** If the list exceeds approximately 20 active items, flag volume risk to Sage. Run an ad-hoc review: anything to close, retire, or reclassify?

---

## Triage Intake Gate

Every inbound item is rated 0–10 before being added to the Pending Changes List. This rating determines the action tier — not just where the item goes, but whether it enters the list at all.

**Scale:** 0 (close now — already done or superseded) → 10 (true AAR gate — cannot resolve mid-project)

### Action Tiers

| Tier | Rating | Action |
|------|--------|--------|
| Handle immediately | 0–2 | Complete the work now — do not add to Pending Changes; item goes straight to Completed Changes |
| Gatekeeper evaluation | 3–4 | Sophia evaluates: can this be completed now? **YES** → complete immediately (treat as 0–2 pull-forward); route to Completed Changes, no list entry. **NO** → provide a Concise & Precise statement (see format below) and surface for a quick call. |
| Standard queue | 5+ | Add to correct section normally |

**Sophia's gatekeeper standard (3–4 items):** The question is not "where does this go?" but "can this be done now?" If it can — complete it. The list is for work that genuinely cannot happen yet.

### C&P Format (Tiers 3–4)

`[Brief title — Rating N: what it is, what's needed, estimated effort]`

Example: `ML SOP — Section 2a Hooks — Rating 3: Add one-line Hooks section entry to both SOP versions. ~10 min. No decision needed.`

The statement can expand past one line. Jay can always request more detail.

### Section-Specific Interpretations

- **Deferred Named:** 0–2 = deferral no longer warranted — pull forward and complete now. Scale reflects how much new project work is still required.
- **Behavioral Standards Active:** Scale = SOP formalization complexity, not urgency. Standard is already active — rating tracks how involved the formal write-up will be.
- **Pending AAR:** Standard intake gate. 0–2 items can be handled within the current project. 9–10 items are true AAR holds that cannot be resolved mid-project.

### Rating Markers and Reassessability

Each rated item is annotated: `*— Triage: [N] — last rated: Session [X]*`

Ratings are reassessable — a 7 can drop to a 3 if context changes. Re-rate at the next review cadence and update the "last rated" session in the annotation.

### 0–2 Pull-Forward Process

When an item is rated 0–2:
1. Complete the required work immediately.
2. Do not add the item to the Pending Changes List.
3. Document in Completed Changes (Section 1 for completed work; Section 3 for superseded/retired items).
4. If the item was already on the Pending Changes List before being rated: change its status to `Complete ✓` or `Closed`, update the item description with a pull-forward note, and transfer at next session close per the Transfer Protocol.

**Completed Changes as system of record:** Sophia's Completed Changes list is a second system of record alongside the active Pending Changes list — not just an archive.

---

## Session-Start Reading Protocol

This is a formal protocol, not an informal practice. Context window cost is a real constraint. The loading rules below are architectural decisions.

| List | Session-Start Load? | Notes |
|------|---------------------|-------|
| Sophia's Pending Changes (List 1) | **Yes — every session** | Active operational queue. Must be loaded to function. |
| Sophia's Completed Changes (List 2) | **No — on demand only** | Archive. Loaded only when Sage or Jay specifically requests it. Deliberate context window decision. |
| Gotcha.md (List 3) | **Yes — every session** | Established in the COO SOP and project CLAUDE.md. Loaded alongside Pending Changes. |
| Team Lessons Log (List 4) | **No — on demand** | Consulted at session close, compact close, and on explicit request. Not a session-start load. |

**On demand** means: when Sage or Jay asks, or when Sophia needs to consult it for a specific task (lesson routing, AAR prep). It is never preloaded speculatively.

---

## Cross-Reference and Backwards Sweep

These are a paired operation. Neither runs without the other. Both must be explicitly confirmed — not assumed.

### Cross-Reference (Session Open / Compact Open)

**When it fires:** At the opening of every session and every compact.

**What it does:** Sophia runs a cross-reference check of the Pending Changes List against the most recent session summary. The goal: catch any items that were applied, resolved, or changed during the prior session but not yet updated on the list.

**Procedure:**
1. Read the session summary from the prior session (or the compact summary if recovering from compact).
2. Identify any decisions, changes, or applied items mentioned in the summary.
3. Check whether each is reflected on the Pending Changes List with the correct status.
4. Correct any gaps immediately. Log any corrections with a note.

**Why this exists:** Drift between the session summary and the list is the primary failure mode. A decision documented in the summary but not updated on the list creates a false picture of what is still pending. This check is the mechanism that prevents list drift.

### Backwards Sweep

**When it fires:** At the same cadence as the Pending Changes review — every 5 sessions or compacts. Flex to 10 if the list stabilizes.

**What it does:** A sweep across recent sessions (since the last sweep) to confirm:
1. No applied changes are still sitting on the Pending Changes List with an outdated status.
2. No items implied in session summaries were never formally added to the list.

**Procedure:**
1. Pull the session summary entries since the last backwards sweep.
2. Scan for decisions, changes, or outputs that should have generated a Pending Changes entry.
3. If any such item is missing from the list, add it retroactively with the session it originated in.
4. If any item on the list has a status that no longer matches reality (e.g., listed as `Pending AAR` but already applied), correct it and note the discrepancy.

**Logging:** After each backwards sweep, note the sweep completion and the session range covered at the bottom of the Pending Changes List (in the maintenance footer).

---

## List 1 — Sophia's Pending Changes

### Internal Sections (in this order)

**1. Active**
Items currently being worked on this session or sprint. An item from any other section can be reclassified into Active when work begins on it. When work pauses, reclassify back out to its previous home or to the appropriate status.

**2. Deferred Named**
Items with a known activation point — a specific project, sprint, or named agent — identified before project close. Grouped by project in pipeline order.

This is Sophia's confirmed call and a formal SOP rule: when an item has a named activation point, it goes here, not to Pending AAR. Deferred Named cross-references the LHF list but does not own project details or duplicate LHF content. LHF is Jay's domain.

**3. Deferred No Home**
Items deferred with no named activation point yet. Parked here for disciplined holding — not a dumping ground. At every Pending Changes review, run a quality check: does any Deferred No Home item now have a known activation point? If yes, reclassify to Deferred Named.

**4. Notes & Objectives**
Future-use section. Fills as live projects accumulate purpose, goals, and ongoing operator notes. Currently a placeholder — expected to grow once real projects are underway with significant tracked scope.

**5. Pending AAR**
True post-project items only. Applied after project closes at AAR. Quality check at every review: "Does any Pending AAR item actually have a known activation point before project close? If yes, reclassify to Deferred Named."

This section is not for items with an unclear home — that is Deferred No Home. Pending AAR is specifically for items that will not and should not be applied until the AAR review confirms them.

**6. Behavioral Standards Active**
Active behavioral standards currently being tracked on the list — behavioral rules that have been established operationally but whose SOP or formal documentation is still pending. Items move off this section when the formal documentation is complete.

### Format

- **Legend at top** — summary entries only. Every legend entry references this SOP as the source of truth. The legend does not define anything.
- **Quick Stats line** — placed between the Legend and the Active section. One-line snapshot of current section counts (e.g., `Active: 2 | Deferred Named: 5 | Deferred No Home: 1 | Notes & Objectives: 0 | Pending AAR: 12 | Behavioral Standards Active: 1`). Purpose: at-a-glance context without opening every section.
  - **Two-phase behavior (by design):** The Quick Stats count is pre-adjusted at scrub time — when an item's status changes (e.g., to `Closed`), Sophia updates the count immediately to reflect the new state. When the physical transfer to Completed Changes runs at session close, the counts do not change again — they were already adjusted. A reader comparing Quick Stats before and after a transfer batch will see no numerical change. This is correct and intentional: the Quick Stats always reflect the current active state of the list, not the pending transfer batch.
- **Maintenance footer** — at the bottom of the file. Records last update date, session, and backwards sweep completion.

### P/M Lead Pending List — Ownership, Location & Routing

This is the standing framework rule for any project that runs with a P/M Lead (or P/M Lead group). It formalizes who owns a P/M Lead's pending list, where it lives, what it is named, what routes to it versus to Sophia's, and the guardrail that keeps it discoverable.

**1. Ownership.** Every P/M Lead owns a dedicated pending list for their own coursework and project-execution items. The P/M Lead maintains it; Sophia does not manage a P/M Lead's list day to day. This is additive to Sophia's role — Sophia still owns the project-level Pending Changes List for all structural and source-material scope (see routing below).

**2. Location (home).** The P/M Lead's pending list lives **in the P/M Lead's own folder** (the Project Lead Personal Folder established under HR20), alongside the project soul and master deliverable summary.
- **No-lead fallback:** If a project has *no* P/M Lead, there is no separate list — those items live in Sophia's Pending Changes List in her COO Folder → Operational Files, as normal. The P/M Lead list exists only when a P/M Lead exists.

**3. Naming (locked convention).** The file is named `[lead]-pending-changes.md` — lowercase, the P/M Lead's name, hyphenated (e.g., a lead named "Casey" → `casey-pending-changes.md`). One list per P/M Lead. For a P/M Lead *group*, each lead owns their own `[lead]-pending-changes.md` in their own letter-prefixed folder (HR20 multi-lead convention).

**4. Two-tier routing.** What goes where is determined by item type, not by who surfaced it:

| Item type | Routes to | Owner |
|-----------|-----------|-------|
| Coursework / project-execution items (the P/M Lead's actual deliverable work within their project scope) | The P/M Lead's `[lead]-pending-changes.md` | P/M Lead |
| Source-material and structural / MIP changes — CLAUDE.md, either Master Guide, any Initial Package template, project architecture, governance, or any change that reaches beyond the single project's deliverable scope | Sophia's Pending Changes List | Sophia |

When in doubt, the test is: *does this change anything outside the P/M Lead's own project deliverable?* If yes → Sophia's list. If it is purely the Lead's own execution work → the Lead's list. Sage reviews both lists.

**5. Index-pointer guardrail (mandatory).** Whenever a P/M Lead pending list is created, an index pointer to it **must** be added to the project file index in the same setup pass — naming the file, its owner, and its home folder. A P/M Lead list with no index entry is a discoverability gap (Gotcha Entry 27 / 29 pattern — a file an agent cold-starting cannot find is effectively invisible). The pointer is not optional and is not deferred: created list, created pointer, same pass.

---

## List 2 — Sophia's Completed Changes

### Purpose

Archive for items that have moved off the Pending Changes List. **Not loaded at session start.** Loaded on demand only. This is a deliberate context window decision.

### Internal Sections (in this order)

**1. Completed**
Items fully applied and verified. No remaining action required.

**2. Removed**
Items explicitly removed from scope — confirmed decision not to proceed, not just deferred.

**3. Not Used / Closed**
Items superseded, retired, or no longer applicable. A reason is required on each entry. Distinguish from Removed: Removed is an active decision to not do the thing; Not Used / Closed is a passive retirement (e.g., the item became irrelevant, was superseded by a broader change, or the approach changed).

### Format

- **Legend at top** — same structure as Pending Changes legend. SOP is the source of truth.
- **No Quick Stats line** — this file is not a live operational queue; at-a-glance count is not needed.
- **Maintenance footer** — records last transfer date and session.

---

## Transfer Protocol — Pending Changes to Completed Changes

This protocol governs when and how items move from the Pending Changes List to the Completed Changes List.

### Trigger for Transfer

An item is eligible for transfer when its status reaches a terminal state — meaning no further action is required on the item itself:

| Status on Pending Changes | Destination in Completed Changes |
|---------------------------|----------------------------------|
| `Complete ✓` | Completed section |
| `Closed` | Not Used / Closed section |
| `COMPLETE ✓` (variant notation) | Completed section |
| `CLOSED` (variant notation) | Not Used / Closed section |
| Items explicitly removed from scope | Removed section |

Items with `Pending AAR`, `Active`, `Moved to [project]`, or `Applied — Jay approved ✓` status are **not** eligible for transfer. They remain on the Pending Changes List until they reach a terminal state or are explicitly retired.

**Note:** `Applied — Jay approved ✓` items are mid-project overrides that remain on the list until AAR review confirms the application. They do not transfer until the AAR explicitly closes them.

### Who Confirms

Transfer requires Sage's review before Sophia executes. Sophia identifies the eligible items and presents them to Sage for confirmation. Sage approves the batch. Sophia executes.

### Transfer Batching — Confirmed Rule

**Confirmed:** Transfers happen at session close, Jay's explicit request, major COHK projects, and AAR. No mid-session transfers. Compacts are not transfer triggers by default.

**Project-level exception:** A project's session-close or compact-wrap-up SOP may specify compact close as an additional transfer trigger, with explicit operator approval documented in that SOP. When this exception is in effect, the project-level SOP governs — the default (compacts not triggers) applies to all other projects.

**Rationale:** Session close fires once per session at a natural break point — preventing multiple transfer passes within a single session. Compacts are context-management events that can fire multiple times mid-session; treating them as transfer triggers would violate the spirit of the no-mid-session rule. COHK projects and Jay's explicit requests are appropriate flex points with clear authorization. AAR is the final project-close sweep.

### Transfer Execution

1. Sophia identifies all terminal-status items on the Pending Changes List.
2. Sophia presents the batch to Sage with a one-line summary per item (what it is, its terminal status, destination section).
3. Sage confirms the batch.
4. Sophia moves each item to the correct section in Completed Changes — copying the full item entry, not summarizing.
5. Sophia removes the item from Pending Changes.
6. Sophia updates the Quick Stats line on Pending Changes and the maintenance footer on both files.

---

## List 3 — Gotcha.md

**Governing SOP:** Sophia's COO SOP, Step 6.

**Purpose:** Per-project operational watch list. Captures what went wrong, why, the fix applied, and the standing watch-out rule. Not a blame list. Sophia creates this file at project activation and maintains it throughout.

**Current location:** Sophia's COO Folder → Operational Files (`Gotcha.md`)

**Session-start load:** Yes — loaded every session.

For entry format, entry quality standard, AAR review process, and permanent location note: see COO SOP Step 6. That section governs. This pointer is the extent of List Management SOP coverage for Gotcha.md.

---

## List 4 — Team Lessons Log

**Governing SOP:** Sophia's COO SOP, Step 5.

**Purpose:** Team-wide lessons capture. Sophia manages it for the whole team and is also a contributor. Any agent or Sage routes lessons through Sophia. Sophia logs them in standard format. Promotion decisions belong to Sage (and Jay at AAR) — not to Sophia.

**Location:** Sophia's COO Folder → Teams Lesson Log - TLL (`Team-Lessons-Log.md`)

**Session-start load:** No — consulted at session close, compact close, and on demand.

For logging format, dual-role protocol (manager + contributor), promotion pipeline, and AAR review: see COO SOP Step 5. That section governs. This pointer is the extent of List Management SOP coverage for the Team Lessons Log.

---

## Status Labels — Source of Truth

These are the confirmed status labels for the Pending Changes List. The legend in the actual list file summarizes them. This SOP defines them.

| Status | When to Use |
|--------|-------------|
| `Active` | Item is currently being worked on this session. Can be applied to any item when work begins; reclassified when work pauses. |
| `Pending AAR` | True post-project item. Applied after project closes at AAR. Not for items with an unclear home — that is Deferred No Home. |
| `Moved to [project] — build input for [agent]` | Known activation point before project close. Used for items that belong to a named future project or agent build. |
| `Applied — Jay approved ✓` | Emergency mid-project operator override. Flagged for AAR review. Item stays on the list until AAR review closes it. |
| `Complete ✓` | Item fully applied, verified, done. Ready for transfer to Completed Changes. |
| `Closed` | Superseded, retired, or no longer applicable. Note reason on the entry. Ready for transfer to Completed Changes — Not Used / Closed section. |

**Status assignment rule:** Sophia assigns status — not the agent surfacing the item. Source agents surface items and provide context. Sophia categorizes and assigns.

---

### Hard Rule 19 — Three-Altitude Problem-Solving

Before retrying or escalating any blocked task, Sophia classifies the problem by altitude:

- **Task level** (within her lane and current scope): Apply the two-round rule. Round 1 — try a new approach. Round 2 — Sage and Sophia brainstorm a new direction together, attempt once. If Round 2 fails — stop. Report to Sage: what was tried, what happened, current state. Never retry a documented failed approach.
- **System level** (affects the overall approach, other agents, or design decisions beyond Sophia's lane): Surface to Sage immediately. Do not apply the two-round rule first.
- **Vision level** (touches end goals or company direction): Sage escalates to Jay.

**Resource access:** Master Library first. Information-only research → submit request to Sage, routed to Rose (Soren not required). New external deployable resource → full pipeline (Sage → Rose → Soren → Lexi). Never grind at the wrong altitude.

---

## Edge Cases

| Situation | Response |
|-----------|----------|
| Item surfaced without a clear status | Sophia assigns the most appropriate status based on context. If genuinely ambiguous, document as `Pending AAR` temporarily and flag for Sage's review at the next check-in. |
| Pending Changes List exceeds ~20 active items | Run an ad-hoc review immediately. Any items to close, retire, or reclassify? Flag volume risk to Sage. |
| Completed Changes List is requested mid-session | Load it. Use it. Do not preload it speculatively going forward. |
| A `Pending AAR` item is discovered to have a known activation point | Reclassify to `Moved to [project] — build input for [agent]`. Note the reclassification date and session. |
| A `Deferred No Home` item acquires a home | Reclassify to Deferred Named. Update the Quick Stats line. |
| Two items on the list describe the same underlying change | Merge them into one entry. Document the merge with a note. Surface to Sage if the merge changes scope. |
| An item was applied mid-project without queuing first | Source material freeze bypass. Surface to Sage immediately — what was changed, when, who changed it, which files are affected. This is a project security catch. Sage assesses. |
| Backwards sweep finds a session summary item not on the list | Add it retroactively with the originating session noted. No blame — gaps happen. Capture it cleanly. |
| Cross-reference finds a list item that was applied but still shows old status | Update the status immediately. Note the correction. If the item is now terminal, add it to the next transfer batch. |
| PARTIAL item — part done, part pending AAR | See Open Design Questions. Current approach: land in Pending AAR with a status note describing what is done vs. what is pending. Flag at next review for resolution per design question. |

---

## Reporting

**Default:** Concise and precise. At session close and compact, Sophia rolls up list status to Sage: new items added, status changes made, any items flagged for Sage's attention.

**At Pending Changes review:** Report the outcome of the review to Sage — items reclassified, volume note if applicable, quality check findings.

**At AAR:** Full Pending Changes List presented to Sage and Jay for review. Jay decides which items are approved and applied. Sophia determines who needs to be present per COO SOP Step 15.

**Verification note:** Sophia's status reports ("list is current," "no new items," etc.) are inputs to independent verification — not substitutes for it. Reports are written to make verification easy: specific, complete, and checkable.

---

## File Organization

| File | Location | Session-Start Load | Notes |
|------|----------|--------------------|-------|
| Sophia's Pending Changes (List 1) | COO Folder → Operational Files (`sophia-pending-changes.md`) | Yes — every session | Active operational queue; Sophia manages |
| Sophia's Completed Changes (List 2) | COO Folder → Operational Files (`sophia-completed-changes.md`) | No — on demand only | Archive; context window decision |
| Gotcha.md (List 3) | COO Folder → Operational Files (`Gotcha.md`) | Yes — every session | Governed by COO SOP Step 6 |
| Team Lessons Log (List 4) | COO Folder → Teams Lesson Log - TLL (`Team-Lessons-Log.md`) | No — on demand | Governed by COO SOP Step 5; team-wide |
| This SOP — Sage/Agent version | COO Folder → COO Suite (`Sophia-List-Management-SOP.md`) | No | Source of truth for all list definitions |

**Note on Completed Changes path:** The path above is Sophia's proposed placement — consistent with Pending Changes location and logical grouping. Flag for Sage confirmation before the file is created if this placement has not been explicitly confirmed.

---

## Design Decisions — Resolved

**Design Question 1 — PARTIAL item handling**

**RESOLVED — Session 115.** Status note approach confirmed as the intended design. When an item is partially complete, it lands in Pending AAR with a status note distinguishing what is done from what is pending. No split rule. The Edge Case entry above documents the current behavior — it stands as written. Revisit only if the status note approach proves insufficient in practice.

---

**Design Question 2 — Transfer batching schedule**

**RESOLVED — Session 115; REVISED — Session 116.** Initial resolution was compact/AAR only. Revised in Session 116 after recognizing that compacts can fire multiple times within a single session, creating unintended mid-session transfers. New confirmed triggers: session close, Jay's explicit request, major COHK projects, AAR. Compacts explicitly removed as a trigger. See Transfer Batching section above for full rationale.

---

## Version Log

| Version | Date | What Changed | Why |
|---------|------|-------------|-----|
