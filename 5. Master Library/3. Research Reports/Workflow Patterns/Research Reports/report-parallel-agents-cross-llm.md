# Technical Reference: Parallel Agents, Agent Teams, and Cross-LLM Coordination

**Date Researched:** 2026-04-20 to 2026-04-21
**Researched by:** Rose
**Report Type:** Fact-Finding Reference — Architectural Guidance
**Section:** 6. Workflow Patterns

---

## Executive Summary

This is a comprehensive reference document covering parallel agent execution in Claude Code, Agent Teams architecture, cross-LLM coordination patterns, and desktop automation alternatives.

**Key findings:**
- Parallel Claude Code sessions are possible via isolated Git worktrees; upgrade decision should be based on usage ceiling, not feature availability
- Claude Code Agent Teams are experimental and disabled by default — architecture limits to Claude-only models
- Cross-LLM bridges work via Python (SDKs coexist, sequential or concurrent patterns); LiteLLM is the recommended abstraction layer
- Desktop automation (CoWork) is shelved; Python script layer with Pete is the recommended replacement
- Three unified surfaces (VS Code Extension, VS Code Terminal, Claude Desktop Code tab) run the same Claude Code engine — start and end in the same application per session

---

## 1. Claude Code Parallel Sessions — Architecture & Constraints

### What They Are

Parallel sessions are multiple simultaneous Claude Code agents executing in isolated Git worktrees. Each agent has its own isolated repository state with independent file modifications. Agents cannot directly see each other's context or conversational state.

### Technical Architecture

**Worktree Isolation:**
- Git worktrees provide filesystem isolation — each parallel agent session gets its own working directory tree
- File state (committed code, uncommitted changes) is independent per worktree
- Agents can commit to their own branches without affecting other agents' branches
- All agents share the same Git history and remote (GitHub) but work in separate physical directories

**Conversational Isolation:**
- Each parallel session is a separate conversation thread — no context sharing between sessions
- Agent 1's conversation context is not visible to Agent 2, even if working on the same project

**Rule:** Start and end in the same application per session. File state carries across applications; conversational context does not.

### What They Enable

- True parallel work: multiple agents tackle different tasks simultaneously without blocking
- Faster iteration on independent features or branches
- Risk isolation: one agent's changes don't affect another agent's stable branch
- Load distribution: heavy multi-step tasks split across agents instead of sequential execution

### What They Don't Enable

- Shared context: agents can't reference each other's in-conversation reasoning
- Direct communication: agents can't message each other mid-execution without a bridge layer
- Atomic coordination: if two agents modify the same file, merge conflicts require resolution

---

## 2. Claude Max Plan — Parallel Session Rate Limits

### Subscription Tiers

**Claude Max 5x ($100/month):**
- ~225 messages per 5-hour rolling window (empirically observed, not officially documented)
- Per-minute rate limits still apply on top of the window cap
- Real-world finding: heavy parallel use has burned through the cap in ~90 minutes

**Claude Max 20x ($200/month):**
- Same rolling window structure; exact cap scaling is undocumented
- Per-minute rate limits still apply

### Known Gaps (Undocumented as of April 2026)

- Whether the ~225-message window cap is per-agent or combined across all active parallel sessions
- Exact per-minute rate limits for Claude Max tiers (API tier limits are published; Max subscription limits are not)
- Whether Agent Teams peer-to-peer messaging counts against the window cap

### Upgrade Decision Rule

Do not upgrade to Max for parallel features until usage against the current tier ceiling consistently hits 80%+. Feature-chasing is not a valid trigger. Real bottleneck = message cap, not agent count.

---

## 3. Claude Code Agent Teams — Architecture & Status

### What It Is

Agent Teams is an experimental feature allowing multiple Claude Code agents to coordinate via a shared task list and peer-to-peer messaging. A team consists of one team lead (orchestrator) and multiple teammates.

### How It Differs from Subagents

| Factor | Subagents (Standard) | Agent Teams (Experimental) |
|--------|---------------------|--------------------------|
| Communication | Agent → parent only | Peer-to-peer mailbox + shared task list |
| Coordination | Parent manages all flow | Teammates self-coordinate with lead oversight |
| Context | Each agent isolated | Each agent isolated (same) |
| Token cost | Lower (summarized results) | Higher (linear scaling per agent) |
| Status | Available now | Experimental, disabled by default |

### Current Status

- **Experimental** — subject to breaking changes
- **Disabled by default** — requires explicit enable
- **No stability timeline** — Anthropic has not indicated when this moves to stable

### How to Enable

**Option 1: Environment Variable**
```bash
export CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=true
```

**Option 2: settings.json**
```json
{
  "experimental": {
    "agentTeams": true
  }
}
```

