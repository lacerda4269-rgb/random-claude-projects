# Resource Report: claude-remember

**URL:** https://claude.com/plugins/remember (Anthropic Marketplace) | https://github.com/Digital-Process-Tools/claude-remember (source)
**Date Researched:** 2026-06-03
**Researched by:** Rose (Research Specialist) | Security pre-check: Soren — CLEARED WITH CONDITIONS (2026-06-03) | Report by: Rose
**Already in Master Library?** No — new resource, not previously cataloged

---

## What It Is

claude-remember is a Claude Code plugin that gives Claude Code persistent memory across sessions. It is not an MCP server — it is a hook-based plugin that runs entirely through Claude Code lifecycle hooks (SessionStart, UserPromptSubmit, PostToolUse). When a session ends or a tool-use threshold is crossed, the plugin captures the session state, uses Claude Haiku to compress it into tiered daily summaries, and loads those summaries back into context when the next session opens. The result is that Claude Code begins every session already aware of what happened in prior sessions — what was built, what broke, what was decided — without any manual note-taking by the user. The developer is Digital Process Tools (GitHub: Digital-Process-Tools). Install count as of research date: 31,565. Current version: v0.7.2 (released 2026-05-13).

---

## What It Does

- Automatically captures session content via PostToolUse hook when a tool-use delta threshold is crossed — no manual trigger required for saves
- Compresses captured sessions using Claude Haiku into a four-tier memory structure: current session buffer (now.md), daily summaries (today-*.md), 7-day rolling window (recent.md), and long-term archive (archive.md)
- Loads relevant memory files into context automatically at SessionStart — prior session context is present before the first message
- Injects current timestamp into each user prompt via UserPromptSubmit hook for accurate session threading
- Provides a /remember slash command for manual handoff — writes a concise project-state note to remember.md before clearing context; the next session loads this note automatically
- Supports an optional identity.md file that preserves a persistent agent identity definition across sessions
- Supports two storage modes: default (project-root .remember/ folder) and external mode (~/.remember/{slug}/ outside the project tree, one folder per project slug)
- Runs locking and cooldown mechanisms to prevent concurrent write conflicts
- Provides a git backup option (optional, off by default); threat model documented in docs/git-backup-security.md
- All compression costs route through the existing Claude API key using Haiku — no separate billing account needed

---

## MCP Tool Manifest

**NOT APPLICABLE — claude-remember is a hook-based plugin, not an MCP server.**

claude-remember exposes no MCP tools and registers no mcpServers block in settings.json. Its integration with Claude Code is entirely through the hooks system. There is no stdio or HTTP transport layer. There is no tool manifest to document.

**What it registers instead (settings.json hooks block):**

```json
{
  "hooks": {
    "SessionStart": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "\"$CLAUDE_PROJECT_DIR\"/.claude/remember/scripts/session-start-hook.sh"
          }
        ]
      }
    ],
    "UserPromptSubmit": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "\"$CLAUDE_PROJECT_DIR\"/.claude/remember/scripts/user-prompt-hook.sh"
          }
        ]
      }
    ],
    "PostToolUse": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "\"$CLAUDE_PROJECT_DIR\"/.claude/remember/scripts/post-tool-hook.sh"
          }
        ]
      }
    ]
  }
}
```

These hooks are registered automatically at install. The team does not write them manually.

**Hook behavior summary:**

| Hook | Script | When it fires | What it does |
|------|--------|---------------|--------------|
| SessionStart | session-start-hook.sh | Every session open | Loads memory files into context; recovers any missed session saves |
| UserPromptSubmit | user-prompt-hook.sh | Every user message | Injects current timestamp for session threading |
| PostToolUse | post-tool-hook.sh | After each tool use, when delta crosses threshold | Captures session state; triggers Haiku compression pipeline |

**Prompt Injection Check:** The hooks inject memory file content directly into context at session start. This is intended behavior — but it means the content of .remember/ files arrives in context before Claude Code processes the first user message, with no filtering layer between disk and context injection. If a memory file were modified adversarially, that content would be injected into context silently. This is inherent to the architecture, not a specific discovered vulnerability. Flagged for Soren formal review.

---

## Relevance to This Project

*(Context as of 2026-06-03 — does not automatically carry to future projects)*

Jay has designated claude-remember as Layer 2 of the team's 4-layer memory stack for the Initial Package Project. Layer 1 is the existing MEMORY.md / CLAUDE.md system (manual, curated, long-lived). Layer 2 (this tool) is intended to provide automatic session-level continuity — capturing what happened in each session without requiring Sophia or Sage to write it manually. This addresses a real operational gap: session summaries are currently Sophia's job and require active effort; claude-remember would run automatically in parallel.

The key architectural fact for this project: claude-remember is completely independent of the existing MEMORY.md system. It writes to its own .remember/ folder and injects into context through SessionStart hooks. It does not touch CLAUDE.md, MEMORY.md, or any existing project files. The two systems can coexist without conflict — but the team needs to decide whether claude-remember's automatic context injection duplicates or overlaps with what CLAUDE.md already loads at session start. That is a Sage-level decision, not a research question.

One compatibility flag: this project runs on Windows with Claude Code. claude-remember's scripts are Bash-based. The team's current shell constraint (PowerShell blocked by Bitdefender; Bash tool used instead) does not directly affect plugin hooks, but the dependency on Git Bash/MSYS2 or WSL being in PATH when Claude Code fires hooks is a real installation requirement that must be confirmed before the plugin will function on this machine.

---

## Builder Footprint

