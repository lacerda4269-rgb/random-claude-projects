# Vicky — Videographer Tool Deployment SOP

**Version:** 0
**Owner:** Vicky (Videographer) | Sophia (COO) | Sage (CEO)
**Created:** 2026-06-02
**Updated:** 2026-06-23 (Session 270)
**Status:** Active
**Paired with:** `Vicky-Videographer-Tool-Deployment-SOP-Jay.md` (v1.1) — Hard Rule 13
**Document type:** SOP (executable procedure)

---

## Purpose

This SOP defines how Vicky's deployable tool stack is managed: the pipeline for adding any new tool going forward, the steps for activating Vicky for her first live project task, the standard handoff format to Pete, and edge case handling. 

This SOP does NOT govern the nine tools already cleared (see current status below). Those are live and usable. This SOP governs what happens when a new tool is proposed, and how Vicky activates cleanly on a live task.

---

## Current Tool Stack Status

All nine deployable tools in Vicky's stack were cleared in a batch security review at Session 161 CP5. Status: CLEARED ✓ for all.

| Tool | Status |
|------|--------|
| FFmpeg | CLEARED ✓ Session 161 |
| HandBrake v1.10.2 | CLEARED ✓ Session 161 |
| ffmpeg-python | CLEARED ✓ Session 161 |
| MoviePy v2.2.1 | CLEARED ✓ Session 161 |
| OpenAI Whisper | CLEARED ✓ Session 161 |
| faster-whisper | CLEARED ✓ Session 161 |
| auto-subtitle | CLEARED ✓ Session 161 |
| Git LFS | CLEARED ✓ Session 161 |
| DVC | CLEARED ✓ Session 161 |

Web-UI tools (Google Vids / Veo 3.1, Runway ML, Kling AI, Google Drive, YouTube unlisted) require no clearance — no download or installation involved. Pre-approved web-only class (Soren governance).

---

## Trigger

This SOP activates in two scenarios:

1. **New tool addition** — any tool not on the cleared list above is proposed for Vicky's use
2. **First live task activation** — Vicky is activating for her first real production task on a new project

The batch-clearance pipeline already complete (Session 161) does not re-activate this SOP. The nine cleared tools are live.

---

## Part 1 — New Tool Pipeline

When Vicky (or any team member) identifies a tool that should be added to Vicky's deployable stack:

### Step 1 — Vicky proposes to Sage

Vicky submits a proposal to Sage. Proposal includes:
- Tool name and what it does
- Why it is needed (what gap it fills in the current toolset)
- Proposed use case within Vicky's lane

Vicky does not source, research, or contact the tool vendor directly. The proposal is an intent and a use-case statement, not a technical evaluation.

### Step 2 — Sage routes to Rose

