# Vicky Tool Deployment — Your Version

**For your use only.** Plain guide to what happens when Vicky adds a new tool or starts her first live production task. For full operational detail, see `Vicky-Videographer-Tool-Deployment-SOP.md`.

**Version:** 0
**Paired with:** `Vicky-Videographer-Tool-Deployment-SOP.md` (v1.1) — Hard Rule 13

---

## 1. What This SOP Covers

Two things:

1. **Adding a new tool to Vicky's stack** — the pipeline that runs any time Vicky wants to use a tool that isn't already cleared
2. **First live task startup** — the confirmation steps Vicky runs before she starts work on a new project

The nine tools already in Vicky's stack (FFmpeg, HandBrake, Whisper family, Git LFS, DVC) were all cleared at Session 161. They're live. This SOP is for anything new, and for making sure her first task on a new project starts cleanly.

---

## 2. Adding a New Tool

Every deployable tool goes through the full security pipeline before Vicky uses it. No exceptions — even if it's something well-known, commonly used, or "obviously safe."

**How it works:**

1. **Vicky tells Sage** — what the tool is, what gap it fills, how she'd use it. That's all she needs to provide.
2. **Sage routes to Rose** — Rose researches the tool, produces a standard report.
3. **Soren reviews** — Rose's report goes to Soren. He runs the full clearance check: reads the content, scans for injection risks, runs the appropriate security tools.
4. **Lexi files** — if Soren clears it, Lexi catalogs the research report in the Master Library.
5. **Vicky activates** — Sage notifies Vicky. Vicky updates her toolset list.

**If Soren rejects it:** the tool doesn't get used. Sage tells Vicky. If the underlying need still exists, Sage may direct a search for an alternative.

**If a scan tool is unavailable:** the item is held, not cleared. It doesn't move forward until the check can actually run.

*Full pipeline: `Vicky-Videographer-Tool-Deployment-SOP.md` — Part 1*

---

## 3. First Live Task Startup

Before Vicky starts any real production work on a new project, she runs three quick confirmation steps:

**Step 1 — Tool stack confirmed:** Is the right tool installed and working? If a required tool isn't set up, she stops and tells Sage before touching any source material.

**Step 2 — Delivery format locked:** What exactly is she producing? File type, resolution, platform constraint (e.g., Discord 25MB limit), subtitle format, quality standard. Nothing starts until this is in writing.

**Step 3 — Scope confirmed:** What files is she working from? What are the specific cuts or operations? If Pete's automation is involved, what does the handoff look like? Who approves the quality pass — Sage or you?

These steps take a few minutes. They prevent a situation where Vicky delivers the wrong format, in the wrong quality, for the wrong platform.

*Full detail: `Vicky-Videographer-Tool-Deployment-SOP.md` — Part 2*

---

## 4. When Vicky Hands Off to Pete

When Vicky needs Pete to build or run an automation script, the handoff goes through Sage — not directly between them. Vicky writes a brief with five things:

1. Source file (name, location, format)
2. What the script should do (specific operation)
3. What the output should look like (format, file size target, resolution)
4. Any quality constraints
5. Where Pete should deliver the output

That's the handoff artifact. Sage routes it to Pete.

*Full detail: `Vicky-Videographer-Tool-Deployment-SOP.md` — Part 3*

---

## 5. Problems to Know About

A few scenarios you should be aware of:

**Tool fails mid-task** — Vicky stops. No debugging attempts. She flags to Sage with what happened. If it's Pete's script, Sage routes to Pete.

**A tool gets deprecated or a CVE is published** — Vicky stops using it immediately. Flags to Sage. Soren assesses before use resumes.

**Task starts bleeding into code or system config** — Vicky stops. That's Pete or Cosmo's lane. Flags to Sage before touching anything outside her lane.

**Quality pass — "technically right but feels wrong"** — Vicky flags it. She doesn't deliver silently when something looks off. Sage decides what happens next.

---

## 6. What You Need to Do

Mostly nothing — Sage and Vicky run this without you.

You'd be involved if:
- Soren rejects a tool Vicky needs and a judgment call is needed on an alternative
- A quality pass issue is escalated to you for a final call
- You want to review a delivery before it goes out

That's it.

---



*Reference for Jay. Full operational detail: `Vicky-Videographer-Tool-Deployment-SOP.md`.*
