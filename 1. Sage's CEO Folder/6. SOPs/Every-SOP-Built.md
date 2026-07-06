# Every SOP Built

**Version:** 0
**Owner:** Sage (CEO)
**Created:** 2026-05-09
**Status:** Active
**Replaces:** Agent-SOP-Build-SOP.md (archived Session 129)
**Applies to:** Initial Package Project (v0) and all future projects

---

## Purpose

This SOP defines the standard process for building any operational document in the project — agent SOPs, standard SOPs, pipelines, simple guides, master guides, and runbooks. The document type determines the source and standard sections; the core 9-step build cycle is universal.

The process ensures every document is built from its proper foundation, reviewed from both inside and outside its domain, checked by Jay before finalizing, and validated against all prior built documents before the work closes.

**Skills carve-out:** Skills have their own dedicated build pipeline. When a Skill is being built, use `Cosmo-Skill-Creator-SOP.md`. This SOP does not govern Skill construction.

---

## TodoWrite — Execution Sequences

**Before any execution sequence with 2+ steps that produces or changes something persistent, a TodoWrite task list is the first action.** Items are crossed off as each step is completed.

**Trigger test:** Does each step produce or change something that persists after the session? Yes → TodoWrite required. No → not required.

Excludes: session summary updates and compacting actions.

---

## The Cycle at a Glance

For every document build, in this order:

0. **Paired Version Decision** — confirm whether this document type gets a paired version; document the answer
0a. **Source Scan** — search all existing built documents for references to the new document
0b. **Identify & Read the Source** — identify the document type; read the source file before writing anything
0c. **Compile Input List** — combine source scan findings with Sophia's pending build inputs; check for type-specific standing inputs
1. **First Draft (Primary Perspective)** → primary reviewer reviews → corrections applied → V1 locked
2. **Second Pass (External Perspective)** → Sage adds outside view → primary reviewer agrees or refines → V2 final → paired version built from V2 (if Yes at Step 0)
3. **Review Gate** → Jay reviews document and paired version (if applicable) → corrections applied → last internal gate before Backward Sweep
4. **Backward Sweep** → all findings resolved → clear to proceed
5. **Team Lessons Check** → all invoked agents asked and answered → build closed

---

## Step 0 — Paired Version Decision

Before any drafting begins, confirm: does this document type have a paired version? Document the answer.

| Decision | What Happens |
|----------|-------------|
| **Yes** | The paired version is built at Step 2 (from V2 final). Hard Rule 13 applies from then on — both versions update together in every future session. |
| **No** | The build proceeds without a paired version. The decision is recorded — this is a deliberate documented choice, not a gap. A paired version can always be added later. |

**Judgment check — applies both ways:** If Jay says Yes but the document is simple enough that a paired version adds little value (or it already IS a plain-language document), push back with reasoning before building one. If Jay says No but the document is complex, governs a process Jay interacts with directly, or carries approval responsibilities he'll need to reference — make the case and try to change his mind. The call is Jay's; the pushback is Sage's responsibility.

The type of paired version depends on the document type — see the Document Type Reference below. For most documents, the paired version is Jay's plain-language version. For Simple Guides / Jay's Versions themselves, there is no paired version — they ARE the paired version, so Step 0 always returns No for this type.

**Why this step exists:** Undocumented gaps and alignment-sweep flags traced to the question never being asked upfront. This gate closes that gap — the decision is made and recorded before any work begins, not discovered after.

---

## Step 0a — Source Scan

Before writing anything, search all existing built documents for any reference to, mention of, or handoff involving the new document.

**What to look for:**
- References by name or role
- Handoff protocols that touch this document
- Constraints or rules that reference it
- Embedded markers in prior documents that the new document should address

**Who runs it:** Sage. Targeted pass — search for the document name and type across all built files. Not a deep read of every line.

**Output:** List of findings. Carry into Step 0c.

---

## Step 0b — Identify & Read the Source

What type of document are we building? This determines what the source is. See the Document Type Reference section for the source per type.

Read the source before drafting a single line. The document is built from its foundation — not from observed behavior or assumed scope. Starting anywhere else produces a document that describes what something does rather than what it is and why.

---

## Step 0c — Compile Input List

Combine two sources into one input list:

1. Findings from the Source Scan (Step 0a)
2. Pending build inputs from Sophia's Pending Changes (if applicable to this document)

For each build input, check whether the item text explicitly names other files for update. If yes, add those files to the build scope — they are updated in the same pass.

See the Document Type Reference for any type-specific standing inputs that apply at this step.

This combined input list drives what gets built into the document beyond the standard structure. Nothing from the list gets skipped without a documented reason.

