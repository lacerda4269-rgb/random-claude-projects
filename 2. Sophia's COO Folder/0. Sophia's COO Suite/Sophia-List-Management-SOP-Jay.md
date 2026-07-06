# Sophia — List Management — Jay's Version

**Version:** 0
**Format:** Simple Guide (operator-facing)
**Ref:** `Sophia-List-Management-SOP.md` (v1.13) — full operational detail
**Created:** 2026-05-05 (Session 115)

---

## 1. What These Lists Are

Sophia keeps four lists throughout every project. Together they are the operational record — what's pending, what's done, what went wrong and got fixed, and what the team learned.

**Sophia's Pending Changes List** — the active queue. Everything that needs to happen eventually (source material updates, behavioral rules awaiting formal documentation, future project inputs, post-project items) lives here. It stays loaded every session. You see it at AAR.

**Sophia's Completed Changes List** — the archive. When items leave the Pending Changes List, they go here. Sophia's filing cabinet — not something you interact with directly.

**Gotcha.md** — the per-project watch list. Sophia's record of what went wrong, why, the fix, and the rule it produced. Stays loaded every session. You see it at AAR.

**Team Lessons Log** — team-wide lessons from every agent. Sophia manages it. Consulted at session close, compact close, and on demand. You see it at AAR.

> **Behind the scenes:** Two of these four lists load every session — Pending Changes and Gotcha.md. The other two (Completed Changes and Team Lessons Log) are on-demand only. This keeps the session-start context lean without losing access to the full record.

---

## 2. What You See

You don't interact with these lists during normal sessions. They run in the background.

What surfaces to you:

- **During sessions:** Occasionally Sage may raise a reclassification decision from the Pending Changes List that genuinely needs your call. Most reclassifications Sophia handles herself — this is the exception, not the norm.
- **At AAR:** Sophia presents the full Pending Changes List. You review it and decide what gets applied. That is the primary decision point for the whole project.
- **At AAR:** You'll also see Gotcha.md and the Team Lessons Log. These are reviewed for patterns — not for re-litigating old problems.

> **Behind the scenes:** Status labels on the Pending Changes List tell you where each item stands at a glance. The ones you're most likely to see: `Pending AAR` (waits for your decision at project close), `Moved to [project]` (has a named home in a future project), `Applied — Jay approved ✓` (an emergency mid-project override you approved; flagged for AAR review), `Complete ✓` (done, moves to archive at next compact or AAR), `Closed` (retired or no longer applicable).

---

## 3. Your Role

Small. That's intentional.

**During the project:** Nothing specific. Items surface through Sage and agents naturally. If a decision genuinely needs you, Sage brings it. Otherwise Sophia manages the lists without interrupting you.

**At AAR:** The AAR is a group effort — not you reviewing a list alone. At minimum: you, Sage, Sophia, and any agent whose work is directly affected by what's changing. Sophia determines who needs to be in the room based on what's on the Pending Changes List.

The main purpose of this review is to decide what should become a universal standard for every future project going forward. If something is agreed upon, the Master IP gets updated. You're the final approval authority — but nothing gets decided in a vacuum if it can be helped.

Each person who participated in the project also answers four questions at the AAR — including Sage:
1. What went right?
2. What went wrong?
3. What do we improve next time?
4. What did we build that should become a reusable tool for future projects?

> *Full AAR process: Sophia's COO SOP, Steps 14–15. Master Guide — Sage's Version, Section 7.*

**If something catches your eye mid-project:** Say it. Sage or Sophia will capture it and route it correctly.

---

## 3a. Triage Rating Scale

Before any item enters the Pending Changes List, it gets a 0–10 rating. The rating determines what actually happens to it.

| Rating | What It Means | What You See |
|--------|---------------|--------------|
| 0–2 | Work done immediately — no list entry | Item shows up in Completed Changes only |
| 3–4 | Sophia evaluates: completable now? | If yes → done, no list entry. If no → Brief C&P statement: `[Title — Rating N: what it is, estimated effort]` |
| 5+ | Standard queue item | Added to the correct section normally |

