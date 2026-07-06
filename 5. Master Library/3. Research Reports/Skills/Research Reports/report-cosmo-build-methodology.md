# Report: Build Methodology — Claude Code Resource Types
**Topic:** Best practices methodology for building Skills, Hooks, CLIs, MCPs, Plugins, and Python engines in the Claude Code ecosystem
**Date Researched:** 2026-05-04
**Researched by:** Rose
**Security pre-check:** N/A — fact-finding report, no deployable resource
**Report by:** Rose

---

## Overview

This report covers the six resource types Cosmo builds and maintains. Each section defines the resource in the team's context, explains the correct build structure, identifies best practices, and flags common failure modes. This is an orientation document — surface level, high accuracy, built for a technically sophisticated reader who will identify gaps for deeper research.

---

## Section 1: Skills

### What It Is

A Skill is a markdown file (SKILL.md) with YAML frontmatter that teaches Claude how to perform a specific, repeatable task. When invoked — either by the user via a /slash-command or by Claude automatically based on context — the skill's instructions become Claude's operating procedure for that task. Skills live in the .claude/skills/ directory (user-level) or can be bundled inside a Plugin.

### Correct Build Structure

A skill is a folder, not just a file. The folder name becomes the default slash command name. Inside the folder:

```
my-skill/
  SKILL.md          <- required; frontmatter + instructions
  reference.md      <- optional; supporting knowledge/context
  scripts/          <- optional; supporting scripts
```

The SKILL.md file has two parts.

**Frontmatter (between --- markers):**
```yaml
---
name: skill-name
description: What this skill does and when to use it.
disable-model-invocation: false
user-invocable: true
allowed-tools:
  - Read
  - Edit
---
```

Key frontmatter fields:
- **name** — the slash command trigger. Defaults to folder name if omitted; set it explicitly.
- **description** — the primary trigger mechanism for model-invoked skills. Must describe both what the skill does and when to use it.
- **disable-model-invocation: true** — user must explicitly call the skill via slash command. Use for anything with side effects (deploy, commit, send message). Claude will not auto-invoke.
- **user-invocable: false** — Claude can use it; the user cannot call it directly. Use for background knowledge or internal sub-skills.
- **allowed-tools** — restricts which tools the skill can use. Enforced, not advisory.
- Additional fields: argument-hint, model, effort, context, agent, hooks.

**Markdown body:** Step-by-step instructions in plain markdown. Use XML tags for structure when the body is long.

### Best Practices

- **One skill, one job.** Narrow scope wins. A skill that does three things is three poorly-done things.
- **Description is the trigger.** For model-invoked skills, the description is what Claude pattern-matches against. Write it to match the natural language someone would use when they need this skill.
- **Separate process from knowledge.** Instructions in SKILL.md. Reference material (style guides, schemas, domain rules) in a separate file. This keeps the skill lean and lets knowledge files update independently.
- **Be explicit about output format.** Never assume Claude knows what format you want. State it: "Write the output to X path as a markdown file," not "produce a report."
- **Keep SKILL.md under 500 lines.** If it is growing past that, something belongs in a reference file or should be split into sub-skills.
- **Control invocation deliberately.** Default behavior is model-invoked. Set disable-model-invocation: true for anything the user should consciously choose to run. Set user-invocable: false for anything that should never appear in the slash command menu.

### Common Mistakes

- **Vague description field.** The model cannot pattern-match on "helps with tasks." Be specific.
- **Monolithic SKILL.md.** Putting all context, instructions, and reference material in one file inflates load time and hurts maintainability.
- **Conflating disable-model-invocation and user-invocable.** These are separate axes. disable-model-invocation: true means only the user can trigger it. user-invocable: false means only the model can trigger it. They can coexist but usually should not — if both are set, the skill becomes unreachable.
- **Skipping allowed-tools.** For skills that should not read files or run shell commands, failing to restrict tools leaves the skill with more permission than it needs.
- **Naming the folder ambiguously.** The folder name is the slash command. my-thing works. MT or helper do not.

