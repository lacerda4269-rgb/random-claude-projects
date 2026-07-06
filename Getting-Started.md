# Getting Started

**Owner:** Sage (CEO)
**Status:** Active — Item 38 (Phase 0 SOP Wiring Pass) complete — Session 192
**Last Updated:** 2026-06-23 (Sterilization pass — canonical package name alignment)

---

## What This Package Is

The Master Universal Initial Package (MUIP) is a ready-to-use project launch system. Every new project starts by copying this blank version — the folder structure, SOPs, blank templates, and this guide all come pre-built. Nothing needs to be built from scratch.

**The clean-blank rule:** Never modify the Blank directly. Copy it into the new project's folder. The Blank stays clean. The project copy gets used, filled in, and built out. At project close, the AAR decides what — if anything — gets applied back to the Blank to improve future projects.

---

## Before You Start Phase 0

Confirm these before running the activation sequence:

- [ ] New project folder created with the copied MUIP content
- [ ] GitHub repository created for the new project
- [ ] Project name decided
- [ ] Initial team roster known (Sage is always present; specialty agents identified where possible)
- [ ] P/M Lead designated (if applicable) — if assigned, create `[N]. [Name]'s Folder (Project Lead Personal Folder)/` at the top level alongside the CEO and COO folders before activation begins. See **Project Soul Locations** below. Temporary P/M Lead: add to `.claude/agents/` only if parallel runs are required. Brief required only on first introduction — not on every session.
- [ ] P/M Lead pending list created (if a P/M Lead is designated) — pull `[lead]-pending-changes (Blank Template).md` from `6. Blank Universal Templates/`, fill the name, and place it in the P/M Lead's folder as `[lead]-pending-changes.md` (lowercase, hyphenated). **In the same pass, add an index pointer** to `project-file-index.md` naming the file, its owner, and its home folder — the list is not done until the pointer exists. **If no P/M Lead is designated, skip this — Sophia's Pending Changes List serves the whole project.** Full rule: Hard Rule 20 + `Sophia-List-Management-SOP.md` → "P/M Lead Pending List — Ownership, Location & Routing."

---

## Phase 0 Activation Sequence

All blank templates live in `6. Blank Universal Templates/`. Pull the blank, fill it out, and place the completed file in its destination. The blank always stays in `6.` unchanged — do not modify originals.

---

### Section 1 — CEO Soul Setup

**Templates to activate:**

| Template | Filled Name | Destination |
|----------|-------------|-------------|
| `Project-Soul (Blank Template).md` | `Sage-project-soul.md` | `1. Sage's CEO Folder/0. Sage's CEO Project Soul/` |
| `project-file-index (Blank Template).md` | `project-file-index.md` | `1. Sage's CEO Folder/` |
| `project-navigation-map (Blank Template).md` | `project-navigation-map.md` | `1. Sage's CEO Folder/` |

**How to fill:**
- **`Sage-project-soul.md`:** Sage fills this. End goal, core rules, agent roster, involvement scale, session management. See the template's section prompts. This is the CEO project soul — Sage's operating layer for this specific project.
- **`project-file-index.md`:** Sage populates the master file registry — every key file, its location, and its owner. Grows throughout the project.
- **`project-navigation-map.md`:** Sage builds the project vocabulary, trigger list, path log, and current snapshot. The team's shared living reference throughout the project.

**`ME - Jay.md`:** Travels pre-filled — do not copy from `6. Blank Universal Templates/` for this file. It is already present in the CEO Project Soul folder.

---

### Section 2 — Session Records

**Templates to activate:**

| Template | Filled Name | Destination |
|----------|-------------|-------------|
| `Session Summary (Blank Template).md` | `Session Summary.md` | `1. Sage's CEO Folder/1. Session Summary/` |
| `Session Summary Index (Blank Template).md` | `Session Summary Index.md` | `1. Sage's CEO Folder/1. Session Summary/` |

**How to fill:**
- Both files: Sophia creates the structure at project open and writes the first entry at the end of Session 1. Leave blank at activation; Sophia fills at session close. Newest-first format — most recent session at the top.

---

### Section 3 — COO Setup

**Templates to activate:**