Sage reviews the proposal for domain relevance (is this genuinely in Vicky's production lane?) and routes to Rose for a standard research report if approved.

**Rose's deliverable:** Standard resource report including C&P Summary, version/license/CVE evaluation, source links, and Prompt Injection Check field. Classified as Resource Report (tool is deployable).

### Step 3 — Soren clearance

Rose's report arrives at Sage. Sage routes to Soren for the full clearance pipeline:
- Step 1: Receive item and Rose report
- Step 2: Prompt Injection Protocol check
- Step 3: Category 1 scan (SecureClaw)
- Step 4: Category-appropriate scan (file type determines which tools run)
- Step 5–6: Assessment and determination (CLEARED / REJECTED / ESCALATE / HOLD)
- Step 7: Report to Sage

**Soren provides to Sage:**
- Tool name
- Checks run and results
- Any findings
- Determination (CLEARED / REJECTED / ESCALATE / HOLD)
- What would clear it (if REJECTED or ESCALATE)

### Step 4 — Lexi catalogs

CLEARED determination only. Sage routes to Lexi. Lexi files the Rose research report in the appropriate Master Library section and updates the index. Vicky's soul toolset table is not updated by Lexi — that is a soul update (see Step 5).

### Step 5 — Vicky activates

After CLEARED and Lexi cataloging:
- Sage notifies Vicky: "Tool [name] is cleared. You may add it to your stack."
- Vicky updates her soul toolset table (with Sage's review per soul governance)
- Tool is now usable in Vicky's lane

**REJECTED:** Tool does not enter Vicky's stack. Vicky is notified by Sage. If the concept has merit (the need the tool was meant to fill remains), Sage may direct a follow-on search for an alternative.

**ESCALATE:** Tool is on hold — a required scan could not run. Sage and Soren work to resolve tooling or defer. Vicky waits.

**HOLD — Dependency Pending:** Parent tool is held while a required dependency clears. Vicky is notified. No use of either the parent or the dependency until both CLEAR.

---

## Part 2 — First Live Task Activation Sequence

When Vicky is activated for her first real production task on a live project, run this sequence before work begins:

### Step 1 — Confirm tool stack active

Vicky confirms the tools required for this specific task are:
- On the cleared list (see Current Tool Stack Status above)
- Installed and functional in the current project environment
- Any required Pete-built scripts are built and tested

If a required tool is missing clearance or not installed: stop. Flag to Sage before proceeding. No workarounds.

### Step 2 — Confirm delivery format with Sage

Vicky confirms with Sage:
- What the final deliverable is (file type, resolution, format, length, platform)
- Discord upload limit or other platform constraint in effect (confirm current limit — do not assume)
- Whether burned-in subtitles or soft subtitles are required
- Whether a quality pass standard has been defined for this project (or confirm default: "technically compliant + worth watching")

Sage confirms or adjusts. Nothing starts until delivery format is locked.

### Step 3 — Confirm scope

Vicky confirms with Sage:
- Exactly what source material she is working from (file name, location, format)
- Any cuts, trims, or processing decisions already specified
- What the handoff to Pete looks like, if automation is involved
- Whether Jay will review before final delivery, or if Sage approves the quality pass

Scope confirmed in writing (session notes or a brief message in the session summary). Nothing starts on assumptions.

---

## Part 3 — Handoff Format (Vicky → Pete)

When Vicky hands off to Pete for automation script execution or script requests:

**Handoff artifact:** A brief written handoff, not a verbal summary. Minimum fields:

| Field | Content |
|-------|---------|
| Source file | Full file name, location, format |
| Task | What Pete's script should do (specific operation: trim to X:XX–Y:YY, compress to ≤8MB, burn SRT from [file], etc.) |
| Output spec | Expected file name, format, resolution, platform constraint |
| Quality flag | Any known quality constraints (e.g., preserve audio quality, do not re-encode if possible) |
| Return path | Where Pete should deliver the output file |

**Channel:** All Pete coordination routes through Sage, not directly. Vicky delivers the handoff brief to Sage; Sage routes to Pete. Vicky does not contact Pete directly.

**If Pete's script fails mid-task:** Stop. Do not attempt script debugging — that is Pete's lane. Report to Sage with: script name, what it was doing, the error or unexpected output observed. Sage routes to Pete.

---

## Part 4 — Edge Cases

| Situation | Action |
|-----------|--------|
| A tool fails mid-task (crash, unexpected output, error) | Stop. Flag to Sage immediately. Include: what tool, what step, what the output was. Do not attempt to patch around the failure — stay in your lane. |
| A tool in the cleared stack is deprecated or a critical CVE is published | Flag to Sage immediately. Stop using the tool until Sage and Soren assess. Sage may direct a Rule 3 freshness check (Rose) and new clearance before use resumes. |
| Scope creep — task starts touching code editing, script writing, or system configuration | Stop immediately. That is Pete's (code), Cosmo's (automation/config), or Soren's (security) lane. Flag to Sage. Proceed only with explicit Sage direction. |
| A source file arrives in an unsupported format | Flag to Sage before attempting any conversion. Conversion is within Vicky's lane (FFmpeg), but confirm the output format before proceeding — do not assume a target format. |
| Quality pass fails (output is technically within spec but "wrong") | Flag to Sage with a specific description of what feels wrong and why. Do not deliver silently. Sage decides: re-do, accept, or escalate to Jay. |
| A Pete-built script produces output that meets spec but looks wrong | Run the quality pass. Flag the quality issue to Sage — same as above. The script delivering the right file does not close the quality gate. |
| A web-UI AI generation tool requires a new account or signup | Flag to Sage before creating any account. This is a new credential and a potential scope change — Sage decides. |

---

## File Organization

| File | Location | Notes |
|------|----------|-------|
| Soul | `1. Soul Folder/Vicky the Videographer/vicky-videographer.md` | Identity, principles, behavioral standards |
| SOP — Agent version (this file) | `1. Soul Folder/Vicky the Videographer/Vicky-Videographer-Tool-Deployment-SOP.md` | Full operational reference for tool deployment and first live task |
| SOP — Jay's version | `1. Soul Folder/Vicky the Videographer/Vicky-Videographer-Tool-Deployment-SOP-Jay.md` | Plain-language reference for Jay |
| Core SOP | `1. Soul Folder/Vicky the Videographer/Vicky-Videographer-SOP.md` | Primary production operations SOP |
| Batch clearance record | Soren's folder — `Soren-Security-Review-Session161.md` | Documents all 9 batch clearances from Session 161 CP5 |

---

## Version Log

| Version | Date | What Changed | Why |
|---------|------|-------------|-----|
