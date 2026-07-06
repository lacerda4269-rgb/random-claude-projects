# Your Guide — What You Do

**Version:** 0
**Date:** 2026-06-23
**For:** Jay — operator guide only. What you do at each step.
**Note:** The technical details are Sage's job. This guide covers your part only. For full technical depth, see Master Guide — Sage's Version (SOP v1).

---

## Who Is Sage

Sage is your CEO — one title, two layers always running at the same time.

**As your CEO (company-wide):** Sage is your right hand across everything. She translates your vision into a plan, manages the team, keeps the system moving, and flags problems before they become blockers. This role never changes project to project.

**As your CEO (per-project lead):** Every project gets Sage as its dedicated project lead — same person, project-specific focus. The project soul file is where that layer lives.

**The team:**

| Agent | Role | What They Do |
|---|---|---|
| Sage | CEO | Orchestrates everything. Thinks, routes, decides, flags. Never does the domain work — makes sure the right agent does it. |
| Rose | Researcher | Primary internet researcher — operational tools, CLIs, skills, and resources. Feynman handles academic and deep-source investigation. No agent submits research requests directly to Rose — they go through Sage first. Sage checks domain relevance and routes to Rose if approved. Every report includes a plain-English C&P Summary. |
| Soren | Security Manager | Clears everything from outside before it enters the library. Pipeline: Rose researches → Soren clears → Lexi files. No shortcuts. **Web-only tool class (Item 66):** Tools used via browser only (no download, install, credentials, or local code execution) are pre-approved and bypass the clearance pipeline. Pre-approved list: `Web-Only-Pre-Approved-Tools.md` (Soren's folder). Any new addition requires Jay's or Sage's approval. |
| Lexi | Librarian | Files all cleared resources. Owns the Master Library and catalog. Nothing enters without Soren's clearance first. |
| Sophia | COO | Active from session start. Manages documentation, operational health, and records; writes SOPs; maintains Gotcha.md (per-project operational watch list); **writes the project Session Summary and Index at every session close and compact** (Sage reviews before push); second in command to Sage; runs the AAR at close. |
| Cosmo | Skill Creator | Builds the team's automation and integration layer — Skills, Hooks, CLIs, MCPs, plugins, and any resource the project needs. Evaluates operational documents for hook/skill designation. Proactively flags build candidates. Coordinates with Lexi to prevent duplicates. |
| Nick | NinjaTrader Specialist | NinjaScript/C# for NinjaTrader only. Feature branch only — never directly to main. |
| Todd | TradingView Specialist | Pine Script for TradingView only. Feature branch only — never directly to main. |
| Pete | Python Specialist | Python across toolkits. Feature branch only — never directly to main. |
| Vicky | Videographer | Full video production (editing, captions, AI generation). No code writing — Pete builds scripts, Vicky runs them. Web-UI-only for AI generation (no API access). Video tooling clears Soren per project before use. |
| Feynman | Academic Research Specialist | Deep research when operational research isn't enough — academic literature, primary sources, scholarly citations. College and academic work direct (no Rose prerequisite for Jay). Rose first for all non-Jay requests. |

> *Cosmo SOP — `5. Master Library/1. Soul Folder/Cosmo the Skill Creator/Cosmo-Skill-Creator-SOP.md` + Jay's version: `Cosmo-Skill-Creator-SOP-Jay.md`. Specialty agents (Nick, Todd, Pete, Vicky) are activated at the start of their phase only.*
> *Nick SOP — `1. Soul Folder/Nick and NinjaTrader/Nick-NinjaTrader-SOP.md` + Jay's version: `Nick-NinjaTrader-SOP-Jay.md`.*
> *Todd SOP — `1. Soul Folder/Todd and TradingView/Todd-TradingView-SOP.md` + Jay's version: `Todd-TradingView-SOP-Jay.md`.*
> *Pete SOP — `1. Soul Folder/Pete and Python/Pete-Python-SOP.md` + Jay's version: `Pete-Python-SOP-Jay.md`.*
> *Vicky SOP — `1. Soul Folder/Vicky the Videographer/Vicky-Videographer-SOP.md` + Jay's version: `Vicky-Videographer-SOP-Jay.md`.*
> *Feynman SOP — `1. Soul Folder/Feynman the Scholar/Feynman-Scholar-SOP.md` + Jay's version: `Feynman-Scholar-SOP-Jay.md`.*
> *Feynman Session Management SOP — `1. Soul Folder/Feynman the Scholar/Feynman-Session-Management-SOP.md` + Jay's version: `Feynman-Session-Management-SOP-Jay.md`.*

**What Sage is not:** Sage orchestrates — she thinks, routes, decides, and flags. The domain work belongs to the right agent. Sage makes sure it gets done and done right. She does not code, research the internet, file resources, write documentation, or clear security. Those lanes belong to the agents who own them.

### Two-Lane Rule — How Your Agents Participate

Every agent stays in their own lane for building work. Nick builds only NinjaTrader code. Todd builds only TradingView Pine Script. Vicky builds only video work. This is a hard rule — no agent creates, edits, or writes anything outside their own domain.

But any agent can join a discussion or project when you invite them — give opinions, flag something they notice, review another agent's work, or ask questions. That participation has no lane limit.

**The practical test:** Nick can advise Vicky on the NT trading content in her video. He cannot build any part of the video itself. Participation is open. Building is strictly in-lane. Session 161 — Jay direction.

### Sage and Sophia Are Always in the Loop (Item 102)

It doesn't matter how a task gets assigned — whether Sage routes it to an agent or you assign it directly. Sage and Sophia are always in the loop. There is no assignment path that bypasses the chain of command.

**What this means for you:** When you assign something directly to an agent, they treat it as though Sage already knows — because she does. You don't need to separately brief Sage or make sure she's aware. The system assumes Sage is in the loop by default.

*Session 139 — Jay direction (extended to all agents at Phase 0, Session 201).*

### Cross-Agent Handoff Format — JSON Standard (Item 146)

When Nick or Todd passes a build output to Pete's Python pipeline, the exchange format is file-based JSON.

Required fields: input source, output format, validation target, pass/fail result. Additional fields are project-specific. Pete owns this standard.

You don't need to manage the format — Pete, Nick, and Todd handle it. But it's worth knowing it exists: when one agent hands off to another across platforms, there's a defined format so nothing gets lost in translation.

*Pete's soul defines this standard. Wired to Nick SOP, Todd SOP, and both MGs at Phase 0 (Session 201 — Item 146).*

---

## 1. Session Start — Every Session

> **Technical stack reference:** Before the behavioral read-in sequence runs, plugins and hooks initialize automatically. See `~/.claude/startup-stack-reference.md` for the full technical layer map, hook load order, and failure recovery guide.

**When you return:** Just say hi. Sage reads everything automatically and tells you where you left off — what was done last session and what's coming next. You don't need to do anything to get her up to speed.

> **Behind the scenes:** Before responding, Sage runs a query-first read-in: memory files and global lessons first, then a graphify knowledge graph query plus claude-remember / context-mode recall to surface current state without bulk-reading all soul files. If those queries surface a gap, she reads the specific file just-in-time. Sophia is activated with an opening brief before any work begins. That's what the catch-up is — a structured query, not a bulk read. The full step-by-step is written up in `Session-Start-SOP.md` (in Sage's SOPs folder) — you don't need to read it; it's Sage's procedure.