---

## Step 1 — First Draft (Primary Perspective)

Draft from inside the document's domain — from the perspective of whoever operates it, executes it, or is described by it. Draw from the source file and the compiled input list.

Standard sections vary by document type — see Document Type Reference.

Once drafted, bring in the primary reviewer (see Document Type Reference for who this is per type). Primary reviewer identifies issues, gaps, or anything that doesn't match how the document reads from the inside. Apply all corrections. Lock as **V1**.

**Done when:** Primary reviewer has reviewed, all issues resolved, V1 locked.

---

## Step 2 — Second Pass (External Perspective)

Sage adds the outside view — what cannot be seen from inside the document's domain.

**What the outside-in pass typically surfaces:**
- Downstream implications
- Cross-document dependencies or handoff gaps
- System-level context visible from the orchestrator position
- Edge cases that only appear from outside

Primary reviewer reviews the outside-in additions. Agrees or refines. Result: **V2 final**.

If Step 0 returned Yes: build the paired version from V2 — not from V1. V2 is the complete, reviewed source.

---

## Step 3 — Review Gate

Jay reviews the document (and paired version if applicable). Corrections applied. If corrections require changes to the other version as well, update both before the Backward Sweep begins.

**Jay's review is the last internal gate.** The Backward Sweep does not begin until Jay has signed off.

---

## Step 4 — Backward Sweep

**Trigger:** Jay's review complete.

**Purpose:** Catch any ripple effects the new document introduces into prior built documents — clashing rules, gaps, stale references, scope conflicts, or handoff mismatches.

**Scope — targeted, not full reads:** Identify what the new document introduced (new rule, changed pipeline step, new boundary condition, new edge case). Check only the sections of prior documents that touch the same rule, pipeline, or boundary. Light scan of everything else.

**Order:**
1. The document just completed (+ paired version if applicable) — confirm they are in sync as a paired unit before sweeping outward
2. Prior documents of the same type — reverse order (most recent first). Each prior pair (full + paired version) is checked together as one unit
3. Related documents of other types that touch the same process or rule — checked after
4. Master Guides — checked last

Also sweep any files updated as part of this build beyond the primary document. Confirm they are internally consistent with the new document and with each other.

**Self-check clause:** After sweeping prior documents, check: are there any previously-built documents whose own placeholders in shared files (Master Guide standing team section, Phase 0 section, or equivalent) still show "to be built"? If yes — replace them with actual file references in this pass.

**Who runs it:** Sage. Pull an agent in only when a specific section of their document needs their direct input to resolve a finding. Not a team review — targeted and fast.

**Done when:** All findings resolved. No unresolved clashes, gaps, or stale references. Clear to move to Step 5.

---

## Step 5 — Team Lessons Check

**Trigger:** Any agent invoked during the build counts as an agent deployment. The check fires at each agent dismissal and at build close.

**When it fires:**
- After Step 1 — primary reviewer dismissed following V1 lock
- After Step 2 — agent dismissed following V2 final
- At build close — after Backward Sweep complete

Ask each invoked agent directly: did a lesson emerge from this work? Record the answer by name. "No lesson" is a valid result — but only when the agent gives it, not when Sage draws the conclusion on their behalf.

**Done when:** All invoked agents have been asked and answered. Responses recorded by name in the session record.

---

## Document Type Reference

This section defines what varies by document type. At Step 0b, identify the type. Apply that type's overlay for Steps 0–1 and for standard sections.

---

### Type 1 — Agent SOP

**Source (Step 0b):** Agent soul file. Read the soul before drafting a single line. The SOP is built from identity and principle — not from observed behavior.
- Soul gap check: Before drafting, compare the soul against recent observed operational behavior from active sessions. If behaviors are running that are not in the soul, surface them to Sage before drafting. Undocumented behaviors become SOP gaps.
- Cross-agent dependency check: If this agent has a direct workflow dependency on another named specialist (one agent produces something this agent runs or consumes), verify the soul's Principles section explicitly names the routing protocol for that cross-lane work. If it is absent, flag it to Sage before drafting — the soul must be corrected first. Cross-agent routing protocols belong in the soul, not discovered at the Outside-In Pass.

**Primary reviewer (Step 1):** The agent being built

**Standard sections:**
- Purpose
- Trigger
- Step-by-step process (named and numbered)
- Reporting format
- Edge cases
- Handoff protocol
- Tool stack reference (if applicable)
- File organization
- Version log

**Paired version:** Jay's plain-language version — always ask at Step 0; Hard Rule 13 applies from then on

