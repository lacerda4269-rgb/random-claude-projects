# Cross Talk / Fire Drill SOP

**Owner:** Sage
**Version:** 0
**Created:** 2026-05-19 (Session 161)
**Updated:** 2026-05-20 (Session 164)
**Status:** Active
**Future:** Convert to Cosmo skill during Agent Onboarding / Master Library tasking
**Jay's Version:** Mermaid visual workflow — `CrossTalk-FireDrill-Mermaid.md` in the SOPs folder

---

## Purpose

The Cross Talk / Fire Drill is a recurring operational health check for the entire company system. It runs at Jay's or Sage's direction — not on a fixed schedule. It is not a one-time project. Every time it runs, the system gets an honest look at what's broken, missing, or misaligned before those problems compound into something that blocks real work.

**Two components, always together:**

- **Cross Talk** — Agents independently review their own domain and report upward. No briefing first; no hint of what the answer should be. The value is in what they surface without prompting, and especially where two agents find the same gap from opposite sides. That's the Cross Talk signal — it confirms the gap is real, not a misread.
- **Fire Drill** — A system-wide three-pass audit applied to all surfaced findings: Content, Trigger, Timing. Every accepted item gets sorted into the pass that caught it. Multiple passes for one item is normal.

Both components run together. Neither is optional.

---

## Trigger

- Jay calls it explicitly — "Fire Drill," "Cross Talk," or any equivalent phrase
- Sage calls it — when operational health is in question, a major new phase is about to open, or a significant system change has just landed
- No fixed cadence required — runs on judgment, not a calendar

**When to strongly consider it:**
- Before a new project opens that depends on prior work being clean
- After a significant structural change: new agent built, major SOP overhaul, folder restructure, new pipeline added
- When something feels off and the root cause isn't obvious

---

## Readiness Check

Before the Fire Drill runs, Sage confirms the following. If any are missing, note it — that is a finding in itself, not a blocker.

1. Are the relevant SOPs, souls, and documents accessible and current enough to be meaningfully audited?
2. Have the agents being asked to review actually worked with the material they're reviewing?
3. Is Jay available for the decision gate at the end? If not, plan the session around that constraint.
4. **Hard Rule 5 — Rose META check:** For the first Fire Drill run on any given project, queue Rose for a security META check (latest AI security threats, prompt injection vectors, emerging protective measures) before the scope brief goes out. Soren reviews findings per standard pipeline. For subsequent runs within the same project: HR5 is optional unless Sage judges the security landscape has materially changed since the last META check. Note: this item fires at the *first* run only — it is a project-open trigger, not a per-run requirement.

**Minimum readiness:** At least one version of each document an agent is expected to review must exist. An empty or stub system cannot be audited in a meaningful way.

---

## Step 1 — Scope Brief

Sage issues a scope brief to all participating agents before reviews begin.

Brief includes:
- What each agent is reviewing — their own domain (souls, SOPs, research reports, catalog, tools, etc.)
- The lens to apply: *"What's broken, missing, incomplete, or unconnected to a real trigger in YOUR area? Be specific. Item label, what you found, why it matters."*
- The independence rule: agents do not see each other's findings before submitting their own. Cross-lane convergence on the same item is a Cross Talk signal — it only has value if the convergence is genuine, not influenced.
- Deadline: same session unless scope is very large enough to warrant splitting.

**Agent domain assignments (standing):**

| Agent | Domain |
|-------|--------|
| Soren | Clearance pipeline, pending flags, security protocol consistency |
| Lexi | Master Library structure, file organization, catalog integrity |
| Sophia | Operational files, documentation standards, queue health |
| Cosmo | Skill/hook candidates, "Future: Convert" notes across all SOPs and workflows |
| Rose | Research pipeline, protocol compliance, pending research items |
| Nick | NinjaTrader domain — soul and SOP consistency |
| Todd | TradingView domain — soul and SOP consistency |
| Pete | Python domain — soul and SOP consistency |
| Vicky | Videographer domain — toolset status, soul and SOP consistency |
| Feynman | Academic research domain — soul and SOP consistency (activate if applicable) |

Sage and Sophia run their own pass after all agent reports are in.

---

## Step 2 — Bottom-Up Review

Each agent reviews their domain and reports findings. Reports include three fields:
- **Item label** (agent initial + sequential number: S-1, V-1, L-1, etc.)
- **What was found** — describe the gap, inconsistency, or missing element specifically
- **Why it matters** — what breaks, gets confused, or stays invisible if this isn't addressed

Agents report findings. Sophia and Sage handle categorization and recommendations.

**Rule:** No agent reads another agent's report before submitting their own. Sage collects all reports before any cross-referencing begins.

**Sage and Sophia's own pass** follows after all agent reports are collected. Sage applies a CEO lens (cross-system consistency, three-pass classification, altitude check). Sophia applies a COO lens (file consistency, structural health, Gotcha entries, list health).

---

## Step 3 — Sophia's Filter

Sophia reviews each item through the WHY lens before it reaches Sage:
- Why was the original decision made?
- Is the agent's reading of the gap correct?
- What is the recommended action?

Sophia categorizes each item:
- **Accept** — gap is real, agent's reading is correct, action warranted
- **Accept with context** — gap is real, but there is important background that shapes how it's addressed
- **Flag to Jay** — design question or decision that isn't Sophia's to make
- **Confirm deferral** — item is already correctly deferred; no new action needed