Three things before any work begins:

**Step 1 — Pick a mode and say it out loud:**
- **Ask Mode** → the default. Back and forth with Sage and any agent. Use this for Phase 0, Phase 1, and most sessions.
- **Plan Mode** → when Sage or any agent is building a proposal or plan for your review — without creating any actual files. You review; if approved, switch to Auto.
- **Auto Mode** → approved builds executing. Files get created and changed.

**PBM — Parallel Build Mode:** Some projects run in two tracks at once — a live operational track (e.g., active college coursework) and an infrastructure track (SOPs, architecture, project setup). When that's the case, tell Sage which track you're working on at session open: *"infrastructure"* or *"live/operational."* If you don't say, Sage will ask before any work begins — she owns that check. Full details: Master Guide — Sage's Version, Standing Rules (Parallel Build Mode).

**Step 2 — Set Claude Code's permission level (Shift+Tab to toggle):**
- **Ask** → Sage pauses before each action and waits for your approval. The default setting.
- **Plan (read-only)** → nothing gets created or edited. Sage and agents can draft and propose but cannot write files. Use when in Plan Mode.
- **Auto** → Sage runs everything without stopping to ask. Use for approved build sessions.

Simple rule: Default = Ask. Building a proposal for review = Plan (read-only). Approved builds executing = Auto.

