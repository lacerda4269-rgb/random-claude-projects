# Team Lessons Log

**Owner:** Sage (CEO)
**Executor:** Sophia (COO)
**Project:** Random Projects
**Version:** 0
**Created:** 2026-07-06 (Session 1)
**Updated:** 2026-07-06 (Session 1)
**Status:** Active

---

## Purpose

A living record of lessons any agent on this team has learned — from any session, any project phase, any role. The goal is simple: make the team smarter over time without relying on memory.

This is not a blame log. It is not a policy document. It is an honest record of the gap between what was expected and what actually happened — and the rule that closes that gap going forward.

---

## What Belongs Here

- Any agent (including Sage) surfaces a lesson during a project session
- Lessons must be non-obvious — "test before committing" is a reminder, not a lesson
- Scope: team-wide. If it applies only to Sage, it goes to Sage's lessons files instead

**Does NOT belong here:**
- Policy and rules → Hard Rules or SOPs
- Items already captured in Sophia's Pending Changes → stay there
- Sage's personal operational corrections → lessons.md (project) or lessons_global.md (global)

**Multi-agent attribution convention:** When a lesson is team-wide with no single source agent, attribute as `Team`. When a lesson emerged from a specific collaboration between two named agents, attribute as `[Agent A] + [Agent B]`. `Team` = lesson applies to all agents equally, no single source. Named pair = lesson from a specific two-agent collaboration.

---

## Contribution Path

1. Any agent identifies a lesson during a session
2. Agent reports to Sage
3. Sage routes to Sophia with a brief: what happened, why, rule going forward
4. Sophia logs it here — same session, no queuing
5. **Hot path:** if the lesson is clearly universal and agent-specific, Sage promotes it to that agent's soul immediately — does not wait for AAR
6. **AAR path:** at project close, Sage and Jay review all entries — determine what gets promoted to agent souls and what stays as team log only

**Sophia's own lessons:** Sophia is both the executor of this log and a contributor to it. She works every session. At every session close and compact wrap-up, Sage asks Sophia directly whether she has any lessons worth logging. Sophia surfaces to Sage; Sage confirms scope; Sophia self-logs.

---

## Quick Reference

| # | Session | Date | Agent | Topic (brief) | Promotion Status |
|---|---------|------|-------|---------------|-----------------|
| 1 | 1 | 2026-07-06 | Sophia | Template→live instances don't self-rebase — governance/meta docs must be flipped at Phase 0 | AAR — pending review |
| 2 | 1 | 2026-07-06 | Soren | A read-only web repo clearance can't run the automated CVE scan — deliver as CLEARED WITH CONDITIONS, carry the scan as a build-time gate | AAR — pending review |
| 3 | 1 | 2026-07-06 | Rose | Flag operator-owned/adjacent repo provenance as an early question for Jay — a cheap human confirm collapses a whole licensing branch | AAR — pending review |

---

## Entry Format

```
## Entry [N] — Session [N] — [Date] — [Agent]

**What happened:** [Specific situation — not a vague summary]

**Why it happened:** [Root cause]

**Recurrence:** First occurrence / Recurrence of Entry [N] — [brief note on what pattern repeated]

**Rule going forward:** [The adjustment — specific and actionable]

**Promotion status:** [Hot path / AAR — pending review / No — team log only / Applied same session]
**Promotion destination:** [file name + entry or section reference if promoted | Pending if AAR | N/A if no promotion]
```

---

## Log

## Entry 1 — Session 1 — 2026-07-06 — Sophia

**What happened:** At Phase 0 activation, the empty folders got filled correctly, but the documents that *describe* the structure — the three governance docs and the root README — silently kept their MUIP "baseline template / no project-specific content" framing, which now directly contradicted the live Random Projects reality. The gap wasn't visible because the folders looked done; only the meta-docs still read as a blank template. Caught at the Step 0 pre-close sweep.

**Why it happened:** Instantiating a template package (MUIP → live project) fills structure but does not re-base identity. Nothing in the activation flow flips a doc's self-description from "template" to "instance," so the descriptive/reference layer lags the physical one.

**Recurrence:** First occurrence.

**Rule going forward:** At Phase 0, treat every inherited "baseline/template" status line and self-description as a re-base target — not just the empty folders. The folders get filled; the docs that describe the structure must have their identity flipped from template to live instance in the same pass. Applies to any future template-instantiated project, not just this one.

**Promotion status:** AAR — pending review (paired with Pending Changes AAR item 1: add a governance-docs update step to Getting-Started Phase 0).
**Promotion destination:** Pending — candidate for `Getting-Started.md` Phase 0 sequence and/or `lessons_global.md`.

---

## Entry 2 — Session 1 — 2026-07-06 — Soren (security domain)

**What happened:** Soren cleared the `board` repo for the Jot mini-project via a read-only web review (manual source read + provenance via api.github.com and raw.githubusercontent.com). That path could fully cover the source review but structurally could not run the automated CVE/dependency scan, which needs a local clone.

**Why it happened:** A web-only clearance and a local automated scan are two halves of one clearance, not substitutes. Treating the web review as complete would have shipped an unscanned dependency tree into the build.

**Recurrence:** First occurrence.

**Rule going forward (verbatim):** "A read-only web clearance of a GitHub repo can fully cover manual source review and provenance (via api.github.com + raw.githubusercontent.com), but it structurally cannot run the automated CVE/dependency scan — that needs a local clone. Don't treat a web review as a complete clearance. Deliver it as CLEARED WITH CONDITIONS and carry the automated scan forward as an explicit build-time gate. The web review and the local scan are two halves of one clearance, not substitutes for each other."

**Promotion status:** AAR — pending review.
**Promotion destination:** Pending — candidate for Soren's soul / security SOP.

---

## Entry 3 — Session 1 — 2026-07-06 — Rose (research domain)

**What happened:** Rose's fit report on the `board` repo flagged provenance (is The-Coding-Trader Jay's own account?) as an open question rather than vetting it as an unknown third party. A one-line human confirm from Jay (a friend's account; MIT settles legal either way) collapsed the entire licensing/provenance branch.

**Why it happened:** Vetting operator-adjacent provenance as if it were an anonymous third party burns research effort that a cheap early question to Jay can eliminate.

**Recurrence:** First occurrence.

**Rule going forward (verbatim):** "When research surfaces a repo that may be operator-owned or operator-adjacent, flag provenance as an explicit question for Jay early rather than vetting it as an unknown third party — a cheap human confirm can collapse an entire branch of licensing/provenance work, as it did here."

**Promotion status:** AAR — pending review (Rose suggested lightweight weight; Sage's call).
**Promotion destination:** Pending — candidate for Rose's soul / research SOP.

---

*All three Active Agents Check respondents logged by name (Sophia, Soren, Rose). Soren additionally verified `charm.land` is Charmbracelet's official vanity import domain, closing Rose's typosquat concern — handoff completed, recorded in the Session 1 Summary reconciliation note.*

---

## Version Log

| Version | Date | What Changed | Why |
|---------|------|-------------|-----|
| 0 | 2026-07-06 | Created at Phase 0 (Random Projects, Session 1) | Project activation — Getting-Started §4 |