- **Integration type:** Hook-triggerable (the plugin self-installs its hooks; Cosmo does not need to build the hook layer)
- **Extension points:** The memory files (.remember/*.md) are plain markdown — any skill or hook Cosmo builds can read from them directly. The /remember slash command is plugin-owned; Cosmo could build complementary skills that write to remember.md or read from recent.md
- **Build complexity signal:** Simple — the plugin self-installs; the only build work for Cosmo would be complementary skills or hooks that interact with the memory file outputs
- **Known conflicts:** The SessionStart hook injects memory files into context alongside what CLAUDE.md already loads. If both are active, every session opening will carry the CLAUDE.md/MEMORY.md content AND the .remember/ content. Cosmo should know this before designing any session-start orchestration skills — the combined context load will be larger than either system alone. Not checked against full ML catalog — catalog access unavailable at research time.

---

## Master Library Assessment

- **Proposed Section:** Section 4 — MCP Servers *(Note: despite being listed on the MCP plugin marketplace and presented as an MCP server, claude-remember is architecturally a hook-based plugin — it exposes no MCP tools and registers no mcpServers block. Recommend Sage and Lexi confirm the correct ML section at filing — Section 4 may be appropriate given the marketplace origin, or a dedicated plugin subsection may be warranted.)*
- **Proposed Tier:** Tier 2
- **Rationale:** The plugin is functional and actively maintained (v0.7.1 via DPT marketplace vs. the stale v0.5.0 on the official Anthropic Marketplace). It solves a real Layer 2 memory need. It does not receive Tier 1 because: (a) POSIX environment dependency must be verified on this Windows machine before hooks will fire correctly; (b) source-available license needs Soren formal evaluation; (c) automatic context injection at session start interacts with the existing MEMORY.md system in ways that need deliberate design before deployment.

---

## Soren Security Pre-check

**Formal Soren review completed: 2026-06-03**

- **Verdict:** CLEARED WITH CONDITIONS
- **Checked:** GitHub repo (Digital-Process-Tools/claude-remember), license terms, hook architecture, .remember/ write path, context injection model, Windows POSIX dependency, API billing model, git backup feature noted
- **Notes:**

| # | Rose Severity | Soren Severity | Flag | Disposition |
|---|---|---|---|---|
| 1 | HIGH | MEDIUM | Source-available license — no forking/modification/redistribution | ACCEPTABLE WITH NOTE — use permitted; degradation path exists (plain markdown files owned by team); 6-month license status check recommended |
| 2 | HIGH | MEDIUM | SessionStart context injection, no filtering layer | ACCEPTABLE WITH CONDITIONS — same trust model as CLAUDE.md and MEMORY.md; .remember/ write access must be scoped to plugin only |
| 3 | MEDIUM | LOW | Haiku API calls on existing key | ACCEPTABLE — operational checks only: confirm Haiku access enabled, rate limits not a concern |
| 4 | MEDIUM | MEDIUM | Windows POSIX dependency (Git Bash/MSYS2/WSL) | OPERATIONAL — not a security flag; must be confirmed in PATH before install; Cosmo to validate hook fires post-install |
| 5 | LOW | LOW | Official Marketplace serves v0.5.0 (buggy) | PROCEDURAL — install from DPT marketplace only |
| 6 | INFO | INFO | Git backup feature, off by default | OFF — PERMANENT (Soren confirmed, Session 256, Item 167). Git backup stays disabled in this environment; not to be enabled. Original HOLD resolved to a permanent OFF disposition — no separate enable review pending. |

**Deployment conditions (all three required before install):**
1. Only claude-remember writes to `.remember/` — no other agent, skill, or hook writes those files without explicit Sage authorization
2. POSIX environment confirmed in PATH; Cosmo validates SessionStart hook fires and writes to `.remember/` before declaring live
3. Git backup remains off — confirmed PERMANENT (Soren, Session 256, Item 167); not to be enabled in this environment

*Soren (Security Manager) | 2026-06-03*

---

## Recommendation

CLEARED WITH CONDITIONS (Soren, 2026-06-03). Recommend Tier 2 placement in Section 2a (Hooks) — this is a hook-based plugin, not an MCP server. Three deployment conditions must be met before install: (1) POSIX environment confirmed in PATH; (2) Cosmo validates hook fires post-install; (3) git backup remains off. Install from DPT marketplace only — not the official Anthropic Marketplace (v0.5.0 has known bugs fixed in v0.7.1). Deploy on one project first to validate the Windows hook chain before team-wide rollout.

---

## C&P Summary

claude-remember is a plugin for Claude Code that gives it automatic memory between work sessions. Without it, Claude Code starts every session completely fresh — it does not remember what happened in previous sessions unless you manually tell it. With claude-remember installed, the plugin quietly captures what happened during your session, uses a cheap AI model (Claude Haiku, less than a penny per session) to summarize and compress it, and then loads that summary automatically the next time you open Claude Code. You do not have to do anything — it runs in the background. There is also a /remember command you can type manually before closing a session to write a short handoff note that the next session will read.

A few things the team needs to know before installing: (1) It only works on this Windows machine if Git Bash or WSL is installed and reachable from Claude Code — that setup step has to happen first. (2) The license is not open source — the team is allowed to use it, but cannot modify or distribute it. (3) The automatic memory loading happens alongside the existing MEMORY.md and CLAUDE.md system, so both systems will be adding context at the start of every session — that is fine, but something Sage should review so sessions do not get bloated. (4) Install from the developer's own marketplace (DPT marketplace), not Anthropic's official marketplace — the official version has known bugs fixed in the current version. Soren needs to clear this before it goes in.

---
*Report by Rose (Research Specialist) | Session 208 | 2026-06-03*

---

## Report Version Log

| Version | Date | What Changed |
|---------|------|--------------|

---
*Keep-both pair (S264): this is the **full research report**. Install/deployment record → `0. Resources Installed/report-claude-remember.md`.*