**Step 3 — Check your context window:**
Watch the % in the Claude Code status bar. When it gets high, let Sage know you're about to compact.

> **Behind the scenes:** When you signal a compact, Sage runs the full Compact Wrap-Up sequence — all files updated, everything pushed to GitHub — before you compact. After you compact, Sage reads only the most recent Session Summary entry to re-orient. The compact summary captures everything else — she reads other files only when the task actually requires them. A compact means you're continuing the session. A session close means you're done for the day — different sequence, same push to GitHub. Two things to know: (1) before either a close or a compact starts, Sage checks that no agent (like Sophia) is in the middle of a task — if someone is, it gets finished or parked first; (2) the coming-back-after-a-compact steps are written up in `Post-Compact-Return-SOP.md`, and the fresh-session steps in `Session-Start-SOP.md` — both Sage's procedures, nothing you need to run.

---

## 2. New Project Setup

Your steps — then Phase 0 begins immediately:

1. **Capture your idea.** Notes, thoughts, support docs — anything that helps describe what you want to build.
2. **Create the project folder** on your computer.
3. **Send the trigger prompt:** Open VS Code + Claude. Say: *"New Project. Process guide and package: [path to Initial Package]. Project folder: [path to new project folder]."*

> **Behind the scenes:** Sage executes the full new project setup automatically — copies the Initial Package files into the project folder, creates the project CLAUDE.md, sets up the memory directory, confirms GitHub status, sets default mode to Ask/Sonnet. She confirms when ready and Phase 0 begins. You don't need to do anything until she confirms.

**GitHub:** You may or may not create a repo — that's fine. Let Sage know during Phase 0 whether you've created one. If you don't bring it up, she'll ask.

---

## 3. Phase 0 — Brainstorming (Mandatory)

**Your job:** Share your idea and think out loud with Sage.

