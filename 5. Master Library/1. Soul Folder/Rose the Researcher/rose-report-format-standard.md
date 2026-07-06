# Rose — Research Report Format Standard

**Version:** 0
**Created:** 2026-05-13
**Author:** Rose (Research Specialist)
**Status:** APPROVED — format standard confirmed permanent at Dr. Frankenstein Phase 2 open (Session 167). This is the permanent baseline going forward.

---

## Purpose

This document is the authoritative format reference for all research reports filed to the Master Library. It captures the complete report structure in order, including all five format additions approved after Dr. Frankenstein Phase 1 (Cosmo's builder review, Session 145). All future reports use this standard.

This is the first formalization of the report format. It did not exist as a written standard before this document.

---

## Standard Report Structure

The sections below represent every field in a complete research report, listed in the order they appear. Required fields appear in all reports. Section-specific fields apply only where noted.

---

### Header Block

```
# Resource Report: [Item Name]

**URL:** [source URL]
**Date Researched:** [date]
**Researched by:** [Rose | Security pre-check: Soren | Report by: Rose (or Sophia for older reports)]
**Already in Master Library?** [Yes — [section/entry] | No — [source description]]
```

---

### ## What It Is

One paragraph. Plain-English definition of what the resource is. No jargon assumed — if a term is used, it can be understood from context.

---

### ## What It Does

Bulleted list. Concrete capabilities — what the tool does, not what it is. Distinct from "What It Is."

---

### ## Invocation Interface
*(Section 3 — CLI reports only)*

- **Typical command pattern:** One-line example showing the most common invocation
- **Output format:** plain text / JSON / binary / mixed
- **Key structured output flags:** flags that change output format (e.g., `--json`, `--format`, `--output`)
- **Exit code behavior:** exit 0 = success; what non-zero exits mean (e.g., exit 1 = error, exit 2 = critical failure/blocking)
- **Stdin/stdout/stderr notes:** only if non-standard or relevant to hook/skill integration

Position: After "What It Does," before "Relevance to This Project."

---

### ## MCP Tool Manifest
*(Section 4 — MCP Server reports only)*

- **Tool count:** [number] tools
- **Tools:**
  - `tool_name` — one-line description of what it does
  - `tool_name` — one-line description of what it does
  - *(continue for all tools)*
- **Transport type:** stdio / Streamable HTTP
- **settings.json registration:**
```json
{
  "mcpServers": {
    "[server-name]": {
      "command": "[command]",
      "args": ["[arg1]", "[arg2]"],
      "env": {
        "OPTIONAL_VAR": "value"
      }
    }
  }
}
```

**serverInstructions Field Convention:**

`serverInstructions` is Claude's orientation to a server before any tool is called. It answers: *why would I reach for this MCP, and what should I expect from it?*

It is NOT:
- A duplicate of individual tool descriptions (those live in the MCP schema)
- A setup guide or installation walkthrough
- Marketing copy
- A list of every tool the MCP exposes

**What belongs:**

Every entry should answer three questions, in order:

1. **What does this server do?** One sentence. Functional, specific. If you can't state the function in one sentence, note the scope issue in the report — but still try.
2. **When should Claude reach for it?** One sentence. The routing signal. What situation triggers this MCP vs. a CLI vs. another MCP? Include this even when the name seems obvious — it prevents misrouting when similar MCPs are loaded together.
3. **Key tools or capabilities** *(optional — include when 3+ tools or non-obvious scope)*: A short phrase list or one additional sentence. Not exhaustive — just enough for Claude to pattern-match on first contact.

Template (adapt, don't copy verbatim):
```
"This server [does X]. Use it when [situation Y]. Key capabilities: [brief phrase list]."
```

**What does NOT belong:**
- Per-tool details (those go in individual tool descriptions)
- Setup, config, or version info
- Warning blocks or multi-sentence caveats
- Repetition of the server name ("The [name] MCP server is a server that…")
- Filler language ("powerful and versatile tool that can help…")

**Format:**
- **Length:** 1-3 sentences. Hard ceiling: 3 sentences. If you're past 3, trim.
- **Tone:** Functional and direct. Write for Claude, not a human reader.
- **Structure:** Free-form prose. No headers, bullets, or markdown inside the field — the string is injected into context directly.
- **Voice:** Third person for the server ("This server…"), imperative for routing ("Use it when…").

**Edge cases:**

- **Single-tool MCPs:** One sentence, routing-signal focused. Skip the capabilities phrase.
- **Name-obvious MCPs:** Still write it — include the routing signal for when similar MCPs coexist ("Use it for email, not calendar or Drive").
- **Sensitive systems (trading execution, file write, financial data):** Include one in-line constraint phrase: `"…Executes live trades — do not invoke without explicit user instruction."` Not a warning block — one phrase, in the flow.
- **RETROFIT status (no tool manifest yet):** Write function and scope from available docs. Omit the capabilities phrase. Append: `"— capabilities TBD pending tool manifest review."`

**Checklist (use when writing the field):**
- [ ] One sentence on function
- [ ] One sentence on routing signal
- [ ] Capabilities phrase — only if 3+ tools or non-obvious scope
- [ ] No per-tool details, no setup info, no filler
- [ ] No markdown formatting inside the field string
- [ ] 1-3 sentences, hard ceiling
- [ ] Sensitive system? One in-line constraint phrase
- [ ] RETROFIT? Flag TBD + omit capabilities

Position: After "What It Does," before "Relevance to This Project."

---

### ## Relevance to This Project *(as of research date — context may not carry to future projects)*

One to three paragraphs. Project-specific framing — why this resource matters here, what it enables, how it fits into the current build. Not a repetition of "What It Does."

---

### ## Builder Footprint
*(Sections 1, 2, 3, 3a, 4, 8 — external resource reports only)*

- **Integration type:** [choose one or more: Standalone tool / CLI-invocable / MCP tool layer / Skill-composable / Hook-triggerable]
- **Extension points:** [APIs, plugin hooks, or event streams Cosmo can build against — or "None identified"]
- **Build complexity signal:** [Simple (~1–2 hours, e.g., wrapping an existing CLI) / Moderate (~half-day, e.g., custom integration layer) / Complex (multi-day, e.g., new MCP or Python engine)]
- **Known conflicts:** [Does this overlap with existing ML items in ways Cosmo should know before building? Check the catalog. — or "None identified" / "Not checked — catalog access unavailable"]

Position: After "Relevance to This Project," before "ML Assessment."

---

### ## Master Library Assessment

```
- **Proposed Section:** [number and name]
- **Proposed Tier:** [1 / 2 / 3]
- **Rationale:** [one to two sentences on why this tier]
```

For Section 7 (Reference & Ecosystem) reports only, add one line inside this section after Tier:

```
- **Deployment Potential:** [None / Indirect / Conditional]
```

- **None** — read-only reference; no components to build with
- **Indirect** — patterns and concepts worth applying; no direct integration path
- **Conditional** — contains deployable components; individual clearance required per component before deployment

---

### ## Soren Security Pre-check

```
- **Verdict:** [CLEARED / CLEARED WITH CONDITIONS / FLAG / HOLD]
- **Checked:** [what was reviewed: stars, commits, license, patterns, code audit, etc.]
- **Notes:** [conditions, flags, or clearance constraints — if none, brief confirmation of clean check]
```

When any flag exists at CRITICAL or HIGH severity — use the table below regardless of flag count. For a single-condition entry at MEDIUM severity or below — prose is acceptable.

```
| # | Severity | Flag | Notes |
|---|----------|------|-------|
| 1 | CRITICAL | Item | Detail |
| 2 | HIGH | Item | Detail |
| 3 | MEDIUM | Item | Detail |
```

Severity levels: CRITICAL / HIGH / MEDIUM / LOW / INFO

Note: Severity-rated table is the going-forward standard. Retroactive severity rating on older reports is Soren's judgment — not Rose's lane.

---

### ## Recommendation

One to three sentences. What to do with this resource: add to ML at what section/tier, when to install, any conditions or prerequisites. This is Rose's recommendation — Sage and Jay make the final call.

---

### ## C&P Summary

Required in every report. Single plain-English paragraph. Explains what the resource is and does, written for a non-technical reader. No jargon, no assumed knowledge. If Jay can read it and immediately understand what the thing does and why it matters — the C&P is done. A report without a C&P is an incomplete report.

---

### Footer Attribution

```
---
*Report by [name] | Session [number] | [date]*
```

---

### ## Report Version Log
*(All reports — applied at first substantial revision. v1.0 = current state when block is first applied; no backfilling of pre-block history. The Session Summary entry for the session in which the block is applied serves as the provenance record for all prior changes.)*

```
## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
```

Subsequent revisions add a new row. Applied by Rose when a report receives its first substantial update (freshness sweep, retrofit, or new section addition).

Position: After Footer Attribution, as the final field in the report.

---

## Section-Specific Variant Summary

| Section | Extra Field | Position | Going-Forward or Retroactive |
|---------|-------------|----------|-------------------------------|
| 3 — CLI | `## Invocation Interface` | After "What It Does," before "Relevance" | Going-forward only |
| 4 — MCP | `## MCP Tool Manifest` | After "What It Does," before "Relevance" | Retroactive (all existing Section 4 reports) |
| 1, 2, 3, 3a, 4, 8 — external resources | `## Builder Footprint` | After "Relevance to This Project," before "ML Assessment" | Retroactive for Tier 1 items; going-forward for all |
| 7 — Reference & Ecosystem | `Deployment Potential:` line in ML Assessment | Inside ML Assessment, after Tier | Going-forward only |
| All sections | Severity table in Soren Pre-check | Required when any flag is CRITICAL or HIGH (regardless of count); prose acceptable for single MEDIUM-or-below conditions | Going-forward only; retroactive severity rating is Soren's call |
| All sections | `## Report Version Log` | After Footer Attribution — final field | Applied at first substantial revision (going-forward); v1.0 = current state when block applied; no backfilling |

---

## Field Order — Complete Report (all fields)

1. Header block
2. What It Is
3. What It Does
4. [Invocation Interface — Section 3 only]
5. [MCP Tool Manifest — Section 4 only]
6. Relevance to This Project
7. [Builder Footprint — Sections 1, 2, 3, 3a, 4, 8 only]
8. Master Library Assessment [includes Deployment Potential for Section 7]
9. Soren Security Pre-check
10. Recommendation
11. C&P Summary
12. Footer attribution
13. Report Version Log (all reports — applied at first substantial revision)

---

## Approval Status

These additions were approved by Sage (CEO) after Dr. Frankenstein Phase 1 — Cosmo's consolidated builder review of the full Master Library format (Session 145). Approval is **permanent** as of Dr. Frankenstein Phase 2 open (Session 167). Phase 2 soul audit did not surface additional format changes. This document is the confirmed baseline format standard for all research reports going forward. Future revisions may still occur through normal versioning — update and bump version accordingly when they do.

---

## Related Standard

For internally built artifacts (hooks, skills, MCPs built by the team rather than sourced externally), see the Internal-Build Record format standard:
Sophia's COO Folder → COO Suite (`internal-build-record.md`)

This document covers externally researched resources only. The Internal-Build Record covers internally authored content.

---

## Version Log

| Version | Date | What Changed |
|---------|------|-------------|