---

## Section 2: Hooks

### What It Is

Hooks are shell commands (or HTTP calls) registered in settings.json that Claude Code executes automatically at specific lifecycle events. They are deterministic guardrails — not prompts or suggestions. The system executes them, not Claude, which is what makes them reliable for enforcement, logging, formatting, and blocking.

### Correct Build Structure

Hooks are configured in settings.json:

- **Project-level:** .claude/settings.json — committed to the repo, shared with the team.
- **User-level:** ~/.claude/settings.json — personal, applies to every project.

Basic configuration structure:
```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "path/to/hook-script.sh",
            "timeout": 30
          }
        ]
      }
    ]
  }
}
```

**Hook event types:**
- **PreToolUse** — fires before a tool executes. Can block. The most powerful event; use it for validation and security gates.
- **PostToolUse** — fires after a tool executes successfully. Cannot undo. Use for auto-formatting, logging, post-validation.
- **PostToolUseFailure** — fires when a tool fails.
- **Stop** — fires when Claude finishes responding. Does not fire on user interrupts.
- **Notification** — fires when Claude needs user attention.
- **PermissionRequest / PermissionDenied** — fire on permission events.

**The matcher field** filters which tool triggers the hook. Supports tool names (e.g., Bash, Write) and glob patterns.

**Hook input:** The hook script receives a JSON payload via stdin. Common fields: session_id, transcript_path, cwd, permission_mode, hook_event_name, tool_name, tool_input.

**Hook output and exit codes:**
- Exit 0 — success. stdout is processed (JSON or context addition).
- Exit 1 — non-blocking error. Action proceeds. Use for soft warnings.
- Exit 2 — blocking error. Action is prevented. stderr becomes the error message shown. Every security gate must use exit 2.

**Structured JSON output** (exit 0 with JSON to stdout) gives finer-grained control:
```json
{
  "decision": "block",
  "reason": "Reason shown to Claude and user"
}
```
Fields: decision (approve/block/allow/deny), reason, continue (Stop hooks only), updatedInput (modify tool params before execution).

**Additional handler types:**
- **async: true** — runs the hook in the background without blocking Claude's execution.
- **HTTP hooks** — send the event to a web server instead of running a local script. Enables remote validation services and team-wide policy enforcement.

### Best Practices

- **Use PreToolUse for enforcement, PostToolUse for cleanup.** Do not try to block in PostToolUse — it is too late.
- **Exit 2 for everything security-critical.** Exit 1 is not a gate; it is a log entry. If it must not proceed, use exit 2.
- **Keep hook scripts fast.** Hooks run synchronously by default. A slow hook blocks Claude's entire execution. Use async: true for anything that might take time.
- **Scope matchers tightly.** A hook on "*" runs on every tool call. This adds latency and noise. Match only the tools the hook needs to touch.
- **Project-level for team enforcement; user-level for personal workflows.** Do not put personal formatting preferences in the project settings file.
- **Test exit code behavior explicitly.** The difference between exit 1 and exit 2 is consequential. Verify that your security gates actually block.
- **disableAllHooks: true in settings** is available as a kill switch. Know it exists.

### Common Mistakes

- **Using exit 1 when you meant exit 2.** The action proceeds. The hook did nothing except log.
- **Writing slow synchronous hooks.** Any hook that calls an external API or does disk-heavy work should be async.
- **Overly broad matchers.** Matching all tools when you only care about Write or Bash adds friction to every operation.
- **Putting team enforcement in user-level settings.** User-level settings are per-person and not committed. Team rules belong in the project settings file.
- **Assuming Stop fires on interrupt.** It does not. Do not rely on Stop for cleanup logic that needs to run when the user kills a session.

---

## Section 3: CLIs

### What It Is

In the team's context, CLIs means two things: using existing command-line tools (gh, uv, git, etc.) as first-class integration points, and building custom command-line tools when no existing CLI covers the workflow. CLIs are the preferred integration layer before reaching for an MCP — lower complexity, zero OAuth overhead, no schema loading cost.