**Type-specific standing inputs (Step 0c):**
- Item 37 (file placement): every Agent SOP includes a File Organization section mapping where the agent's files live
- Item 55 (routing model): agents submit research requests to Sage — not to Rose directly; Sage applies a CEO relevance check; Sage is sole authorized submitter to Rose; wire into every Agent SOP
- Hard Rule 19 (Semi-AGI three-altitude framework): before retrying or escalating any blocked task, classify the problem by altitude — Task level (apply two-round rule), System level (escalate to Sage immediately), Vision level (Sage escalates to Jay); resource access: Master Library first; information-only needs → submit to Sage, routed to Rose (Soren not required); new external deployable resource → full pipeline (Sage → Rose → Soren → Lexi); wire into every Agent SOP
- Proactive freshness check: when reviewing the Master Library at project start, apply expansive thinking — not just "what do I need?" but "is this still the right approach?"; surface meaningful gaps to Sage; evaluate, don't rebuild; wire into every Agent SOP
- Soul governance reminder: if the soul gap check surfaces soul change candidates, apply the CLAUDE.md soul governance framework — agents own their souls; Sage reviews for appropriateness; Jay approves; do not fold undocumented behaviors into soul updates without this gate

**Scope note:** This type covers Stage 4 (Full SOP Build — AAR Gate) of the agent creation lifecycle. For the complete lifecycle (Generic Soul Shell, True Soul Build, Basic SOP), see `Agent-Creation-Pipeline-SOP.md`.

---

### Type 2 — Standard SOP

Non-agent operational procedures.

**Source (Step 0b):** Relevant Hard Rules + existing procedures + the process context that triggered the need for this SOP

**Primary reviewer (Step 1):** Sophia (COO)

**Standard sections:**
- Purpose
- Trigger
- Step-by-step process (named and numbered)
- Edge cases
- Handoff (if applicable)
- Version log

**Paired version:** Jay's plain-language version — ask at Step 0; Hard Rule 13 applies if Yes

**Example:** Session-Close-SOP.md, CrossTalk-FireDrill-SOP.md

---

### Type 3 — Pipeline

Multi-stage process flow documents.

**Source (Step 0b):** Process inputs — existing stage descriptions, agent role documents, rules governing the flow

**Primary reviewer (Step 1):** The executing agents (by stage, if applicable)

**Standard sections:**
- Purpose
- Pipeline overview
- Stage-by-stage steps (numbered)
- Handoffs between stages
- Edge cases
- Version log

**Paired version:** Jay's plain-language version — ask at Step 0; Hard Rule 13 applies if Yes

---

### Type 4 — Simple Guide / Jay's Version

Plain-language paired version of a full document.

**Source (Step 0b):** The paired full document (V2 final). This document is always built from V2 — not V1.

**Primary reviewer (Step 1):** Jay (his review at Step 3 IS the primary review for this type)

**Standard sections:**
- Who/What [X] Is
- When [X] Activates/Triggers
- What Goes Through [X] (and What Doesn't)
- What [X] Does
- What You'll See
- Your Role
- The One Rule (or equivalent adapted for the document type)

**Paired version:** None — this document IS the paired version. Step 0 always returns No for this type.

**Note:** Built at Step 2 of the paired document's build cycle (from V2 final), reviewed at Step 3 (Jay's gate).

---

### Type 5 — Master Guide

Comprehensive team-facing reference document.

**Source (Step 0b):** All agent SOPs + Hard Rules Master List + project soul + phase structure + any team-wide standards

**Primary reviewer (Step 1):** Sage + team review (Sophia coordinates)

**Standard sections:**
- Purpose
- Standing rules
- Phase structure
- Agent roster
- Escalation paths
- Cross-references
- Version log

**Paired version:** Simple Guide (Jay's version) — always paired; Hard Rule 13 applies

---

### Type 6 — Runbook

Step-by-step execution guide for a specific SOP or process.

**Source (Step 0b):** The SOP or process it executes

**Primary reviewer (Step 1):** Sophia (COO)

**Standard sections:**
- Purpose
- When to use
- Prerequisites
- Step-by-step execution (numbered, atomic)
- Verification checks
- Version log

**Paired version:** None typically — ask at Step 0 if scope warrants

---

## The Cycle Compounds

As each document is built, this process grows more rigorous:

- The Source Scan at Step 0a grows — more existing documents to scan, same targeted approach
- The Backward Sweep at Step 4 grows in scope — more prior documents to check in reverse, same targeted method
- By the time a project has many built documents, Steps 0a and 4 are the primary quality gates

---

## Version Log

| Version | Date | What Changed | Why |
|---------|------|-------------|-----|