| Template | Filled Name | Destination |
|----------|-------------|-------------|
| `Gotcha (Blank Template).md` | `Gotcha.md` | `2. Sophia's COO Folder/1. Operational Files/` |
| `Project Resources Log (Blank Template).md` | `Project Resources Log.md` | `2. Sophia's COO Folder/1. Operational Files/` |
| `sophia-pending-changes (Blank Template).md` | `sophia-pending-changes.md` | `2. Sophia's COO Folder/1. Operational Files/` |
| `sophia-completed-changes (Blank Template).md` | `sophia-completed-changes.md` | `2. Sophia's COO Folder/1. Operational Files/` |

**How to fill:**
- **`Gotcha.md`:** Sophia creates at project open. No entries yet — structure is ready; entries accumulate as the project runs. Read every session start; never re-read post-compact. CEO is accountable for its health and accuracy.
- **`Project Resources Log.md`:** Sophia creates at project open. Tracks all Skills, Hooks, CLIs, MCPs, and Plugins acquired or built during the project.
- **`sophia-pending-changes.md` and `sophia-completed-changes.md`:** Sophia creates both at project open. Both start empty — they fill as the project generates source material changes to track.

**Additional item built per project on spin-up (not from a blank template):**
- **`internal-build-record-Jay.md`:** Sophia creates this in `2. Sophia's COO Folder/0. Sophia's COO Suite/` alongside the pre-loaded `internal-build-record.md`. This is the Jay-facing version of the internal build record — written in plain language for Jay's reference. Created at Phase 0 open.

**Jay's Project Office** — `3. Jay's Project Office/` is Jay's input zone for this project. No activation required — it starts empty. Jay places reference documents, inputs, and materials for the team to work from throughout the project.

---

### Section 3a — Agent Teams (Teammate Mode) Setup

Agent Teams is enabled going forward on all projects. This step wires Sophia (and any assigned P/M Lead) into `.claude/agents/` so Claude Code can spawn them as subagents.

> **Prerequisite — one-time global setup:** Agent Teams requires `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` in `~/.claude/settings.json` (set once globally, never per project). In Claude Code `/config`, this feature shows as **"Default Teammate mode"**. On Windows, set display to **in-process** — split-pane requires a standalone terminal and won't work in VS Code or Windows Terminal.

**Sophia (required on every project):**

1. Copy `sophia-coo.md` from `2. Sophia's COO Folder/0. Sophia's COO Suite/`
2. Add the Agent Teams YAML frontmatter header to the copy (name, description, tools)
3. Place the copy in `.claude/agents/sophia-coo.md` at the project root

The copy in `.claude/agents/` is Sophia's **live soul** for this project. The original in her COO Suite folder is the **dormant soul** — it stays unchanged until project close, when any deltas from the live copy are reviewed and applied back. See Session-Close-SOP.md for the soul sync step.

**P/M Lead (conditional):**

Add the P/M Lead to `.claude/agents/` ONLY if parallel runs are required for that lead's work. If parallel runs are not needed, no `.claude/agents/` entry is created.

Brief rule: a brief is required ONLY when bringing in a new or temporary P/M Lead for the first time on this project. A long-term P/M Lead established at Phase 0 or Phase 1 does not need a brief on subsequent sessions.

**Agent-activation trigger map (on-demand residency — the forgotten-agent guardrail):**

Only Sophia ships live every session. Every other agent is **on-demand** — pulled from the Soul Folder when the work calls for them, and spun down after. Activation fires on a **work-trigger** OR on **Jay's direct call** — whichever comes first. Use this map so no needed agent is forgotten:

| Trigger (work need) | Activate |
|---------------------|----------|
| Research / internet fact-finding | **Rose** |
| Build a Skill / Hook / CLI / MCP / Plugin | **Cosmo** |
| An external / deployable resource is involved | **Soren — BEFORE use** (security clearance is mandatory and comes first; nothing external is touched, built on, or cataloged until Soren clears it) |
| Catalog a cleared resource into the Master Library | **Lexi** |
| Specialty work (NinjaTrader / TradingView / Python / video / coursework) | the matching specialty agent (Nick / Todd / Pete / Vicky / Feynman) |

**+ Jay-as-trigger:** any of the above also activates when Jay calls for it directly, even without the matching work-trigger surfacing first. **Soren-before-deploy is non-negotiable** — it holds regardless of who triggered the work or how urgent it is.

---

### Section 4 — Lessons & Tracking

**Templates to activate:**

| Template | Filled Name | Destination |
|----------|-------------|-------------|
| `Team-Lessons-Log (Blank Template).md` | `Team-Lessons-Log.md` | `2. Sophia's COO Folder/3. Teams Lesson Log - TLL/` |
| `lessons-template (Blank Template).md` | `lessons.md` | `.claude/projects/[project-path]/memory/` |
| `status-board (Blank Template).md` | `status-board.md` | Project-defined active resources folder |
| `task-tracker (Blank Template).md` | `task-tracker.md` | Project-defined active resources folder |

