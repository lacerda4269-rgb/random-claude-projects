# 3. Teams Lesson Log - TLL

**Owner:** Sophia (COO) manages; Sage routes
**Purpose:** Team-wide lesson capture — corrections and insights from every agent, every session.

---

## What This Folder Is

The Team Lessons Log is where the whole team gets smarter. Every time an agent makes a correction, surfaces a non-obvious insight, or learns something that would help future work — it gets logged here. Sophia manages the log; Sage routes entries from the field.

**File here (after Phase 0 setup):**
- `Team-Lessons-Log.md` — The live log. Sophia maintains it. Sage reviews and routes entries at session close.

**Blank version:** Empty at baseline. Phase 0 copies `Team-Lessons-Log (Blank Template).md` from `99.` and places it here.

---

## How the Three-File System Works

Lessons flow through three levels:
1. **TLL (this file)** — team-level lessons, agent-level corrections, session-by-session captures
2. **`lessons.md`** (in `.claude/memory/`) — project-scoped lessons, specific to this project's files and context
3. **`lessons_global.md`** (in `~/.claude/`) — lessons that apply to every future project; promoted from the other two when clearly universal

**AAR promotion:** At project close, Sage and Jay review TLL entries marked "AAR — pending review" and decide what to promote to agent souls, keep in the team log, or discard.

---

## Visual Companion (Mermaid code)

- `Lessons-Gotcha-Routing-Mermaid.md` — paired visual for the lessons/Gotcha routing flow (Sage corrections → `lessons.md` / `lessons_global.md`; agent lessons → TLL; recurring traps → `Gotcha.md`). A companion, not an SOP. **Paired-update rule (Gotcha Entry 36):** when the routing logic changes, this visual updates in the same pass.

---

*Sophia keeps it. Sage promotes it. The team gets smarter every project.*
