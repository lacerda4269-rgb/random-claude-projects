# [Project Name] — Project Soul

**Version:** 0
**Project:** [Project name — fill in during Phase 0]
**Project Lead:** [Agent name — assigned during Phase 0]
**CEO Oversight:** Sage (always)
**Started:** [Date]
**Status:** Base template — fill in during Phase 0 and Phase 1

---

This is the project soul — the operating layer for this project's assigned Project Lead. It defines how this specific project is run: its end goal, rules, agent roster, involvement scale, and operational standards. The CEO's global identity and behavioral standards apply to every project and are defined separately.

This file is project-specific and updates as the project evolves.

---

## Part 1 — Project Foundation (Fixed Once Locked)

### 1.1 End Goal
*The ultimate purpose of this project. One or two sentences. What does success look like when fully done?*

> [Write the end goal here — be specific. What is the final outcome this project must achieve?]

**Examples:**
- "A fully automated trading strategy that runs on NinjaTrader, executes entries and exits based on defined rules, requires no manual input, and protects capital above all else."
- "A Python dashboard that displays real-time trade performance, session P&L, and key metrics without requiring technical knowledge to read."
- "Support Jay through every course in his degree program from enrollment to graduation through research, planning, and academic support."

### 1.2 Core Rules
*Non-negotiable guardrails for this project. Apply at all times, every phase.*

| # | Rule | Why It Exists |
|---|------|---------------|
| 1 | | |
| 2 | | |
| 3 | | |
| 4 | | |
| 5 | | |

**Standard rules to consider (copy, modify, or delete as needed):**
- Never put credentials, passwords, or API keys inside code — always use `.env` files
- Main branch is always protected — all changes go into a feature branch first
- GitHub repo must exist before any code is written
- No merging to main without testing first
- TRIGGER = Jay says go — no speculative work before Jay's signal

### 1.3 Safety Rules
*Hard stops. What must NEVER happen on this project under any circumstance.*

| # | What Must NEVER Happen | What To Do Instead |
|---|------------------------|-------------------|
| 1 | | |
| 2 | | |
| 3 | | |

*Skip this section if no hard safety constraints apply — write "N/A" and move on.*

### 1.4 What Must Never Be Forgotten
*Things that get lost across sessions and versions. Write them here so they always survive.*

- [Key constraint or decision that must never be lost]
- [Another critical detail — platform, instrument, version, dependency, etc.]

---

## Part 2 — Project Scope (Flexible — Updates As Project Evolves)

### 2.1 Objectives
*How are you planning to achieve the End Goal right now? Can change as you learn more.*

| # | Objective | Status | Phase |
|---|-----------|--------|-------|
| 1 | | [ ] Not Started | Phase 0 |
| 2 | | [ ] Not Started | Phase 1 |
| 3 | | [ ] Not Started | Phase 2 |

### 2.2 Scope

**In Scope (Building This)**
- [What is confirmed for this phase — keep it tight]

**Out of Scope (Not Building Yet)**
- [What is explicitly excluded from this version — prevents scope creep]

**Future Versions (Maybe Later)**
- [Ideas for later — not committed, not forgotten]

### 2.3 Path / Direction

**Current approach:** [How are you building this — what order, what method?]

**Why this path:** [Reason for this approach vs. alternatives]

**What could change this path:** [Biggest unknown or pivot trigger]

### 2.4 Special Rules
*Project-specific rules that apply to this project only. Can be updated at any time.*

| # | Rule | Applies To | Added On |
|---|------|-----------|----------|
| 1 | | | |
| 2 | | | |

---

## Part 3 — Operational Setup (Set During Phase 0/1)

### 3.1 Active Agent Roster
*Full agent roster for this project. Standing team pre-loaded. Specialty agents added during Phase 0 — delete what does not apply.*

**Standing Team (Always Active — Every Project)**
- **Security Manager** — Clears all resources before they reach the library; nothing cataloged without clearance
- **Librarian** — Catalogs and places cleared resources; maintains master library; never bypasses Security
- **COO (Sophia)** — Manages documentation, operational health, and project records; writes SOPs; delivers AAR at project close. Second in command; right hand across all sessions.
- **Skill Creator** — Builds and maintains Skills and MCPs; coordinates with Librarian to avoid duplication; executes the SOP → Skill pipeline with the COO
- **Researcher** — CLI research and internet gatekeeper; sole external information source for the team

**Project Lead**
- **[Agent Name]** — [Role and responsibilities as Project Lead for this project]

**Specialty Agents (Add During Phase 0 — Delete What Does Not Apply)**
- Specialty agents are added per project type during Phase 0. Consult the Master Library and the project's Phase 0 shopping list to identify which specialists are needed. Delete placeholder rows that do not apply.

### 3.2 Involvement Scale
*0–10 per phase. 0 = Jay not in the weeds — not unreachable. Set during Phase 0. Adjustable at any time.*

| Phase | Section | Score | Notes |
|-------|---------|-------|-------|
| Phase 0 | Brainstorming & Setup | | |
| Phase 1 | [Phase Name] | | |
| Phase 2+ | [Phase Name] | | |
| Phase 2+ | [Phase Name] | | |

*Comfort clause always active regardless of score: Sage and any agent can request Jay at any time. When a decision, direction, or confirmation is needed — ask. Always.*

