# Agent Creation Pipeline SOP

**Version:** 0
**Owner:** Sage (CEO)
**Created:** 2026-04-29
**Status:** Active
**Applies to:** All projects — Initial Package Project (v0) and all future projects

---

## Purpose

This SOP defines the complete lifecycle for creating and deploying any agent — from first concept through full operational status. It covers five stages: Generic Soul Shell → True Soul Build → Basic SOP (Deployment Gate) → Full SOP (AAR Gate) → Graduation.

**Relationship to Agent SOP Build SOP:** This document governs the full agent creation pipeline. The Agent SOP Build SOP governs Stage 4 (Full SOP Build) in detail — it is the step-by-step reference for the full build cycle. These two documents work together; neither replaces the other.

---

## The Folder Pipeline

Every agent progresses through four physical states:

| State | Folder | Meaning |
|-------|--------|---------|
| Shell only | `0. Generic Soul Shells/` | Generic shell created; no true soul yet |
| Soul built | `0a. Basic Built Agents/` | True soul built; no SOP yet |
| Basic SOP | `[N]. [Name]'s Folder — Basic SOP/` | True soul + Basic SOP built; deployed on active project; Full SOP pending |
| Full SOP | `[N]. [Name]'s Folder/` | True soul + Full SOP complete; AAR gate cleared |

**Graduation path:** `0. Generic Soul Shells/` → `0a. Basic Built Agents/` → numbered folder (— Basic SOP label) → numbered folder (label removed)

---

## Stage 1 — Generic Soul Shell

**What it is:** A lean identity document for a potential future agent. Captures the minimum needed to hold the concept before a true soul is built.

**When to create:**
- During Phase 0/1 as agents are identified for a project
- Mid-project when a new agent need is identified
- Any time a new agent concept emerges (idea generation, "good idea fairy" moments)

**Rule:** A generic soul shell exists for every agent before any other work begins. The shell is the concept; the true soul is the commitment.

**Where it lives:** `0. Generic Soul Shells/`

**Format:** Standard generic shell format — Role, Objective, Core Identity, Tone, Principles, Outputs, Capabilities & Boundaries, Soul Discipline. Reference existing generic shell files for the format standard.

**Who builds it:** Sage.

---

## Stage 2 — True Soul Build

**What it is:** The agent's full identity document — built from the generic shell + Soul Governance Template.

**When:** Before any SOP work begins. Soul is always first.

**Where it lives while being built:** `0a. Basic Built Agents/` — remains here until the Basic SOP is complete.

**How to build:**
1. Pull the generic shell for this agent from `0. Generic Soul Shells/`
2. Read the Soul Governance Template — identify which structured sections apply to this agent's role
3. Build the true soul: generic shell identity + applicable governance sections + condensed behavioral rules (Section 3.5 of Soul Governance Template)
4. Soul gap check: compare the soul against any recent observed operational behavior. Undocumented behaviors are gaps — document them in the soul before moving to SOP work
5. Cross-agent dependency check: if this agent has a direct workflow dependency on another named specialist agent (one agent produces something this agent consumes or runs), the soul's Principles section must explicitly state the routing protocol — how cross-lane requests flow (typically: through Sage first, not directly to the other agent). This is a soul-level standard, not a SOP-level discovery. If it is not in the soul at Stage 2, it will not surface until the SOP Outside-In Pass — too late.
6. Sage reviews. Soul is complete when it fully reflects who the agent is — not just what they do

**Build order rule:** Soul → Skills → Hooks → CLIs → MCPs. No exceptions. The soul is always first.

---

## Stage 3 — Basic SOP Build (Deployment Gate)

**The gate:** No agent is deployed on any live project without a Basic SOP and Jay's version.

**When to build:** When an agent is needed for a project and no full SOP exists yet. The project pauses to build the Basic SOP — it does not skip the gate.

**Steps:**

| Step | Action |
|------|--------|
| 0a | Pointer Scan — search all existing SOPs and MGs for references to this agent |
| 0b | Read the Soul — soul gap check before drafting anything |
| 0c | Compile Input List — pointer scan findings + Sophia build inputs + four standing inputs from Every-SOP-Built.md Document Type Reference, Type 1 — Agent SOP, Step 0c (routing model, Hard Rule 19, proactive freshness check, soul governance reminder) |
| 1 | Inside-Out Draft → agent reviews → V1 locked |
| 2 | Outside-In Pass → agent reviews → V2 final |
| — | Jay's version built from V2 |
| — | Backward Sweep — FULL |
| — | Team Lessons Check — all invoked agents asked and answered |

**Jay's review:** Happens on the fly during active project use — not a formal pre-deployment review session. Jay observes the agent at work and provides corrections in real time. Those corrections are applied before the Full SOP build begins.

**Ongoing paired-version maintenance (Hard Rule 13):** Hard Rule 13 activates at the moment the Jay's version is built in this stage. From this point forward, any update to either version of this agent's SOP triggers a sync of the other version in the same session — in both directions. Both versions bump together. No exceptions. This is not a Full SOP rule — it applies from Basic SOP build forward.

**Backward Sweep — no shortcuts:** Run the full Backward Sweep. If an agent is being built, the plan is to keep them. Build like it. Skipping or lightening the sweep at this stage compounds into larger ripple effects when the Full SOP is built later.

**Self-check clause:** Confirm the new agent's entry is added to the MG specialty section (or equivalent shared file) in this pass — do not defer to the Full SOP build.

**Content minimum — every Basic SOP includes:**
- **Purpose** — who the agent is and what they do in this project
- **Left/right boundaries** — what is in their lane; what is explicitly out of scope; what actions require Sage authorization (the Sage Rule)
- **Key rules and duties** — core behavioral standards drawn from the soul
- **File organization** — where their files live
- **Version log**