### Using Existing CLIs

The decision rule: if a well-maintained CLI exists for a service or system, use it. Do not build an MCP to wrap something that gh, git, aws, or similar already handle competently. CLIs are faster to integrate, easier to debug, and impose no context window cost.

### Building Custom CLIs — Correct Structure

When a custom CLI is warranted, the standard Python approach uses **Typer** (modern, type-hint-driven) or **Click** (more control, complex nested commands). Argparse is standard library but verbose.

Recommended project structure:
```
my-tool/
  cli.py            <- entry point, argument parsing
  core.py           <- business logic (separated from CLI layer)
  exceptions.py     <- custom exception types
  logging_config.py <- structured logging setup
  tests/
  pyproject.toml    <- packaging, entry_points for installable command
```

A Typer CLI entry point:
```python
import typer
app = typer.Typer()

@app.command()
def run(input_file: str, verbose: bool = False):
    """Process the input file."""
    ...

if __name__ == "__main__":
    app()
```

Package via pyproject.toml with [project.scripts] to make it installable as a named command.

### When to Build a Custom CLI

Build a custom CLI when:
- No existing tool covers the workflow.
- The operation will be called repeatedly from hooks, skills, or scripts.
- The team needs a stable, named interface that abstracts implementation details.
- The workflow involves multiple steps that should be a single atomic command.

Do not build a custom CLI when:
- An existing CLI covers 80%+ of the use case. Wrap or compose instead.
- The operation is a one-off. A standalone script is sufficient; a CLI is premature.
- The primary use is inside Python code only. Use a module, not a CLI.

### Best Practices

- **Separate CLI layer from business logic.** cli.py handles arguments and output; core.py does the work. This makes both testable independently.
- **Never expose raw Python tracebacks to users.** Catch and translate exceptions at the CLI boundary. Custom exception types make this clean.
- **Structured logging from the start.** Add it before you need it.
- **Version the tool.** --version flag, semantic versioning, changelog. CLIs become dependencies; treat them like ones.
- **Provide --dry-run for anything destructive.** Users and agents will thank you.
- **Help text is documentation.** Write it as if the user has never seen the code.

### Common Mistakes

- **Building a CLI for a one-time task.** Premature formalization is waste.
- **Logic in the CLI layer.** cli.py becomes untestable and fragile.
- **Silent failures.** A CLI that exits 0 when something went wrong is a debugging nightmare. Exit codes must be meaningful.
- **No input validation.** Validate before acting; fail fast with a clear message.
- **Skipping packaging.** An unpackaged CLI that lives in a scripts folder is not a stable interface. If it is worth building, it is worth packaging.

---

## Section 4: MCPs

### What It Is

An MCP (Model Context Protocol) server is a process that exposes tools, resources, and/or prompts to Claude via a standardized JSON-RPC 2.0 protocol. In the team's context, MCPs are the last resort in the build order — reached for only when no CLI exists for the service, or when the use case genuinely requires OAuth authentication or stateful session management that a CLI cannot provide. As of 2026, MCP schemas load on demand via ToolSearch rather than in full at session start, so adding MCP servers has a much lower context cost than it used to.

### Correct Build Structure

MCP servers expose three primitive types:
- **Tools** — functions Claude can call (with user approval). The most commonly used primitive.
- **Resources** — file-like data Claude can read.
- **Prompts** — pre-written templates Claude can use.

Transport options:
- **stdio** — local process, communicates over stdin/stdout. Default for local servers. Zero network overhead. Claude Code launches the server as a subprocess.
- **Streamable HTTP** — remote server, communicates over HTTP. Use when the server must be shared or run remotely.

Minimal Python MCP server structure (using the mcp SDK with uv):
```python
from mcp.server.fastmcp import FastMCP

mcp = FastMCP("my-server")

@mcp.tool()
def do_thing(param: str) -> str:
    """Description of what this tool does."""
    return result

if __name__ == "__main__":
    mcp.run()
```

