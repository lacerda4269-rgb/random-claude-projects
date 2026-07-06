# Internal Build Record — Jay's Version

**Format:** Plain-language guide
**Ref:** `internal-build-record.md` — full format standard (Agent Version)
**Owner:** Sophia (COO)
**Created:** 2026-05-29 — Session 192
**Status:** Active — Jay's version (two-version rule)
**Travels with every project** — lives in Sophia's COO Folder alongside the Agent Version.

---

## What This Is

The Internal Build Record is Sophia's index of everything Cosmo builds for the team — skills, hooks, MCPs. Unlike external tools (which go through Rose → Soren → Lexi), internally built artifacts don't come from outside. Cosmo builds them, Sage reviews them, and Sophia files the record. This document is your plain-language version of that index.

One record gets written every time Cosmo completes a build. Each record tells you: what got built, what it does, what triggers it, and that Sage signed off on it before it went live.

---

## When an Entry Gets Created

Every time Cosmo finishes building a skill, hook, or MCP — one record per artifact. The record is not written until the build is complete and Sage has reviewed it.

**No entry = not formally filed.** Until both the Agent Version (full technical detail) and this Jay Version (plain language) exist for an artifact, it is not considered fully recorded. One without the other is not done.

---

## What Each Entry Contains

| Field | What It Means |
|-------|--------------|
| **What It Does** | Plain description — what behavior the artifact triggers or enables, and why it was built |
| **Trigger or Invocation** | How it fires — automatically on an event, when Sage calls it, via agent slash command, or on file save |
| **Scope** | What it touches — which agents, files, or project phases it affects; what it explicitly does NOT affect |
| **Dependencies** | What it needs to function — other tools, permissions, or configurations; "None" if clean |
| **Known Limitations** | Edge cases or conditions where it may not behave as expected; "None identified" at build time is valid |
| **Build Reference** | Pointer to the SOP or skill document governing its design |
| **Sage Review** | Confirmation Sage reviewed it — this substitutes for the external Soren clearance |

---

## How It Gets Into the Master Library

When the record is complete, Sophia hands it to Lexi. Lexi files it in the Master Library catalog with these values:

- **Source:** "Internally built — [builder's name]"
- **Soren column:** "Internally built — Sage-reviewed" (Sage's review replaces the external clearance pipeline — internal builds skip Rose and Soren entirely)
- **Report column:** Link to the completed record file

The path for internal builds is: Cosmo builds → Sage reviews → Sophia files the record → Lexi catalogs. No external sourcing pipeline applies.

---

## Key Rules

| Rule | What It Means |
|------|--------------|
| One record per artifact | Every internally built skill, hook, or MCP gets its own entry — no bundling multiple builds into one record |
| Both versions required | This Jay Version and the Agent Version must both exist; one without the other is not done |
| Sage review required before filing | Sage signs off before Sophia delivers to Lexi — this is the internal clearance substitute |
| No external pipeline | Internal builds skip Rose → Soren → Lexi. Path: Cosmo builds → Sage reviews → Sophia files → Lexi catalogs |

---

*Internal Build Record — Jay's Version*
*Sophia (COO) — Session 192, 2026-05-29*
*Paired with: `internal-build-record.md` (Agent Version v1.0) per Hard Rule 13*