Sophia also runs her COO pass:
- File consistency checks (paired documents, version alignment, naming conventions)
- Gotcha.md entries for any new operational watch items surfaced in the review
- Sophia pending list health check — are new items landing in the right sections?

---

## Step 4 — Sage's Routing

Sage reviews Sophia's filtered list and assigns a routing rating to each accepted item:

| Rating | Action |
|--------|--------|
| 0–2 | Sage handles — no Jay input needed |
| 3–5 | Sage handles — flag to Jay as FYI |
| 6–10 | Jay decision required — nothing moves without Jay's call |

**Three-altitude check (Hard Rule 19) applied before routing:**
- Task level (within current scope and an agent's lane): route per table above
- System level (affects multiple agents, overall design, or pipeline architecture): surface to Jay directly — skip the routing table
- Vision level (touches company direction or end goals): surface to Jay immediately

---

## Step 5 — Three-Pass Audit

After routing, Sage sorts all accepted findings into the three-pass framework. This is not a separate review — it is a classification step applied to the findings already surfaced. Some items fit more than one pass; note all that apply.

**Content Pass — Is every step present, in the right order, and complete?**
- An SOP exists but a required step is missing, out of sequence, or incomplete
- An agent soul references a document, rule, or standard that doesn't exist yet
- A template or format was defined but never propagated to the files that need it

**Trigger Pass — Is there a mechanism that actually fires each step?**
- A step is in an SOP but nothing causes it to execute at the right moment
- A rule exists in a soul or behavioral standard but has no hook, gate, or activation condition
- A process was deferred to "first live use" with no mechanism ensuring it fires before first live use
- *"It's in the SOP" is not a trigger. The question is: what causes it to run?*

**Timing Pass — Are steps firing at the correct point in the sequence?**
- A step fires too early, causing state changes that outpace the documentation meant to capture them
- A step fires too late, meaning a gap was live for multiple sessions before being caught
- A trigger exists but is positioned incorrectly in the sequence — it runs after it needed to

---

## Step 6 — Jay Decision Gate

All items rated 6–10 are presented to Jay in a clear decision list:

| Column | Content |
|--------|---------|
| Item | Agent item label and short description |
| Rating | Sage's assigned rating |
| Sage's recommendation | Recommended path, trade-offs if relevant |
| Jay's decision | Approve / Redirect / Defer |

Jay must make a call on every 6–10 item before the Fire Drill can progress. Items rated 0–5 that have already been actioned are reported as FYI at this gate — no decision required, just awareness.

**Rule:** No item rated 6–10 is actioned without Jay's explicit decision. Sage's recommendation is not a substitute.

---

## Step 7 — Resolution and Tracking

After Jay's decisions are in, all accepted items are resolved or formally parked:

1. **Gotcha.md entries** — any operational watch items (traps, recurring gaps, timing failures) logged to the project Gotcha.md using the v2.0 block format. See Gotcha.md Field Definitions for the block structure.
2. **Sophia's pending list** — all accepted items with a known activation point queued to the correct project section with a triage rating.
3. **Agent soul / SOP corrections** — any immediate corrections that can be actioned in-session are done. Anything requiring a dedicated project is queued to Sophia's list.
4. **LHF and Suggested Project Order** — status markers updated as items resolve, activate, or get formally parked.
5. **Permanent review report** — the full bottom-up review report is filed as a permanent project record. Sophia or Sage authors it. It does not get deleted or superseded by future runs — each run produces its own permanent record.

---

## Step 8 — Project Close Gate

**Status does not move to Complete ✓ until Jay gives explicit approval.**

Before closing, confirm:
- All deliverables from this run are produced
- All accepted items are either resolved in-session or formally queued with a named home
- The permanent review report is filed
- Jay has reviewed the full set of outputs and findings

**Jay's explicit approval is the only close trigger.** No agent, and not Sage, can mark the Fire Drill complete independently.

---

## Outputs

Every run of the Cross Talk / Fire Drill produces:

- Permanent bottom-up review report (filed as project record — never deleted)
- Gotcha.md entries for all operational watch items surfaced
- Sophia pending list updates — all accepted items queued to named projects
- Routing summary — 0–5 actioned items + 6–10 Jay decisions
- Status updates to LHF and Suggested Project Order

---

## Notes

- **Recurring process:** The Fire Drill runs 0 to infinite times per project, at Jay's and Sage's judgment. Same model as COHK — no fixed cadence, no lifecycle gate beyond Jay's discretion.
- **Independence is the mechanism:** The value of Cross Talk comes from agents reviewing their own domain without seeing what others found first. If that independence is broken, the cross-lane convergence signal is lost. Protect it.
- **Cross Talk signal:** Two agents finding the same gap from opposite sides without coordination is not coincidence — it is confirmation. Flag it explicitly. It is stronger evidence than a single agent's finding.
- **Minimum readiness matters:** Don't run the Fire Drill on a blank or stub system. There must be something real to audit. If major pieces are missing, note it and either wait or scope the review to what exists.
- **Project Close Gate is Jay's call, always:** No team member marks the Fire Drill complete. Jay's explicit approval is required every time.
- **Paired documents:** This SOP has a Jay's version — the Mermaid visual workflow in the SOPs folder (`CrossTalk-FireDrill-Mermaid.md`). Both must be updated together when this SOP is revised (Hard Rule 13).

---