Claude Code integration — registered in .claude/settings.json or ~/.claude/settings.json:
```json
{
  "mcpServers": {
    "my-server": {
      "command": "uv",
      "args": ["run", "my_server.py"],
      "serverInstructions": "Brief description of what this server provides and when to use it."
    }
  }
}
```

The serverInstructions field matters when Tool Search is active — it helps Claude decide when to fetch tool schemas from this server.

### When to Build vs. Use Existing

**Use an existing MCP server when:**
- A maintained server already exists for the service (GitHub, Postgres, Slack, etc.).
- The existing server covers your specific workflow needs.
- Default: always check the official MCP registry and anthropics/claude-plugins-official first.

**Build a custom MCP when:**
- No existing server covers your platform or internal system.
- The use case requires OAuth auth or stateful sessions a CLI cannot handle.
- You are exposing internal documentation or proprietary data to the agent layer.
- Scope is clear: 3-6 tools covering the core workflow, not the full API surface.

### Best Practices

- **Start with 3-6 tools.** Scope creep in MCP servers produces bloated context and maintenance burden.
- **Write clear tool descriptions.** The tool description is what Claude uses to decide whether to call it. Vague descriptions mean missed calls or wrong calls.
- **Write clear serverInstructions.** With Tool Search active, this is Claude's first signal about when to fetch your tools. Put the most critical information first.
- **Keep credentials and complex logic inside the server.** The MCP boundary is a security boundary. Secrets do not cross it.
- **Use stdio for local servers.** Streamable HTTP adds complexity. Only reach for it if the server must be remote.
- **Log initialization, connection events, errors, and external API calls.** MCP servers are silent processes; logging is your only debugging surface.
- **Validate inputs.** Tools receive arbitrary model-generated parameters. Validate before acting.

### Common Mistakes

- **Building an MCP when a CLI would do.** The team build order exists for a reason.
- **Tool sprawl.** Exposing the entire API surface as tools. Build the core workflow, not a complete SDK.
- **Vague tool or server descriptions.** Claude cannot use what it cannot understand.
- **Ignoring transport selection.** Defaulting to HTTP when the server is local adds unnecessary complexity and latency.
- **No error handling.** An MCP server that crashes silently leaves the agent in an unknown state.

---

## Section 5: Plugins

### What It Is

A Plugin is a distributable package that bundles multiple Claude Code extensions into a single installable unit. Where a Skill is a single instruction file and an MCP is a single server, a Plugin can contain skills, MCP server configurations, hooks, agents, and commands — all packaged together and namespaced to avoid conflicts with other plugins.

Plugins are the packaging and distribution layer. They do not introduce new capabilities on their own — they organize and ship combinations of the capabilities already described in this report.

### Correct Build Structure

A Plugin requires a root-level .claude-plugin/plugin.json metadata file. The rest is optional based on what the plugin includes.

```
my-plugin/
  .claude-plugin/
    plugin.json       <- required; metadata and configuration
  skills/
    my-skill/
      SKILL.md
  hooks/
    pre-tool.sh
  commands/
  agents/
  .mcp.json           <- MCP server configurations
  README.md
```

plugin.json structure:
```json
{
  "name": "my-plugin",
  "version": "1.0.0",
  "description": "What this plugin does.",
  "author": "Author Name"
}
```

Plugin skills are namespaced: /my-plugin:skill-name. This prevents collisions when multiple plugins are installed.

**Installation methods:**
- Official directory: claude plugin add @anthropic/plugin-name
- GitHub: claude plugin add github:username/repo-name
- Local (development): use the --plugin-dir flag
- Reload during development: /reload-plugins

### When to Build a Plugin vs. a Standalone Skill or MCP

Build a Plugin when:
- You are distributing a coherent set of capabilities that belong together (e.g., a deploy workflow that needs a skill, a hook, and an MCP connection).
- The package needs to be installed by other users or teams.
- Namespacing matters — the plugin's commands need to coexist with other plugins without collision.