### Token Cost Warning

N agents = N independent context windows. Token cost scales linearly. 3 agents = roughly 3x cost. Test on low-stakes tasks only until Agent Teams reaches stable status. Do not depend on it for real project work.

---

## 4. Agent Teams — Model Restrictions

### Claude-Only — Architectural Constraint

Agent Teams is built on Claude's architecture. Non-Claude models cannot participate. This is not a temporary limitation.

**Available models in Agent Teams:** Opus 4.7, Opus 4.6, Sonnet 4.6, Haiku 4.5

**Cannot participate:** GPT (any version), Gemini, Grok, Kimi, or any non-Anthropic model.

The developer community has requested mixed-model support. As of April 2026, this is unimplemented with no announced timeline.

---

## 5. Subscription Realities — Multi-Tool Landscape

### ChatGPT Plus ($20/month)

- **What it is:** Consumer web interface access to ChatGPT
- **What it is NOT:** API access
- **Programmatic use:** Zero — no integration with Claude Code, Python scripts, or any custom workflow
- **For API access:** Requires a separate OpenAI Platform API account with per-token billing

### Claude Code — Unified Surfaces

Three surfaces run the same Claude Code engine with CLAUDE.md auto-loading:
1. VS Code Extension
2. VS Code Terminal
3. Claude Desktop Code tab

**Not synced:** Claude Desktop Chat tab (no CLAUDE.md auto-loading, workaround-only via MCP stack). Claude Web (personal use only).

---

## 6. Desktop Automation — CoWork Status

### Current Status

- **Windows support:** Released April 3, 2026
- **Feature maturity:** Research preview — experimental
- **Reliability on complex workflows:** ~50%
- **Security:** Known vulnerability shipped knowingly by Anthropic
- **No stability timeline announced**

### Why It's Shelved

Race conditions, timing issues, unexpected dialogs, Windows 11 UAC/DPI issues, and the security vulnerability collectively make CoWork unsuitable for production workflows. Revisit when reliability reaches 90%+ and the security issue is resolved.

### CoWork Generic Soul Shell

The Desktop-CoWork Agent generic soul shell remains in the Generic Soul Shells folder — still valid for AI-driven desktop use cases if those conditions are eventually met. It is not deleted. Pete's Python script layer is the default first approach going forward.

---

## 7. Pete's Python Script Layer — CoWork Revamp

### The Pattern

Pete (Python Specialist) writes deterministic automation scripts that handle the tasks CoWork was meant to handle. Scripts do the deterministic work; Claude Code agents handle decisions and error recovery.

```
Claude Agent: "Compile this and return the result"
    ↓
Pete's Script (deterministic):
    1. Execute compile step
    2. Read output
    3. Check for errors
    4. Return result + status to file
    ↓
Claude Agent (decision):
    Success → continue
    Error → analyze, retry, or escalate
```

### Libraries

**Primary: PyWinAuto (UIA backend)**
- Structural UI automation — finds elements by type/name, not pixel coordinates
- More reliable than image-based approaches for Windows apps
- Handles UAC-elevated windows with proper setup

**Supplement: PyDirectInput**
- DirectInput-level input (uses SendInput() Win32 function)
- Required for DirectX-dependent applications where PyWinAuto's structural access fails

**Avoid: PyAutoGUI**
- Unreliable on multi-monitor setups
- Blocks desktop during execution
- Image-based locators break on DPI scaling and theme changes

### Windows 11 Gotchas

- **UAC Elevation:** Script running non-elevated cannot control elevated apps — run script elevated or use COM interface
- **DPI Scaling:** Coordinates shift on 125%+ DPI monitors — use structural access (PyWinAuto) not pixel coordinates
- **Timing Races:** Fixed waits are fragile — use wait-loops with timeout instead
- **Theme Changes:** Dark/light mode switches break pixel-based automation — structural access is immune

### Reliability Expectations

- **Happy path (deterministic, well-defined):** 75–80% success rate
- **Unexpected scenarios (dialogs, errors, UI changes):** Rate drops significantly
- **Hybrid (recommended):** Pete's script handles the happy path; Claude agent wraps with error handling

---

## 8. LiteLLM — Recommended Cross-LLM Bridge Tool

### What It Is

LiteLLM is a Python library that provides a single, unified interface to 100+ LLM providers (Claude, GPT, Gemini, Grok, Kimi, etc.).

```python
from litellm import completion

# Claude
response = completion(model="claude-opus-4-20250514", messages=[...])

# Switch to GPT — one string change
response = completion(model="gpt-4o", messages=[...])

# Or Gemini
response = completion(model="gemini-2.0-flash", messages=[...])
```

