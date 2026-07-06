# Promotion Pipeline SOP

**Owner:** Sage
**Version:** 0
**Created:** 2026-04-19
**Updated:** 2026-05-24
**Status:** Active
**Future:** Convert to Cosmo skill during Master Library tasking

---

## Purpose

This SOP defines how lessons move through the system — from capture to permanent home. A lesson captured but never promoted is a lesson that gets forgotten the moment an agent starts fresh. Promotion is what makes the team actually smarter over time.

---

## The Three Files

| File | Scope | Owner | What Goes Here |
|---|---|---|---|
| `Team-Lessons-Log.md` | Project + team | Sage (Sophia executes) | Any agent's lessons, any session |
| `lessons.md` (project memory) | This project, Sage only | Sage | Sage-specific corrections tied to this project's structure |
| `lessons_global.md` (~/.claude/) | All projects, Sage only | Sage | Sage-specific corrections that apply everywhere |

Agent soul files are the destination for permanent agent-level lessons. The three files above are capture and routing — not final storage for agent behavior.

---

## Two Promotion Paths

### Hot Path — Immediate Promotion

**When to use:** The lesson is clearly universal, non-borderline, and shouldn't wait until project close.

**Trigger:** Sage identifies a lesson (from any agent or herself) that is obviously permanent.

**Steps:**

1. Sophia logs the entry in Team-Lessons-Log.md (standard format, same session)
2. Sage updates the agent's soul file with the new rule — same session, same commit
3. Sage marks the entry in Team-Lessons-Log.md: `Promoted to soul: Yes — [Agent] soul updated [Date]`
4. If the lesson is Sage-global: Sage adds it to lessons_global.md and notes promotion
5. No AAR required for hot path promotions — they are done and confirmed

### AAR Path — End-of-Project Review

**When to use:** The lesson is captured but borderline, or needs context from the full project before deciding.

**Trigger:** Project AAR session.

**Steps:**

1. Sage and Jay review all Team-Lessons-Log.md entries marked `Promoted to soul: AAR — pending review`
2. For each entry: decide promote / team log only / discard
3. **Promote:** Sage updates the agent's soul file. Sophia marks entry as promoted with date.
4. **Team log only:** Entry stays as a reference — no soul update. Sophia marks with reason.
5. **Discard:** Entry noted as not applicable. Sophia marks and moves to Retired section.
6. After all decisions: Sage confirms all promoted souls are updated in the Final Master IP folder

---

## Soul Carry-Forward Rule

Agents carry their souls from project to project. This is how they grow.

- **Source of truth — three-tier folder system in the Soul Folder:**
  - `0a. Basic Built Agents/` — soul built, no SOP yet (base level)
  - `[N]. [Name]'s Folder — Basic SOP/` — soul + Basic SOP built, Full SOP pending
  - `[N]. [Name]'s Folder/` — soul + Full SOP complete (highest tier)
- **At new project Phase 0:** Agents are pulled from the highest tier they have reached — not re-spun from scratch unless they are genuinely new (first-time build).
- **At project close (AAR):** All updated souls are written into the Final Master IP. No base versions.
- **New agents:** Spun up fresh at Phase 0 of the project that needs them. They start at base. They grow from there.

---

## Sage's Lesson Split — Quick Reference

| Lesson type | Where it goes |
|---|---|
| Sage correction — clearly universal | lessons_global.md (hot path or AAR) |
| Sage correction — project-specific | lessons.md (project memory) |
| Any agent lesson — project | Team-Lessons-Log.md → agent soul (hot path or AAR) |

---

## Notes

- Sophia logs but does not decide promotion. Sage decides. Jay approves at AAR if the change is major.
- An agent soul change is a significant edit — treat it as such. Version bump required on the soul file.
- This SOP feeds into the Session-Close-SOP (Step 5 updated) and the project AAR.

---