Do not build a Plugin when:
- You only need a single skill or a single MCP. Packaging overhead is not justified.
- The resource is for internal use only and will not be distributed. A skill folder or a settings.json MCP entry is sufficient.

### Best Practices

- **Plugins are bundles, not features.** Everything inside a plugin should belong together conceptually. A plugin that does five unrelated things is five things that should be separate plugins or standalone skills.
- **Namespace your skill names.** Plugin skills are automatically namespaced, but make names descriptive within that namespace. /my-plugin:review beats /my-plugin:r.
- **Keep plugin.json accurate.** Version, description, and author are what users see before installing. Treat them as the first line of documentation.
- **Test with --plugin-dir before publishing.** Local testing with the flag avoids polluting the installed plugin list during development.
- **Include a README.** Users installing your plugin cannot read your code. Tell them what the plugin does, what each skill does, and any configuration required.

### Common Mistakes and Gaps

- **Over-bundling.** Combining unrelated capabilities into one plugin because it is convenient to ship one thing. This creates installation bloat and makes individual components hard to update.
- **Skipping namespacing awareness.** Skills inside plugins are namespaced, but if names are generic (review, deploy), they still collide conceptually with user habits.
- **Not testing reload behavior.** During development, /reload-plugins must be run to pick up changes. Forgetting this leads to debugging old behavior.

**Transparency note:** Plugin documentation from Anthropic is newer and thinner than Skills or Hooks documentation. The Plugin system is functional and documented, but developer community patterns and failure mode catalogs are less mature than for the other resource types. Cosmo should flag this as a candidate area for Feynman research if deeper methodology is needed.

---

## Section 6: Python Engines and Scripts

### What It Is

Python in the team's context is the glue layer — the mechanism that connects agents, manages file-based handoffs between processes, coordinates across LLMs via LiteLLM, and handles desktop automation for physical GUI tasks. Python scripts and engines are not standalone products; they are the connective tissue that makes the rest of the stack function as a coherent system.

Three distinct roles Python plays on this team:
1. **Glue and orchestration** — coordinating multi-step workflows, calling CLIs and MCPs programmatically, managing state between sessions.
2. **Cross-LLM coordination via LiteLLM** — routing calls to different models through a unified interface; swapping providers without rewriting integration code.
3. **Desktop automation** — physical GUI tasks (paste, click, confirm) handled by the Desktop-CoWork Agent via PyAutoGUI or similar.

### Correct Build Structure

For glue scripts and engines:
```
engine/
  main.py           <- orchestration entry point
  core.py           <- business logic
  handoff.py        <- file-based handoff read/write
  exceptions.py     <- custom exceptions
  config.py         <- configuration loading
  tests/
```

**File-based handoff pattern** (the standard inter-agent communication mechanism when direct API calls are not in play):
- Agent A writes a structured output file (JSON or markdown with a defined schema) to a shared location.
- Agent B reads that file as its input.
- The orchestrator (Python script) manages the hand-off: confirms A's output exists and validates it, then triggers B with the file path as argument.
- Never pass raw agent output to the next agent without validation at the boundary.

**LiteLLM integration pattern:**
```python
from litellm import completion

response = completion(
    model="anthropic/claude-sonnet-4-6",
    messages=[{"role": "user", "content": prompt}]
)
# Swap model string to change providers — no other code changes needed
```

LiteLLM provides a unified interface across 100+ models with built-in cost tracking and rate limiting. The right choice when the workflow needs to route to different LLMs or when provider portability matters.

**Structured handoffs between LLM agents** — use Pydantic models or JSON schema to validate what one agent produces before passing it to the next. Non-deterministic LLM output plus unvalidated handoffs equals debugging that is very hard to trace.

**Desktop automation (PyAutoGUI):**
```python
import pyautogui

# Fail-safe enabled by default: move mouse to corner to abort
pyautogui.click(x, y)
pyautogui.typewrite("text", interval=0.05)
pyautogui.hotkey("ctrl", "v")
```

PyAutoGUI is best for lightweight, visual automation on a consistent interface. Combine with subprocess to launch applications before automating them.