- Start in **Ask Mode** — back and forth with Sage. Switch to **Plan (read-only)** only when Sage is building a file or proposal for your review.
- Tell Sage your idea. You and Sage brainstorm freely — goals, constraints, open questions, what you want to build. Nothing is final here.
- Sage fills in two files: `discovery.md` (what exists, what we're doing) and `research.md` (how things work).
- **Your approval step:** Review both files when Sage presents them. You approve before Phase 1 starts.
- Sage will ask you to set an **involvement score** (0–10) for each phase — 0 means hands-off, 10 means fully involved. You decide. You can change it at any time.
- Sage will ask about **reporting cadence** — how often she reports back. You set it.

> **Behind the scenes:** After the initial Sage + Jay structure conversation, Sage deploys the standing team with a clear brief. Specialty agents (Nick, Todd, Pete) are staged but not activated — they cost nothing until their phase begins. Sophia builds the project navigation files (`project-file-index.md` and `project-navigation-map.md`) from templates — both ready before Phase 1 starts. Sage also identifies your personal notes folder during Phase 0 housekeeping and records it in the project CLAUDE.md. She never reads it.
>
> **CEO shopping list scope (Item 80):** Sage's Phase 0 shopping list goes beyond what this project alone needs. As CEO, she also evaluates tools, GitHub resources, and solutions that improve the company-wide operational infrastructure — memory systems, workflows, processes, databases, idea capture, anything that makes the whole system smarter and more efficient across all projects. You don't need to manage this — just know that when Sage brings you a resource recommendation at Phase 0, it may serve the entire company, not just this project.

**Standing team activated in Phase 0:**
- Rose handles any internet research needed (requests go through Sage first) → *Rose SOP — `1. Soul Folder/Rose the Researcher/Rose-Researcher-SOP.md` + Jay's version: `Rose-Researcher-SOP-Jay.md`*
- Soren clears anything coming in from outside → *Soren SOP — `1. Soul Folder/Soren the Security Boss/Soren-Security-Manager-SOP.md` + Jay's version: `Soren-Security-Manager-SOP-Jay.md`*
- Lexi files cleared resources into the Master Library → *Lexi SOP — `1. Soul Folder/Lexi the Librarian/Lexi-Librarian-SOP.md` + Jay's version: `Lexi-Librarian-SOP-Jay.md`*
- Sophia opens her Pending Changes List and starts observing → *Sophia SOP — COO Folder → COO Suite (`Sophia-COO-SOP.md`) + Jay's version: `Sophia-COO-SOP-Jay.md`*
- Cosmo flags anything that should become a skill, hook, or CLI → *Cosmo SOP — `5. Master Library/1. Soul Folder/Cosmo the Skill Creator/Cosmo-Skill-Creator-SOP.md` + Jay's version: `Cosmo-Skill-Creator-SOP-Jay.md`*

> Phase 0 is never skipped. Every project starts here, no matter how simple.

---

## 4. Phase 1 — Blueprint (Mandatory)

**Your job:** Review the plan and approve it before anything gets built.

- Start in **Ask Mode** — review and discuss the blueprint with Sage. Switch to **Plan (read-only)** when Sage is building the blueprint document for your review. Switch to **Auto** when you approve and Phase 1 assembly begins.
- Sage builds the project blueprint (`plan.md`) from Phase 0 outputs. She fills in what she's certain about and flags anything she needs from you.
- **Your approval step:** Sage presents the blueprint. You review it, fill in any gaps, and approve it. Nothing moves to building until you say go.

> **Behind the scenes:** Once you approve, Sage switches to setup mode and installs what the project needs in the right order: Soul → Skills → Hooks → CLIs → MCPs. She tells you what and why before installing anything. Cosmo is involved when skills, hooks, or CLIs are being built. → *Cosmo SOP — `5. Master Library/1. Soul Folder/Cosmo the Skill Creator/Cosmo-Skill-Creator-SOP.md` + Jay's version: `Cosmo-Skill-Creator-SOP-Jay.md`*

> Phase 1 is never skipped. Every project gets a blueprint.

---

## 5. The Build — Phases 2 through Z

**Your job:** Stay in the loop at whatever involvement level you set.

- Phases beyond Phase 1 are flexible — you name them and structure them however makes sense for the project. No fixed number, no fixed names.
- Sage keeps `task-tracker.md` updated throughout.
- She reports back on the cadence you set in Phase 0.
- You can adjust your involvement score at any time — just say so.
- If something is blocked, Sage brings it to you. You, Sage, and the relevant agent resolve it together.

**Involvement score (0–10):**
- **0** = fully hands-off for that phase or section. You are not in the weeds — but you are never unreachable.
- **10** = fully hands-on, involved in every decision.
- Set per phase and section in Phase 0. Adjust at any time — just say so.
- **Comfort clause:** Any agent — including Sage — can come to you at any time, regardless of your score. A score of 0 is not a lock-out.

**When something is blocked:**
Agents get two rounds before it reaches you. Round 1: the agent fails and tries a new approach. Round 2: Sage and the agent brainstorm a new direction and attempt it once. If Round 2 fails, the task goes on hold and Sage brings it to you. You, Sage, and the agent resolve it together. A documented failed approach is never retried.

> **Behind the scenes:** Sage runs the full operation at any involvement level. She manages both rounds before anything comes to you. You're always reachable — regardless of your involvement score.

**Multi-agent windows:** When a project is big enough, Sage runs multiple agents at the same time. With Agent Teams turned on (below), most of this happens inside Sage's own session — she runs the agents directly, so there's nothing for you to open. Separate windows are just the fallback for work that needs to run on its own; in that case you open them manually and Sage gives you the brief to paste. Either way, you don't manage the agents — Sage does.

> **Behind the scenes:** For short tasks or quick consultations, Sage brings an agent into her window instead of opening a separate one. Lower cost, faster. Phase 0 is where you and Sage decide which agents need their own window.

**Agent Teams setup:** Agent Teams is turned on via `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` in `~/.claude/settings.json` — set once globally at MIP, never repeated per project. In Claude Code `/config`, you'll see it labeled **"Default Teammate mode"**. On Windows, pick **in-process** (split-pane won't work in VS Code or Windows Terminal).

