# Resource Report: VS Code Multi-Agent Chat Panel (Claude Code Extension)

**URL:** https://code.visualstudio.com/blogs/2026/02/05/multi-agent-development
**Official Claude Code VS Code Docs:** https://code.claude.com/docs/en/vs-code
**Date Researched:** 2026-04-14
**Researched by:** Rose | Security pre-check: Soren — QUEUED FOR INITIAL REVIEW | Report by: Rose (compiled by Sage)
**Already in Master Library?** No — pending Soren initial review before formal filing

> **Status Note:** Report confirmed complete and current 2026-04-16 (LHF Part 2 review). Official Microsoft/Anthropic tooling — not an external install. Queued for Soren initial review before formal ML filing. Expected outcome: standard clearance given official provenance.

---

## What It Is

A feature built into VS Code (since v1.109, January 2026) that provides a unified sidebar panel showing all active AI agent sessions — Claude Code, GitHub Copilot, Codex, and third-party agents — in one place. The Claude Code tab within this panel is the graphical interface for the Claude Code CLI, native to VS Code.

## What It Does

**The unified panel:**
- Shows all active AI agent sessions side by side (Claude Code, Copilot, Codex, others)
- Allows switching between agents without leaving VS Code
- Runs background and cloud agents alongside local agents

**The Claude Code tab specifically:**
- Full chat interface with Claude inside VS Code
- Diff review: Claude shows exactly what it wants to change before applying it
- @-mention of specific files and line ranges
- Multiple conversation tabs in parallel
- Checkpoints: rewind Claude's edits to any earlier point in the session
- Plan mode: Claude describes what it will do, waits for approval before acting
- Searchable conversation history

**Capability gaps vs. the Claude Code CLI:**

| Feature | CLI | VS Code Extension |
|---|---|---|
| All slash commands / skills | All available | Subset only (type `/` to see available list) |
| MCP server configuration | Full | Partial (add via CLI; manage existing via `/mcp`) |
| `!` bash shortcut | Yes | No |
| Tab completion | Yes | No |
| Checkpoints (rewind) | Yes | Yes |

The VS Code extension includes the Claude Code CLI under the hood — open VS Code's integrated terminal and run `claude` to access CLI-only features within the same environment.

## Relevance to This Project

High relevance for ongoing session design. This is how Claude Code sessions are run inside VS Code. Understanding capability gaps vs. the CLI determines when to use the VS Code panel vs. dropping into the terminal.

**Architecture note for multi-window design:**
- Known issue: `editor.open` command always targets the leftmost/primary VS Code window, not the focused one
- Multiple Claude Code tabs can cause process conflicts (multiple `claude.exe` processes competing for the same session file, no file locking)
- Anthropic has reverted some multi-terminal support due to responsiveness issues
- Workaround: one Claude Code extension panel per VS Code window; use CLI in integrated terminal for CLI-only features

**Architecture recommendation (Rose's finding):** The VS Code Claude Code tab is the right default interface for most single-session work. The CLI (with git worktrees via `claude --worktree`) remains the more stable path for parallel deep work across multiple simultaneous sessions. The unified multi-agent panel adds visibility across all agents but does not change the underlying multi-window architecture design.

## Master Library Assessment

- **Proposed Section:** 7 — Reference & Ecosystem
- **Proposed Tier:** 1
- **Rationale:** This is core tooling knowledge — how the primary development environment (VS Code + Claude Code extension) actually works. Tier 1 because it directly affects every session and every agent interaction design decision. Not something to install — something to understand and reference.

## Soren Security Pre-check

- **Verdict:** PENDING — not yet reviewed
- **Notes:** This is an official Microsoft VS Code feature and an official Anthropic Claude Code integration. Standard security concerns (malicious code, data exfiltration, license issues) are minimal given the provenance. Soren review is a formality here but still required before formal ML filing.

## Recommendation

File as Section 7 (Reference & Ecosystem), Tier 1, once Soren clears. Core architecture reference — every agent and every multi-window design decision should account for the capability gap table above.

---

## C&P Summary

VS Code now has a unified sidebar that shows all your active AI agent sessions — Claude Code, GitHub Copilot, Codex, and others — in one panel so you can see what's running and switch between them without leaving VS Code. The Claude Code tab in that panel is essentially the full Claude Code experience in graphical form: you get a chat interface, the ability to @-mention specific files, diff review before Claude applies any changes, the ability to rewind edits to an earlier checkpoint if something goes wrong, and Plan mode where Claude tells you exactly what it's going to do before doing it. The main thing the extension doesn't have that the CLI does: not all slash commands and skills work, MCP configuration is partial, and you can't use the `!` bash shortcut or tab completion. For anything that needs CLI-only features, you open VS Code's integrated terminal and type `claude` — the same session, just the terminal interface. For running two Claude Code sessions at the same time on different tasks, the CLI with git worktrees is still the more stable approach; the VS Code multi-agent panel is best as your main interface for a single focused session.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---

*Research by Rose | Compiled by Sage | Session 42 — 2026-04-14 | Confirmed current Session 49 — 2026-04-16*
*Updated by Rose | Session 230 | 2026-06-08*