### Best Practices

- **Separate orchestration from logic.** The file that manages the workflow (what runs, in what order, what feeds what) should not contain business logic. Keep them in separate modules.
- **Validate at every handoff boundary.** Use Pydantic or JSON schema validation when consuming any LLM output. This is the single highest-leverage place to prevent cascading failures.
- **Use LiteLLM for any multi-provider or provider-agnostic workflow.** Do not write provider-specific API clients when LiteLLM already handles the abstraction.
- **File-based handoffs should use defined schemas.** JSON with a schema beats unstructured markdown for machine-to-machine handoffs. Both parties must agree on the schema before either is built.
- **Desktop automation scripts must be idempotent where possible.** GUI states are fragile. If a script fails halfway, it should be able to restart cleanly rather than leaving the UI in an unknown state.
- **PyAutoGUI fail-safe is on by default — keep it on.** The corner-escape behavior exists for a reason. Do not disable it in production scripts.
- **Error handling at every subprocess call.** Check return codes. Log stderr. Never assume a subprocess succeeded because it returned.
- **Structured logging over print statements.** Automation scripts run in the background. print() gets lost. logging with file output does not.

### Common Mistakes

- **Passing raw LLM output between agents without validation.** This is the single most common source of cascading failures in multi-agent Python orchestration.
- **Monolithic orchestration scripts.** Everything in one file. Impossible to test, debug, or hand off to another agent or developer.
- **Hardcoded model strings throughout the codebase.** When the provider changes, the fix should be one line. If it is not, the model string is in the wrong place.
- **Desktop automation against dynamic interfaces.** PyAutoGUI relies on screen coordinates or UI element locations. If the interface layout changes, scripts break silently. Use image recognition (pyautogui.locateOnScreen) where possible instead of fixed coordinates.
- **No timeout on subprocess calls.** Long-running subprocesses without timeouts hang the entire orchestration chain.
- **Mixing orchestration and glue into a skill or hook script.** If a hook or skill is growing into a multi-step orchestration engine, it should become a proper Python module with its own structure — not a growing shell script.

---

## C&P Summary

This report covers how to correctly build the six resource types the team works with: Skills, Hooks, CLIs, MCPs, Plugins, and Python engines. Skills are markdown instruction files with YAML frontmatter that teach Claude how to do a specific task — the key is narrow scope, a clear description that acts as the trigger, and keeping instructions separate from reference material. Hooks are shell commands that fire automatically at lifecycle events in Claude Code; they are the team's only reliable enforcement layer, and exit codes are critical — exit 2 blocks, exit 1 does not. CLIs are the preferred integration layer before reaching for an MCP, and custom CLIs are worth building when a workflow will be called repeatedly and no existing tool covers it; the core principle is separating the CLI argument layer from the business logic. MCPs are the last resort in the build order — reached for only when a CLI cannot do the job — and the common mistakes are building them too early, making them too broad, and writing vague tool descriptions that Claude cannot use. Plugins are the packaging layer, not a feature layer; they bundle skills, hooks, MCPs, and agents into a distributable unit and are only justified when the package will be distributed or when multiple capabilities genuinely belong together. Python engines are the glue that holds the rest of the stack together — orchestrating workflows, managing file-based handoffs between agents, routing across LLMs via LiteLLM, and handling desktop automation; the cardinal rule is validating every handoff boundary between agents, because unvalidated LLM output passed to the next step is where multi-agent systems most commonly fail. One honest gap: Plugin documentation is newer and thinner than the rest; community patterns and failure mode knowledge for Plugins are less developed than for the other resource types, and that section may be worth a Feynman pass if Cosmo wants deeper methodology grounding there.

---

*Report complete. Sources consulted: Anthropic Claude Code Docs (code.claude.com), Model Context Protocol official docs (modelcontextprotocol.io), GitHub anthropics/claude-code repository, developer community resources (DEV Community, DataCamp, MCP Academy, multiple technical blogs). All information current as of 2026-05-04.*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