**How to fill:**
- **`Team-Lessons-Log.md`:** Sophia creates at project open. No entries yet. Read every session start (same cadence as Gotcha.md).
- **`lessons.md`:** Sage creates it in the `.claude` memory folder for this project at project open (Claude Code creates this folder automatically — confirm it exists before placing the file; create manually if it does not). No entries yet. Project-scoped lessons only — global lessons go to `~/.claude/lessons_global.md` via hot path.
- **`status-board.md` / `task-tracker.md`:** Sage places them in the designated active resources folder (confirmed during Phase 0 setup). Sophia updates them throughout the project. (`task-tracker.md` is the canonical living task tracker; `status-board.md` is the status-story snapshot.)

---

### Section 5 — Project Initialization

**Templates to activate:**

| Template | Filled Name | Destination |
|----------|-------------|-------------|
| `CLAUDE (Blank Template).md` | `CLAUDE.md` | Project root — the folder Claude Code is opened in. Same level as `.claude/`, NOT inside it or any version subfolder. |

**How to fill:**
- **`CLAUDE.md`:** Sage fills this out. It is the project auto-loader — instructs Sage to read the project soul and Session Summary at every session start, eliminating the need for a manual wake-up prompt. Update whenever the project name, current phase, or core file paths change.
- **What it is not:** It is not Sage's global identity (that is `~/.claude/CLAUDE.md`). It is the project pointer file only — a lean connector between Claude Code and this project's operational files.

---

### Section 6 — Research Setup

**No template to pull — Rose's format standard travels with her soul.** As of the Session 265 residency change, `rose-report-format-standard.md` lives as Rose's source-of-truth inside her Soul Folder entry (`5. Master Library/1. Soul Folder/Rose the Researcher/rose-report-format-standard.md`). The old `(Blank Template)` staging copy was retired (Soul Folder SOT is authoritative).

**How to use:**
- When Rose is activated on-demand for a project, she confirms her format standard is current against the ML SOP (check for any updates since the last project). It is her reference document for all research reports produced during this project — no Phase-0 copy step is required.

---

### Section 7 — Trading & Python Deliverables (apply only if project produces these)

These templates apply only to projects that will produce NinjaTrader strategies, TradingView indicators, or Python deliverables. Skip this section if no trading or Python deliverable is in scope.

All templates below live in `6. Blank Universal Templates/` — same as every other section.

**Templates to activate (when applicable):**

| Template | Filled Name | Destination |
|----------|-------------|-------------|
| `technical-manual-template (Blank Template).md` | `[deliverable-name]-technical-manual.md` | Trading deliverable folder |
| `technical-manual-python-template (Blank Template).md` | `[deliverable-name]-technical-manual.md` | Python deliverable folder |
| `user-guide-template (Blank Template).md` | `[deliverable-name]-user-guide.md` | Deliverable folder |

**How to fill:** These are filled when the deliverable is ready for documentation — not at Phase 0. Pull the blank, fill in the deliverable name, and place in the deliverable's folder when the time comes. Sophia tracks these in `Project Resources Log.md`.

---

### Section 8 — Project Documentation Type Standard (Item 121)

Every document produced by the project is typed at Step 0 of its build cycle. The type is recorded in the document header.

**Document types:**
- **SOP** — executable procedure; describes what to do, in what order, and under what conditions
- **Reference Guide** — non-executable look-up; describes how something works or what it contains
- **Runbook** — step-by-step checklist for a recurring operation; confirms each step was done

**Project documentation format decision:**

| Project type | Primary deliverable format | Jay's version default |
|---|---|---|
| Technical project (code, strategy, indicator, script) | Technical Manual + User Guide (templates in `6. Blank Universal Templates/`) | User Guide = Jay's version equivalent |
| Non-technical / process project (SOPs, governance, onboarding) | Project SOP (agent version) | Visual workflow (Mermaid diagram) — default; plain-text Jay's version only when a genuine operational need exists |

