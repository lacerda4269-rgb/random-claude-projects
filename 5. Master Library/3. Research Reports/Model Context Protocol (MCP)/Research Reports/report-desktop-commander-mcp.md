# Resource Report: Desktop Commander MCP

**URL:** https://github.com/wonderwhy-er/DesktopCommanderMCP
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Report by: Sophia
**Already in Master Library?** No — gap item from old source list (5. Master Library List)

---

## What It Is
An enhanced filesystem MCP server with full terminal control, enabling Claude to read files, run processes, execute code, and manage the local environment end-to-end.

## What It Does
- Full terminal control: run scripts, manage processes, execute commands
- Diff-based file editing (token-efficient patch approach)
- Native support for Excel, PDF, and DOCX files
- Docker isolation option for sandboxed execution
- Symlink traversal prevention and audit logging (active security hardening)
- Acts as a proxy bridge for NinjaTrader and Quantower — no MCP exists for those platforms; Desktop Commander handles file-level interaction with both
- Auto-update support across 6 installation methods

## MCP Tool Manifest

- **Tool count:** 26 tools
- **Tools:**
  - `execute_command` — Execute a terminal command with full output; long-running commands supported
  - `read_output` — Read new output from a long-running terminal process
  - `force_terminate` — Force-terminate a running terminal process by PID
  - `list_processes` — List all currently running processes
  - `kill_process` — Kill a process by PID
  - `block_command` — Add a command to the blocked list
  - `unblock_command` — Remove a command from the blocked list
  - `read_file` — Read file contents with optional offset and length parameters
  - `read_multiple_files` — Read multiple files simultaneously
  - `write_file` — Write content to a file (token-efficient diff-based when possible)
  - `create_directory` — Create a new directory
  - `list_directory` — List directory contents
  - `move_file` — Move or rename a file or directory
  - `search_files` — Search for files matching a pattern across the filesystem
  - `search_code` — Full-text search inside file contents
  - `get_file_info` — Get metadata about a file (size, dates, permissions)
  - `edit_block` — Apply a diff-style block edit to a file (token-efficient patch)
  - `get_config` — Get the complete server configuration as JSON
  - `set_config_value` — Set a specific configuration key-value pair
  - `get_system_info` — Get operating system and environment details
  - `open_application` — Open a desktop application by name
  - `close_application` — Close a running desktop application
  - `take_screenshot` — Capture a screenshot of the current desktop
  - `get_screen_text` — Extract visible text from the current screen
  - `click_at` — Click at specific screen coordinates
  - `type_text` — Type text at the current cursor position
- **Transport type:** stdio
- **settings.json registration:**
```json
{
  "mcpServers": {
    "desktop-commander": {
      "command": "npx",
      "args": ["-y", "@wonderwhy-er/desktop-commander@latest"]
    }
  }
}
```
- **Recommended serverInstructions:** "Desktop Commander MCP provides full terminal control and enhanced filesystem access — execute commands, manage processes, read/write files with diff-based editing, and search code. Use for any local file, terminal, or process management task."

## Builder Footprint

- **Integration type:** MCP Server (stdio, npx) — registered in `claude_desktop_config.json` or VS Code `settings.json`; 26 tools covering terminal, filesystem, process management, and screen interaction; Docker isolation option available for sandboxed execution
- **Extension points:** Block/unblock command list configurable via `block_command` / `unblock_command` tools or config; Docker isolation toggleable per deployment; `set_config_value` tool enables runtime config changes; acts as proxy bridge for NT/Quantower file-level interaction until those platforms release official MCPs
- **Build complexity signal:** Low — npx auto-install on first run; no separate build step; 6 installation methods documented; auto-update support; Docker isolation adds complexity only if explicitly enabled
- **Known conflicts:** `execute_command`, `type_text`, `click_at`, and `take_screenshot` tools interact with the live desktop — use Docker isolation in any environment where Claude should not have unrestricted system access. Per Soren: use Docker isolation option in production environments for strongest security posture. Full terminal access scope is intentional and must be understood before deployment.

## Relevance to This Project
Critical for the trading workflow. Until NinjaTrader or Quantower release official MCP servers, this is the bridge. Also foundational for any local file/terminal-heavy coding or automation workflow — it closes the loop: edit → execute → read results → iterate.

## Master Library Assessment
- **Proposed Section:** 4 — MCP Servers
- **Proposed Tier:** 1
- **Rationale:** Foundation-level tool. Enables the full NT + Python backtesting loop and acts as a universal file bridge for any platform without its own MCP.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** 6,128 stars (was 5.8k at original review), active maintenance cadence, dedicated security policy, symlink traversal protections documented in README, audit logging feature, Docker isolation option for risk reduction. License confirmed. No prompt injection or malicious patterns detected.
- **Notes:** Active development team (hiring noted in README). Multiple installation paths including auto-update. Use Docker isolation option in production environments for strongest security posture. Latest release v0.2.42 (up from v0.2.40 at v1.0 log); last push 2026-06-05.
- **Re-reviewed 2026-06-08 — verdict confirmed.** Stars now 6,128 (was 6k); last push 2026-06-05; latest release v0.2.42. Continued active maintenance cadence. No new CVEs or security disclosures. CLEARED status stands — Docker isolation condition for production environments remains the operative guidance.

## Recommendation
Add to Section 4, Tier 1. Phase 1 install — highest priority MCP in the stack.

---
*Report by Sophia | Session 31 | 2026-03-29*

---

## C&P Summary

Desktop Commander MCP is an enhanced filesystem MCP server with full terminal control — it lets Claude read files, run processes, execute code, and manage the local environment end-to-end. It uses a diff-based patch approach for token-efficient file editing and natively handles Excel, PDF, and DOCX files. For this project, it is the critical bridge to NinjaTrader and Quantower: until those platforms release official MCP servers, Desktop Commander handles file-level interaction with both. It is the highest-priority MCP in the stack — Phase 1 install alongside GitHub MCP. Cleared by Soren with no concerns; Docker isolation option is recommended for production environments.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