### Key Advantages

1. **Single import** — no juggling 10 different SDKs
2. **Consistent error handling** — all provider errors map to same exception types
3. **Built-in retry logic** — configurable per provider
4. **Cost tracking** — automatic token counting across providers
5. **Drop-in migration** — switch providers by changing one string

### Rate Limits & Billing

- Rate limits: per-provider and independent
- Billing: per-provider; Claude API bills to Anthropic, GPT bills to OpenAI
- API Keys: separate accounts required per provider (`ANTHROPIC_API_KEY`, `OPENAI_API_KEY`, etc.)

### Important: ChatGPT Plus ≠ OpenAI API

ChatGPT Plus ($20/month) is a consumer interface — it does not include OpenAI API access. A separate OpenAI Platform API account and key is required for Pete to call GPT via LiteLLM.

### Status in This Project

LiteLLM is flagged in LHF for research and potential build during Agent Onboarding or first project that needs cross-LLM coordination. Pete is the intended owner. Soren clears before deployment.

---

## 9. Python as Cross-LLM Bridge — Patterns

### Both SDKs Coexist

`anthropic` and `openai` Python SDKs can be imported in the same script — no conflicts.

### Sequential Pattern

```python
from anthropic import Anthropic
from openai import OpenAI

claude = Anthropic()
openai = OpenAI()

# Step 1: Claude processes
claude_result = claude.messages.create(
    model="claude-opus-4-20250514",
    messages=[{"role": "user", "content": prompt}]
).content[0].text

# Step 2: GPT refines
gpt_result = openai.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": claude_result}]
).choices[0].message.content
```

### Concurrent Pattern (asyncio)

```python
import asyncio
from anthropic import AsyncAnthropic
from openai import AsyncOpenAI

async def call_both(prompt):
    claude = AsyncAnthropic()
    openai = AsyncOpenAI()
    
    results = await asyncio.gather(
        claude.messages.create(...),
        openai.chat.completions.create(...)
    )
    return results
```

**Or use LiteLLM** — recommended for anything more than a one-off test.

---

## 10. Claude Code ↔ Python Script Interface Patterns

### Pattern 1: File-Based JSON Handoff (Recommended)

Agent writes to file → Pete's script reads and processes → Pete writes result → Agent reads and continues.

- Auditable: file state is inspectable
- Decoupled: no subprocess management
- Recoverable: agent can check if file appeared and retry

### Pattern 2: Claude API Direct Call from Python

Pete's script calls Claude API directly (no Claude Code CLI). Simplest pattern. Requires separate API key and billing. Does not use Claude Code's orchestration or tools.

### Pattern 3: Subprocess JSON-Lines Pipe

High complexity. Pete spawns Claude Code CLI as subprocess, communicates via stdin/stdout JSON lines. Not recommended unless file-based handoff is structurally impossible.

---

## 11. Cross-LLM Orchestration Frameworks (Alternatives)

If native Claude Code coordination hits limits, these Python frameworks support multi-LLM agent teams. All are production-ready. None are native to Claude Code.

| Framework | Architecture | Best For |
|-----------|-------------|----------|
| **LangGraph** | Graph-based, explicit control flow | Complex branching, approval gates |
| **CrewAI** | Role-based crews | Multi-role task delegation |
| **AutoGen** (Microsoft) | Conversational group chat | Multi-turn reasoning, debate-style |

**A2A Protocol:** Google's Agent Development Kit (ADK) supports the A2A (Agent-to-Agent) protocol for cross-framework agent discovery. Early-stage adoption.

**Decision rule:** Build with Claude Code native agents first. Reach for these frameworks only if native coordination hits architectural limits.

---

## 12. Recommended Workflow Architecture

```
┌─────────────────────────────────────────────┐
│     LAYER 1: Agent Coordination             │
│     Claude Code subagents (now)             │
│     Agent Teams (when stable)               │
│     Sage orchestrates; agents report        │
└─────────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────┐
│     LAYER 2: Desktop Automation             │
│     Pete's Python scripts                   │
│     PyWinAuto + PyDirectInput               │
│     Deterministic happy path                │
│     Agents handle error recovery            │
└─────────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────┐
│     LAYER 3: Cross-LLM Calls               │
│     Pete's scripts via LiteLLM             │
│     Call Claude + GPT + any provider        │
│     File-based handoff to Claude agents     │
└─────────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────┐
│     LAYER 4: Session Architecture           │
│     Three unified surfaces                  │
│     CLAUDE.md auto-loads in all three       │
│     Start and end in same application       │
└─────────────────────────────────────────────┘
```

**Not every project uses every layer.** Workflow adapts to the project's needs.