**Visual-as-default rule (Hard Rule 13 — Item 121):** When building a new SOP for a non-technical process project, a visual workflow or flowchart (e.g., Mermaid diagram) is the default format for the Jay's version when it fully represents the SOP workflow. A separate plain-text Jay's version is built only when a genuine operational need exists for one. "One or both" is case-by-case at Jay's discretion — it is NOT a hard requirement to produce both. Sage documents the call at Step 0 of the build cycle.

---

## Project Soul Locations

Every project has two project-level soul documents. Before reading them, understand the soul architecture:

**The corporation/branch model:** `~/.claude/CLAUDE.md` is the corporate charter — Sage's universal identity, behavioral standards, and CEO role that apply to every project without exception. Each project soul is a branch incorporation: same CEO, same principles, scoped to one entity. The branch has its own team, rules, and scope; the corporation sets the identity and the floor. When the two appear to conflict, the corporation wins — the branch never overrides the charter.

**1. Sage's CEO Project Soul** — always exists on every project. Lives in `1. Sage's CEO Folder/0. Sage's CEO Project Soul/` as `Sage-project-soul.md`. Sage fills it at Phase 0 from `Project-Soul (Blank Template).md` in `6. Blank Universal Templates/`.

**2. P/M Lead Project Soul** — exists when a designated Project/Mission Lead is assigned. Lives in the P/M Lead's personal folder (`[N]. [Name]'s Folder (Project Lead Personal Folder)/`) as `[lead-name]-project-soul.md`. The P/M Lead fills it at Phase 0 from the same blank template.

Both souls are distinct from Sage's global identity at `~/.claude/CLAUDE.md`, which spans all projects and never changes.

**If no P/M Lead is designated:** No P/M Lead folder is created. Sage runs the project as CEO. The folder is created only when a lead is formally assigned — at Phase 0, during Phase 1, or at any point in the active project.

*(Full rule: Hard Rule 20. P/M Lead folder naming convention and escalation chain are in the global CLAUDE.md. Corporation/branch soul architecture: global CLAUDE.md is the corporate charter; project soul is the branch incorporation.)*

---

## For Cross-LLM Projects (Item 130)

If this project uses LiteLLM for cross-model cost management, complete this before declaring Phase 0 done:

- [ ] **LiteLLM cost threshold defined.** Agree on a per-session, per-phase, or total project budget limit before any LLM API calls are made. Document the threshold in `Sage-project-soul.md` (§3.3 Session Management) and notify Pete (if active) — Pete's soul references a project-defined threshold as a dependency.

---

## After Phase 0

When all applicable sections above are complete:
- All blank templates pulled, filled, and placed in their destinations
- Project soul complete
- GitHub repo exists and first commit pushed
- All session tracking files in place

Move to Phase 1 per the project soul and Master Guide. The first session close is the first real test of all these files — Sophia runs the session close SOP against them.

---

## First Spin-Up — Artifact Build Order

Two of the files built at Phase 0 are not one-time setup — they are consumed every session for the life of the project. The build-order linkage:

- **Phase 0 builds them:** `project-file-index.md` (the file catalog) and `project-navigation-map.md` (the vocabulary, triggers, path log, and current snapshot) are created during Phase 0 — Section 1 above covers how Sage fills each.
- **`Session-Start-SOP.md` consumes them every session thereafter:** the session-start sequence queries the project knowledge graph for current state and, when a gap needs the file catalog or the navigation layer, consults these two artifacts directly. They are reference artifacts the session-start procedure reads — they are not rebuilt each session.

The order matters: the artifacts must exist (Phase 0) before the procedure that reads them runs (every session start). On a brand-new project's very first session there is no graph and no Session Summary yet — that is a valid first-run state; the Session-Start-SOP fallbacks cover it. See `Session-Start-SOP.md` (in `1. Sage's CEO Folder/6. SOPs/`) for the full session-start procedure.

---

## The Clean-Blank Rule

> This blank package is the source of truth. Every future project copies it — the Blank is never used directly. When a project closes and the AAR runs, one question is always asked: "Did we discover anything that should make the next project start better?" If yes, apply it back to the Blank. That is the only time the Blank changes — through deliberate improvement, not mid-project edits.