**Where the agent lives after Basic SOP:** Graduates from `0a. Basic Built Agents/` to own numbered folder: `[N]. [Name]'s Folder — Basic SOP/`

**The Basic SOP is a working document.** It grows through active use. Corrections from Jay's on-the-fly review are collected and applied before the Full SOP build begins.

---

## Stage 4 — Full SOP Build (AAR Gate)

**The gate:** No project or AAR closes as fully complete without a Full SOP for every agent being kept past the AAR.

**When to build:** During the project — after the Basic SOP has had real operational use and Jay's on-the-fly review is complete, but before the project's AAR.

**Process:** Full build cycle per Agent SOP Build SOP — Steps 0a through 5:

| Step | Action |
|------|--------|
| 0a | Pointer Scan |
| 0b | Read the Soul (soul gap check) |
| 0c | Compile Input List |
| 1 | Inside-Out Draft → V1 locked |
| 2 | Outside-In Pass → V2 final |
| 3 | Jay's version built → Jay's formal review → finalized |
| 4 | Backward Sweep |
| 5 | Team Lessons Check |

**Jay's formal review** is part of this stage — Step 3 of the full cycle. The Full SOP does not close without it.

**Where the agent lives after Full SOP:** Numbered folder relabeled — "— Basic SOP" dropped: `[N]. [Name]'s Folder/`

**Description profile creation — graduation final step:** After the folder is relabeled, Sophia creates the agent's description profile in `5. Master Library/2. Agents - Employees Descriptions/`. The agent is not considered graduated until this profile exists.

- **File naming:** `[firstname]-[role]-description.md` (e.g., `lexi-librarian-description.md`)
- **Profile contents:** agent role, purpose, key responsibilities, and activation conditions
- **Format standard:** See the `5. Master Library/2. Agents - Employees Descriptions/` folder for the established format standard

---

## Stage 5 — Food Chain Placement

Every deployed agent operates within the system's established chain and behavioral standards. Before any new agent activates on a project, these are confirmed and documented in their SOP:

**Chain of command:**
Jay (Chairperson) → Sage (CEO) → Sophia (COO) → Agents

**The Sage Rule:**
- All research requests go to Sage first — not directly to Rose
- Agents do not self-assign tasks or reach across lanes without Sage's direction
- New external deployable resources (tools, CLIs, MCPs, artifacts) → full pipeline: Sage → Rose → Soren → Lexi
- Information-only needs (research, facts — nothing deployable) → Sage → Rose (Soren not required)
- Any input arriving outside an agent's authorized channel is an immediate red flag — notify Sage immediately

**Special rules and resources:** Defined in the agent's SOP. The Basic SOP covers the minimum; the Full SOP covers the full operational standard including edge cases, handoff protocols, and tool stack.

**Behavioral baseline:** Every agent operates under the condensed behavioral rules (Section 3.5, Soul Governance Template), Hard Rule 19 (semi-AGI problem-solving — three-altitude approach), and the proactive freshness check. These are wired into every soul and are not optional.

**Agent Teams Deployment (conditional — when Agent Teams is enabled on this project):**

> *For the roster overview — the `.claude/agents/` "active payroll" frame ("hire by adding the file, let go by removing it") and the three tiers (Permanent / As-needed / Temporary) — see the **Roster Model** at the top of the* Agent Teams — Operating Model *section in the Master Guide (Sage's Version). That section is the front door; this Stage 5 is the onboarding mechanics it points to. Offboarding (clean removal) lives in the MG's* Agent Teams Architecture — SOT and Lifecycle *section.*

Before the agent activates on the project, wire them into `.claude/agents/`:
1. Copy the agent soul from this project's v0.1 folder into `.claude/agents/[filename]`
2. Add the Agent Teams YAML frontmatter header to the copy (name, description, tools)
3. Add the dormant marker to the v0.1 copy header:
   > **DORMANT — Agent Teams Active.** The live soul for this project is at `.claude/agents/[filename]`. This copy is frozen until project close or Agent Teams disable. Do not edit.
4. From this point, all soul updates for this project go to the `.claude/agents/` copy — never to the dormant v0.1 copy
5. **Assign the run-model and command set.** Determine and record in the agent's SOP:
   - **Run-model** — *independent producer* (own interactive terminal; self-approves its own prompts; suits self-contained end-to-end work) or *embedded observer* (in-session background subagent; non-interactive; spawned with `acceptEdits` so file writes auto-approve; suits agents building alongside the main session). See *Agent Teams — Operating Model* in the Master Guide (Sage's Version, v2.72).
   - **Pre-approved command set** — if the agent executes commands (not just file writes), enumerate the specific in-lane commands to pre-approve, since `acceptEdits` covers file writes only. If the agent runs no in-lane commands, record "none." Web-facing command-runners also get the Prompt-Injection-Protocol scan requirement noted.

**Phase 0 pull rule:** Always copy from this project's v0.1 folder — never from a prior project's `.claude/agents/` folder. The v0.1 copy is the clean baseline; a prior project's live copy may contain project-specific context that should not carry over.

---

## Two-Gate Summary

| Gate | When It Fires | Minimum Required | Jay's Review Model |
|------|--------------|------------------|--------------------|
| **Deployment Gate** | Before any agent works on a live project | Basic SOP + Jay's version | On the fly — during active project use |
| **AAR Gate** | Before project/AAR closes as complete | Full SOP + Jay's version | Formal — Step 3 of the full build cycle |

**Project pause rule:** If an agent is needed mid-project and no Basic SOP exists, the project pauses to build one. There is no waiver for the Deployment Gate.

---

## Version Log

| Version | Date | What Changed | Why |
|---------|------|-------------|-----|