### Decision Tree

| Situation | Solution |
|-----------|----------|
| Need desktop automation | Pete's Python script (PyWinAuto) first; CoWork if script can't do it |
| Need Claude + GPT in same workflow | Pete writes LiteLLM script |
| Need 5 agents in parallel | Claude Max 5x + isolated worktrees |
| Need agents to message each other | File-based messaging now; Agent Teams when stable |
| Need cross-framework orchestration | LangGraph / CrewAI / AutoGen (external dependency) |

---

## 13. Known Gaps — Undocumented as of April 2026

1. Whether the ~225-message window cap is per-agent or shared across all active sessions
2. Exact per-minute rate limits for Claude Max tiers
3. Whether Agent Teams peer messaging counts against the window cap
4. Agent Teams stability timeline — no announcement from Anthropic
5. CoWork production readiness timeline — no announcement

---

## C&P Summary

Parallel agents in Claude Code work via isolated Git worktrees — multiple agents execute simultaneously, each with independent file state and conversational context. Start and end in the same application per session; file state carries, conversation does not. Claude Max 5x ($100/month) supports up to 5 parallel agents with approximately 225 messages per 5-hour rolling window (real-world cap: ~90 minutes under heavy parallel load); upgrade when hitting the ceiling, not for the feature. Claude Code Agent Teams is experimental, disabled by default, and Claude-only — GPT, Gemini, Grok, and others cannot participate. Agent Teams enables direct peer-to-peer messaging between agents, but costs scale linearly with team size and stability is unknown — do not depend on it for production work. Cross-LLM coordination uses Python: LiteLLM is the recommended tool (unified SDK for 100+ providers via one interface), owned by Pete. ChatGPT Plus does not include OpenAI API access — a separate API account is required to call GPT from Pete's scripts. Desktop automation: CoWork is shelved (~50% reliability, known security vulnerability, no stability timeline). Replace with Pete's Python scripts (PyWinAuto primary, PyDirectInput for DirectX apps) combined with Claude agents for error recovery. Two items on the future watch list: (1) LiteLLM — flagged in LHF for research and build during Agent Onboarding; (2) Agent Teams — flagged in LHF for revisit when Anthropic marks it stable.

---

**Sources:**
- [Orchestrate teams of Claude Code sessions — Claude Code Docs](https://code.claude.com/docs/en/agent-teams)
- [Create custom subagents — Claude Code Docs](https://code.claude.com/docs/en/sub-agents)
- [Claude Max Plan — Anthropic](https://claude.com/pricing/max)
- [Claude Max Plan Complete Guide 2026 — claudelab.net](https://claudelab.net/en/articles/claude-ai/claude-max-plan-complete-guide-2026)
- [Claude Code Worktrees: Parallel Sessions Without Conflicts — claudefa.st](https://claudefa.st/blog/guide/development/worktree-guide)
- [How to Run Claude Code Agents in Parallel — Towards Data Science](https://towardsdatascience.com/how-to-run-claude-code-agents-in-parallel/)
- [Claude vs Cursor: Two Different Approaches — MindStudio](https://www.mindstudio.ai/blog/cursor-vs-claude-code)
- [ChatGPT Plus: API access — AIonX](https://aionx.co/chatgpt-reviews/chatgpt-plus-api-access/)
- [What is ChatGPT Plus — OpenAI Help Center](https://help.openai.com/en/articles/6950777-what-is-chatgpt-plus)
- [LiteLLM Documentation](https://docs.litellm.ai/docs/)
- [LiteLLM on GitHub](https://github.com/BerriAI/litellm)
- [PyWinAuto Documentation](https://pywinauto.readthedocs.io/en/latest/)
- [PyDirectInput on GitHub](https://github.com/learncodebygaming/pydirectinput)
- [Rate limits — Claude API Docs](https://platform.claude.com/docs/en/api/rate-limits)
- [Best Multi-Agent Frameworks in 2026 — gurusup.com](https://gurusup.com/blog/best-multi-agent-frameworks-2026)
- [LangGraph vs CrewAI vs AutoGen Guide 2026 — DEV Community](https://dev.to/pockit_tools/langgraph-vs-crewai-vs-autogen-the-complete-multi-agent-ai-orchestration-guide-for-2026-2d63)
- [From Tasks to Swarms: Agent Teams in Claude Code — alexop.dev](https://alexop.dev/posts/from-tasks-to-swarms-agent-teams-in-claude-code/)
- [Rate Limits Explained 2026 — SitePoint](https://www.sitepoint.com/claude-code-rate-limits-explained/)

---

*Last updated: 2026-04-21*
*Section: 6. Workflow Patterns — Research Reports*

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