---

## New Agent — What to Know

You are joining a new or active project — this section applies at any phase. This section gets you oriented fast. Read it once, know it, then go find your soul file.

---

**Chain of Command**

Jay (Chairperson) → Sage (CEO) → Sophia (COO) → You.

Jay sets direction and holds final authority. Sage translates that into phases, assignments, and decisions — she is your direct report line. Sophia is Sage's second in command; she owns documentation, operational health, and the session record. Your job is to execute your domain with full ownership and surface anything that affects the broader team upward, not sideways.

---

**Routing**

Research requests go to Sage — not to Rose directly. Sage applies a relevance check and routes if approved.

Escalation works at three levels:
- **Task-level blocker** — try a new approach (Round 1). Still blocked — brainstorm with Sage, try once more (Round 2). Still blocked — hold the task, report to Sage, wait.
- **System-level issue** — anything touching overall project design, another agent's lane, or a decision outside your scope — surface to Sage immediately. Skip the two-round rule.
- **Vision-level issue** — anything touching end goals or company direction — Sage takes it to Jay. Flag it and step back.

---

**Where to Find Your Files**

- **Soul** — your identity, principles, and boundaries. Know it before you start anything.
- **SOP** — your procedure. Follow it. If something in your lane is not covered, flag the gap to Sage.
- **Master Guide** — the team operating manual. Lives in `1. Sage's CEO Folder/2. Master Guides/`. Sage's version is the team reference. Jay's version is Jay's reference. Do not confuse the two.
- **Pending Changes List** — lives in Sophia's COO folder. Any change to source material you identify mid-project goes there, not into the file directly.
- **Involvement score** — set in the project soul. Check it before your first task. It defines how much Jay is in the weeds on your work — your operating latitude for the current phase.

---

**Standing Rules — Every Agent**

- First and second person in all dialogue. Never use the operator's name in conversation.
- Lane discipline: do your job. Do not create, edit, or build anything outside your domain.
- Surface findings and blockers to Sage proactively — do not sit on them and do not wait to be asked.
- Never guess on Jay's intent or direction. Stop, ask Sage, wait for a clear answer before proceeding.

---

*Phase 0 SOP Wiring Pass — Item 38 — Session 192*
*Cosmo design ruling (Session 192): Phase 0 file creation = manual SOP steps. Future skill candidate when project initialization triggers are stable — flag at Agent Onboarding.*
*Sophia drafts. Sage reviews. Jay confirms final content.*
*Section 8 added (Item 121 — Project Documentation Type Standard + visual-as-default rule) — Project 6 Batch 2, Session 203.*
*New Agent — What to Know section added (chain of command, routing, file locations, standing rules) — Session 232, P7 Sandbox.*
*Agent Teams wiring — Item 157 (P7 Gate List Item 1): Section 3a added (Agent Teams Setup); P/M Lead checkbox expanded; Project Soul Locations corporation/branch model added — Session 236, P7 Sandbox.*
*Agent Teams (Teammate Mode) — Session 252: Section 3a title updated; prerequisite block added (env var `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`, `/config` "Default Teammate mode" UI label, Windows in-process-only note). Env var enabled in `~/.claude/settings.json`.*
*First Spin-Up — Artifact Build Order section added (Item 161 — Session SOP Suite, D3) — Session 254. The one new linkage: Phase 0 builds project-file-index + project-navigation-map; Session-Start-SOP consumes them every session thereafter. Pointer to Session-Start-SOP added. No duplication of Section 1 (which owns how the artifacts are built). Per-environment edit (×3).*
*Sterilization pass (2026-06-23): package name aligned to canonical "Master Universal Initial Package (MUIP)" — competing "MIP" and "MC-IP" labels removed ("MC-IP rule" → "clean-blank rule"); leftover `99.` references swept to `6. Blank Universal Templates/`.*
*P/M Lead pending-list setup checkbox added to "Before You Start Phase 0" (Item 176 — HR20 universal rollout) — Session 261. When a P/M Lead is designated: pull `[lead]-pending-changes (Blank Template).md`, place as `[lead]-pending-changes.md` in the Lead's folder, add index pointer same pass; no-lead → Sophia's list serves the project. Cross-references Sage MG v2.75 / Jay MG v3.55 / Sophia-List-Management-SOP v1.11. Per-environment edit (×3).*
