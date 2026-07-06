# Internal Build Record — Format Standard

**Version:** 0
**Created:** 2026-05-14
**Author:** Sophia (COO)
**Status:** Active
**Travels with every project** — lives in Sophia's COO Folder; pulled during Phase 0 with all other Sophia resources.

---

## Purpose

This is the documentation standard for internally built artifacts — hooks, skills, and MCPs that Cosmo builds rather than sourced from an external provider. It is a standalone format, parallel to Rose's research report format standard (rose-report-format-standard.md), and serves the same function: a consistent, complete record that gives Lexi everything she needs to catalog the artifact correctly.

This standard covers **internally built artifacts only.** For externally sourced resources (tools, CLIs, MCPs brought in from outside), the pipeline runs through Rose and Soren — use the research report format standard for those.

---

## Template

Use one completed record per artifact. Copy the block below; fill in every field.

---

**Builder:** [Agent name]
**Build type:** [Hook / Skill / MCP / Other]
**Session built:** [Session number]
**Date:** [YYYY-MM-DD]
**Status:** [Active / Draft / Superseded]

## What It Does

[One paragraph. Plain-English description of what this artifact does, what behavior or outcome it is designed to trigger or enable, and why it was built. No jargon that is not immediately explained.]

## Trigger or Invocation

[How this artifact fires or is called. Examples: event-triggered on session close / manually invoked by Sage / called by agent via slash command / runs on file save. One to two lines.]

## Scope

[What this artifact acts on. Which agents it touches, which files it reads or writes, what phases or sessions it is active in. What it explicitly does NOT affect — boundaries matter here.]

## Dependencies

[Other artifacts, tools, permissions, or configurations required for this artifact to function. If none: "None."]

## Known Limitations or Conditions

[Edge cases, failure conditions, constraints, or situations where this artifact may not behave as expected. If none identified at build time: "None identified."]

## Build Reference

[Link or path to the SOP or skill document that governs this artifact's design and behavior. If the SOP has not been written yet: "SOP pending."]

## Sage Review

[Sage-reviewed — Session [N]]

---

*Internal build record by [builder name] | Session [number] | [date]*

---

## Catalog Entry — What Lexi Receives

When an internally built artifact is ready for cataloging, Sophia delivers the completed record to Lexi. Lexi files it using the following column values:

| Column | Value |
|--------|-------|
| **Source** | Internally built — [Builder name] |
| **Soren** | Internally built — [Builder name]; Sage-reviewed |
| **Report** | Link to the completed internal-build-record file for this artifact |

**No external Soren clearance pipeline applies.** Internal artifacts do not go through the Rose → Soren → Lexi pipeline. Sage review substitutes for Soren clearance. The "Soren" column is populated to confirm that review occurred — it is Sage who conducted it, not Soren.

---

## Two-Version Rule

Every completed internal-build-record file is the **Agent Version** — full operational detail, built for agents and Sage.

A **Jay Version** — plain-language equivalent, written for Jay's index — is a future item for each artifact and is not blocking for the first build. When the Jay Version is created, it links from the same catalog entry.

One without the other is not done. The Jay Version is deferred, not optional.

---

## Version Log

| Version | Date | Session | Notes |
|---------|------|---------|-------|