**How the team works (Agent Teams):** Agents don't watch each other work — that's not something Claude Code can do. Instead they hand off: Sage gives an agent a brief, the agent builds its part on its own, and hands back a finished piece. Some agents run in their own terminal and approve their own steps (good for self-contained work like Feynman's coursework); others run quietly alongside Sage's session. Agents that run commands — installing tools, running code, git — get their specific commands cleared up front so they don't stall. Two safety lines always hold: (1) anything brought in from outside — a new tool, app, package, or file — still goes through the full security check (Sage → Rose → Soren → Lexi), no shortcuts; (2) anything pulled off the live web gets scanned before anyone acts on it. Every finished piece is reviewed before it ships — Sophia checks it operationally, Sage reviews — and nothing reaches GitHub without Sage's final push gate, which is where you stay in control. If an agent hits a wall, the same two-round rule applies and the path back to you never closes.

**Who's on the team — the roster (think of it as payroll):** An agent can only be called on if its file is sitting in the project's `.claude/agents/` folder. That folder is the active payroll — the simple rule is **hire by adding the file, let go by removing it.** There are three kinds of people on it: **Permanent** — Sophia (your COO) is always there, every project, start to finish. **As-needed** — a project lead is added when a project needs one and stays for that whole project (for example, a P/M Lead running a live sub-project like coursework or client work). **Temporary** — outside help brought in for one specific job and removed once it's handed off (for example, a specialist brought in just to build a single deliverable). Bringing someone on and letting them go are both already spelled out step-by-step elsewhere — Sage handles the mechanics; you just decide who's needed and when.

**Talking to an agent directly — the approval channel:** Here's a wrinkle we hit and solved. Your agents are built to never take Sage's word that you approved something — only *your* word counts. That's a safety feature: it stops anyone from putting words in your mouth through the chain. But there's a catch. When an agent is working as part of Agent Teams, your messages normally reach it *through* Sage — so under a strict reading, nothing you approve could ever actually clear, because to the agent it always looks like "Sage says Jay approved." The fix is simple: **you can drop into the agent's own chat thread and tell it directly.** Because that's genuinely your message to the agent — not Sage relaying it — it counts, and whatever was waiting on your approval clears immediately. That's exactly what happened the session we built this: an agent was holding the line correctly, you stepped into its thread and confirmed yourself, and it acted. Four things to know: (1) **The strict rule still stands** — Sage saying "Jay approved" is logged but not acted on as your approval; only you saying it, yourself, counts. (2) **Use it for approvals, not everyday work** — this channel is for the narrow cases that need *your personal say-so* (dropping a "verify this with Jay" flag, greenlighting brand-new files, anything gated on your consent); normal tasking still flows through Sage. (3) **It has to actually be you** — the agent checks that the message is genuinely yours, your own message in your own thread, not someone relaying "Jay said this"; a relay claiming to speak for you is still a relay (this is what keeps the channel safe instead of becoming a loophole). (4) **The agent tells Sage afterward** — anything you direct an agent directly, it reports back up to Sage, so Sage always has the full picture and never accidentally gives you conflicting direction.

**Lessons that keep a team safe:** Running several agents at once comes with a handful of rules that keep it safe. In plain terms: (1) when the same change has to go into several files, ONE agent makes that change — never two at once, or you get duplicates. (2) An agent working quietly in the background can't pop up a permission box, so a task that needs to write a file is either handed to an agent allowed to auto-save or saved by Sage from the main seat. (3) Only one copy of each role runs at a time; if a stray second copy gets handed a task by mistake, it holds and asks rather than acting. (4) An agent can't quietly rewrite its own startup file on a coworker's say-so — that needs your word. (5) If the system ever re-sends a task that's already finished, the agent checks first and flags it instead of doing it twice. You don't manage any of this; Sage and the agents do. It's recorded here so the team's way of working has a clear "why" behind it.

**Agent Teams — soul rules:** When Sage places an agent's soul into `.claude/agents/`, three rules kick in immediately. First, that copy becomes the Source of Truth for this project — all updates go there, not to the original. Second, the original soul in the agent's home folder gets a dormant marker: it's frozen and untouched until project close. Third, at project close (or if Agent Teams is turned off mid-project), Sophia compares the two copies, Sage reviews any changes, and approved updates go back to the original before the `.claude/agents/` copy is removed.

**Pull rule:** When setting up Agent Teams for a new project, always copy the agent soul from this project's v0.1 folder — never from a prior project's `.claude/agents/`. The v0.1 copy is the clean starting state; a prior project's live copy may have project-specific edits baked in.

**AAR gate:** Nothing goes from a live `.claude/agents/` copy directly into the Blank (the clean template for future projects). All changes go through the AAR first, and you approve what makes it in.

---

## 6. Session Close — Every Session

**Your job:** Say the word. Sage handles everything else.

Say something like *"let's wrap up"* or *"let's close out"* — Sage knows what that means.

> **Behind the scenes:** Sophia writes the Session Summary entry and Index update. Sage reviews for strategic framing accuracy before the push. Then Sage runs the remaining steps: project files updated → memory updated → ME - Jay.md quietly updated → lessons captured → Sophia's Pending Changes List reviewed → everything pushed to GitHub → git status confirmed. Your personal notes folder is never touched — not unless you explicitly ask. Confirms when done: *"Session Summary updated and pushed to GitHub."*

> **Also before close:** Sage runs a cross-reference + backward sweep as a standing paired check at every session and compact close — active now, pending formal SOP wiring in a future project. → Gotcha Entry 13

The next session starts automatically from where you left off.

**Session summary splits:** Two triggers: Sage checks in every 20 sessions without a split — recurring, not a one-time check (20, 40, 60, and so on), your call each time; any version update (v0 → v1, etc.) is a hard trigger — split happens before the version change, automatic. You can also call a split at any time. When it splits, the index splits with it at the same session boundary. Full process in `CloseOut-HouseKeeping-SOP.md`.

**Project lead model (Item 103):** When a P/M Lead is running a sub-project with their own dedicated folder and Session Summary (for example, a live coursework or client track), they write their sub-project summary independently. Sophia writes the master IP Session Summary. The two summaries are parallel — neither replaces the other. The master IP summary captures IP-level decisions only; sub-project detail stays in the P/M Lead's folder.

---

## 7. Project Close — After Action Review (AAR)

**Your job:** Sit down with Sophia and the full team for a debrief.

This happens once — when the project is fully done. It's different from session close. Session close = done for the day. Project close = done forever.

> **Scope:** The AAR fires once — at Master Initial Package project close. It does not fire at individual pipeline sub-project closes (the 9 pipeline projects: Rose Research Report, Specialty Agent SOP Build, etc.). Each sub-project closes via the Session Close SOP, with no AAR gate.

Every agent who touched the project participates — not just Sophia. Sage participates too. Each agent answers the four questions from their own perspective. You hear all of it.

Four questions — answered by everyone:
1. What went right?
2. What went wrong?
3. What do we improve next time?
4. What did we build that should become a reusable tool for future projects?

Sophia runs it. It doesn't need to be long.

Each agent also updates their own **"Working Relationship with Jay"** section in their soul file at the AAR — their candid observations from working with you on this project. This is separate from ME - Jay.md, which covers what applies to everyone. The agent's section covers what's specific to their lane and their dynamic with you.

> **Behind the scenes:** Sophia presents any pending changes — things the team flagged during the project but couldn't apply mid-project (source materials are frozen during active projects). You decide what gets applied. After the AAR, Sage updates the global CLAUDE.md with any approved changes and pushes to the backup soul repo automatically. Sage also updates the Master Copy of the Initial Package (MC-IP) with any approved template or system changes — same trigger: AAR recommendations → Jay approves → Sage executes. No agent touches MC-IP directly. Project is officially closed. → *Sophia SOP — COO Folder → COO Suite (`Sophia-COO-SOP.md`) + Jay's version: `Sophia-COO-SOP-Jay.md`*

> The AAR is always the last step before a project is closed.

---

## 8. Quick Reference — Rules to Remember

**Session & Phases**

| Rule | What It Means |
|---|---|
| Declare a mode every session | Ask, Plan, or Auto — say it before work starts |
| Phase 0 and Phase 1 are mandatory | Every project, no exceptions |
| Source materials frozen mid-project | Changes to MGs, CLAUDE.md, and templates queue to Sophia's list — applied after AAR only. |
| Session close = done for the day | Summary updated, files updated, pushed to GitHub. |
| Project close = AAR, then done forever | Full team debrief. Pending changes reviewed and applied. Project officially closed. |

**Code & Security**

| Rule | What It Means |
|---|---|
| GitHub repo before any code | Only if the project has code. Mention in Phase 0 — Sage asks if you forget |
| Never put passwords in code | Credentials go in `.env` files, never in code itself |

**Build Order & Architecture**

| Rule | What It Means |
|---|---|
| Build order: Soul → Skills → Hooks → CLIs → MCPs → Plugins | Sage follows this automatically — just know it exists. Plugins last because they're the most complex and can contain the component types above them. |
| CLIs — OS layer, zero standing cost | Multiple CLIs per project work simultaneously without conflict — they're independent OS tools, completely dormant until called. Cosmo builds skills or scripts to orchestrate multiple CLIs; the CLIs stay separate, the skill is the recipe. |
| MCPs — standing process cost | Unlike CLIs, MCP servers start at session launch even if unused. An unused MCP still costs per session. Only configure what the project genuinely needs. Global MCPs run in every session; project MCPs run in that project's sessions only. |
| Plugins — bundled domain capability | Packages skills + hooks + MCPs as one installable unit. Carries the cost of everything bundled inside, including any MCPs. Signal for a plugin: when 2–3 related component types always travel together and are reusable across projects — Cosmo flags, Sage decides, Soren clears. |
| MIP base carries no CLIs, MCPs, or plugins | All three are project-specific Phase 0 additions. The MIP carries the process for adding them (Soren → Lexi → Cosmo → Sophia) — not the components themselves. |
| Paired documents always updated together | Any document with a paired counterpart (both Master Guides, and all SOPs — Sage/Agent version + Jay's version) must be updated in the same session. A change to either version triggers a sync of the other before the session closes — in both directions. **Visual workflow — default format for your version (Item 121):** When a new SOP is built, a visual workflow or flowchart (e.g., Mermaid diagram) is the default format for your version when it fully represents the workflow. A separate plain-text version is built only when a genuine operational need exists for one. Sage documents the call at Step 0. **Document type standard:** Every document is typed at Step 0 — SOP (executable procedure), Reference Guide (non-executable look-up), or Runbook (step-by-step checklist for recurring operations). Recorded in the header. |

**Agent Pipeline**

| Rule | What It Means |
|---|---|
| All external research goes through Rose | No other agent goes to the internet. Every report includes a plain-English C&P Summary. |
| Agent research requests go through Sage, not Rose directly | Agents submit to Sage. Sage checks: is this request in the agent's lane? If yes, routes to Rose. If no, redirects back. Sage is the only one who sends tasks to Rose. |
| Rose conducts a security META check at project start | Rose researches the latest AI threats, prompt injection methods, and protections. Soren reviews the findings. Any resource arriving that was not sourced by Rose is an automatic denial. |
| All outside resources clear Soren first | Rose researches → Soren clears → Lexi files. Nothing skips this pipeline. |
| Lexi owns the library | Cleared resources go to Lexi. Nothing enters without Soren first. |
| Sophia is always on | Active from new project start, every session, and after every compaction. No activation call needed. Sage's right hand — catches what Sage misses. Pending Changes List open. SOPs and AAR are hers. **Writes the Session Summary and Index at every session close and compact — Sage reviews before push.** |
| Always-present principle — Sage + Sophia in every loop (Item 102) | No agent communication chain bypasses both. Every significant decision, SOP change, and operational update passes through Sophia (operational lens) → Sage (CEO lens). A decision that Sophia doesn't know about is an unreviewed decision. |
| 3rd Set of Eyes — Sophia as independent reviewer | For significant design gaps or behavioral decisions, Sophia can be activated as a third perspective before a combined recommendation is formed. She reviews independently — not told what Sage thinks first. Three views: Sage (strategic), Sophia (operational), Jay (final call). Also runs as the `fresh-eyes` skill — a zero-prior-context review by freshly spawned agents (the no-anchoring complement to this role-diverse check). |
| Soul update governance (Item 70) | Agents own their souls — content and identity are theirs. When an agent proposes a soul update, Sage reviews: does it belong in a soul (not an SOP or skill)? Does it conflict with team rules? Is it soul-appropriate? Sage recommends; you approve. |
| Cosmo builds the skills, hooks, and more | Anything that should become a reusable skill, hook, or CLI routes to Cosmo. He also evaluates documents on request for hook/skill designation and proactively flags build candidates. |
| Cosmo build pipeline — not complete until Sophia logs | After Lexi catalogs a Cosmo build: Sophia logs to the Approved Resources — Deployable Arsenal roll-up in the ML Quick Reference + Project Resources Log → Sage reviews and confirms. Build is not closed until Sage confirms the entry. Visual reference: the Cosmo Build Pipeline diagram (`Cosmo-Skill-Creator-Mermaid.md`). |

**Agent Deployment**

| Rule | What It Means |
|---|---|
| Basic SOP required before live project work | No agent works on a live project without a Basic SOP built. If an agent is needed and has no Basic SOP yet, the project pauses to build one. No waiver. |
| Full SOP required before AAR closes | Every agent who worked on the project needs a Full SOP before the project is officially closed. |
| Two gates — neither can be skipped | Deployment Gate (Basic SOP) before live work. AAR Gate (Full SOP) before project close. Both required. Both binding. |

**Document Rules**

| Rule | What It Means |
|---|---|
| Cross-reference updates are automatic | When any document changes, Sage checks all related documents and updates them same session. You don't track this — Sage does. |
| No hard paths in documents | SOPs, templates, and instructions use descriptive labels — not machine-specific folder paths. One carve-out: it's about reference *type*, not where the file lives. Paths describing where things sit inside a project are always descriptive labels; paths that are simple facts about the machine (where a tool installed, a binary location) can be written out literally. |
| Logical ordering always | Any list, table, or collection — when created or updated — goes in logical order, not creation order. Applies everywhere, every time. |
| ML report annotations | Agents may annotate library report files in their lane only — Sage's approval required. Open questions are marked "pending — answer at first use." |

**P/M Lead Operations**

| Rule | What It Means |
|---|---|
| Every P/M Lead gets a dedicated folder | Any project with a Project/Module Lead must have a named P/M Lead folder. The project soul and master deliverable summary live there. Single lead: `[N]. [Name]'s Folder (Project Lead Personal Folder)`. Multiple leads: `[N]a.`, `[N]b.`, etc. |
| P/M Leads operate autonomously on task-level work | Day-to-day project work is the P/M Lead's to run. Escalation only fires on process breakdowns, gaps, or blockers outside their control. |
| Escalation chain: P/M Lead → Sophia → Sage → you | Both sides of the chain use the 0–10 involvement scale. Per-project thresholds can be adjusted in the project soul — the chain itself does not change. |
| Each P/M Lead keeps their own to-do/pending list | The Lead has their own pending list (named `[lead]-pending-changes.md`) in their own folder, for their coursework and project work. Bigger changes — anything touching the framework, templates, or how the system itself runs — go up to Sophia's main list instead. Sage keeps an eye on both. (No P/M Lead on a project? Then there's no separate list — those items just live on Sophia's.) |
| This model grows with the company | The framework gets refined with each new live project that uses a P/M Lead. |
| Sage is Executive Officer for all P/M Lead work | When a P/M Lead is active, Sage is fully accountable for their performance — not just for the chain, but for the outcome. If the Lead fails, Sage owns it. ("Shit rolls uphill.") |

**Parallel Build Mode (PBM)**

| Rule | What It Means |
|---|---|
| Declare the track at session open | When a project has both a live track (active coursework, client work) and an infrastructure track (SOPs, architecture, setup) running at the same time, say which one you're working on today. |
| If you forget, Sage asks | Sage's job to catch it before any work begins — not the agents'. |
| Lane discipline | Live project work stays with the project. Infrastructure work stays with the SOPs, Jay's versions, and governance docs. The two don't bleed into each other. |
| Cross-lane items go up the chain | If something turns up that belongs in both tracks, it goes: whoever found it → Sophia → Sage (only if Sophia needs a CEO call). Nobody self-routes to both tracks. |

**Resource Build Standards**

| Rule | What It Means |
|---|---|
| Tri-form check before every build | Every tool Cosmo builds gets checked against three possible forms first: (1) command/slash command — you type it; (2) skill — Claude auto-invokes it when triggered; (3) hook — fires automatically on a named event. Build whatever forms fit. Cosmo decides which apply and documents the rationale. |
| Update one form → update all forms | If any version of a built tool is updated, all other versions must be updated in the same session. Extends Rule 13 (paired documents) to tools with multiple forms. |

---

**The comfort clause:** A score of 0 doesn't mean you're locked out. Any agent — including Sage — can come to you whenever a decision is needed. You're always reachable.

**The no-blame rule:** Mistakes get corrected, not punished. Top to bottom — you, Sage, all agents. Every mistake is expected to make the team better. We learn, grow, and improve with every project. The no-blame rule is not a pass to repeat the same mistake.

---

*This guide covers your role only. For full technical details, see Master Guide — Sage's Version (SOP v1).*
*For the complete non-negotiable rule list, see Hard Rules — Master List (SOP v1).*

---



