**Sophia's gatekeeper role on 3–4 items:** Sophia evaluates before anything lands on the list. If it can be done now — she does it. Only items that genuinely cannot be completed now surface to you as C&P statements. Your call: queue it or drop it.

**Ratings are reassessable.** A 7 today can become a 3 next session. Each rated item shows a "last rated: Session X" marker so stale ratings are visible.

---

## 4. Key Rules (Plain)

| Rule | What It Means |
|------|--------------|
| Items transfer at defined checkpoints only | Items move from Pending Changes to Completed Changes at session close, at your explicit request, at major COHK reviews, or at AAR. Never mid-session. Compacts do not trigger transfers by default; project-level SOPs may add compact close as a trigger with your explicit approval. |
| Quick Stats update at scrub time, not at transfer | When an item's status changes, the Quick Stats count adjusts immediately. When the physical transfer runs at session close, the numbers don't change again — they were already updated. Seeing no change to the count at transfer time is correct. |
| Source materials are frozen mid-project | Anything needing to change in CLAUDE.md, Master Guides, templates, or souls goes to Pending Changes — it is never applied until after AAR. Emergency exception: you explicitly approve it in-session, and it gets flagged for AAR review. |
| AAR is the decision point | The Pending Changes List builds the whole project. You decide what gets applied at the end — not before. |
| Completed Changes is the archive, not the record | The active operational record is the Pending Changes List. Completed Changes is where resolved items go to rest. |
| Gotcha.md is the watch list, not a blame log | It records what went wrong and what the fix produced as a standing rule. The point is to not repeat it — not to track who caused it. |
| P/M Leads keep their own list | When a P/M Lead owns a dedicated pending list (say, for a live coursework or client track), coursework and project-execution items go to that lead's list. Source-material and structural changes still go to Sophia's list. Sage reviews both. (Full rule below.) |

---

## 4a. The P/M Lead Pending List — How It Works (Plain)

When a project runs with a P/M Lead, that lead keeps their own pending list. Here's the simple version of how it works:

- **Who owns it:** The P/M Lead owns and maintains their own list. Sophia doesn't manage it day-to-day. Sophia still owns the main project Pending Changes List for everything structural and source-material.
- **Where it lives:** In the P/M Lead's own personal folder (the same folder that holds their project soul). If a project has *no* P/M Lead, there's no separate list — everything just goes to Sophia's list as normal.
- **What it's called:** `[lead]-pending-changes.md` — the lead's name, lowercase, hyphenated. A lead named "Casey" would have `casey-pending-changes.md`. One list per lead.
- **What goes where (the simple test):** *Does this change anything outside the lead's own project work?* If no — it's their own coursework or execution work — it goes on their list. If yes — it touches CLAUDE.md, a Master Guide, a template, governance, or anything beyond their one project — it goes on Sophia's list. Sage reviews both.
- **The one hard rule:** The moment a P/M Lead's list is created, a pointer to it gets added to the project file index in the same pass — naming the file, its owner, and where it lives. A list nobody can find is the same as no list. Created list, created pointer — always together.

---

*Ref: `Sophia-List-Management-SOP.md` v1.12 for full operational procedures, section definitions, status label logic, and transfer rules.*
*Both versions maintained together per Hard Rule 13.*

---

## Hard Rule 19 — How Sophia Handles Blockers

When Sophia hits a wall, she doesn't just retry the same thing. She classifies the problem first:

- **Her lane, her task:** She tries a new approach (Round 1). If that fails, Sage and Sophia figure out a different direction together (Round 2). If Round 2 fails — stop. Sophia tells Sage exactly what happened, and Sage brings it to you if needed.
- **Bigger than her lane** (affects other agents or the project approach): Straight to Sage. Sophia does not spend rounds on a problem that isn't hers to solve.
- **Touches your goals or company direction:** Sage brings it to you.

---

## Version Log

| Version | Date | What Changed | Why |
|---------|------|-------------|-----|