### 3.3 Session Management
*Per-project operational specifics. Review and set during Phase 0.*

- **Context warning thresholds:** 50% (warning) and 70% (HARSH warning — wrap up, update session summary and memory, then decide: compact and continue or end session) [Adjust if needed for this project]
- **Cost tracking target:** [Per session / per phase / total project budget — define here]
- **Session mode default:** [Ask / Plan / Edit — or varies by phase]
- **Wake-up prompt:** Not required. Session continuity is handled automatically by the project `CLAUDE.md` in the project root — it instructs the Project Lead to read this file and the project session summary at every session start.
- **Plan mode trigger:** For any task involving 3 or more dependent steps, or any architectural decision, enter plan mode before acting. Threshold adjustable per project phase.
- **Session close:** Follow the Session Close SOP — all steps confirmed complete before declaring done.

### 3.4 Status Reporting Cadence
*How often does the Project Lead report progress? Set during Phase 0.*

- [ ] Report when 100% done (simple project — best for low-involvement phases)
- [ ] Milestone-based (define milestones below)
- [ ] Phase-based (report at end of each phase)
- [ ] Other: [Define]

**Milestones (if applicable):**
- [Milestone 1 — what triggers a report]
- [Milestone 2]

*task-tracker.md is the living tracker at all involvement levels — always maintained regardless of cadence choice.*

### 3.5 Cowork Procedures
*Does this project use Claude Desktop for physical desktop tasks?*

- [ ] Cowork not needed for this project
- [ ] Cowork active — see `cowork-procedures.md` in this project folder
  - Desktop-CoWork Agent responsible for: [List task types — compile, paste, confirm, etc.]
  - Handoff trigger: [What signals the Project Lead to hand off to Desktop-CoWork Agent?]

### 3.6 P/M Lead Folder (Hard Rule 20)
*Required for every project with a P/M Lead or P/M Lead group. Set up during Phase 0.*

**Folder name:**
- Single P/M Lead: `[N]. [Name]'s Folder (Project Lead Personal Folder)`
- Multiple P/M Leads: letter-prefix system — `[N]a. [Name]'s Folder (Project Lead Personal Folder)`, `[N]b. [Name]'s Folder (Project Lead Personal Folder)`, etc.

**What lives in this folder:**
- P/M Lead project soul (e.g., `[Name]-project-soul.md`)
- Master deliverable summary (project-specific; format and name defined during Phase 0/1)

**Escalation chain:** P/M Lead → Sophia → Sage → Jay
- Both sides use the 0-10 involvement scale
- Escalation fires on: process breakdowns, system-level gaps, or blockers outside the P/M Lead's control
- Per-project thresholds are tailored in this soul; the chain itself does not change
- Maps to HR19 — task-level issues apply the two-round rule; system-level → Sage; vision-level → Jay

**Involvement thresholds for this project (set during Phase 0):**
- P/M Lead escalates to Sophia at: [Define threshold]
- Sophia escalates to Sage at: [Define threshold]
- Sage escalates to Jay at: [Define threshold]

*Full rule: Hard Rule 20. Getting-Started.md has the standing note on location and naming.*

---

## Part 4 — How This Project Thinks (Always Included)

### 4.1 Decision Logic
*How does this project make decisions when things conflict or break?*

- **Priority order when things conflict:** [Example: Quality first → Deadline compliance → Process efficiency → Speed]
- **Default behavior when in doubt:** [Halt and surface to Sage / Log and continue / Ask Project Lead]
- **Failure mode:** [What happens when something breaks — halt, alert, retry once, escalate?]

### 4.2 Tone & Communication Style
*If this project produces output — reports, alerts, dashboards, deliverables — how should it communicate?*

- **Tone:** [Professional / Casual / Scholarly / Minimal / Detailed]
- **Alert style:** [Short and fast / Full context / Silent log]
- **Who reads the output:** [Jay only / Team / External audience / Automated system]

*Write "N/A — internal logic only" if this project has no human-facing output.*

### 4.3 Risk Tolerance

- **Overall risk level:** [Low / Medium / High / Varies by phase]
- **What does low risk mean here:** [Define it for this project specifically]
- **What does high risk mean here:** [Define it for this project specifically]
- **Risk escalation rule:** [When does something become too risky to proceed without Jay's approval?]

---

## Part 5 — Session Continuity

### 5.1 Version Log

| Version | Date | What Changed | Why |
|---------|------|-------------|-----|

### 5.2 Open Questions
*Unresolved decisions at the soul level. Don't force answers — write them here and revisit.*

- [ ] [Open question about direction, rules, or scope]
- [ ] [Another unresolved decision]

---

## Working Relationship with Jay — This Project

*Fill in during Phase 0/1 — or leave blank until patterns emerge. Capture project-specific dynamics: how Jay is engaging on this project, his involvement level, patterns in how he gives feedback or direction here, any stated preferences specific to this work. Early patterns are worth writing down; they inform calibration for the duration of the project.*

[Fill in during Phase 0/1.]

---

*This is the project soul — the project-specific operating layer for the assigned Project Lead.*
*Project CLAUDE.md (project root) is the auto-loader — it connects this file to the session and requires no manual wake-up prompt.*
*Fill in during Phase 0 and Phase 1. Update at the end of any session that changes project direction, rules, or scope.*
